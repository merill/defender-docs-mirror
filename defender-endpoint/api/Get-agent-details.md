---
layout: Conceptual
title: Get scan agent by ID - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/get-agent-details
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use the "Get-Agent-Details" API.
keywords: apis, graph api, supported apis, agent details, definition
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
document_id: 084439ef-58c5-1435-c48f-3e685359689a
document_version_independent_id: 084439ef-58c5-1435-c48f-3e685359689a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/Get-agent-details.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/get-agent-details
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/Get-agent-details.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 46336e32-a809-b589-32f2-4855b5e34308
---

# Get scan agent by ID - Microsoft Defender for Endpoint | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## API description

Retrieves the details for a specified agent by its ID.

## Limitations

- Rate limitations for this API are 100 calls per minute and 1,500 calls per hour.

## Permissions

When obtaining a token using user credentials:

- To view data the user needs to have at least the following role permission: `ViewData` or `TvmViewData`. For more information, see: [Create and manage roles](../user-roles)

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro).

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Machine.Read.All | Read all scan information. |
| Delegated (work or school account) | Machine.Read.All | Read all scan information. |

## HTTP request

```http
GET /api/DeviceAuthenticatedScanAgents
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |

## Request body

Empty

## Response

If successful, this method returns 200 - OK response code with the details of the specified agent.

## Example request

Here's an example of the request.

```http
GET https://api.security.microsoft.com/api/DeviceAuthenticatedScanAgents/7f3d76a6976818553e996875dc91f55df6b26625
```

## Response example

```json
{
"@odata.context": "https://api.security.microsoft.com/api/$metadata#DeviceAuthenticatedScanAgents/$entity",
    "value": [
    {
    "id": "47df41a0c-asad-4fd6d3-bbea-a93dbc0bfcaa_4edd75b2407a5b64d704b4e53d74f15",
    "machineId": "4ejh675b240118fbehiuiy5b64d704b4e53d15",
    "lastSeen": "2022-05-08T12:18:41.538203Z",
    "computerDnsName": "TEST_DOMAIN",
    "AssignedApplicationId": "9E0FA0EB-0A51-4357-9C87-C21BFBE07571",
    "ScannerSoftwareVersion": "7.1.1",
    "LastCommandExecutionTimestamp": "2022-05-08T12:18:41.538203Z",
    "mdeClientVersion": "10.8295.22621.1195"
    },
   ]
}

```