---
layout: Conceptual
title: What is Microsoft Sentinel’s support for MCP? - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/sentinel-mcp-overview
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
description: Learn how Model Context Protocol (MCP)
author: mberdugo
ms.topic: overview
ms.date: 2026-05-07T00:00:00.0000000Z
ms.author: monaberdugo
locale: en-us
document_id: 7a3a1ca9-26ed-cc3e-2434-5e9b6ba953c0
document_version_independent_id: dd3e812a-6e09-3541-4958-c02c3c3d4ad3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/sentinel-mcp-overview.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/sentinel-mcp-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/sentinel-mcp-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c6f99e62-1cf6-4b71-af9b-649b05f80cce
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3f56b378-07a9-4fa1-afe8-9889fdc77628
platformId: 262cfec2-e04f-2423-201a-5b6b6f13ed3a
---

# What is Microsoft Sentinel’s support for MCP? - Microsoft Security | Microsoft Learn

Microsoft Sentinel, Microsoft's security platform, introduces support for Model Context Protocol (MCP). This support includes multiple scenario-focused collections of security tools through a unified server interface. By using this support, you can interactively query security data in natural language and build effective security agents that can perform complex automation. This collection of security tools helps security teams bring AI into their daily security operations to assist with common tasks like data exploration, building agentic automation, and incident triage and threat hunting.

## Key features of Microsoft Sentinel’s support for MCP

The following features and benefits are part of Microsoft Sentinel’s MCP servers:

- **Unified, hosted interface for AI-driven security operations**: Microsoft Sentinel’s unified MCP server interface is fully hosted, requires no infrastructure deployment, and uses Microsoft Entra for identity. Security teams can connect compatible clients to streamline daily AI operations.
- **Scenario-focused and natural language security tools**: Microsoft Sentinel’s MCP support comes through scenario-focused collections of ready-to-use security tools. These collections help security teams interact and reason over security data in Microsoft Sentinel data lake and Microsoft Defender using natural language, removing the need for code-first integration, understanding data schema, or writing well-formed data queries.
- **Accelerated development of effective security agents**: Microsoft Sentinel’s collection of security tools automates discovery and retrieval of security data and delivers predictable, actionable responses to customize agents. This support speeds up efficient security agent creation and delivers better and highly effective security agents.
- **Cost-effective, context-rich security data integration**: The data lake lets you bring all your security data into Microsoft Sentinel cost-effectively, so you don't need to choose between coverage and cost. Microsoft Sentinel’s collection of tools natively integrates with the security data lake and Microsoft Defender, letting you build comprehensive security context engineering.

For more information on how AI is used within Microsoft Sentinel's unified MCP server, see [Application card: Microsoft Sentinel MCP server](sentinel-mcp-application-card).

## Introduction to MCP

The [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) is an open protocol that manages how language models interact with external tools, memory, and context in a safe, structured, and stateful way. MCP uses a client-server architecture with several components:

- **MCP host**: The AI application that coordinates and manages one or multiple MCP clients.
- **MCP client**: A component that maintains a connection to an MCP server and obtains context from an MCP server for the MCP host to use.
- **MCP server**: A program that provides context to MCP clients.

For example, Visual Studio Code acts as an MCP host. When Visual Studio Code establishes a connection to an MCP server, such as the Microsoft Sentinel MCP server for data exploration, the Visual Studio Code runtime instantiates an MCP client object that maintains the connection to the connected MCP server.

[Learn more about MCP architecture](https://modelcontextprotocol.io/docs/learn/architecture).

## Scenarios for using Microsoft Sentinel’s MCP collections

When you connect a [compatible client](sentinel-mcp-get-started#add-microsoft-sentinels-collection-of-mcp-tools) with Microsoft Sentinel’s MCP collections, you can use tools to:

- **Interactively explore long term security data**: Security analysts and threat hunters, like those focusing on identity-based attacks, need to quickly query and correlate data across various security tables. Today, they must have knowledge of all tables and what data each table contains. With the data exploration collection, analysts can now use natural language prompts to search and retrieve relevant data from tables in Microsoft Sentinel data lake without needing to remember tables and their schema or writing well-formed Kusto Query Language (KQL) queries.

    For example, an analyst can look for possible insider threats by correlating file activity with Purview sensitivity label to uncover signs of data exfiltration, policy violations, or suspicious user behavior that might have gone unnoticed during the original 90 to 180 day/time window. This interactive approach accelerates threat discovery and investigation while reducing reliance on manual query formulation.

    [Get started with data exploration over long term data](sentinel-mcp-data-exploration-tool)
- **Analyze entities across your security data:** Security Operations Center (SOC) engineers, analysts, and even agents need an easy way to analyze and triage entities, such as URLs and users, using all of an organization's security data. However, today’s fragmented data sources make this process complex and time-consuming to automate. As one of the most common incident triage tasks, entity enrichment therefore often becomes a manual context-gathering effort, slowing down response times. With the entity analyzer tools in the data exploration collection, analysts and SOC engineers have a one-click action that can retrieve, reason over, and clearly present comprehensive verdicts and analyses on entities using the security data in the data lake, making it easy to automate entity enrichment for you and the agents you build.

    [Get started with analyzing entities automatically during investigations](sentinel-mcp-data-exploration-tool#entity-analyzer)
- **Build Security Copilot agents through natural language:** SOC engineers often spend weeks manually automating playbooks due to fragmented data sources and rigid schema requirements. With the agent creation tools, engineers can describe their intent in natural language to quickly build agents with the right AI model instructions and tools that reason over their security data, creating automations that are customized to their organization's workflows and processes.

    [Get started with building agents](sentinel-mcp-agent-creation-tool)
- **Triage incidents and hunt for threats:** SOC engineers need to prioritize incidents rapidly and hunt over your organization’s own data easily without having to worry about security workflow issues and interoperability among platforms and tools that they use. The triage collection of tools integrates your AI models with APIs that support incident triage and hunting. This integration reduces mean time to resolution, risk exposure, and dwell time and empowers your team to leverage AI for smarter and faster decision-making.

    [Get started with incident triage and threat hunting](sentinel-mcp-triage-tool)