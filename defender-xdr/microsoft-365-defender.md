---
layout: Conceptual
title: What is Microsoft Defender XDR? - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/microsoft-365-defender
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Microsoft Defender XDR is a coordinated threat protection solution designed to protect devices, identity, data, and applications.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.custom:
- admindeeplinkDEFENDER
- intro-overview
ms.collection:
- essentials-overview
- tier1
ms.topic: overview
adobe-target: true
ms.date: 2026-08-07T00:00:00.0000000Z
locale: en-us
document_id: f40be2e8-cf32-599c-2d3f-920c2af1284e
document_version_independent_id: f40be2e8-cf32-599c-2d3f-920c2af1284e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/microsoft-365-defender.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: microsoft-365-defender
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/microsoft-365-defender.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 3cc55dcd-c123-c2e2-a80a-bc31cb61c9fc
---

# What is Microsoft Defender XDR? - Microsoft Defender XDR | Microsoft Learn

Microsoft Defender XDR is a unified pre- and post-breach enterprise defense suite that natively coordinates detection, prevention, investigation, and response across endpoints, identities, email, and applications to provide integrated protection against sophisticated attacks.

Microsoft Defender helps security teams protect their organizations and detect threats by using information from other Microsoft security products, including:

- [**Microsoft Defender for Endpoint**](/en-us/defender-endpoint/microsoft-defender-endpoint)
- [**Microsoft Defender for Office 365**](/en-us/defender-office-365/mdo-about#defender-for-office-365-plan-1-vs-plan-2-cheat-sheet)
- [**Microsoft Defender for Identity**](/en-us/defender-for-identity/what-is)
- [**Microsoft Defender for Cloud Apps**](/en-us/defender-cloud-apps/what-is-defender-for-cloud-apps)
- [**Microsoft Defender Vulnerability Management**](/en-us/defender-vulnerability-management/defender-vulnerability-management)
- [**Microsoft Defender for Cloud**](/en-us/azure/defender-for-cloud/defender-for-cloud-introduction)
- [**Microsoft Entra ID Protection**](/en-us/azure/active-directory/identity-protection/overview-identity-protection)
- [**Microsoft Data Loss Prevention**](/en-us/microsoft-365/compliance/dlp-learn-about-dlp)
- [**App Governance**](/en-us/defender-cloud-apps/app-governance-manage-app-governance)
- [**Microsoft Purview Insider Risk Management**](/en-us/purview/insider-risk-management-solution-overview)
- [**Microsoft Security Exposure Management**](/en-us/security-exposure-management)

With the integrated Microsoft Defender solution, security professionals can stitch together the threat signals that each of these products receive and determine the full scope and impact of the threat; how it entered the environment, what it's affected, and how it's currently impacting the organization. Microsoft Defender takes automatic action to prevent or stop the attack and self-heal affected mailboxes, endpoints, and user identities.

Note

Microsoft Defender correlates signals from Microsoft security products that you have licensed and provisioned access to.

## Microsoft Defender protection

Microsoft Defender services protect:

- **Endpoints with Defender for Endpoint** - Microsoft Defender for Endpoint is a unified endpoint platform for preventative protection, post-breach detection, automated investigation, and response.
- **Assets with Defender Vulnerability Management** - Microsoft Defender Vulnerability Management delivers continuous asset visibility, intelligent risk-based assessments, and built-in remediation tools to help your security and IT teams prioritize and address critical vulnerabilities and misconfigurations across your organization.
- **Email and collaboration with Defender for Office 365** - Defender for Office 365 safeguards your organization against malicious threats posed by email messages, links (URLs) and collaboration tools.
- **Identities with Defender for Identity and Microsoft Entra ID Protection** - Microsoft Defender for Identity is a cloud-based security solution that uses your on-premises Active Directory signals to identify, detect, and investigate advanced threats, compromised identities, and malicious insider actions directed at your organization. Microsoft Entra ID Protection uses the learnings Microsoft acquired from their position in organizations with Microsoft Entra ID, the consumer space with Microsoft Accounts, and in gaming with Xbox to protect your users.
- **Applications with Defender for Cloud Apps** - Microsoft Defender for Cloud Apps is a comprehensive cross-SaaS solution bringing deep visibility, strong data controls, and enhanced threat protection to your cloud apps.

Microsoft Defender's unique cross-product layer augments the individual service components to:

- Help protect against attacks and coordinate defensive responses across the services through signal sharing and automated actions.
- Narrate the full story of the attack across product alerts, behaviors, and context for security teams by joining data on alerts, suspicious events and impacted assets to incidents.
- Automate response to compromise by triggering self-healing for impacted assets through automated remediation.
- Enable security teams to perform detailed and effective threat hunting over endpoint, identity, email, and cloud app data.

Microsoft Defender XDR cross-product features include:

- **Cross-product single pane of glass in the Microsoft Defender portal** - A central view for all information on detections, impacted assets, automated actions taken, and related evidence in a single queue and a single pane in [Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2077139).
- **Combined incidents queue** - To help security professionals focus on what is critical by ensuring the full attack scope, impacted assets and automated remediation actions are grouped together and surfaced in a timely manner.
- **[Automatic attack disruption](automatic-attack-disruption)** - Microsoft Defender XDR correlates high-confidence signals from multiple workloads and automatically applies containment actions to stop in-progress attacks and limit lateral movement.

    For example, if a malicious file is detected on an endpoint protected by Defender for Endpoint, it instructs Defender for Office 365 to scan and remove the file from all email messages. The file is blocked on sight by the entire Microsoft 365 security suite.
- **Self-healing for compromised devices, user identities, and mailboxes** - Microsoft Defender uses AI-powered automatic actions and playbooks to remediate impacted assets back to a secure state. Microsoft Defender leverages automatic remediation capabilities of the suite products to ensure all impacted assets related to an incident are automatically remediated where possible.
- **Cross-product threat hunting** - Security teams can leverage their unique organizational knowledge to hunt for signs of compromise by creating their own custom queries over the raw data collected by the various protection products. Microsoft Defender XDR provides query-based access to 30 days of historic raw signals and alert data from Defender for Endpoint, Defender for Office 365, Defender for Identity, and Defender for Cloud Apps.

## Get started

Microsoft Defender XDR licensing requirements must be met before you can enable the service in the Microsoft Defender portal at https://security.microsoft.com. For more information, see:

- [Licensing requirements](prerequisites#licensing-requirements)
- [Turn on Microsoft Defender XDR](m365d-enable)
- [Microsoft Defender XDR in the Microsoft Defender portal](microsoft-365-defender-portal)

Tip

Do you want to learn more? Engage with the Microsoft Security community in our Tech Community: [Microsoft Defender XDR Tech Community](https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection).