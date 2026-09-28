---
layout: Conceptual
title: Overview of Microsoft Defender for Endpoint Plan 1 - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/defender-endpoint-plan-1
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Get an overview of Defender for Endpoint Plan 1. Learn about the features and capabilities included in this endpoint protection subscription.
author: paulinbar
ms.author: painbar
ms.topic: overview
ms.service: defender-endpoint
ms.subservice: onboard
ms.localizationpriority: medium
ms.date: 2026-07-28T00:00:00.0000000Z
ms.reviewer: shlomiakirav
ms.collection:
- m365-security
- tier1
ms.custom: intro-overview
locale: en-us
document_id: 039a8d99-1411-cd3a-91ec-677104d78b1f
document_version_independent_id: 039a8d99-1411-cd3a-91ec-677104d78b1f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/defender-endpoint-plan-1.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-endpoint-plan-1
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/defender-endpoint-plan-1.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 1a0d6f87-e75d-7e6b-03bf-37df36a58038
---

# Overview of Microsoft Defender for Endpoint Plan 1 - Microsoft Defender for Endpoint | Microsoft Learn

Microsoft Defender for Endpoint is an enterprise endpoint security platform designed to help organizations to prevent, detect, investigate, and respond to advanced threats. Defender for Endpoint is now available in two plans:

- **Defender for Endpoint Plan 1**, described in this article; and
- **[Defender for Endpoint Plan 2](microsoft-defender-endpoint)**, generally available, and formerly known as [Defender for Endpoint](microsoft-defender-endpoint).

The green boxes in the following image depict what's included in Defender for Endpoint Plan 1:

