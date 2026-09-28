---
layout: Conceptual
title: Entities API - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/api-entities
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: This article provides information about using the Entities API.
ms.date: 2024-11-28T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: 57aa0af2-cb53-0468-cbcc-ae4f860fe02d
document_version_independent_id: 57aa0af2-cb53-0468-cbcc-ae4f860fe02d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/api-entities.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-entities
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/api-entities.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 5807ab4d-cbe8-7419-9d40-7b15b88b075b
---

# Entities API - Microsoft Defender for Cloud Apps | Microsoft Learn

Note

This API is not available for Microsoft 365 Cloud App Security.

The Entities API provides you with basic information about the users and accounts using your organization's cloud apps, allowing you to understand service use patterns.

The following lists the supported requests:

- [List entities](api-entities-list)
- [Fetch entity](api-entities-fetch)
- [Fetch entity tree](api-entities-fetch-tree)

## Filters

For information about how filters work, see [Filters](api-introduction#filters).

The following table describes the supported filters:

| Filter | Type | Operators | Description |
| --- | --- | --- | --- |
| type | string | eq, neq | Filter entities by their type |
| isAdmin | string | eq | Filter entities that are admins |
| entity | entity pk | eq, neq | Filter entities with specific entities pks. If a user is selected, this filter also returns all of the user's accounts. Example: `[{ "id": "entity-id", "inst": 0 }]` |
| userGroups | string | eq, neq | Filter entities by their associated group IDs |
| app | integer | eq, neq | Filter entities using services with the specified SaaS ID for example: 11770 |
| instance | integer | eq, neq | Filter entities using services with the specified app instances (SaaS ID and Instance ID). For example: 11770, 1059065 |
| isExternal | boolean | eq | The entity's affiliation. Possible values include:**true**: External**false**: Internal**null**: No value |
| domain | string | eq, neq, isset, isnotset | The entity's related domain |
| organization | string | eq, neq, isset, isnotset | Filter entities with the specified organization unit |
| status | string | eq, neq | Filter entities by status. Possible values include:**0**: N/A**1**: Staged**2**: Active**3**: Suspended**4**: Deleted |

If you run into any problems, we're here to help. To get assistance or support for your product issue, please [open a support ticket](/en-us/defender-xdr/contact-defender-support).