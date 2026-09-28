---
layout: Conceptual
title: Work with anomaly detection analytics rules in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/work-with-anomaly-rules
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
description: This article explains how to view, create, manage, assess, and fine-tune anomaly detection analytics rules in Microsoft Sentinel.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 421c1c0a-ea2c-b917-beb9-376c9f82a562
document_version_independent_id: fcc9c42a-1c62-c9da-51aa-fc61e682b30a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/work-with-anomaly-rules.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/work-with-anomaly-rules
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/work-with-anomaly-rules.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: d243949d-a58b-18f4-9e94-0847dcc791c3
---

# Work with anomaly detection analytics rules in Microsoft Sentinel | Microsoft Learn

Important

[**Custom detections**](/en-us/defender-xdr/custom-detections-overview?toc=/azure/sentinel/TOC.json&amp;bc=/azure/sentinel/breadcrumb/toc.json) is now the best way to create new rules across Microsoft Sentinel SIEM Microsoft Defender XDR. With custom detections, you can reduce ingestion costs, get unlimited real-time detections, and benefit from seamless integration with Defender XDR data, functions, and remediation actions with automatic entity mapping. For more information, read the blog post [Custom detections are now the unified experience for creating detections in Microsoft Defender XDR](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/custom-detections-are-now-the-unified-experience-for-creating-detections-in-micr/4463875).

