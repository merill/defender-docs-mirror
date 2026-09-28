---
layout: Conceptual
title: Find devices by tag API - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/find-machines-by-tag
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Find all devices that contain specific tag
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
ms.date: 2021-02-02T00:00:00.0000000Z
locale: en-us
document_id: 8f86b616-1295-fd6b-7b83-4107b1a9296a
document_version_independent_id: 8f86b616-1295-fd6b-7b83-4107b1a9296a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/find-machines-by-tag.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/find-machines-by-tag
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/find-machines-by-tag.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 144ed9d0-7331-6100-f6e6-3f61406c400e
---

# Find devices by tag API - Microsoft Defender for Endpoint | Microsoft Learn

## API description

Find [Machines](machine) by [Tag](../machine-tags).

`startswith` query is supported.

## Limitations

Rate limitations for this API are 100 calls per minute and 1,500 calls per hour.

## Permissions

When obtaining a token using user credentials:

- Responses include only devices that the user have access to based on device group settings. For more information, see: [Create and manage device groups](../machine-groups).
- The user needs to have at least the following role permission: 'View Data'. For more information, see: [Create and manage roles](../user-roles)
- Responses include only devices that the user have access to based on device group settings. For more information, see: [Create and manage device groups](../machine-groups).

The following permission is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro)

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Machine.ReadWrite.All | 'Read and write all machine information' |
| Delegated (work or school account) | Machine.ReadWrite | 'Read and write machine information' |

## HTTP request

```http
GET /api/machines/findbytag?tag={tag}&useStartsWithFilter={true/false}
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |

## Request URI parameters

| Name | Type | Description |
| --- | --- | --- |
| tag | String | The tag name. **Required**. |
| useStartsWithFilter | Boolean | When set to true, the search finds all devices with tag name that starts with the given tag in the query. Defaults to false. **Optional**. |

## Request body

Empty

## Response

If successful - 200 OK with list of the machines in the response body.

## Example

### Request

Here's an example of the request.

```http
GET https://api.security.microsoft.com/api/machines/findbytag?tag=testTag&useStartsWithFilter=true
```