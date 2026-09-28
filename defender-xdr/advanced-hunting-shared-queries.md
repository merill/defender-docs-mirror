---
layout: Conceptual
title: Use shared queries in Microsoft Defender advanced hunting - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-shared-queries
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Start threat hunting immediately with predefined and shared queries. Share your queries to the public or to your organization.
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
document_id: 77f6317f-c37c-1efa-009e-6244a6b46d83
document_version_independent_id: 77f6317f-c37c-1efa-009e-6244a6b46d83
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-shared-queries.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-shared-queries
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-shared-queries.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: cb14da23-f376-4d1f-62c5-fbec04ef7d75
---

# Use shared queries in Microsoft Defender advanced hunting - Microsoft Defender XDR | Microsoft Learn

[Advanced hunting](advanced-hunting-overview) queries can be shared with users in your organization. You can also save queries that only you can access. Community queries on GitHub are available too. With saved queries, you can quickly start hunting for threats. You don't need to write queries from scratch.

The **Queries** tab in advanced hunting lists **Shared queries**, **My queries**, and **Community queries**. Select an arrow to expand a group.

[![Shared queries, My queries, and Community queries in the Microsoft Defender portal](media/advanced-hunting-shared-queries/advanced-hunting-shared-queries-1.png)](media/advanced-hunting-shared-queries/advanced-hunting-shared-queries-1.png#lightbox)

## Save, modify, and share a query

You can save a new or existing query so that it is only accessible to you or shared with other users in your organization.

1. Create or modify a query.
2. Click the **Save query** drop-down button and select **Save as**.
3. Enter a name for the query.

    [![The new query that is about to be saved in the Microsoft Defender portal](media/advanced-hunting-shared-queries/shared-query-2.png)](media/advanced-hunting-shared-queries/shared-query-2.png#lightbox)
4. Select the folder where you'd like to save the query.

    - **Shared queries** — shared to all users your organization
    - **My queries** — accessible only to you
5. Select **Save**.

## Delete or rename a query

You can rename or delete a saved query at any time.

1. Find the query. Select the three dots next to it.

    [![Rename or delete a query in the Advanced Hunting page in the Microsoft Defender portal](media/advanced-hunting-shared-queries/advanced-hunting-del-save-query.png)](media/advanced-hunting-shared-queries/advanced-hunting-del-save-query.png#lightbox)

Caution

Deleting a query removes it permanently. If you want to keep the query, rename it instead.

1. To remove the query, select **Delete** and confirm. To change its name, select **Rename** and enter a new name.

## Create a direct link to a query

To generate a link that opens your query directly in the advanced hunting query editor, finalize your query and select **Share link**.

## Access community queries in the GitHub repo

Microsoft security researchers share hunting queries in a [public GitHub repository](https://github.com/Azure/Azure-Sentinel/tree/master/Hunting%20Queries/Microsoft%20365%20Defender). All queries are reviewed before they're published. To contribute, [join GitHub for free](https://github.com/).

You can also find these queries in the **Community queries** list.

[![Community queries organized by folder in the Microsoft Defender portal](media/advanced-hunting-shared-queries/advanced-hunting-shared-queries-2.png)](media/advanced-hunting-shared-queries/advanced-hunting-shared-queries-2.png#lightbox)

Community queries are grouped into folders such as *Campaigns*, *Collection*, and *Defense evasion*. Each query includes in-line comments with more details.

Tip

Microsoft security researchers also share queries that help you find activity linked to emerging threats. Look for these queries in the [threat analytics](/en-us/windows/security/threat-protection/microsoft-defender-atp/threat-analytics) reports in the Defender portal.