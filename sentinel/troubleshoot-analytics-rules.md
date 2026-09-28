---
layout: Conceptual
title: Troubleshooting analytics rules in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/troubleshoot-analytics-rules
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
description: Learn how to deal with certain known issues that can affect analytics rules, and understand the meaning of AUTO DISABLED.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: troubleshooting-general
ms.custom: devx-track-arm-template
ms.date: 2024-03-26T00:00:00.0000000Z
locale: en-us
document_id: 989a4c19-ddce-6018-349b-e0a8b70e9ae7
document_version_independent_id: 3e156556-c213-0693-757d-58afa2c901e7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/troubleshoot-analytics-rules.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/troubleshoot-analytics-rules
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/troubleshoot-analytics-rules.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 6504171f-b9b3-30ed-6543-cdf442e5794f
---

# Troubleshooting analytics rules in Microsoft Sentinel | Microsoft Learn

Important

[**Custom detections**](/en-us/defender-xdr/custom-detections-overview?toc=/azure/sentinel/TOC.json&amp;bc=/azure/sentinel/breadcrumb/toc.json) is now the best way to create new rules across Microsoft Sentinel SIEM Microsoft Defender XDR. With custom detections, you can reduce ingestion costs, get unlimited real-time detections, and benefit from seamless integration with Defender XDR data, functions, and remediation actions with automatic entity mapping. For more information, read [this blog](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/custom-detections-are-now-the-unified-experience-for-creating-detections-in-micr/4463875).

This article explains how to deal with certain issues that may arise with execution of [scheduled analytics rules](detect-threats-custom) in Microsoft Sentinel.

## Issue: No events appear in query results

When **event grouping** is set to **trigger an alert for each event**, query results viewed at a later time may appear to be missing, or different than expected. For example, you might view a query's results at a later time when investigating a related incident, and as part of that investigation you decide to pivot back to this query's earlier results.

Results are automatically saved with the alerts. However, if the results are too large, no results are saved, and no data appears when viewing the query results again.

In cases where there's [ingestion delay](ingestion-delay), or the query is not deterministic due to aggregation, the alert's result might be different than the result shown by running the query manually.

To solve this problem, when a rule has this event grouping setting, Microsoft Sentinel adds the **OriginalQuery** field to the results of the query. Here's a comparison of the existing **Query** field and the new field:

| Field name | Contains | Running the query in this fieldresults in... |
| --- | --- | --- |
| **Query** | The compressed record of the event that generated this instance of the alert. | The event that generated this instance of the alert;limited to 10 kilobytes. |
| **OriginalQuery** | The original query as written in the analytics rule. | The most recent event in the timeframe in which the query runs, that fits the parameters defined by the query. |

In other words, the **OriginalQuery** field behaves like the **Query** field behaves under the default event grouping setting.

## Issue: A scheduled rule failed to execute, or appears with AUTO DISABLED added to the name

It's a rare occurrence that a scheduled query rule fails to run, but it can happen. Microsoft Sentinel classifies failures up front as either transient or permanent, based on the specific type of the failure and the circumstances that led to it.

### Transient failure

A transient failure occurs due to a circumstance that's temporary and soon returns to normal, at which point the rule execution succeeds. Some examples of failures that Microsoft Sentinel classifies as transient are:

- A rule query takes too long to run and times out.
- Connectivity issues between data sources and Log Analytics, or between Log Analytics and Microsoft Sentinel.
- Any other new and unknown failure is considered transient.

In the event of a transient failure, Microsoft Sentinel continues trying to execute the rule again after predetermined and ever-increasing intervals, up to a point. After that, the rule will run again only at its next scheduled time. A rule is never autodisabled due to a transient failure.

### Permanent failure—rule autodisabled

A permanent failure occurs due to a change in the conditions that allow the rule to run, which without human intervention can't return to their former status. The following are some examples of failures that are classified as permanent:

- The target workspace (on which the rule query operated) was deleted.
- The target table (on which the rule query operated) was deleted.
- Microsoft Sentinel was removed from the target workspace.
- A function used by the rule query is no longer valid; it was either modified or removed.
- Permissions to one of the data sources of the rule query were changed (see example).
- One of the data sources of the rule query was deleted.

**In the event of a predetermined number of consecutive permanent failures, of the same type and on the same rule,** Microsoft Sentinel stops trying to execute the rule, and also takes the following steps:

1. Disables the rule.
2. Adds the words **"AUTO DISABLED"** to the beginning of the rule's name.
3. Adds the reason for the failure (and the disabling) to the rule's description.

You can easily determine the presence of any autodisabled rules, by sorting the rule list by name. The autodisabled rules are at or near the top of the list.

SOC managers should be sure to check the rule list regularly for the presence of autodisabled rules.

### Permanent failure due to resource drain

Another kind of permanent failure occurs due to an **improperly built query** that causes the rule to consume **excessive computing resources** and risks being a performance drain on your systems. When Microsoft Sentinel identifies such a rule, it takes the same three steps mentioned for the other types of permanent failures—disables the rule, prepends **"AUTO DISABLED"** to the rule name, and adds the reason for the failure to the description.

To re-enable the rule, you must address the issues in the query that cause it to use too many resources. For more information, see:

- [Query best practices - Kusto documentation](/en-us/kusto/query/best-practices?view=microsoft-sentinel&amp;preserve-view=true&amp;toc=/azure/sentinel/TOC.json&amp;bc=/azure/sentinel/breadcrumb/toc.json)
- [Optimize log queries in Azure Monitor](/en-us/azure/azure-monitor/logs/query-optimization)
- [Kusto Query Language learning resources](/en-us/kusto/query/kql-learning-resources?view=microsoft-sentinel?view=microsoft-sentinel&amp;preserve-view=true&amp;toc=/azure/sentinel/TOC.json&amp;bc=/azure/sentinel/breadcrumb/toc.json)

### Permanent failure due to lost access across subscriptions/tenants

One particular example of when a permanent failure could occur due to a permissions change on a data source (see the list) concerns the case of a Microsoft Security Solution Provider (MSSP)—or any other scenario where analytics rules query across subscriptions or tenants.

When you create an analytics rule, an access permissions token is applied to the rule and saved along with it. This token ensures that the rule can access the workspace that contains the tables referenced by the rule's query, and that this access is maintained even if the rule's creator loses access to that workspace.

There's one exception, however: when a rule is created to access workspaces in other subscriptions or tenants, such as what happens in the case of an MSSP, Microsoft Sentinel takes extra security measures to prevent unauthorized access to customer data. These kinds of rules have the credentials of the user that created the rule applied to them, instead of an independent access token. When the user no longer has access to the other tenant, the rule stops working.

If you operate Microsoft Sentinel in a cross-subscription or cross-tenant scenario, and if one of your analysts or engineers loses access to a particular workspace, any rules created by that user will stop working. You'll get a health monitoring message regarding "insufficient access to resource", and the rule will be autodisabled according to the procedure described previously.