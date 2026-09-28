---
layout: Conceptual
title: ExposureGraphEdges table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-exposuregraphedges-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about the ExposureGraphEdges table of the advanced hunting schema, which provides attack surface information, to help you understand how potential threats might reach, and compromise, valuable assets.
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.custom:
- cx-ti
- cx-ah
ms.topic: reference
ms.date: 2025-03-28T00:00:00.0000000Z
locale: en-us
document_id: fa124cd4-18c7-88fb-c98a-c0952f43f031
document_version_independent_id: fa124cd4-18c7-88fb-c98a-c0952f43f031
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-exposuregraphedges-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-exposuregraphedges-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-exposuregraphedges-table.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
platformId: 3345dc41-e17f-a4c5-1614-40df1ffc532c
---

# ExposureGraphEdges table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- Microsoft Defender XDR
- Microsoft Security Exposure Management (public preview)

Important

Some information relates to prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

The `ExposureGraphEdges` table in the [advanced hunting](advanced-hunting-overview) schema provides visibility into relationships between entities and assets in the enterprise exposure graph. This visibility can help uncover critical organizational assets and explore entity relationships and attack paths. Use this reference to construct queries that return information from this table.

This advanced hunting table is populated by records from various Microsoft Defender services, including Defender for Endpoint, Defender for Identity, Defender for Cloud, Entra ID, and others. The table also gets populated by third-party data through the various Security Exposure Management data connectors. The more security products you deploy, the richer the graph becomes with more meaningful data. If your organization hasn't deployed any service in Microsoft Defender, queries that use the table aren't going to work or return any results. For more information about how to deploy services in the Defender portal, read [Deploy supported services](deploy-supported-services).

For information on other tables in the advanced hunting schema, [see the advanced hunting reference](advanced-hunting-schema-tables).

| Column name | Data type | Description |
| --- | --- | --- |
| `EdgeId` | `string` | Unique identifier for the relationship/edge |
| `EdgeLabel` | `string` | The edge label like "routes traffic to" |
| `SourceNodeId` | `string` | Node ID of the edge's source |
| `SourceNodeName` | `string` | Source node display name |
| `SourceNodeLabel` | `string` | Source node label |
| `SourceNodeCategories` | `dynamic` | Categories list of the source node in JSON format |
| `TargetNodeId` | `string` | Node ID of the edge's target |
| `TargetNodeName` | `string` | Display name of the target node |
| `TargetNodeLabel` | `string` | Target node label |
| `TargetNodeCategories` | `dynamic` | The categories list of the target node in JSON format |
| `EdgeProperties` | `dynamic` | Optional data relevant for the relationship between the nodes in JSON format |