---
layout: Conceptual
title: What is Microsoft Sentinel MCP server's tool collection? - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/sentinel-mcp-tools-overview
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
description: Learn about the different MCP collection of tools in Microsoft Sentinel
ms.author: pauloliveria
author: poliveria
ms.reviewer: macasgra
ms.topic: article
ms.date: 2026-05-04T00:00:00.0000000Z
locale: en-us
document_id: 103e1a5f-e693-ed3d-deba-996518b32f6d
document_version_independent_id: f10ce701-ed83-fb49-75ce-9bdc2800e763
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/sentinel-mcp-tools-overview.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/sentinel-mcp-tools-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/sentinel-mcp-tools-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 639e8c86-f529-7b27-2ff9-17fe0d97f06a
---

# What is Microsoft Sentinel MCP server's tool collection? - Microsoft Security | Microsoft Learn

Microsoft Sentinel’s Model Context Protocol (MCP) Server collections are logical groupings of related security-focused MCP tools that you can use in any [compatible client](sentinel-mcp-get-started#add-microsoft-sentinels-collection-of-mcp-tools) to:

- Search for relevant tables
- Retrieve data
- Analyze entities
- Create Security Copilot agents
- Triage incidents
- Hunt for threats

Our collections are scenario-focused and have security-optimized descriptions that help AI models pick the right tools and deliver those outcomes. For example, you can use the following sample prompts to get the appropriate tool:

- Find the top three users that are at risk and explain why they're at risk.
- Find sign-in failures in the last 24 hours and give me a brief summary of key findings.
- Identify devices that showed an outstanding number of outgoing network connections.
- Help me understand if the user &lt;user object ID&gt; is compromised.
- Investigate users with a password spray alert in the last seven days and tell me if any of them are compromised.
- Find all the URL IOCs from &lt;threat analytics report&gt; and analyze them to tell me everything Microsoft knows about them.

## Available collections

The following table lists the available collections you can use:

| Collection | Description | Server URL |
| --- | --- | --- |
| [Data exploration](sentinel-mcp-data-exploration-tool) | Explore security data in Microsoft Sentinel data lake by searching for relevant tables, querying the lake, and analyzing entities | `https://sentinel.microsoft.com/mcp/data-exploration` |
| [Security Copilot agent creation](sentinel-mcp-agent-creation-tool) | Create Microsoft Security Copilot agents for complex workflows | `https://sentinel.microsoft.com/mcp/security-copilot-agent-creation` |
| [Triage](sentinel-mcp-triage-tool) | Triage incidents rapidly and hunt over your own data easily | `https://sentinel.microsoft.com/mcp/triage` |

## Create your own custom MCP tool

You can enable agents to retrieve and reason over knowledge from your library of saved Kusto Query Language (KQL) queries in [advanced hunting](/en-us/defender-xdr/advanced-hunting-microsoft-defender?toc=%2Fazure%2Fsentinel%2FTOC.json&amp;bc=%2Fazure%2Fsentinel%2Fbreadcrumb%2Ftoc.json) by using custom MCP tools. Creating your own Sentinel MCP tools lets you have granular control over the data accessible to your security agents and create deterministic agentic workflows.

For more information, see [Create and use custom Microsoft Sentinel MCP tools](sentinel-mcp-create-custom-tool).