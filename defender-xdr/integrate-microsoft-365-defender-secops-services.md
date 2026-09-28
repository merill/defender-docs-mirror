---
layout: Conceptual
title: Step 3. Plan for Microsoft Defender XDR integration with your SOC catalog of services - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/integrate-microsoft-365-defender-secops-services
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Evaluate your SOC catalog of services and learn how Microsoft Defender XDR components map to service areas such as threat intelligence, incident response, and endpoint detection.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- msftsolution-secops
- tier3
ms.topic: how-to
ms.date: 2026-08-07T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: 8eba55d8-c791-1cd1-8a6f-ba32178111e5
document_version_independent_id: 8eba55d8-c791-1cd1-8a6f-ba32178111e5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/integrate-microsoft-365-defender-secops-services.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: integrate-microsoft-365-defender-secops-services
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/integrate-microsoft-365-defender-secops-services.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: d58be39f-3265-0522-9b0f-12dec35ba8b1
---

# Step 3. Plan for Microsoft Defender XDR integration with your SOC catalog of services - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- Microsoft Defender XDR

## SOC services and Microsoft Defender XDR components

This section lists common SOC service areas and introduces the Microsoft Defender XDR components that map to those functions, so your team can plan integration and assign responsibilities.

An established Security Operations Center (SOC) should have a catalog of services that might include:

- Intrusion & malware analysis
- Attribution & reverse engineering
- Threat intelligence
- Analytics
- Hunting investigation
- Forensics
- Incident response
- Computer Security Incident Response Team (CSIRT) (that may be segregated from SOC)
- Compliance testing
- Insider threat & fraud monitoring
- Security incident & event monitoring
- Vulnerability scanning
- Extended Detection and Response (XDR)/Security Orchestration, Automation, and Response (SOAR)
- Phishing
- Data loss prevention
- Brand monitoring

The components of Microsoft Defender XDR are:

- **Microsoft Defender for Identity** (formerly Azure Advanced Threat Protection, also known as Azure ATP) is a cloud-based security solution that uses Active Directory Domain Services (AD DS) signals to identify, detect, and investigate advanced threats, compromised identities, and malicious insider actions directed at organizations.
- **Microsoft Defender for Endpoint** is a holistic, cloud delivered endpoint security solution for devices that includes risk-based vulnerability management and assessment, attack surface reduction, behavioral based and cloud-powered next generation protection, endpoint detection and response (EDR), automatic investigation and remediation, managed hunting services, rich APIs, and unified security management.
- **Microsoft Defender for Office 365** is a cloud-based email filtering service that helps protect organizations against unknown malware and viruses by providing robust zero-day protection and includes features to safeguard organizations from harmful links in real time. It also offers a comprehensive slate of investigation and hunting, response and remediation, awareness and training, and secure posture features.
- **Microsoft Defender for Cloud Apps** is a cloud access security broker (CASB) that supports various deployment modes including log collection, API connectors, and reverse proxy. It provides rich visibility, control over data travel, and sophisticated analytics to identify and combat cyberthreats across all Microsoft and third-party cloud services.

Because Microsoft Defender XDR components and technologies span various functions, your SOC team will need to determine which roles and responsibilities are best suited to manage each component of Microsoft Defender XDR and align to service function.

To integrate the capabilities of Microsoft Defender XDR, you will need to refine your SOC catalog of services. For more information about the capabilities of Microsoft Defender XDR, see the following articles:

- [What is Microsoft Defender for Endpoint?](/en-us/defender-endpoint/microsoft-defender-endpoint)
- [What is Microsoft Defender for Identity?](/en-us/defender-for-identity/what-is)
- [What is Defender for Office 365?](/en-us/defender-office-365/mdo-about)
- [What is Microsoft Defender for Cloud Apps?](/en-us/defender-cloud-apps/what-is-defender-for-cloud-apps)