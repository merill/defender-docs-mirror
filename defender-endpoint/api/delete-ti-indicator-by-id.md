---
layout: Conceptual
title: Delete Indicator API. - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/delete-ti-indicator-by-id
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use the Delete Indicator API to delete an Indicator entity by ID in Microsoft Defender for Endpoint.
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
document_id: 6aaa2a43-4b31-1803-301c-1a0ae4968f2b
document_version_independent_id: 6aaa2a43-4b31-1803-301c-1a0ae4968f2b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/delete-ti-indicator-by-id.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/delete-ti-indicator-by-id
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/delete-ti-indicator-by-id.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: f64f8cab-582a-2eff-7961-0d5e45903d19
---

# Delete Indicator API. - Microsoft Defender for Endpoint | Microsoft Learn

## API description

Deletes an [Indicator](ti-indicator) entity by ID.

## Limitations

Rate limitations for this API are 100 calls per minute and 1,500 calls per hour.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Get started](apis-intro).

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Ti.ReadWrite.All | 'Read and write Indicators' |

## HTTP request

```http
Delete https://api.security.microsoft.com/api/indicators/{id}
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |

## Request body

Empty

## Response

If Indicator exists and deleted successfully - 204 OK without content.

If Indicator with the specified ID wasn't found - 404 Not Found.

## Example

### Request

Here's an example of the request.

```http
DELETE https://api.security.microsoft.com/api/indicators/995
```