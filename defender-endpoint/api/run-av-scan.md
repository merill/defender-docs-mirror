---
layout: Conceptual
title: Run antivirus scan API - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/run-av-scan
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use this API to create calls related to running an antivirus scan on a device.
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
document_id: 0028584a-0bef-0c3e-8a8a-5274dcf0549a
document_version_independent_id: 0028584a-0bef-0c3e-8a8a-5274dcf0549a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/run-av-scan.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/run-av-scan
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/run-av-scan.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 3eeacc1e-2811-6f81-aba8-9d15c3e860af
---

# Run antivirus scan API - Microsoft Defender for Endpoint | Microsoft Learn

## API description

Initiate Microsoft Defender Antivirus scan on a device.

A Microsoft Defender Antivirus scan can run alongside other antivirus solutions, whether Microsoft Defender Antivirus is the active antivirus solution or not. Microsoft Defender Antivirus can be in Passive mode. For more information, see [Microsoft Defender Antivirus compatibility](../microsoft-defender-antivirus-compatibility).

## Limitations

Rate limitations for this API are 100 calls per minute and 1500 calls per hour.

## Prerequisites

### Supported operating systems

- Windows 10, version 1709 or later, and on Windows 11.
- Linux Servers. See [Supported Linux distributions](../mde-linux-prerequisites#supported-linux-distributions)
- macOS. See [Prerequisites for Defender for Endpoint on macOS](../microsoft-defender-endpoint-mac-prerequisites)

## Permissions

When obtaining a token using user credentials:

- The user needs to have at least the following role permission: 'Active remediation actions'. For more information, see: [Create and manage roles](../user-roles).
- The user needs to have access to the device, based on device group settings. For more information, see [Create and manage device groups](../machine-groups).

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro)

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Machine.Scan | 'Scan machine' |
| Delegated (work or school account) | Machine.Scan | 'Scan machine' |

## HTTP request

```http
POST https://api.security.microsoft.com/api/machines/{id}/runAntiVirusScan
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |
| Content-Type | string | application/json |

## Request body

In the request body, supply a JSON object with the following parameters:

| Parameter | Type | Description |
| --- | --- | --- |
| Comment | String | Comment to associate with the action. **Required**. |
| ScanType | String | Defines the type of the Scan. **Required**. |

**ScanType** controls the type of scan to perform and can be one of the following:

- **Quick**: Perform quick scan on the device
- **Full**: Perform full scan on the device

## Response

If successful, this method returns 201, Created response code and *MachineAction* object in the response body.

If you send multiple API calls to run an antivirus scan for the same device, it returns "pending machine action" or HTTP 400 with the message "Action is already in progress".

## Example

### Request

Here is an example of the request.

```http
POST https://api.security.microsoft.com/api/machines/1e5bc9d7e413ddd7902c2932e418702b84d0cc07/runAntiVirusScan
```

```json
{
  "Comment": "Check machine for viruses due to alert 3212",
  "ScanType": "Full"
}
```