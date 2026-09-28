---
layout: Conceptual
title: Finalize file upload - cloud discovery API - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/api-discovery-finalize
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
description: This article describes the done_upload request in the Defender for Cloud Apps cloud discovery API.
ms.date: 2023-01-29T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: 46d93c6d-c34a-387c-55b7-2cfa6b8ce10b
document_version_independent_id: 46d93c6d-c34a-387c-55b7-2cfa6b8ce10b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/api-discovery-finalize.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-discovery-finalize
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/api-discovery-finalize.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 695b47c9-0ae1-8a96-718e-b571b73a978e
---

# Finalize file upload - cloud discovery API - Microsoft Defender for Cloud Apps | Microsoft Learn

After the file content upload successfully completes, notify us in order to begin the processing of the file.

## HTTP request

```rest
POST /api/v1/discovery/done_upload/
```

## Request BODY parameters

| Parameter | Description |
| --- | --- |
| uploadUrl | The URL that was returned in the initial call requesting file upload. |
| inputStreamName | The name of the data source from which data is coming in (to see the list of names, in the portal, go to **Settings** &gt; **Automatic log upload**). |
| uploadAsSnapshot | Upload the data as a snapshot report instead of uploading to a continuous report. If this parameter is set, then the report will be created with the name specified in inputStreamName. |

## Example

### Request

Here is an example of the request.

```rest
curl -XPOST -H "Authorization:Token <your_token_key>" -H "Content-Type: application/json" "https://<tenant_id>.<tenant_region>.portal.cloudappsecurity.com/api/v1/discovery/done_upload/" -d {\"uploadUrl\":\"<initiate_file_upload_response_url>\",\"inputStreamName\":\"<inputStreamName>\"}
```

If you run into any problems, we're here to help. To get assistance or support for your product issue, please [open a support ticket](/en-us/defender-xdr/contact-defender-support).