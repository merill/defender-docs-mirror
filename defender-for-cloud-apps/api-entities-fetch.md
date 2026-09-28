---
layout: Conceptual
title: Fetch - Entities API - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/api-entities-fetch
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: This article describes the fetch request in the Defender for Cloud Apps Entities API.
ms.date: 2023-01-29T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: 37f130b6-a455-a6d9-093b-ded5f5ff22c1
document_version_independent_id: 37f130b6-a455-a6d9-093b-ded5f5ff22c1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/api-entities-fetch.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-entities-fetch
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/api-entities-fetch.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: b55185d7-735d-73d4-f2ed-2436a0722684
---

# Fetch - Entities API - Microsoft Defender for Cloud Apps | Microsoft Learn

Note

This request is not available for Microsoft 365 Cloud App Security.

Run the GET request to fetch the entity matching the specified primary key.

## HTTP request

```rest
GET /api/v1/entities/<pk>/
```

## Request URL parameters

| Parameter | Description |
| --- | --- |
| pk | A dictionary with the entity ID, SaaS, and instance details encoded as a base64 string. For example: `{"id":"00aa00aa-bb11-cc22-dd33-44ee44ee44ee","saas":11161,"inst":0}` encoded as a base64 string. |

## Example

### Request

Here's an example of the request.

```rest
curl -XPOST -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.portal.cloudappsecurity.com/api/v1/entities/<pk>/"
```

### Response

Returns the specified entity in JSON format.

```json
{
  // entity record
}
```

If you run into any problems, we're here to help. To get assistance or support for your product issue, please [open a support ticket](/en-us/defender-xdr/contact-defender-support).