---
layout: Conceptual
title: Detect and investigate threats to AI agents using Microsoft Defender (Preview) - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/security-for-ai/ai-agent-detection-protection
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to detect, investigate, and hunt for threats to AI agents using Microsoft Defender.
ms.author: guywild
author: guywi-ms
ms.reviewer: itaicohen
ms.service: microsoft-defender
ms.update-cycle: 180-days
ms.date: 2026-08-07T00:00:00.0000000Z
audience: Admin
ms.topic: concept-article
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
locale: en-us
document_id: 6f65dc2c-f042-7dc6-7731-e4ce36d2aeb8
document_version_independent_id: 6f65dc2c-f042-7dc6-7731-e4ce36d2aeb8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/security-for-ai/ai-agent-detection-protection.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-for-ai/ai-agent-detection-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/security-for-ai/ai-agent-detection-protection.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 5332b7a0-9762-bedc-8de5-2a5377272c9f
---

# Detect and investigate threats to AI agents using Microsoft Defender (Preview) - Microsoft Defender XDR | Microsoft Learn

Important

This feature is currently in public preview. The Microsoft Defender preview terms apply to features that are in public preview.

Deployed AI agents operate autonomously, invoking tools, accessing data, and taking actions on connected systems in response to natural‑language input. This makes continuous detection and investigation critical. Microsoft Defender detects suspicious and malicious agent behavior, provides alerts in near‑real‑time, and enables security teams to investigate incidents and trace the full root cause and blast radius.

Microsoft Defender detects and enables security teams to investigate threats to AI agents managed through [Microsoft Agent 365](/en-us/microsoft-agent-365/overview), including the extended detection capabilities available for supported agent platforms. To block unsafe agent actions during runtime, see [Protect AI agents in real time using Microsoft Defender](ai-agent-real-time-protection).

## Prerequisites

