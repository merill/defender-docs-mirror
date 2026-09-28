---
layout: Conceptual
title: Get machine related alerts API - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/get-machine-related-alerts
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use the Get machine related alerts API. This API allows you to retrieve all alerts that are related to a specific device in Microsoft Defender for Endpoint.
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
document_id: 220b0506-fc99-bb91-a6bd-05eaf73dc1eb
document_version_independent_id: 220b0506-fc99-bb91-a6bd-05eaf73dc1eb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/get-machine-related-alerts.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/get-machine-related-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/get-machine-related-alerts.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 46fcfa97-8c2f-0e35-32d4-6a15c4aacf76
---

# Get machine related alerts API - Microsoft Defender for Endpoint | Microsoft Learn

## API description

Retrieves all [Alerts](alerts) related to a specific device.

## Limitations

- You can query on devices last updated according to your configured retention period.
- Rate limitations for this API are 100 calls per minute and 1500 calls per hour.

## Permissions

When obtaining a token using user credentials:

- The user needs to have at least the following role permission: 'View Data'. For more information about permissions, see: [Create and manage roles](../user-roles).
- The user needs to have access to the device, based on device group settings. For more information about device group settings, see: [Create and manage device groups](../machine-groups).

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Alert.ReadWrite.All | 'Read and write all alerts' |
| Delegated (work or school account) | Alert.ReadWrite | 'Read and write alerts' |

## HTTP request

```http
GET /api/machines/{id}/alerts
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |

## Request body

Empty

## Response

If successful and device exists: 200 OK with list of [alert](alerts) entities in the body. If device was not found: 404 Not Found.