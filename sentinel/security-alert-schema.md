---
layout: Conceptual
title: Microsoft Sentinel security alert schema reference | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/security-alert-schema
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
description: This article displays the schema of security alerts in Microsoft Sentinel.
services: sentinel
cloud: na
author: guywi-ms
ms.author: guywild
ms.topic: reference
ms.date: 2022-01-11T00:00:00.0000000Z
locale: en-us
document_id: bc733f5f-a9fd-55a9-aa22-eb249c684ff0
document_version_independent_id: 18906474-1d26-a954-2094-58d539c4e84b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/security-alert-schema.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/security-alert-schema
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/security-alert-schema.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: ea96b63f-c294-4906-cea2-cbd448f3889e
---

# Microsoft Sentinel security alert schema reference | Microsoft Learn

Microsoft Sentinel [analytics rules](detect-threats-built-in) create incidents as the result of **security alerts**. Security alerts can come from different sources, and accordingly use different kinds of analytics rules to create incidents:

- **Scheduled** analytics rules generate alerts as the result of their regular queries of data in logs ingested from external sources, and those same rules create incidents from those alerts. (For the purposes of this document, "scheduled" rule alerts include **NRT rule alerts**.)
- **Microsoft Security** analytics rules create incidents from alerts that are ingested as-is from other Microsoft security products, for example, Microsoft Defender XDR and Microsoft Defender for Cloud.

Regardless of the source, these alerts are all stored together in the *SecurityAlert* table in your Log Analytics workspace. This article describes the schema of this table.

Because alerts come from many sources, not all fields are used by all providers. Some fields may be left blank.

## Schema definitions

| Column Name | Type | Description |
| --- | --- | --- |
| **AlertLink** | string | A link to the alert in the portal of the originating product. |
| **AlertName** | string | The display name of the alert. <br>- **Scheduled rule alerts:** taken from the rule name.<br>- **Ingested alerts:** the display name of the alert in the originating product. |
| **AlertSeverity** | string | The severity of the alert. [Informational / Low / Medium / High] |
| **AlertType** | string | The type of alert. <br>- **Scheduled rule alerts:** taken from the rule ID.<br>- **Ingested alerts:** some products group their alerts by type. In some cases, may be identical to or synonymous with the product name. |
| **CompromisedEntity** | string | The display name of the main entity being alerted on. |
| **ConfidenceLevel** | string | The confidence level of this alert: how sure the provider is that this is not a false positive. |
| **ConfidenceScore** | real | The confidence score of the alert, on a scale of 0.0-1.0, if applicable. This property allows for a more fine-grained representation of the confidence level of the alert compared to the ConfidenceLevel field. |
| **Description** | string | The description of the alert. |
| **DisplayName** | string | The display name of the alert. Synonymous with *AlertName* but retained for compatibility. |
| **EndTime** | datetime | The end time of the impact of the alert. <br>- **Scheduled rule alerts:** the value of the *TimeGenerated* field for the last *event* captured by the query.<br>- **Ingested alerts:** the time of the last event or activity included in the alert. |
| **Entities** | string | A list of the entities identified in the alert. This list can include a combination of entities of different types. The entities' types can be any of those defined in the schema, as described in the [entities documentation](entities-reference). |
| **ExtendedLinks** | string | A bag (a collection) for all links related to the alert. This bag can include a combination of links of different types. |
| **ExtendedProperties** | string | A collection of other properties of the alert, including user-defined properties. Any [custom details](surface-custom-details-in-alerts) defined in the alert, and any dynamic content in the [alert details](customize-alert-details), are stored here. |
| **IsIncident** | boolean | DEPRECATED. Always set to *false*. |
| **ProcessingEndTime** | datetime | The time of the alert's publishing. <br>- **Scheduled rule alerts:** the value of the *TimeGenerated* field.<br>- **Ingested alerts:** the time that the originating product completes the production of the alert. |
| **ProductComponentName** | string | The name of the component of the product that generated the alert. |
| **ProductName** | string | The name of the product that generated the alert. |
| **ProviderName** | string | The name of the alert provider (the service within the product) that generated the alert. |
| **RemediationSteps** | string | A list of action items to take to remediate the alert. |
| **ResourceId** | string | A unique identifier for the resource that is the subject of the alert. |
| **SourceComputerId** | string | DEPRECATED. Was the agent ID on the server that created the alert. |
| **SourceSystem** | string | DEPRECATED. Always populated with the string "Detection". |
| **StartTime** | datetime | The start time of the impact of the alert. <br>- **Scheduled rule alerts:** the value of the *TimeGenerated* field for the first *event* captured by the query.<br>- **Ingested alerts:** the time of the first event or activity included in the alert. |
| **Status** | string | The status of the alert within the life cycle. [New / InProgress / Resolved / Dismissed / Unknown] |
| **SystemAlertId** | string | The internal unique ID for the alert in Microsoft Sentinel. |
| **Tactics** | string | A comma-delineated list of MITRE ATT&CK tactics associated with the alert. |
| **Techniques** | string | A comma-delineated list of MITRE ATT&CK techniques associated with the alert. |
| **TenantId** | string | The unique ID of the tenant. |
| **TimeGenerated** | datetime | The time the alert was generated (in UTC). |
| **Type** | string | The constant ('SecurityAlert') |
| **VendorName** | string | The vendor of the product that produced the alert. |
| **VendorOriginalId** | string | Unique ID for the specific alert instance, set by the originating product. |
| **WorkspaceResourceGroup** | string | DEPRECATED |
| **WorkspaceSubscriptionId** | string | DEPRECATED |