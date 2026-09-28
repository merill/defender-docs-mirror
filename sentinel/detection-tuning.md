---
layout: Conceptual
title: Get fine-tuning recommendations for your analytics rules in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/detection-tuning
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
description: Learn how to fine-tune your threat detection rules in Microsoft Sentinel, using automatically generated recommendations, to reduce false positives while maintaining threat detection coverage.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: f0b98e96-86c3-9a9f-3623-b2593e451360
document_version_independent_id: 0ab61833-680e-4c74-73f0-2a47526e573d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/detection-tuning.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/detection-tuning
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/detection-tuning.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: c0a6c1d5-a836-50f9-a981-b22f13a2ed18
---

# Get fine-tuning recommendations for your analytics rules in Microsoft Sentinel | Microsoft Learn

Important

[**Custom detections**](/en-us/defender-xdr/custom-detections-overview?toc=/azure/sentinel/TOC.json&amp;bc=/azure/sentinel/breadcrumb/toc.json) is now the best way to create new rules across Microsoft Sentinel SIEM Microsoft Defender XDR. With custom detections, you can reduce ingestion costs, get unlimited real-time detections, and benefit from seamless integration with Defender XDR data, functions, and remediation actions with automatic entity mapping. For more information, read [Custom detections are now the unified experience for creating detections in Microsoft Defender XDR](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/custom-detections-are-now-the-unified-experience-for-creating-detections-in-micr/4463875).

Important

Detection tuning is currently in **PREVIEW**. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

Fine-tuning threat detection rules in your SIEM can be a difficult, delicate, and continuous process of balancing between maximizing your threat detection coverage and minimizing false positive rates. Microsoft Sentinel simplifies and streamlines this process by using machine learning to analyze billions of signals from your data sources as well as your responses to incidents over time, deducing patterns and providing you with actionable recommendations and insights that can significantly lower your tuning overhead and allow you to focus on detecting and responding to actual threats.

Tuning recommendations and insights are now built in to your analytics rules. The following sections explain what these insights show and how you can implement the tuning recommendations.

## View rule insights and tuning recommendations

To see if Microsoft Sentinel has any tuning recommendations for any of your analytics rules, select **Analytics** from the Microsoft Sentinel navigation menu.

Any rules that have recommendations display a lightbulb icon next to the rule name:

[![Screenshot of list of analytics rules with recommendation indicator.](media/detection-tuning/rule-list-with-insight.png)](media/detection-tuning/rule-list-with-insight.png#lightbox)

Edit an analytics rule that displays the lightbulb icon to view its recommendations along with the other insights. They will appear together on the **Set rule logic** tab of the analytics rule wizard, below the **Results simulation** display.

[![Screenshot of tuning insights in analytics rule.](media/detection-tuning/tuning-insights.png)](media/detection-tuning/tuning-insights.png#lightbox)

### Types of analytics rule insights

The **Tuning insights** display consists of several panes that you can scroll or swipe through, each showing you something different. The time frame - 14 days - for which the insights are displayed is shown at the top of the frame.

1. The first insight pane displays some statistical information - the average number of alerts per incident, the number of open incidents, and the number of closed incidents, grouped by classification (true/false positive). This insight helps you figure out the load on this rule, and understand if any tuning is required - for example, if the grouping settings need to be adjusted.

    ![Screenshot of rule efficiency insight.](media/detection-tuning/rule-efficiency.png)

    This insight is the result of a Log Analytics query. Selecting **Average alerts per incident** will take you to the query in Log Analytics that produced the insight. Selecting **Open incidents** will take you to the **Incidents** blade.
2. The second insight pane recommends for you a list of [entities](entities) to be excluded. These entities are highly correlated with incidents that you closed and classified as **false positive**. Select the plus-sign next to each listed entity to exclude it from the query in future executions of this rule.

    ![Screenshot of entity exclusion recommendation.](media/detection-tuning/entity-exclusion.png)

    This recommendation is produced by Microsoft's advanced data science and machine learning models. This pane's inclusion in the **Tuning insights** display is dependent on there being any recommendations to show.
3. The third insight pane shows the four most frequently-appearing mapped entities across all alerts produced by this rule. Entity mapping must be configured on the rule for this insight to produce any results. This insight might help you become aware of any entities that are "hogging the spotlight" and drawing attention away from other ones. You might want to handle these entities separately in a different rule, or you might decide that they are false positives or otherwise noise, and exclude them from the rule.

    ![Screenshot of top entities insight.](media/detection-tuning/top-entities.png)

    This insight is the result of a Log Analytics query. Selecting any of the entities will take you to the query in Log Analytics that produced the insight.