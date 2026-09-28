---
layout: Conceptual
title: Microsoft Defender Antivirus ring deployment guide overview - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/microsoft-defender-antivirus-ring-deployment
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Microsoft Defender Antivirus is an enterprise endpoint security platform that helps defend against advanced persistent threats. This article provides an overview about how to use ring deployment methods to update your Microsoft Defender Antivirus clients.
ms.service: defender-endpoint
ms.author: chrisda
author: chrisda
ms.reviewer: yongrhee
ms.localizationpriority: high
ms.collection:
- m365-security
- tier1
- mde-ngp
ms.custom: intro-overview
ms.topic: concept-article
ms.subservice: ngp
ms.date: 2025-10-20T00:00:00.0000000Z
locale: en-us
document_id: 401d4eb0-e3bc-8090-6d83-f00d2ca48f7f
document_version_independent_id: 401d4eb0-e3bc-8090-6d83-f00d2ca48f7f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/microsoft-defender-antivirus-ring-deployment.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: microsoft-defender-antivirus-ring-deployment
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/microsoft-defender-antivirus-ring-deployment.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 62cf5f87-9f77-bf5a-2eb7-4ee75fbe5502
---

# Microsoft Defender Antivirus ring deployment guide overview - Microsoft Defender for Endpoint | Microsoft Learn

Microsoft Defender for Endpoint is an enterprise endpoint security platform designed to help enterprise networks prevent, detect, investigate, and respond to advanced threats.

Tip

Microsoft Defender for Endpoint is available in two plans, Defender for Endpoint Plan 1 and Plan 2. A new Microsoft Defender Vulnerability Management add-on is now available for Plan 2.

Deploying Microsoft Defender for Endpoint can be done using a ring-based deployment approach and updating using the gradual rollout process.

## Prerequisites

### Supported operating systems

- Windows
- Windows Server

## Ring deployment overview

It's important to ensure that client components are up to date to deliver critical protection capabilities and prevent attacks. Capabilities are provided through several components:

- [Endpoint Detection & Response](overview-endpoint-detection-response)
- [Next-generation protection](microsoft-defender-antivirus-windows) with [cloud-delivered protection](cloud-protection-microsoft-defender-antivirus)
- [Attack Surface Reduction](attack-surface-reduction-overview)

Updates are released monthly using a gradual release process. This process helps to enable early failure detection to identify problematic results in your unique environment as it occurs and address it quickly before a larger rollout.

Note

For more information on how to control daily security intelligence updates, see [Schedule Microsoft Defender Antivirus protection updates](manage-protection-update-schedule-microsoft-defender-antivirus). Updates ensure that next-generation protection can defend against new threats, even if cloud-delivered protection is not available to the endpoint.

This article provides overview information about deploying Microsoft Defender Antivirus in rings for a gradual rollout process.

## Management tools

To create your own custom gradual rollout process for daily and/or monthly updates, you can use the following methods that use the tools:

- **Microsoft Intune and Microsoft Update** microsoft-intune-and-microsoft-update - Requires direct access to the internet. Microsoft Update (MU), formerly known as Windows Update (WU)
- **System Center Configuration Manager and Windows Server Update Services** - System Center Configuration Manager (SCCM) Software Update Point (SUP) = SCCM + Windows Server Update Services (WSUS)
- **Group Policy and Microsoft Update** - Requires direct access to the internet
- **Group Policy and network share** - For example, UNC path, SMB, CIFS
- **Group Policy and WSUS**

For details on how to use these tools, see [Create a custom gradual rollout process for Microsoft Defender updates](configure-updates).

Customers that prioritize availability over security, should take a crawl, walk, run approach.

## Deployment scenarios

- [Ring deployment using Intune and Microsoft Update](microsoft-defender-antivirus-ring-deployment-intune-microsoft-update)
- [Ring deployment using System Center Configuration Manager and Windows Server Update Services (WSUS)](microsoft-defender-antivirus-ring-deployment-sscm-wsus)
- [Ring deployment using Group Policy and Microsoft Update](microsoft-defender-antivirus-ring-deployment-group-policy-microsoft-update)
- [Ring deployment using Group Policy and network share](microsoft-defender-antivirus-ring-deployment-group-policy-network-share)
- Ring deployment using Group Policy and Windows Server Update Services
    - [Pilot ring deployment using Group Policy and Windows Server Update Services](microsoft-defender-antivirus-pilot-ring-deployment-group-policy-wsus)
    - [Production ring deployment using Group Policy and Windows Server Update Services](microsoft-defender-antivirus-production-ring-deployment-group-policy-wsus)