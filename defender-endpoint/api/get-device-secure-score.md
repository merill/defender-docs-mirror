---
layout: Conceptual
title: Get the device secure score - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/get-device-secure-score
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Retrieves the organizational device secure score.
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
document_id: 1467c9f4-fff7-3d19-b7ea-2b61f2607cc9
document_version_independent_id: 1467c9f4-fff7-3d19-b7ea-2b61f2607cc9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/get-device-secure-score.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/get-device-secure-score
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/get-device-secure-score.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cd48b104-e308-4e08-a405-66f04a7df418
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ac23bdb5-c078-4620-8ee2-60eba45e97f8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 0b3bc258-d33d-112a-5089-7096519b5f4a
---

# Get the device secure score - Microsoft Defender for Endpoint | Microsoft Learn

Retrieves your [Microsoft Secure Score for Devices](/en-us/defender-vulnerability-management/tvm-microsoft-secure-score-devices). A higher Microsoft Secure Score for Devices means your endpoints are more resilient from cybersecurity threat attacks.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro) for details.

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Score.Read.All | 'Read Threat and Vulnerability Management score' |
| Delegated (work or school account) | Score.Read | 'Read Threat and Vulnerability Management score' |

## HTTP request

```http
GET /api/configurationScore
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |

## Request body

Empty

## Response

If successful, this method returns 200 OK, with the device secure score data in the response body.

## Example

### Request example

Here is an example of the request.

```http
GET https://api.security.microsoft.com/api/configurationScore
```

### Response example

Here's an example of the shortned response list.

```json
{
    "@odata.context": "https://api.security.microsoft.com/api/$metadata#ConfigurationScore/$entity",
    "time": "2019-12-03T09:15:58.1665846Z",
    "score": 340
}
```