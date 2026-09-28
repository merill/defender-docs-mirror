---
layout: Conceptual
title: Rerun queries in query history - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-query-history
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: View previously run advanced hunting queries in the Query history tab and rerun them even after closing the original query tab.
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.custom:
- msecd-doc-authoring-1014
- cx-ti
- cx-ah
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 9301f020-ae29-7224-9eb5-c90e25d8e86b
document_version_independent_id: 9301f020-ae29-7224-9eb5-c90e25d8e86b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-query-history.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-query-history
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-query-history.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 69f51fd8-567f-64bd-5113-0911175c1140
---

# Rerun queries in query history - Microsoft Defender XDR | Microsoft Learn

## Query history overview

Important

Some information relates to prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

Your previous queries appear in the **Query history** tab in the lower half of the advanced hunting page. You can rerun past queries even after closing the tab where they ran.

## View the query history tab

To view your query history, select the **Query history** tab.

[![Screenshot of the query history pane in advanced hunting](media/advanced-hunting-query-history/advanced-hunting-query-history.png)](media/advanced-hunting-query-history/advanced-hunting-query-history.png#lightbox)

Recent queries appear with the newest first. The list keeps up to 30 queries from the last 28 days.

By default, **Query history** shows these columns:

- Time - when the query started
- Query
- Query time - how long the query took
- State - whether the query finished, failed, or was throttled

To hide columns, select **Customize columns**.

## Rerun queries from query history

To reuse a previous query, select it. The **Run query** and **Use in editor** options appear.

[![Screenshot of the query history functions in advanced hunting](media/advanced-hunting-query-history/advanced-hunting-query-history-functions.png)](media/advanced-hunting-query-history/advanced-hunting-query-history-functions.png#lightbox)

Select **Run query** to run it right away, or select **Use in editor** to edit it first.