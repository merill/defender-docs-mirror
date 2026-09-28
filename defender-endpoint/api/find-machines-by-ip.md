---
layout: Conceptual
title: Find devices by internal IP API - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/find-machines-by-ip
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Find devices seen with the requested internal IP in the time range of 15 minutes prior and after a given timestamp
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
document_id: e1d630d3-4dbf-ff61-3f59-d9c3263834a3
document_version_independent_id: e1d630d3-4dbf-ff61-3f59-d9c3263834a3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/find-machines-by-ip.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/find-machines-by-ip
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/find-machines-by-ip.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 5a94167c-4e37-374d-1cbe-c21feb9b8324
---

# Find devices by internal IP API - Microsoft Defender for Endpoint | Microsoft Learn

## API description

Find [Machines](machine) seen with the requested internal IP in the time range of 15 minutes prior and after a given timestamp.

## Limitations

- The given timestamp must be in the past 30 days.
- Rate limitations for this API are 100 calls per minute and 1,500 calls per hour.

## Permissions

When obtaining a token using user credentials:

- Responses include only devices that the user have access to based on device group settings. For more information, see [Create and manage device groups](../machine-groups).
- The user needs to have at least the following role permission: 'View Data'. For more information, see [Create and manage roles](../user-roles).
- Responses include only devices that the user have access to based on device group settings. For more information, see [Create and manage device groups](../machine-groups).

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro)

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | Machine.ReadWrite.All | 'Read and write all machine information' |
| Delegated (work or school account) | Machine.ReadWrite | 'Read and write machine information' |

## HTTP request

```http
GET /api/machines/findbyip(ip='{IP}',timestamp={TimeStamp})
```

## Request headers

| Name | Type | Description |
| --- | --- | --- |
| Authorization | String | Bearer {token}. **Required**. |

## Request body

Empty

## Response

If successful - 200 OK with list of the machines in the response body. If the timestamp isn't in the past 30 days - 400 Bad Request.

## Example

### Request

Here's an example of the request.

```http
GET https://api.security.microsoft.com/api/machines/findbyip(ip='10.248.240.38',timestamp=2019-09-22T08:44:05Z)
```