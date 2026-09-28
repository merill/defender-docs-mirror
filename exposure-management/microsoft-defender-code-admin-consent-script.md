---
layout: Conceptual
title: Microsoft Defender Code admin consent script - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/microsoft-defender-code-admin-consent-script
author: DebLanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Reference script for granting admin consent for Microsoft Defender Code CLI authentication.
ms.topic: reference
ms.date: 2026-07-08T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 5b5f3e6a-394c-5e0d-fd69-5025ef5ec04d
document_version_independent_id: 5b5f3e6a-394c-5e0d-fd69-5025ef5ec04d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/microsoft-defender-code-admin-consent-script.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: microsoft-defender-code-admin-consent-script
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/microsoft-defender-code-admin-consent-script.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: eda9e802-fd44-7592-9f10-ec32ffbef07f
---

# Microsoft Defender Code admin consent script - Microsoft Security Exposure Management | Microsoft Learn

Use this script to grant tenant-wide admin consent for the Microsoft Azure CLI client to call the Microsoft Defender Code first-party app with the `Defender.InteractiveLogin` delegated scope.

Copy the script and save it as `Grant-DefenderAdminConsent.ps1`:

```powershell
[CmdletBinding()]
param(
    [Parameter(Mandatory = $true, Position = 0)]
    [ValidatePattern('^[0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{4}-[0-9a-fA-F]{12}$')]
    [string]$TenantId,

    [switch]$VerifyToken
)

$ErrorActionPreference = 'Stop'

# Constants
$FpaAppId   = 'c2fd607e-fe6e-41bd-ae58-08e2f24014aa'  # Microsoft Defender Code
$CliAppId   = '04b07795-8ddb-461a-bbee-02f9e1bf7b46'
$ScopeValue = 'Defender.InteractiveLogin'

function Invoke-AzCli {
    param([Parameter(Mandatory)][string[]]$Arguments)
    $out = & az @Arguments 2>&1
    if ($LASTEXITCODE -ne 0) {
        throw "az $($Arguments -join ' ') failed:`n$out"
    }
    return $out
}

function Get-OrCreateServicePrincipal {
    param([Parameter(Mandatory)][string]$AppId)

    $filter = "appId eq '$AppId'"
    $url    = "https://graph.microsoft.com/v1.0/servicePrincipals?`$filter=$filter&`$select=id,appId,displayName"
    $resp   = Invoke-AzCli -Arguments @('rest','--method','GET','--url',$url) | Out-String | ConvertFrom-Json

    if ($resp.value -and $resp.value.Count -gt 0) {
        return $resp.value[0]
    }

    Write-Host "Service principal for appId $AppId not found in tenant -- creating..." -ForegroundColor Yellow
    $bodyFile = New-TemporaryFile
    try {
        Set-Content -Path $bodyFile -Value ('{"appId":"' + $AppId + '"}') -NoNewline -Encoding utf8
        $created = Invoke-AzCli -Arguments @(
            'rest','--method','POST',
            '--url','https://graph.microsoft.com/v1.0/servicePrincipals',
            '--headers','Content-Type=application/json',
            '--body',"@$bodyFile"
        ) | Out-String | ConvertFrom-Json
        return $created
    }
    finally {
        Remove-Item $bodyFile -ErrorAction SilentlyContinue
    }
}

Write-Host "==> az login to tenant $TenantId" -ForegroundColor Cyan
& az login --tenant $TenantId --use-device-code --allow-no-subscriptions | Out-Host
if ($LASTEXITCODE -ne 0) { throw "az login failed (exit $LASTEXITCODE)" }

Write-Host "==> Resolving service principals" -ForegroundColor Cyan
$fpaSp = Get-OrCreateServicePrincipal -AppId $FpaAppId
$cliSp = Get-OrCreateServicePrincipal -AppId $CliAppId
Write-Host "    FPA SP: $($fpaSp.id) ($($fpaSp.displayName))"
Write-Host "    CLI SP: $($cliSp.id) ($($cliSp.displayName))"

Write-Host "==> Checking for existing oauth2PermissionGrant" -ForegroundColor Cyan
$existing = Invoke-AzCli -Arguments @(
    'rest','--method','GET',
    '--url',"https://graph.microsoft.com/v1.0/oauth2PermissionGrants?`$filter=clientId eq '$($cliSp.id)' and resourceId eq '$($fpaSp.id)' and consentType eq 'AllPrincipals'"
) | Out-String | ConvertFrom-Json

$match = $existing.value | Where-Object { ($_.scope -split '\s+') -contains $ScopeValue }
if ($match) {
    Write-Host "    Grant already exists (id $($match.id)). Skipping create." -ForegroundColor Green
    $grant = $match
}
else {
    Write-Host "==> Creating tenant-wide admin consent grant ($ScopeValue)" -ForegroundColor Cyan
    $bodyFile = New-TemporaryFile
    try {
        $body = @{
            clientId    = $cliSp.id
            consentType = 'AllPrincipals'
            resourceId  = $fpaSp.id
            scope       = $ScopeValue
        } | ConvertTo-Json -Compress
        Set-Content -Path $bodyFile -Value $body -NoNewline -Encoding utf8
        $grant = Invoke-AzCli -Arguments @(
            'rest','--method','POST',
            '--url','https://graph.microsoft.com/v1.0/oauth2PermissionGrants',
            '--headers','Content-Type=application/json',
            '--body',"@$bodyFile"
        ) | Out-String | ConvertFrom-Json
    }
    finally {
        Remove-Item $bodyFile -ErrorAction SilentlyContinue
    }
    Write-Host "    Grant id: $($grant.id)" -ForegroundColor Green
}

if ($VerifyToken) {
    Write-Host "==> Acquiring verification token" -ForegroundColor Cyan
    $tok = Invoke-AzCli -Arguments @(
        'account','get-access-token',
        '--tenant',$TenantId,
        '--scope',"$FpaAppId/$ScopeValue",
        '--query','accessToken','-o','tsv'
    ) | Out-String
    $tok = $tok.Trim()
    Write-Host "    Token acquired." -ForegroundColor Green
}

Write-Host "`nDone." -ForegroundColor Green
```