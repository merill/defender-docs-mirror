---
layout: Conceptual
title: Get Investigation object API - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/get-investigation-object
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use this API to create calls related to get Investigation object
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
document_id: 81b2f725-c8b4-305f-5af9-4fb186f41cb2
document_version_independent_id: 81b2f725-c8b4-305f-5af9-4fb186f41cb2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/get-investigation-object.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/get-investigation-object
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/get-investigation-object.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 5adc61af-2ffd-1e68-25a1-e9f38720f837
---

# Get Investigation object API - Microsoft Defender for Endpoint | Microsoft Learn

## API description

Retrieves specific [Investigation](investigation) by its ID.  ID can be the investigation ID or the investigation triggering alert ID.

## Limitations

Rate limitations for this API are 100 calls per minute and 1500 calls per hour.

## Permissions

When obtaining a token using user credentials:

- The user needs to have at least the following role permission: 'View Data'. For more information, see [Create and manage roles](../user-roles).

One of the following permissions is required to call this API. TFor more information on how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro)

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Alert.ReadWrite.All | 'Read and write all alerts' |
| Delegated (work or school account) | Alert.ReadWrite | 'Read and write alerts' |

## HTTP request

```http
GET https://api.security.microsoft.com/api/investigations/{id}
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |

## Request body

Empty

## Response

If successful, this method returns 200, Ok response code with an [Investigations](investigation) entity.