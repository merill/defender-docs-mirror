---
layout: Conceptual
title: Microsoft Defender for Endpoint AI agent support matrix - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/ai-agent-support-matrix
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn which local AI agents, MCP server configurations, and runtime protection methods Microsoft Defender for Endpoint supports.
author: j0shbregman
ms.author: joshbregman
ms.service: defender-endpoint
ms.topic: concept-article
ms.custom: msecd-doc-authoring-1030
ms.date: 2026-10-07T00:00:00.0000000Z
ai-usage: ai-generated
locale: en-us
document_id: abe9e026-5716-699f-a004-f1f31a28907b
document_version_independent_id: abe9e026-5716-699f-a004-f1f31a28907b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/ai-agent-support-matrix.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: ai-agent-support-matrix
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/ai-agent-support-matrix.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/341fdab2-4964-4759-8241-f5820b012a47
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cc1f92bb-c0d6-4d40-99ce-dabea3161a84
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
platformId: fbba1eb6-4eb3-53ec-5a39-1699f4762ddc
---

# Microsoft Defender for Endpoint AI agent support matrix - Microsoft Defender for Endpoint | Microsoft Learn

The Microsoft Defender for Endpoint AI agent support matrix identifies the local AI agents and related scenarios that Defender supports for discovery and runtime protection. Discovery support and runtime protection support are listed separately because they have different operating system and integration requirements.

Only supported combinations appear in the matrix. If a combination isn't listed, it isn't currently documented as supported.

## AI agent discovery support

AI agent discovery identifies local AI agents and their configured Model Context Protocol (MCP) servers on onboarded devices. The `Name` values in these tables correspond to the `Name` column in the [`AgentsInfo`](/en-us/defender-xdr/advanced-hunting-agentsinfo-table) advanced hunting table. The `Vendor` values correspond to `RawAgentInfo.localAgentMetadata.vendor`.

Discovery is activity based. Defender lists an agent after it observes agent activity on an onboarded device. Installing an agent doesn't by itself guarantee that the agent appears in the local AI agent inventory. For more information about how Defender observes agent activity and how this inventory differs from an inventory of installed software, see [Local AI agent discovery with Microsoft Defender for Endpoint](local-agent-discovery-overview).

A checkmark in the **Discovers MCP** column indicates that Defender reports remote MCP server data in `McpServers` and local MCP server data in `RawAgentInfo.localAgentMetadata.localMcps`. A dash indicates that MCP server configuration discovery isn't documented for that combination.

A checkmark in the **Discovers agent** column indicates that Defender supports discovery of that local AI agent.

