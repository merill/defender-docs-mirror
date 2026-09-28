---
layout: Conceptual
title: Perform file upload - cloud discovery API - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/api-discovery-perform
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
description: This article describes the perform file upload request in the Defender for Cloud Apps cloud discovery API.
ms.date: 2023-01-29T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: c7f9c70d-ae33-fe68-93d4-a3e91adcf630
document_version_independent_id: c7f9c70d-ae33-fe68-93d4-a3e91adcf630
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/api-discovery-perform.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-discovery-perform
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/api-discovery-perform.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 2d3c6189-480b-953d-b863-4b8b844d648a
---

# Perform file upload - cloud discovery API - Microsoft Defender for Cloud Apps | Microsoft Learn

Upload the file contents by performing an HTTP PUT request. You will be required to use the URL returned by the [Initiate file upload](api-discovery-initiate) request.

Note

- You can upload individual files of up to 5 GB. If you need to upload larger files, break the cloud discovery data into multiple chunks.
- If you do not know which environment you are running, check the [Initiate file upload](api-discovery-initiate) request, which returns this information.

## HTTP request

```rest
PUT https://<initiate_file_upload_response_url>
```

Note

For Azure:

- If your file is under 64 MB, add the header "x-ms-blob-type: BlockBlob" to your request.
- If your file size is greater than 64MB, upload it in chunks. the easiest way to do this is using the [Azure SDK](https://azure.microsoft.com/downloads/).

## Example

### Request

Here is an example of the request for Azure.

```rest
curl --request PUT --upload-file <file_to_upload_full_path> -H "x-ms-blob-type: BlockBlob" "https://<initiate_file_upload_response_url>"
```

Here is an example of the request for Azure Java SDK.

```java
File fileReference = new File("file.name");
// Create a blob using the URI that contains the shared access signature.
CloudBlockBlob sasBlob = new CloudBlockBlob(uri);

// Upload the file to the blob.
sasBlob.upload(new FileInputStream(fileReference), fileReference.length());
```

If you run into any problems, we're here to help. To get assistance or support for your product issue, please [open a support ticket](/en-us/defender-xdr/contact-defender-support).