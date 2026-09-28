---
layout: Conceptual
title: Handle Ingestion Delay in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/ingestion-delay
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
description: Handle ingestion delay in Microsoft Sentinel scheduled analytics rules.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: f513fb85-2173-d379-962a-5d14f77ece7f
document_version_independent_id: 49d03e8f-37e4-e936-3205-71ae63183976
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/ingestion-delay.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/ingestion-delay
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/ingestion-delay.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: ba21aaa5-e770-4f7d-a613-c4e2509f8e25
---

# Handle Ingestion Delay in Microsoft Sentinel | Microsoft Learn

Important

[**Custom detections**](/en-us/defender-xdr/custom-detections-overview?toc=/azure/sentinel/TOC.json&amp;bc=/azure/sentinel/breadcrumb/toc.json) is now the best way to create new rules across Microsoft Sentinel SIEM Microsoft Defender XDR. With custom detections, you can reduce ingestion costs, get unlimited real-time detections, and benefit from seamless integration with Defender XDR data, functions, and remediation actions with automatic entity mapping. For more information, read [Custom detections are now the unified experience for creating detections in Microsoft Defender XDR](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/custom-detections-are-now-the-unified-experience-for-creating-detections-in-micr/4463875).

Although Microsoft Sentinel can ingest data from [connected data sources](connect-data-sources), ingestion time for each data source might differ in different circumstances.

This article describes how ingestion delay might impact your scheduled analytics rules and how you can fix them to cover these gaps.

## Why delay is significant

For example, you might write a custom detection rule, setting the **Run query every** and **Lookup data from the last** fields to have the rule run every five minutes, looking up data from those last five minutes:

![Screenshot showing the Analytics Rule Wizard - Create new rule window.](media/ingestion-delay/create-rule.png)

The **Lookup data from the last** field defines a setting known as a *look-back* period. Ideally, when there's no delay, this detection misses no events, as shown in the following diagram:

![Diagram showing a five-minute look-back window.](media/ingestion-delay/look-back.png)

The event arrives as it's generated, and is included in the *lookback* period.

Now, assume there's some delay for your data source. For this example, let's say the event was *ingested* two minutes after it was *generated*. The delay is two minutes:

![Diagram showing five-minute look back windows with a delay of two minutes.](media/ingestion-delay/look-back-delay.png)

The event is generated within the first look-back period, but isn't ingested in your Microsoft Sentinel workspace on the first run. The next time the scheduled query runs, it ingests the event, but the time-generated filter removes the event because it happened more than five minutes ago. In this case, **the rule does not fire an alert**.

## How to handle delay

Use the following approach to account for ingestion delay in scheduled analytics rules.

Note

You can either solve the issue using the process described below, or implement Microsoft Sentinel's near-real-time detection (NRT) rules. For more information, see [Detect threats quickly with near-real-time (NRT) analytics rules in Microsoft Sentinel](near-real-time-rules).

To solve the issue, you need to know the delay for your data type. For this example, you already know the delay is two minutes.

For your own data, you can understand delay using the Kusto `ingestion_time()` function, and calculating the difference between **TimeGenerated** and the ingestion time. For more information, see Calculate ingestion delay.

After determining the delay, you can address the problem as follows:

- **Increase the look-back period**: Basic intuition tells you that increasing the look-back period size will help. Since your look-back period is five minutes and your delay is two minutes, setting the look-back period to *seven* minutes will help address this problem. For example, in your rule settings:

    ![Screenshot that shows setting the look-back window to seven minutes.](media/ingestion-delay/set-look-back.png)

    The following diagram shows how the look-pack period now contains the missed event:

    ![Diagram that shows seven-minute look back windows with a delay of two minutes.](media/ingestion-delay/longer-look-back.png)
- \**Handle duplication*:. Only increasing the look-back period can create duplication, because the look-back windows now overlap. For example, a different event may look as shown in the following diagram:

    ![Diagram showing how overlapping look-back windows create duplication.](media/ingestion-delay/overlapping-look-back.png)

    Because the event **TimeGenerated** value is found in both look-back periods, the event fires two alerts. You need to find a way to solve the duplication.
- **Associate the event to a specific look-back period**: In the first example, you missed events because your data wasn't ingested when the scheduled query ran. You extended the look-back to include the event, but this caused duplication. You have to associate the event to the window you extended to contain it.

    Do this by setting `ingestion_time() > ago(5m)`, instead of the original rule `look-back = 5m`. This setting associates the event to the first look-back window. For example:

    ![Diagram showing how setting the ago restriction avoids duplication.](media/ingestion-delay/ago-restriction.png)

    The ingestion time restriction now trims the extra two minutes you added to the look-back period. And for the first example, the second run look-back period now captures the event:

    ![Diagram showing how setting the ago restriction captures the event.](media/ingestion-delay/ago-restriction-capture.png)

The following sample query summarizes the solution for solving ingestion delay issues:

```kusto
let ingestion_delay = 2min;
let rule_look_back = 5min;
CommonSecurityLog
| where TimeGenerated >= ago(ingestion_delay + rule_look_back)
| where ingestion_time() > ago(rule_look_back)
```

See more information on the following items used in the preceding example in the Kusto documentation:

- [***let*** statement](/en-us/kusto/query/let-statement?view=microsoft-sentinel&amp;preserve-view=true)
- [***where*** operator](/en-us/kusto/query/where-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***ago()*** function](/en-us/kusto/query/ago-function?view=microsoft-sentinel&amp;preserve-view=true)

## Calculate ingestion delay

By default, Microsoft Sentinel scheduled alert rules are configured to have a five-minute look-back period. However, each data source might have its own, individual ingestion delay. When joining multiple data types, you must understand the different delays for each data type in order to configure the look-back period correctly.

The **Workspace Usage Report**, provided in Microsoft Sentinel out-of-the-box, includes a dashboard that shows latency and delays for the different data types flowing into your workspace.

For example:

![Screenshot of the Workspace Usage Report showing End to End Latency by table](media/ingestion-delay/end-to-end-latency.png)