---
layout: Conceptual
title: Azure portal vs Defender portal feature comparison - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/azure-portal-vs-defender-portal-comparison
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Compare Microsoft Defender for Cloud features and capabilities between the Azure portal and Defender portal experiences to understand the enhanced functionality available in each platform.
ms.topic: article
ms.date: 2026-03-29T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: e69c729e-c7f4-30e1-a1f9-c785b703a4e8
document_version_independent_id: 5a0aa775-6160-6b25-b1b1-7f8c6a258142
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/azure-portal-vs-defender-portal-comparison.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/azure-portal-vs-defender-portal-comparison
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/azure-portal-vs-defender-portal-comparison.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 323c969b-ccd4-c049-79c2-1826ec8d5dc0
---

# Azure portal vs Defender portal feature comparison - Microsoft Defender for Cloud | Microsoft Learn

Important

Microsoft Defender for Cloud is expanding to the Defender portal to provide a unified security experience across cloud and code environments. As part of this expansion, some features are now available in the Microsoft Defender Portal, and additional capabilities will be added to the Defender portal over time.

This change is designed to:

- Unlock new cloud and posture management experiences.
- Provide deep integration with other Microsoft security services.
- Empower security teams with streamlined workflows by bringing all tools together in one portal.

To identify documentation specific for the Defender Portal, look for the portal entry point at the top of the article. This pivot indicates whether the content applies to the Defender portal or the Azure portal.

Our documentation will be continuously updated to reflect these changes, so check back regularly for the latest guidance and feature availability.

This article provides a comprehensive comparison of Microsoft Defender for Cloud features and capabilities between the Azure portal and Defender portal experiences. Understanding these differences helps you choose the right experience for your security operations and take advantage of enhanced capabilities available in the Defender portal.

## Feature comparison matrix

| Feature name | Azure portal | Defender portal |
| --- | --- | --- |
| **Security recommendations** | Yes | Yes - Integrated into Exposure Management**Note**: In the Defender portal, some recommendations that previously appeared as a single aggregated item now display as multiple individual recommendations. |
| **Asset inventory** | Yes**Note**: Only assets that have security issues detected on them are reflected. | Yes**Note**: All discovered resources in customers' environments are reflected, even if there are no security issues detected on them. |
| **Secure score** | Yes | Yes - New risk-based secure score |
| **Data visualization and reporting with Azure Workbooks** | Yes | No |
| **Data exporting** | Yes | No |
| **Workflow automation** | Yes | No |
| **Tools for remediation (quick fixes)** | Yes | No |
| **Microsoft Cloud Security Benchmark** | Yes | Partial - Security recommendations appear but security policies management is only in Azure. You can see the results in the Defender portal. |
| **AI security posture management** | Yes | Yes |
| **Agentless VM vulnerability scanning** | Yes | Yes |
| **Agentless VM secrets scanning** | Yes | Yes |
| **Attack path analysis** | Yes | Yes - Integrated into Attack Paths experience in Exposure Management |
| **Risk prioritization** | Yes | Yes |
| **Risk hunting with security explorer** | Yes | No |
| **Code-to-cloud mapping for containers** | Yes | Yes |
| **Code-to-cloud mapping for IaC** | Yes | Yes |
| **PR annotations** | Yes | No |
| **Internet exposure analysis** | Yes | Yes |
| **External attack surface management** | Yes | Yes |
| **Regulatory compliance assessments** | Yes | Partial - Security recommendations appears but security policies management only in Azure |
| **ServiceNow Integration** | Yes | No |
| **Critical assets protection** | Yes | Yes |
| **Governance to drive remediation at scale** | Yes | No |
| **Data security posture management (DSPM)** | Yes | Yes |
| **Agentless discovery for Kubernetes** | Yes | Yes |
| **Custom Recommendations** | Yes | No |
| **Agentless code-to-cloud containers vulnerability assessment** | Yes | Yes |
| **API security posture management** | Yes | Yes |