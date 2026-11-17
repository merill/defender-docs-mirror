---
layout: Conceptual
title: Manually convert Microsoft Sentinel analytics rules to custom detections | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/transition-custom-detections
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
ms.service: microsoft-defender
ms.subservice: unified-security-operations
search.appverid: met150
description: Learn how to manually convert Microsoft Sentinel analytics rules to Microsoft Defender custom detections and validate the replacement detections.
author: guywi-ms
ms.author: guywild
ms.date: 2026-10-07T00:00:00.0000000Z
ms.collection:
- M365-security-compliance
- tier1
- usx-security
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1030
locale: en-us
document_id: 8b69b7d4-be0f-0e4e-5143-788cfda381f0
document_version_independent_id: fa983a44-237e-d9b0-1506-6ec3da4d547f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/transition-custom-detections.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/transition-custom-detections
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/transition-custom-detections.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: fa86a0a0-8822-0c33-fd20-4116a28f9096
---

# Manually convert Microsoft Sentinel analytics rules to custom detections | Microsoft Learn

When you transition to using Microsoft Defender XDR data directly, you can convert Microsoft Sentinel analytics rules to Microsoft Defender custom detections.

For eligible analytics rules identified in SOC optimization recommendations, you can use the [automatic migration tool](transition-custom-detections-automatic). For rules that aren't eligible for automatic migration, or when you need to recreate rules outside the supported migration workflow, follow the guidance in this article to convert them manually.

Some analytics rule capabilities work differently in custom detections and require changes to the rule configuration or query. Other capabilities don't have direct custom detection equivalents and might require you to redesign the detection scenario.

Before you retire an analytics rule, review the differences described in this article and validate the replacement custom detection.

## Differences between analytics rules and custom detections

The following table summarizes the main differences to consider when converting analytics rules to custom detections.

| Area | What changes | Custom detection support |
| --- | --- | --- |
| Rule scheduling and execution | Microsoft Defender XDR-based rules use fixed frequency and lookback options. | Partial |
| Alerts, incidents, and correlation | Grouping and correlation are handled centrally and are based on mapped entities instead of per-rule configuration. | Partial |
| Automation, tuning, and suppression | Recreate automation by using alert-triggered automation. Handle tuning and suppression in the query or through automation. | Partial |
| Detection queries and functions | Recreate custom functions in Advanced Hunting. Nested functions and cross-workspace queries aren't supported. | Partial |
| Alert content and entities | Custom detections support one tactic and one identifier per entity. Dynamic values are supported for alert titles and descriptions. | Partial |
| Multi-workspace and MSSP scenarios | Custom detections don't support cross-workspace queries, secondary-workspace detections, or query isolation. | Not supported |
| Monitoring, health, and auditing | Use custom detection run status and `CloudAppEvents` audit data instead of Microsoft Sentinel health data and workbooks. | Partial |
| Managing rules programmatically | Custom detection APIs and Bicep support are in preview. Existing analytics rules and ARM templates can't be imported directly as custom detections. New Content Hub solutions can include custom detection counterparts to analytics rules. | Preview |

## Update rule scheduling and execution

When you recreate an analytics rule as a custom detection, review its scheduling, execution, and near-real-time configuration.

| Analytics rule capability | In custom detections | What to do |
| --- | --- | --- |
| Frequency from 5 minutes to 14 days | Supported scheduling options are **Continuous (NRT)**, **Hourly**, **Every 3 hours**, **Every 12 hours**, and **Every 24 hours**. | Recreate the rule by using the closest supported frequency. |
| Flexible lookback | The lookback period is automatically determined by the selected frequency. For example, an hourly detection evaluates the previous four hours of data. | Select the closest supported frequency. The corresponding lookback window is applied automatically. |
| Near-real-time (NRT) | Continuous detections support only specific single-table queries and a limited set of KQL operators. | If the query and tables are supported, use **Continuous (NRT)**. Otherwise, use a scheduled detection. |
| NRT with enrichment, such as watchlists | Continuous detections use a limited KQL set, so lookups can't run as part of a continuous detection. | Remove the enrichment to use a continuous detection, or keep the enrichment and use a scheduled detection. |
| Delayed first run | Custom detections don't provide start-time control. When you save a custom detection, it initially evaluates the previous 30 days of data and then continues at the selected frequency. | Plan for the initial evaluation and any alerts it might generate. |
| On-demand rerun over a previous time window | Custom detections don't support arbitrary reruns. Each run evaluates the predefined lookback associated with the selected frequency. | Use the default lookback. Late-arriving events are evaluated automatically and duplicate alerts are prevented. |

