---
layout: Conceptual
title: What is Microsoft Defender for Business? - Microsoft Defender for Business | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-business/mdb-overview
breadcrumb_path: /defender-business/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Microsoft Defender for Business is a cybersecurity solution for small and medium sized businesses. Defender for Business protects against threats across your devices.
author: chrisda
ms.author: chrisda
ms.topic: overview
ms.service: defender-business
ms.localizationpriority: medium
ms.date: 2025-08-27T00:00:00.0000000Z
ms.reviewer: yaelbenari, efratka, nehabha
ms.collection:
- SMB
- m365-security
- m365-initiative-defender-business
- tier1
- essentials-overview
ms.custom: intro-overview
locale: en-us
document_id: 75049d1c-b8fd-f3aa-8bc0-710905e9bd25
document_version_independent_id: 75049d1c-b8fd-f3aa-8bc0-710905e9bd25
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-business/mdb-overview.md
site_name: Docs
depot_name: Learn.defender-business
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdb-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-business/mdb-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b11ae577-8d18-47ab-998c-ea182a941e71
- https://authoring-docs-microsoft.poolparty.biz/devrel/82f69bd7-5cb0-4163-9fd6-9103bb1a8352
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/87b1d24d-826d-4337-90a0-b6c35e4561f2
- https://authoring-docs-microsoft.poolparty.biz/devrel/f003597a-dab2-429a-8639-1d2acd9c0371
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: a317732f-11ef-596f-f1b6-623350d5a056
---

# What is Microsoft Defender for Business? - Microsoft Defender for Business | Microsoft Learn

Microsoft Defender for Business is an endpoint security solution based on [Microsoft Defender for Endpoint](/en-us/defender-endpoint/microsoft-defender-endpoint). Defender for Business is designed for small and medium sized business up to 300 users, and offers protection from ransomware, malware, phishing, and other threats on devices.

Defender for Business is available in the following subscriptions:

- **Standalone**: Available to non-Microsoft organizations or eligible Microsoft 365 or Office 365 organizations with up to 300 users. For example:
    - Microsoft 365 Business Basic
    - Microsoft 365 Business Standard
    - Office 365 E1
- **Microsoft 365 Business Premium**: [Business Premium](/en-us/microsoft-365/business-premium/m365bp-overview) includes Defender for Business.

Watch the following video to learn more about Defender for Business:

This article describes what's included in Defender for Business and provides links to learn more about these features and capabilities.

## What's included with Defender for Business?

Defender for Business includes a full range of device protection capabilities, as shown in the following diagram:

![Defender for Business features and capabilities.](media/mdb-offering-overview.png)

With Defender for Business, you can help protect the devices and data your business uses with:

- **Enterprise-grade security**: Defender for Business brings powerful endpoint security capabilities from our industry-leading [Microsoft Defender for Endpoint](/en-us/defender-endpoint/microsoft-defender-endpoint) solution and optimizes those capabilities for IT administrators to support small and medium sized businesses.
- **An easy-to-use security solution**: Defender for Business offers streamlined experiences that guide you to action with recommendations and insights into the security of your endpoints. No specialized knowledge is required, because Defender for Business offers wizard-driven configuration and default security policies that are designed to help protect your company's devices from day one.
- **Flexibility for your environment**: Defender for Business can work with your business environment, whether you're using Microsoft Intune or you're brand new to the Microsoft Cloud. Defender for Business works with components that are built into Windows, and with apps for Mac, iOS, and Android devices.
- **Integration with Microsoft 365 Lighthouse, RMM tools, and PSA software**:

    - Microsoft cloud solution providers (CSPs) using [Microsoft 365 Lighthouse](/en-us/microsoft-365/lighthouse/m365-lighthouse-overview) can view security incidents and alerts across customer organizations. For more information, see [Microsoft 365 Lighthouse and Defender for Business](mdb-lighthouse-integration)
    - Microsoft managed service providers (MSPs) can integrate Defender for Business with remote monitoring and management (RMM) tools and professional service automation (PSA) software. For more information, see [Defender for Business and MSP resources](mdb-partners).

## How does Defender for Business compare to Microsoft Defender for Endpoint?

Defender for Business includes the features of Defender for Endpoint Plan 1, some features from Defender for Endpoint Plan 2, and some unique features for small to medium sized businesses. The following table summarizes the differences between Defender for Business and Defender for Endpoint:

| Feature | Defender forBusiness | Defender forEndpoint Plan 1 | Defender forEndpoint Plan 2 |
| --- | --- | --- | --- |
| APIs | ✔ | ✔ | ✔ |
| Attack surface reduction | ✔ | ✔ | ✔ |
| Automated investigation and remediation | ✔ |  | ✔ |
| Automatic attack disruption | ✔ |  | ✔ |
| Centralized management | ✔ | ✔ | ✔ |
| Cross-platform support  (Mac, iOS/iPadOS, Android) | ✔ | ✔ | ✔ |
| Data retention: <br>- 30 days advanced hunting<br>Six months of data retention |  |  | ✔ |
| Endpoint detection & response (EDR) | ✔  (optimized) |  | ✔ |
| Microsoft 365 Lighthouse  (optimized; for CSPs only) | ✔ | ✔ | ✔ |
| Microsoft Defender multitenant management | ✔ | ✔ | ✔ |
| Microsoft Threat Experts |  |  | ✔ |
| Monthly security summary reporting | ✔ |  | ✔ |
| Next-generation protection | ✔ | ✔ | ✔ |
| Server support | ^\*^ | ^\*^ | ^\*^ |
| Simplified firewall and antivirus configuration for Windows | ✔ |  |  |
| Threat analytics | ✔  (optimized) |  | ✔ |
| Vulnerability management (core capabilities) | ✔ |  | ✔ |

^\*^ Protection for Windows servers and Linux servers is available, but requires extra licenses. For more information, see [Does Defender for Business support servers?](mdb-faq#does-defender-for-business-support-servers).

## How does Defender for Business compare to Microsoft 365 Business Premium?

Microsoft 365 Business Premium includes Defender for Business and provides more cybersecurity and productivity capabilities as showing in the following diagram.

![Diagram comparing Defender for Business to Microsoft 365 Business Premium.](media/mdb-m365bp-comparison.png)

For more detailed information about what's included in each subscription, see the following resources:

- [Microsoft 365 licensing guidance for security & compliance](/en-us/office365/servicedescriptions/microsoft-365-service-descriptions/microsoft-365-tenantlevel-services-licensing-guidance/microsoft-365-security-compliance-licensing-guidance)
- [Microsoft 365 Education](/en-us/office365/servicedescriptions/office-365-platform-service-description/microsoft-365-education)