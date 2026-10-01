---
layout: Conceptual
title: Mobile Threat Defense Capabilities in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-business/mdb-mtd
breadcrumb_path: /defender-business/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Get an overview of mobile threat defense in Defender for Business. Learn what mobile threat defense includes and how to onboard devices.
author: chrisda
ms.author: chrisda
ms.date: 2025-09-25T00:00:00.0000000Z
ms.topic: article
ms.service: defender-business
ms.localizationpriority: medium
ms.collection:
- SMB
- m365-security
- m365-initiative-defender-business
- tier1
ms.reviewer: nehabha
locale: en-us
document_id: f123a4ef-d96c-814d-c381-cf212fa802c5
document_version_independent_id: f123a4ef-d96c-814d-c381-cf212fa802c5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-business/mdb-mtd.md
site_name: Docs
depot_name: Learn.defender-business
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdb-mtd
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-business/mdb-mtd.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b11ae577-8d18-47ab-998c-ea182a941e71
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/a72e95ff-4b4f-4cc1-90c6-7dcba67ff05f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/87b1d24d-826d-4337-90a0-b6c35e4561f2
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/24dc3ccd-591a-4415-a1fe-8759afafcb12
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 6c109180-aeef-69ca-e78e-5431a5ff1975
---

# Mobile Threat Defense Capabilities in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn

Microsoft Defender for Business provides advanced threat protection capabilities for devices, such as Windows and Mac clients. Defender for Business also includes mobile threat defense. Mobile threat defense capabilities help protect Android and iOS devices, without requiring you to use Microsoft Intune to onboard mobile devices.

In addition, mobile threat defense capabilities integrate with [Microsoft 365 Lighthouse](/en-us/microsoft-365/lighthouse/m365-lighthouse-overview), where Cloud Solution Providers (CSPs) can view information about vulnerable devices and help mitigate detected threats.

## What does mobile threat defense include?

The following table summarizes the capabilities that are included in mobile threat defense in Defender for Business:

| Capability | Android | iOS |
| --- | --- | --- |
| **Web Protection** Anti-phishing, blocking unsafe network connections, and support for custom indicators.  Web protection is turned on by default with [web content filtering](mdb-web-content-filtering). | ![](media/feature-present-icon.png) | ![](media/feature-present-icon.png) |
| **Malware protection** Scanning for malicious apps, including system apps. | ![](media/feature-present-icon.png) | ![](media/feature-absent-icon.png) |
| **Jailbreak detection** Detection of jailbroken devices. | ![](media/feature-absent-icon.png) | ![](media/feature-present-icon.png) |
| **Microsoft Defender Vulnerability Management**Vulnerability assessment of onboarded mobile devices. Includes vulnerability assessments for operating systems and apps for Android and iOS.  For more information, see [Use your vulnerability management dashboard in Microsoft Defender for Business](mdb-view-tvm-dashboard). | ![](media/feature-present-icon.png) | ![](media/feature-present-icon.png) ¹ |
| **Network Protection** Protection against rogue Wi-Fi related threats and rogue certificates.  Network protection is turned on by default with [next-generation protection](mdb-next-generation-protection).  As part of mobile threat defense, network protection also includes the ability to allow root certification authority and private root certification authority certificates in Intune. It also establishes trust with endpoints. | ![](media/feature-present-icon.png) ² | ![](media/feature-present-icon.png) ² |
| **Unified alerting** Alerts from all platforms are listed in the unified [Microsoft Defender portal](https://security.microsoft.com). In the navigation pane, choose **Incidents**.  For more information, see [View and manage incidents in Microsoft Defender for Business](mdb-view-manage-incidents) | ![](media/feature-present-icon.png) | ![](media/feature-present-icon.png) |
| **Conditional Access** and **conditional launch**[Conditional Access](/en-us/intune/intune-service/protect/conditional-access) and [conditional launch](/en-us/intune/intune-service/apps/app-protection-policies-access-actions) block risky devices from accessing corporate resources. <br>- Conditional Access policies require certain criteria to be met before a user can access company data on their mobile device.<br>- Conditional launch policies enable your security team to block access or wipe devices that don't meet certain criteria.<br>- Defender for Business risk signals can also be added to app protection policies. | ![](media/feature-absent-icon.png) ³ | ![](media/feature-absent-icon.png) ³ |
| **Privacy controls** Configure privacy in threat reports by controlling the data sent by Defender for Business. Privacy controls are available for admin and end users, and for both enrolled and unenrolled devices. | ![](media/feature-absent-icon.png) ³ | ![](media/feature-absent-icon.png) ³ |
| **Integration with Microsoft Tunnel** Integration with [Microsoft Tunnel](/en-us/intune/intune-service/protect/microsoft-tunnel-overview), a VPN gateway solution for Microsoft Intune. | ![](media/feature-absent-icon.png) ⁴ | ![](media/feature-absent-icon.png) ⁴ |

¹ Operating system vulnerabilities are included. Software and app vulnerabilities require Microsoft Intune. ² You can manage an allowlist of root certification authority certificates and private root certification authority certificates in Microsoft Intune. ³ Requires Microsoft Intune. ⁴ Requires Microsoft Intune. For more information, see [Prerequisites for the Microsoft Tunnel in Intune](/en-us/intune/intune-service/protect/microsoft-tunnel-prerequisites).

## How to get mobile threat defense capabilities

Mobile threat defense capabilities are now generally available to [Defender for Business](get-defender-business) customers. Here's how to get these capabilities for your organization:

1. Make sure that Defender for Business finished provisioning. In the [Microsoft Defender portal](https://security.microsoft.com), go to **Assets** &gt; **Devices**.

    - The message, *Hang on! We're preparing new spaces for your data and connecting them* means Defender for Business isn't finished provisioning. The process can take up to 24 hours to complete.
    - If you see a list of devices, or you're prompted to onboard devices, it means Defender for Business provisioning is complete.
2. Review and, if necessary, edit your [next-generation protection policies](mdb-next-generation-protection).
3. Review and, if necessary, edit your [firewall policies and custom rules](mdb-firewall).
4. Review and, if necessary, edit your [web content filtering](mdb-web-content-filtering) policy.
5. To onboard mobile devices, see the "Use the Microsoft Defender app" procedures in [Onboard devices to Microsoft Defender for Business](mdb-onboard-devices).