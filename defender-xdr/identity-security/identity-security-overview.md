---
layout: Conceptual
title: Microsoft Defender Identity Security Overview - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/identity-security/identity-security-overview
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Protect your organization from identity-based threats with Microsoft Defender's integrated identity security solution. Detect, investigate, and respond to attacks across your environment.
author: AbbyMSFT
ms.author: abbyweisberg
ms.reviewer: maelgami
ms.date: 2026-02-18T00:00:00.0000000Z
ms.topic: article
ms.service: defender-xdr
locale: en-us
document_id: 12ffc0af-0963-c86f-ad5a-fc030a8d0939
document_version_independent_id: 12ffc0af-0963-c86f-ad5a-fc030a8d0939
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/identity-security/identity-security-overview.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity-security/identity-security-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/identity-security/identity-security-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: cc612a53-d3a9-c944-616b-a3e04e434953
---

# Microsoft Defender Identity Security Overview - Microsoft Defender XDR | Microsoft Learn

Microsoft Defender identity security detects, investigates, and responds to threats that target digital identities. Because identities are a primary attack vector in enterprise breaches, identity security is a core part of modern security architecture. Defender monitors identity activity, analyzes behavior, and detects anomalies that indicate malicious activity. When threats are identified, it supports rapid response actions such as isolating accounts, enforcing authentication controls, and triggering automated remediation.

Defender protects identities across the organization through a single, integrated identity security solution that brings posture management, threat detection, and response into one platform. Coverage includes on-premises Active Directory, cloud identity providers such as Microsoft Entra ID, SaaS applications, and supported third-party identity providers. Both human identities and non-human identities (NHIs)—including service accounts, service principals, and OAuth applications—are protected. Connecting these identity sources provides end-to-end visibility and enables earlier response to identity-based attacks.

## Identity security capabilities

Defender identity security provides a set of capabilities that address both high-level posture management and in-depth threat investigation.

### Identity protection for all identity types

Identity security protects human and non-human identities across Microsoft and non-Microsoft systems, including identities used by applications and automated agents:

- **Non-human and application identity protection**: Discovers and protects service accounts, service principals, OAuth applications, cloud app identities, and agentic identities.
- **Unified signal ingestion**: Ingests identity signals from Microsoft and non-Microsoft sources into the unified identity inventory to provide consistent visibility across all identity types.
- **Non-Microsoft identity and PAM integration**: Extends protection to external identity providers and privileged access management (PAM) solutions.

### Insight into identity coverage and maturity

The coverage and maturity page helps assess and improve identity protection across the environment:

- **Maturity and coverage scoring**: Presents identity protection maturity as a simple score to track progress and guide improvement.
- **Deployment and coverage insights**: Shows which identity sources are connected, which protections are enabled, and where gaps exist across Active Directory, Entra ID, SaaS applications, non-human identities, and third-party providers.
- **Recommended Actions**: Identifies deployment gaps and next actions across identity sources, Entra Conditional Access (CA) policies, SaaS applications, and NHIs to provide optimum identity protection.

### Unified investigation and response capabilities

Identity security provides integrated capabilities for detecting and responding to identity-based threats:

- **Unified identity inventory**: The unified identity inventory consolidates identity accounts and relationships across on-premises Active Directory, Entra ID, SaaS applications, and third-party identity providers.

    - Provides a single view of all identity types, including users and non-human identities.
    - Supplies context for posture management, threat detection, and investigation.
    - Enables analysts to pivot from incidents and alerts to identity relationships, permissions, and activity.
- **Threat detection and hunting**: Identity detections are unified across Defender, with identity-focused queries available in advanced hunting.
- **Attack disruption actions**: Active attacks can be contained by disabling compromised accounts, revoking sessions, isolating devices, and resetting credentials.

### Insight into identity risk and conditional access

Defender integrates with Microsoft Entra to strengthen identity protection:

- **Identity risk score**: Aggregates signals from Defender for Identity and Entra ID Protection to help prioritize investigations and drive automated enforcement.
- **Conditional Access coverage insights**: Identifies missing or weak CA policy coverage and provides recommendations during onboarding.
- **Security Copilot integration**: Identity insights flow into Security Copilot to support faster triage and investigation.