Microsoft Sentinel’s [customizable anomalies feature](soc-ml-anomalies) provides [built-in anomaly templates](detect-threats-built-in#anomaly) for immediate value out-of-the-box. These anomaly templates were developed to be robust by using thousands of data sources and millions of events, but the customizable anomalies feature also enables you to change thresholds and parameters for the anomalies easily within the user interface. Anomaly rules are enabled, or activated, by default, so they will generate anomalies out-of-the-box. You can find and query these anomalies in the **Anomalies** table in the **Logs** section.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## View customizable anomaly rule templates

You can now find anomaly rules displayed in a grid in the **Anomalies** tab in the **Analytics** page.

1. For users of the Microsoft Defender portal, select **Microsoft Sentinel &gt; Configuration &gt; Analytics** from the Microsoft Defender navigation menu.

    For users of Microsoft Sentinel in the Azure portal, select **Analytics** from the Microsoft Sentinel navigation menu.
2. On the **Analytics** page, select the **Anomalies** tab.
3. To filter the list by one or more of the following criteria, select **Add filter** and choose accordingly.

    - **Status** - whether the rule is enabled or disabled.
    - **Tactics** - the MITRE ATT&CK framework tactics covered by the anomaly.
    - **Techniques** - the MITRE ATT&CK framework techniques covered by the anomaly.
    - **Data sources** - the type of logs that need to be ingested and analyzed for the anomaly to be defined.
4. Select a rule and view the following information in the details pane:

    - **Description** explains how the anomaly works and the data it requires.
    - **Tactics and techniques** are the MITRE ATT&CK framework tactics and techniques covered by the anomaly.
    - **Parameters** are the configurable attributes for the anomaly.
    - **Threshold** is a configurable value that indicates the degree to which an event must be unusual before an anomaly is created.
    - **Rule frequency** is the time between log processing jobs that find the anomalies.
    - **Rule status** tells you whether the rule runs in **Production** or **Flighting** (staging) mode when enabled.
    - **Anomaly version** shows the version of the template that is used by a rule. If you want to change the version used by a rule that is already active, you must recreate the rule.

The rules that come with Microsoft Sentinel out of the box cannot be edited or deleted. To customize a rule, you must first create a duplicate of the rule, and then customize the duplicate. For complete instructions, see Tune anomaly rules.

Note

**Why is there an Edit button if the rule can't be edited?**

While you can't change the configuration of an out-of-the-box anomaly rule, you can do two things:

1. You can toggle the **rule status** of the rule between **Production** and **Flighting**.
2. You can submit feedback to Microsoft on your experience with customizable anomalies.

## Assess the quality of anomalies

You can see how well an anomaly rule is performing by reviewing a sample of the anomalies created by a rule over the last 24-hour period.

1. For users of Microsoft Sentinel in the Azure portal, select **Analytics** from the Microsoft Sentinel navigation menu.

    For users of the Microsoft Defender portal, select **Microsoft Sentinel &gt; Configuration &gt; Analytics** from the Microsoft Defender navigation menu.
2. On the **Analytics** page, select the **Anomalies** tab.
3. Select the rule you want to assess, and copy its ID from the top of the details pane to the right.
4. From the Microsoft Sentinel navigation menu, select **Logs**.
5. If a **Queries** gallery pops up over the top, close it.
6. Select the **Tables** tab on the left pane of the **Logs** page.
7. Set the **Time range** filter to **Last 24 hours**.
8. Copy the Kusto query below and paste it in the query window (where it says "Type your query here or..."):

    ```kusto
    Anomalies 
    | where RuleId contains "<RuleId>"
    ```

    Paste the rule ID you copied above in place of `<RuleId>` between the quotation marks.
9. Select **Run**.

When you have some results, you can start assessing the quality of the anomalies. If you don’t have results, try increasing the time range.

Expand the results for each anomaly and then expand the **AnomalyReasons** field. This will tell you why the anomaly fired.

The "reasonableness" or "usefulness" of an anomaly may depend on the conditions of your environment, but a common reason for an anomaly rule to produce too many anomalies is that the threshold is too low.

## Tune anomaly rules

While anomaly rules are engineered for maximum effectiveness out of the box, every situation is unique and sometimes anomaly rules need to be tuned.

Since you can't edit an original active rule, you must first duplicate an active anomaly rule and then customize the copy.

The original anomaly rule will keep running until you either disable or delete it. The original rule continues to run by design, so you can compare the results generated by the original configuration and the new one. Duplicate rules are disabled by default. You can only make one customized copy of any given anomaly rule. Attempts to make a second copy will fail.

1. To change the configuration of an anomaly rule, select the rule from the list in the **Anomalies** tab.
2. Right-click anywhere on the row of the rule, or left-click the ellipsis (...) at the end of the row, then select **Duplicate** from the context menu.

    A new rule will appear in the list, with the following characteristics:

    - The rule name will be the same as the original, with " - Customized" appended to the end.
    - The rule's status will be **Disabled**.
    - The **FLGT** badge will appear at the beginning of the row to indicate that the rule is in Flighting mode.
3. To customize this rule, select the rule and select **Edit** in the details pane, or from the rule's context menu.
4. The rule opens in the Analytics rule wizard. Here you can change the parameters of the rule and its threshold. The parameters that can be changed vary with each anomaly type and algorithm.

    You can preview the results of your changes in the **Results preview pane**. Select an **Anomaly ID** in the results preview to see why the ML model identifies that anomaly.
5. Enable the customized rule to generate results. Some of your changes may require the rule to run again, so you must wait for it to finish and come back to check the results on the logs page. The customized anomaly rule runs in **Flighting** (testing) mode by default. The original rule continues to run in **Production** mode by default.
6. To compare the results, go back to the Anomalies table in **Logs** to assess the new rule as described earlier in Assess the quality of anomalies, but use the following query instead to look for anomalies generated by the original rule as well as the duplicate rule.

    ```kusto
    Anomalies 
    | where AnomalyTemplateId contains "<RuleId>"
    ```

    Paste the rule ID you copied from the original rule in place of `<RuleId>` between the quotation marks. The value of `AnomalyTemplateId` in both the original and duplicate rules is identical to the value of `RuleId` in the original rule.

If you are satisfied with the results for the customized rule, you can go back to the **Anomalies** tab, select the customized rule, select the **Edit** button and on the **General** tab switch it from **Flighting** to **Production**. The original rule will automatically change to **Flighting** since you can't have two versions of the same rule in production at the same time.