Use the values in the `Name` and `Vendor` columns in your advanced hunting queries. For examples, see [Get an inventory of local AI agents](discover-local-ai-agents#get-an-inventory-of-local-ai-agents) and [Review the MCP servers and tools that local AI agents use](discover-local-ai-agents#review-the-mcp-servers-and-tools-that-local-ai-agents-use).

Note

For runtime protection support, see AI agent runtime protection support.

### Windows

| `Name` | `Vendor` | Discovers agent | Discovers MCP |
| --- | --- | --- | --- |
| Amp CLI | Amp | ✓ | - |
| Antigravity CLI | Google | ✓ | ✓ |
| Antigravity Desktop | Google | ✓ | ✓ |
| Antigravity IDE | Google | ✓ | ✓ |
| Buzz | Block | ✓ | - |
| ChatGPT Classic | OpenAI | ✓ | - |
| ChatGPT Desktop | OpenAI | ✓ | ✓ |
| Claude Code | Anthropic | ✓ | ✓ |
| Claude Desktop | Anthropic | ✓ | ✓ |
| Clawpilot | Microsoft | ✓ | - |
| Cline CLI | Cline | ✓ | - |
| CoCo CLI | Snowflake | ✓ | - |
| CoCo Desktop | Snowflake | ✓ | - |
| Codex CLI | OpenAI | ✓ | ✓ |
| Codex Desktop | OpenAI | ✓ | ✓ |
| Cursor | Anysphere | ✓ | ✓ |
| DeepSeek Harness | DeepSeek | ✓ | - |
| Devin CLI | Cognition | ✓ | - |
| Devin Desktop | Cognition | ✓ | ✓ |
| Foundry Local | Microsoft | ✓ | - |
| Gemini CLI | Google | ✓ | ✓ |
| GitHub Copilot App | GitHub | ✓ | ✓ |
| GitHub Copilot CLI | GitHub | ✓ | ✓ |
| Goose CLI | Agentic AI Foundation | ✓ | - |
| Goose Desktop | Agentic AI Foundation | ✓ | - |
| Grok Bot | SpaceXAI | ✓ | - |
| Grok Build | SpaceXAI | ✓ | - |
| Hermes Agent | Nous Research | ✓ | - |
| Junie CLI | JetBrains | ✓ | ✓ |
| Kilo CLI | Kilo Code | ✓ | - |
| Kimi Code CLI | Moonshot AI | ✓ | - |
| Kiro CLI | Amazon | ✓ | ✓ |
| Kiro IDE | Amazon | ✓ | ✓ |
| LM Studio | Element Labs | ✓ | - |
| LM Studio Bionic | Element Labs | ✓ | - |
| Microsoft Scout | Microsoft | ✓ | - |
| Nanobot | Claw | ✓ | - |
| Oh My Pi | Stencil | ✓ | - |
| Ollama Desktop | Ollama | ✓ | - |
| OpenClaw | OpenClaw Foundation | ✓ | ✓ |
| OpenCode | Anomaly | ✓ | ✓ |
| Perplexity Desktop | Perplexity | ✓ | - |
| Pi Coder | Earendil Works | ✓ | - |
| Poe Desktop | Quora | ✓ | - |
| QClaw | Tencent | ✓ | - |
| Qwen Code | Alibaba Cloud | ✓ | - |
| Qwen Code Desktop | - | ✓ | - |
| Qwen Studio | Alibaba Cloud | ✓ | - |
| Trae IDE | ByteDance | ✓ | - |
| VSCode Claude Code Extension | Anthropic | ✓ | ✓ |
| VSCode Cline Extension | Cline | ✓ | ✓ |
| VSCode Codex Extension | OpenAI | ✓ | ✓ |
| VSCode Gemini Code Assist Extension | Google | ✓ | ✓ |
| VSCode GitHub Copilot Extension | GitHub | ✓ | ✓ |
| VSCode Kimi Code Extension | Moonshot AI | ✓ | - |
| VSCode Roo Code Extension | Roo Code | ✓ | ✓ |
| Warp | Warp | ✓ | ✓ |
| Windsurf | Cognition | ✓ | ✓ |
| ZCode | Z.ai | ✓ | - |
| ZeroClaw | Claw | ✓ | ✓ |

#### Windows Subsystem for Linux (preview)

The following local AI agents are supported when they run in Windows Subsystem for Linux (WSL). WSL support doesn't indicate support for native Linux endpoints.

| `Name` | `Vendor` | Discovers agent | Discovers MCP |
| --- | --- | --- | --- |
| Claude Code | Anthropic | ✓ | - |
| Codex CLI | OpenAI | ✓ | - |
| GitHub Copilot CLI | GitHub | ✓ | - |

### macOS (preview)

| `Name` | `Vendor` | Discovers agent | Discovers MCP |
| --- | --- | --- | --- |
| Antigravity CLI | Google | ✓ | - |
| Antigravity Desktop | Google | ✓ | - |
| Antigravity IDE | Google | ✓ | - |
| ChatGPT Classic | OpenAI | ✓ | - |
| ChatGPT Desktop | OpenAI | ✓ | ✓ |
| Claude Code | Anthropic | ✓ | ✓ |
| Claude Desktop | Anthropic | ✓ | ✓ |
| Clawpilot | Microsoft | ✓ | - |
| Cline CLI | Cline | ✓ | - |
| CoCo Desktop | Snowflake | ✓ | - |
| Codex CLI | OpenAI | ✓ | ✓ |
| Codex Desktop | OpenAI | ✓ | ✓ |
| Cursor | Anysphere | ✓ | ✓ |
| Devin CLI | Cognition | ✓ | ✓ |
| Devin Desktop | Cognition | ✓ | - |
| Foundry Local | Microsoft | ✓ | - |
| Gemini CLI | Google | ✓ | ✓ |
| GitHub Copilot App | GitHub | ✓ | ✓ |
| GitHub Copilot CLI | GitHub | ✓ | ✓ |
| Goose CLI | Agentic AI Foundation | ✓ | - |
| Goose Desktop | Agentic AI Foundation | ✓ | - |
| Grok Build | SpaceXAI | ✓ | - |
| Hermes Agent | Nous Research | ✓ | - |
| Junie CLI | JetBrains | ✓ | - |
| Kimi Code CLI | Moonshot AI | ✓ | - |
| Kiro CLI | Amazon | ✓ | - |
| Kiro IDE | Amazon | ✓ | - |
| LM Studio | Element Labs | ✓ | - |
| LM Studio Bionic | Element Labs | ✓ | - |
| Microsoft Scout | Microsoft | ✓ | - |
| Nanobot | Claw | ✓ | - |
| Ollama Desktop | Ollama | ✓ | ✓ |
| OpenClaw | OpenClaw Foundation | ✓ | ✓ |
| OpenCode | Anomaly | ✓ | ✓ |
| Perplexity Desktop | Perplexity | ✓ | - |
| Pi Coder | Earendil Works | ✓ | - |
| Poe Desktop | Quora | ✓ | - |
| QClaw | Tencent | ✓ | - |
| Qwen Code | Alibaba Cloud | ✓ | - |
| Qwen Studio | Alibaba Cloud | ✓ | - |
| Trae IDE | ByteDance | ✓ | - |
| VSCode Claude Code Extension | Anthropic | ✓ | ✓ |
| VSCode Cline Extension | Cline | ✓ | ✓ |
| VSCode Codex Extension | OpenAI | ✓ | ✓ |
| VSCode Gemini Code Assist Extension | Google | ✓ | ✓ |
| VSCode GitHub Copilot Extension | GitHub | ✓ | ✓ |
| VSCode Kimi Code Extension | Moonshot AI | ✓ | - |
| VSCode Roo Code Extension | Roo Code | ✓ | - |
| Warp | Warp | ✓ | ✓ |
| Windsurf | Cognition | ✓ | - |
| ZeroClaw | Claw | ✓ | - |

## AI agent runtime protection support

Support is organized by the method Defender uses to inspect agent activity.

Runtime protection support doesn't indicate that protection is enabled on a device. To configure audit or block mode, see [Set up AI agent runtime protection with Microsoft Defender for Endpoint](configure-ai-agent-runtime-protection).

A dash indicates that a mode or minimum version doesn't apply or isn't specified.

### Windows (preview)

The following tables list agent and inspection method combinations on Windows.

#### Agent-native event inspection

Agent-native event inspection uses vendor-supported event interfaces. The hooks documentation links describe the applicable vendor interface.

| AI agent or application | Mode | Minimum versions | Hooks documentation |
| --- | --- | --- | --- |
| Claude Code | - | - | [Claude Code hooks](https://code.claude.com/docs/en/hooks) |
| GitHub Copilot CLI | - | - | [GitHub Copilot CLI hooks](https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/use-hooks) |
| GitHub Copilot app | - | - | [GitHub Copilot hooks reference](https://docs.github.com/copilot/reference/hooks-reference) |
| Claude Desktop | Code | - | [Claude Code hooks](https://code.claude.com/docs/en/hooks) |
| VS Code GitHub Copilot extension | - | - | [GitHub Copilot hooks reference](https://docs.github.com/copilot/reference/hooks-reference) |
| VS Code Claude Code extension | - | - | [Claude Code hooks](https://code.claude.com/docs/en/hooks) |

#### Network inspection

Network inspection covers agents that communicate with LLMs through well-known inference services. It doesn't cover agents that use certificate pinning or HTTP/3.

| AI agent or application | Mode | Minimum versions |
| --- | --- | --- |
| OpenClaw | - | - |
| Ollama Desktop | - | - |
| ChatGPT Classic | - | - |
| ChatGPT Desktop | Chat | ChatGPT Desktop 26.810.52044 (minimum tested) |