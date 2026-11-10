---
layout: Conceptual
title: Enable security for AI agents using Microsoft Defender - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/security-for-ai/get-started-defender-security-for-ai
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
ms.author: guywild
author: guywi-ms
ms.reviewer: itaicohen
ms.service: microsoft-defender
ms.date: 2026-10-30T00:00:00.0000000Z
audience: Admin
ms.topic: how-to
ai-usage: ai-assisted
description: Enable Microsoft Defender security for AI agents by configuring data sources, connecting Microsoft 365, and onboarding Copilot Studio.
locale: en-us
document_id: 9e82fe72-f8ae-3029-2752-dbadca27cbd5
document_version_independent_id: 9e82fe72-f8ae-3029-2752-dbadca27cbd5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/security-for-ai/get-started-defender-security-for-ai.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-for-ai/get-started-defender-security-for-ai
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/security-for-ai/get-started-defender-security-for-ai.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/302444b9-4a43-4841-8014-3d9e4251ff15
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c389ea6b-b6a0-46df-93a1-1e21f25e19e7
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/bebd8809-dac1-4c22-83e2-66d98af8a94d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19ada1b6-705b-4ed7-aad0-bffd1bd03dfa
platformId: 24cbe069-0c09-da8f-26ec-c530caa9c339
---

# Enable security for AI agents using Microsoft Defender - Microsoft Defender XDR | Microsoft Learn

Microsoft Defender integrates with [Microsoft Agent 365](/en-us/microsoft-agent-365/overview) to secure the AI agents in your organization. After you onboard to Agent 365, enable security for AI agents to discover, protect, and respond to threats targeting agents in your tenant. For an overview of the agent security capabilities, see [Protect AI agents using Microsoft Defender](defender-security-for-ai#protect-ai-agents-using-microsoft-defender).

Onboarding includes enabling data collection, connecting the Microsoft 365 app connector, and onboarding Copilot Studio for real-time protection.

## Prerequisites

Local agents are onboarded separately from cloud agents. For local AI agent discovery, meet the [discovery prerequisites](/en-us/defender-endpoint/discover-local-ai-agents#prerequisites). Discovery doesn't require you to enable AI agent runtime protection. To configure runtime protection separately, see [Set up AI agent runtime protection](/en-us/defender-endpoint/configure-ai-agent-runtime-protection).

Before you onboard cloud agents, make sure you have:

- [Onboard to Microsoft Agent 365](/en-us/microsoft-agent-365/overview).
- Security Administrator role or higher in Microsoft Entra ID.
- For Copilot Studio real-time protection, you need collaboration with a Power Platform administrator.

## Connect data sources

To configure the data sources that Microsoft Defender uses to surface, investigate, and protect AI agents in your tenant:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Go to **Settings** &gt; **Security for AI** &gt; **Get started**.

    When you onboard to Agent 365, security for AI agents is enabled automatically, including AI agent discovery, security posture assessment, and threat detection. The **Enable** toggle is on by default. To stop collecting data for AI agents, switch it to **Off**.

    A setup checklist shows the status of required and optional data sources. **Agent 365** provides unified visibility into AI agents and is marked as **Done** automatically.
3. Enable the Microsoft 365 connector to get [investigation and advanced hunting capabilities](ai-agent-detection-protection) for AI agent activity:

    1. In the **Get started** page, select the **Microsoft 365 connector** step.
    2. On the **Select Microsoft 365 components** step, select at least the two components required for AI agent monitoring:

        - **Microsoft Entra ID Management events**: audit admin activities performed in Microsoft Entra ID.
        - **Microsoft 365 activities**: audit activities performed by users in your Microsoft 365 apps.

        **Microsoft Entra Users and groups** is a prerequisite for all monitoring capabilities and is selected by default.
    3. Select **Connect Microsoft 365** to complete the connector setup.

    When the connector is active, its status shows as **Connected**.

    Note

    For Copilot Studio agents, if the Microsoft 365 connector isn't connected, alerts and incidents related to these actions don't appear in the Microsoft Defender portal.