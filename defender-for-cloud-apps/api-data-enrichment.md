---
layout: Conceptual
title: Data Enrichment API - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/api-data-enrichment
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
description: This article provides information about using the Data Enrichment API.
ms.date: 2023-01-29T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: 120cc7e5-1589-63e5-ecfe-99220b2658a3
document_version_independent_id: 120cc7e5-1589-63e5-ecfe-99220b2658a3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/api-data-enrichment.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-data-enrichment
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/api-data-enrichment.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
platformId: c320c23d-72f5-cc3e-cbc6-7a70213c965f
---

# Data Enrichment API - Microsoft Defender for Cloud Apps | Microsoft Learn

The Data Enrichment API enables you to manage identifiable IP address ranges, such as your physical office IP addresses. IP address ranges allow you to tag, categorize, and customize the way logs and alerts are displayed and investigated. For more information, see [Working with IP ranges and tags](ip-tags).

The following lists the supported requests:

- [List IP address ranges](api-data-enrichment-list)
- [Create IP address range](api-data-enrichment-create)
- [Update IP address range](api-data-enrichment-update)
- [Delete IP address range](api-data-enrichment-delete)

## Properties

The response object defines the following properties.

| Property | Type | Description |
| --- | --- | --- |
| total | int | Total number of record |
| hasNext | bool | Indicates whether there are additional records |
| data | list | List of the existing records |
| \_id | string | Unique id of the IP range |
| name | string | The unique name of the range |
| subnets | list | An array of masks, IP addresses (IPv4 / IPv6), and original strings |
| location | string | An object including the location name, latitude, longitude, country code, and country name |
| organization | string | The registered ISP |
| tags | list | An array of new or existing objects including the tag name, id, description, name template, and tenant id |
| category | int | The category of the IP range. Providing a category helps you easily recognize activities from interesting IP addresses. Possible values include:**1**: Corporate**2**: Administrative**3**: Risky**4**: VPN**5**: Cloud provider**6**: Other |
| lastModified | long | [Timestamp](api-introduction#timestamps) of the last rule changed |

## Filters

For information about how filters work, see [Filters](api-introduction#filters).

The following table describes the supported filters:

| Filter | Type | Operators | Description |
| --- | --- | --- | --- |
| category | integer | eq, neq | Filter IP ranges by category. Possible values include:**1**: Corporate**2**: Administrative**3**: Risky**4**: VPN**5**: Cloud provider**6**: Other |
| tags | string | eq, neq | Filter IP ranges by tag IDs |
| builtIn | bool | eq | Filter IP ranges by type. Possible values include: **true** (built-in) or **false** (custom) |

If you run into any problems, we're here to help. To get assistance or support for your product issue, please [open a support ticket](/en-us/defender-xdr/contact-defender-support).