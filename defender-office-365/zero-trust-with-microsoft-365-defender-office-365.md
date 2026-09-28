---
layout: Conceptual
title: Zero Trust with Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/zero-trust-with-microsoft-365-defender-office-365
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how Microsoft Defender for Office 365 supports Zero Trust principles for email and collaboration workloads, including threat protection capabilities and architecture considerations.
ms.service: microsoft-365-zero-trust
author: chrisda
ms.author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- zerotrust-services
- essentials-privacy
- essentials-security
- essentials-compliance
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
adobe-target: true
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: c06b0331-e0e8-a89a-229d-d9d341becdea
document_version_independent_id: c06b0331-e0e8-a89a-229d-d9d341becdea
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/zero-trust-with-microsoft-365-defender-office-365.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: zero-trust-with-microsoft-365-defender-office-365
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/zero-trust-with-microsoft-365-defender-office-365.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 0ddf6cc4-c58e-db31-05d2-71e579c36f8b
---

# Zero Trust with Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn

## How Microsoft Defender for Office 365 supports Zero Trust

Microsoft Defender for Office 365 is a cloud-based email filtering service that helps protect your organization against advanced threats to email and collaboration tools (for example, phishing, business email compromise, and malware attacks). Defender for Office 365 also provides investigation, Threat Hunting, and remediation capabilities to help security teams efficiently identify, prioritize, investigate, and respond to threats.

[Zero Trust](/en-us/security/zero-trust/zero-trust-overview) is a security strategy for designing and implementing the following set of security principles:

| Verify explicitly | Use least privilege access | Assume breach |
| --- | --- | --- |
| Always authenticate and authorize based on all available data points. | Limit user access with Just-In-Time and Just-Enough-Access (JIT/JEA), risk-based adaptive policies, and data protection. | Minimize blast radius and segment access. Verify end-to-end encryption and use analytics to get visibility, drive threat detection, and improve defenses. |

Defender for Office 365 is the primary component of the **Assume breach** principle and an important element of your extended detection and response (XDR) deployment with Microsoft Defender XDR. Defender for Office 365 consists of three levels of protection based on your subscription level:

| Protection level | Description |
| --- | --- |
| The built-in security features for all cloud mailboxes | Prevent broad, volume-based, known attacks. |
| Defender for Office 365 P1 | Protects email and collaboration from zero-day malware, phish, and business email compromise. |
| Defender for Office 365 P2 | Adds post-breach investigation, hunting, and response, as well as automation, and simulation (for training). |

## Threat protection capabilities that support Zero Trust

The Defender for Office 365 protection or filtering stack can be broken out into four phases:

1. **Edge protection**: Edge blocks are designed to be automatic. For false positives, senders are notified and told how to address their issue. Mail flow connectors that route messages from trusted partners with limited reputation can ensure deliverability, or temporary overrides can be put in place, when onboarding new endpoints.
2. **Sender intelligence**: Critical for catching spam, bulk, impersonation, and unauthorized spoof messages, and also factor into phish detection.
3. **Content filtering**: The filtering stack begins to handle the specific contents of the mail, including its hyperlinks and attachments.
4. **Post-delivery protection**: After mail or file delivery, acting on mail that is in various mailboxes and files and links that appear in clients like Microsoft Teams.

The Defender for Office 365 is also secure by default by quarantining email with suspected malware and using anti-spam policies to handle email with a high suspicion of phishing.