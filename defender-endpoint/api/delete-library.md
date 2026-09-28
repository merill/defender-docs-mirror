---
layout: Conceptual
title: Delete a file from the live response library - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/delete-library
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to delete a file from the live response library.
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
ms.date: 2025-12-11T00:00:00.0000000Z
locale: en-us
document_id: 90d36e41-a2a9-a52d-458e-03d5d3ebd8be
document_version_independent_id: 90d36e41-a2a9-a52d-458e-03d5d3ebd8be
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/delete-library.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/delete-library
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/delete-library.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: a742210b-a2c3-3147-2f97-d03157d59152
---

# Delete a file from the live response library - Microsoft Defender for Endpoint | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## API description

Delete a file from live response library.

Tip

You can also delete live response files from the [Library management](../configure-libraries-live-response) page in the Microsoft Defender portal.

## Limitations

Rate limitations for this API are 100 calls per minute and 1500 calls per hour.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Get started](apis-intro).

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Library.Manage | Manage live response library |
| Delegated (work or school account) | Library.Manage | Manage live response library |

## HTTP request

DELETE [https://api.security.microsoft.com/api/libraryfiles/{fileName}](https://api.security.microsoft.com/api/libraryfiles/%7BfileName%7D)

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer&lt;token&gt;. **Required**. |

## Request body

Empty

## Response

- If file exists in library and deleted successfully 204 No Content.
- If specified file name was not found 404 Not Found.

## Example

Request

Here is an example of the request.

```http
DELETE https://api.security.microsoft.com/api/libraryfiles/script1.ps1
```