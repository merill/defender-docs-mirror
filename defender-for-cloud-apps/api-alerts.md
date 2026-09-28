---
layout: Conceptual
title: Alerts API - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/api-alerts
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
description: This article provides information about using the Alerts API.
ms.date: 2023-01-29T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: 9b7a3349-c966-8e65-7812-1c15cc43efe8
document_version_independent_id: 9b7a3349-c966-8e65-7812-1c15cc43efe8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/api-alerts.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/api-alerts.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 43e3e106-b2e1-7562-9063-d6b9a4d8c159
---

# Alerts API - Microsoft Defender for Cloud Apps | Microsoft Learn

The Alerts API provides you with information about immediate risks identified by Defender for Cloud Apps that require attention. Alerts can result from suspicious usage patterns or from files containing content that violates company policy.

The following lists the supported requests:

- [List alerts](api-alerts-list)
- [Close benign](api-alerts-close-benign)
- [Close false positive](api-alerts-close-false-positive)
- [Close true positive](api-alerts-close-true-positive)
- [Fetch alert](api-alerts-fetch)
- [Mark alert as read](api-alerts-mark-read)
- [Mark alert as unread](api-alerts-mark-unread)

## Deprecated requests

The following table lists the requests deprecated as obsolete, and the requests that replace them.

| Obsolete request | Alternative |
| --- | --- |
| Bulk dismiss | [Close false positive](api-alerts-close-false-positive) |
| Bulk resolve | [Close true positive](api-alerts-close-true-positive) |
| Dismiss alert | [Close false positive](api-alerts-close-false-positive) |

Note

The deprecated requests have been mapped to their alternatives to avoid disruption. However, if you're using obsolete requests in your environment, we recommend updating them to their alternatives.

## Properties

The response object defines the following properties.

| Property | Type | Description |
| --- | --- | --- |
| \_id | int | Alert type identifier |
| timestamp | long | [Timestamp](api-introduction#timestamps) of when the alert was raised |
| entities | list | A list of entities related to the alert |
| title | string | The title of the alert |
| description | string | The alert's description |
| isMarkdown | bool | Flag to indicate if the alert's description is already in HTML |
| statusValue | int | The alert's state. Possible values include:**0**: UNREAD**1**: READ**2**: ARCHIVED |
| severityValue | int | The alert's severity. Possible values include:**0**: LOW**1**: MEDIUM**2**: HIGH**3**: INFORMATIONAL |
| resolutionStatusValue | int | Alert's status. Possible values include:**0**: OPEN**1**: DISMISSED**2**: RESOLVED**3**: FALSE\_POSITIVE**4**: BENIGN**5**: TRUE\_POSITIVE |
| stories | list | Risk category. Possible values include:**0**: THREAT\_DETECTION**1**: PRIVILEGED\_ACCOUNT\_MONITORING**2**: COMPLIANCE**3**: DLP**4**: DISCOVERY**5**: SHARING\_CONTROL**7**: ACCESS\_CONTROL**8**: CONFIGURATION\_MONITORING |
| evidence | list | List of short descriptions of main parts of the alert |
| intent | list | A field that specifies the kill chain related intent behind the alert. Multiple values can be reported in this field. The **intent** enumeration values follow the [MITRE att@ck enterprise matrix model](https://attack.mitre.org/matrices/enterprise/). Further guidance on the different techniques that make up each intent can be found in MITRE's documentation. Possible values include:**0**: UNKNOWN**1**: PREATTACK**2**: INITIAL\_ACCESS**3**: PERSISTENCE**4**: PRIVILEGE\_ESCALATION**5**: DEFENSE\_EVASION**6**: CREDENTIAL\_ACCESS**7**: DISCOVERY**8**: LATERAL\_MOVEMENT**9**: EXECUTION**10**: COLLECTION**11**: EXFILTRATION**12**: COMMAND\_AND\_CONTROL**13**: IMPACT |
| isPreview | bool | Alerts that have been recently released as GA |
| audits *(optional)* | list | List of event IDs that are related to the alert |

## Filters

For information about how filters work, see [Filters](api-introduction#filters).

The following table describes the supported filters:

| Filter | Type | Operators | Description |
| --- | --- | --- | --- |
| entity.entity | entity pk | eq,neq | Filter alerts related to specified entities. Example: `[{ "id": "entity-id", "inst": 0 }]` |
| entity.ip | string | eq, neq | Filter alerts related to specified IP addresses |
| entity.service | integer | eq, neq | Filter alerts related to the specified service appId, e.g: 11770 |
| entity.instance | integer | eq, neq | Filter alerts related to the specified instances, e.g: 11770, 1059065 |
| entity.policy | string | eq, neq | Filter alerts related to the specified policies |
| entity.file | string | eq, neq | Filter alerts related to specified file |
| alertOpen | boolean | eq | If set to *true*, returns only open alerts, if set to *false*, returns only closed alerts |
| severity | integer | eq, neq | Filter by severity. Possible values include:**0**: Low**1**: Medium**2**: High |
| resolutionStatus | integer | eq, neq | Filter by alert resolution status, possible values include:**0**: Open **1**: Dismissed (legacy status)**2**: Resolved (legacy status)**3**: Closed as false positive**4**: Closed as benign**5**: Closed as true positive |
| read | boolean | eq | If set to *true*, returns only read alerts, if set to *false*, returns unread alerts |
| date | timestamp | lte, gte, range, lte\_ndays, gte\_ndays | Filter by the time when an alert was triggered |
| resolutionDate | timestamp | lte, gte, range | Filter by the time when an alert was resolved |
| risk | integer | eq, neq | Filter by risk |
| alertType | integer | eq, neq | Filter by alert type |
| ID | string | eq, neq | Filter by alert IDs |
| source | string | eq | The alert's origin, either built-in or policy |

If you run into any problems, we're here to help. To get assistance or support for your product issue, please [open a support ticket](/en-us/defender-xdr/contact-defender-support).