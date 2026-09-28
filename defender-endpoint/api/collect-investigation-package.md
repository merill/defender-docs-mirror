---
layout: Conceptual
title: Collect investigation package API - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/collect-investigation-package
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use this API to create calls related to the collecting an investigation package from a device.
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
document_id: 4de410ec-54c1-1d4f-ab98-c4d5c3c3c42e
document_version_independent_id: 4de410ec-54c1-1d4f-ab98-c4d5c3c3c42e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/collect-investigation-package.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/collect-investigation-package
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/collect-investigation-package.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 786404a4-27af-e0ed-5252-1910a3689160
---

# Collect investigation package API - Microsoft Defender for Endpoint | Microsoft Learn

## API description

Collect investigation package from a device.

## Limitations

- Rate limitations for this API are 100 calls per minute and 1500 calls per hour.

## Permissions

When obtaining a token using user credentials:

- The user needs to have at least the following role permission: 'Alerts Investigation'. For more information, see: [Create and manage roles](../user-roles)
- The user needs to have access to the device, based on device group settings. For more information, see: [Create and manage device groups](../machine-groups)

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Defender for Endpoint APIs](apis-intro)

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Machine.CollectForensics | 'Collect forensics' |
| Delegated (work or school account) | Machine.CollectForensics | 'Collect forensics' |

## HTTP request

```http
POST https://api.security.microsoft.com/api/machines/{id}/collectInvestigationPackage
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

If successful, this method returns 201 - Created response code and [Machine Action](machineaction) in the response body. If a collection is already running, this returns 400 Bad Request.

## Example

### Request

Here is an example of the request.

```http
POST https://api.security.microsoft.com/api/machines/fb9ab6be3965095a09c057be7c90f0a2/collectInvestigationPackage
```

```json
{
  "Comment": "Collect forensics due to alert 1234"
}
```