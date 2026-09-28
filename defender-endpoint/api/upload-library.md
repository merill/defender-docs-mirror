---
layout: Conceptual
title: Upload files to the live response library - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/upload-library
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to upload a file to the live response library.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- must-keep
ms.topic: reference
ms.subservice: reference
ms.custom: api
ms.date: 2025-12-11T00:00:00.0000000Z
locale: en-us
document_id: 4b8defd1-208a-bb84-f5af-71a1c2218326
document_version_independent_id: 4b8defd1-208a-bb84-f5af-71a1c2218326
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/upload-library.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/upload-library
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/upload-library.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 4c5cb046-66c9-bc17-8342-eddedfd66b25
---

# Upload files to the live response library - Microsoft Defender for Endpoint | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## API description

Upload file to live response library.

Tip

You can also upload live response files from the [Library management](../configure-libraries-live-response) page in the Microsoft Defender portal.

## Limitations

- File max size limitation is 20MB.
- Rate limitations for this API are 100 calls per minute and 1500 calls per hour.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Get started](apis-intro).

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Library.Manage | Manage live response library |
| Delegated (work or school account) | Library.Manage | Manage live response library |

## HTTP request

Upload

```HTTP
POST https://api.security.microsoft.com/api/libraryfiles
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer&lt;token&gt;. Required. |
| Content-Type | string | multipart/form-data. Required. |

## Request body

In the request body, supply a form-data object with the following parameters:

| Parameter | Type | Description |
| --- | --- | --- |
| File | File content | The file to be uploaded to live response library.Required |
| Description | String | Description of the file. |
| ParametersDescription | String | (Optional) Parameters required for the script to run. Default value is an empty string. |
| OverrideIfExists | Boolean | (Optional) Whether to override the file if it already exists. Default value is an empty string. |

## Response

- If successful, this method returns 200 - OK response code and the uploaded live response library entity in the response body.
- If not successful: this method returns 400 - Bad Request. Bad request usually indicates incorrect body.

## Example

Request

Here is an example of the request using curl.

```CURL
curl -X POST https://api.security.microsoft.com/api/libraryfiles -H
"Authorization: Bearer \$token" -F "file=\@mdatp1.png" -F
"ParametersDescription=test"
-F "HasParameters=true" -F "OverrideIfExists=true" -F "Description=test
description"
```