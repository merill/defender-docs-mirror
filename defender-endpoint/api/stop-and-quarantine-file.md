---
layout: Conceptual
title: Stop and quarantine file API - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/stop-and-quarantine-file
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to stop running a file on a device and delete the file in Microsoft Defender for Endpoint. See an example.
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
document_id: 36c7215b-8496-2ca1-5c0e-3af4c246e367
document_version_independent_id: 36c7215b-8496-2ca1-5c0e-3af4c246e367
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/stop-and-quarantine-file.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/stop-and-quarantine-file
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/stop-and-quarantine-file.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/e0ffb20c-01c6-407b-a9bd-29111652a1dc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/3904bce4-d817-48cf-85fd-b6146fca83b7
platformId: d72d6e67-4a63-875d-49ea-2751def753fb
---

# Stop and quarantine file API - Microsoft Defender for Endpoint | Microsoft Learn

## API description

Stop execution of a file on a device and delete it.

## Limitations

- Rate limitations for this API are 100 calls per minute and 1500 calls per hour.

You can only take this action if:

- The device you're taking the action on is running Windows 10, version 1703 or later, or Windows 11
- The file does not belong to trusted third-party publishers or is not signed by Microsoft
- Microsoft Defender Antivirus must at least be running on Passive mode. For more information, see: [Microsoft Defender Antivirus compatibility](../microsoft-defender-antivirus-compatibility).

## Permissions

When obtaining a token using user credentials:

- The user needs to have at least the following role permission: 'Active remediation actions'. For more information, see: [Create and manage roles](../user-roles).
- The user needs to have access to the device, based on device group settings. For more information, see: [Create and manage device groups](../machine-groups).

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro)

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Machine.StopAndQuarantine | 'Stop And Quarantine' |
| Application | Machine.ReadWrite.All | 'Read and write all machine information' |
| Delegated (work or school account) | Machine.StopAndQuarantine | 'Stop And Quarantine' |

## HTTP request

```http
POST https://api.security.microsoft.com/api/machines/{id}/StopAndQuarantineFile
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
| Sha1 | String | Sha1 of the file to stop and quarantine on the device. **Required**. |

## Response

If successful, this method returns 201 - Created response code and [Machine Action](machineaction) in the response body.

## Example

### Request

Here's an example of the request.

```http
POST https://api.security.microsoft.com/api/machines/1e5bc9d7e413ddd7902c2932e418702b84d0cc07/StopAndQuarantineFile
```

```json
{
  "Comment": "Stop and quarantine file on machine due to alert 441688558380765161_2136280442",
  "Sha1": "87662bc3d60e4200ceaf7aae249d1c343f4b83c9"
}
```