---
layout: Conceptual
title: Set device value API - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/set-device-value
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to specify the value of a device using a Microsoft Defender for Endpoint API.
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
document_id: f806862f-bc08-0f88-ad30-6b0f3acefcd6
document_version_independent_id: f806862f-bc08-0f88-ad30-6b0f3acefcd6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/set-device-value.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/set-device-value
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/set-device-value.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 979423b2-7887-94a9-6ec1-4d180d7a9f01
---

# Set device value API - Microsoft Defender for Endpoint | Microsoft Learn

## API description

Set the device value of a specific [Machine](machine). See [assign device values](/en-us/defender-vulnerability-management/tvm-assign-device-value) for more information.

## Limitations

- You can post on devices last seen according to your configured retention period.
- Rate limitations for this API are 100 calls per minute and 1500 calls per hour.

## Permissions

When obtaining a token using user credentials:

- The user needs to have at least the following role permission: 'Manage security setting'. For more information, see [Create and manage roles](../user-roles).
- The user needs to have access to the machine, based on machine group settings. For more information, see [Create and manage machine groups](../machine-groups).

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro)

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Machine.ReadWrite.All | 'Read and write all machine information' |
| Delegated (work or school account) | Machine.ReadWrite | 'Read and write machine information' |

## HTTP request

```http
POST https://api.security.microsoft.com/api/machines/{machineId}/setDeviceValue
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |
| Content-Type | string | application/json. **Required**. |

## Request body

In the request body, supply a JSON object with the following parameters:

| Parameter | Type | Description |
| --- | --- | --- |
| DeviceValue | Enum | Device value. Allowed values are: 'Normal', 'Low' and 'High'. **Required**. |

## Response

If successful, this method returns 200 - Ok response code and the updated Machine in the response body.

## Example

### Request

Here is an example of a request that adds machine tag.

```http
POST https://api.security.microsoft.com/api/machines/1e5bc9d7e413ddd7902c2932e418702b84d0cc07/setDeviceValue
```

```json
{
  "DeviceValue" : "High"
}
```