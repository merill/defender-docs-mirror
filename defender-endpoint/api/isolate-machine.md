---
layout: Conceptual
title: Isolate machine API - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/isolate-machine
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use the Isolate machine API to isolate a device from accessing external network in Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- must-keep
ms.topic: reference
ms.subservice: reference
ms.custom: api
ms.date: 2025-11-13T00:00:00.0000000Z
locale: en-us
document_id: 78788d95-4175-1eed-4516-49635001387d
document_version_independent_id: 78788d95-4175-1eed-4516-49635001387d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/isolate-machine.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/isolate-machine
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/isolate-machine.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 613e3905-af06-3f5c-5eb6-5180b0cb8704
---

# Isolate machine API - Microsoft Defender for Endpoint | Microsoft Learn

## API description

Isolates a device from accessing external network.

When isolating a device, only certain processes and destinations are allowed. Therefore, devices that are behind a full VPN tunnel won't be able to reach the Microsoft Defender for Endpoint cloud service after the device is isolated. We recommend using a split-tunneling VPN for Microsoft Defender for Endpoint and Microsoft Defender Antivirus cloud-based protection-related traffic.

Calling this API on unmanaged devices triggers the [contain device from the network](../respond-machine-alerts#contain-devices-from-the-network) action. The IsolationType value should be set to 'UnManagedDevice.'

## Limitations

Rate limitations for this API are 100 calls per minute and 1,500 calls per hour.

## Prerequisites

### Supported operating systems

- Full isolation is available for devices on Windows 10, version 1703, and on Windows 11.
- Full isolation is available for all supported Linux devices. See [Microsoft Defender for Endpoint on Linux](../microsoft-defender-endpoint-linux).
- Selective isolation is available for devices on Windows 10, version 1709 or later, and on Windows 11.

## Permissions

When obtaining a token using user credentials:

- The user needs to have at least the following role permission: 'Active remediation actions.' For more information, see [Create and manage roles](../user-roles).
- The user needs to have access to the device, based on device group settings. For more information, see [Create and manage device groups](../machine-groups).

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro)

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Machine.Isolate | 'Isolate machine' |
| Delegated (work or school account) | Machine.Isolate | 'Isolate machine' |

## HTTP request

```http
POST https://api.security.microsoft.com/api/machines/{id}/isolate
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
| IsolationType | String | Type of the isolation. Allowed values are: **Full**, **Selective**, or **UnManagedDevice**. |

**IsolationType** controls the type of isolation to perform and can be one of the following:

- Full: Full isolation. Works for managed devices.
- Selective: Restrict only limited set of applications from accessing the network on managed devices. For more information, see [Isolate devices from the network](../respond-machine-alerts#isolate-devices-from-the-network).
- UnManagedDevice: The isolation targets unmanaged devices only.

## Response

If successful, this method returns 201 - Created response code and [Machine Action](machineaction) in the response body.

## Example

### Request

Here's an example of the request.

```http
POST https://api.security.microsoft.com/api/machines/1e5bc9d7e413ddd7902c2932e418702b84d0cc07/isolate
```

```json
{
  "Comment": "Isolate machine due to alert 1234",
  "IsolationType": "Full"
}
```