---
layout: Conceptual
title: Identity attack graph in Microsoft Sentinel - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/identity-attack-graph
breadcrumb_path: ../breadcrumb/toc.json
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
ms.subservice: sentinel-platform
search.appverid: met150
description: Learn how the identity attack graph in Microsoft Sentinel models identities, permissions, and Azure resources to surface lateral movement paths and privilege escalation risks.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: evwhite
ms.topic: overview
ms.date: 2026-04-10T00:00:00.0000000Z
locale: en-us
document_id: 1c51e855-9f15-3e8f-ab54-bf8e15de8166
document_version_independent_id: 33c38b57-8569-7cd7-7d47-5a0653b79137
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/identity-attack-graph.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/identity-attack-graph
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/identity-attack-graph.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 2af2b03e-4e73-a0de-d121-3618082493b2
---

# Identity attack graph in Microsoft Sentinel - Microsoft Security | Microsoft Learn

The identity attack graph in Microsoft Sentinel visualizes how identities connect to Azure resources through permissions and group memberships. Security analysts can use the graph to identify lateral movement paths, which are the potential routes an attacker could take to move from one identity or resource to another by exploiting existing permissions, group memberships, or trust relationships, often to escalate privileges or reach sensitive assets.

The predefined identity attack graph represents your environment as interconnected entities and relationships, making it easier to answer complex questions, such as "What resources could an attacker reach if this account is compromised?" or "Which identities have paths to critical assets?"

SOC analysts, threat hunters, cloud security engineers, and IAM teams can use the graph to understand and reduce identity risk across Azure and Entra.

## How the identity attack graph works

The identity attack graph uses asset data from the Microsoft Sentinel lake's Entra ID asset and Azure resource graph connectors to build a comprehensive model of your environment:

- **Identities**: Users, service principals, managed identities, and groups
- **Resources**: Azure subscriptions, resource groups, virtual machines, storage accounts, and other assets
- **Access and permission relationships**: Role assignments and group memberships that create paths to resources they can access

After setup, use Graph Query Language (GQL) to uncover hidden risks that are difficult to detect with traditional methods.

You can query the graph to:

- **Surface lateral movement paths**: Find all routes an attacker could take from a compromised identity to reach critical resources
- **Identify overprivileged accounts**: Discover identities with excessive permissions or indirect paths to privileged roles
- **Prioritize remediation**: Focus on the shortest paths to your most sensitive assets

## Prerequisites

To set up the identity attack graph, make sure you meet the following prerequisites:

- Microsoft Sentinel data lake enabled in your environment
- [Permissions](/en-us/azure/sentinel/datalake/enable-data-connectors#required-permissions-for-asset-sources) to turn on or update the **Microsoft Entra ID Assets** and **Azure Resource Graph connectors**
- Global Administrator, Security Administrator to create the graph

## Set up the identity attack graph

Follow these steps to set up the identity attack graph:

1. In the Microsoft Defender portal, navigate to **Microsoft Sentinel** &gt; **Graphs**.
2. Locate the **identity attack graph** card and select **Set up graph**.
3. Follow the setup steps and turn on or update the required connectors.
4. Select **Turn on graph** to create your graph.
5. Select **Query graph** on the graph tile to view the graph query page.

    [![Screenshot showing the Microsoft Sentinel identity attack graph overview panel.](media/identity-attack-graph/identity-graph-overview-panel.png)](media/identity-attack-graph/identity-graph-overview-panel.png#lightbox)

After you turn on the graph, the graph begins ingesting data and building relationships. Initial processing may take up to 48 hours.

## Explore and query the identity attack graph

Follow these steps to query the graph when the graph is ready to use:

1. Use the **Schema** tab to understand the types of entities and relationships in the graph.

    [![Screenshot showing the schema tab on the graph query page.](media/identity-attack-graph/visualize-graph-schema.png)](media/identity-attack-graph/visualize-graph-schema.png#lightbox)
2. Select any node to view the detailed metadata.
3. Use the **Graph** tab to visualize relationships and privilege paths. Write your own GQL queries or use the predefined queries to get started.

    [![Screenshot showing the predefined query on the graph.](media/identity-attack-graph/predefined-query.png)](media/identity-attack-graph/predefined-query.png#lightbox)

    Note

    It's recommended that you start with the predefined queries, which are designed to surface common and high‑value investigation scenarios. These queries help you get immediate value without writing GQL from scratch.
4. Select **Run GQL query** to see the results.

    [![Screenshot showing the graph tab to visualize query.](media/identity-attack-graph/visualize-query.png)](media/identity-attack-graph/visualize-query.png#lightbox)