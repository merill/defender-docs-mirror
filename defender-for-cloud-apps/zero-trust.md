---
layout: Conceptual
title: Zero Trust and Microsoft Defender for Cloud Apps - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/zero-trust
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection:
- zerotrust-services
ms.service: defender-for-cloud-apps
ms.suite: ems
description: This article describes how Microsoft Defender for Cloud Apps fits into an overall Zero Trust security strategy when deployed with Microsoft Defender XDR.
ms.date: 2024-05-12T00:00:00.0000000Z
ms.topic: concept-article
locale: en-us
document_id: 8a49b94a-145f-c623-0ec5-0a612e4015de
document_version_independent_id: 8a49b94a-145f-c623-0ec5-0a612e4015de
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/zero-trust.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: zero-trust
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/zero-trust.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 2cde8c55-59f0-f16a-e256-770679f47523
---

# Zero Trust and Microsoft Defender for Cloud Apps - Microsoft Defender for Cloud Apps | Microsoft Learn

[Zero Trust](/en-us/security/zero-trust/zero-trust-overview) is a security strategy for designing and implementing the following sets of security principles:

| Verify explicitly | Use least privilege access | Assume breach |
| --- | --- | --- |
| Always authenticate and authorize based on all available data points. | Limit user access with Just-In-Time and Just-Enough-Access (JIT/JEA), risk-based adaptive policies, and data protection. | Minimize blast radius and segment access. Verify end-to-end encryption and use analytics to get visibility, drive threat detection, and improve defenses. |

Microsoft Defender for Cloud apps is a primary component of a Zero Trust strategy and your deployment with Microsoft Defender. Microsoft Defender for Cloud Apps gathers signals from your organization's use of cloud apps and protects data flowing between your environment and these apps, including both sanctioned and unsanctioned cloud apps. For example, Microsoft Defender for Cloud Apps notices anomalous behavior like impossible-travel, credential access, and unusual download, file share, or mail forwarding activity and reports these to the security team for mitigation.

## Monitoring for Zero Trust

When monitoring for Zero Trust, use Defender for Cloud Apps to [discover and secure](best-practices#discover-and-assess-cloud-apps) the SaaS apps being used in your organization and deploy policies that define how you want your users to behave in the cloud.

Respond to threats with Defender for Cloud Apps's user and entity behavioral analytics (UEBA) and anomaly detection, malware protection, OAuth app protection, incident investigation, and remediation. Monitor for [security anomaly alerts](investigate-anomaly-alerts), such as for impossible travel, suspicious inbox rules, and ransomware. Focus on identifying app usage patterns, assessing risk levels and business readiness of apps, preventing data leaks to noncompliant apps, and limiting access to regulated data.

Use Defender for Cloud Apps to inform Microsoft Entra ID about what happened to the user after they authenticated and received a token. If the user pattern starts to look suspicious, such as if a user starts to download gigabytes of data from OneDrive or starts to send spam emails in Exchange Online, notify Microsoft Entra ID that the user seems to be compromised or high risk. On the next access request from this user, Microsoft Entra ID can correctly take action to verify the user or block them.

### IaaS and PaaS security

Beyond SaaS applications, Defender for Cloud Apps helps you strengthen your security posture for IaaS and PaaS services by getting visibility into the security configuration and compliance status across your public cloud platforms. This enables a risk-based investigation of the entire platform configuration status. [Integrate Microsoft Purview with Defender for Cloud Apps](azip-integration#how-to-integrate-microsoft-purview-with-defender-for-cloud-apps) to label your apps and protect data across your apps, preventing inadvertent exposure to sensitive information.