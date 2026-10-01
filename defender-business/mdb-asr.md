---
layout: Conceptual
title: Attack Surface Reduction in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-business/mdb-asr
breadcrumb_path: /defender-business/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn about attack surface reduction capabilities in Microsoft Defender for Business, including ASR rules, controlled folder access, and firewall protection.
author: chrisda
ms.author: chrisda
ms.date: 2026-06-10T00:00:00.0000000Z
ms.topic: concept-article
ms.service: defender-business
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.reviewer: efratka
ms.custom: msecd-doc-authoring-1012
ai-usage: ai-assisted
locale: en-us
document_id: 216e8d4b-f9a5-2687-3bc5-2f0fad2126a0
document_version_independent_id: 216e8d4b-f9a5-2687-3bc5-2f0fad2126a0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-business/mdb-asr.md
site_name: Docs
depot_name: Learn.defender-business
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdb-asr
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-business/mdb-asr.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b11ae577-8d18-47ab-998c-ea182a941e71
- https://authoring-docs-microsoft.poolparty.biz/devrel/bba62c59-6b53-4be4-8b9d-6624f9184c22
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/87b1d24d-826d-4337-90a0-b6c35e4561f2
- https://authoring-docs-microsoft.poolparty.biz/devrel/f3a81ffb-ee36-4ec7-b54a-01b6681aff65
platformId: 5b5fcb2f-83d9-413b-e8bb-e4ff9b6bb092
---

# Attack Surface Reduction in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn

*Attack surfaces* are all the places and ways the network and devices in your organization are vulnerable to cyberattack. For example:

- Unsecured devices.
- Unrestricted access to URLs on company devices.
- Unrestricted running of apps or scripts on company devices.

To help protect your network and devices, Microsoft Defender for Business includes several attack surface reduction capabilities. These capabilities include *attack surface reduction (ASR) rules* as described in the following table:

| Capability | Description |
| --- | --- |
| **[Attack surface reduction (ASR) rules](/en-us/defender-endpoint/attack-surface-reduction-rules-overview)** | Prevent specific actions commonly associated with malicious activity from running on Windows devices. |
| **[Controlled folder access (CFA)](/en-us/defender-endpoint/controlled-folder-access-overview)** | Allow only trusted apps to access protected folders on Windows devices. Think of this capability as ransomware mitigation. |
| **[Firewall protection](mdb-firewall)** | Determines which network traffic can flow to or from your organization's devices. |
| **[Network protection](/en-us/defender-endpoint/network-protection)** | Prevent users from accessing dangerous domains through applications on their Windows and Mac devices. Network protection is also a key component of [web content filtering](mdb-web-content-filtering). |
| **[Web protection](/en-us/defender-endpoint/web-protection-overview)** | Integrates with web browsers and works with network protection to protect against web threats and unwanted content. Web protection includes [web threat protection](/en-us/defender-endpoint/web-threat-protection), [web content filtering](/en-us/defender-endpoint/web-content-filtering), and [custom indicators](/en-us/defender-endpoint/indicators-overview). |

## Configure attack surface reduction features

Note

Microsoft 365 Business Premium includes Microsoft Intune Plan 1, which is the recommended method to configure and deploy security features on devices. Standalone Defender for Business doesn't include Intune, so you need to use another configuration method, for example, Group Policy or PowerShell locally on devices.

- **Attack surface reduction (ASR) rules**: For more information, see [Deployment and configuration methods for ASR rules](/en-us/defender-endpoint/attack-surface-reduction-rules-overview#deployment-and-configuration-methods-for-asr-rules) and [ASR rules deployment guide](/en-us/defender-endpoint/attack-surface-reduction-rules-deployment).
- **Controlled folder access (CFA)**: For more information, see [Deployment and configuration methods for CFA](/en-us/defender-endpoint/controlled-folder-access-overview#deployment-and-configuration-methods-for-cfa).
- **Firewall protection**: Enabled by default when devices are onboarded to Defender for Business and [firewall policies in Defender for Business](mdb-firewall) are applied.
- **Network protection**: Enabled by default when devices are onboarded to Defender for Business and [next-generation protection policies](mdb-next-generation-protection) are applied. Default policies are configured with the recommended security settings.
- **Web protection**: [Set up web content filtering in Microsoft Defender for Business](mdb-web-content-filtering).

## Monitor attack surface reduction features

You can monitor how attack surface reduction features are working in your organization by using the following reports in the Microsoft Defender portal:

- **ASR rules**: [Attack surface reduction (ASR) rules report](/en-us/defender-endpoint/attack-surface-reduction-rules-report)
- **Controlled folder access**: [Monitor controlled folder access activity](/en-us/defender-endpoint/controlled-folder-access-monitor)
- **Network and web protection**: [Web protection monitoring report](/en-us/defender-endpoint/web-protection-monitoring)
- **Firewall**: [Host firewall reporting](/en-us/defender-endpoint/host-firewall-reporting)