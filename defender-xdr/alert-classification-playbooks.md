---
layout: Conceptual
title: Alert classification playbooks in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/alert-classification-playbooks
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Review the alerts for well-known attacks and take recommended actions to remediate the attack and protect your network.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.topic: how-to
ms.custom:
- msecd-doc-authoring-1014
- autoir
- admindeeplinkDEFENDER
ms.reviewer: evaldm, isco
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 95edcf16-229e-88c1-6719-a5701e966053
document_version_independent_id: 95edcf16-229e-88c1-6719-a5701e966053
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/alert-classification-playbooks.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: alert-classification-playbooks
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/alert-classification-playbooks.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: c73efb10-e4fd-0538-c1d9-22f6cafcd2d9
---

# Alert classification playbooks in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

## Overview

Alert classification playbooks allow you to methodically review and quickly classify the alerts for well-known attacks and take recommended actions to remediate the attack and protect your network. Alert classification will also help in properly classifying the overall incident.

As a security researcher or security operations center (SOC) analyst, you must have access to the Microsoft Defender portal so that you can:

- Assess and review the generated alerts and associated incidents. See [investigate alerts](investigate-alerts).
- Search your tenant's security signal data and check for potential threats and suspicious activities. See [advanced hunting](advanced-hunting-overview).

Note

You can provide feedback to Microsoft about true positive and false positives alerts, not only at the end of the investigation, but also during the investigation process. This can help Microsoft with future analysis and classification of security events.

## Alert classification for Microsoft Defender for Office 365

[Microsoft Defender for Office 365](/en-us/defender-office-365/mdo-about) safeguards your organization against malicious threats posed by email messages, links (URLs), and collaboration tools. Defender for Office 365 includes:

- Threat protection policies

    Define threat-protection policies to set the appropriate level of protection for your organization.
- Reports

    View real-time reports to monitor Defender for Office 365 performance in your organization.
- Threat investigation and response capabilities

    Use leading-edge tools to investigate, understand, simulate, and prevent threats.
- Automated investigation and response capabilities

    Save time and effort investigating and mitigating threats.

Defender for Office 365 alerts can be classified as:

- True positive (TP) for confirmed malicious activity.
- False positive (FP) for confirmed non-malicious activity.

Note

Microsoft Defender portal ([Microsoft Defender portal](https://security.microsoft.com)) brings together functionality from existing Microsoft security portals. The Microsoft Defender portal emphasizes quick access to information, simpler layouts, and bringing related information together for easier use.

## Alert classification for Microsoft Defender for Cloud Apps

[Microsoft Defender for Cloud Apps](/en-us/defender-cloud-apps) is a Cloud Access Security Broker (CASB) that supports various deployment modes including log collection, API connectors, and reverse proxy. It provides rich visibility, control over data travel, and sophisticated analytics to identify and combat cyberthreats across all your Microsoft and third-party cloud services.

Defender for Cloud Apps natively integrates with leading Microsoft solutions and is designed with security professionals in mind. It provides simple deployment, centralized management, and innovative automation capabilities.

The Defender for Cloud Apps framework includes the capability to protect your network against cyberthreats and anomalies, detects unusual behavior across cloud apps to identify ransomware, compromised users or rogue applications. It enables the analysis of high-risk usage and can remediate automatically to limit the risk to your organization.

Defender for Cloud Apps alerts can be classified as:

- TP for confirmed malicious activity.
- Benign true positive (B-TP) for suspicious but not malicious activity, such as a penetration test or other authorized suspicious action.
- FP for confirmed non-malicious activity.

## Available alert classification playbooks

See these playbooks for steps to more quickly classify alerts for the following threats:

- [Suspicious email forwarding activity](alert-grading-playbook-email-forwarding)
- [Suspicious inbox manipulation rules](alert-grading-playbook-inbox-manipulation-rules)
- [Suspicious inbox forwarding rules](alert-grading-playbook-inbox-forwarding-rules)
- [Suspicious IP addresses related to password spray activity](alert-classification-suspicious-ip-password-spray)
- [Password spray attacks](alert-classification-password-spray-attack)
- [Malicious Exchange connectors](alert-classification-malicious-exchange-connectors)

See [Investigate alerts](investigate-alerts) for information on how to examine alerts with the Microsoft Defender portal.

Tip

Do you want to learn more? Engage with the Microsoft Security community in our Tech Community: [Microsoft Defender XDR Tech Community](https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection).