---
layout: Conceptual
title: Graph icons and visualizations in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/understand-graph-icons
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about the different icons used in graph nodes and edges when visualizing attack paths, blast radius, and entity relationships in Microsoft Defender
ms.service: defender-xdr
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- m365initiative-m365-defender
- tier1
ms.custom:
- cx-ti
- cx-ah
- seo-marvel-apr2020
ms.topic: overview
ms.date: 2025-09-30T00:00:00.0000000Z
locale: en-us
document_id: c7f8f379-d5f9-5b5a-9fa4-9bceff2e5b55
document_version_independent_id: c7f8f379-d5f9-5b5a-9fa4-9bceff2e5b55
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/understand-graph-icons.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: understand-graph-icons
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/understand-graph-icons.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: b18527db-1103-0c4d-e75b-a3f91aa3511e
---

# Graph icons and visualizations in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn

Microsoft Defender use interactive graphs to visualize attack paths, [blast radius](investigate-incidents#view-blast-radius-graphs), and relationships between entities in your environment. These visualizations provide a bird’s eye view of a possible threat or attack, letting you and your security operations (SOC) team to investigate and [hunt](advanced-hunting-graph) them quickly.

The graphs generated in the Defender portal are composed of nodes and edges. This article enumerates and defines the commonly used icons for graph these elements.

## Nodes

A **node** pertains to an entity in your environment (for example, a device, user account, or IP address, among others). Defender portal graphs usually depict nodes as any of the following circular icons:

| **Icon** | **Node type** | **Entity type examples** |
| --- | --- | --- |
| ![General node icon.](media/understand-graph-icons/node-icon-01.png) | General | App service plan |
| ![Compute node icon.](media/understand-graph-icons/node-icon-02.png) | Compute | Device, virtual machine, Microsoft Azure Logic App |
| ![Networking node icon.](media/understand-graph-icons/node-icon-03.png) | Networking | Interface, public IP address, network security group |
| ![Data node icon.](media/understand-graph-icons/node-icon-04.png) | Data | SQL data store, Azure Monitor Log Analytics workspace, storage account, Azure Event Hubs |
| ![Containers node icon.](media/understand-graph-icons/node-icon-05.png) | Containers | Kubernetes cluster |
| ![Keys node icon.](media/understand-graph-icons/node-icon-06.png) | Keys & secrets | Key vault |
| ![DevOps node icon.](media/understand-graph-icons/node-icon-07.png) | DevOps | Azure DevOps repositories |
| ![APIs node icon.](media/understand-graph-icons/node-icon-08.png) | APIs | Cloud applications |
| ![Identity node icon.](media/understand-graph-icons/node-icon-09.png) | Identity & access | User account, Microsoft Entra ID service principal |
| ![IoT node icon.](media/understand-graph-icons/node-icon-10.png) | IoT |  |
| ![Certificate node icon.](media/understand-graph-icons/node-icon-11.png) | Certificate |  |
| ![IP node icon.](media/understand-graph-icons/node-icon-12.png) | IP address |  |
| ![Subscriptions node icon.](media/understand-graph-icons/node-icon-13.png) | Subscriptions |  |

Selecting a node opens a side panel that provides more details about the chosen entity, such as entity name, type, last updated date, and discovery source. This panel might also display additional information such as attack paths and blast radius, depending on the selected node and its relationship to other nodes in the graph.

[![Screenshot of the side panel in the hunting graph containing node details.](media/understand-graph-icons/hunting-graph-node-details.png)](media/understand-graph-icons/hunting-graph-node-details.png#lightbox)

Entities and might also appear as **grouped nodes**, which have numerical indicators (for example, to indicate the total number of user accounts). To expand and view all nodes in a grouped node, use the **ungroup** toggle.

A node might also have any of the following indicators around it:

- **Critical asset** - Indicates that an entity is classified as business-critical or valuable, as identified in the [critical asset management](/en-us/security-exposure-management/critical-asset-management) in Microsoft Security Exposure Management. This indicator appears as a golden crown ![Critical asset icon.](media/understand-graph-icons/critical-asset-icon.png). The nodes representing critical assets also have a golden halo surrounding them.
- **Vulnerability** - Indicates that at least one vulnerability was detected on the entity. This indicator appears as a red bug ![Vulnerability icon.](media/understand-graph-icons/vulnerability-icon.png).
- **Explore connected assets** - Indicates that the node can expand the hunting graph further beyond the initial results. Expanding the graph lets you explore other relationships the selected entity has with the other ones. This indicator appears as a blue plus sign ![Explore connected asset icon.](media/understand-graph-icons/explore-icon.png).
- **Discovery source** - Indicates the entity's data source. This indicator appears as the icon of the Defender product protecting the entity in blue (for example, ![Defender for Endpoint icon.](media/understand-graph-icons/discovery-source-endpoint.png) for Microsoft Defender for Endpoint, or ![Defender for Cloud icon.](media/understand-graph-icons/discovery-source-cloud.png) for Microsoft Defender for Cloud).

    Tip

    You can turn this indicator on and off a graph by toggling the **Discovery Source** switch in the graph's **Layers**.

## Edges

An **edge** indicates the relationship or connection properties between two nodes. The Defender portal graphs depicts an edge as lines or directional arrows that might have the following icons:

| **Icon** | **Edge type** |
| --- | --- |
| ![Contain edge icon.](media/understand-graph-icons/edge-icon-01.png) | Contains |
| ![Route edge icon.](media/understand-graph-icons/edge-icon-02.png) | Routes traffic to |
| ![Permission edge icon.](media/understand-graph-icons/edge-icon-03.png) | Has permission to / Has role on |
| ![Authenticate edge icon.](media/understand-graph-icons/edge-icon-04.png) | Can authenticate as / Can authenticate to |
| ![Push edge icon.](media/understand-graph-icons/edge-icon-05.png) | Pushes |
| ![Maintain edge icon.](media/understand-graph-icons/edge-icon-06.png) | Maintains |
| ![Application edge icon.](media/understand-graph-icons/edge-icon-07.png) | Application |
| ![Move edge icon.](media/understand-graph-icons/edge-icon-08.png) | Moves data to |
| ![Exposed edge icon.](media/understand-graph-icons/edge-icon-09.png) | Exposed to internet |
| ![Login edge icon.](media/understand-graph-icons/edge-icon-10.png) | Can interactive logon to / Can logon over the network to / Can remote interactive logon to |
| ![Run edge icon.](media/understand-graph-icons/edge-icon-11.png) | Runs on |
| ![Provision edge icon.](media/understand-graph-icons/edge-icon-12.png) | Provisions |
| ![Identify edge icon.](media/understand-graph-icons/edge-icon-13.png) | Identified as owner of |
| ![Member edge icon.](media/understand-graph-icons/edge-icon-14.png) | Member of |
| ![Running edge icon.](media/understand-graph-icons/edge-icon-15.png) | Is running |
| ![Generic edge icon.](media/understand-graph-icons/edge-icon-16.png) | Generic / Affects |
| ![Create edge icon.](media/understand-graph-icons/edge-icon-17.png) | Created from / Used to create |

Selecting an edge opens a side panel that provides more details about the connection properties. If two nodes have more than one relationship, a number appears on the edge, in place of an icon. You can find more information about these nodes’ relationships by hovering over the number or opening the side panel.

[![Screenshot of the side panel in the hunting graph containing edge details.](media/understand-graph-icons/hunting-graph-edge-details.png)](media/understand-graph-icons/hunting-graph-edge-details.png#lightbox)