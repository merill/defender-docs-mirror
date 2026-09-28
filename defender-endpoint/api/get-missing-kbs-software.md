---
layout: Conceptual
title: Get missing KBs by software ID - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/get-missing-kbs-software
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Retrieves missing security updates by software ID
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
document_id: 7bc13c84-dfb2-bfc3-0360-e419641b2d5b
document_version_independent_id: 7bc13c84-dfb2-bfc3-0360-e419641b2d5b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/get-missing-kbs-software.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/get-missing-kbs-software
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/get-missing-kbs-software.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: d2863c5d-0af1-a742-1582-b3968c3f4f97
---

# Get missing KBs by software ID - Microsoft Defender for Endpoint | Microsoft Learn

Retrieves missing KBs (security updates) by software ID

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro) for details.

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Software.Read.All | 'Read Threat and Vulnerability Management Software information' |
| Delegated (work or school account) | Software.Read | 'Read Threat and Vulnerability Management Software information' |

## HTTP request

```http
GET /api/Software/{Id}/getmissingkbs
```

## Request header

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |

## Request body

Empty

## Response

If successful, this method returns 200 OK, with the specified software missing kb data in the body.

## Example

### Request

Here's an example of the request.

```http
GET https://api.security.microsoft.com/api/Software/microsoft-_-edge/getmissingkbs
```

### Response

Here's an example of the response.

```json
{
    "@odata.context": "https://api.security.microsoft.com/api/$metadata#Collection(microsoft.windowsDefenderATP.api.PublicProductFixDto)",
    "value": [
         {
            "id": "4540673",
            "name": "March 2020 Security Updates",
            "productsNames": [
                "edge"
            ],
            "url": "https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB4540673",
            "machineMissedOn": 240,
            "cveAddressed": 14
         },
         ...
        ]
}
```