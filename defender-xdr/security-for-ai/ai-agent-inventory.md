---
layout: Conceptual
title: Discover AI agents and assess security posture using Microsoft Defender - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/security-for-ai/ai-agent-inventory
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to discover AI agents, review their risk and security posture, and access recommendations, incidents, alerts, and Advanced Hunting in Microsoft Defender.
ms.service: microsoft-defender
ms.author: guywild
author: guywi-ms
ms.reviewer: itaicohen
ms.topic: how-to
ms.date: 2026-07-14T00:00:00.0000000Z
audience: Admin
ai-usage: ai-assisted
locale: en-us
document_id: ccd22ac7-a931-e7fb-973f-6fdd1a8ca283
document_version_independent_id: ccd22ac7-a931-e7fb-973f-6fdd1a8ca283
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/security-for-ai/ai-agent-inventory.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-for-ai/ai-agent-inventory
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/security-for-ai/ai-agent-inventory.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 231aba6c-37d3-042b-fe60-27f0581557e9
---

# Discover AI agents and assess security posture using Microsoft Defender - Microsoft Defender XDR | Microsoft Learn

Microsoft Defender provides a centralized inventory of AI agents in your organization and assesses their security posture.

The inventory includes:

- Agents built with Microsoft Copilot Studio, Microsoft Foundry, Microsoft 365, and [supported non-Microsoft platforms](/en-us/microsoft-agent-365/admin/agent-registry).
- [Local AI agents](/en-us/defender-endpoint/local-agent-discovery-overview) discovered on endpoint devices.

Use the **AI Agents** page in the Microsoft Defender portal to review agent configuration, risk levels, risk indicators, recommendations, alerts, tools, identities, and related security context. You can also query agent inventory and configuration data by using Advanced Hunting.

## Prerequisites

- Enable security for AI agents, including the Microsoft 365 connector. See [Enable security for AI agents using Microsoft Defender](get-started-defender-security-for-ai).
- To discover local AI agents that run on endpoints, set up [AI agent runtime protection in Microsoft Defender for Endpoint](/en-us/defender-endpoint/configure-ai-agent-runtime-protection). Discovery requires Microsoft Defender for Endpoint and Microsoft Defender Antivirus in active mode. Local agents are onboarded separately.

## Review AI agent risk and security posture

Microsoft Defender calculates an agent's risk level from its active risk indicators. Security recommendations identify available actions for improving the agent's posture but are calculated separately from the risk level.

The available risk indicators, recommendations, tabs, and supporting evidence depend on the agent type and the security information available for that agent.

To review the risk and security posture of AI agents:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. In the left navigation pane, select **Assets** &gt; **AI agents**.
3. Select the **Agents** tab.

    The inventory includes the following risk-related columns:

    - **Risk level**: The overall risk level calculated from the agent's active risk indicators.
    - **Risk indicators**: The conditions contributing to the agent's risk level.
    - **Recommendations**: The number and severity of active security recommendations for the agent.
    - **Active alerts**: The number and severity of active alerts associated with the agent.

    [![Screenshot that shows the AI Agents page in the Defender portal with the Agents tab selected, displaying agent name, platform, publish status, MCP servers count, discovered tools, active alerts, and creation time columns.](media/ai-agent-inventory/ai-agent-inventory.png)](media/ai-agent-inventory/ai-agent-inventory.png#lightbox)
4. Use the filter bar to narrow the inventory by properties such as **Agent name**, **Platform**, **Publish status**, **Risk level**, or **Risk indicators**.
5. Select **Customize columns** to add, remove, or reorder columns in the inventory.
6. Select an agent to open its details pane.

    The pane displays the risk and configuration information available for the selected agent.

    [![Screenshot of the AI agent inventory in the Defender portal showing the agent details pane for a selected Copilot Studio agent, including description, version, publish status, creation time, model, tools, channels, and MCP servers.](media/ai-agent-inventory/ai-agent-details-pane.png)](media/ai-agent-inventory/ai-agent-details-pane.png#lightbox)
7. Select **Open Agent page** to review more information about the agent.

    The **Overview** tab shows the security and configuration information available for the agent, which can include:

    - Risk level and active risk indicators
    - Agent configuration details
    - Identity and authentication information
    - Endpoint and user context, when available
    - Attack-surface relationships
    - Active alerts
    - Security recommendations
    - Tools
    - MCP servers
8. Review any additional tabs available for the agent:

    - Select **Security recommendations** to review posture recommendations associated with the agent. Select a recommendation to review its description and supporting evidence on the **Overview** tab, corrective actions on the **Remediation steps** tab, and affected agents on the **Exposed assets** tab.
    - Select **Incidents and alerts** to review security incidents and alerts associated with the agent. Select an incident to open its details pane, or select **Open incident page** for the full investigation experience.

    The available tabs depend on the agent platform and the security information associated with the agent.

For details about risk indicators, risk levels, and recommendation logic, see [AI agent posture risk in Microsoft Defender](ai-agent-risk-assessment).

For more information about investigating agent threats, see [Detect and investigate threats to AI agents using Microsoft Defender](ai-agent-detection-protection).

## Discover and assess AI agents using Advanced Hunting

The [AgentsInfo table](/en-us/defender-xdr/advanced-hunting-agentsinfo-table) in Advanced Hunting provides an inventory of AI agents and their security-relevant properties.

Use the table to:

- Discover AI agents in your environment.
- Review available agent properties, such as authentication, access control, tools, knowledge sources, orchestration settings, endpoint context, and user context.
- Correlate agent inventory information with other security data.

Note

The `AgentsInfo` table replaces the previous `AIAgentsInfo` table as part of the Microsoft Agent 365 transition. For more information, see [Transition Microsoft Copilot Studio and Microsoft Foundry agent security capabilities to Microsoft Agent 365](transition-agent-security-to-agent-365).

To query agent inventory data:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. Select **Investigation & response** &gt; **Hunting** &gt; **Advanced hunting**.
3. Query the `AgentsInfo` table.

    To use the prebuilt queries maintained by Microsoft, select the **Queries** tab, and then select **AI Agents**. For more information, see [Sample queries](/en-us/defender-xdr/advanced-hunting-agentsinfo-table).

    To return the latest record for each agent, run the following query:

    ```kusto
    AgentsInfo
    | summarize arg_max(Timestamp, *) by AgentId
    | where LifecycleStatus != "Deleted"
    ```

[![Screenshot of Advanced Hunting in Microsoft Defender showing an AgentsInfo query and agent inventory results.](media/ai-agent-inventory/advanced-hunting-ai-agents-query.png)](media/ai-agent-inventory/advanced-hunting-ai-agents-query.png#lightbox)

Important

The `AgentsInfo` table stores multiple snapshots of each agent over time. Use `arg_max(Timestamp, *)` to return the latest state of each agent. For more information, see [arg_max() aggregation function](/en-us/kusto/query/arg-max-aggregation-function).

For more information:

- To query local agents discovered on endpoint devices, see [Discover local AI agents in Microsoft Defender for Endpoint](/en-us/defender-endpoint/discover-local-ai-agents).
- For information about Advanced Hunting, see [Proactively hunt for threats with Advanced Hunting in Microsoft Defender](/en-us/defender-xdr/advanced-hunting-overview).