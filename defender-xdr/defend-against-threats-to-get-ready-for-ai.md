---
layout: Conceptual
title: Defend Against Threats - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/defend-against-threats-to-get-ready-for-ai
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Prepare for AI with Microsoft Defender. Learn five steps to deploy protection, disrupt attacks, respond to incidents, and strengthen your defenses.
author: cjwoodling6
ms.author: cjwoodling6
ms.topic: how-to
ms.service: defender-xdr
ms.date: 2026-10-26T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1028
locale: en-us
document_id: 4e07b2de-2fb4-a0d7-44b3-bcf37396b4aa
document_version_independent_id: 4e07b2de-2fb4-a0d7-44b3-bcf37396b4aa
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/defend-against-threats-to-get-ready-for-ai.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defend-against-threats-to-get-ready-for-ai
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/defend-against-threats-to-get-ready-for-ai.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: d6680523-98d0-291d-be22-d4563fe5d28f
---

# Defend Against Threats - Microsoft Defender XDR | Microsoft Learn

**Security imperative: Get ready for AI** **Job to be done: Defend against threats**

## Context and problem

AI is shrinking the window from intrusion to impact—and expanding the number of targets attackers can pursue at once.

AI is helps attackers find and connect weaknesses organizations already carry: over-permissioned identities, unpatched software, exposed assets, and inadequately protected data. Addressing vulnerabilities in isolation—such as prioritizing software patches alone—no longer delivers the same impact. Nor can a collection of robust controls stop attackers who move across domains. Getting ready for AI requires a connected system that can uncover, understand, and adapt to threats before attackers turn a chain of exposures into a viable attack path.

## Solution

Getting ready for AI requires strengthening how you defend the environment you already have. Unify security signals and workflows, connect the data sources most relevant to your estate, and give defenders one place to investigate incidents, understand activity, automate response, and verify that threats have been contained. This foundation enables AI agents and human defenders to investigate and respond together effectively.

Five sequential steps can get you there: deploy comprehensive protection, set up automatic attack disruption, respond to and contain incidents, prevent recurrence, and continuously optimize protection to reduce exposure. Comprehensive coverage improves detection, automated disruption limits attacker movement, and lessons from each incident help strengthen protection against the next attack.

## Guidance

Security practitioners, including SOC analysts, threat hunters, detection engineers, and incident responders, can strengthen threat defense by following this step-by-step guidance, implemented through Microsoft Defender.

| Step | Recommended action | Resource |
| --- | --- | --- |
| 1. Deploy Defender workloads for comprehensive protection. | Deploy the Defender workloads relevant to your environment for endpoints, identities, email and collaboration, and cloud apps so Microsoft Defender can correlate threat signals and coordinate prevention, detection, investigation, and response for those domains. | [Setup guides for Microsoft Defender](deploy-configure-m365-defender) |
| 2. Set up attack disruption to detect and contain active attacks. | Review the licensing, permissions, and product-specific prerequisites for automatic attack disruption, then deploy and configure the required Defender workloads so compromised assets can be automatically contained during high-confidence attacks. | [Configure automatic attack disruption in Microsoft Defender](configure-attack-disruption) |
| 3. Respond to incidents and validate the threat containment. | Triage and investigate incidents in the Defender portal, contain and eradicate the threat, recover affected resources to a trusted state, and validate that the threat is no longer active before resolving the incident. | [Plan an incident response workflow in the Microsoft Defender portal](plan-incident-response) |
| 4. Hunt for related and recurring activity. | Hunt in Defender data for related or recurring activity, then turn what you learn into custom detections that continuously identify and respond to suspected breach activity and other findings. | [Advanced hunting overview in Microsoft Defender](advanced-hunting-overview) |
| 5. Optimize protection to reduce exposure. | Use SOC optimization recommendations to identify gaps in security coverage and adjust controls and data as threats and business priorities change, helping continuously reduce exposure throughout the environment. | [Optimize security operations](/en-us/azure/sentinel/soc-optimization/soc-optimization-access?tabs=defender-portal) |

## Outcomes

- **Help reduce the risk that exposures become attacks:** connected context reveals how vulnerabilities, identities, permissions, assets, and data create attack paths, helping teams close the gaps that pose the greatest risk before attackers exploit them.
- **Help contain attacks and limit their spread:** shared signals across identity, devices, data, applications, cloud, and code enable coordinated detection and response instead of isolated action from point tools.
- **Use incident learnings to strengthen future defenses:** teams verify that remediation took effect, measure the exposure that remains, and feed lessons from investigations back into protections, priorities, and response workflows.

## Key success factors

To measure progress, consider tracking the following metrics:

- Percentage of identities, devices, applications, workloads, data, and AI systems covered by security policy and protection, with unmanaged or unprotected assets identified
- Percentage of critical assets and sensitive data mapped to their related vulnerabilities, identities, permissions, and attack paths
- Percentage of high-priority exposures assigned to an accountable owner and approved remediation or compensating-control action
- Percentage of high-priority attack paths broken through patching, access reduction, configuration changes, data protection, or other controls
- Percentage of prioritized remediation actions verified as effective, with remaining exposure measured
- Mean time to detect, investigate, contain, and evict active threats across the environment
- Percentage of incidents whose findings result in updated exposure priorities, detections, controls, or automated response workflows

## Summary

Defending against threats to get ready for AI changes the question from how many alerts you can process to how quickly you can detect, contain, and learn from attacks. Deploy Defender workloads across your environment, prepare automatic attack disruption to contain active threats, respond to and fully remediate incidents, hunt for related activity to prevent recurrence, and continually optimize protection to reduce exposure. Together, these steps create a continuous defense cycle that gets stronger as threats and the environment change.

**By connecting threat response with continuous exposure reduction, you strengthen the environment for AI and make each defense improve the next.**