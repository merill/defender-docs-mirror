---
layout: Conceptual
title: Update machine entity API - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/update-machine-method
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to update machine tags by using this API. You can update the tags and devicevalue properties.
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
document_id: b667ee1c-c5e0-28a2-c23a-95ee6e61f4c0
document_version_independent_id: b667ee1c-c5e0-28a2-c23a-95ee6e61f4c0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/update-machine-method.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/update-machine-method
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/update-machine-method.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 6c8b7e90-43cb-007b-a876-2eeaacf52925
---

# Update machine entity API - Microsoft Defender for Endpoint | Microsoft Learn

## API description

Updates properties of existing [Machine](machine).

Updatable properties are: `machineTags` and `deviceValue`.

## Limitations

- You can update machines that are available in the API.
- Update machine only appends tags to the tag collection. If tags exist, they must be included in the tags collection in the body.
- Rate limitations for this API are 100 calls per minute and 1500 calls per hour.

## Permissions

When obtaining a token using user credentials:

- The user needs to have at least the following role permission: 'Alerts investigation'. For more information, see: [Create and manage roles](../user-roles).
- The user needs to have access to the device associated with the alert, based on device group settings. For more information, see: [Create and manage device groups](../machine-groups).

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see: [Use Microsoft Defender for Endpoint APIs](apis-intro)

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Machine.ReadWrite.All | 'Read and write machine information for all machines' |
| Delegated (work or school account) | Machine.ReadWrite | 'Read and write machine information' |

## HTTP request

```http
PATCH /api/machines/{machineId}
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |
| Content-Type | String | application/json. **Required**. |

## Request body

In the request body, supply the values for the relevant fields that should be updated.

Existing properties that aren't included in the request body will maintain their previous values or be recalculated based on changes to other property values.

For best performance, you shouldn't include existing values that haven't change.

| Property | Type | Description |
| --- | --- | --- |
| machineTags | String collection | Set of [machine](machine) tags. |
| deviceValue | Nullable Enum | The [value of the device](/en-us/defender-vulnerability-management/tvm-assign-device-value). Possible values are: 'Normal', 'Low' and 'High'. |

## Response

If successful, this method returns 200 OK, and the [machine](machine) entity in the response body with the updated properties.

If machine tags collection in body doesn't contain existing machine tags - replaces all tags with the tags provided in the request body.

If machine with the specified ID wasn't found - 404 Not Found.

## Example

### Request

Here's an example of the request.

```http
PATCH https://api.security.microsoft.com/api/machines/{machineId}
```

```json
{
    "deviceValue": "Normal",
    "machineTags": [
                     "Demo Device",
                     "Generic User Machine - Attack Source",
                     "Windows 10" "Windows11",
                     "Windows Insider - Fast"
    ]
}
```