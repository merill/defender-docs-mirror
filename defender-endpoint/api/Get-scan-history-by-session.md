---
layout: Conceptual
title: Get scan history by session - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/get-scan-history-by-session
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use the get scan history by session api.
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
ms.date: 2025-11-10T00:00:00.0000000Z
locale: en-us
document_id: ebb7f9d6-2de0-8114-8d82-930c2afbfd01
document_version_independent_id: ebb7f9d6-2de0-8114-8d82-930c2afbfd01
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/Get-scan-history-by-session.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/get-scan-history-by-session
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/Get-scan-history-by-session.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 599d59b7-0466-078e-7ef1-ad60bcee6379
---

# Get scan history by session - Microsoft Defender for Endpoint | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## API description

Retrieves a list of the scan history by session.

## Limitations

Rate limitations for this API are 100 calls per minute and 1,500 calls per hour.

## Permissions

When obtaining a token using user credentials:

- To view data the user needs to have at least the following role permission: `ViewData` or `TvmViewData`. For more information, see [Create and manage roles](../user-roles).
- One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro).

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Machine.Read.All | Read all scan information. |
| Delegated (work or school account) | Machine.Read.All | Read all scan information. |

## HTTP request

```http
POST /api/DeviceAuthenticatedScanDefinitions/GetScanHistoryBySessionId
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | string | Bearer {token}. **Required**. |
| Content-Type | string | application/json. **Required**. |

## Request body

In the request body, supply a JSON object with the following parameters:

| Parameter | Type | Description |
| --- | --- | --- |
| SessionIds | String | The session Id. **Required**. |

## Response

If successful, this method returns 200 - OK response code with a list of the scan history for a session.

## Example request

Here's an example of the request.

```http
POST https://api.security.microsoft.com/api/DeviceAuthenticatedScanDefinitions/GetScanHistoryBySessionId
```

```json
{
    "SessionIds": ["01decc497f4b4ec49a5fc4e12597f8c8"]
}
```

## Response example

```json
{
 "@odata.context": "https://api.security.microsoft.com/api/DeviceAuthenticatedScanDefinitions/GetScanHistoryBySessionId",
    "value": [
    {
     "orgId": "asdf781a0c-792d-46d3-bbea-a93dbc0bfcaa",
     "ScanDefinitionIds": "4ad8d463-6b3a-4894-b42a-a2de9ea0a8ae",
     "SessionIds": "01decc497f4b4ec49a5fc4e12597f8c8",
     "NumberOfSuccessfullyScannedTargets": 3,
     "NumberOfTargets": 3,
     "ScanStatus": "Success",
     "LastScanned": "2022-12-19T15:14:24.5561791Z",
     "ListScannedTargets": {
         "Ip": "127.0.0.1",
         "Hostname": "DESKTOP-Test",
         "ScannedDeviceDescription": "Network device",
         "ErrorMessage": "",
         "ScanStatus": "Success",
         "ScanDuration": "00:08:30",
        },
        {
         "Ip": "127.0.0.2",
         "Hostname": "DESKTOP-Test2",
         "ScannedDeviceDescription": "Network device 2",
         "ErrorMessage": "",
         "ScanStatus": "Success",
         "ScanDuration": "00:08:00",
        },
{
         "Ip": "127.0.0.3",
         "Hostname": "DESKTOP-Test3",
         "ScannedDeviceDescription": "Network device 3",
         "ErrorMessage": "",
         "ScanStatus": "Success",
         "ScanDuration": "00:08:50",
        },
    }
  ]
}
```