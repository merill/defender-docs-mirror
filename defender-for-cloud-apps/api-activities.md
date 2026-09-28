---
layout: Conceptual
title: Activities API - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/api-activities
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
description: This article provides information about using the Activities API.
ms.date: 2023-01-29T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: de775bf0-6c3a-5ac7-18a4-e2d7ccffe1c5
document_version_independent_id: de775bf0-6c3a-5ac7-18a4-e2d7ccffe1c5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/api-activities.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-activities
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/api-activities.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: e4e09f00-2de1-97ba-8da3-83b537475cff
---

# Activities API - Microsoft Defender for Cloud Apps | Microsoft Learn

The Activity API gives you visibility into all actions performed in your cloud apps. The data from this API can supply information regarding who logs in to which app and when, which files are being downloaded from suspicious locations, and so on.

The following lists the supported requests:

- [List activities](api-activities-list)
- [Fetch activity](api-activities-fetch)
- [Feedback on activity](api-activities-feedback)

## Filters

For information about how filters work, see [Filters](api-introduction#filters).

The following table describes the supported filters:

| Filter | Type | Operators | Description |
| --- | --- | --- | --- |
| service | integer | eq, neq | Filter activities related to the specified service appID, for example: 11770 |
| instance | integer | eq, neq | Filter activities from specified instances |
| user.orgUnit | string | eq, neq, isset, isnotset | Filter activities by the organization unit of the performing user |
| actionType | string | Contains, eq, neq, isset, isnotset | Filter activities by more specific action type |
| activity.eventActionType | string | eq, neq | Filter activities by event type |
| activity.id | string | eq | Find an activity by ID |
| activity.impersonated | boolean | eq | If set to *true*, returns only impersonated events, if set to *false*, returns nonimpersonated events |
| actionType | string | Contains, eq, neq, isset, isnotset | Filter activities by more specific action type |
| activity.type | boolean | eq | If set to *true*, returns only admin events, if set to *false*, returns regular events |
| activity.takenAction | string | eq, neq | Filter activities by the actions taken on them. Possible values include:**block**: Blocked**proxy**: Redirected to session control**BypassProxy**: Bypass session control**encrypt**: Encrypted**decrypt**: Decrypted**verified**: Verified**encryptionFailed**: Encryption failed**protect**: Protected**verify**: Require step-up authentication**null**: No action |
| device.type | string | eq, neq | Filter activities by device type. Possible values include:**DESKTOP**: PC**MOBILE**: Mobile**TABLET**: Tablet**OTHER**: Other**null**: No value |
| device.tags | string | eq, neq | Filter activities by device tag IDs |
| userAgent.userAgent | string | contains, ncontains | Filter activities that do or don't contain the given strings in the user agent |
| userAgent.tags | string | eq, neq | Filter activities containing the specified user agent tag IDs |
| location.country | string | eq, neq, isset, isnotset | Filter activities originating from the specified country/region code |
| location.organizations | string | eq, neq, isset, isnotset, contains | Filter activities originating from the specified organization |
| ip.address | string | eq, startswith, doesnotstartwith, isset, isnotset, neq | Filter activities originating from the given IP address |
| fileSelector | file | eq, neq | Filter activities containing the specified file/folder |
| office365url | string | startswith, eq, endswith | Filter activities by Microsoft 365 URLs |
| fileId | string | eq | Find a file by ID |
| ip.category | integer | eq, neq | Filter activities with the specified subnet categories. Possible values include:**1**: Corporate**2**: Administrative**3**: Risky**4**: VPN**5**: Cloud provider**6**: Other |
| ip.tags | string | eq, neq | Filter activities by IP tag IDs |
| text | string | eq, startswithsingle, text | Filter activities by performing a free text search |
| date | [timestamp](api-introduction#timestamps) | lte, gte, range, lte\_ndays, gte\_ndays | Filter activities that occurred in the specified time range |
| policy | string | eq, neq, isset, isnotset | Filter activities related to the specified policies |
| source | string | eq, neq | Filter all activities by source type or stream ID. Example: `[{ "s:stream-id", "t:source-type" }]` Possible source type values include:**0**: Access control**1**: Session control**2**: App connector**3**: App connector analysis**5**: Discovery**6**: MDATP |
| activity.alertId | string | eq | Filter all activities relevant to an alert ID |
| activityObject | string | eq, neq | Filter activities containing the specified ID |
| created |  | lte, gte, range, gt, lt, eq | Filter activities that were created in the specified time range |
| entity | entity pk | eq, neq, isset, isnotset, startswith | Filter activities by the entity who performed the activity. Example: `[{ "id": "entity-id", "inst": 0 }]` |
| user.username | string | eq, neq, isset, isnotset, startswith | Filter activities by the user who performed the activity |
| user.tags | string | eq, neq, isset, isnotset, startswith | Filter activities by tags belonging to the performing user. Requires group IDs |
| user.domain | string | eq, neq, isset, isnotset | Filter activities by the performing user domain |

If you run into any problems, we're here to help. To get assistance or support for your product issue, please [open a support ticket](/en-us/defender-xdr/contact-defender-support).