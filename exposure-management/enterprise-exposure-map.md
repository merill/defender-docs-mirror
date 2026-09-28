---
layout: Conceptual
title: Explore with the attack surface map in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/security-exposure-management/enterprise-exposure-map
author: dlanger
ms.author: dlanger
manager: orspodek
ms.service: exposure-management
breadcrumb_path: /security-exposure-management/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-Security
description: Learn how to use the attack surface map in Microsoft Security Exposure Management.
ms.topic: overview
ms.date: 2025-09-09T00:00:00.0000000Z
locale: en-us
document_id: 743d0f8a-dde7-d2a5-de04-b138056cb3ba
document_version_independent_id: 743d0f8a-dde7-d2a5-de04-b138056cb3ba
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/exposure-management/enterprise-exposure-map.md
site_name: Docs
depot_name: office.exposure-management
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: enterprise-exposure-map
moniker_range_name: 
monikers: []
item_type: Content
source_path: exposure-management/enterprise-exposure-map.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
platformId: 97c13938-0a39-1b24-6d79-94931c70d374
---

# Explore with the attack surface map in Microsoft Security Exposure Management - Microsoft Security Exposure Management | Microsoft Learn

To visualize exposure data, use the attack surface map in [Microsoft Security Exposure Management](microsoft-security-exposure-management), together with the enterprise exposure graph schema.

## Prerequisites

- [Read about](cross-workload-attack-surfaces) attack surface management.
- [Review required permissions](prerequisites#permissions) for working with the graph.

## Access the map

1. In the device inventory, select a device.
2. Select **View Map**.

You can also search for an asset from **Attack surface &gt; Map**, from **Identities**, or from the **Overview** dashboard.

## Explore the map

The exposure map gives you visibility into asset connections.

1. In **Attack surface map**, explore assets and connections.
2. Use the map features to explore.

    - **Indicators**: Icon indicators show node type and edge type. Visual indicators show information such as the high criticality crown or a vulnerability bug, providing visual input to where critical organizational data is at risk.
    - **Expandable groups**: Provide a way to expand similar assets when you want to view them more in depth. Expanding the view helps you to discover choke points and specific highly vulnerable or critical assets. If not needed, leave them collapsed for a more organized screen.
    - **Hovering**: Hover over nodes and edges to get additional information.
    - **Explore assets and their edges**. To explore assets and edge, select the plus sign. Or select the option to explore connected assets from the contextual menu.
    - **Asset details**: To view details, select the asset icon.
    - **Focus on asset**: Provides a way to refocus the graph visualization on the specific node you want to explore, similar to the **Graph** view when selecting an individual [attack path](work-attack-paths-overview). The Cloud attack paths focus on real, externally-driven and exploitable threats rather than broad potential attack path scenarios.
    - **Search**: Helps you to discover items by node type. By selecting **all results**, search the particular type for specific results. You can also filter your search by devices, identity, or cloud assets from the initial screen.
    - **Discovery source**: Use the layer option to show or hide the origin of the data directly on the attack surface map.

    [![Screenshot of the attack surface exposure map.](media/value-data-connectors/attack map data connectors.png)](media/value-data-connectors/attack%20map%20data%20connectors.png#lightbox)
3. Open the side panel to view asset details.

    - **General**: View general information about the asset, including **Type**, **IDs**, and **Discovery source**.
    - **All data**: View all data about the asset, including **Categories**, **Node Properties**, **Metadata**, and **IDs**.
    - **Top Vulnerabilities**: View up to the top 100 CVEs (by severity) on the asset.
    - **Findings**: View all the security findings on the asset.

    [![Screenshot of attack surface map side pane.](media/enterprise-exposure-map/attack-surface-exposure-map-sidepane.png)](media/enterprise-exposure-map/attack-surface-exposure-map-sidepane.png#lightbox)