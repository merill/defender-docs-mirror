---
layout: Conceptual
title: Release device from isolation API - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/unisolate-machine
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use this API to create calls related to release a device from isolation.
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
ms.date: 2025-11-13T00:00:00.0000000Z
locale: en-us
document_id: 5f1c5d6b-ea6b-89b1-38f7-9fd80acbba63
document_version_independent_id: 5f1c5d6b-ea6b-89b1-38f7-9fd80acbba63
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/unisolate-machine.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/unisolate-machine
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/unisolate-machine.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/e0ffb20c-01c6-407b-a9bd-29111652a1dc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/3904bce4-d817-48cf-85fd-b6146fca83b7
platformId: 1bf4b5e3-6e12-6c4a-6f63-721564ade88f
---

# Release device from isolation API - Microsoft Defender for Endpoint | Microsoft Learn

## API description

Undo isolation of a device.

When isolating a device, only certain processes and destinations are allowed. Devices that are behind a full VPN tunnel won't be able to reach the Microsoft Defender for Endpoint cloud service after the device is isolated. We recommend using a split-tunneling VPN for Microsoft Defender for Endpoint and Microsoft Defender Antivirus cloud-based protection-related traffic.

## Limitations

Rate limitations for this API are 100 calls per minute and 1500 calls per hour.

## Prerequisites

### Supported operating systems

- Full isolation is available for devices on Windows 10, version 1703.
- Full isolation is available in **public preview** for all supported Microsoft Defender for Endpoint on Linux listed in [System requirements](../mde-linux-prerequisites).
- Selective isolation is available for devices on Windows 10, version 1709 or later.

## Permissions

When obtaining a token using user credentials:

- The user needs to have at least the following role permission: 'Active remediation actions'. For more information, see: [Create and manage roles](../user-roles).
- The user needs to have access to the device, based on device group settings. For more information, see: [Create and manage device groups](../machine-groups).

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro)

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Machine.Isolate | 'Isolate machine' |
| Delegated (work or school account) | Machine.Isolate | 'Isolate machine' |

## HTTP request

```http
POST https://api.security.microsoft.com/api/machines/{id}/unisolate
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
| Comment | String | Comment to associate with the action. **Required**. |

## Response

If successful, this method returns 201 - Created response code and [Machine Action](machineaction) in the response body.

If you send multiple API calls to remove isolation for the same device, it returns "pending machine action" or HTTP 400 with the message "Action is already in progress".

## Example

### Request

Here is an example of the request.

```http
POST https://api.security.microsoft.com/api/machines/1e5bc9d7e413ddd7902c2932e418702b84d0cc07/unisolate
```

```json
{
  "Comment": "Unisolate machine since it was clean and validated"
}
```