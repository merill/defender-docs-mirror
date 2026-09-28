---
layout: Conceptual
title: Quick threat detection with near-real-time (NRT) analytics rules in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/near-real-time-rules
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
description: This article explains how the new near-real-time (NRT) analytics rules can help you detect threats quickly in Microsoft Sentinel.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: concept-article
ms.date: 2024-05-28T00:00:00.0000000Z
locale: en-us
document_id: 0506d3a2-4757-e93d-8c64-21bff9221c21
document_version_independent_id: abb04804-e394-4238-7715-2ba253fcf5a9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/near-real-time-rules.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/near-real-time-rules
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/near-real-time-rules.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 9089be6c-36da-c72c-a0d4-f56558beab3b
---

# Quick threat detection with near-real-time (NRT) analytics rules in Microsoft Sentinel | Microsoft Learn

When you're faced with security threats, time and speed are of the essence. You need to be aware of threats as they materialize so you can analyze and respond quickly to contain them. Microsoft Sentinel's near-real-time (NRT) analytics rules offer you faster threat detection—closer to that of an on-premises SIEM—and the ability to shorten response times in specific scenarios.

Microsoft Sentinel’s [near-real-time analytics rules](detect-threats-built-in#nrt) provide up-to-the-minute threat detection out-of-the-box. This type of rule was designed to be highly responsive by running its query at intervals just one minute apart.

## How NRT rules work

NRT rules are hard-coded to run once every minute and capture events ingested in the preceding minute, to supply you with information as up-to-the-minute as possible.

Unlike regular scheduled rules that run on a built-in five-minute delay to account for ingestion time lag, NRT rules run on just a two-minute delay, solving the ingestion delay problem by querying on events' ingestion time instead of their generation time at the source (the TimeGenerated field). This results in improvements of both frequency and accuracy in your detections. (To understand this issue more completely, see [Query scheduling and alert threshold](detect-threats-custom#schedule-and-scope-the-query) and [Handle ingestion delay in scheduled analytics rules](ingestion-delay).)

NRT rules have many of the same features and capabilities as scheduled analytics rules. The full set of alert enrichment capabilities is available—you can map entities and surface custom details, and you can configure dynamic content for alert details. You can choose how alerts are grouped into incidents, you can temporarily suppress the running of a query after it generates a result, and you can define automation rules and playbooks to run in response to alerts and incidents generated from the rule.

For the time being, these templates have limited application as outlined below, but the technology is rapidly evolving and growing.

## Considerations

The following limitations currently govern the use of NRT rules:

- No more than 50 rules can be defined per customer at this time.
- By design, NRT rules will only work properly on log sources with an **ingestion delay of less than 12 hours**.

    (Since the NRT rule type is supposed to approximate **real-time** data ingestion, it doesn't afford you any advantage to use NRT rules on log sources with significant ingestion delay, even if it's far less than 12 hours.)
- The syntax for this type of rule is gradually evolving. At this time the following limitations remain in effect:

    - Because this rule type is in near real time, we have reduced the built-in delay to a minimum (two minutes).
    - Since NRT rules use the ingestion time rather than the event generation time (represented by the TimeGenerated field), you can safely ignore the data source delay and the ingestion time latency (see above).
    - Queries can now run across multiple workspaces.
    - Event grouping is now configurable to a limited degree. NRT rules can produce up to 30 single-event alerts. A rule with a query that results in more than 30 events will produce alerts for the first 29, then a 30th alert that summarizes all the applicable events.
    - Queries defined in an NRT rule can now reference **more than one table**.