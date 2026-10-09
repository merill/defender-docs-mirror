---
layout: Conceptual
title: Discover local AI agents with Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/discover-local-ai-agents
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to discover, view, and investigate local AI agents on Windows and macOS devices by using Microsoft Defender.
author: lwainstein
ms.author: lwainstein
ms.service: defender-endpoint
ms.topic: how-to
ms.custom: msecd-doc-authoring-1030
ms.date: 2026-10-07T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 3ab263d3-69ba-bccb-3caf-8a3d135be6b6
document_version_independent_id: 3ab263d3-69ba-bccb-3caf-8a3d135be6b6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/discover-local-ai-agents.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: discover-local-ai-agents
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/discover-local-ai-agents.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: 02bd370a-d6ee-28a3-0704-0b8885819855
---

# Discover local AI agents with Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Microsoft Defender discovers supported AI agents and their MCP servers after it observes agent activity on onboarded devices and surfaces them in the AI agent inventory and advanced hunting. An installed agent might not appear until Defender observes agent activity. To learn more about local AI agent discovery, see [Local AI agent discovery with Microsoft Defender for Endpoint](local-agent-discovery-overview). For coverage by agent, operating system, and MCP server configuration, see [Microsoft Defender for Endpoint AI agent support matrix](ai-agent-support-matrix).

In this article, you learn how to view discovered agents in the inventory, review their configuration and risk, explore their relationships with devices and identities, and investigate agent presence using advanced hunting.

Note

Local AI agent discovery on macOS is in preview.

## Prerequisites

Before you can discover local AI agents on endpoints, make sure you meet the following requirements:

- Your environment is in the commercial cloud. Sovereign and national clouds aren't supported.
- Your organization has a Microsoft Defender for Endpoint Plan 2 license. For more information, see Licensing.
- Your devices are [onboarded to Microsoft Defender for Endpoint](onboard-configure).
- Your devices run a supported version of Windows or macOS, and Microsoft Defender Antivirus is updated with current monthly platform and engine updates.
- Microsoft Defender Antivirus is running in active mode on your devices, with real-time protection enabled.

You don't need additional deployment, configuration, or scripts beyond the device onboarding requirements. If the device meets all of the prerequisites, agent discovery begins automatically.

### Licensing

Microsoft Defender for Endpoint Plan 2 is the minimum license for local AI agent discovery. Security posture capabilities for the agents that Defender discovers require another license, as described in the following table.

| Capability | Required license |
| --- | --- |
| Discover local AI agents and view them in the AI agent inventory, including the agent details, the device and account, and the configured MCP servers | Microsoft Defender for Endpoint Plan 2 |
| Query local AI agents in advanced hunting, including the `AgentsInfo` table | Microsoft Defender for Endpoint Plan 2 |
| View the risk level, risk indicators, and security recommendations for discovered local AI agents | Microsoft 365 E7, or Microsoft Agent 365 together with Microsoft Defender for Endpoint Plan 2 |

Microsoft 365 E5 and Microsoft 365 E7 both include Microsoft Defender for Endpoint Plan 2. If your organization has Microsoft Defender for Endpoint Plan 2 without Microsoft 365 E7 or Microsoft Agent 365, you can discover local AI agents, view the inventory, and query agents in advanced hunting, but the risk level, risk indicators, and security recommendations aren't available.