- Enable security for AI agents, including the Microsoft 365 app connector to collect Agent 365 observability data for AI agent actions. See [Enable security for AI agents using Microsoft Defender](get-started-defender-security-for-ai).
- Ensure that your AI agent emits observability data to Microsoft 365:

    - Agents built with Microsoft Copilot Studio, Microsoft Foundry, and declarative agents built with the Microsoft Copilot Agent Builder send observability data to Microsoft 365 by default.
    - For AI agents built on other platforms, enable observability using the Microsoft Agent 365 SDK, as described in the [Agent 365 development lifecycle documentation](/en-us/microsoft-agent-365/developer/a365-dev-lifecycle#1-build-and-run-agent). 
        Note

        Threat detection is supported only for published Microsoft Foundry agents. Unpublished agents, including agents used only in a playground environment, aren’t supported. For more information, see [Publish agents to Microsoft Copilot and Microsoft Teams in the Foundry portal](/en-us/azure/foundry/agents/how-to/publish-copilot?tabs=portal)
- To detect threats to local AI agents that run on endpoints, set up [AI agent runtime protection in Microsoft Defender for Endpoint](/en-us/defender-endpoint/configure-ai-agent-runtime-protection). Microsoft Defender for Endpoint must run in active mode. Local agents are onboarded separately from cloud agents.
- *(Optional)* To include the prompt snippets that triggered a detection as evidence in alerts, enable [prompt evidence collection](ai-agent-real-time-protection#control-prompt-evidence-in-alerts). This setting is enabled by default.

## Detect AI agent threats in near-real-time

Microsoft Defender continuously monitors AI agent activity and detects suspicious and malicious behavior for all Agent 365-managed agents. Defender analyzes agent telemetry, tool usage, and execution patterns to identify threats such as *jailbreak attempts*, *indirect prompt injection (XPIA) attempts*, *malicious content propagation*, *secret and credential leakage*, *evasion techniques*, *large language model (LLM) reconnaissance*, and *suspicious user or IP access*.

Microsoft Defender surfaces detections as near‑real‑time alerts in the Defender portal and enables security teams to investigate them using familiar security operations workflows, including alert triage, incident correlation, and Advanced Hunting.

For more information, see [Incidents and alerts in the Microsoft Defender portal](/en-us/defender-xdr/incidents-overview).

Near-real-time detections rely on Agent 365 observability data, which also provides valuable context for investigating incidents and threat hunting. Microsoft Defender analyzes this data to identify suspicious agent behavior and generate alerts.

To enrich alert investigation with the prompt snippets that triggered a detection, enable prompt evidence collection. For more information, see [Control prompt evidence in alerts](ai-agent-real-time-protection#control-prompt-evidence-in-alerts).

## Investigate AI agent threats and hunt for risks using Advanced Hunting

Microsoft Defender correlates AI agent alerts into incidents and surfaces the related context so security teams can quickly assess impact and prioritize response. Advanced Hunting then lets analysts query Agent 365 observability data by using Kusto Query Language (KQL) to investigate incidents and hunt for risks throughout their environment.

### Investigate incidents and alerts

Microsoft Defender correlates AI agent alerts from near‑real‑time detections into incidents. Real‑time protection audit and block events are recorded as behaviors in the `BehaviorInfo` table, which you can correlate with alerts during investigation.

Security analysts can use the incident graph and investigation experience to understand the full context of a potential attack, including relationships between involved entities and the blast radius of AI agent threats. For more information, see [Incidents and alerts in the Microsoft Defender portal](/en-us/defender-xdr/incidents-overview).

Note

Block events from Microsoft Prompt Shields for Foundry and Microsoft Copilot Agent Builder are also recorded as behaviors. This isn't yet supported for agents built with Microsoft Copilot Studio.

### Correlate alerts and Agent 365 observability data and hunt for risks using Advanced Hunting

Advanced Hunting in Microsoft Defender enables security teams to query Agent 365 observability data alongside other security data by using Kusto Query Language (KQL). This supports proactive threat hunting, incident investigation, and root‑cause analysis for agents, applications, identities, and devices.

For example, use Advanced Hunting to:

- Trace specific agent tool invocations and correlate them with related alerts or block events
- Investigate the root cause and scope of a detected AI agent threat
- Identify anomalous execution patterns or risky agent behavior throughout environments
- Build custom detection rules based on agent activity signals

### Advanced Hunting tables for AI agent investigation

The following Advanced Hunting tables provide visibility into [AI agent configuration](ai-agent-inventory#discover-and-assess-ai-agents-using-advanced-hunting), alerts, and activity. You can query these tables individually or correlate them to investigate incidents and hunt for agent-related risks.

| Table name | Description | Common use cases |
| --- | --- | --- |
| [AlertInfo](/en-us/defender-xdr/advanced-hunting-alertinfo-table) | Contains alert metadata generated by Microsoft Defender, including alerts related to near-real-time detections. | Investigate AI agent alerts, understand alert context, and pivot into related incidents and entities. |
| [CloudAppEvents](/en-us/defender-xdr/advanced-hunting-cloudappevents-table) | Contains Agent 365 observability data for AI agent activity, including agent actions, tool invocations, and data access events. | Hunt for suspicious agent behavior, trace agent actions, and perform root-cause analysis using Agent 365 observability data. |
| [AgentsInfo](/en-us/defender-xdr/advanced-hunting-agentsinfo-table) | Contains inventory and configuration details for AI agents, including agent identity, platform, ownership, and metadata. | Review agent posture, identify risky or misconfigured agents, and correlate agent identity with alerts and activity. |
| [AlertEvidence](/en-us/defender-xdr/advanced-hunting-alertevidence-table) | Contains entities and artifacts associated with alerts, such as agents, users, tools, URLs, or resources. | Understand the scope of an alert and identify related entities involved in an AI agent incident. |
| [BehaviorInfo](/en-us/defender-xdr/advanced-hunting-behaviorinfo-table) | Contains behaviors that record real-time protection rule activity, including audit and block events, as queryable telemetry. | Build custom detections, hunting queries, and downstream automation based on real-time protection events. |
| [BehaviorEntities](/en-us/defender-xdr/advanced-hunting-behaviorentities-table) | Contains the entities and artifacts associated with behaviors, such as agents, users, tools, and resources. | Correlate behaviors with related entities to investigate the scope of real-time protection events. |