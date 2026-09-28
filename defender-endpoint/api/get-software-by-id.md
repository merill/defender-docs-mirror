---
layout: Conceptual
title: Get software by ID - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/get-software-by-id
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Retrieves a list of software details by ID.
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
ms.date: 2025-11-16T00:00:00.0000000Z
locale: en-us
document_id: 71f54498-1337-4467-0a69-29a9b61294b0
document_version_independent_id: 71f54498-1337-4467-0a69-29a9b61294b0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/get-software-by-id.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/get-software-by-id
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/get-software-by-id.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: f6a0754e-37b6-3c6b-70bd-aa713cd98816
---

# Get software by ID - Microsoft Defender for Endpoint | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

Retrieves software details by ID.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro) for details.

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Software.Read.All | 'Read Threat and Vulnerability Management Software information' |
| Delegated (work or school account) | Software.Read | 'Read Threat and Vulnerability Management Software information' |

## HTTP request

```http
GET /api/Software/{Id}
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}.**Required**. |

## Request body

Empty

## Response

If successful, this method returns 200 OK with the specified software data in the body.

## Example

### Request example

Here's an example of the request.

```http
GET https://api.security.microsoft.com/api/Software/microsoft-_-edge
```

### Response example

Here's an example of the response.

```json
{
    "@odata.context": "https://api.security.microsoft.com/api/$metadata#Software/$entity",
    "id": "microsoft-_-edge",
    "name": "edge",
    "vendor": "microsoft",
    "weaknesses": 467,
    "publicExploit": true,
    "activeAlert": false,
    "exposedMachines": 172,
    "impactScore": 2.39947438
}
```