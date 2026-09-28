---
layout: Conceptual
title: List Indicators API - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/get-ti-indicators-collection
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use the List Indicators API to retrieve a collection of all active Indicators in Microsoft Defender for Endpoint.
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
ms.date: 2025-12-11T00:00:00.0000000Z
locale: en-us
document_id: 87bf5c63-ed06-13f6-bab7-55177af631b1
document_version_independent_id: 87bf5c63-ed06-13f6-bab7-55177af631b1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/get-ti-indicators-collection.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/get-ti-indicators-collection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/get-ti-indicators-collection.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: a03db079-d73a-6144-d7e6-0a804b69420d
---

# List Indicators API - Microsoft Defender for Endpoint | Microsoft Learn

## API description

Retrieves a collection of all active [Indicators](ti-indicator).

Supports [OData V4 queries](https://www.odata.org/documentation/). OData supported operators:

- `$filter` on the following operators: `application`
    - `createdByDisplayName`
    - `expirationTime`
    - `generateAlert`
    - `title`
    - `rbacGroupNames`
    - `rbacGroupIds`
    - `indicatorValue`
    - `indicatorType`
    - `creationTimeDateTimeUtc`
    - `createdBy`
    - `action`
    - `severity`
- `$top` with max value of 10,000.
- `$skip`

See examples at [OData queries with Microsoft Defender for Endpoint](exposed-apis-odata-samples).

## Limitations

Rate limitations for this API are 100 calls per minute and 1,500 calls per hour.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Get started](apis-intro).

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Ti.ReadWrite | `Read and write Indicators` |
| Application | Ti.ReadWrite.All | `Read and write All Indicators` |
| Delegated (work or school account) | Ti.ReadWrite | `Read and write Indicators` |

## HTTP request

```http
GET https://api.security.microsoft.com/api/indicators
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |

## Request body

Empty

## Response

If successful, this method returns 200, Ok response code with a collection of [Indicator](ti-indicator) entities.

If the Application has `Ti.ReadWrite.All` permission, it will be exposed to all Indicators. Otherwise, it will be exposed only to the Indicators it created.

## Example 1

### Example 1 request

Here's an example of a request that gets all indicators.

```http
GET https://api.security.microsoft.com/api/indicators
```

### Example 1 response

Here's an example of the response.

```json
HTTP/1.1 200 Ok
Content-type: application/json
{
    "@odata.context": "https://api.security.microsoft.com/api/$metadata#Indicators",
    "value": [
        {
            "id": "995",
            "indicatorValue": "12.13.14.15",
            "indicatorType": "IpAddress",
            "action": "Alert",
            "application": "demo-test",
            "source": "TestPrdApp",
            "sourceType": "AadApp",
            "title": "test",
            "creationTimeDateTimeUtc": "2018-10-24T11:15:35.3688259Z",
            "createdBy": "45097602-1234-5678-1234-9f453233e62c",
            "expirationTime": "2020-12-12T00:00:00Z",
            "lastUpdateTime": "2019-10-24T10:54:23.2009016Z",
            "lastUpdatedBy": TestPrdApp,
            "severity": "Informational",
            "description": "test",
            "recommendedActions": "test",
            "rbacGroupNames": []
        },
        {
            "id": "996",
            "indicatorValue": "220e7d15b0b3d7fac48f2bd61114db1022197f7f",
            "indicatorType": "FileSha1",
            "action": "AlertAndBlock",
            "application": null,
            "source": "TestPrdApp",
            "sourceType": "AadApp",
            "title": "test",
            "creationTimeDateTimeUtc": "2018-10-24T10:54:23.2009016Z",
            "createdBy": "45097602-1234-5678-1234-9f453233e62c",
            "expirationTime": "2020-12-12T00:00:00Z",
            "lastUpdateTime": "2019-10-24T10:54:23.2009016Z",
            "lastUpdatedBy": TestPrdApp,
            "severity": "Informational",
            "description": "test",
            "recommendedActions": "TEST",
            "rbacGroupNames": [ "Group1", "Group2" ]
        }
        ...
    ]
}
```

## Example 2

### Example 2 request

Here's an example of a request that gets all Indicators with `AlertAndBlock` action.

```http
GET https://api.security.microsoft.com/api/indicators?$filter=action+eq+'AlertAndBlock'
```

### Example 2 response

Here's an example of the response.

```json
HTTP/1.1 200 Ok
Content-type: application/json
{
    "@odata.context": "https://api.security.microsoft.com/api/$metadata#Indicators",
    "value": [
        {
            "id": "997",
            "indicatorValue": "111e7d15b0b3d7fac48f2bd61114db1022197f7f",
            "indicatorType": "FileSha1",
            "action": "AlertAndBlock",
            "application": null,
            "source": "TestPrdApp",
            "sourceType": "AadApp",
            "title": "test",
            "creationTimeDateTimeUtc": "2018-10-24T10:54:23.2009016Z",
            "createdBy": "45097602-1234-5678-1234-9f453233e62c",
            "expirationTime": "2020-12-12T00:00:00Z",
            "lastUpdateTime": "2019-10-24T10:54:23.2009016Z",
            "lastUpdatedBy": TestPrdApp,
            "severity": "Informational",
            "description": "test",
            "recommendedActions": "TEST",
            "rbacGroupNames": [ "Group1", "Group2" ]
        }
        ...
    ]
}
```