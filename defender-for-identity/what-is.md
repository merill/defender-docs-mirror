---
layout: Conceptual
title: Microsoft Defender for Identity Overview - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/what-is
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: Learn how Microsoft Defender for Identity helps detect, investigate, and respond to identity-based attacks across on-premises, cloud, and hybrid environments.
ms.date: 2026-07-23T00:00:00.0000000Z
ms.topic: overview
ms.reviewer: AbbyMSFT
locale: en-us
document_id: 81189541-c7e6-43b6-9766-63da782702e2
document_version_independent_id: 81189541-c7e6-43b6-9766-63da782702e2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/what-is.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: what-is
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/what-is.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: e873ac6a-38a1-8a31-cd37-5571c7bfa2c0
---

# Microsoft Defender for Identity Overview - Microsoft Defender for Identity | Microsoft Learn

Microsoft Defender for Identity helps organizations detect, investigate, and respond to identity-based attacks across on-premises, cloud, and hybrid environments. Attackers frequently target identities such as users, applications, and service accounts to gain access, escalate privileges, and maintain persistence.

Defender for Identity monitors identity signals from on-premises Active Directory and Microsoft Entra ID, other IAM solutions (for example, Okta). It analyzes these signals using behavioral analytics, threat intelligence, and known attack patterns to detect suspicious activity across the full identity attack lifecycle. Alerts include investigation context in the Microsoft Defender portal, helping security teams understand what happened, why it matters, and how to respond.

## Identity Security

Microsoft Defender for Identity is a core component of Microsoft Identity Security. Identity Security focuses on protecting identities by providing visibility into identity coverage and posture, detecting identity‑based threats, and enabling investigation and response across identity systems, applications, and infrastructure.

Defender for Identity streams identity signals into the Microsoft Defender portal, where they are correlated with data from endpoints, email, SaaS applications, cloud workloads, and other security sources. This correlation helps security teams identify anomalous behavior, track attacker movement, and respond through unified incidents that reflect the full scope of an attack rather than isolated alerts.

## Defender for Identity capabilities

Defender for Identity delivers a modern identity threat detection solution with:

- Proactive identity security posture assessments
- Real‑time threat detection using analytics and behavioral intelligence
- Investigation of suspicious activities with clear, actionable incident context
- Remediation actions for compromised identities

### Prevent breaches with proactive identity security posture assessments

Defender for Identity helps organizations proactively reduce their identity attack surface. It evaluates identity configurations and highlights security weaknesses that attackers commonly exploit, allowing teams to address risks before they are abused.

Key posture capabilities include:

- Identity security posture assessments available through Microsoft Secure Score
- Identification of risky configurations and exposures
- Analysis of lateral movement paths that reveal how an attacker could traverse the environment

These insights help organizations strengthen identity resilience and reduce the likelihood of successful compromise.

### Detect identity-based threats

Defender for Identity is designed to detect threats that specifically target identities, including both human and non-human identities such as service accounts, synchronization accounts, and applications. Detection is based on behavioral analytics and signal correlation rather than single events.

Defender for Identity monitors and analyzes identity activity such as:

- Authentication and authorization behavior
- Credential abuse and risky sign ins
- Privilege escalation and suspicious role or group membership changes
- Lateral movement attempts within the environment
- Abnormal behavior related to service accounts and other non‑human identities

The following table shows how Defender for Identity detections align to key stages of an identity based attack:

| Attack stage | Defender for Identity detections |
| --- | --- |
| Reconnaissance | Identifies suspicious discovery activity, such as attempts to enumerate user names, group membership, IP addresses, and resources. |
| Compromised credentials | Detects attempts to compromise credentials using techniques such as brute force, repeated failed authentications, and suspicious changes to user group membership. |
| Lateral movement | Detects attempts to move laterally and expand control of sensitive identities and across different environments. |
| AD Domain dominance | Highlights behavior associated with full domain compromise, such as remote code execution on domain controllers, DCShadow, malicious domain controller replication, and Golden Ticket activity. |

Attackers often begin with any accessible identity and then move laterally toward high-value targets such as domain administrators, global administrators, and application administrators, along with sensitive data. Defender for Identity helps identify these behaviors early by building behavioral profiles for users, devices, and accounts and detecting deviations that indicate attacker activity.

### Investigate identity threats

Defender for Identity generates alerts that are enriched with context such as affected identities, related activity, and attacker techniques. Analysts can use this context to validate suspicious behavior and understand what happened.

Defender for Identity also supports identity investigation and hunting workflows. Identity entities and authentication activity are available within the Microsoft Defender portal, enabling security teams to investigate activity patterns and hunt for additional identity based threats across cloud, on-premises, and hybrid users.

### Respond to identity-based attacks

Defender for Identity supports response by:

- Correlating identity alerts into unified incidents in Microsoft Defender
- Providing identity context (users, accounts, roles, and lateral movement indicators) to scope impact and prioritize actions
- Enabling remediation actions in the Microsoft Defender portal for affected identities and related entities

## Microsoft Defender portal experience

The Microsoft Defender portal provides a unified experience for monitoring, investigating, and responding to identity threats. From the portal, security teams can:

- View identity based alerts and correlated incidents
- Investigate users, devices, and identity relationships
- Track identity security posture and remediation recommendations
- Perform response actions on compromised identities

By contributing rich identity context into unified incidents, Defender for Identity helps security teams understand attacker behavior, prioritize risk, and take action to disrupt identity based attacks across the organization.

## Architecture overview

Microsoft Defender for Identity uses lightweight [sensors](deploy/deploy-defender-identity), API connectors, and a cloud‑based analytics service managed in the Microsoft Defender portal.

Sensors run on your identity infrastructure, capturing and parsing relevant network traffic and Windows events locally. API connectors integrate external Identity and Access Management (IAM) systems, to provide comprehensive identity protection.

Only the required signals are sent to the Defender for Identity cloud service, minimizing performance impact and avoiding complex network changes.

The cloud service analyzes identity signals and integrates them with other Microsoft Defender workloads, contributing identity intelligence to correlated alerts and incidents in Microsoft Defender.