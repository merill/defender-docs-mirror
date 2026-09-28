---
layout: Conceptual
title: Attack surface reduction in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/attack-surface-reduction-overview
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Reduce your attack surface with Microsoft Defender for Endpoint capabilities like ASR rules, exploit protection, network protection, and controlled folder access.
author: chrisda
ms.author: chrisda
ms.service: defender-endpoint
ms.subservice: asr
ms.topic: concept-article
ms.collection:
- m365-security
- tier2
- mde-asr
ms.custom: msecd-doc-authoring-1012
ms.date: 2026-05-04T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: a3dc1a9e-0fab-eec8-3064-559408ed44a2
document_version_independent_id: a3dc1a9e-0fab-eec8-3064-559408ed44a2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/attack-surface-reduction-overview.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: attack-surface-reduction-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/attack-surface-reduction-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bba62c59-6b53-4be4-8b9d-6624f9184c22
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/f3a81ffb-ee36-4ec7-b54a-01b6681aff65
platformId: f2fe79ba-f046-a9d0-1e4d-f4c8e1cae417
---

# Attack surface reduction in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Attack surface reduction is a set of capabilities in Microsoft Defender for Endpoint that eliminate risky or unnecessary behaviors on devices and networks, reducing the opportunities that attackers have to compromise your organization. Attack surfaces are all the places where your organization is vulnerable to cyberthreats. By hardening these surfaces, you can prevent attacks from happening in the first place.

These capabilities block risky software behaviors, prevent connections to malicious sites, and protect data from unauthorized access or exfiltration. Together, they form a layered defense that complements the detection and response features in Defender for Endpoint.

## Attack surface reduction capabilities

Attack surface reduction in Defender for Endpoint includes the following capabilities:

- **Attack surface reduction (ASR) rules** constrain risky software behaviors that attackers exploit, such as launching executables that attempt to download files, running obfuscated scripts, or performing actions that apps don't normally initiate during day-to-day work. For more information, see [Attack surface reduction (ASR) rules overview](attack-surface-reduction-rules-overview).
- **Controlled folder access** (CFA) protects valuable data from malicious apps and threats like ransomware. It checks apps against a list of known, trusted apps and prevents untrusted apps from modifying files in protected folders. For more information, see [Controlled folder access (CFA) overview](controlled-folder-access-overview).
- **Exploit protection** applies exploit mitigation techniques to operating system processes and apps automatically. It builds on the protections that were available in the Enhanced Mitigation Experience Toolkit (EMET) and integrates with Defender for Endpoint for reporting and alerting. For more information, see [Protect devices from exploits](exploit-protection).
- **Network protection** prevents connections to malicious or suspicious domains and IP addresses. It extends Microsoft Defender SmartScreen protection to block all outbound HTTP(S) traffic that attempts to connect to low-reputation sources. For more information, see [Network protection](network-protection).
- **Web protection** secures devices against web threats and helps regulate unwanted content. Web protection includes web threat protection, web content filtering, and custom indicators. For more information, see [Web protection](web-protection-overview).
- **Web content filtering** tracks and regulates access to websites based on their content categories, allowing you to block categories that violate compliance regulations or organizational policies. For more information, see [Web content filtering](web-content-filtering).
- **Device control** determines whether users can install and use peripheral devices like USB drives, printers, and Bluetooth devices on their computers. Device control helps prevent data loss and malware from removable media. For more information, see [Device control in Microsoft Defender for Endpoint](device-control-overview).
- **Network firewall reporting** integrates with Windows Firewall to provide centralized visibility into firewall events in the Microsoft Defender portal. For more information, see [Host firewall reporting](host-firewall-reporting).

The availability of these features is summarized in the following table:

| Feature | Windows | macOS | Linux |
| --- | --- | --- | --- |
| ASR rules | Y | N | N |
| Controlled folder access | Y | N | N |
| Exploit protection | Y | N | N |
| Network protection | Y | Y | Y^\*^ |
| Web protection | Y | Y | Y^\*^ |
| Web content filtering | Y | Y | Y |
| Device control | Y | Y | N |
| Firewall reporting | Y | N | N |

^\*^ Currently in Preview.

### Related Windows security features

The following Windows security features complement attack surface reduction in Defender for Endpoint, but are configured and managed separately:

- **Microsoft Defender Application Guard** provides hardware-based isolation for Microsoft Edge, opening untrusted sites in a container to protect your organization. For more information, see [Microsoft Defender Application Guard overview](/en-us/windows/security/application-security/application-isolation/microsoft-defender-application-guard/md-app-guard-overview).
- **Windows Defender Application Control (WDAC)** ensures that only trusted applications run on your devices. For more information, see [Application control for Windows](/en-us/windows/security/application-security/application-control/app-control-for-business/appcontrol).
- **Windows Firewall** controls inbound and outbound network traffic on devices. For more information, see [Windows Firewall with advanced security](/en-us/windows/security/operating-system-security/network-security/windows-firewall).

## How attack surface reduction fits into Defender for Endpoint

Attack surface reduction complements other Defender for Endpoint capabilities that detect and respond to threats after they occur. While next-generation protection and endpoint detection and response focus on identifying and remediating active threats, attack surface reduction prevents threats from gaining a foothold.

Each capability addresses a different part of the attack surface:

- **Risky software behavior**: ASR rules limit how applications and scripts can behave, blocking common techniques that attackers use to deliver malware or steal credentials.
- **Network connections**: Network protection and web protection block access to known malicious or inappropriate sites before content reaches the device.
- **Data and file access**: Controlled folder access and device control limit which applications and hardware can access or modify sensitive files.
- **Application vulnerabilities**: Exploit protection applies mitigations that make it harder for attackers to exploit vulnerabilities in operating system processes and applications.

## Audit mode

Audit mode helps you evaluate the impact of attack surface reduction features on your environment without affecting productivity. The following capabilities support audit mode:

- [Attack surface reduction (ASR) rules and exclusions](attack-surface-reduction-rules-configure)
- [Controlled folder access](controlled-folder-access-configure)
- [Exploit protection](enable-exploit-protection)
- [Network protection](enable-network-protection)

In audit mode, the features don't block apps, scripts, or connections. Instead, the Windows Event Log records events as if the features were active. You can review event logs and use advanced hunting in the Microsoft Defender portal to understand how each feature would affect your line-of-business applications. For more information about the data in Windows Event Viewer, see [View attack surface reduction events in Windows Event Viewer](attack-surface-reduction-windows-events).

## Management tools

You can configure attack surface reduction capabilities by using several management tools. The following tools are commonly used:

- Microsoft Intune
- Microsoft Configuration Manager
- Group Policy
- PowerShell cmdlets

The right tool depends on your organization's infrastructure and management preferences. For detailed configuration guidance, see the individual feature articles linked in the Attack surface reduction capabilities section.