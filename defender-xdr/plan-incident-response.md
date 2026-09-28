---
layout: Conceptual
title: Plan an incident response workflow in the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/plan-incident-response
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Plan an incident response workflow in the Microsoft Defender portal, including triage, investigation, containment, resolution, and post-incident review.
author: guywi-ms
ms.author: guywild
ms.service: defender-xdr
ms.collection:
- m365-security
- tier1
- usx-security
- sentinel-only
ms.custom: admindeeplinkDEFENDER, msecd-doc-authoring-1014
ms.topic: how-to
ms.date: 2026-07-15T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 12c835c6-160e-0468-8c44-152c71fdef34
document_version_independent_id: 12c835c6-160e-0468-8c44-152c71fdef34
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/plan-incident-response.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: plan-incident-response
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/plan-incident-response.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: e74643a8-278f-d620-b9ad-7f55bf58aab8
---

# Plan an incident response workflow in the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn

Note

Incident cases are in preview and are the recommended experience for managing incidents in the Microsoft Defender portal. The legacy incident experience remains available during this preview. This article provides incident response workflow guidance that applies to both incident cases and the legacy incident experience.

In the Microsoft Defender portal, security incidents bring together related alerts and investigation context to help your security operations team understand, manage, and respond to potential attacks.

This article provides workflow guidance for triaging, investigating, containing, resolving, and reviewing incidents. It also maps response activities to responder experience levels and security team roles.

## Incident response workflow example in the Microsoft Defender portal

Here's a workflow example for responding to incidents in the Microsoft Defender portal.

[![An example of an incident response workflow for the Microsoft Defender portal.](media/plan-incident-response/incidents-example-workflow.png)](media/plan-incident-response/incidents-example-workflow.png#lightbox)

On an ongoing basis, identify the highest priority incidents for analysis and resolution and get them ready for response.

You can use [automation rules](siem-defender-create-automation-rules) to automatically triage, manage, or respond to some incidents as they're created.

Consider the following incident response workflow stages and actions for your own process:

| Stage | Actions |
| --- | --- |
| Triage and prioritize the incident. | Review the incident severity, priority, affected assets, related alerts, and available context. Identify incidents that require immediate action, escalation, or continued monitoring. For more information, see [Prioritize incident cases in the Microsoft Defender portal](prioritize-incident-cases). |
| Investigate and analyze the incident. | Review the attack story, alerts, impacted assets, evidence, automated investigations, and related activity to understand the scope, impact, and recommended response actions. For more information, see [Investigate incident cases in the Microsoft Defender portal](investigate-incident-cases). |
| Contain and eradicate the threat. | Take response actions to reduce additional impact and remove the threat. For example, disable compromised users, isolate affected devices, block malicious IP addresses, or approve remediation actions. For more information, see [Automated investigation and response in Microsoft Defender XDR](m365d-autoir). |
| Recover affected resources. | Restore affected users, devices, workloads, or other tenant resources to a trusted state. Validate that the threat is no longer active. |
| Resolve or close the incident. | Document the outcome, classification, determination, response actions, and resolution details. Make sure required tasks and handoffs are complete. For more information, see [Manage incident cases in the Microsoft Defender portal](manage-incident-cases). |
| Review and improve the process. | Review what happened, what actions were taken, and what can be improved. Update workflows, playbooks, policies, automation rules, detections, or security configuration as needed. For more information, see [Incident response playbooks](/en-us/security/operations/incident-response-playbooks). |

For more information about incident response across Microsoft products, see [Incident response overview](/en-us/security/operations/incident-response-overview).

## Plan initial incident management tasks

Use the following guidance to plan initial incident management tasks based on your team's experience level and security operations role.

### Assess responder experience levels

Use the following experience-level guidance for security analysis and incident response.

| Level | Guidance |
| --- | --- |
| **New** | Start with guided workflows and incident prioritization. Review which incidents need attention, assign ownership, document actions, and use the investigation experience to understand alerts, assets, evidence, and recommended response actions. |
| **Experienced** | Use filters, incident context, investigation details, automation results, and related threat intelligence to prioritize response. Manage incident work, investigate affected entities, perform containment and remediation, and document outcomes. |
| **Advanced** | Use advanced hunting, threat analytics, incident response playbooks, and automation to investigate complex incidents, identify related activity, improve detections, and refine response processes. |

### Define tasks by security team role

Use the following role-based guidance for your security team.

| Role | Guidance |
| --- | --- |
| Incident responder (Tier 1) | Triage incidents, identify priority items, assign ownership, update status and severity, add tags and comments, follow standard response procedures, and escalate when needed. |
| Security investigator or analyst (Tier 2) | Investigate incidents, review alerts and evidence, analyze impacted assets, validate automated investigation results, perform containment or remediation actions, and document findings. |
| Advanced security analyst or threat hunter (Tier 3) | Investigate complex or high-impact incidents, use advanced hunting and threat analytics, identify related activity, improve detections, and update incident response playbooks. |
| SOC manager | Define response workflows, ownership models, escalation paths, service-level expectations, and post-incident review processes. Review incident trends and improve operational readiness. |