---
layout: Conceptual
title: Batch Delete Indicators API - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/batch-delete-ti-indicators
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use the Batch Delete Indicators API to delete indicator entities by ID in Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.subservice: reference
ms.reviewer: itsela
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- must-keep
ms.topic: reference
ms.custom: api
ms.date: 2025-12-11T00:00:00.0000000Z
locale: en-us
document_id: fd0ea04d-abf3-69a1-2da1-af6e9e89a60d
document_version_independent_id: fd0ea04d-abf3-69a1-2da1-af6e9e89a60d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/batch-delete-ti-indicators.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/batch-delete-ti-indicators
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/batch-delete-ti-indicators.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86a4b315-a9f1-4577-b985-6fb0e0e67420
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/96ac410d-d052-4707-8007-df31dd0fe041
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 28302e75-d8be-cfa4-4a74-daf6b104d357
---

# Batch Delete Indicators API - Microsoft Defender for Endpoint | Microsoft Learn

## API description

Deletes [Indicator](ti-indicator) entities by ID.

## Limitations

- Rate limitations for this API are 30 calls per minute and 1,500 calls per hour.
- Batch size limit of up to 500 [Indicator](ti-indicator) IDs.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Get started](apis-intro).

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Ti.ReadWrite.All | 'Read and write Indicators' |

## HTTP request

```http
POST https://api.security.microsoft.com/api/indicators/BatchDelete
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |

## Request body

In the request body, supply a JSON object with the following parameters:

| Parameter | Type | Description |
| --- | --- | --- |
| IndicatorIds | List *String* | A list of the IDs of the indicators to be removed. **Required** |

## Response

- If Indicators all existed and were deleted successfully - 204 OK without content.
- If indicator IDs list is empty or exceeds size limit - 400 Bad Request.
- If any indicator ID is invalid - 400 Bad Request.
- If requestor isn't exposed to any indicator's device groups - 403 Forbidden.
- If any Indicator ID wasn't found - 404 Not Found.

## Example

### Request

Here's an example of the request.

```http
POST https://api.security.microsoft.com/api/indicators/BatchDelete
```

```json
{
    "IndicatorIds": [ "1", "2", "5" ]
}
```