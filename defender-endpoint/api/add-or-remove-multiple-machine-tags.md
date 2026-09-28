---
layout: Conceptual
title: Add or remove a tag for multiple machines - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/add-or-remove-multiple-machine-tags
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use the Add or Remove machine tags API to add or remove a tag for multiple devices in Microsoft Defender for Endpoint.
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
document_id: c52d6114-0129-06de-ed7b-5060d87dfea5
document_version_independent_id: c52d6114-0129-06de-ed7b-5060d87dfea5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/add-or-remove-multiple-machine-tags.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/add-or-remove-multiple-machine-tags
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/add-or-remove-multiple-machine-tags.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: e5d450aa-db7b-827b-8cd8-19bb8f0f4797
---

# Add or remove a tag for multiple machines - Microsoft Defender for Endpoint | Microsoft Learn

## API description

Adds or removes a tag for the specified set of machines.

## Limitations

- You can post on machines last seen according to your configured retention period.
- Rate limitations for this API are 100 calls per minute and 1,500 calls per hour.
- We can add or remove a tag for up to 500 machines per API call.

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
POST https://api.security.microsoft.com/api/machines/AddOrRemoveTagForMultipleMachines
```

Tip

For better performance, instead of using api.security.microsoft.com, use a server closer to your geolocation:

- us.api.security.microsoft.com
- eu.api.security.microsoft.com
- uk.api.security.microsoft.com
- au.api.security.microsoft.com
- swa.api.security.microsoft.com
- ina.api.security.microsoft.com
- aea.api.security.microsoft.com

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |
| Content-Type | string | application/json. **Required**. |

## Request body

In the request body, supply a JSON object with the following parameters:

| Parameter | Type | Description |
| --- | --- | --- |
| Value | String | The tag name. **Required**. |
| Action | Enum | Add or Remove. Allowed values are: 'Add' or 'Remove'. **Required**. |
| MachineIds | List (String) | List of machine IDs to update. Required. |

## Response

If successful, this method returns 200 - Ok response code and the updated machines in the response body.

## Example Request

To remove machine tags, set the Action to 'Remove' instead of 'Add' in the request body.

Here's an example of a request that adds a tag to multiple machines.

```http
POST https://api.security.microsoft.com/api/machines/AddOrRemoveTagForMultipleMachines
```

```json
{
  "Value" : "Tag",
  "Action": "Add",
  "MachineIds": ["34e83ca3feea4dae2353006ba389262c033a025e",
  "2a398439b4975924e87a65943972bc702469b329",
  "a610c00c65fdf79960cc0077d9d8c569d23f09a5"]
}
```