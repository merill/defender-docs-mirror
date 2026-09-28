---
layout: Conceptual
title: Get domain-related alerts API - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/get-domain-related-alerts
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use the Get domain-related alerts API to retrieve alerts related to a given domain address in Microsoft Defender for Endpoint.
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
document_id: 7448b458-3fc7-c9d5-ff6b-7d9c8740fc5f
document_version_independent_id: 7448b458-3fc7-c9d5-ff6b-7d9c8740fc5f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/get-domain-related-alerts.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/get-domain-related-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/get-domain-related-alerts.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: d75f345e-e899-cf9a-2085-6d00ea0400de
---

# Get domain-related alerts API - Microsoft Defender for Endpoint | Microsoft Learn

## API description

Retrieves a collection of [Alerts](alerts) related to a given domain address.

## Limitations

- You can query on alerts last updated according to your configured retention period.
- Rate limitations for this API are 100 calls per minute and 1,500 calls per hour.

## Permissions

When obtaining a token using user credentials, the user needs to have at least the following role permission: `View Data`. For more information,see [Create and manage roles](../user-roles).

A response includes only alerts, associated with devices, that the user has access to, based on device group settings. For more information,see [Create and manage device groups](../machine-groups).

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro)

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Alert.ReadWrite.All | 'Read and write all alerts' |
| Delegated (work or school account) | Alert.ReadWrite | 'Read and write alerts' |

## HTTP request

```http
GET /api/domains/{domain}/alerts
```

## Request headers

| Header | Value |
| --- | --- |
| Authorization | String |

## Request body

Empty

## Response

If successful and domain exists - 200 OK with list of [alert](alerts) entities. If domain doesn't exist - 200 OK with an empty set.

## Example

### Request

Here's an example of the request.

```http
GET https://api.security.microsoft.com/api/domains/client.wns.windows.com/alerts
```