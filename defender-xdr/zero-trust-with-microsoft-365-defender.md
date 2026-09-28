---
layout: Conceptual
title: Zero Trust with Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/zero-trust-with-microsoft-365-defender
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Microsoft Defender XDR contributes to a strong Zero Trust strategy and architecture.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- essentials-privacy
- essentials-security
- essentials-compliance
ms.custom: 
ms.topic: get-started
adobe-target: true
ms.date: 2026-09-10T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: ba8f3f64-9817-3b0a-c181-fbc31a1ef58e
document_version_independent_id: ba8f3f64-9817-3b0a-c181-fbc31a1ef58e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/zero-trust-with-microsoft-365-defender.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: zero-trust-with-microsoft-365-defender
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/zero-trust-with-microsoft-365-defender.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 1df4a4f0-d383-62cc-cdc7-1adf3639b31c
---

# Zero Trust with Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- Microsoft Defender XDR

Microsoft Defender XDR contributes to a strong Zero Trust strategy and architecture by providing extended detection and response (XDR). Microsoft Defender XDR works together with other Microsoft XDR tools and services and can be integrated with Microsoft Sentinel as a security information and event management (SIEM) source for a complete XDR/SIEM solution.

Microsoft Defender XDR is an XDR solution that automatically collects, correlates, and analyzes signal, threat, and alert data from across your Microsoft 365 environment, including endpoints, email, applications, and identities.

[![Diagram that shows the Microsoft Defender XDR in the Zero Trust architecture.](media/zero-trust-with-microsoft-365-defender/m365-zero-trust-architecture-defender.png)](media/zero-trust-with-microsoft-365-defender/m365-zero-trust-architecture-defender.png#lightbox)

In the illustration: Microsoft Defender provides XDR capabilities for protecting:

- Endpoints, including laptops and mobile devices
- Data in Office 365, including email
- Cloud apps, including other SaaS apps that your organization uses
- On-premises Active Directory Domain Services (AD DS) and Active Directory Federated Services (AD FS) servers

Microsoft Defender helps you apply the principles of Zero Trust in the following ways:

| Zero Trust principle | Met by |
| --- | --- |
| Verify explicitly | Microsoft Defender provides XDR across users, identities, devices, apps, and emails. |
| Use least privileged access | If used with Microsoft Entra ID Protection, Microsoft Defender blocks users based on the level of risk posed by an identity. Microsoft Entra ID Protection is licensed separately from Microsoft Defender and is included with Microsoft Entra ID P2. |
| Assume breach | Microsoft Defender continuously scans the environment for threats and vulnerabilities. It can implement automated remediation tasks, including automated investigations and isolating endpoints. |

## Extend Zero Trust with unified security operations

Unified security operations in the Defender portal extends Zero Trust beyond Defender XDR:

- **Verify explicitly** by using Microsoft Sentinel analytics and automation, Defender Threat Intelligence enrichment, Microsoft Security Exposure Management context, Defender for Cloud signals, and Microsoft Entra ID Protection risk.
- **Use least privilege** with Defender unified role-based access control (RBAC), Microsoft Entra Privileged Identity Management (PIM), Conditional Access app control, and Security Copilot on-behalf-of authentication.
- **Assume breach** with Defender XDR automatic attack disruption, Microsoft Sentinel automation rules and playbooks, Defender for Cloud response capabilities, and Microsoft Entra risk notifications.

To add Microsoft Defender to your Zero Trust strategy and architecture, go to [Pilot and deploy Microsoft Defender](pilot-deploy-overview) for a methodical guide to piloting and deploying Microsoft Defender components. The following table summarizes what these topics include.

| Includes | Prerequisites | Doesn't include |
| --- | --- | --- |
| Set up the evaluation and pilot environment for all components: <br>- Defender for Identity<br>- Defender for Office 365<br>- Defender for Endpoint<br>- Microsoft Defender for Cloud Apps<br><br> Protect against threats  Investigate and respond to threats | See the guidance for the architecture requirements for each component of Microsoft Defender. | Microsoft Entra ID Protection isn't included in this solution guide. It's included in [Step 1. Configure Zero Trust identity and device access protection](/en-us/microsoft-365/security/microsoft-365-zero-trust#step-1-configure-zero-trust-identity-and-device-access-protection-starting-point-policies). |