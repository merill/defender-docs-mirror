---
layout: Conceptual
title: Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/microsoft-defender-endpoint
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn about Microsoft Defender for Endpoint, an enterprise endpoint security platform that helps defend against advanced persistent threats.
ms.service: defender-endpoint
author: paulinbar
ms.author: painbar
ms.localizationpriority: high
ms.collection:
- m365-security
- tier1
- essentials-overview
ms.custom: intro-overview
ms.topic: overview
ms.date: 2026-07-28T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 75f04c47-50c6-8c29-8f7c-5b97ffc15e3f
document_version_independent_id: 75f04c47-50c6-8c29-8f7c-5b97ffc15e3f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/microsoft-defender-endpoint.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: microsoft-defender-endpoint
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/microsoft-defender-endpoint.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 1f8b2085-27ce-d0e8-3f0d-593c0d2051ef
---

# Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Microsoft Defender for Endpoint is an enterprise endpoint security platform designed to help organizations prevent, detect, investigate, and respond to advanced threats on their endpoints. These endpoints include laptops, phones, tablets, PCs, access points, routers, and firewalls.

As the endpoint security pillar of [Microsoft Defender](/en-us/defender-xdr/), Defender for Endpoint feeds endpoint signals into the unified Defender portal. The portal correlates these signals with alerts from identity, email, and cloud workloads to form complete incident views. Your security team can trace an attack from a phishing email to a compromised endpoint to lateral movement - all in one place.

Defender for Endpoint also integrates with the broader Microsoft security ecosystem, including:

- [Intune](/en-us/intune/intune-service/)
- [Microsoft Defender for Cloud](/en-us/azure/defender-for-cloud/)
- [Microsoft Defender for Cloud Apps](/en-us/defender-cloud-apps/)
- [Microsoft Defender for Identity](/en-us/defender-for-identity/)
- [Microsoft Defender for Office 365](/en-us/defender-office-365/)
- [Microsoft Defender Vulnerability Management](/en-us/defender-vulnerability-management/defender-vulnerability-management)
- [Microsoft Sentinel](/en-us/azure/sentinel/)
- [Microsoft threat intelligence](threat-protection-integration)

## Operating systems

Microsoft Defender for Endpoint supports the following operating systems: Windows, macOS, Linux, Android, and iOS. For detailed information about capabilities on each platform, see the following articles.

- [Microsoft Defender for Endpoint on Windows](microsoft-defender-endpoint-windows)
- [Microsoft Defender for Endpoint on Linux](microsoft-defender-endpoint-linux)
- [Microsoft Defender for Endpoint on macOS](microsoft-defender-endpoint-mac)
- [Microsoft Defender for Endpoint on Android and iOS](mtd)

For detailed system requirements and supported versions, see [Minimum requirements for Microsoft Defender for Endpoint](minimum-requirements).

## Licensing

Defender for Endpoint is available with several licensing options, including Defender for Endpoint Plan 1, Plan 2, and Microsoft Defender for Business. Microsoft 365 E5 and Microsoft 365 E5 Security include Defender for Endpoint Plan 2. For licensing requirements, see [Minimum requirements for Microsoft Defender for Endpoint](/en-us/defender-endpoint/minimum-requirements#licensing-requirements). For full plan comparison and pricing, see [Microsoft Defender for Endpoint plans and pricing](https://www.microsoft.com/security/business/endpoint-security/microsoft-defender-endpoint#Licensing).

Tip

The more Microsoft Defender workloads you deploy (identity, email, cloud apps, and endpoints), the stronger your overall protection becomes. Each workload contributes signals that enrich detection, correlation, and automated response in the unified Defender portal.

### Server licensing and Defender for Servers

If you're using Defender for Endpoint on servers, you might be eligible for a discount if you're also using [Microsoft Defender for Servers](/en-us/azure/defender-for-cloud/defender-for-servers-overview). Learn about [licensing discounts available when you have both Defender for Endpoint and Defender for Servers](/en-us/azure/defender-for-cloud/faq-defender-for-servers#can-i-get-a-discount-if-i-already-have-a-microsoft-defender-for-endpoint-license-).

## Defender for Endpoint capabilities

Defender for Endpoint provides a comprehensive set of capabilities, including [endpoint detection and response](overview-endpoint-detection-response), [autonomous protection](/en-us/defender-xdr/automatic-attack-disruption) with [automatic attack disruption](/en-us/defender-xdr/automatic-attack-disruption) and [predictive shielding](/en-us/defender-xdr/shield-predict-threats), [next-generation protection](next-generation-protection) with ransomware prevention, [attack surface reduction](overview-attack-surface-reduction), [vulnerability management](/en-us/defender-vulnerability-management/defender-vulnerability-management), [Endpoint Attack Notifications](endpoint-attack-notifications), and [APIs](api/management-apis) for integration with your existing workflows.

For guidance on planning and rolling out Defender for Endpoint in your environment, see [Plan your Defender for Endpoint deployment](mde-planning-guide). Before you begin, review [Minimum requirements](minimum-requirements) to confirm your environment is ready. To learn about new and upcoming capabilities, see [What's new in Microsoft Defender for Endpoint](whats-new-in-microsoft-defender-endpoint). To turn on preview features in your environment, see [Preview features in Microsoft Defender XDR](/en-us/defender-xdr/preview).

For a step-by-step workflow for piloting and deploying Defender for Endpoint in a production environment, including onboarding endpoints and verifying pilot groups, see [Pilot and deploy Defender for Endpoint](/en-us/defender-xdr/pilot-deploy-defender-endpoint).

For platform-specific capabilities, see the [Windows](microsoft-defender-endpoint-windows), [Linux](microsoft-defender-endpoint-linux), [macOS](microsoft-defender-endpoint-mac), and [Android and iOS mobile threat defense](mtd) documentation.

### APIs and integrations

Use these capabilities to integrate Microsoft Defender for Endpoint with your existing security tools and workflows, and automate tasks by using APIs. [Management and automation APIs](api/management-apis) enable you to automate workflows and integrate Defender for Endpoint into your existing processes. You can also use [partner integrations](partner-integration) to connect with Microsoft and non-Microsoft security solutions.

## Privacy and compliance

Defender for Endpoint is built with privacy, data protection, and regulatory compliance as core principles. For details on how Defender for Endpoint collects, stores, and protects your data, see [Data storage and privacy](data-storage-privacy).

Defender for Endpoint supports a [Zero Trust](zero-trust-with-microsoft-defender-endpoint) security model, helping you verify identities and device health before granting access. To learn more about Microsoft's data handling practices and privacy commitments, visit the [Microsoft Trust Center](https://www.microsoft.com/trust-center/privacy) and [Privacy at Microsoft](https://privacy.microsoft.com/). For an overview of how Microsoft manages data privacy and protection in compliance with global standards, see [Privacy and data management](/en-us/compliance/assurance/assurance-privacy).