## Review alert grouping and incident correlation

Microsoft Defender handles alert grouping and incident correlation centrally by using the entities, assets, and evidence associated with alerts.

When converting an analytics rule, consider the following differences:

- **Automatic event grouping**: Custom detections can group and deduplicate related events. Events that share the same assets and evidence might be combined into a single alert.
- **One alert for all matching events**: Custom detections don't provide a rule setting that explicitly generates one alert for all matching events. Grouping is determined by the Microsoft Defender correlation engine.
- **Correlation configuration**: Settings for excluding alerts from correlation, creating alerts without incidents, and configuring alert or incident grouping don't have direct equivalents in custom detections. Correlation uses mapped entities to group related alerts and incidents.
- **Alert thresholds**: Custom detections don't provide a rule-level alert threshold. Add threshold logic directly to the KQL query instead.

For example, the following query generates results only when an account has more than five failed sign-in events:

```kusto
DeviceLogonEvents
| where Timestamp > ago(1h)
| where ActionType == "LogonFailed"
| summarize FailedCount = count() by AccountName, DeviceName
| where FailedCount > 5
```

## Recreate automation, tuning, and suppression

Recreate automation by using alert-triggered automation in Microsoft Defender. Handle tuning and suppression through KQL filtering and automation instead of analytics rule settings.

Consider the following differences:

- **Alert-triggered automation and playbooks**: After you create the custom detection, recreate any required alert-triggered automation in Microsoft Defender.
- **Incident automation based on a rule**: You can't currently use a custom detection as a condition in an incident-triggered automation rule.
- **In-rule suppression**: Custom detections don't have a direct equivalent to the analytics rule **Stop running query after alert is generated** behavior. Reduce noise by refining the detection query and using automation to resolve known-benign alerts.
- **Alert tuning and suppression rules**: Custom detection alerts don't currently have a direct equivalent. Use query filtering and automation-based resolution where needed.

## Update detection queries and functions

Custom detections run against Advanced Hunting data and use Advanced Hunting functions.

Review the following query differences when converting a rule:

- **ASIM parsers**: Built-in unifying parsers, such as `_Im_<schema>`, can be used directly in custom detection queries.
- **Custom functions**: Recreate Microsoft Sentinel workspace functions as Advanced Hunting functions and save them under **Shared functions** or **My functions**. Functions stored only in the Microsoft Sentinel workspace aren't available to custom detections.
- **Cross-workspace queries**: The `workspace()` operator isn't supported. Rewrite the query to use local Advanced Hunting tables. If the required data isn't available locally, redesign the detection or continue using the analytics rule.
- **Nested functions**: Advanced Hunting functions can't call other functions. Combine nested function logic into a single function or directly into the detection query.
- **Function scope**: After a function is used by a custom detection, you can't modify the function to broaden its data scope. Create a new function instead.

## Recreate alert content and entity mappings

Review MITRE ATT&CK mappings, entity identifiers, and dynamic alert content when you recreate a rule.

