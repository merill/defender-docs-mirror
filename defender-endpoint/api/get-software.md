---
layout: Conceptual
title: List software - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/get-software
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Retrieves a list of software inventory
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
document_id: 3116ca63-cba3-0f39-a782-7ccbc21f6e54
document_version_independent_id: 3116ca63-cba3-0f39-a782-7ccbc21f6e54
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/get-software.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/get-software
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/get-software.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 626589c7-30a2-451d-ee78-b495585d7461
---

# List software - Microsoft Defender for Endpoint | Microsoft Learn

## API description

Retrieves the organization software inventory.

Supports [OData V4 queries](https://www.odata.org/documentation/). OData supported operators:

- `$filter`on the following properties:
    - `id`
    - `name`
    - `vendor`
- `$top` with max value of 10,000.
- `$skip`

See examples at [OData queries with Microsoft Defender for Endpoint](exposed-apis-odata-samples).

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro) for details.

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Software.Read.All | 'Read Threat and Vulnerability Management Software information' |
| Delegated (work or school account) | Software.Read | 'Read Threat and Vulnerability Management Software information' |

## HTTP request

```http
GET /api/Software
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |

## Request body

Empty

## Response

If successful, this method returns 200 OK with the software inventory in the body.

## Example

### Request example

Here is an example of the request.

```http
GET https://api.security.microsoft.com/api/Software
```

### Response example

Here's an example of the response.

```json
{
    "@odata.context": "https://api.security.microsoft.com/api/$metadata#Software",
    "value": [
            {
                "id": "microsoft-_-edge",
                "name": "edge",
                "vendor": "microsoft",
                "weaknesses": 467,
                "publicExploit": true,
                "activeAlert": false,
                "exposedMachines": 172,
                "impactScore": 2.39947438
            }
            ...
        ]
}
```