## View local AI agents in the inventory

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com/).
2. In the left navigation pane, select **Assets** &gt; **AI agents**.
3. Select the **Local agents** tab to see the local AI agents discovered on your devices.

    [![Screenshot showing the local AI agents inventory in the Microsoft Defender portal with discovered agents listed.](media/local-agent-discovery-overview/discovery-overview.png)](media/local-agent-discovery-overview/discovery-overview.png#lightbox)

The **Agents insights** cards summarize the total number of monitored agents, the number of agents at a high risk level, and the number of critical agents.

The list shows one entry for each agent installation, so an agent that runs on several devices, or under several accounts on the same device, appears more than once. Use the filters to narrow the list, select **Customize columns** to change which columns appear, or select **Export** to download the list.

| Column | Description |
| --- | --- |
| **Agent name**, **Version** | The discovered agent, and the version installed. |
| **Device name**, **Device ID**, **OS platform**, **Device type** | The device where the agent was discovered. |
| **Account name**, **Account domain** | The account that the agent runs under. |
| **Risk level** | The overall risk level of the agent. |
| **Risk indicators** | Why the agent is considered risky, such as **Running on a Critical Device** or **Used by a Critical User**. |
| **Recommendations** | The security recommendations that apply to the agent. |
| **MCP servers**, **Local MCPs** | The number of remote MCP servers, and of local MCP servers, configured for the agent. |
| **First seen** | When the agent was first discovered. |

Note

Risk levels, risk indicators, and security recommendations require Microsoft 365 E7 or Microsoft Agent 365. Without one of these licenses, you can still view the inventory and the details of each agent. For more information, see Licensing.

### View the details of a local AI agent

From the **Local agents** list, select an agent to open its details pane:

- **Details** shows the agent name, vendor, model, related process, whether the host process is trusted, whether the agent automatically approves its own actions, and the source agent ID.
- **Risk** shows the risk level, the risk indicators, and the security recommendations that apply to the agent.
- **Device details** shows the device where the agent was discovered, including the OS platform and version, the device type and roles, and the Microsoft Entra device ID.
- **User details** shows the ID, name, and domain of the account that the agent runs under.
- **MCP servers** lists the MCP servers configured for the agent, with the name, type, and endpoint of each server.
- **Local MCP servers** lists the local MCP entries discovered on the device.

To investigate further, select **Go hunt** to query the agent in advanced hunting, **View on map** to see the agent in the attack surface map, or **Open Agent page** to open the full agent page.

### Review an agent's attack surface and recommendations

The agent page has an **Overview** tab and a **Security recommendations** tab. The **Attack surface** map on the **Overview** tab shows the other agents, devices, identities, and resources associated with the agent.

For more information on using the AI agent inventory, see [Discover AI agents and assess security posture using Microsoft Defender](/en-us/defender-xdr/security-for-ai/ai-agent-inventory).

## Query local AI agents using advanced hunting

Use advanced hunting to proactively investigate local AI agent presence, understand how agents are configured, and identify the agents and users that carry the most risk. These queries help you inventory agents, review the MCP servers they connect to, and trace access to critical or sensitive assets.

### Understand the tables

Three advanced hunting tables describe local AI agents. Each answers a different question, and they're most useful together.

| Table | What it contains | Use it to answer |
| --- | --- | --- |
| [AgentsInfo](/en-us/defender-xdr/advanced-hunting-agentsinfo-table) | A profile record for every AI agent that Microsoft Defender discovers on all agent platforms. For local AI agents, the record includes the publisher, version, host process, trust and auto-approve settings, configured MCP servers, and the device and account where the agent was seen. | What is this agent, and how is it configured? |
| [ExposureGraphNodes](/en-us/defender-xdr/advanced-hunting-exposuregraphnodes-table) | Every entity in your organization as a node, including AI agents, devices, identities, and cloud resources, along with properties such as asset criticality and whether the entity holds sensitive data. | What is this entity, and how much does it matter? |
| [ExposureGraphEdges](/en-us/defender-xdr/advanced-hunting-exposuregraphedges-table) | The relationships between nodes, such as the device an agent runs on, or the resources an identity can access. | What can this agent reach? |

In short, `AgentsInfo` describes what an agent *is*, and the exposure graph describes what an agent can *reach*.

Both data sources contain agents from every platform, including cloud agents, so each one needs its own filter.

In `AgentsInfo`, filter on the `Platform` column:

```kusto
AgentsInfo
| where Platform == "LocalAgents"
```

In `ExposureGraphNodes`, AI agents use the `ai-agent` node label. Filter on the platform reported in the node properties:

```kusto
ExposureGraphNodes
| where NodeLabel == "ai-agent"
| where tostring(NodeProperties.rawData.aiAgentMetadata.platform) == "LocalAgents"
```

Important

The `ExposureGraphEdges` table doesn't include a property that identifies local AI agents. Filtering only on `SourceNodeLabel == "ai-agent"` returns edges for every AI agent in your tenant, including cloud agents. Always resolve the local agent set from `ExposureGraphNodes` first, and then join to `ExposureGraphEdges` on the node ID, as shown in the following queries.

### Combine the tables

An agent has two identifiers, and queries that combine the tables need both:

- `AgentId` identifies the agent profile in `AgentsInfo`. The exposure graph stores the same value in the agent node, as `NodeProperties.rawData.aiAgentMetadata.id`.
- `NodeId` identifies the agent's node in the exposure graph. This is the value that `ExposureGraphEdges` refers to, in `SourceNodeId` and `TargetNodeId`.

| To go from | To | Match on |
| --- | --- | --- |
| `AgentsInfo` | `ExposureGraphNodes` | `tostring(AgentId)` and `tostring(NodeProperties.rawData.aiAgentMetadata.id)` |
| `ExposureGraphNodes` | `ExposureGraphEdges` | `NodeId` and `SourceNodeId` or `TargetNodeId` |

Note

`AgentId` is a `guid` column in `AgentsInfo`, but the exposure graph stores the same value as a string. Convert it with `tostring()` on both sides of the join. A join between columns of different types doesn't match any rows.

Local AI agent nodes connect to the rest of the exposure graph through the following edges:

| Edge label | Target node label | Description |
| --- | --- | --- |
| `runs on` | `device`, `ec2.instance`, `microsoft.compute/virtualmachines` | The device where the agent was discovered. |
| `uses` | `mcp/server` | An MCP server that's configured for the agent. |
| `used by` | `user` | The identity that uses the agent. |

Cloud AI agents also use a `can authenticate as` edge that points to a service principal or a Microsoft Entra OAuth app. Local AI agents don't use that edge, so use `used by` to resolve the identity behind a local AI agent.

Asset criticality is stored in `ExposureGraphNodes`, in `NodeProperties.rawData.criticalityLevel.criticalityLevel`, where `0` is the highest level (very high) and `3` is the lowest (low). The `ruleNames` property lists the classification rules that made the asset critical.

### Work with local AI agent profiles

`AgentsInfo` adds a record each time an agent profile is updated, so a single agent usually has several records. To return only the most recent record for each agent, summarize with `arg_max` on `Timestamp`:

```kusto
AgentsInfo
| where Platform == "LocalAgents"
| summarize arg_max(Timestamp, Name, Version, LifecycleStatus, RawAgentInfo) by AgentId
```

`LifecycleStatus` reports whether the agent is still present on the device. An agent that's reinstalled can also be reissued with a new `AgentId`, which leaves the earlier record marked as `Deleted`, so filter out `Deleted` and `Uninstalled` records when you want a current inventory.

Many `AgentsInfo` columns describe cloud agents and are empty for local AI agents. The columns that carry local AI agent data are `AgentId`, `Name`, `Version`, `PublishedStatus`, `LifecycleStatus`, `LastUpdatedDateTime`, `McpServers`, `DeclaredTools`, and `RawAgentInfo`.

Local AI agent posture is nested in the `RawAgentInfo` column, under `localAgentMetadata`:

| Property | Description |
| --- | --- |
| `vendor` | The publisher of the agent, such as Anthropic, Google, or OpenAI. |
| `relatedProcess` | The process that hosts the agent, such as `code.exe`. |
| `trustedProcess` | Whether the host process is trusted. Reported as the string `"true"` or `"false"`. |
| `autoApprove` | Whether the agent acts without prompting the user for approval. Reported as the string `"true"` or `"false"`. |
| `deviceName`, `aadDeviceId` | The device where the agent was discovered. |
| `accountName`, `accountDomain`, `accountSid` | The account that the agent ran under. |
| `localMcps` | MCP servers that run locally on the device, including the command that starts each one. |

Note

`trustedProcess` and `autoApprove` are reported as strings, not as boolean values. Compare them to `"true"` or `"false"` rather than using `tobool()`.

Each of the following queries is self-contained. The queries that use the exposure graph start with a set of `let` statements that resolve local AI agents and the devices they run on.

### Get an inventory of local AI agents

This query lists the local AI agents discovered in your organization, together with the publisher, the host process, the versions in use, and how widely each agent is deployed:

```kusto
AgentsInfo
| where Platform == "LocalAgents"
| summarize arg_max(Timestamp, Name, Version, LifecycleStatus, RawAgentInfo)
    by AgentId
| where LifecycleStatus !in~ ("Deleted", "Uninstalled")
| extend AgentMetadata = RawAgentInfo.localAgentMetadata
| extend Vendor = tostring(AgentMetadata.vendor),
         Process = tostring(AgentMetadata.relatedProcess),
         Device = tostring(AgentMetadata.deviceName),
         Account = tostring(AgentMetadata.accountName)
| summarize Installations = count(),
            DeviceCount = dcount(Device),
            Devices = make_set(Device, 100),
            Versions = make_set(Version, 20),
            Accounts = make_set_if(Account, isnotempty(Account), 50)
    by Agent = Name, Vendor, Process
| sort by DeviceCount desc, Installations desc
```

Each `AgentId` represents one agent profile, which is a single agent on a single device for a single account. `Installations` counts those profiles, so an agent that two people use on the same device counts twice, while `DeviceCount` counts the device once.

Compare the `Name` and `Vendor` values returned by the query with the [AI agent discovery support matrix](ai-agent-support-matrix#ai-agent-discovery-support).

### Review the MCP servers and tools that local AI agents use

This query lists the MCP servers and tools configured for local AI agents, the agents and devices that use them, and where each one runs:

```kusto
let localAgentProfiles =
    AgentsInfo
    | where Platform == "LocalAgents"
    | extend AgentMetadata = RawAgentInfo.localAgentMetadata
    | project Timestamp,
              Agent = Name,
              Device = tostring(AgentMetadata.deviceName),
              Account = tostring(AgentMetadata.accountName),
              McpServers,
              DeclaredTools,
              LocalServers = AgentMetadata.localMcps;
let remoteMcpServers =
    localAgentProfiles
    | mv-expand Server = McpServers
    | project Timestamp, Agent, Device, Account,
              McpServer = tostring(Server.name),
              Origin = "Remote MCP server",
              Transport = tostring(Server.type),
              Location = tostring(Server.endpoint);
let agentDeclaredTools =
    localAgentProfiles
    | mv-expand Tool = DeclaredTools
    | project Timestamp, Agent, Device, Account,
              McpServer = tostring(Tool.name),
              Origin = "Declared tool",
              Transport = tostring(Tool.type),
              Location = tostring(Tool.endpoint);
let localMcpServers =
    localAgentProfiles
    | mv-expand Server = LocalServers
    | project Timestamp, Agent, Device, Account,
              McpServer = tostring(Server.name),
              Origin = "Local MCP server",
              Transport = tostring(Server.transportType),
              Location = tostring(Server.commandName);
remoteMcpServers
| union agentDeclaredTools, localMcpServers
| where isnotempty(McpServer)
| summarize LastSeen = max(Timestamp),
            Agents = make_set(Agent, 20),
            Devices = make_set(Device, 20),
            Accounts = make_set_if(Account, isnotempty(Account), 20)
    by McpServer, Origin, Transport, Location
| sort by McpServer asc, Origin asc
```

The `Origin` column distinguishes the three ways a server or tool is reported:

- A **remote MCP server** is reached over the network, and `Location` holds its endpoint.
- A **local MCP server** runs as a process on the device, and `Location` holds the command that starts it. Local MCP servers are reported only in `AgentsInfo`.
- A **declared tool** is a tool the agent advertises. Declared tools are often backed by an MCP server, but they don't always report an endpoint.

Unlike the other queries, this one reads every profile record for each agent, so that MCP servers reported at any point are included. The `LastSeen` column shows when each server was last reported.

### Find local AI agents with risky configurations

This query returns local AI agents that act without asking the user for approval, or that run in a host process that isn't trusted:

```kusto
AgentsInfo
| where Platform == "LocalAgents"
| summarize arg_max(Timestamp, Name, Version, LifecycleStatus, RawAgentInfo)
    by AgentId
| where LifecycleStatus !in~ ("Deleted", "Uninstalled")
| extend AgentMetadata = RawAgentInfo.localAgentMetadata
| extend AutoApprove = tostring(AgentMetadata.autoApprove),
         TrustedProcess = tostring(AgentMetadata.trustedProcess),
         Vendor = tostring(AgentMetadata.vendor),
         Process = tostring(AgentMetadata.relatedProcess),
         Device = tostring(AgentMetadata.deviceName),
         Account = tostring(AgentMetadata.accountName)
| where AutoApprove =~ "true" or TrustedProcess =~ "false"
| extend RiskReason = case(
    AutoApprove =~ "true" and TrustedProcess =~ "false",
        "Acts without approval, and the host process isn't trusted",
    AutoApprove =~ "true",
        "Acts without approval",
    "The host process isn't trusted")
| project Agent = Name, Vendor, Version, Process, Device, Account,
          AutoApprove, TrustedProcess, RiskReason, LastSeen = Timestamp
| sort by Device asc, Agent asc
```

An agent that auto-approves its own actions runs tools and reaches resources without a person confirming each step, so the account and device that the agent runs on define what it can do unsupervised.

### Find risky local AI agents on critical devices

This query combines agent configuration from `AgentsInfo` with asset criticality from the exposure graph, so you can start with the agents that both act unsupervised and run on business-critical devices:

```kusto
let deviceLabels = dynamic(["device", "ec2.instance",
                            "microsoft.compute/virtualmachines"]);
let riskyAgentProfiles =
    AgentsInfo
    | where Platform == "LocalAgents"
    | summarize arg_max(Timestamp, Name, Version, LifecycleStatus, RawAgentInfo)
        by AgentId
    | where LifecycleStatus !in~ ("Deleted", "Uninstalled")
    | extend AgentMetadata = RawAgentInfo.localAgentMetadata
    | extend AutoApprove = tostring(AgentMetadata.autoApprove),
             TrustedProcess = tostring(AgentMetadata.trustedProcess)
    | where AutoApprove =~ "true" or TrustedProcess =~ "false"
    | project AgentId = tostring(AgentId),
              Agent = Name,
              Version,
              Vendor = tostring(AgentMetadata.vendor),
              Account = tostring(AgentMetadata.accountName),
              AutoApprove,
              TrustedProcess;
let localAgentNodes =
    ExposureGraphNodes
    | where NodeLabel == "ai-agent"
    | where tostring(NodeProperties.rawData.aiAgentMetadata.platform) == "LocalAgents"
    | project AgentNodeId = NodeId,
              AgentId = tostring(NodeProperties.rawData.aiAgentMetadata.id);
let agentDeviceEdges =
    ExposureGraphEdges
    | where SourceNodeLabel == "ai-agent"
    | where EdgeLabel =~ "runs on"
    | where TargetNodeLabel in (deviceLabels)
    | project AgentNodeId = SourceNodeId, DeviceId = TargetNodeId,
              Device = TargetNodeName, DeviceType = TargetNodeLabel;
let criticalDevices =
    ExposureGraphNodes
    | where NodeLabel in (deviceLabels)
    | where NodeProperties has "criticalityLevel"
    | extend CriticalityLevel =
        toint(NodeProperties.rawData.criticalityLevel.criticalityLevel)
    | where CriticalityLevel between (0 .. 3)
    | extend Criticality = case(
        CriticalityLevel == 0, "Very high",
        CriticalityLevel == 1, "High",
        CriticalityLevel == 2, "Medium",
        "Low")
    | project DeviceId = NodeId, CriticalityLevel, Criticality,
              CriticalityReason =
                  tostring(NodeProperties.rawData.criticalityLevel.ruleNames);
riskyAgentProfiles
| join kind=inner localAgentNodes on AgentId
| join kind=inner agentDeviceEdges on AgentNodeId
| join kind=inner criticalDevices on DeviceId
| project Device, DeviceType, Criticality, CriticalityReason,
          Agent, Vendor, Version, Account, AutoApprove, TrustedProcess,
          CriticalityLevel
| sort by CriticalityLevel asc, Device asc, Agent asc
| project-away CriticalityLevel
```

To review every local AI agent on a critical device instead of only the risky ones, remove the `where AutoApprove =~ "true" or TrustedProcess =~ "false"` line.

### Rank the users whose local AI agents reach critical or sensitive assets

This query ranks the identities that use local AI agents by how many critical or sensitive resources they can reach, so you can prioritize the users with the widest blast radius. The `UserCriticality` column shows whether the identity is itself classified as a critical asset, such as a Global Administrator:

```kusto
let deviceLabels = dynamic(["device", "ec2.instance",
                            "microsoft.compute/virtualmachines"]);
let localAgents =
    ExposureGraphNodes
    | where NodeLabel == "ai-agent"
    | where tostring(NodeProperties.rawData.aiAgentMetadata.platform) == "LocalAgents"
    | project AgentNodeId = NodeId, AIAgent = NodeName;
let agentDeviceEdges =
    ExposureGraphEdges
    | where SourceNodeLabel == "ai-agent"
    | where EdgeLabel =~ "runs on"
    | where TargetNodeLabel in (deviceLabels)
    | project AgentNodeId = SourceNodeId, DeviceId = TargetNodeId,
              Device = TargetNodeName;
let agentUserEdges =
    ExposureGraphEdges
    | where SourceNodeLabel == "ai-agent"
    | where EdgeLabel =~ "used by"
    | project AgentNodeId = SourceNodeId, UserId = TargetNodeId,
              User = TargetNodeName;
let userReach =
    ExposureGraphEdges
    | where EdgeLabel in~ ("has permissions to", "has role on")
    | project UserId = SourceNodeId, AssetId = TargetNodeId
    | union (
        ExposureGraphNodes
        | where NodeLabel == "user"
        | project UserId = NodeId, AssetId = NodeId
    );
let sensitiveAssets =
    ExposureGraphNodes
    | where NodeProperties has "criticalityLevel"
         or NodeProperties has "containsSensitiveData"
    | extend
        CriticalityLevel =
            toint(NodeProperties.rawData.criticalityLevel.criticalityLevel),
        SensitiveDataRaw = tostring(NodeProperties.rawData.containsSensitiveData)
    | extend HasSensitiveData =
        iff(isnotempty(SensitiveDataRaw) and SensitiveDataRaw !~ "false", "Yes", "No")
    | where CriticalityLevel between (0 .. 3) or HasSensitiveData == "Yes"
    | extend CriticalityRank =
        iff(CriticalityLevel between (0 .. 3), CriticalityLevel, 4)
    | project AssetId = NodeId, AssetName = NodeName,
              CriticalityRank, HasSensitiveData;
let agentUsers =
    localAgents
    | join kind=inner agentDeviceEdges on AgentNodeId
    | join kind=inner agentUserEdges on AgentNodeId
    | project AIAgent, Device, UserId, User;
agentUsers
| join kind=inner userReach on UserId
| join kind=inner sensitiveAssets on AssetId
| summarize AIAgents = make_set(AIAgent, 20),
            Devices = make_set(Device, 20),
            ReachableAssets = dcountif(AssetId, AssetId != UserId),
            SensitiveAssets = dcountif(AssetId,
                AssetId != UserId and HasSensitiveData == "Yes"),
            Assets = make_set_if(AssetName, AssetId != UserId, 50),
            UserRank = minif(CriticalityRank, AssetId == UserId),
            AssetRank = minif(CriticalityRank, AssetId != UserId)
    by User
| extend UserCriticality = case(
             UserRank == 0, "Very high",
             UserRank == 1, "High",
             UserRank == 2, "Medium",
             UserRank == 3, "Low",
             "Not classified"),
         HighestAssetCriticality = case(
             AssetRank == 0, "Very high",
             AssetRank == 1, "High",
             AssetRank == 2, "Medium",
             AssetRank == 3, "Low",
             AssetRank == 4, "Sensitive data",
             "None")
| extend SortRank = coalesce(AssetRank, 99)
| project User, UserCriticality, ReachableAssets, SensitiveAssets,
          HighestAssetCriticality, AIAgents, Devices, Assets, SortRank
| sort by SortRank asc, ReachableAssets desc
| project-away SortRank
```