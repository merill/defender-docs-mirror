---
layout: Conceptual
title: Work with near-real-time (NRT) detection analytics rules in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/create-nrt-rules
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
description: View and create near-real-time (NRT) analytics rules in Microsoft Sentinel for up-to-the-minute threat detection, including key limitations and usage considerations.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 97468f8f-f0e4-293d-7a91-556b05b7f2aa
document_version_independent_id: 6f6704c1-875a-116e-ad3d-7a5aeb0040d2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/create-nrt-rules.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/create-nrt-rules
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/create-nrt-rules.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 06e1c17d-26dc-294f-e141-1e00c8d01334
---

# Work with near-real-time (NRT) detection analytics rules in Microsoft Sentinel | Microsoft Learn

Important

[**Custom detections**](/en-us/defender-xdr/custom-detections-overview?toc=/azure/sentinel/TOC.json&amp;bc=/azure/sentinel/breadcrumb/toc.json) is now the best way to create new rules across Microsoft Sentinel SIEM Microsoft Defender XDR. With custom detections, you can reduce ingestion costs, get unlimited real-time detections, and benefit from seamless integration with Defender XDR data, functions, and remediation actions with automatic entity mapping. For more information, read [Custom detections are now the unified experience for creating detections in Microsoft Defender XDR](https://techcommunity.microsoft.com/blog/microsoftthreatprotectionblog/custom-detections-are-now-the-unified-experience-for-creating-detections-in-micr/4463875).

Microsoft Sentinel’s [near-real-time analytics rules](near-real-time-rules) provide up-to-the-minute threat detection out-of-the-box. Near-real-time analytics rules are designed to be highly responsive by running their queries at intervals just one minute apart.

For the time being, NRT rule templates have limited application, as outlined in [Considerations for NRT rules](near-real-time-rules#considerations), but the technology is rapidly evolving and growing.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## View near-real-time (NRT) rules

To view your existing NRT rules, filter the analytics rules list by rule type:

# [Defender portal](#tab/defender-portal)
To view NRT rules in the Defender portal:

1. From the Microsoft Defender navigation menu, expand **Microsoft Sentinel**, then **Configuration**. Select **Analytics**.
2. On the **Analytics** screen, with the **Active rules** tab selected, filter the list for **NRT** templates:

    1. Select **Add filter** and choose **Rule type** from the list of filters.
    2. From the resulting list, select **NRT**. Then select **Apply**.

# [Azure portal](#tab/azure-portal)
To view NRT rules in the Azure portal:

1. From the **Configuration** section of the Microsoft Sentinel navigation menu, select **Analytics**.
2. On the **Analytics** screen, with the **Active rules** tab selected, filter the list for **NRT** templates:

    1. Select **Add filter** and choose **Rule type** from the list of filters.
    2. From the resulting list, select **NRT**. Then select **Apply**.

---

## Create NRT rules

Create NRT rules by following the same procedure used for regular [scheduled-query analytics rules](detect-threats-custom):

# [Defender portal](#tab/defender-portal)
To create an NRT rule in the Defender portal:

1. From the Microsoft Defender navigation menu, expand **Microsoft Sentinel**, then **Configuration**. Select **Analytics**.
2. In the action bar at the top of the grid, select **+Create** and select **NRT query rule**. This opens the **Analytics rule wizard**.

    [![Screenshot shows how to create a new NRT rule.](media/create-nrt-rules/defender-create-nrt-rule.png)](media/create-nrt-rules/create-nrt-rule.png#lightbox)

# [Azure portal](#tab/azure-portal)
To create an NRT rule in the Azure portal:

1. From the **Configuration** section of the Microsoft Sentinel navigation menu, select **Analytics**.
2. In the action bar at the top, select **+Create** and select **NRT query rule**. This opens the **Analytics rule wizard**.

    [![Screenshot shows how to create a new NRT rule.](media/create-nrt-rules/create-nrt-rule.png)](media/create-nrt-rules/create-nrt-rule.png#lightbox)

---

1. Follow the steps in [Create a scheduled query analytics rule](detect-threats-custom) to complete the **Analytics rule wizard**.

    The configuration of NRT rules is in most ways the same as that of scheduled analytics rules.

    - You can refer to multiple tables and [**watchlists**](watchlists) in your query logic.
    - You can use all of the alert enrichment methods: [**entity mapping**](map-data-fields-to-entities), [**custom details**](surface-custom-details-in-alerts), and [**alert details**](customize-alert-details).
    - You can choose how to group alerts into incidents, and to suppress a query when a particular result has been generated.
    - You can automate responses to both alerts and incidents.
    - You can run the rule query across multiple workspaces.

    Because of the [**nature and limitations of NRT rules**](near-real-time-rules#considerations), however, the following features of scheduled analytics rules will *not be available* in the wizard:

    - **Query scheduling** is not configurable, since queries are automatically scheduled to run once per minute with a one-minute lookback period.
    - **Alert threshold** is irrelevant, since an alert is always generated.
    - **Event grouping** configuration is now available to a limited degree. You can choose to have an NRT rule generate an alert for each event for up to 30 events. If you choose this option and the rule results in more than 30 events, single-event alerts will be generated for the first 29 events, and a 30th alert will summarize all the events in the result set.

    In addition, due to the size limits of the alerts, your query should make use of `project` statements to include only the necessary fields from your table. Otherwise, the information you want to surface could end up being truncated.