---
layout: Conceptual
title: Delete IP address range - Data Enrichment API - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/api-data-enrichment-delete
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
description: This article describes the delete IP address range request in the Defender for Cloud Apps Data Enrichment API.
ms.date: 2023-01-29T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: 4ba6de05-c320-77a5-c268-e279f13413d6
document_version_independent_id: 4ba6de05-c320-77a5-c268-e279f13413d6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/api-data-enrichment-delete.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-data-enrichment-delete
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/api-data-enrichment-delete.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 518bcc18-11b0-2334-bd7f-498b98d18766
---

# Delete IP address range - Data Enrichment API - Microsoft Defender for Cloud Apps | Microsoft Learn

Run the DELETE request to delete an IP address range.

## HTTP request

```rest
DELETE /api/v1/subnet/<ip_range_id>/
```

## Example

### Request

Here's an example of the request.

```rest
curl -X DELETE -H "Authorization:Token <your_token_key>" "https://<tenant_id>.<tenant_region>.portal.cloudappsecurity.com/api/v1/subnet/<ip_range_id>/"
```

If you run into any problems, we're here to help. To get assistance or support for your product issue, please [open a support ticket](/en-us/defender-xdr/contact-defender-support).