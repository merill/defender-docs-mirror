---
layout: Conceptual
title: Surface custom details in Microsoft Sentinel alerts | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/surface-custom-details-in-alerts
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
description: Extract and surface custom event details in alerts in Microsoft Sentinel analytics rules, for better and more complete incident information
ms.author: guywild
author: guywi-ms
ms.reviewer: idpelleg
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: e7751deb-6d40-0c50-9384-f39279427e26
document_version_independent_id: 42df02e9-eb5f-7112-2456-bd36d3ae2de1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/surface-custom-details-in-alerts.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/surface-custom-details-in-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/surface-custom-details-in-alerts.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
platformId: 089ae3a0-608b-4ddd-04a4-5dde6dd98c52
---

# Surface custom details in Microsoft Sentinel alerts | Microsoft Learn

[Scheduled query analytics rules](detect-threats-custom) analyze **events** from data sources connected to Microsoft Sentinel, and produce **alerts** when the contents of these events are significant from a security perspective. These alerts are further analyzed, grouped, and filtered by Microsoft Sentinel's various engines and distilled into **incidents** that warrant a SOC analyst's attention. However, when the analyst views the incident, only the properties of the component alerts themselves are immediately visible. Getting to the actual content - the information contained in the events - requires doing some digging.

Using the **custom details** feature in the **analytics rule wizard**, you can surface event data in the alerts that are constructed from those events, making the event data part of the alert properties. In effect, this gives you immediate event content visibility in your incidents, enabling you to triage, investigate, draw conclusions, and respond with much greater speed and efficiency.

Use this procedure to add or modify custom details in an existing scheduled query analytics rule. These steps are part of the analytics rule creation wizard but are treated here independently.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## How to surface custom event details

Perform the following steps to surface custom event details in an analytics rule.

1. Enter the **Analytics** page in the portal through which you access Microsoft Sentinel:

# [Microsoft Defender portal](#tab/defender)
From the Microsoft Defender navigation menu, expand **Microsoft Sentinel**, then **Configuration**. Select **Analytics**.

# [Microsoft Azure portal](#tab/azure)
From the **Configuration** section of the Microsoft Sentinel navigation menu, select **Analytics**.

---
2. Select a scheduled query rule and click **Edit**. Or create a new rule by clicking **Create &gt; Scheduled query rule** at the top of the screen.
3. Click the **Set rule logic** tab.
4. In the **Alert enrichment** section, expand **Custom details**.

    ![Find and select custom details](media/surface-custom-details-in-alerts/alert-enrichment.png)
5. In the expanded **Custom details** section, add key-value pairs for the details you want to surface:

    1. In the **Key** field, enter a name of your choosing that will appear as the field name in alerts.
    2. In the **Value** field, choose the event parameter you wish to surface in the alerts from the drop-down list. This list will be populated by values corresponding to the fields in the tables that are the subject of the rule query.

        ![Add custom details](media/surface-custom-details-in-alerts/custom-details.png)
6. To surface more details, click **Add new** and enter a **Key** name and select a **Value** from the drop-down list for each additional key-value pair.

    If you change your mind, or if you made a mistake, you can remove a custom detail by clicking the trash can icon next to the **Value** drop-down list for that detail.
7. When you have finished defining custom details, click the **Review and create** tab. Once the rule validation is successful, click **Save**.

    Note

    **Service limits**

    - You can define **up to 20 custom details** in a single analytics rule. Each custom detail can contain **up to 50 values**.
    - The combined size limit for all custom details and their values in a single alert is **2 KB**. Values in excess of this limit are dropped.