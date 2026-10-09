---
layout: Conceptual
title: AI agent runtime protection with Microsoft Defender for Endpoint (Preview) - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/ai-agent-runtime-protection-overview
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how Microsoft Defender for Endpoint provides runtime protection for local AI agents by detecting and blocking prompt injection attacks.
author: lwainstein
ms.author: lwainstein
ms.service: defender-endpoint
ms.topic: overview
ms.custom: msecd-doc-authoring-1030
ms.date: 2026-10-08T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 2840101c-b02b-c6b4-ccda-603c72dcf7d6
document_version_independent_id: 2840101c-b02b-c6b4-ccda-603c72dcf7d6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/ai-agent-runtime-protection-overview.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: ai-agent-runtime-protection-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/ai-agent-runtime-protection-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/0850fefd-e402-4507-ae98-46cfdfc2e16c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6ecf98a5-97c7-4249-b209-a9d9e42633a0
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 37e11f67-a65b-b20b-dfef-2569e4ee0cbd
---

# AI agent runtime protection with Microsoft Defender for Endpoint (Preview) - Microsoft Defender for Endpoint | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

Local AI agents, including coding assistants, CLI tools, desktop AI apps, and autonomous agent platforms, run with user privileges on endpoints. These agents act on text from prompts, files, web content, and tool output, and can't reliably separate trusted content from hidden instructions. A single injected instruction can misuse agent access to exfiltrate data, modify code, or run harmful commands.

Microsoft Defender provides AI agent runtime protection by inspecting critical points in the agent loop where content enters or leaves the agent's reasoning. This helps detect malicious prompts and the harmful agent actions they can cause, audit them, and block actions before they run when the inspection method allows it. Defender uses two inspection approaches: agent-native event inspection for agents that expose vendor-supported event interfaces, and network inspection for covered network paths. To learn more about how runtime protection audits and blocks attacks, see What runtime protection detects and How it works.

[![Screenshot showing the blocking notification displayed to the user when Defender detects and blocks a prompt injection attack on a local AI agent.](media/configure-ai-agent-runtime-protection/ai-runtime-agent-block-and-toast.png)](media/configure-ai-agent-runtime-protection/ai-runtime-agent-block-and-toast.png#lightbox)

Learn what runtime protection stops, how it works, and how to investigate detections.

Tip

Runtime protection complements Microsoft Defender's **discovery capabilities**, which inventory local AI agents and their MCP server configurations on your devices. For more information, see [Local AI agent discovery with Microsoft Defender for Endpoint](local-agent-discovery-overview).

Tip

To safely validate runtime protection on a test device, run the [AI agent runtime protection demonstration](defender-endpoint-demonstration-ai-agent-runtime-protection).

## What runtime protection detects

Runtime protection helps protect against attacks involving malicious prompts and the resulting compromise of agent behavior. Defender inspects critical points in the agent loop where content enters or leaves the agent's reasoning and catches attacks regardless of where the content originated, whether a file, a web page, a repository, or a tool's output.

For example, a coding agent fetches a project's documentation to answer a question, and the page contains hidden text that instructs the agent to read the local *.env* file and post its contents to an external URL. The agent treats the instruction as part of the page and is about to comply, but Defender detects the prompt injection in the tool response and blocks the action before any data leaves the device.

## How it works

Runtime protection uses two approaches to inspect agent activity:

### Agent-native event inspection

Agent-native event inspection uses vendor-supported event interfaces exposed by the agent. Agents such as Claude Code, Codex CLI, and GitHub Copilot CLI expose these interfaces, and Defender uses them to inspect agent activity and apply audit or block decisions at critical points in the agent workflow.

Defender scans the available agent activity for malicious prompts and high-risk actions. Depending on the event interfaces that the agent supports, Defender can stop malicious content from continuing through the agent loop or prevent a harmful tool action from running.

Each scan is a fast, inline check rather than continuous monitoring of the agent process, so the added latency is minimal.

### Network inspection

Network inspection extends runtime protection to agents that don't expose agent-native event interfaces. Instead of relying on structured agent events, Defender inspects the agent-to-Large Language Model (LLM) network flows covered by the support matrix to detect prompt injection in transit.

Use network inspection when you want to protect agents that communicate with LLM services over the network but don't expose a vendor-supported event interface. This helps close the coverage gap for agents that would otherwise have no runtime protection before or during interaction with the model.

Note

Network inspection doesn't support agents that use certificate pinning or HTTP/3.

## What happens when you enable runtime protection

Once enabled on a device, Defender inspects agent activity at the available inspection points, without changing how users run the agent. What happens following a detection depends on the configured mode:

- **Block:** Defender blocks the threat and follows the notification rules configured for the device. Defender notifies the user both in the agent UI and through a Windows toast notification. The detection is recorded in Defender protection history on the device, and a security alert is sent to Defender, correlated into incidents for the SOC to investigate.
- **Audit:** Defender allows the action to continue and records the detection. A security alert is still raised in Defender for investigation.
- **Disabled:** Runtime protection is off. Defender doesn't inspect agent activity, and agents run without prompt injection detection or blocking.

Microsoft recommends starting in audit mode to observe detections and validate accuracy before switching to block mode for active enforcement. The runtime protection setting is protected by tamper protection, which prevents unauthorized changes, and works alongside your existing Defender controls.

For local PowerShell and organization-wide Microsoft Intune configuration options, see [Set up AI agent runtime protection with Microsoft Defender for Endpoint](configure-ai-agent-runtime-protection).

## Investigation

When runtime protection detects prompt injection, Defender raises a **Suspicious AI prompt injection** alert and correlates related activity into incidents for investigation.

[![Screenshot showing a Suspicious AI prompt injection alert in Microsoft Defender, including the process tree and related detection details.](media/configure-ai-agent-runtime-protection/runtime-protection-suspicious-prompt-injection-alert.png)](media/configure-ai-agent-runtime-protection/runtime-protection-suspicious-prompt-injection-alert.png#lightbox)

For the full investigation workflow, including user and SOC experiences, see [Review and investigate detections](configure-ai-agent-runtime-protection#review-and-investigate-detections).

## Supported agents

For coverage by agent, mode, inspection method, minimum version, and vendor hooks documentation, see [Microsoft Defender for Endpoint AI agent support matrix](ai-agent-support-matrix).

## Broader AI security capabilities

Defender's runtime protection capabilities are part of a comprehensive AI security approach. Defender provides other capabilities in your organization's AI ecosystem:

- **Discover local AI agents**: Detect local AI agents and their configured MCP servers on your devices after Defender observes agent activity. For more information, see [Local AI agent discovery with Microsoft Defender for Endpoint](local-agent-discovery-overview).
- **Discover cloud and platform agents**: Find agents built with Microsoft Copilot Studio, Microsoft Foundry, Amazon Web Services (AWS) Bedrock, and Google Cloud Platform (GCP) Vertex AI.
- **Assess security posture**: Evaluate agent configurations, identify risks, get prioritized recommendations, and surface attack paths.
- **Detect and investigate threats**: Correlate alerts and investigate suspicious agent behavior in your security infrastructure.

For details on these capabilities and how to apply them, see [Protect AI assets from emerging threats and vulnerabilities using Microsoft Defender](/en-us/defender-xdr/security-for-ai/defender-security-for-ai).