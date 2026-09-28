---
layout: Conceptual
title: Add or remove a tag for a machine - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/add-or-remove-machine-tags
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use the Add or Remove machine tags API to adds or remove a tag for a machine in Microsoft Defender for Endpoint.
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
document_id: 6616229d-c4ba-123d-ad63-302f0c8ef20f
document_version_independent_id: 6616229d-c4ba-123d-ad63-302f0c8ef20f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/add-or-remove-machine-tags.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/add-or-remove-machine-tags
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/add-or-remove-machine-tags.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: b19ddd35-723e-bfa8-2a05-2e9a294e01cc
---

# Add or remove a tag for a machine - Microsoft Defender for Endpoint | Microsoft Learn

## API description

Adds or removes a tag for a specific [device](machine).

## Limitations

- You can post on machines last seen according to your configured retention period.
- Rate limitations for this API are 100 calls per minute and 1500 calls per hour.

## Permissions

When obtaining a token using user credentials:

- The user needs to have at least the following role permission: 'Manage security setting'. For more information, see: [Create and manage roles](../user-roles).
- The user needs to have access to the machine, based on machine group settings. For more information, see: [Create and manage machine groups](../machine-groups).

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Defender for Endpoint APIs](apis-intro).

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Machine.ReadWrite.All | 'Read and write all machine information' |
| Delegated (work or school account) | Machine.ReadWrite | 'Read and write machine information' |

## HTTP request

```http
POST https://api.security.microsoft.com/api/machines/{id}/tags
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |
| Content-Type | string | application/json. **Required**. |

## Request body

To remove machine tag, set the Action to 'Remove' instead of 'Add' in the request body.

In the request body, supply a JSON object with the following parameters:

| Parameter | Type | Description |
| --- | --- | --- |
| Value | String | The tag name. **Required**. |
| Action | Enum | Add or Remove. Allowed values are: 'Add' or 'Remove'. **Required**. |

## Response

If successful, this method returns 200 - Ok response code and the updated Machine in the response body.

## Example Request

Here is an example of a request that adds a machine tag.

```http
POST https://api.security.microsoft.com/api/machines/1e5bc9d7e413ddd7902c2932e418702b84d0cc07/tags
```

```json
{
  "Value" : "test Tag 2",
  "Action": "Add"
}
```