---
layout: Conceptual
title: Start your Defender for Identity deployment security assessment - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/security-assessment-deploy-defender-for-identity
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: Learn how the Start your Defender for Identity deployment assessment helps identify missing sensor installations on domain controllers and other eligible servers.
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: rlitinsky
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 73e1d68c-b3fb-128e-6b6e-26d40a4ba279
document_version_independent_id: 73e1d68c-b3fb-128e-6b6e-26d40a4ba279
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/security-assessment-deploy-defender-for-identity.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-assessment-deploy-defender-for-identity
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/security-assessment-deploy-defender-for-identity.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/37da4cc9-0cfc-42a9-ba5e-805706b01ef8
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3661fb96-d414-4a4e-b7ad-9370637790dd
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 99160197-8732-1b14-58e4-53e244625240
---

# Start your Defender for Identity deployment security assessment - Microsoft Defender for Identity | Microsoft Learn

This article describes the **Start your Defender for Identity deployment** security assessment, which encourages you to install sensors on domain controllers and other eligible servers. This assessment identifies servers in your environment that lack a Defender for Identity sensor and helps you understand the security risks of incomplete deployment. Use this guide to review the assessment findings in Microsoft Secure Score and take action to deploy sensors across your infrastructure.

## Why is not having Defender for Identity deployed considered a risk?

If you've obtained a Defender for Identity license, but haven't yet deployed Defender for Identity sensors, not only are you not yet using your purchased services, but you may be missing advanced threats in your identity infrastructure.

Defender for Identity uses your on-premises Active Directory signals to identify, detect, and investigate advanced threats, compromised identities, and malicious insider actions directed at your organization.

Defender for Identity is also part of monitoring for Zero Trust. You may also want to use [advanced hunting queries in Microsoft Defender](/en-us/microsoft-365/security/defender/advanced-hunting-overview) to look for threats in identities, devices, and cloud apps.

For more information, see:

- [What is Microsoft Defender for Identity?](what-is)
- [Zero Trust with Defender for Identity](zero-trust)

## How do I use this security assessment?

Use the following steps to review this assessment and remediate it.

1. Review the recommended action at https://security.microsoft.com/securescore?viewid=actions to be alerted if you have a Defender for Identity license, but don't have Defender for Identity deployed.
2. Take appropriate action by deploying Defender for Identity. For more information, see [Deploy Microsoft Defender for Identity with Microsoft Defender XDR](deploy-defender-identity).

Note

While assessments are updated in near real time, scores and statuses are updated every 24 hours. While the list of impacted entities is updated within a few minutes of your implementing the recommendations, the status may still take time until it's marked as **Completed**.