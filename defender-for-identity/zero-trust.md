---
layout: Conceptual
title: Zero Trust with Microsoft Defender for Identity - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/zero-trust
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: zerotrust-services
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: Explains how Microsoft Defender for Identity fits into an overall Zero Trust strategy when deploying Microsoft Defender XDR.
ms.date: 2024-05-12T00:00:00.0000000Z
ms.topic: article
ms.reviewer: rlitinsky
locale: en-us
document_id: f0db8663-7086-6ae7-9535-6ca10a3eddc6
document_version_independent_id: f0db8663-7086-6ae7-9535-6ca10a3eddc6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/zero-trust.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: zero-trust
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/zero-trust.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 193431c9-8f36-6591-5cf5-4e68acfc2fde
---

# Zero Trust with Microsoft Defender for Identity - Microsoft Defender for Identity | Microsoft Learn

[Zero Trust](/en-us/security/zero-trust/zero-trust-overview) is a security strategy for designing and implementing the following sets of security principles:

| Verify explicitly | Use least privilege access | Assume breach |
| --- | --- | --- |
| Always authenticate and authorize based on all available data points. | Limit user access with Just-In-Time and Just-Enough-Access (JIT/JEA), risk-based adaptive policies, and data protection. | Minimize blast radius and segment access. Verify end-to-end encryption and use analytics to get visibility, drive threat detection, and improve defenses. |

Defender for Identity is a primary component of a Zero Trust strategy and your deployment with Microsoft Defender. Defender for Identity uses Active Directory signals to detect sudden account changes like privilege escalation or high-risk lateral movement, and reports on easily exploited identity issues like unconstrained Kerberos delegation, for correction by the security team.

## Monitoring for Zero Trust

When monitoring for Zero Trust, make sure review and mitigate open alerts from Defender for Identity together with your other security operations. You may also want to use [advanced hunting queries in Microsoft Defender](/en-us/microsoft-365/security/defender/advanced-hunting-overview) to look for threats in identities, devices, and cloud apps.

Tip

Ingest your alerts into [Microsoft Sentinel with Microsoft Defender](/en-us/azure/sentinel/microsoft-365-defender-sentinel-integration), a cloud-native, security information event management (SIEM) and security orchestration automated response (SOAR) solution to provide your Security Operations Center (SOC) with a single pane of glass for monitoring security events in your enterprise.