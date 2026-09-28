---
layout: Conceptual
title: AgentsInfo table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-agentsinfo-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about agent information in the AgentsInfo table of the advanced hunting schema
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.custom:
- cx-ti
- cx-ah
ms.topic: reference
ms.date: 2026-06-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 29e2e56f-100a-b517-81bd-b4eba89f59d8
document_version_independent_id: 29e2e56f-100a-b517-81bd-b4eba89f59d8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-agentsinfo-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-agentsinfo-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-agentsinfo-table.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: f0d38fa7-edfd-67a4-933c-45340e42fe5d
---

# AgentsInfo table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

Important

Some information relates to prereleased product that may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

The `AIAgentsInfo` table is transitioning to the `AgentsInfo` table. Microsoft Agent 365 customers should use the `AgentsInfo` table today. The `AIAgentsInfo` table remains accessible until July 1, 2026. Migrate your queries from `AIAgentsInfo` to `AgentsInfo` before this date. For more information, see [Advanced hunting schema - Naming changes](advanced-hunting-schema-changes).

The `AgentsInfo` table in the [advanced hunting](advanced-hunting-overview) schema contains information about AI agents and their properties from various platforms. Use this reference to construct queries that return information from this table.

For information on other tables in the advanced hunting schema, [see the advanced hunting reference](advanced-hunting-schema-tables).

| Column name | Data type | Description |
| --- | --- | --- |
| `Timestamp` | `datetime` | Date and time the agent information was recorded |
| `AgentId` | `string` | Unique identifier for the agent |
| `AgentName` | `string` | Display name of the agent |
| `Platform` | `string` | The platform that provided the information about the agent |
| `AgentDescription` | `string` | Description of the agent as displayed in the agent's source |
| `Version` | `string` | Version of the agent |
| `SourceAgentId` | `string` | Native identifier assigned by the platform where the agent originated |
| `EntraAgentId` | `string` | The agent's unique enterprise application object identifier by Microsoft Entra ID |
| `EntraBlueprintId` | `string` | The unique identifier by Microsoft Entra ID for the agent identity blueprint, which serves as the template from which the agent's identity was created |
| `ToolsAuthenticationType` | `dynamic` | Structured summary of agent identity, authentication, and authorization model |
| `Permissions` | `dynamic` | Permissions record of the agent, including those that have been requested and granted, their approval state, and consent enumeration |
| `PublishedStatus` | `string` | The agent's publication status; possible values: `Draft`, `Published` |
| `LifecycleStatus` | `string` | The agent's current operational state in the tenant; possible values: `Active`, `Blocked`, `Uninstalled`, `Deleted` |
| `Availability` | `string` | The deployment scope of the agent (that is, whether deployed to all users, specific groups, or individual users) |
| `CreatedDateTime` | `datetime` | Date and time when the agent was created |
| `LastPublishedDateTime` | `datetime` | Date and time when the agent was last published or deployed |
| `LastUpdatedDateTime` | `datetime` | Date and time when the agent's metadata was last modified |
| `Owners` | `dynamic` | Primary owners of the agent |
| `SharedWith` | `dynamic` | The users and security groups the agent has been shared with |
| `InstanceCount` | `int` | Number of agent instances created from the same Microsoft Entra ID agent identity blueprint |
| `Instructions` | `string` | The agent's system prompt that defines its default behavior, persona, and operating boundaries |
| `Model` | `string` | The AI model powering the agent |
| `Channels` | `dynamic` | The channels or surfaces where the agent can operate, such as Microsoft 365 applications or APIs |
| `Capabilities` | `dynamic` | The intents, actions, skills, and orchestrations of the agent |
| `DeclaredDataSources` | `dynamic` | The data repositories and knowledge sources the agent can access |
| `DeclaredTools` | `dynamic` | Functional tools the agent can invoke at runtime |
| `McpServers` | `dynamic` | The Model Context Protocol (MCP) servers connected to the agent, including server URLs and credential configuration |
| `Skills` | `dynamic` | Skills attached to the agent |
| `ConnectedAgents` | `dynamic` | List of other agents connected to the agent for multi-agent orchestration |
| `Memory` | `dynamic` | The agent's declarative memory store configuration |
| `Triggers` | `dynamic` | List of the agent's triggers |
| `Guardrails` | `dynamic` | Guardrails attached to the agent and their coverage |
| `Endpoints` | `dynamic` | List of agent runtime endpoints, including URL, transport type, and external connectivity flag |
| `ObservabilityId` | `dynamic` | Unique identifier used to correlate the agent with its usage and activity data in Microsoft Agent 365 |
| `RawAgentInfo` | `dynamic` | Additional information about the agent, in JSON format |