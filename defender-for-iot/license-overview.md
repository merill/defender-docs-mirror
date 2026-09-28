---
layout: Conceptual
title: Overview of the permanent site license and how to choose one for Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-iot/license-overview
breadcrumb_path: /defender-for-iot/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn about a permanent site license, how to upgrade and the different options available for Microsoft Defender for IoT in the Defender portal.
ms.service: defender-for-iot
author: limwainstein
ms.author: lwainstein
ms.localizationpriority: medium
ms.date: 2024-08-01T00:00:00.0000000Z
ms.topic: overview
locale: en-us
document_id: 147ff80f-c1b1-702a-6237-f983e65ba3bf
document_version_independent_id: 147ff80f-c1b1-702a-6237-f983e65ba3bf
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot/license-overview.md
site_name: Docs
depot_name: Learn.defender-for-iot
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: license-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot/license-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 6ba0abb1-cf73-ec2a-1a92-9b957a9b54a7
---

# Overview of the permanent site license and how to choose one for Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn

Our site-based license model streamlines your licensing needs by covering entire sites instead of individual devices. With this model, you can purchase annual licenses for your operational sites where Operational Technology (OT) devices are deployed. This ensures comprehensive security coverage for all devices within each site.

Important

This article discusses Microsoft Defender for IoT in the Defender portal (Preview).

Some features are not yet available in the Defender portal. If you're interested in these features, or you're an existing customer working on the Azure portal, see the [Defender for IoT on Azure documentation](/en-us/azure/defender-for-iot/organizations/overview).

Learn more about the [Defender for IoT management portals](/en-us/defender-for-iot/microsoft-defender-iot#what-are-the-different-management-portals-for-microsoft-defender-for-iot).

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Sites in Defender for IoT

A site refers to a logical grouping of devices within your organization. It represents a specific physical location, such as a manufacturing facility, campus, office building, hospital, rig, or any other relevant site.

## OT site-based licenses

Licenses come in five different sizes, based on the number of devices at the site. The licenses range from the smallest tier that covers up to 100 devices per site, to the largest tier, which secures up to 5000 devices per site. For more information, see [license sizing details](https://www.microsoft.com/en-us/security/business/endpoint-security/microsoft-defender-iot-pricing#xfb84a030eec341cb84a6165f393e928a).

The size of a site is determined by the maximum number of devices per site. Billing is based on the license tier, regardless of the number of devices actually discovered.

## Adjust the number of devices for a site

Once a license is purchased, the number of devices can only be adjusted at the renewal period. During the annual license renewal, you can change to a different license tier for a site based on your updated discovered device count.

## Assess the number of devices at a site

There are two methods for assessing the number of devices at your site. You could either utilize your OT network monitoring tools to detect and count the devices per site, or use previous knowledge of the number of devices at the site and update the license during the annual license renewal if needed.

Note

The license should cover all types of devices identified on your site, including both OT and IT devices. This includes endpoints managed by Microsoft Defender for Endpoint.