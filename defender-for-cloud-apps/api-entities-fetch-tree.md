---
layout: Conceptual
title: Fetch entity tree - Entities API - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/api-entities-fetch-tree
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
description: This article describes the fetch entity tree request in the Defender for Cloud Apps Entities API.
ms.date: 2023-01-29T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: 31597716-ae05-8784-a7ab-54170c3ec2e0
document_version_independent_id: 31597716-ae05-8784-a7ab-54170c3ec2e0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/api-entities-fetch-tree.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-entities-fetch-tree
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/api-entities-fetch-tree.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 90815f27-9c34-4396-7205-42430c5e3eb5
---

# Fetch entity tree - Entities API - Microsoft Defender for Cloud Apps | Microsoft Learn

Note

This request is not available for Microsoft 365 Cloud App Security.

Run the GET request to fetch all entities related to the entity matching the specified primary key. If the entity is a user, fetches all accounts associated with the user. If the entity is an account, fetches the entity's parent and siblings.

## HTTP request

```rest
GET /api/v1/entities/<pk>/retrieve_tree/
```

## Request URL parameters

| Parameter | Description |
| --- | --- |
| pk | The ID of the entity |

## Example

### Request

Here is an example of the request.

```rest
curl -XGET -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.portal.cloudappsecurity.com/api/v1/entities/<pk>/retrieve_tree/"
```

### Response

Returns the specified entity tree in JSON format.

```json
{
  // entity tree record
}
```

If you run into any problems, we're here to help. To get assistance or support for your product issue, please [open a support ticket](/en-us/defender-xdr/contact-defender-support).