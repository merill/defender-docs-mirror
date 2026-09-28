---
layout: Conceptual
title: Local AI agent discovery with Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/local-agent-discovery-overview
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how Microsoft Defender discovers local AI agents and MCP servers configured on your devices through inventory and investigation capabilities.
author: lwainstein
ms.author: lwainstein
ms.service: defender-endpoint
ms.topic: overview
ms.date: 2026-09-16T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: d76258bb-b8c4-0e21-0c6a-94d5623ec4e6
document_version_independent_id: d76258bb-b8c4-0e21-0c6a-94d5623ec4e6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/local-agent-discovery-overview.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: local-agent-discovery-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/local-agent-discovery-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 5fbe46e6-1635-6e3d-c6d8-da353b0d5708
---

# Local AI agent discovery with Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Local AI agents run with user-level permissions and can access files, tools, and services on the devices where they operate. Without visibility into which agents are running and what they can reach, security teams can't assess exposure, enforce governance, or respond to agent-related incidents.

Microsoft Defender automatically discovers supported local AI agents and MCP server configurations on onboarded devices, then surfaces them in the Microsoft Defender portal. This gives security teams a centralized view of AI agent presence across the organization.

[![Screenshot showing the local AI agents inventory in the Microsoft Defender portal with discovered agents listed.](media/local-agent-discovery-overview/discovery-overview.png)](media/local-agent-discovery-overview/discovery-overview.png#lightbox)

This article explains how local AI agent discovery works, lists supported agents and MCP server configurations, and describes how to view discovered agents in the Microsoft Defender portal.

Tip

Defender also provides **AI agent runtime protection** for local agents. When enabled, runtime protection monitors activity in the agentic loop and blocks malicious instructions before the agent can act on them. For more information, see [AI agent runtime protection](ai-agent-runtime-protection-overview).

## Local AI agent discovery on endpoints

Defender automatically detects supported local AI agents and MCP server configurations on onboarded devices. When Defender identifies a supported local AI agent, the agent is displayed as a discoverable asset in the Microsoft Defender portal with visibility into:

- **Local AI agent inventory**: A centralized view of discovered local AI agents with device and user associations and discovery metadata.
- **Exposure map**: Visual relationships between local AI agents, devices, identities, and the resources those identities can access, to help assess potential impact.
- **Advanced hunting**: Hunting for discovery data using Kusto Query Language (KQL) to investigate local AI agents and the resources they can access based on the permissions of the user running them.

Note

Local AI agent discovery on macOS is in preview.

## Supported local AI agents and MCP server configurations

Defender defines an agent as a combination of a user, a device, and an agent type. For example, if Claude Code runs in 15 different project folders on the same device for the same user, it appears as a single agent entry in the inventory.

Defender discovers supported local AI agents on Windows and macOS endpoints. This includes agents that run from the command line, desktop apps, agentic IDEs, VS Code extensions, and Claw-based local agent implementations. When supported, Microsoft Defender also discovers MCP server configurations associated with these agents, including local and remote MCP server configurations.

Examples of supported local AI agents include:

- **CLI agents**: Claude Code, Codex CLI, Gemini CLI, GitHub Copilot CLI, Junie CLI, Kiro CLI, OpenCode, Warp, Antigravity CLI
- **Desktop apps**: ChatGPT Desktop, Claude Desktop, Codex Desktop, GitHub Copilot app, Goose Desktop, Hermes Agent, Microsoft Copilot app, Ollama Desktop, Perplexity Desktop, Poe Desktop
- **Agentic IDEs**: Cursor, Devin Desktop (formerly Windsurf), Kiro IDE, Antigravity IDE
- **VS Code extensions**: Claude Code, Cline, Codex, Gemini Code Assist, GitHub Copilot, Roo Code
- **Claw-based agents**: OpenClaw, Clawpilot, QClaw, Claw/Nanobot, ZeroClaw

For supported agents, Defender associates discovered MCP server configurations with the agent. The available configuration details can include the server name, type, endpoint, and the command used to start a local MCP server. An agent can have multiple configured MCP servers. To query these details, see [Review the MCP servers and tools that local AI agents use](discover-local-ai-agents#review-the-mcp-servers-and-tools-that-local-ai-agents-use).

To learn how to discover and view local AI agents, see [Discover local AI agents](discover-local-ai-agents).

## Broader AI security capabilities

Microsoft Defender's discovery capabilities are part of a comprehensive AI security approach. Microsoft Defender provides other capabilities across your organization's AI ecosystem:

- **Discover cloud and platform agents**: Find agents built with Microsoft Copilot Studio, Microsoft Foundry, Amazon Web Services (AWS) Bedrock, and Google Cloud Platform (GCP) Vertex AI.
- **Detect and investigate threats**: Correlate alerts and investigate suspicious agent behavior across your security infrastructure.

For details on these capabilities and how to apply them, see [Protect AI assets from emerging threats and vulnerabilities using Microsoft Defender](/en-us/defender-xdr/security-for-ai/defender-security-for-ai).