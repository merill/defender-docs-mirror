---
layout: Conceptual
title: Get domain statistics API - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/get-domain-statistics
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use the Get domain statistics API to retrieve the statistics on the given domain in Microsoft Defender for Endpoint.
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
document_id: 140d8056-6bb8-96dd-a705-4a2d1aeda193
document_version_independent_id: 140d8056-6bb8-96dd-a705-4a2d1aeda193
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/get-domain-statistics.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/get-domain-statistics
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/get-domain-statistics.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 40c28705-5331-d2de-6d57-0e0dc56cf110
---

# Get domain statistics API - Microsoft Defender for Endpoint | Microsoft Learn

## API description

Retrieves the statistics on the given domain.

## Limitations

- Rate limitations for this API are 100 calls per minute and 1500 calls per hour.
- The maximum value for `lookbackhours` is 720 hours (30 days).

## Permissions

When obtaining a token using user credentials:

- The user needs to have at least the following role permission: 'View Data'. For more information, see [Create and manage roles](../user-roles).

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro)

| Permission type | Permission | Permission display name |
| --- | --- | --- |
| Application | URL.Read.All | 'Read URLs' |
| Delegated (work or school account) | URL.Read.All | 'Read URLs' |

## HTTP request

```http
GET /api/domains/{domain}/stats
```

## Request headers

| Header | Value |
| --- | --- |
| Authorization | Bearer {token}. **Required**. |

## Request URI parameters

| Name | Type | Description |
| --- | --- | --- |
| lookBackHours | Int32 | Defines the hours we search back to get the statistics. Defaults to 30 days. **Optional**. |

## Request body

Empty

## Response

If successful and domain exists - 200 OK, with statistics object in the response body. If domain doesn't exist - 200 OK with a prevalence set to 0.

## Example

### Request example

Here's an example of the request.

```http
GET https://api.security.microsoft.com/api/domains/example.com/stats?lookBackHours=48
```

### Response example

Here's an example of the response.

```json
{
    "@odata.context": "https://api.security.microsoft.com/api/$metadata#microsoft.windowsDefenderATP.api.InOrgDomainStats",
    "host": "example.com",
    "organizationPrevalence": 4070,
    "orgFirstSeen": "2017-07-30T13:23:48Z",
    "orgLastSeen": "2017-08-29T13:09:05Z"
}
```