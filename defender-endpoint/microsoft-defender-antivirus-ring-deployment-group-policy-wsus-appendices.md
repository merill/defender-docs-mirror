---
layout: Conceptual
title: Microsoft Defender Antivirus ring deployment appendices for Group Policy and WSUS - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/microsoft-defender-antivirus-ring-deployment-group-policy-wsus-appendices
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Supplemental information about security intelligence, engine, and platform updates for Microsoft Defender Antivirus Group Policy and WSUS ring deployments.
ms.service: defender-endpoint
ms.author: chrisda
author: chrisda
ms.reviewer: yongrhee
ms.localizationpriority: high
ms.collection:
- m365-security
- tier1
- mde-ngp
ms.custom: intro-overview, msecd-doc-authoring-1012
ms.topic: concept-article
ms.subservice: ngp
ms.date: 2026-05-06T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: c00cd087-81cb-d923-fec0-104c0bba9248
document_version_independent_id: c00cd087-81cb-d923-fec0-104c0bba9248
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/microsoft-defender-antivirus-ring-deployment-group-policy-wsus-appendices.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: microsoft-defender-antivirus-ring-deployment-group-policy-wsus-appendices
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/microsoft-defender-antivirus-ring-deployment-group-policy-wsus-appendices.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
platformId: 26c13d04-f2b1-795b-c254-bbb76156ce7d
---

# Microsoft Defender Antivirus ring deployment appendices for Group Policy and WSUS - Microsoft Defender for Endpoint | Microsoft Learn

This article provides supplemental information about security intelligence updates, engine updates, and platform updates for the Microsoft Defender Antivirus ring deployment using Group Policy and Windows Server Update Services (WSUS).

## Prerequisites

### Supported operating systems

- Windows
- Windows Server

## Appendix A - Security Intelligence Updates

Microsoft continually updates security intelligence in antimalware products to cover the latest threats and to constantly tweak detection logic. The updates enhance the ability of Microsoft Defender Antivirus and other Microsoft antimalware solutions to accurately identify threats. This security intelligence works directly with cloud-based protection to deliver fast and powerful AI-enhanced, next-generation protection.

### References

- [Security intelligence updates for Microsoft Defender Antivirus and other Microsoft antimalware](https://www.microsoft.com/wdsi/defenderupdates)

## Appendix B - Engine Updates

Engine updates are updates for the scan engine that's used by security intelligence updates. The scan engine was first released on July 15, 2010.

## Appendix C - Platform Updates

Platform updates are the .exe, .dll, and .sys files for the Microsoft Defender Antivirus service.

| Channel | Version | Revision | Remarks |
| --- | --- | --- | --- |
| **Beta Channel - Prerelease** | 4.18.2304.4 | '23 April, minor rev 4 | This channel is the one you want to test for app compatibility, reliability, and performance. |
| **Current Channel (Preview)** | 4.18.2303.8 | '23 Mar, minor rev 8 | Same as for *Beta Channel - Prerelease*. |
| **Current Channel (Staged)** | 4.18.2303.7 | '23 Mar, minor rev 7 | Same as for *Beta Channel - Prerelease*. |
| **Current Channel (Broad)** | 4.18.2302.7  see note | '23 Feb, minor rev 7 | This channel is the one you want to push out to 90%-100% of your production systems. |

Note

Where **23** == *2023*, **02** == *February*, and **.7** is the *minor revision*.