[![A diagram showing what's included with Defender for Endpoint Plan 1](/en-us/defender/media/mde-p1/mde-p1-overview-diagram.png)](/en-us/defender/media/mde-p1/mde-p1-overview-diagram.png#lightbox)

Use this guide to:

- Get an overview of what's included in Defender for Endpoint Plan 1
- [Learn how to set up and configure Defender for Endpoint Plan 1](mde-p1-setup-configuration)
- [Get started using the Microsoft Defender portal, where you can view incidents and alerts, manage devices, and use reports about detected threats](mde-plan1-getting-started)
- [Get an overview of maintenance and operations](preferences-setup)

For minimum requirements for Microsoft Defender for Endpoint, see [Microsoft Defender for Endpoint requirements](minimum-requirements).

## Defender for Endpoint Plan 1 capabilities

Defender for Endpoint Plan 1 includes the following capabilities:

- **Next-generation protection** that includes industry-leading, robust antimalware and antivirus protection
- **Manual response actions**, such as sending a file to quarantine, that your security team can take on devices or files when threats are detected
- **Attack surface reduction capabilities** that harden devices, prevent zero-day attacks, and offer granular control over endpoint access and behaviors
- **Centralized configuration and management** with the Microsoft Defender portal and integration with Microsoft Intune

The following sections provide more details about these capabilities.

## Next-generation protection

Next-generation protection includes robust antivirus and antimalware protection. With next-generation protection, you get:

- Behavior-based, heuristic, and real-time antivirus protection
- Cloud-delivered protection, which includes near-instant detection and blocking of new and emerging threats
- Dedicated protection and product updates, including updates related to Microsoft Defender Antivirus

To learn more, see [Next-generation protection overview](next-generation-protection).

## Manual response actions

Manual response actions are actions that your security team can take when threats are detected on endpoints or in files. Defender for Endpoint includes certain [manual response actions that can be taken on a device](respond-machine-alerts) that is detected as potentially compromised or has suspicious content. You can also run [response actions on files](respond-file-alerts) that are detected as threats. The following table summarizes the manual response actions that are available in Defender for Endpoint Plan 1. 

| File/Device | Action | Description |
| --- | --- | --- |
| Device | Run antivirus scan | Starts an antivirus scan. If any threats are detected on the device, those threats are often addressed during an antivirus scan. |
| Device | Isolate device | Disconnects a device from your organization's network while retaining connectivity to Defender for Endpoint. This action enables you to monitor the device and take further action if needed. |
| File | Add an indicator to block or allow a file | Block indicators prevent portable executable files from being read, written, or executed on devices. <br>Allow indicators prevent files from being blocked or remediated. |

To learn more, see the following articles:

- [Take response actions on devices](respond-machine-alerts)
- [Take response actions on files](respond-file-alerts)

## Attack surface reduction

Your organization's attack surfaces are all the places where you're vulnerable to cyberattacks. With Defender for Endpoint Plan 1, you can reduce your attack surfaces by protecting the devices and applications that your organization uses. The attack surface reduction capabilities that are included in Defender for Endpoint Plan 1 are described in the following sections.

- Attack surface reduction (ASR) rules
- Ransomware mitigation
- Device control
- Web protection
- Network protection
- Network firewall
- Application control

To learn more about attack surface reduction capabilities in Defender for Endpoint, see [Overview of attack surface reduction](attack-surface-reduction-overview).

### Attack surface reduction rules

Attack surface reduction (ASR) rules target risky software behavior, because software used by attackers exhibit similar behavior.

To learn more, see [Attack surface reduction (ASR) rules overview](attack-surface-reduction-rules-overview).

### Ransomware mitigation

With controlled folder access (CFA), you get ransomware mitigation. Controlled folder access allows only trusted apps to access protected folders on your endpoints. Apps are added to the trusted apps list based on their prevalence and reputation. Your security operations team can add or remove apps from the trusted apps list, too.

To learn more, see [Controlled folder access (CFA) overview](controlled-folder-access-overview).

### Device control

Sometimes threats to your organization's devices come in the form of files on removable drives, such as USB drives. Defender for Endpoint includes capabilities to help prevent threats from unauthorized peripherals from compromising your devices. You can configure Defender for Endpoint to block or allow removable devices and files on removable devices.

To learn more, see [Control USB devices and removable media](device-control-overview).

### Web protection

With web protection, you can protect your organization's devices from web threats and unwanted content. Web protection includes web threat protection and web content filtering.

- [Web threat protection](web-threat-protection) prevents access to phishing sites, malware vectors, exploit sites, untrusted or low-reputation sites, and sites that you explicitly block.
- [Web content filtering](web-content-filtering) prevents access to certain sites based on their category. Categories can include adult content, leisure sites, legal liability sites, and more.

To learn more, see [web protection](web-protection-overview).

### Network protection

With network protection, you can prevent your organization from accessing dangerous domains that might host phishing scams, exploits, and other malicious content on the Internet.

To learn more, see [Protect your network](network-protection).

### Network firewall

With network firewall protection, you can set rules that determine which network traffic is permitted to flow to or from your organization's devices. With your network firewall and advanced security that you get with Defender for Endpoint, you can:

- Reduce the risk of network security threats
- Safeguard sensitive data and intellectual property
- Extend your security investment

To learn more, see [Windows Defender Firewall with advanced security](/en-us/windows/security/operating-system-security/network-security/windows-firewall).

### Application control

Application control protects your Windows endpoints by running only trusted applications and code in the system core (kernel). Your security team can define application control rules that consider an application's attributes, such as its codesigning certificates, reputation, launching process, and more. Application control is available in Windows 10 or later.

To learn more, see [Application control for Windows](/en-us/windows/security/application-security/application-control/app-control-for-business/appcontrol).

## Centralized management

Defender for Endpoint Plan 1 includes the Microsoft Defender portal, which enables your security team to view current information about detected threats, take appropriate actions to mitigate threats, and centrally manage your organization's threat protection settings.

To learn more, see [Microsoft Defender portal overview](/en-us/defender-xdr/microsoft-365-security-center-mde).

### Role-based access control

Using role-based access control (RBAC), your security administrator can create roles and groups to grant appropriate access to the Microsoft Defender portal (https://security.microsoft.com). With RBAC, you have fine-grained control over who can access the Defender for Cloud, and what they can see and do.

To learn more, see [Manage portal access using role-based access control](rbac).

Important

Starting February 16, 2025, new Microsoft Defender for Endpoint customers will only have access to the Unified Role-Based Access Control (URBAC). Existing customers keep their current roles and permissions. For more information, see URBAC [Unified Role-Based Access Control (URBAC) for Microsoft Defender for Endpoint](/en-us/defender-xdr/manage-rbac)

### Reporting

The Microsoft Defender portal (https://security.microsoft.com) provides easy access to information about detected threats and actions to address those threats.

- The **Home** page includes cards to show at a glance which users or devices are at risk, how many threats were detected, and what alerts/incidents were created.
- The **Incidents & alerts** section lists any incidents that were created as a result of triggered alerts. Alerts and incidents are generated as threats are detected across devices.
- The **Action center** lists remediation actions that were taken. For example, if a file is sent to quarantine, or a URL is blocked, each action is listed in the Action center on the **History** tab.
- The **Reports** section includes reports that show threats detected and their status.

To learn more, see [Get started with Microsoft Defender for Endpoint Plan 1](mde-plan1-getting-started).

### APIs

With the Defender for Endpoint APIs, you can automate workflows and integrate with your organization's custom solutions.

To learn more, see [Defender for Endpoint APIs](api/management-apis).

## Licensing

Defender for Endpoint Plan 1 is available as a standalone subscription or as part of Microsoft 365 E3. For server deployments, you can license Defender for Endpoint Plan 1 for servers separately.

If you're also using [Microsoft Defender for Servers](/en-us/azure/defender-for-cloud/defender-for-servers-overview) as part of Defender for Cloud, check if you're eligible for a [licensing discount when you have both Defender for Endpoint and Defender for Servers](/en-us/azure/defender-for-cloud/faq-defender-for-servers#can-i-get-a-discount-if-i-already-have-a-microsoft-defender-for-endpoint-license-).