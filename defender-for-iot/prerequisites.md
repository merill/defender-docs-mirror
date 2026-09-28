---
layout: Conceptual
title: Prerequisites for a license or setting up a site for Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-iot/prerequisites
breadcrumb_path: /defender-for-iot/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: This article describes the prerequisites for a license or setting up a site for Microsoft Defender for IoT in the Microsoft Defender portal.
ms.service: defender-for-iot
author: limwainstein
ms.author: lwainstein
ms.localizationpriority: medium
ms.date: 2024-05-19T00:00:00.0000000Z
ms.topic: get-started
locale: en-us
document_id: 67b2eb91-b9ed-2d59-e2b0-9e32e3afb934
document_version_independent_id: 67b2eb91-b9ed-2d59-e2b0-9e32e3afb934
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot/prerequisites.md
site_name: Docs
depot_name: Learn.defender-for-iot
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: prerequisites
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot/prerequisites.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: bc104533-f9ed-4e39-ced7-6d489dc4905d
---

# Prerequisites for a license or setting up a site for Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn

Microsoft Defender for IoT in the Microsoft Defender portal monitors and secures network traffic across your operational technology (OT) networks and allows you to analyze OT data, generate alerts, identify network risks, and more.

This article describes the prerequisites needed to set up a license for Microsoft Defender for IoT.

Important

This article discusses Microsoft Defender for IoT in the Defender portal (Preview).

Some features are not yet available in the Defender portal. If you're interested in these features, or you're an existing customer working on the Azure portal, see the [Defender for IoT on Azure documentation](/en-us/azure/defender-for-iot/organizations/overview).

Learn more about the [Defender for IoT management portals](/en-us/defender-for-iot/microsoft-defender-iot#what-are-the-different-management-portals-for-microsoft-defender-for-iot).

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Prerequisites for a license

Before you start, you need:

- A Microsoft tenant, with Global or Billing admin access to the tenant.

    For more information, see [Buy or remove licenses for a Microsoft business subscription](/en-us/microsoft-365/commerce/licenses/buy-licenses) and [About admin roles in the Microsoft 365 admin center](/en-us/microsoft-365/admin/add-users/about-admin-roles).
- A Microsoft 365 E5 or E5 security license or a Defender for Endpoint P2 license.
- Microsoft Defender for Endpoint agents deployed in your environment. For more information, see [onboard Microsoft Defender for Endpoint](/en-us/defender-endpoint/onboarding).

## Prerequisites for setting up a site

We recommend that you note the IP or MAC address details of at least one OT device listed in Defender for Endpoint. You'll need this information later when you [set up a site](set-up-sites).