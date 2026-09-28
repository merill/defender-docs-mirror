---
layout: Conceptual
title: Cloud protection and Microsoft Defender Antivirus - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/cloud-protection-microsoft-defender-antivirus
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn about cloud protection and Microsoft Defender Antivirus
ms.service: defender-endpoint
ms.localizationpriority: medium
author: chrisda
ms.author: chrisda
ms.reviewer: mkaminska
ms.custom: nextgen
ms.subservice: ngp
ms.topic: concept-article
ms.date: 2025-10-20T00:00:00.0000000Z
ms.collection:
- m365-security
- tier2
- mde-ngp
locale: en-us
document_id: 0c2ec571-5d42-ebf4-386a-4d546fa881b6
document_version_independent_id: 0c2ec571-5d42-ebf4-386a-4d546fa881b6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/cloud-protection-microsoft-defender-antivirus.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: cloud-protection-microsoft-defender-antivirus
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/cloud-protection-microsoft-defender-antivirus.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: e3e621e3-0ea6-74ff-f127-ac74a90bdc7b
---

# Cloud protection and Microsoft Defender Antivirus - Microsoft Defender for Endpoint | Microsoft Learn

Next-generation technologies in Microsoft Defender Antivirus provide near-instant, automated protection against new and emerging threats. To identify new threats dynamically, next-generation technologies work with large sets of interconnected data in the Microsoft Intelligent Security Graph and powerful artificial intelligence (AI) systems driven by advanced machine learning models. Cloud protection works together with Microsoft Defender Antivirus to deliver accurate, real-time, and intelligent protection.

[\[!\[Diagram showing how cloud protection works together with Microsoft Defender Antivirus\](media/mde-cloud-protection.png)\](media/mde-cloud-protection.png#lightbox)](cloud-protection-configure)

Tip

We recommend keeping cloud protection turned on. To learn more, see [Why cloud protection should be turned on](cloud-protection-configure#why-cloud-protection-should-be-turned-on).

## Prerequisites

### Supported operating systems

- Windows

## How cloud protection works

Microsoft Defender Antivirus works seamlessly with Microsoft cloud services. These cloud protection services, also referred to as Microsoft Advanced Protection Service (MAPS), enhance standard real-time protection. With cloud protection, next-generation technologies provide rapid identification of new threats, sometimes even before a single endpoint is infected.

The following blog posts illustrate how cloud protection works:

- [Get to know the advanced technologies at the core of Microsoft Defender for Endpoint next-generation protection](https://www.microsoft.com/security/blog/2019/06/24/inside-out-get-to-know-the-advanced-technologies-at-the-core-of-microsoft-defender-atp-next-generation-protection/)
- [Why Microsoft Defender Antivirus is the most deployed in the enterprise](https://www.microsoft.com/security/blog/2018/03/22/why-windows-defender-antivirus-is-the-most-deployed-in-the-enterprise)
- [Behavior monitoring combined with machine learning spoils a massive coin-mining campaign](https://www.microsoft.com/security/blog/2018/03/07/behavior-monitoring-combined-with-machine-learning-spoils-a-massive-dofoil-coin-mining-campaign)
- [How artificial intelligence stopped an "Emotet" outbreak](https://www.microsoft.com/security/blog/2018/02/14/how-artificial-intelligence-stopped-an-emotet-outbreak)
- [Detonating a bad rabbit: Microsoft Defender Antivirus and layered machine learning defenses](https://www.microsoft.com/security/blog/2017/12/11/detonating-a-bad-rabbit-windows-defender-antivirus-and-layered-machine-learning-defenses)
- [Microsoft Defender Antivirus cloud protection service: Advanced real-time defense against never-before-seen malware](https://www.microsoft.com/security/blog/2017/07/18/windows-defender-antivirus-cloud-protection-service-advanced-real-time-defense-against-never-before-seen-malware)

Note

The Microsoft Defender Antivirus cloud service is a mechanism for delivering updated protection to your network and endpoints. As a cloud service, it is not simply protection for files stored in the cloud; instead, the cloud service uses distributed resources and machine learning to deliver protection to your endpoints at a rate that is far faster than traditional security intelligence updates.

## How to get cloud protection

Cloud protection is enabled by default. However, you might need to re-enable it if it has been disabled as part of previous organizational policies. To learn more, see [Turn on cloud protection](cloud-protection-configure).

If your subscription includes Windows 10 E5, you can take advantage of emergency dynamic intelligence updates, which provide near real-time protection from emerging threats. When you turn on cloud protection, fixes for malware issues can be delivered via the cloud within minutes, instead of waiting for the next update. See [Configure Microsoft Defender Antivirus to automatically receive new protection updates based on reports from our cloud service](manage-event-based-updates-microsoft-defender-antivirus#cloud-report-updates).