---
layout: Conceptual
title: Custom Graphs in Microsoft Sentinel Overview (Preview) | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/custom-graphs-overview
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
description: Learn how custom graphs in Microsoft Sentinel help you model connected security data from Sentinel data lake and external sources to visualize attack paths, uncover hidden relationships, and improve investigations.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: sourinpaul
ms.date: 2026-08-07T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
locale: en-us
document_id: 84243aab-28ee-6468-a17e-403a7350d2d0
document_version_independent_id: a4174a91-fa92-b6e0-1c85-360f448a4d10
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/custom-graphs-overview.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/custom-graphs-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/custom-graphs-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
platformId: 0edfa54d-a7b3-6246-4689-b6cc3176cb3f
---

# Custom Graphs in Microsoft Sentinel Overview (Preview) | Microsoft Learn

Custom graphs let you build tailored security graphs tuned to your unique security scenarios using data from Sentinel data lake as well as non-Microsoft sources. With custom graph, powered by Fabric, you can build, query, and visualize connected data, uncover hidden patterns and attack paths, and help surface risks that are hard to detect when data is analyzed in isolation. Custom graphs provide the knowledge context that enables AI-powered agent experiences to work more effectively, speeding investigations, revealing blast radius, and helping you move from noisy, disconnected alerts to confident decisions at scale.

## Common scenarios

These scenarios show a sample of what’s possible with custom graphs. You can model any entities, relationships, and data from the Sentinel data lake. Build graphs tailored to your security workflows and investigative needs.

| Scenario | Key questions that graph can help answer |
| --- | --- |
| **Phishing email kill chain with enriched business context** | - Who received the phishing email, who clicked on the links, and which clicks were actually allowed by the proxy?- Which emails point to the same URL, revealing waves using shared infrastructure ? Follow attachment → download → process execution → device to show the chain from inbox to compromise. |
| **DNS C2 beacon hunter** | - Show device to domain activity that exhibits beaconing behavior (low interval variance and high time coverage), separating automated traffic from human browsing.- Follow the full evidence chain from device → DNS query → resolved IP → threat indicator. |
| **Behavioral attack chain detection** | - Show all IPs/users that touch behaviors mapped to 3 or more different MITRE techniques.- Follow the full path from a threat indicator through the matched IP through all associated behaviors to every affected user. |
| **OAuth privilege escalation** | - Show service principals that granted permissions to themselves, then chained those permissions to reach a Tier Zero directory role. Self escalation cycle signature. |

## Building custom graphs in Microsoft Sentinel

Use the Jupyter notebooks in Microsoft Visual Studio Code to interactively create and analyze custom graphs with your data in the Microsoft Sentinel data lake. The notebooks are provided by the Microsoft Sentinel Visual Studio Code extension that allows you to interact with the Microsoft Sentinel data lake using Python for Spark (PySpark). For more information on the Microsoft Sentinel Visual Studio Code extension, see [Install Visual Studio Code and the Microsoft Sentinel extension](notebooks#install-visual-studio-code-and-the-microsoft-sentinel-extension).

You can author custom graphs using either AI‑assisted graph authoring or by writing your own code. Use the Microsoft Sentinel graph provider reference to define the nodes and edges in your graph model, transform your data from the Sentinel data lake, and query your graphs with Graph Query Language (GQL). For more information, see [AI-assisted custom graph authoring in Microsoft Sentinel](create-graphs-with-ai), [Microsoft Sentinel graph provider reference](sentinel-graph-provider-reference) and [Graph Query Language (GQL) reference for Sentinel custom graph](gql-reference-for-sentinel-custom-graph).

After you author the graph code in a notebook, run the notebook in an interactive session or publish a graph job. Graphs created during an interactive notebook session are temporary and available only in that session. An on-demand graph job materializes the graph for 30 days and then deletes it. A scheduled graph job rebuilds the graph on the refresh schedule you configure. You can access a materialized graph from the graph experience under Microsoft Sentinel in the Defender portal, Visual Studio Code notebooks, and graph query APIs.

Creating and querying custom graphs is billed under the Microsoft Sentinel graph meter. For more information, see [Graph charges](../billing#graph-charges).

The following table summarizes the steps to build custom graphs in Microsoft Sentinel:

| Step | Description |
| --- | --- |
| **1. Create and investigate a graph in an interactive notebook session** | - Jupyter notebooks in Microsoft Sentinel provide an interactive environment for exploring and analyzing data in the Microsoft Sentinel data lake.- The Microsoft Sentinel extension includes the `sentinel_graph` Python library.- Use a Jupyter notebook to define nodes and edges with data from the Microsoft Sentinel data lake and create graphs.- Use the `sentinel_graph` library to query a graph with Graph Query Language (GQL). |
| **2. Schedule a graph job to materialize your graph** | - Materialize your graph in your tenant for continued access and collaboration.- Use Sentinel jobs to tailor how often you want to refresh a materialized graph with Lake data.- Query and visualize materialized graphs in graph experience in Microsoft Sentinel. |
| **3. Run advanced graph algorithms** | - Use Jupyter notebooks for accessing built-in support for GraphFrames analytics and graph traversal functions.- Use purpose-built Sentinel graph algorithms for common security use cases. |

For detailed instructions on how to build custom graphs in Microsoft Sentinel, see [Custom graphs in Microsoft Sentinel](create-custom-graphs).

## Visualizing graphs in Microsoft Sentinel

Microsoft Sentinel provides multiple options for visualizing graphs, including the graphs experience Microsoft Sentinel, Jupyter notebooks in the Sentinel Visual Studio Code extension. The graph experience lets you run Graph Query Language (GQL) queries, view the graph schema (the defined node and edge types), visualize the graph, view graph results in tabular format, and interactively traverse the graph to the next hop with a simple click.

[![Screenshot of the Sentinel graph in Microsoft Sentinel showing a graph visualization.](media/custom-graphs-overview/graph-exploration-phishing-query.png)](media/custom-graphs-overview/graph-exploration-phishing-query.png#lightbox)

For more information on visualizing graphs in Microsoft Sentinel using Sentinel graph, see [Visualize graphs in Microsoft Sentinel graph (preview)](graph-visualization).