---
layout: Conceptual
title: What is Microsoft Sentinel graph? - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/sentinel-graph-overview
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
description: Learn how Microsoft Sentinel graph enables multi-modal security analytics through graph-based representation of security data, providing deep insights into digital environments and attack paths.
ms.author: monaberdugo
author: mberdugo
ms.reviewer: rmoriarty
ms.topic: overview
ms.date: 2026-08-07T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
locale: en-us
document_id: 825a3fce-1fab-ce7e-d7e5-3f0abf5b6422
document_version_independent_id: 8fa4851f-4cdd-e86e-1f42-74fd61117180
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/sentinel-graph-overview.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/sentinel-graph-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/sentinel-graph-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: cdfc568e-a8d5-c68a-3139-5fca765479bc
---

# What is Microsoft Sentinel graph? - Microsoft Security | Microsoft Learn

Microsoft Sentinel graph is a unified graph analytics capability within Microsoft Sentinel that powers graph-based experiences across security, compliance, identity, and the Microsoft Security ecosystem - empowering security teams to model, analyze, and visualize complex relationships across their digital estate.

Unlike traditional tabular data approaches, Sentinel graph enables defenders and AI agents to reason over interconnected assets, identities, activities, and threat intelligence, unlocking deeper insights and accelerating response to evolving cyber threats across pre-breach and post-breach. Graphs natively represent the real-world web of users, devices, cloud resources, data flows, activities, and attacker actions.

By representing these relationships as nodes and edges, security teams can answer questions that are difficult or impossible with tables such as what could happen if a specific user account is compromised, or what is the blast radius of a compromised document.

## Enable defense at all stages

Sentinel graph offers interconnected security graphs to help you at every stage of defense. The graph capabilities support scenarios throughout Defender and [Microsoft Purview](/en-us/purview/purview), providing graph-based defense strategies across all stages, from pre-breach to post-breach and across assets, activities, and threat intelligence.

For example, your digital environment includes active directory, servers, virtual machines, and other assets, vulnerabilities, misconfigurations, and excessive privileges are common and can increase the risk of security breaches through compromised accounts. An attacker can infiltrate your organization, compromise tokens, and eventually gain access to sensitive information, resulting in data exfiltration.

Microsoft Sentinel graph offers underlying graph analytics capabilities interconnecting activity, asset, and threat intelligence functionalities, enhancing analysis across these networks and enabling comprehensive graph-based security throughout Microsoft solutions across pre-breach and post-breach.

[![Diagram showing graph enabled defense capabilities pre-breach and post breach.](media/sentinel-graph-overview/graph-based-capabilities.png)](media/sentinel-graph-overview/graph-based-capabilities.png#lightbox)

1. Features such as Attack Path within Microsoft Security Exposure Management (MSEM) and Microsoft Defender for Cloud (MDC) provide recommendations to proactively manage attack surfaces, protect critical assets, and explore and mitigate exposure risk.
2. Blast radius analysis in Incident graph in Defender helps you evaluate and visualize the vulnerable paths an attacker could take from a compromise entity to a critical asset.
3. Graph-based hunting in Defender helps you visually traverse the complex web of relationships between users, devices, and other entities to reveal privileged access paths to critical assets to prioritize incidents and response efforts.
4. Activity analysis via Microsoft Purview Insider Risk Management supports user risk assessment and helps you identify data leak blast radius of risky user activity across SharePoint and OneDrive.
5. Microsoft Purview Data Security Investigations graphs facilitate understanding of breach scope by pointing sensitive data access and movement, map potential exfiltration paths, and visualize the users and activities linked to risky files, all in one view.

Collectively, Microsoft Sentinel graph’s capabilities enable defense across all stages of the security lifecycle.

## Embedded graphs in Defender and Purview Portals

Microsoft Sentinel graph powers new advanced capabilities across Microsoft's security portfolio:

| Solution | Capability | Description |
| --- | --- | --- |
| **Microsoft Defender XDR** | [Incident graph extended with Blast Radius](https://aka.ms/sentinel/graph/docs/incidents) | Visualize current impact of a breach and the possible future impact in one consolidated graph |
| **Microsoft Defender XDR** | [Hunting graph in Defender](https://aka.ms/sentinel/graph/docs/hunting) | Interactively traverse graphs to uncover hidden relationships between assets |
| **Microsoft Purview** | [Data risk graph in Insider Risk Management](/en-us/purview/insider-risk-management-data-risk-graph) | Map user activities to detect data exfiltration patterns and understand data leak blast radius |
| **Microsoft Purview** | [Data risk graph in Data Security Investigations](/en-us/purview/data-security-investigations-data-risk-graph) | Trace sensitive data access and movement. Understand data leak blast radius |

## Custom graphs in Microsoft Sentinel (preview)

Custom graphs let you model security scenarios by using connected data from the Microsoft Sentinel data lake and non-Microsoft sources. Build, query, and visualize graphs to uncover relationships, attack paths, and risks that are difficult to detect when data is analyzed in isolation. These graphs give AI-powered agents more context to accelerate investigations, show the scope of an attack, and help analysts make informed decisions.

Author a custom graph in a Jupyter notebook by using the Microsoft Sentinel extension for Visual Studio Code, and then publish and materialize the graph by using a graph job. After publication, query and visualize the graph with Graph Query Language (GQL) on the **Graphs** page in the Defender portal. On-demand graph jobs retain a graph for 30 days, while scheduled graph jobs rebuild the graph on the refresh schedule you configure. Custom graph creation and queries are billed under the Microsoft Sentinel graph meter. For more information, see [Custom graph overview](custom-graphs-overview), [Create custom graphs](create-custom-graphs), and [Graph charges](../billing#graph-charges).

## Get started

To begin using Microsoft Sentinel graph:

# [Defender](#tab/defender)
- Use the [Sentinel data lake onboarding flow](sentinel-lake-onboard-defender) to enable the data lake and graph.
- If you already have the Sentinel data lake, hunting graph and blast radius experience are auto provisioned when you sign in into the Defender portal.
- For information on getting started with custom graphs, see [Custom graph overview](custom-graphs-overview).

# [Microsoft Purview](#tab/purview)
To begin using Microsoft Sentinel graph in Microsoft Purview:

- In **Microsoft Purview Insider Risk Management**, follow the instructions in [Data risk graph in Insider Risk Management](/en-us/purview/insider-risk-management-data-risk-graph).
- In **Microsoft Purview Data Security Investigation**, follow the instructions in [Data risk graph in Data Security Investigations](/en-us/purview/data-security-investigations-data-risk-graph).

---