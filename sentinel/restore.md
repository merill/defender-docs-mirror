---
layout: Conceptual
title: Restore archived logs from search - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/restore
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
description: Learn how to restore archived logs from search job results.
author: EdB-MSFT
ms.topic: how-to
ms.date: 2026-06-15T00:00:00.0000000Z
ms.author: edbaynash
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: 8536d302-4b5d-458b-6ad5-7f9070ecdb73
document_version_independent_id: 3a0c53b3-257d-2e46-7cb3-f2a7b10dc9fd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/restore.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/restore
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/restore.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 5a07cfdd-c182-262f-8a59-28c01fca25fe
---

# Restore archived logs from search - Microsoft Sentinel | Microsoft Learn

When you need to investigate historical security data that has been moved to long-term storage, you can restore archived logs to make them available for high-performance queries and analytics. This article walks you through how to restore archived log data in Microsoft Sentinel, view the restored results, and delete restored tables when you no longer need them.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Prerequisites

Restoring archived log data in Microsoft Sentinel relies on the Azure Monitor restore capability. Before you begin, review the requirements and limitations in [Restore in Azure Monitor](/en-us/azure/azure-monitor/logs/restore).

## Restore archived log data

To restore archived log data in Microsoft Sentinel, specify the table and time range for the data you want to restore. Within a few minutes, the log data is available within the Log Analytics workspace. Then you can use the data in high-performance queries that support full Kusto Query Language (KQL).

Restore archived data directly from the **Search** page or from a saved search.

1. In the [Defender portal](https://security.microsoft.com/), the **Search** page is at the Microsoft Sentinel root level. In Microsoft Sentinel, select **Search**. In the [Azure portal](https://portal.azure.com), the **Search** page is listed under **General**.
2. Restore log data using one of the following methods:

    - Select ![](media/restore/restore-button.png)**Restore** at the top of the page. In the **Restoration** pane on the side, select the table and time range you want to restore, and then select **Restore at the bottom of the pane**.
    - Select **Saved searches**, locate the search results you want to restore, and then select **Restore**. If you have multiple tables, select the one you want to restore and then select **Actions &gt; Restore** in the side pane. For example:

        ![Screenshot of restoring a specific site search.](media/restore/restore-azure.png)
3. Wait for the log data to be restored. View the status of your restoration job by selecting on the **Restoration** tab.

## View restored log data

View the status and results of the log data restore by going to the **Restoration** tab. You can view the restored data when the status of the restore job shows **Data Available**.

1. In Microsoft Sentinel, select **Search** &gt; **Restoration**.
2. When your restore job is complete and the status is updated, select the table name and review the results.

    In the [Azure portal](https://portal.azure.com), results are shown in the **Logs** query page. In the [Defender portal](https://security.microsoft.com/), results are shown in the **Advanced hunting** page.

    For example:

    ![Screenshot that shows the logs query pane with the restored table results.](media/restore/restored-data-logs-view.png)

    The **Time range** is set to a custom time range that uses the start and end times of the restored data.

## Delete restored data tables

To save costs, we recommend you delete the restored table when you no longer need it. When you delete a restored table, the underlying source data isn't deleted.

1. In Microsoft Sentinel, select **Search** &gt; **Restoration** and identify the table you want to delete.
2. Select **Delete** for that table row to delete the restored table.