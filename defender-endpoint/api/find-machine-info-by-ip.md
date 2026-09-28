---
layout: Conceptual
title: Find device information by internal IP API - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/find-machine-info-by-ip
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use this API to create calls related to finding a device entry around a specific timestamp by internal IP.
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
document_id: e923139a-d873-d2e1-92aa-4e23dc896940
document_version_independent_id: e923139a-d873-d2e1-92aa-4e23dc896940
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/find-machine-info-by-ip.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/find-machine-info-by-ip
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/find-machine-info-by-ip.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: b8a1ecf1-43ae-e447-70ff-cd8478a4b4a1
---

# Find device information by internal IP API - Microsoft Defender for Endpoint | Microsoft Learn

Find a device by internal IP.

The timestamp must be within the last 30 days.

## Permissions

The following permission is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro)

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Machine.ReadWrite.All | 'Read and write all machine information' |

## HTTP request

```http
GET /api/machines/find(timestamp={time},key={IP})
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |

## Request body

Empty

## Response

If successful and machine exists - 200 OK. If no machine found - 404 Not Found.

## Example

### Request example

Here's an example of the request.

```http
GET https://graph.microsoft.com/testwdatppreview/machines/find(timestamp=2018-06-19T10:00:00Z,key='10.166.93.61')
Content-type: application/json
```

### Response example

Here's an example of the response.

The response will return a list of all devices that reported this IP address within 16 minutes prior and after the timestamp.

```json
HTTP/1.1 200 OK
Content-type: application/json
{
    "@odata.context": "https://graph.microsoft.com/testwdatppreview/$metadata#Machines",
    "value": [
        {
            "id": "04c99d46599f078f1c3da3783cf5b95f01ac61bb",
            "computerDnsName": "",
            "firstSeen": "2017-07-06T01:25:04.9480498Z",
            "osPlatform": "Windows10",
...
}
```