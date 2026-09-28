---
layout: Conceptual
title: Create custom hunting queries in Microsoft Sentinel - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/hunts-custom-queries
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
description: Create custom hunting queries in Microsoft Sentinel to proactively investigate suspicious activity across your data sources. Learn how to write, clone, and edit KQL-based hunting queries for threat investigation.
ms.author: monaberdugo
author: mberdugo
ms.reviewer: efratka
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: bdbb05b7-fb2d-5187-e655-b75daf3c6ef8
document_version_independent_id: f9d1a533-9a73-7a5c-b9f5-1288042f4ae4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/hunts-custom-queries.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/hunts-custom-queries
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/hunts-custom-queries.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 382f6b1c-32e8-c1d6-4ca6-d0d108c97709
---

# Create custom hunting queries in Microsoft Sentinel - Microsoft Sentinel | Microsoft Learn

## Overview

Hunt for security threats across your organization's data sources with custom hunting queries. Microsoft Sentinel provides built-in hunting queries to help you find issues in the data you have on your network. In addition to built-in hunting queries, you can create custom hunting queries. For more information about hunting queries, see [Threat hunting in Microsoft Sentinel](hunting).

## Create a new query

To create a custom hunting query, first open **Hunting** in Microsoft Sentinel, and then select the **Queries** tab.

1. For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), select **Microsoft Sentinel** &gt; **Threat management** &gt; **Hunting**. For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), under **Threat management** select **Hunting**.
2. Select the **Queries** tab.
3. From the command bar, select **New query**.

# [Defender portal](#tab/defender-portal)
[![Save query](media/hunts-custom-queries/save-query-defender.png)](media/hunts-custom-queries/save-query-defender.png#lightbox)

# [Azure portal](#tab/azure-portal)
## [![Save query](media/hunts-custom-queries/save-query.png)](media/hunts-custom-queries/save-query.png#lightbox)

---
4. Fill in all the blank fields.

    1. Create entity mappings by selecting entity types, identifiers, and columns.

        ![Screenshot for mapping entity types in hunting queries.](media/hunting/map-entity-types-hunting.png)
    2. Map MITRE ATT&CK techniques to your hunting queries by selecting the tactic, technique, and sub-technique (if applicable).

        [![New query](media/hunting/mitre-attack-mapping-hunting.png)](media/hunting/new-query.png#lightbox)
5. When your finished defining your query, select **Create**.

## Clone an existing query

Clone a custom or built-in query and edit it as needed.

1. From the **Hunting** &gt; **Queries** tab, select the hunting query you want to clone.
2. Select the ellipsis (...) in the line of the query you want to modify, and select **Clone**.

# [Defender portal](#tab/defender-portal)
[![Clone query](media/hunts-custom-queries/clone-hunting-query-defender.png)](media/hunts-custom-queries/clone-hunting-query-defender.png#lightbox)

# [Azure portal](#tab/azure-portal)
## [![Clone query](media/hunts-custom-queries/clone-hunting-query.png)](media/hunts-custom-queries/clone-hunting-query.png#lightbox)

---
3. Edit the query and other fields as appropriate.
4. Select **Create**.

## Edit an existing custom query

Only queries that come from a custom content source can be edited. Queries from other content sources, such as content hub solutions or repositories, must be edited in the content source where the query was originally created.

1. From the **Hunting** &gt; **Queries** tab, select the hunting query you want to change.
2. Select the ellipsis (...) in the line of the query you want to change, and select **Edit**.
3. Update the **Query** field with the updated query. You can also change the entity mapping and techniques.
4. When finished select **Save**.