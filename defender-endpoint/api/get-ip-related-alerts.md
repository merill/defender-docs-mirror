---
layout: Conceptual
title: Get IP related alerts API - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/get-ip-related-alerts
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Retrieve a collection of alerts related to a given IP address using Microsoft Defender for Endpoint.
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
document_id: 48a3588e-3942-ccf6-1bc3-bb8f083c446f
document_version_independent_id: 48a3588e-3942-ccf6-1bc3-bb8f083c446f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/get-ip-related-alerts.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/get-ip-related-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/get-ip-related-alerts.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 171c8d22-b08e-937b-fa18-22f1c166b72d
---

# Get IP related alerts API - Microsoft Defender for Endpoint | Microsoft Learn

## API description

Retrieves a collection of alerts related to a given IP address.

## Limitations

Rate limitations for this API are 100 calls per minute and 1,500 calls per hour.

## Permissions

When obtaining a token using user credentials:

- The user needs to have at least the following role permission: `View Data`. For more information, see [Create and manage roles](../user-roles) for more information.
- Response includes only alerts, associated with devices, that the user have access to, based on device group settings (See [Create and manage device groups](../machine-groups) for more information)

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Defender for Endpoint APIs](apis-intro).

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Alert.Read.All | `Read all alerts` |
| Application | Alert.ReadWrite.All | `Read and write all alerts` |
| Delegated (work or school account) | Alert.Read | `Read alerts` |
| Delegated (work or school account) | Alert.ReadWrite | `Read and write alerts` |

## HTTP request

```http
GET /api/ips/{ip}/alerts
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |

## Request body

Empty

## Response

If successful and IP exists - 200 OK with list of [alert](alerts) entities in the body. If IP address is unknown but valid, it returns an empty set. If the IP address is invalid, it returns HTTP 400.

## Example

### Request

Here's an example of the request.

```http
GET https://api.security.microsoft.com/api/ips/10.209.67.177/alerts
```