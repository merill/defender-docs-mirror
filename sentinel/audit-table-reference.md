---
layout: Conceptual
title: Microsoft Sentinel audit tables reference | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/audit-table-reference
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
description: Learn about the fields in the SentinelAudit tables, used for audit monitoring and analysis.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: reference
ms.date: 2023-01-17T00:00:00.0000000Z
locale: en-us
document_id: ab78554a-8375-64a5-ce9f-b49bab9dfed9
document_version_independent_id: 671fae8d-848e-bcc0-50b3-12d6dc0e4173
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/audit-table-reference.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/audit-table-reference
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/audit-table-reference.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 9668a042-c66e-7ee5-f2f4-970d25d275e4
---

# Microsoft Sentinel audit tables reference | Microsoft Learn

This article describes the fields in the SentinelAudit tables, which are used for auditing user activity in Microsoft Sentinel resources. With the Microsoft Sentinel audit feature, you can keep tabs on the actions taken in your SIEM and get information on any changes made to your environment and the users that made those changes.

Learn how to [query and use the audit table](monitor-analytics-rule-integrity) for deeper monitoring and visibility of actions in your environment.

Microsoft Sentinel's audit feature currently covers only the analytics rule resource type, though other types may be added later. Many of the data fields in the following tables will apply across resource types, but some have specific applications for each type. The descriptions below will indicate one way or the other.

## SentinelAudit table columns schema

The following table describes the columns and data generated in the SentinelAudit data table:

| ColumnName | ColumnType | Description |
| --- | --- | --- |
| **TenantId** | String | The tenant ID for your Microsoft Sentinel workspace. |
| **TimeGenerated** | Datetime | The time (UTC) at which the audited activity occurred. |
| **OperationName** | String | The Azure operation being recorded. For example:- `Microsoft.SecurityInsights/alertRules/Write`- `Microsoft.SecurityInsights/alertRules/Delete` |
| **SentinelResourceId** | String | The unique identifier of the Microsoft Sentinel workspace and the associated resource on which the audited activity occurred. |
| **SentinelResourceName** | String | The resource name. For analytics rules, this is the rule name. |
| **Status** | String | Indicates `Success` or `Failure` for the OperationName. |
| **Description** | String | Describes the operation, including extended data as needed. For example, for failures, this column might indicate the failure reason. |
| **WorkspaceId** | String | The workspace GUID on which the audited activity occurred. The full Azure Resource Identifier is available in the SentinelResourceID column. |
| **SentinelResourceType** | String | The Microsoft Sentinel resource type being monitored. |
| **SentinelResourceKind** | String | The specific type of resource being monitored. For example, for analytics rules: `NRT`. |
| **CorrelationId** | String | The event correlation ID in GUID format. |
| **ExtendedProperties** | Dynamic (json) | A JSON bag that varies by the OperationName value and the Status of the event.See Extended properties for details. |
| **Type** | String | `SentinelAudit` |

## Operation names for different resource types

| Resource types | Operation names | Statuses |
| --- | --- | --- |
| **[Analytics rules](monitor-analytics-rule-integrity)** | - `Microsoft.SecurityInsights/alertRules/Write`- `Microsoft.SecurityInsights/alertRules/Delete` | SuccessFailure |

## Extended properties

### Analytics rules

Extended properties for analytics rules reflect certain [rule settings](detect-threats-custom).

| ColumnName | ColumnType | Description |
| --- | --- | --- |
| **CallerIpAddress** | String | The IP address from which the action was initiated. |
| **CallerName** | String | The user or application that initiated the action. |
| **OriginalResourceState** | Dynamic (json) | A JSON bag that describes the rule before the change. |
| **Reason** | String | The reason why the operation failed. For example: `No permissions`. |
| **ResourceDiffMemberNames** | Array[String] | An array of the properties of the rule that were changed by the audited activity. For example: `['custom_details','look_back']`. |
| **ResourceDisplayName** | String | Name of the analytics rule on which the audited activity occurred. |
| **ResourceGroupName** | String | Resource group of the workspace on which the audited activity occurred. |
| **ResourceId** | String | The resource ID of the analytics rule on which the audited activity occurred. |
| **SubscriptionId** | String | The subscription ID of the workspace on which the audited activity occurred. |
| **UpdatedResourceState** | Dynamic (json) | A JSON bag that describes the rule after the change. |
| **Uri** | String | The full-path resource ID of the analytics rule. |
| **WorkspaceId** | String | The resource ID of the workspace on which the audited activity occurred. |
| **WorkspaceName** | String | The name of the workspace on which the audited activity occurred. |