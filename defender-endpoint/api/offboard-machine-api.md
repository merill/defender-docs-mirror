---
layout: Conceptual
title: Offboard machine API - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/offboard-machine-api
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use an API to offboard a device from Microsoft Defender for Endpoint.
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
ms.custom:
- api
- sfi-ga-nochange
ms.date: 2026-08-11T00:00:00.0000000Z
locale: en-us
document_id: 1439b823-735b-857d-4ee0-7519414df51d
document_version_independent_id: 1439b823-735b-857d-4ee0-7519414df51d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/offboard-machine-api.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/offboard-machine-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/offboard-machine-api.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 85d6196d-d8e6-79a4-132d-f1e68f7ca62b
---

# Offboard machine API - Microsoft Defender for Endpoint | Microsoft Learn

## API description

Offboard device from Defender for Endpoint.

## Prerequisites

### Supported operating systems

| Operating system | Supported versions |
| --- | --- |
| Windows client | Windows 11 and Windows 10, version 1703 and later |
| Windows Server | Windows Server 2019 and later; Windows Server 2012 R2 and Windows Server 2016 when using the [new, unified agent for Defender for Endpoint](../update-agent-mma-windows#upgrade-to-the-new-agent-for-defender-for-endpoint) |
| macOS | [macOS 14 and later](../microsoft-defender-endpoint-releases#macos-releases) |
| Linux | [Supported Linux distributions](../mde-linux-prerequisites#supported-linux-distributions) |

## Limitations

- Rate limitations for this API are 100 calls per minute and 1,500 calls per hour.
- On Windows devices, running the offboarding API only stops the sensor service. It doesn't remove the onboarding information from the registry like an offboarding script does.

## Permissions

Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

When obtaining a token using user credentials:

- The user must have an appropriate role assigned. For more information, see: [Permission options](../user-roles#permission-options).
- The user must have access to the device, based on device group settings. For more information, see: [Create and manage device groups](../machine-groups).

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Defender for Endpoint APIs](apis-intro)

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | `Machine.Offboard` | `Offboard machine` |
| Delegated (work or school account) | `Machine.Offboard` | `Offboard machine` |

## HTTP request

```http
POST https://api.security.microsoft.com/api/machines/{id}/offboard
```

The machine ID can be found in the URL when you select the device. Generally, it's a 40 digit alphanumeric number that can be found in the URL.

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

If successful, this method returns `200 - Created response` code and [Machine Action](machineaction) in the response body.

## Example

### Request

Here's an example of the request. If there's no JSON comment added, it errors out with code `400`.

```http
POST https://api.security.microsoft.com/api/machines/1e5bc9d7e413ddd7902c2932e418702b84d0cc07/offboard
```

```json
{
  "Comment": "Offboard machine by automation"
}
```