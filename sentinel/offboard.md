---
layout: Conceptual
title: Remove Microsoft Sentinel from your workspace | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/offboard
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
description: Learn how to delete your Microsoft Sentinel instance to discontinue use of Microsoft Sentinel and the associated costs.
author: EdB-MSFT
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.author: edbaynash
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 9f0a3c56-966e-1dc1-821b-dd121831fcfb
document_version_independent_id: 0a5844bb-a2b5-b9c6-ad1f-ad7c59d016a3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/offboard.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/offboard
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/offboard.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 8f6aa011-8eb2-5a9c-0eb7-86ae5b8b310e
---

# Remove Microsoft Sentinel from your workspace | Microsoft Learn

If you no longer want to use Microsoft Sentinel, this article explains how to remove it from your Log Analytics workspace.

If you instead want to offboard Microsoft Sentinel from the Defender portal, see [Offboard Microsoft Sentinel](/en-us/azure/sentinel/microsoft-sentinel-onboard#offboard-microsoft-sentinel).

## Prerequisites

Before you begin, make sure that you understand the effects of removing Microsoft Sentinel from your environment.

For example, you can't manage Microsoft Sentinel tables in Log Analytics after removing Microsoft Sentinel, such as to set extended data retention. Therefore, to avoid extra data retention charges, we recommend that you set per-table retention to 90 days or less for Microsoft Sentinel tables stored in Log Analytics that will be inaccessible after removing Microsoft Sentinel.

For more information, see [Implications of removing Microsoft Sentinel from your workspace](offboard-implications).

## Remove Microsoft Sentinel

Complete the following steps to remove Microsoft Sentinel from your Log Analytics workspace.

1. For Microsoft Sentinel in the [Azure portal](https://portal.microsoft.com), under **Configuration**, select **Settings**.On the **Settings** page, select the **Settings** tab.  For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), select **System** &gt; **Settings** &gt; **Microsoft Sentinel**.
2. Select **Remove Microsoft Sentinel**.

# [Defender portal](#tab/defender-portal)
![Screenshot of Microsoft Sentinel settings in the Defender portal with the option to remove Microsoft Sentinel highlighted toward the end of the list.](media/offboard/defender-settings-remove-sentinel.png)

# [Azure portal](#tab/azure-portal)
![Screenshot to find the setting to remove Microsoft Sentinel from your workspace in the Azure portal.](media/offboard/locate-remove-sentinel.png)

---
3. Review the **Know before you go...** section on the removal page and the [Implications of removing Microsoft Sentinel from your workspace](offboard-implications) carefully. Take all the necessary actions before proceeding.
4. Select the appropriate checkboxes to let us know why you're removing Microsoft Sentinel. Enter any other details in the space provided, and indicate whether you want Microsoft to email you in response to your feedback.
5. Select **Remove Microsoft Sentinel from your workspace**.

    ![Screenshot that shows the section to remove the Microsoft Sentinel solution from your workspace.](media/offboard/remove-sentinel-reasons.png)

## Clean up resources in the Azure portal (optional)

If you don't want to keep the workspace and the data collected for Microsoft Sentinel, delete the resources associated with the workspace in the Azure portal.

Warning

Deleting resources or the resource group is irreversible and can permanently remove workspace data. Before proceeding, confirm that you no longer need the workspace or its data.

- Delete just the individual resources within the associated resource group that you no longer need. For more information, see [Delete resource](/en-us/azure/azure-resource-manager/management/delete-resource-group?tabs=azure-portal#delete-resource).
- Or, if you don't need any of the resources in the associated resource group, delete the resource group. For more information, see [Delete resource group](/en-us/azure/azure-resource-manager/management/delete-resource-group?tabs=azure-portal).

## Related resources

If you change your mind and want to install Microsoft Sentinel again, see [Onboard Microsoft Sentinel](quickstart-onboard).