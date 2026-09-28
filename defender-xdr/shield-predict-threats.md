---
layout: Conceptual
title: Predictive shielding in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/shield-predict-threats
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Predictive shielding dynamically infers risk, anticipates attacker progression, and hardens your environment.
ms.service: defender-xdr
ms.author: monaberdugo
author: mberdugo
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- usx-security
- usx-security
ms.topic: concept-article
ms.date: 2025-11-04T00:00:00.0000000Z
locale: en-us
document_id: b4eb1046-f5e4-4a6f-b464-14e9bd89c96e
document_version_independent_id: b4eb1046-f5e4-4a6f-b464-14e9bd89c96e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/shield-predict-threats.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: shield-predict-threats
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/shield-predict-threats.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: c6784dd6-39ed-6958-98af-cdecba92e3a8
---

# Predictive shielding in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

Predictive shielding (Preview) is a proactive defense strategy designed to anticipate and mitigate threats as part of an ongoing attack. Predictive shielding expands the Microsoft Defender autonomous protection stack, enhancing automatic attack disruption capabilities with proactive measures.

This article provides an overview of predictive shielding so that you can understand its capabilities and how it enhances your security posture.

Learn how predictive shielding works or how to [manage predictive shielding in Microsoft Defender](shield-predict-threats-manage).

## Why predictive shielding matters

In a typical attack, defenders react after malicious activity is detected — but attackers move fast. By the time a compromised device is identified, lateral movement or data exfiltration might already be underway. Predictive shielding shifts the balance by acting during an attack, before the attacker reaches their next target.

**When predictive shielding becomes relevant:**

- An active attack is detected in your environment (for example, a compromised device or credential).
- Defender identifies other assets that are likely targets based on exposure data, attacker behavior patterns, and organizational topology.
- Instead of waiting for the attacker to reach those assets, predictive shielding proactively applies targeted restrictions — such as containing at-risk user accounts, hardening GPO settings, or enforcing Safeboot — to cut off the attack path.

This means security teams gain critical response time. Rather than racing to manually isolate every potentially affected asset, Defender autonomously narrows the attacker's options while analysts investigate.

## How predictive shielding expands on automatic attack disruption

The evolving threat landscape creates an imbalance: defenders must secure every asset, while attackers need only one opening. Traditional defenses are reactive, responding after malicious activity begins. This approach leaves defenders chasing attackers, who often act too quickly or subtly to detect in real time. While some attacker behaviors must be blocked outright, static prevention disrupts productivity and adds operational overhead.

To address these challenges, predictive shielding enhances Defender's autonomous protection stack, expanding [attack disruption](automatic-attack-disruption) to include proactive measures during an attack, anticipating risks and applying targeted protections only where needed.

This proactive approach reduces the reactive chase, minimizes operational burden, maintains usability, and protects the environment before attackers can advance.

While attack disruption identifies and contains compromised assets, predictive shielding anticipates potential attack progression and proactively restricts vulnerable assets or paths. For example, while automatic attack disruption isolates a compromised device, predictive shielding might proactively restrict access to sensitive data for at-risk devices.

Because predictive shielding is part of the same autonomous protection stack, the confidence and AI model principles described for attack disruption also apply to predictive shielding. For more information, see [How Defender establishes confidence for automatic action](automatic-attack-disruption#how-defender-establishes-confidence-for-automatic-action) and [How attack disruption uses AI](automatic-attack-disruption#how-attack-disruption-uses-ai).

## How predictive shielding works

Predictive shielding uses predictive analytics and real-time insights to dynamically identify emerging risks, and applies targeted protections.

Predictive shielding integrates posture, activity, and scenario context to identify potential attack paths and targets, selectively hardening critical assets, or constraining attack paths just in time.

This approach minimizes operational overhead and provides security teams with more time to respond. For example, predictive shielding can dynamically restrict access to sensitive data for devices identified as at-risk, reducing the need for broad, environment-wide restrictions.

Predictive shielding relies on two pillars:

- **Prediction**
    - Involves analyzing threat intelligence, attacker behavior, past incidents, and organizational exposure.
    - Defender uses this prediction data to identify emerging risks, to understand likely attack progression, and to infer risk on noncompromised assets.
- **Enforcement** applies preventative protective controls to disrupt potential attack paths in real time.

This dual approach ensures that protection is both precise and timely.

### Prediction logic

Prediction allows organizations to identify assets at risk and apply tailored protections in real time. Prediction focuses on emerging risks rather than static prevention, which minimizes operational friction and ensures that security measures are applied precisely where needed. For example, if a specific attacker tool is detected, predictive shielding can infer the next likely target based on past attack patterns.

Defender uses multiple layers of insight to make accurate predictions:

- Threat intelligence aligns observed activity with known attacker tools and tactics.
- Learnings from past incidents are used to recognize statistical patterns, and extrapolate the most probable next steps.
- Organizational exposure data is used to map how the environment is structured—which assets and identities are connected, which permissions these identities have, which vulnerabilities or misconfigurations exist, and how risk can propagate across them.

Together, these insights create a dynamic understanding of the environment and its risks.

### Graph-based logic

Graph-based prediction logic bridges the gap between pre-breach and post-breach systems, providing a unified view of attacker activity across the organizational topology. This unified view includes the organization's assets, connections, and vulnerabilities. Graph-based logic combines live activity data with the structural map of the environment.

This integration allows Defender to dynamically adjust protections based on the most critical vulnerabilities, enabling real-time prioritization of defenses and stopping attackers before they reach critical assets.

The process involves three key stages:

1. Defender overlays post-breach activity onto the organization’s exposure graph, creating a comprehensive view of potential attack paths.
2. Defender identifies the blast radius—the related assets that the identified activity might affect.
3. Reasoning models predict paths attackers are most likely to take, factoring in past behaviors, asset characteristics, and environmental vulnerabilities.

This dynamic understanding allows Defender to move beyond reactive responses, enabling just-in-time protection that stops attackers before they reach critical assets.

## Predictive shielding actions

Predictive shielding uses Defender for Endpoint-based actions. To use these actions, you need a Defender for Endpoint license. For a list of actions, see [Automated response actions](automatic-attack-disruption#automated-response-actions).