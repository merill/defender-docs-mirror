---
layout: Conceptual
title: List - Files API - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/api-files-list
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
description: This article describes the list request in the Defender for Cloud Apps Files API.
ms.date: 2023-01-29T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: e2192faa-5092-a5b3-1bdf-fdf3cabbcd90
document_version_independent_id: e2192faa-5092-a5b3-1bdf-fdf3cabbcd90
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/api-files-list.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-files-list
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/api-files-list.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: b19c6989-b495-f155-e8ab-11b5c670cb28
---

# List - Files API - Microsoft Defender for Cloud Apps | Microsoft Learn

Note

- This API is not available for Microsoft 365 Cloud App Security.
- This endpoint might time out when filtering and paginating large collections.

Run the GET or POST request to fetch a list of files matching the specified filters.

## HTTP request

```rest
GET /api/v1/files/
```

```rest
POST /api/v1/files/
```

## Request BODY parameters

| Parameter | Description |
| --- | --- |
| filters | Filter objects with all the search filters for the request, for more details see [file filters](api-files#filters) |
| skip | Skips the specified number of records |
| limit | Maximum number of records returned by the request |

## Example

### Request

Here's an example of the request.

```rest
curl -XPOST -H "Authorization:Token <your_token_key>" -H "Content-Type: application/json" "https://<tenant_id>.<tenant_region>.portal.cloudappsecurity.com/api/v1/files/" -d '{
  "filters": {
    // some filters
  },
  "skip": 5,
  "limit": 10
  ...
}'
```

### Response

Returns a list of files in JSON format.

```json
{
  "total": 5 // approximate number of records
  "hasNext": true // whether there is more data to show or not.
  "data": [
    // returned records
  ]
}
```

If you run into any problems, we're here to help. To get assistance or support for your product issue, please [open a support ticket](/en-us/defender-xdr/contact-defender-support).