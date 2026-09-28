---
layout: Conceptual
title: Import Indicators API - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/import-ti-indicators
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use the Import batch of Indicator API in Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- must-keep
ms.topic: reference
ms.custom: api
ms.subservice: reference
ms.date: 2025-12-11T00:00:00.0000000Z
locale: en-us
document_id: 8fcf82fb-257e-410f-f17c-4de50d2b8160
document_version_independent_id: 8fcf82fb-257e-410f-f17c-4de50d2b8160
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/import-ti-indicators.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/import-ti-indicators
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/import-ti-indicators.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86a4b315-a9f1-4577-b985-6fb0e0e67420
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/96ac410d-d052-4707-8007-df31dd0fe041
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: d0ff323a-3b5c-1b62-08e7-bddbea697b12
---

# Import Indicators API - Microsoft Defender for Endpoint | Microsoft Learn

## API description

Submits or Updates batch of [Indicator](ti-indicator) entities.

CIDR notation for IPs isn't supported.

## Limitations

- Rate limitations for this API are 30 calls per minute.
- There's a limit of 15,000 active [Indicators](ti-indicator) per tenant.
- Maximum batch size for one API call is 500.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Get started](apis-intro).

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Ti.ReadWrite.All | `Read and write All Indicators` |
| Delegated (work or school account) | Ti.ReadWrite | `Read and write Indicators` |

## HTTP request

```http
POST https://api.security.microsoft.com/api/indicators/import
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
| Indicators | List&lt;[Indicator](ti-indicator)&gt; | List of [Indicators](ti-indicator). **Required** |

## Response

- If successful, this method returns 200 - OK response code with a list of import results per indicator, see the following example.
- If not successful: this method return 400 - Bad Request. Bad request usually indicates incorrect body.

## Example

### Request example

Here's an example of the request.

```http
POST https://api.security.microsoft.com/api/indicators/import
```

```json
{
    "Indicators":
    [
        {
            "indicatorValue": "220e7d15b011d7fac48f2bd61114db1022197f7f",
            "indicatorType": "FileSha1",
            "title": "demo",
            "application": "demo-test",
            "expirationTime": "2021-12-12T00:00:00Z",
            "action": "Alert",
            "severity": "Informational",
            "description": "demo2",
            "recommendedActions": "nothing",
            "rbacGroupNames": ["group1", "group2"]
        },
        {
            "indicatorValue": "2233223322332233223322332233223322332233223322332233223322332222",
            "indicatorType": "FileSha256",
            "title": "demo2",
            "application": "demo-test2",
            "expirationTime": "2021-12-12T00:00:00Z",
            "action": "Alert",
            "severity": "Medium",
            "description": "demo2",
            "recommendedActions": "nothing",
            "rbacGroupNames": []
        }
    ]
}
```

### Response example

Here's an example of the response.

```json
{
    "value": [
        {
            "id": "2841",
            "indicator": "220e7d15b011d7fac48f2bd61114db1022197f7f",
            "isFailed": false,
            "failureReason": null
        },
        {
            "id": "2842",
            "indicator": "2233223322332233223322332233223322332233223322332233223322332222",
            "isFailed": false,
            "failureReason": null
        }
    ]
}
```