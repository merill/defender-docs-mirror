---
layout: Conceptual
title: Update IP address range - Data Enrichment API - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/api-data-enrichment-update
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
description: This article describes the update IP address range request in the Defender for Cloud Apps Data Enrichment API.
ms.date: 2023-01-29T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: 778de272-a2bb-cf1c-3464-b2d363c06659
document_version_independent_id: 778de272-a2bb-cf1c-3464-b2d363c06659
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/api-data-enrichment-update.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-data-enrichment-update
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/api-data-enrichment-update.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: a532e956-e4c4-c4cf-38a6-2a829a6c7138
---

# Update IP address range - Data Enrichment API - Microsoft Defender for Cloud Apps | Microsoft Learn

Run the POST request to update an existing IP address range.

Important

This endpoint isn't built for partial updates. All required parameters must be passed and any optional parameters will get an empty value if not passed.

## HTTP request

```rest
POST /api/v1/subnet/<ip_range_id>/update_rule/
```

## Request BODY parameters

| Parameter | Type | Description |
| --- | --- | --- |
| name | string | The unique name of the range |
| category | int | The ID of the range category. Providing a category helps you easily recognize activities from interesting IP addresses. Possible values include:**1**: Corporate**2**: Administrative**3**: Risky**4**: VPN**5**: Cloud provider**6**: Other |
| subnets | list | An array of masks as strings (IPv4 / IPv6) |
| organization (Optional) | string | The registered ISP |
| tags (Optional) | list | An array of new or existing objects including the tag name, ID, description, name template, and tenant ID |

## Example

### Request

Here's an example of the request.

```rest
curl -XPOST -H "Authorization:Token <your_token_key>" -H "Content-Type: application/json" "https://<tenant_id>.<tenant_region>.portal.cloudappsecurity.com/api/v1/subnet/<ip_range_id>/update_rule/" -d '{
  "name":"range name",
  "category":5,
  "organization":"Microsoft",
  "subnets":[
    "192.168.1.0/24",
    "192.168.2.0/16"
  ],
  "tags":[
    "existing tag"
  ]
}'
```

If you run into any problems, we're here to help. To get assistance or support for your product issue, please [open a support ticket](/en-us/defender-xdr/contact-defender-support).