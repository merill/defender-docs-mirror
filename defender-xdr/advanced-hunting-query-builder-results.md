---
layout: Conceptual
title: Work with query results in guided mode for hunting in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-query-builder-results
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to review, export, and customize query results in guided mode for advanced hunting in Microsoft Defender XDR, including adding or removing columns in the Results tab.
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.custom:
- msecd-doc-authoring-1014
- cx-ti
- cx-ah
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: da4e4442-5772-9a7a-37d3-0ac61567f08d
document_version_independent_id: da4e4442-5772-9a7a-37d3-0ac61567f08d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-query-builder-results.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-query-builder-results
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-query-builder-results.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: d31901a5-70cc-6ce3-dec5-248cd5586ae1
---

# Work with query results in guided mode for hunting in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

Important

Some information relates to prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

This article explains how to view and work with query results in guided mode for advanced hunting, including exporting results, reviewing runtime and resource usage information, and customizing which columns appear.

In hunting using guided mode, the results of the query appear in the **Results** tab.

![Screenshot of the Results tab showing query output in guided mode for advanced hunting](media/advanced-hunting-query-builder-results/35-query-results.png)

You can work on the results further by exporting them to a CSV file. Selecting **Export** downloads the CSV file for your use.

You can view other information in the Results view:

- Number of records in the results list (beside the Search button)
- Duration of the query run time
- Resource usage of the query

## View more columns

A few standard columns are included in the results for easy viewing.

To view more columns:

1. Select **Customize columns** in the upper right-hand portion of the results view.
2. In the **Customize columns** pane, select the columns to include in the results view and clear the columns to hide.

    ![Screenshot of the Customize columns picker showing available columns to control which fields appear in query results](media/advanced-hunting-query-builder-results/36-columns.png)
3. Select **Apply** to view results with the added columns. Use the scroll bars if necessary.