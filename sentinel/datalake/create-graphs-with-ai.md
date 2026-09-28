---
layout: Conceptual
title: AI-assisted custom graph authoring in Microsoft Sentinel (preview) - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/create-graphs-with-ai
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
description: Use AI assistance in Visual Studio Code to create, modify, and query custom security graphs using Jupyter notebooks and GitHub Copilot.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: sourinpaul
ms.topic: how-to
ms.date: 2026-06-12T00:00:00.0000000Z
ms.collection: ms-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: 70bb1961-cc4d-66a9-cc25-28a76e86d525
document_version_independent_id: 6257cacc-d0cb-1245-3c1b-d70c0c9239e0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/create-graphs-with-ai.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/create-graphs-with-ai
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/create-graphs-with-ai.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/341fdab2-4964-4759-8241-f5820b012a47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cc1f92bb-c0d6-4d40-99ce-dabea3161a84
platformId: 5ae041fb-b35f-e540-088b-71904fd9aeda
---

# AI-assisted custom graph authoring in Microsoft Sentinel (preview) - Microsoft Security | Microsoft Learn

Use GitHub Copilot in Visual Studio Code with Microsoft Sentinel to create, modify, and query custom security graphs using Jupyter notebooks. Describe what you want to build in natural language, review the generated notebook, and refine it as needed.

Use Copilot for various graph authoring tasks, including:

- Create a complete graph authoring notebook from a description
- Modify or debug an existing graph
- Understand generated graph code
- Write and run graph queries

## How AI assistance works for custom graphs

When you work in a Jupyter notebook connected to Microsoft Sentinel, GitHub Copilot can help with graph authoring tasks using natural-language prompts.

Use the following workflow to interact with Copilot for graph authoring:

1. Describe the graph or change you want to make.
2. Copilot generates or updates graph-related code.
3. You review, run, and iterate on the results.

For graph-specific scenarios, Microsoft Sentinel provides optional helpers that give Copilot additional context about graph APIs, schemas, and your workspace. These helpers improve accuracy and consistency but aren't required to use Copilot assistance.

## Prerequisites

Before you begin, make sure you have:

- **The Microsoft Sentinel extension for Visual Studio Code** installed and signed in. For more information, see [Run notebooks on the Microsoft Sentinel data lake](notebooks).
- **The Jupyter extension for Visual Studio Code** installed. Download from the [VS Code Extensions Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter).
- **GitHub Copilot** installed and enabled. For more information, see [GitHub Copilot extension](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot).
- **GitHub Copilot Business or Copilot Enterprise plan**, see [GitHub Copilot plans](https://github.com/features/copilot#pricing)
- **A Microsoft Sentinel data lake** configured with appropriate permissions. For more information, see [Onboarding to Microsoft Sentinel data lake](sentinel-lake-onboarding).

## Create and edit a custom graph with Copilot

Use the following steps to create a new graph or modify an existing one using GitHub Copilot:

1. Open an existing Jupyter notebook (`.ipynb`), or allow Copilot to create one.
2. Open GitHub Copilot Chat (**Ctrl+Shift+I** on Windows, **Cmd+Shift+I** on macOS).
3. Describe the graph you want to build.

For best results when creating or modifying a full graph, use the Sentinel graph authoring helper by including `@sentinel /graph-authoring` in your prompt. This provides Copilot with additional context about graph APIs, schemas, and best practices.

```text
@sentinel /graph-authoring Create a graph that maps email senders to recipients and URLs using EmailEvents
```

The assistant generates a complete notebook that follows the standard graph authoring lifecycle:

| Step | Description |
| --- | --- |
| Environment setup | Verifies required packages and connection information |
| Data loading | Reads tables from the Sentinel data lake |
| Data transformation | Prepares node and edge data |
| Graph schema | Defines nodes and edges |
| Schema validation | Validates the graph definition |
| Graph build | Materializes the graph |
| Graph query | Runs graph queries |

### Refine the graph

Once the graph is created, you can continue the conversation to refine it, for example:

```text
@sentinel Add an edge from User to IPAddress
```

```text
@sentinel Filter the data to show only failed sign-ins
```

## Modify or debug an existing graph

Ask Copilot to update or fix specific parts of your notebook. For example, you can change filters, adjust columns, or troubleshoot build errors:

```text
@sentinel Change the time range to the last 7 days
```

The following prompt asks Copilot to modify a specific notebook cell by adding a field to the output:

```text
@sentinel Update cell 3 to include the Subject column
```

The following prompt asks Copilot to troubleshoot and repair a failure in the graph build stage:

```text
@sentinel Fix the error in the graph build step
```

Only the affected cells are updated. Other cells remain unchanged.

## Understand graph code and queries

Ask questions about the generated code without changing the notebook. For example, the following prompt asks Copilot to explain the purpose of a specific graph API helper method:

```text
@sentinel What does show_schema() do?
```

The following prompt asks Copilot to clarify how edge keys are modeled in Sentinel graph schemas:

```text
@sentinel Explain how edge keys are defined
```

The following prompt asks Copilot to explain the logic of a graph query step by step:

```text
@sentinel How does this graph query work?
```

## Look up graph APIs and examples

If you want help with Sentinel graph APIs, method parameters, or example queries, you can ask Copilot for explanations. For more accurate, Sentinel-specific answers, include the `#Sentinel` reference helper in your prompt. For example, the following prompt asks Copilot for reference-style information about the `build_graph_with_data()` method signature:

```text
What parameters does build_graph_with_data() accept? #sentinel
```

The following example asks Copilot to generate a graph traversal query between two entity types:

```text
Write a graph query to find all paths between User and IPAddress #sentinel
```

This helper provides Copilot with authoritative Sentinel graph API documentation. The `#sentinel` reference helper doesn't modify your notebook.

## Choose how to interact with Copilot

Use the following table to choose the best way to interact with Copilot based on your goal:

| What you want to do | Recommended approach |
| --- | --- |
| Create or modify a graph notebook | Describe your goal (use `@sentinel` for best results) |
| Fix or debug a graph error | Describe the problem (use `@sentinel`) |
| Ask about graph APIs or parameters | Ask a question (include `#sentinel`) |
| Ask a general question | Plain Copilot prompt |

## Key concepts

The following concepts are important to understand when using AI-assisted graph authoring.

### Workspace and table availability

AI assistance uses the tables visible in your Sentinel data lake. Only tables you have access to are used in generated code.

Important

If a table doesn't appear in the data lake explorer, it can't be used for graph authoring.

### Notebook changes

When modifying a notebook, only the cells that need to change are updated. You can undo changes using standard editor undo commands.

## Troubleshooting

The following table lists common issues and how to resolve them.

| Issue | Resolution |
| --- | --- |
| No notebook is open | Open or create a `.ipynb` file before starting graph authoring. |
| Tables are missing | Verify that your Sentinel data lake is connected and the expected tables appear in the data lake explorer. |
| Required packages are missing | Ensure your notebook is connected to a supported Sentinel Spark compute pool. |
| An unexpected cell was modified | Undo the change and retry the request, specifying the cell number. |