---
layout: Conceptual
title: Monitor site security for Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-iot/monitor-site-security
breadcrumb_path: /defender-for-iot/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to monitor the site security for Microsoft Defender for IoT in the Microsoft Defender portal.
ms.service: defender-for-iot
author: limwainstein
ms.author: lwainstein
ms.localizationpriority: medium
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 12be47ca-8643-fe89-5a5d-3d7c764a818e
document_version_independent_id: 12be47ca-8643-fe89-5a5d-3d7c764a818e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot/monitor-site-security.md
site_name: Docs
depot_name: Learn.defender-for-iot
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: monitor-site-security
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot/monitor-site-security.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 1ea4d238-f7d6-7a76-f787-c67cba64920e
---

# Monitor site security for Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn

Microsoft Defender for IoT in the Microsoft Defender portal includes the **Site security** page, which offers an overview of the security state of your entire OT environment. Your organization's security team can use this page to regularly monitor the security status of your production sites.

In this article, you learn how to gain an overview of your site security, so your security team can decide how to prioritize and assign security issues.

Learn more about the [site security benefits and use cases](site-security-overview). Before you begin, review the prerequisites.

Important

This article discusses Microsoft Defender for IoT in the Defender portal (Preview).

Some features are not yet available in the Defender portal. If you're interested in these features, or you're an existing customer working on the Azure portal, see the [Defender for IoT on Azure documentation](/en-us/azure/defender-for-iot/organizations/overview).

Learn more about the [Defender for IoT management portals](/en-us/defender-for-iot/microsoft-defender-iot#what-are-the-different-management-portals-for-microsoft-defender-for-iot).

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Prerequisites

Before you review the **Site security** page, make sure you meet the following prerequisites:

- Review [the general prerequisites needed for Microsoft Defender for IoT](prerequisites).
- Review site security permissions according to RBAC requirements. For more information, see [RBAC permissions for Defender for IoT](set-up-rbac).

## Review the Site security page

The **Site security** page gives you an overview of the security status of your entire OT environment and is divided into two main sections:

- Review the top **How protected are your sites** section to get a general overview of your entire network, including sites with the highest number of devices that are exposed or at risk.
- Review the site list to monitor specific security information for each site.

[![Screenshot showing the site security page with a list of sites.](media/monitor-site-security/site-security-page-blurred.png)](media/monitor-site-security/site-security-page-blurred.png#lightbox)

The data displayed in the **Site security** page is the total aggregated data for the entire environment, and might include data for sites that you don't have access to. When you select a device count in the site list table, the **Device Inventory** page only displays data for devices you can access.

## Review site protection information

Review the top **How protected are your sites** section to get the following information:

| Section | Description | Next steps |
| --- | --- | --- |
| **Monitored OT sites** | The number of monitored sites. | Select **Get more sites** to add more sites. |
| **Total devices** | The number of total OT devices monitored across the entire network. | Select **View inventory** to access the Device inventory. |
| **Top vendors** | The number of OT devices in your network according to the vendor that produces them. | Select **View all** to view the devices and vendor information in the **Device Inventory** page. |
| **Top sites with high risk devices** | The number of high risk OT devices for the top three sites. The high-risk device count indicates devices that might have been breached (post-breach). | Select the site name to open the **Device Inventory** page filtered to show devices in this site. |
| **Top sites with high exposure devices** | The number of highly exposed OT devices for the top three sites. The high-exposure device count indicates devices vulnerable to a breach (pre-breach). | Select the site name to open the **Device Inventory** page filtered to show devices in this site. |

## Review the site list

Review the site specific data in the sites list table.

Note that the data displayed in the sites list table is the total aggregated data for the entire environment, and might include data for sites that you don't have access to. When you select a device count in the site list table, the **Device Inventory** page only displays data for devices you can access.

| Column | Description | Next steps |
| --- | --- | --- |
| **Site name** | The site name and description. | - Select the **Site name** to open the **Insights** panel. This panel displays site details, such as total devices, site location, and site owners. You can also select **Edit site** to make changes to the site.- Select the ellipsis (![](media/monitor-site-security/menu-ellipsis.png) ) to the right of the site name to [manage site settings](manage-sites). |
| **Critical devices** | The number of critical devices at this site. A critical device is a self assigned device that has extra importance to your business or system, such as a server that contains confidential data. | - Use the critical-device count to prioritize protection for sites with critical devices.- Select the number to open the **Device Inventory** page, filtered according to the site name and criticality level. |
| **Highly-exposed devices** | The number of highly exposed devices at this site. | Select the number to open the **Device Inventory** page, filtered according to the site name and high exposure level. |
| **Devices with high risk** | The number of high risk devices at this site. | Select the number to open the **Device Inventory** page, filtered according to the site name and high risk level. |

When you select an individual site, the site specific pane open, with details and data about that site, for example:

[![Screenshot showing the site security page with a list of sites and the site specific side pane open displaying details and data for that site.](media/monitor-site-security/site-security-side-pane.png)](media/monitor-site-security/site-security-side-pane.png#lightbox)