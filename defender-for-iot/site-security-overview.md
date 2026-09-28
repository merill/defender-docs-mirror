---
layout: Conceptual
title: Site security features and capabilities in Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-iot/site-security-overview
breadcrumb_path: /defender-for-iot/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Read this article to learn about site security features, capabilities, scenarios and users of Microsoft Defender for IoT in the Defender portal.
ms.service: defender-for-iot
author: limwainstein
ms.author: lwainstein
ms.localizationpriority: medium
ms.date: 2024-06-26T00:00:00.0000000Z
ms.topic: article
locale: en-us
document_id: 3f611ed5-2806-8fbd-bc32-be2477f2fcb6
document_version_independent_id: 3f611ed5-2806-8fbd-bc32-be2477f2fcb6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot/site-security-overview.md
site_name: Docs
depot_name: Learn.defender-for-iot
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: site-security-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot/site-security-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 118c6550-8f1d-c96f-7f81-6cdfc660de59
---

# Site security features and capabilities in Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn

Microsoft Defender for IoT in the Microsoft Defender portal includes the **Site security** page, which offers an overview of the security state of your entire operational environment. The operational environment monitors all types of devices - operational technology (OT) devices and others.

In this article, you learn about the benefits and key scenarios of site security.

*Sites* represent a specific physical location in your organization. For example, a site can represent a manufacturing facility. Use a site based view of your organization to:

- Clearly differentiate security issues by location.
- Identify points with sufficient protection, or areas that need security improvements.

Important

This article discusses Microsoft Defender for IoT in the Defender portal (Preview).

Some features are not yet available in the Defender portal. If you're interested in these features, or you're an existing customer working on the Azure portal, see the [Defender for IoT on Azure documentation](/en-us/azure/defender-for-iot/organizations/overview).

Learn more about the [Defender for IoT management portals](/en-us/defender-for-iot/microsoft-defender-iot#what-are-the-different-management-portals-for-microsoft-defender-for-iot).

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Site security page

The **Site security** page gives the security team management tools to effectively understand and analyze the state of each site. Site security also provides a unified view of all operational sites across your entire organization. Your security team uses this data to make better informed decisions when dealing with security issues.

Learn more about how to use the [Site security page](monitor-site-security).

## Key capabilities

| Capability | Description |
| --- | --- |
| **[Visualize and manage your physical sites](set-up-sites)** | - Create and manage operational sites and devices with ease using automatic suggestions from your inventory.- Utilize the site creation wizard for seamless setup and to group devices by physical proximity for better organization. |
| **[Gain comprehensive insights and analytics](monitor-site-security)** | - Access a unified view of all operational sites, including security insights to understand their importance and prioritize responses.- Monitor site-specific discovery, posture, and threat detection to identify and address exposure, risks, and business impact. |
| **[Take Action to Reduce Risks](monitor-site-security)** | - Dive into dedicated site-based views for detailed insights on inventory, vulnerabilities, and incidents.- Leverage context-driven guidance within the Defender portal to effectively remediate risks and enhance site security. |
| **[Group, track, and manage OT devices](set-up-sites#associate-devices)** | Associate devices discovered by Microsoft Defender for Endpoint agents already installed on your network for a specific site using automatic site suggestions. This allows you to:- Proactively track and gain security insights for the site- Analyze the data for your network- Explore ways to mitigate and reduce risks |

## Key scenarios and users

The **Site security** page is designed to assist the following users:

- **Chief Security Information Officers (CISOs)** and **Security Decision Makers**: develop and improve the organization's overall security strategy giving insights into risk and exposure.
- **OT Security Manager**: develop and implement OT security initiatives across multiple sites or the entire organization.
- **Site Manager**: oversee daily operations at a specific site, ensuring smooth production and implementation of security measures.
- **OT Security Engineers**: design, implement, and maintain security solutions that are aligned with the security program of the site or with the overall organizational security.