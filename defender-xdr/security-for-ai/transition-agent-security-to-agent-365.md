---
layout: Conceptual
title: Transition Microsoft Copilot Studio and Microsoft Foundry agent security capabilities to Microsoft Agent 365 - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/security-for-ai/transition-agent-security-to-agent-365
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn what actions to take as AI agent security capabilities in Microsoft Defender for Cloud Apps and Microsoft Defender for Cloud transition to a Microsoft Agent 365 license on July 1, 2026.
ms.author: guywild
author: guywi-ms
ms.reviewer: gayasalomon
ms.service: microsoft-defender
ms.date: 2026-06-02T00:00:00.0000000Z
audience: Admin
ms.topic: concept-article
ai-usage: ai-assisted
locale: en-us
document_id: 06245857-3075-715d-8726-c0a2d783b4b9
document_version_independent_id: 06245857-3075-715d-8726-c0a2d783b4b9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/security-for-ai/transition-agent-security-to-agent-365.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-for-ai/transition-agent-security-to-agent-365
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/security-for-ai/transition-agent-security-to-agent-365.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/302444b9-4a43-4841-8014-3d9e4251ff15
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/bebd8809-dac1-4c22-83e2-66d98af8a94d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
platformId: b751d333-6346-974b-9b43-18d63e43b625
---

# Transition Microsoft Copilot Studio and Microsoft Foundry agent security capabilities to Microsoft Agent 365 - Microsoft Defender XDR | Microsoft Learn

Effective July 1, 2026, AI agent security capabilities for Microsoft Copilot Studio and Microsoft Foundry agents require a Microsoft Agent 365 license. These capabilities are no longer covered by existing Defender for Cloud Apps or Defender for Cloud licenses. Tenants without an Agent 365-eligible license lose access to these capabilities on July 1, 2026.

Once you onboard to Agent 365, these experiences remain in the Microsoft Defender portal — powered by Agent 365 observability logs and the agent registry as the single source of truth for agent inventory, real-time threat protection, and consistent posture across your environment.

The following sections list the capabilities that require an Agent 365 license, describe how the experience changes after you transition, and provide step-by-step actions to prepare your environment before July 1, 2026.

## Capabilities that require a Microsoft Agent 365 license as of July 1, 2026

These capabilities, currently through Microsoft Defender for Cloud Apps and Microsoft Defender for Cloud, will be fully disabled for tenants without an Agent 365-eligible license starting July 1, 2026:

- **Microsoft Copilot Studio agents** — previously supported through Microsoft Defender for Cloud Apps:

    - Agent discovery and posture
    - Agent threat detection and real-time protection
    - Investigation of agent activity in Advanced Hunting, powered by Agent 365 observability logs
- **Microsoft Foundry agents** — previously supported through Microsoft Defender for Cloud:

    - Discovery and security posture for cloud-hosted agents, including multi-cloud (previously available with the Defender Cloud Security Posture Management plan)
    - Threat protection for agents (previously available with the Defender for AI Services plan)

    Note

    Defender Cloud Security Posture Management (CSPM) continues to discover Microsoft Foundry accounts and projects, but agent-level discovery, posture, and threat detection require an Agent 365 license.

## How does the experience change when you transition to Microsoft Agent 365?

#### Advanced Hunting

The AI agent inventory in Advanced Hunting is moving from the `AIAgentsInfo` table to a new `AgentsInfo` table, powered by Microsoft Agent 365 as the single source of truth for AI agent inventory. The `AIAgentsInfo` table will be deprecated. The `AgentsInfo` schema will be published on Microsoft Learn, and Microsoft-published community queries will be updated to use the new table.

#### Threat detection alerts

- **Copilot Studio agents**: Existing threat detection alerts in Defender for Cloud Apps will be deprecated. Equivalent alerts will run over Microsoft Agent 365 observability logs after July 1, 2026, and will remain available through the Defender portal for licensed tenants.
- **Foundry agents**: Existing agent-specific alerts in Defender for AI Services plan will be deprecated. Equivalent alerts will run over Agent 365 observability logs. The Defender for AI Services plan continues to support Foundry Models such as Azure OpenAI.

#### Real-time protection