- **MITRE ATT&CK mapping**: Custom detections support one tactic per rule. Select the most relevant tactic, or create separate custom detections when different tactics need to be represented.
- **Entity identifiers**: Custom detections map one query column per entity type. If an analytics rule maps multiple identifiers for the same entity, recreate the required mappings individually.
- **Dynamic alert properties**: Custom detections support dynamic values in the alert title and description. You can reference up to three query columns in each field by using `{{Column}}`.
- **Additional runtime values**: Add other values returned by the query as **Custom details**.

For example:

```text
Alert title:
User {{AccountName}} signed in from {{Location}}

Custom details:
SignInCount = TotalSignIns
```

Custom details support up to 20 key-value pairs and a maximum of 4 KB per alert.

## Review multi-workspace scenarios

Custom detections don't provide direct equivalents for some Microsoft Sentinel multi-workspace scenarios.

Before converting a rule, determine whether it depends on:

- Cross-workspace queries that use `workspace()`.
- Data that is available only in a secondary Microsoft Sentinel workspace.
- Query isolation or similar MSSP-specific behavior.

If the required data isn't available to Advanced Hunting in the tenant, redesign the detection scenario or keep the existing analytics rule.

## Monitor custom detection health and auditing

Monitoring for custom detections differs from analytics rule monitoring in Microsoft Sentinel.

- **Rule health**: Review run status and execution details in the custom detection experience. Custom detections don't provide an equivalent Microsoft Sentinel health-log history or Advanced Hunting health table.
- **Rule audit trail**: Custom detection audit information is available in the `CloudAppEvents` table. Use this data for reporting, investigations, or detections that monitor rule changes.
- **Health and quality workbooks**: Microsoft Sentinel health workbooks don't monitor custom detections. Use the custom detection health experience and `CloudAppEvents` audit data instead.

For example:

```kusto
CloudAppEvents
| where Timestamp > ago(7d)
| where ActionType has "detection" or ActionType has "rule"
| project Timestamp, AccountDisplayName, ActionType, RawEventData
```

## Manually convert and validate analytics rules

If you can't migrate an analytics rule automatically, recreate it as a custom detection and validate its behavior before retiring the original rule.

Before converting a rule, verify that it doesn't depend on functionality without a direct custom detection equivalent, such as cross-workspace queries, secondary-workspace detections, correlation opt-out, alerts without incidents, or query isolation.

To manually convert and validate an analytics rule:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Recreate the rule as a custom detection from Advanced Hunting or from the custom detection experience. Rewrite any `workspace()` or nested-function logic first.
3. Reproduce the entity mappings. Map one identifier per entity type. If the analytics rule used multiple identifiers for an entity, recreate each required mapping.
4. Rebuild the alert content. Recreate dynamic alert titles and descriptions, and move other runtime values to **Custom details**.
5. Recreate any required alert-triggered automation in Microsoft Defender.
6. Run the KQL query in Advanced Hunting and validate the results, entity mappings, alert content, frequency, and lookback period.
7. After the custom detection is validated, disable the original analytics rule.
8. Remove the analytics rule when you're confident that the replacement custom detection is working as expected.

## Manage converted rules programmatically

If your organization manages detections as code or at scale, review the automation and deployment processes that currently manage Microsoft Sentinel analytics rules.

- **CI/CD pipelines**: Update source-control and deployment pipelines so they can deploy and manage custom detections and Advanced Hunting-based content.
- **Infrastructure as code and import/export**: Current custom detection automation capabilities depend on the preview API. Analytics rule ARM templates can't be imported directly into custom detections. The automatic migration tool provides a separate conversion workflow for eligible rules. Otherwise, recreate the rules by using the custom detection experience or API.
- **Rule-template API**: Custom detections don't have an equivalent to the Microsoft Sentinel Analytics Rules template catalog API (`alertRuleTemplates`).
- **Create rules from Content Hub**: New Content Hub solutions can include custom detection counterparts to Microsoft Sentinel analytics rules. When a solution includes supported custom detections, they're installed as part of the solution deployment. For existing analytics rules that don't have a custom detection counterpart, use the automatic migration tool when eligible, or recreate the required detections manually.