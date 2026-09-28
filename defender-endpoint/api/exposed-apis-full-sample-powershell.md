---
layout: Conceptual
title: Advanced Hunting with PowerShell API Guide - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/exposed-apis-full-sample-powershell
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: 
description: Use these code samples, querying several Microsoft Defender for Endpoint APIs.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- must-keep
ms.topic: reference
ms.date: 2025-03-21T00:00:00.0000000Z
ms.subservice: reference
ms.custom: api
locale: en-us
document_id: cfecd2e7-3777-0814-7d1d-b2c9ed4ee933
document_version_independent_id: cfecd2e7-3777-0814-7d1d-b2c9ed4ee933
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/exposed-apis-full-sample-powershell.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/exposed-apis-full-sample-powershell
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/exposed-apis-full-sample-powershell.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 9deec812-278b-b9b5-7419-07a983a0ce99
---

# Advanced Hunting with PowerShell API Guide - Microsoft Defender for Endpoint | Microsoft Learn

Important

Advanced hunting capabilities aren't included in Microsoft Defender for Business.

Note

If you're a US Government customer, use the URIs listed in [Microsoft Defender for Endpoint for US Government customers](/en-us/defender-endpoint/gov#api).

Tip

For better performance, instead of using api.security.microsoft.com, use a server closer to your geolocation:

- us.api.security.microsoft.com
- eu.api.security.microsoft.com
- uk.api.security.microsoft.com
- au.api.security.microsoft.com
- swa.api.security.microsoft.com
- ina.api.security.microsoft.com
- aea.api.security.microsoft.com

Full scenario using multiple APIs from Microsoft Defender for Endpoint.

In this section, we share PowerShell samples to:

- Retrieve a token.
- Use token to retrieve the latest alerts in Microsoft Defender for Endpoint.
- For each alert, if the alert has medium or high priority and is still in progress, check how many times the device has connected to suspicious URL.

**Prerequisite**: You first need to [create an app](apis-intro).

## Preparation instructions

1. Open a PowerShell window.
2. If your policy doesn't allow you to run the PowerShell commands, you can run the following command:

    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy Bypass
    ```

For more information, see [PowerShell documentation](/en-us/powershell/module/microsoft.powershell.security/set-executionpolicy).

## Get token

Run the following command, using your information as follows:

- `$tenantId`: ID of the tenant on behalf of which you want to run the query (that is, the query is run on the data of this tenant).
- `$appId`: ID of your Microsoft Entra app (the app must have 'Run advanced queries' permission to Defender for Endpoint).
- `$appSecret`: Secret of your Microsoft Entra app.
- `$suspiciousUrl`: The URL.

Tip

Some Microsoft Defender for Endpoint APIs continue to require access tokens issued for the legacy resource `https://api.securitycenter.microsoft.com`. If the token audience doesn't match the resource expected by the API, requests fail with `403 Forbidden`, even if the API endpoint uses `https://api.security.microsoft.com`. Use `https://api.securitycenter.microsoft.com` as the resource or scope when acquiring tokens.

```powershell
$tenantId = '00000000-0000-0000-0000-000000000000' # Paste your own tenant ID here
$appId = '11111111-1111-1111-1111-111111111111' # Paste your own app ID here
$appSecret = '22222222-2222-2222-2222-222222222222' # Paste your own app secret here
$suspiciousUrl = 'www.suspiciousUrl.com' # Paste your own URL here

$resourceAppIdUri = 'https://api.securitycenter.microsoft.com'
$oAuthUri = "https://login.microsoftonline.com/$TenantId/oauth2/token"
$authBody = [Ordered] @{
    resource = "$resourceAppIdUri"
    client_id = "$appId"
    client_secret = "$appSecret"
    grant_type = 'client_credentials'
}
$authResponse = Invoke-RestMethod -Method Post -Uri $oAuthUri -Body $authBody -ErrorAction Stop
$aadToken = $authResponse.access_token

#Get latest alert
$alertUrl = "https://api.security.microsoft.com/api/alerts?`$top=10"
$headers = @{
    'Content-Type' = 'application/json'
    Accept = 'application/json'
    Authorization = "Bearer $aadToken"
}
$alertResponse = Invoke-WebRequest -Method Get -Uri $alertUrl -Headers $headers -ErrorAction Stop
$alerts =  ($alertResponse | ConvertFrom-Json).value

$machinesToInvestigate = New-Object System.Collections.ArrayList

Foreach($alert in $alerts)
{
    #echo $alert.id $alert.machineId    $alert.severity $alert.status

    $isSevereAlert = $alert.severity -in 'Medium', 'High'
    $isOpenAlert = $alert.status -in 'InProgress', 'New'
    if($isOpenAlert -and $isSevereAlert)
    {
        if (-not $machinesToInvestigate.Contains($alert.machineId))
        {
            $machinesToInvestigate.Add($alert.machineId) > $null
        }
    }
}

$commaSeparatedMachines = '"{0}"' -f ($machinesToInvestigate -join '","')

$query = "NetworkCommunicationEvents
| where MachineId in ($commaSeparatedMachines)
| where RemoteUrl  == `"$suspiciousUrl`"
| summarize ConnectionsCount = count() by MachineId"

$queryUrl = "https://api.security.microsoft.com/api/advancedqueries/run"

$queryBody = ConvertTo-Json -InputObject @{ 'Query' = $query }
$queryResponse = Invoke-WebRequest -Method Post -Uri $queryUrl -Headers $headers -Body $queryBody -ErrorAction Stop
$response =  ($queryResponse | ConvertFrom-Json).Results
$response
```