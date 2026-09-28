---
layout: Conceptual
title: Microsoft Sentinel health tables reference | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/health-table-reference
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
description: Learn about the fields in the SentinelHealth tables, used for health monitoring and analysis.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: reference
ms.date: 2025-08-20T00:00:00.0000000Z
locale: en-us
document_id: 272ba48b-8d6d-7aef-fc91-8d95a2433a46
document_version_independent_id: 36dddfd9-e817-7ac1-f266-a88fc3fbc935
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/health-table-reference.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/health-table-reference
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/health-table-reference.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
platformId: 5f230b91-9590-eca2-c460-e5338725b7f3
---

# Microsoft Sentinel health tables reference | Microsoft Learn

This article describes the fields in the *SentinelHealth* table used for monitoring the health of Microsoft Sentinel resources. With the Microsoft Sentinel [health monitoring feature](health-audit), you can keep tabs on the proper functioning of your SIEM and get information on any health drifts in your environment.

Learn how to query and use the health table for deeper monitoring and visibility of actions in your environment:

- For [data connectors](monitor-data-connector-health)
- For [automation rules and playbooks](monitor-automation-health)
- For [analytics rules](monitor-analytics-rule-integrity)

Microsoft Sentinel's health monitoring feature covers different kinds of resources (see the resource types in the **SentinelResourceType** field in the first table below). Many of the data fields in the following tables apply across resource types, but some have specific applications for each type. The descriptions below will indicate one way or the other.

## SentinelHealth table columns schema

The following table describes the columns and data generated in the SentinelHealth data table:

| ColumnName | ColumnType | Description |
| --- | --- | --- |
| **TenantId** | String | The tenant ID for your Microsoft Sentinel workspace. |
| **TimeGenerated** | Datetime | The time (UTC) at which the health event occurred. |
| **OperationName** | String | The health operation. Possible values depend on the resource type.See Operation names for different resource types for details. |
| **SentinelResourceId** | String | The unique identifier of the resource on which the health event occurred, and its associated Microsoft Sentinel workspace. |
| **SentinelResourceName** | String | The name of the resource (connector, rule, or playbook). |
| **Status** | String | Indicates the overall result of the operation. Possible values depend on the operation name.See Operation names for different resource types for details. |
| **Description** | String | Describes the operation, including extended data as needed. For failures, this can include details of the failure reason. |
| **Reason** | Enum | Shows a basic reason or error code for the failure of the resource. Possible values depend on the resource type. More detailed reasons can be found in the **Description** field. |
| **WorkspaceId** | String | The workspace GUID on which the health issue occurred. The full Azure Resource Identifier is available in the SentinelResourceID column. |
| **SentinelResourceType** | String | The Microsoft Sentinel resource type being monitored.Possible values: `Data connector`, `Automation rule`, `Playbook`, `Analytics rule` |
| **SentinelResourceKind** | String | A resource classification within the resource type.- For data connectors, this is the type of connected data source.- For analytics rules, this is the type of rule. |
| **RecordId** | String | A unique identifier for the record that can be shared with the support team for better correlation as needed. |
| **ExtendedProperties** | Dynamic (json) | A JSON bag that varies by the OperationName value and the Status of the event.See Extended properties for details. |
| **Type** | String | `SentinelHealth` |

## Operation names for different resource types

| Resource types | Operation names | Statuses |
| --- | --- | --- |
| **[Data collectors](monitor-data-connector-health)** | Data fetch status change\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_Data fetch failure summary | SuccessFailure\_\_\_\_\_\_\_\_\_\_\_\_\_Informational |
| **[Automation rules](monitor-automation-health)** | Automation rule run | SuccessPartial successFailure |
| **[Playbooks](monitor-automation-health)** | Playbook was triggered | SuccessFailure |
| **[Analytics rules](monitor-analytics-rule-integrity)** | Scheduled analytics rule runNRT analytics rule run | SuccessFailure |

## Extended properties

### Data connectors

For `Data fetch status change` events with a success indicator, the bag contains a ‘DestinationTable’ property to indicate where data from this resource is expected to land. For failures, the contents vary depending on the failure type.

### Automation rules

| ColumnName | ColumnType | Description |
| --- | --- | --- |
| **ActionsTriggeredSuccessfully** | Integer | Number of actions the automation rule successfully triggered. |
| **IncidentName** | String | The resource ID of the Microsoft Sentinel incident on which the rule was triggered. |
| **IncidentNumber** | String | The sequential number of the Microsoft Sentinel incident as shown in the portal. |
| **TotalActions** | Integer | Number of actions configured in this automation rule. |
| **TriggeredOn** | String | `Alert` or `Incident`. The object on which the rule was triggered. |
| **TriggeredPlaybooks** | Dynamic (json) | A list of playbooks this automation rule triggered successfully.Each playbook record in the list contains:- **RunId:** The run ID for this triggering of the Logic Apps workflow- **WorkflowId:** The unique identifier (full ARM resource ID) of the Logic Apps workflow resource. |
| **TriggeredWhen** | String | `Created` or `Updated`. Indicates whether the rule was triggered due to the creation or updating of an incident or alert. |

### Playbooks

| ColumnName | ColumnType | Description |
| --- | --- | --- |
| **IncidentName** | String | The resource ID of the Microsoft Sentinel incident on which the rule was triggered. |
| **IncidentNumber** | String | The sequential number of the Microsoft Sentinel incident as shown in the portal. |
| **RunId** | String | The run ID for this triggering of the Logic Apps workflow. |
| **TriggeredByName** | Dynamic (json) | Information on the identity (user or application) that triggered the playbook. |
| **TriggeredOn** | String | `Incident`. The object on which the playbook was triggered.(Playbooks using the alert trigger are logged only if they're called by automation rules, so those playbook runs will appear in the **TriggeredPlaybooks** extended property under automation rule events.) |

### Analytics rules

Extended properties for analytics rules reflect certain [rule settings](detect-threats-custom).

| ColumnName | ColumnType | Description |
| --- | --- | --- |
| **AggregationKind** | String | The event grouping setting. `AlertPerResult` or `SingleAlert`. |
| **AlertsGeneratedAmount** | Integer | The number of alerts generated by this running of the rule. |
| **CorrelationId** | String | The event correlation ID in GUID format. |
| **EntitiesDroppedDueToMappingIssuesAmount** | Integer | The number of entities dropped due to mapping issues. |
| **EntitiesGeneratedAmount** | Integer | The number of entities generated by this running of the rule. |
| **Issues** | String |  |
| **QueryEndTimeUTC** | Datetime | The UTC time the query began to run. |
| **QueryFrequency** | Datetime | Value of the "Run query every" setting (HH:MM:SS). |
| **QueryPerformanceIndicators** | String |  |
| **QueryPeriod** | Datetime | Value of the "Lookup data from the last" setting (HH:MM:SS). |
| **QueryResultAmount** | Integer | The number of results captured by the query.The rule will generate an alert if this number exceeds the threshold as defined below. |
| **QueryStartTimeUTC** | Datetime | The UTC time the query completed its run. |
| **RuleId** | String | The rule ID for this analytics rule. |
| **SuppressionDuration** | Time | The rule suppression duration (HH:MM:SS). |
| **SuppressionEnabled** | String | Is rule suppression enabled. `True/False`. |
| **TriggerOperator** | String | The operator portion of the threshold of results required to generate an alert. |
| **TriggerThreshold** | Integer | The number portion of the threshold of results required to generate an alert. |
| **TriggerType** | String | The type of rule being triggered. `Scheduled` or `NrtRun`. |