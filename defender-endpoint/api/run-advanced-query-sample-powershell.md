---
layout: Conceptual
title: Advanced Hunting with PowerShell API Basics - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/run-advanced-query-sample-powershell
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: 
description: Learn the basics of querying the Microsoft Defender for Endpoint API, using PowerShell.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- must-keep
ms.topic: reference
ms.subservice: reference
ms.custom: api
ms.date: 2026-01-08T00:00:00.0000000Z
locale: en-us
document_id: 88ebb267-a2a8-b2d0-65eb-d5a11f13d055
document_version_independent_id: 88ebb267-a2a8-b2d0-65eb-d5a11f13d055
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/run-advanced-query-sample-powershell.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/run-advanced-query-sample-powershell
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/run-advanced-query-sample-powershell.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 6752d058-684b-24c7-0dca-312f7cb7fd23
---

# Advanced Hunting with PowerShell API Basics - Microsoft Defender for Endpoint | Microsoft Learn

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

Run advanced queries using PowerShell. For more information, see [Advanced Hunting API](run-advanced-query-api).

In this section, we share PowerShell samples to retrieve a token and use it to run a query.

## Before you begin

You first need to [create an app](apis-intro).

## Preparation instructions

- Open a PowerShell window.
- If your policy doesn't allow you to run the PowerShell commands, you can run the following command:

    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy Bypass
    ```

For more information, see [PowerShell documentation](/en-us/powershell/module/microsoft.powershell.security/set-executionpolicy).

## Get token

- Run the following:

```powershell
$tenantId = '00000000-0000-0000-0000-000000000000' # Paste your own tenant ID here
$appId = '11111111-1111-1111-1111-111111111111' # Paste your own app ID here
$appSecret = '22222222-2222-2222-2222-222222222222' # Paste your own app secret here

$resourceAppIdUri = 'https://api.securitycenter.microsoft.com'
$oAuthUri = "https://login.microsoftonline.com/$TenantId/oauth2/token"
$body = [Ordered] @{
    resource = "$resourceAppIdUri"
    client_id = "$appId"
    client_secret = "$appSecret"
    grant_type = 'client_credentials'
}
$response = Invoke-RestMethod -Method Post -Uri $oAuthUri -Body $body -ErrorAction Stop
$aadToken = $response.access_token
```

Where:

- $tenantId: ID of the tenant on behalf of which you want to run the query (that is, the query is run on the data of this tenant)
- $appId: ID of your Microsoft Entra app (the app must have 'Run advanced queries' permission to Defender for Endpoint)
- $appSecret: Secret of your Microsoft Entra app

## Run query

Run the following query:

```powershell
$token = $aadToken
$query = 'DeviceRegistryEvents | limit 10' # Paste your own query here

$url = "https://api.security.microsoft.com/api/advancedqueries/run"
$headers = @{
    'Content-Type' = 'application/json'
    Accept = 'application/json'
    Authorization = "Bearer $aadToken"
}
$body = ConvertTo-Json -InputObject @{ 'Query' = $query }
$webResponse = Invoke-WebRequest -Method Post -Uri $url -Headers $headers -Body $body -ErrorAction Stop
$response =  $webResponse | ConvertFrom-Json
$results = $response.Results
$schema = $response.Schema
```

- $results contain the results of your query
- $schema contains the schema of the results of your query

### Complex queries

If you want to run complex queries (or multilines queries), save your query in a file and, instead of the first line in the above sample, run the following command:

```powershell
$query = [IO.File]::ReadAllText("C:\myQuery.txt"); # Replace with the path to your file
```

## Work with query results

You can now use the query results.

To output the results of the query in CSV format in file file1.csv, run the following command:

```powershell
$results | ConvertTo-Csv -NoTypeInformation | Set-Content C:\file1.csv
```

To output the results of the query in JSON format in file file1.json, run the following command:

```powershell
$results | ConvertTo-Json | Set-Content file1.json
```