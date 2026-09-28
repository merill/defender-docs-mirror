---
layout: Conceptual
title: Edit watchlists - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/watchlists-manage
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
description: Edit existing Microsoft Sentinel watchlists and add items to keep them current. Learn when to update a watchlist instead of deleting and recreating it.
author: EdB-MSFT
ms.author: edbaynash
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: usx-security
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: f704c798-99e6-8741-0f72-e6d6bd9dbc36
document_version_independent_id: a7f9582f-1ed2-7801-1411-ccbcd2606779
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/watchlists-manage.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/watchlists-manage
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/watchlists-manage.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 1ed9bfc7-9c0f-c2c6-a7f5-9688d580b05b
---

# Edit watchlists - Microsoft Sentinel | Microsoft Learn

We recommend you edit an existing watchlist instead of deleting and recreating a watchlist. Log analytics has a five-minute SLA for data ingestion. If you delete and recreate a watchlist, you might see both the deleted and recreated entries in Log Analytics during this five-minute window. If you see these duplicate entries in Log Analytics for a longer period of time, submit a support ticket.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Edit a watchlist item

Edit a watchlist to edit or add an item to the watchlist.

1. For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), select **Microsoft Sentinel** &gt; **Configuration** &gt; **Watchlist**. For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), under **Configuration**, select **Watchlist**.
2. Select the watchlist you want to edit.
3. On the details pane, select **Update watchlist** &gt; **Edit watchlist items**.

    [![Screenshot of the edit watchlist option at the bottom of the details pane.](media/watchlists-manage/sentinel-watchlist-edit.png)](media/watchlists-manage/sentinel-watchlist-edit.png#lightbox)
4. To edit an existing watchlist item,

    1. Select the checkbox of that watchlist item.
    2. Edit the item.
    3. Select **Save**.

        ![Screenshot showing how to mark and edit a watchlist item.](media/watchlists-manage/sentinel-watchlist-edit-change.png)
    4. Select **Yes** at the confirmation prompt.

        ![Screenshot of the prompt to confirm your changes.](media/watchlists-manage/sentinel-watchlist-edit-confirm.png)
5. To add a new item to your watchlist,

    1. Select **Add new**.

        ![Screenshot of the new button at the top of the edit watchlist items page.](media/watchlists-manage/sentinel-watchlist-edit-add-new.png)
    2. Fill in the fields of the **Add watchlist item** panel.
    3. At the bottom of that panel, select **Add**.

## Bulk update a watchlist

When you have many items to add to a watchlist, use bulk update. A bulk update of a watchlist appends items to the existing watchlist. Then, it de-duplicates the items in the watchlist where all the value in each column match.

If you've deleted an item from your watchlist file and upload the file, bulk update won't delete the item in the existing watchlist. Delete the watchlist item individually. Or, when you have a lot of deletions, delete and recreate the watchlist.

The updated watchlist file you upload must contain the search key field used by the watchlist with no blank values.

To bulk update a watchlist,

1. For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), under **Configuration**, select **Watchlist**. For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), select **Microsoft Sentinel** &gt; **Configuration** &gt; **Watchlist**.
2. Select the watchlist you want to edit.
3. On the details pane, select **Update watchlist** &gt; **Bulk update**.

    [![Screenshot of the bulk update option on the bottom of the details pane.](media/watchlists-manage/sentinel-watchlist-bulk-update.png)](media/watchlists-manage/sentinel-watchlist-bulk-update.png#lightbox)
4. Under **Upload file**, drag and drop or browse to the file to upload.

    ![Screenshot of the watchlist wizard source page where you select the file to upload and the search key field is disabled.](media/watchlists-manage/sentinel-watchlist-bulk-update-source.png)
5. If you get an error, fix the issue in the file. Then select **Reset** and try the file upload again.
6. Select **Next: Review and update** &gt; **Update**.