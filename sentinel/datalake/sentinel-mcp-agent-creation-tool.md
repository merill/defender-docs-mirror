---
layout: Conceptual
title: Agent Creation Tool Collection in Microsoft Sentinel MCP Server - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/sentinel-mcp-agent-creation-tool
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
description: Learn about the different tools available in the Agent creation collection in Microsoft Sentinel
ms.author: pauloliveria
author: poliveria
ms.reviewer: macasgra
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: fea2ade1-4546-7007-705d-a152613e666f
document_version_independent_id: d99b482c-6580-c2b4-9a55-3dc85eb7f56f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/sentinel-mcp-agent-creation-tool.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/sentinel-mcp-agent-creation-tool
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/sentinel-mcp-agent-creation-tool.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
platformId: 5c2d3d4c-71ab-d599-7bb5-ad97f1c9820a
---

# Agent Creation Tool Collection in Microsoft Sentinel MCP Server - Microsoft Security | Microsoft Learn

The agent creation tool collection in the Microsoft Sentinel Model Context Protocol (MCP) server lets you create effective Microsoft Security Copilot agents. This article explains how to add the tool collection to your code editor and describes each tool and its parameters. Before you start, make sure you meet the prerequisites.

## Prerequisites

To access the agent creation tool collection, you must have the following prerequisites:

- [Microsoft Security Copilot](/en-us/copilot/security/microsoft-security-copilot)
- Any of the supported AI-powered code editors and agent-building platforms:
    - [Visual Studio Code](sentinel-mcp-use-tool-visual-studio-code)

## Add the agent creation collection

The Microsoft Sentinel unified MCP server exposes Sentinel tool collections, including the agent creation collection, to supported code editors and agent-building platforms. To get started, set up the unified MCP server. Follow the steps in [Get started with Microsoft Sentinel MCP server](sentinel-mcp-get-started#add-microsoft-sentinels-collection-of-mcp-tools) for your code editor or agent-building platform.

When you configure your code editor's MCP settings, use the following endpoint URL for the Security Copilot agent creation tool collection. Enter this URL as the MCP server endpoint to connect your editor to the agent creation tools:

```text
https://sentinel.microsoft.com/mcp/security-copilot-agent-creation
```

After adding the agent creation tool collection, you can use the following sample prompt to create complex, agentic workflows in Security Copilot:

- Create an agent that generates a comprehensive post-incident report from Microsoft Defender, Microsoft Purview, and Microsoft Sentinel incidents; aggregates incident summaries, detailed insights, entities, and alerts; and provides actionable remediation steps.

## Tools in the agent creation collection

The following tools help you search for capabilities, create, compose, evaluate, and deploy Security Copilot agents.

### Search for tools (`search_for_tools`)

This tool finds relevant tools, including skills, agents and MCP tools, in Security Copilot that can be used to fulfill the intent.

| Parameters | Required? | Description |
| --- | --- | --- |
| `userQuery` | Yes | The query or problem statement to find relevant tools for (for example, "Defender incident details"). |

### Start agent creation (`start_agent_creation`)

This tool creates a new Security Copilot session to start building a new agent.

| Parameters | Required? | Description |
| --- | --- | --- |
| `userQuery` | Yes | The problem statement for the agent. |

### Compose agent (`compose_agent`)

This tool iterates on composing the Security Copilot agent definition in YAML (a structured text format used for configuration).

| Parameters | Required? | Description |
| --- | --- | --- |
| `sessionID` | Yes | Security Copilot session identifier created by the `start_agent_creation` tool. This shouldn't be the session identifier created by `search_for_tools`. |
| `userQuery` | Yes | User input for the tool to process. This could be confirmations, clarifications, or additional information. |
| `existingDefinition` | No | Optional existing agent definition YAML for the tool to edit. This could be generated from this tool's previous runs or provided by adding a YAML file to the context. |

### Get evaluation (`get_evaluation`)

This tool is called after running the `search_for_tools`, `start_agent_creation`, and `compose_agent` tools to retrieve the result.

| Parameters | Required? | Description |
| --- | --- | --- |
| `sessionID` | Yes | Session identifier of the evaluation |
| `promptID` | Yes | Prompt identifier of the evaluation |
| `evaluationID` | Yes | The identifier of the evaluation |

### Deploy agent (`deploy_agent`)

This tool uploads the agent to the Security Copilot user or workspace scope.

| Parameters | Required? | Description |
| --- | --- | --- |
| `agentDefinition` | Yes | Agent definition in YAML format. This could be generated from the `compose_agent` tool or provided by adding a YAML file to the context. |
| `scope` | Yes | Scope to upload the agent to. This can be `User` or `Workspace` only. |
| `agentSkillsetName` | Yes | Agent skill set name. This must exactly match the `Name` value under **Descriptor** in the agent definition YAML. |