- **Agent 365 real-time protection**: Alerts generated by legacy real-time protection rules (in both audit and block modes) will be replaced by equivalent Advanced Hunting [behaviors](../advanced-hunting-behaviorinfo-table). Behaviors record these events as queryable telemetry in the `BehaviorInfo` table, so you can build custom detections, hunting queries, and downstream automation. Near-real-time detection alerts remain unchanged.
- **Copilot Studio (through Defender for Cloud Apps)**: Real-time protection for Microsoft Copilot Studio through Defender for Cloud Apps remains unchanged for tenants that continue using this experience. No action is required.

Important

Tenants currently configured to **Block** on existing Agent 365 rules will stop blocking on July 1, 2026. To resume blocking, define rules under the new real-time protection policy experience, available under **Settings** &gt; **Security for AI** &gt; **Policies & rules** &gt; **Real-time protection** starting July 1, 2026.

#### Third-party cloud agents (previously through Defender for Cloud)

Third-party cloud agents will no longer be discoverable through Microsoft Defender for Cloud connectors. To continue discovering third-party cloud agents, see [Registry sync in the Microsoft 365 agent registry (preview)](/en-us/microsoft-agent-365/admin/agent-registry).

#### Microsoft Defender portal changes

For tenants with a Microsoft Agent 365-eligible license, the following experiences remain available in the Microsoft Defender portal:

- AI Agents inventory and asset pages
- AI Agents recommendations (Foundry agents)
- `AIAgentsInfo` table in Advanced Hunting (until migrated to `AgentsInfo`)
- Security for AI settings page

The **AI Agents** sub-tab under **Cloud Assets** will be removed for all customers.

For tenants without an eligible license, these experiences will be replaced with guidance on the license required.

#### Azure portal changes (Foundry agents)

Microsoft Foundry agent data will no longer appear in the following Azure portal experiences:

- Data and AI dashboard
- Cloud Security Explorer

## What you need to do to prepare

Note

Some steps (such as redefining policies) are available starting July 1, 2026.

1. **Confirm your tenant has an Agent 365-eligible license** - Review your current licensing against the eligibility and prerequisites described in [Microsoft Agent 365 overview](/en-us/microsoft-agent-365/overview). Tenants without an eligible license lose agent security capabilities at cutover on July 1, 2026.
2. **If you aren't yet licensed, start an Agent 365 trial** - Agent 365 admin-led trials are available for 25 seats for 30 days. The Microsoft Admin Center displays a banner with remaining trial days. Admins with billing permissions can view trial details and purchase the license directly from the banner. For enterprise customers, contact your Microsoft account team.
3. **Confirm your Defender enablement settings** - On July 1, 2026, all Security for AI capabilities consolidate under a single **Security for AI Agents** toggle in Defender settings. Confirm the toggle is **On** and review the consolidated configuration. When the toggle is off, all Security for AI capabilities are disabled.
4. **Update Advanced Hunting queries** - Review saved queries, custom detections, and workbooks that reference the `AIAgentsInfo` table and update them to the new `AgentsInfo` table before July 1, 2026.
5. **If you already use Agent 365, redefine real-time protection blocking rules** - The existing Agent 365 real-time protection settings are moving to a new **Policies** experience. Any rules currently set to **Block** stop enforcing on July 1, 2026. Redefine them under **Settings** &gt; **Security for AI** &gt; **Policies & rules** &gt; **Real-time protection** (available July 1, 2026) to preserve blocking. This applies only to Agent 365 real-time protection — Copilot Studio real-time protection through Defender for Cloud Apps is unchanged.
6. **Connect third-party cloud agents using the Agent 365 registry sync (previously through Defender for Cloud)** - Configure [registry sync in the Microsoft 365 agent registry (preview)](/en-us/microsoft-agent-365/admin/agent-registry) to continue discovering third-party cloud agents previously discovered using Microsoft Defender for Cloud connectors.
7. **Migrate alert workflows** - Move any monitoring or response workflows that consume legacy alerts to their replacements by July 1, 2026:

    - Real-time protection rule alerts (audit and block modes) move to the `BehaviorInfo` table in Advanced Hunting. Build custom detections, hunting queries, and downstream automation against [behaviors](../advanced-hunting-behaviorinfo-table) in place of the legacy alerts.
    - Threat detection alerts move to Microsoft Agent 365 observability logs (auto-enabled upon license provisioning).
8. **Communicate the change to your stakeholders** - Inform security operations, IT, and compliance stakeholders — especially anyone who depends on real-time protection blocking, detection alerts, or Foundry agent visibility — about which Defender experiences will move, change, or be removed on July 1, 2026.