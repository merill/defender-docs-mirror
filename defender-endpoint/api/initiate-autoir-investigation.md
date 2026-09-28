---
layout: Conceptual
title: Start Investigation API - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/initiate-autoir-investigation
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use this API to start investigation on a device.
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
ms.date: 2025-11-11T00:00:00.0000000Z
locale: en-us
document_id: 1139db93-82d3-6e1e-e316-40cc583edf98
document_version_independent_id: 1139db93-82d3-6e1e-e316-40cc583edf98
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/initiate-autoir-investigation.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/initiate-autoir-investigation
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/initiate-autoir-investigation.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/e0ffb20c-01c6-407b-a9bd-29111652a1dc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19ec6774-09b8-473e-a17e-b17b518bbad7
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/3904bce4-d817-48cf-85fd-b6146fca83b7
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ade36b61-c646-4bd8-87ee-f3a843461962
platformId: bb4083f4-c3de-737e-592c-5458964ff8f0
---

# Start Investigation API - Microsoft Defender for Endpoint | Microsoft Learn

## API description

Start automated investigation on a device.

See [Overview of automated investigations](../automated-investigations) for more information.

## Limitations

Rate limitations for this API are 50 calls per hour.

## Prerequisites

Your organization must have Defender for Endpoint, see [Minimum requirements for Microsoft Defender for Endpoint](../minimum-requirements).

### Supported operating systems

- Windows 11
- Windows 10, version [1803](/en-us/windows/release-information/status-windows-10-1809-and-windows-server-2019) or later
- Windows 10, version 1803 (OS Build 17134.704 with [KB4493464](https://support.microsoft.com/servicing/os/windows-10/2019/04/april-9-2019-kb4493464-os-build-17134-706)) or later
- Windows 10, version 1709 (OS Build 16299.1085 with [KB4493441](https://support.microsoft.com/servicing/os/windows-10/2019/04/april-9-2019-kb4493441-os-build-16299-1087)) or later
- Windows Server 2019 and later
- Azure Stack HCI OS, version 23H2 and later

## Permissions

When obtaining a token using user credentials:

- The user needs to have at least the following role permission: 'Active remediation actions'. For more information, see: [Create and manage roles](../user-roles).
- The user needs to have access to the device, based on device group settings. For more information, see: [Create and manage device groups](../machine-groups).

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro)

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Alert.ReadWrite.All | 'Read and write all alerts' |
| Delegated (work or school account) | Alert.ReadWrite | 'Read and write alerts' |

## HTTP request

```http
POST https://api.security.microsoft.com/api/machines/{id}/startInvestigation
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

If successful, this method returns 201 - Created response code and [Investigation](investigation) in the response body.

## Example

### Request

Here's an example of the request.

```https
POST https://api.security.microsoft.com/api/machines/1e5bc9d7e413ddd7902c2932e418702b84d0cc07/startInvestigation
```

```json
{
  "Comment": "Test investigation"
}
```