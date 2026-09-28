---
layout: Conceptual
title: List all recommendations - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/get-all-recommendations
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Retrieves a list of all security recommendations affecting the organization.
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
ms.date: 2025-11-13T00:00:00.0000000Z
locale: en-us
document_id: 562950b3-b939-e40c-ea3e-7e7032ba0782
document_version_independent_id: 562950b3-b939-e40c-ea3e-7e7032ba0782
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/get-all-recommendations.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/get-all-recommendations
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/get-all-recommendations.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 3b9d7366-c4d2-897d-708e-a6c3fa0e5a0c
---

# List all recommendations - Microsoft Defender for Endpoint | Microsoft Learn

Retrieves a list of all security recommendations affecting the organization.

## API description

Returns information about all security recommendations affecting the organization.

*URL:* GET:/api/recommendations:

- Supports [OData V4 queries](https://www.odata.org/documentation/). OData supported operators:
    - `$filter`on the following properties:
        - `id`
        - `productName`
        - `vendor`
        - `recommendedVersion`
        - `recommendationCategory`
        - `subCategory`
        - `severityScore`
        - `remediationType`
        - `recommendedProgram`
        - `recommendedVendor`
        - `status`
    - `$top` with max value of 10,000.
    - `$skip`

See examples at [OData queries with Microsoft Defender for Endpoint](exposed-apis-odata-samples).

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro) for details.

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | SecurityRecommendation.Read.All | 'Read Threat and Vulnerability Management security recommendation information' |
| Delegated (work or school account) | SecurityRecommendation.Read | 'Read Threat and Vulnerability Management security recommendation information' |

## HTTP request

```http
GET /api/recommendations
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |

## Request body

Empty

## Response

If successful, this method returns 200 OK with the list of security recommendations in the body.

## Example

### Request

Here is an example of the request.

```http
GET https://api.security.microsoft.com/api/recommendations
```

### Response

Here is an example of the response.

```json
{
    "@odata.context": "https://api.security.microsoft.com/api/$metadata#Recommendations",
    "value": [
        {
            "id": "va-_-microsoft-_-edge_chromium-based",
            "productName": "edge_chromium-based",
            "recommendationName": "Update Microsoft Edge Chromium-based to version 127.0.2651.74",
            "weaknesses": 762,
            "vendor": "microsoft",
            "recommendedVersion": "127.0.2651.74",
            "recommendedVendor": "",
            "recommendedProgram": "",
            "recommendationCategory": "Application",
            "subCategory": "",
            "severityScore": 0,
            "publicExploit": true,
            "activeAlert": false,
            "associatedThreats": [
                "71d9120e-7eea-4058-889a-1a60bbf7e312"
            ],
            "remediationType": "Update",
            "status": "Active",
            "configScoreImpact": 0,
            "exposureImpact": 1.1744086343876479,
            "totalMachineCount": 261,
            "exposedMachinesCount": 193,
            "nonProductivityImpactedAssets": 0,
            "relatedComponent": "Edge Chromium-based",
            "hasUnpatchableCve": false,
            "tags": [
            "internetFacing"
            ],
            "exposedCriticalDevices": 116
        }
     ]
}
```