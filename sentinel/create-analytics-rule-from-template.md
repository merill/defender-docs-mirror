---
layout: Conceptual
title: Create scheduled analytics rules from templates in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/create-analytics-rule-from-template
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
description: This article explains how to view and create scheduled analytics rules from templates in Microsoft Sentinel.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.collection: usx-security
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 88c619d6-058a-61a7-d3b1-873d6443d909
document_version_independent_id: ebaa5cad-5587-bb09-8c83-0aaa77b7ab79
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/create-analytics-rule-from-template.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/create-analytics-rule-from-template
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/create-analytics-rule-from-template.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 9d99524f-36c2-a007-668c-9649144d19a9
---

# Create scheduled analytics rules from templates in Microsoft Sentinel | Microsoft Learn

By far the most common type of analytics rule, **Scheduled** rules are based on [Kusto queries](/en-us/kusto/query/?toc=/azure/sentinel/TOC.json&amp;bc=/azure/sentinel/breadcrumb/toc.json) that are configured to run at regular intervals and examine raw data from a defined "lookback" period. These queries can perform complex statistical operations on their target data, revealing baselines and outliers in groups of events. If the number of results captured by the query passes the threshold configured in the rule, the rule produces an alert.

Microsoft makes a vast array of **analytics rule templates** available to you through the many [solutions provided in the Content hub](sentinel-solutions), and strongly encourages you to use them to create your rules. The queries in scheduled rule templates are written by security and data science experts, either from Microsoft or from the vendor of the solution providing the template.

The following procedure shows how to create a scheduled analytics rule from a template.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## View existing analytics rules

To view the installed analytics rules in Microsoft Sentinel, go to the **Analytics** page. The **Rule templates** tab displays all the installed rule templates. To find more rule templates, go to the **Content hub** in Microsoft Sentinel to install product solutions that contain the rule templates you need, or install standalone content.

# [Defender portal](#tab/defender-portal)
Use the following steps to view existing analytics rule templates in the Defender portal.

1. From the Microsoft Defender navigation menu, expand **Microsoft Sentinel**, then **Configuration**. Select **Analytics**.
2. On the **Analytics** screen, select the **Rule templates** tab.
3. If you want to filter the list for **Scheduled** templates:

    1. Select **Add filter** and choose **Rule type** from the list of filters.
    2. From the resulting list, select **Scheduled**. Then select **Apply**.

    [![Screenshot of scheduled analytics rule templates in Microsoft Defender portal.](media/create-analytics-rule-from-template/view-detections-defender.png)](media/create-analytics-rule-from-template/view-detections-defender.png#lightbox)

# [Azure portal](#tab/azure-portal)
Use the following steps to view existing analytics rule templates in the Azure portal.

1. From the **Configuration** section of the Microsoft Sentinel navigation menu, select **Analytics**.
2. On the **Analytics** screen, select the **Rule templates** tab.
3. If you want to filter the list for **Scheduled** templates:

    1. Select **Add filter** and choose **Rule type** from the list of filters.
    2. From the resulting list, select **Scheduled**. Then select **Apply**.

    [![Screenshot of scheduled analytics rule templates in Microsoft Azure portal.](media/create-analytics-rule-from-template/view-detections.png)](media/create-analytics-rule-from-template/view-detections.png#lightbox)

---

## Create a rule from a template

This procedure describes how to create an analytics rule from a template.

# [Defender portal](#tab/defender-portal)
From the Microsoft Defender navigation menu, expand **Microsoft Sentinel**, then **Configuration**. Select **Analytics**.

# [Azure portal](#tab/azure-portal)
From the **Configuration** section of the Microsoft Sentinel navigation menu, select **Analytics**.

---

1. On the **Analytics** screen, select the **Rule templates** tab.
2. Select a template name, and then select the **Create rule** button on the details pane to create a new active rule based on that template.

    Each template has a list of required data sources. When you open the selected template, the data sources are automatically checked for availability. If a data source isn't enabled, the **Create rule** button may be disabled, or you might see a message to that effect.

    ![Screenshot of analytics rule preview panel.](media/create-analytics-rule-from-template/use-built-in-template.png)
3. The rule creation wizard opens. All the details are autofilled.
4. Cycle through the tabs of the wizard, customizing the logic and other rule settings where possible to better suit your specific needs. For more information, see:

    - [Kusto Query Language in Microsoft Sentinel](/en-us/kusto/query/?toc=/azure/sentinel/TOC.json&amp;bc=/azure/sentinel/breadcrumb/toc.json)
    - [KQL quick reference guide](/en-us/kusto/query/kql-quick-reference?view=microsoft-sentinel&amp;preserve-view=true)
    - [Best practices for Kusto Query Language queries](/en-us/kusto/query/best-practices?view=microsoft-sentinel&amp;preserve-view=true&amp;toc=/azure/sentinel/TOC.json&amp;bc=/azure/sentinel/breadcrumb/toc.json)

    When you get to the end of the rule creation wizard, Microsoft Sentinel creates the rule. The new rule appears in the **Active rules** tab.

    Repeat these rule-creation steps to create more rules. For more details on how to customize your rules in the rule creation wizard, see [Create a custom analytics rule from scratch](create-analytics-rules).

Tip

- Make sure that you **enable all rules associated with your connected data sources** in order to ensure full security coverage for your environment. The most efficient way to enable analytics rules is directly from the data connector page, which lists any related rules. For more information, see [Connect data sources](connect-data-sources).
- You can also **push rules to Microsoft Sentinel via the [Microsoft Sentinel REST API](/en-us/rest/api/securityinsights/) and [PowerShell](https://www.powershellgallery.com/packages/Az.SecurityInsights/0.1.0)**, although doing so requires additional effort.

    When using API or PowerShell, you must first export the analytics rules you want to enable to JSON before enabling them. API or PowerShell may be helpful when enabling rules in multiple instances of Microsoft Sentinel with identical settings in each instance.