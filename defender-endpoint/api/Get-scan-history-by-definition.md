---
layout: Conceptual
title: Get scan history by definition - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/get-scan-history-by-definition
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use the get scan history by definition API
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
document_id: 4b7fbeeb-c1bb-376d-3940-aa8dbc906f71
document_version_independent_id: 4b7fbeeb-c1bb-376d-3940-aa8dbc906f71
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/Get-scan-history-by-definition.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/get-scan-history-by-definition
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/Get-scan-history-by-definition.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 97f0ff46-8307-eae4-6e2b-4112633d0a88
---

# Get scan history by definition - Microsoft Defender for Endpoint | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## API description

Retrieves a list of the scan history by definitions.

Supports [OData V4 queries](https://www.odata.org/documentation/). OData supported operators:

- `$top` with max value of 10,000.
- `$skip`

For an example of OData operation usage, see example $top request.

## Limitations

Rate limitations for this API are 100 calls per minute and 1,500 calls per hour.

## Permissions

When obtaining a token using user credentials, to view data, the user needs to have at least the following role permission: `ViewData` or `TvmViewData` . For more information, see: [Create and manage roles](../user-roles).

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro).

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Machine.Read.All | Read all scan information. |
| Delegated (work or school account) | Machine.Read.All | Read all scan information. |

## HTTP request

```http
POST api/DeviceAuthenticatedScanDefinitions/GetScanHistoryByScanDefinitionId
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |
| Content-Type | string | application/json. **Required**. |

## Request body

In the request body, supply a JSON object with the following parameters:

| Parameter | Type | Description |
| --- | --- | --- |
| ScanDefinitionIds | String | The scan Id. **Required**. |

## Response

If successful, this method returns 200 - OK response code with a list of the scan history by definition.

## Example request

Here's an example of the request.

```http
POST https://api.security.microsoft.com/api/DeviceAuthenticatedScanDefinitions/GetScanHistoryByScanDefinitionId
```

```json
{
    "ScanDefinitionIds": ["4ad8d463-6b3a-4894-b42a-a2de9ea0a8ae", "60c4aa57-c573-4488-8d18-230914792a92", "c6220f67-2cad-4ba3-a2fa-7ded6384da56"]
}
```

## Response example

```json
{
"@odata.context": "https://api.security.microsoft.com/api/DeviceAuthenticatedScanDefinitions/GetScanHistoryByScanDefinitionId",
    "value": [
    {
    "ScanDefinitionIds": "4ad8d463-6b3a-4894-b42a-a2de9ea0a8ae",
    "LastScanned": "2022-12-20T11:14:24.5561791Z",
    "ScanStatus": "Partial Success",
    "ScannerId": "625431694b7d2ca9d07e77ca1b029ef216bebb6d"
    },
    {
    "ScanDefinitionIds": "60c4aa57-c573-4488-8d18-230914792a92",
    "LastScanned": "2022-11-17T15:13:24.5561791Z",
    "ScanStatus": "Partial Success",
    "ScannerId": "625431694b7d2ca9d07e77ca1b029ef216bebb6d"
    },
    {
    "ScanDefinitionIds": "c6220f67-2cad-4ba3-a2fa-7ded6384da56",
    "LastScanned": "2022-11-10T18:15:24.5561791Z",
    "ScanStatus": "Partial Success",
    "ScannerId": "625431694b7d2ca9d07e77ca1b029ef216bebb6d"
    },
   ]
}
```

## Example $top request

Here's an example of a request that returns only 1 session.

```http
POST https://api.security.microsoft.com/api/DeviceAuthenticatedScanDefinitions/GetScanHistoryByScanDefinitionId?$top=1
```

## $top Response example

```json
{
"@odata.context": "https://api.security.microsoft.com/api/DeviceAuthenticatedScanDefinitions/GetScanHistoryByScanDefinitionId",
    "value": [
    {
    "ScanDefinitionIds": "4ad8d463-6b3a-4894-b42a-a2de9ea0a8ae",
    "LastScanned": "2022-12-20T11:14:24.5561791Z",
    "ScanStatus": "Partial Success",
    "ScannerId": "625431694b7d2ca9d07e77ca1b029ef216bebb6d"
    },
 ]
}
```