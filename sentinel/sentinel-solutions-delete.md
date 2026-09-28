---
layout: Conceptual
title: Delete installed Microsoft Sentinel out-of-the-box content and solutions | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sentinel-solutions-delete
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
description: Remove solutions and content you deployed in Microsoft Sentinel.
author: EdB-MSFT
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.author: edbaynash
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 2b52fa21-7cb7-d093-ab06-c2af7ceca466
document_version_independent_id: 7f1df4f6-4907-4b51-ae18-5c291012a539
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sentinel-solutions-delete.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/sentinel-solutions-delete
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sentinel-solutions-delete.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 0afdf6d3-670f-d5df-e2c4-ab2ec52ef682
---

# Delete installed Microsoft Sentinel out-of-the-box content and solutions | Microsoft Learn

If you installed an out-of-the-box solution, you can remove content items or delete the solution. To restore deleted content items, select **Reinstall** on the solution. You can also restore the solution by reinstalling it.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Delete content items

Delete content items from a solution you installed from the content hub.

1. Open the content hub.

    - **Defender portal**: Select **Microsoft Sentinel** &gt; **Content management** &gt; **Content hub**.
    - **Azure portal**: Under **Content management**, select **Content hub**.
2. Select an installed solution with version 2.0.0 or higher.
3. On the solutions details page, select **Manage**.
4. Select the content item or items you want to delete.
5. Select **Delete**.

    ![Screenshot of solution with content items selected for deletion.](media/sentinel-solutions-delete/manage-solution-delete-item.png)

To restore deleted content items, select **Reinstall** on the solution.

## Delete the solution

Delete a solution and its content templates from the content hub or the manage solution view. Deleting a solution doesn't delete active, cloned, saved, or custom items.

1. In the content hub, select an installed solution.
2. On the solutions details page, select **Delete**.
3. Select **Yes** to delete the solution and the templates.

    ![Screenshot of the confirmation prompt to delete the solution.](media/sentinel-solutions-delete/manage-solution-delete.png)

To restore an out-of-the-box solution from the content hub, select the solution and **Install**.