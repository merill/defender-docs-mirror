---
layout: Conceptual
title: What's new in Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-iot/whats-new
breadcrumb_path: /defender-for-iot/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: This article describes new features available in Microsoft Defender for IoT in the Defender portal, including both OT and Enterprise IoT networks.
ms.topic: whats-new
ms.service: defender-for-iot
author: limwainstein
ms.author: lwainstein
ms.localizationpriority: medium
ms.date: 2025-01-08T00:00:00.0000000Z
ms.custom: enterprise-iot
locale: en-us
document_id: 60a68b9e-8202-d050-ca47-8b8db9f3e456
document_version_independent_id: 60a68b9e-8202-d050-ca47-8b8db9f3e456
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot/whats-new.md
site_name: Docs
depot_name: Learn.defender-for-iot
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: whats-new
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot/whats-new.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: 873a8674-254a-e938-5fd8-f9550e4a9ec9
---

# What's new in Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn

This article describes features available in Microsoft Defender for IoT in the Defender portal, across both OT and Enterprise IoT networks.

Important

This article discusses Microsoft Defender for IoT in the Defender portal (Preview).

Some features are not yet available in the Defender portal. If you're interested in these features, or you're an existing customer working on the Azure portal, see the [Defender for IoT on Azure documentation](/en-us/azure/defender-for-iot/organizations/overview).

Learn more about the [Defender for IoT management portals](/en-us/defender-for-iot/microsoft-defender-iot#what-are-the-different-management-portals-for-microsoft-defender-for-iot).

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## January 2025

| Service area | Updates |
| --- | --- |
| **OT networks** | - Preview and edit the devices list during the site set up process - Manually update the site association of a device |

### Preview and edit the devices list during the site set up process

Before completing the site association process, preview the list of devices you have chosen to associate with the site, and remove any devices that aren't to be included in this site. For more information, see [preview devices](set-up-sites#preview-devices).

### Manually update the site association of a device

Manually assign or modify the site location for a specific device or set of devices. For more information, see [manually update device site association](manage-sites#manually-update-device-site-association).

## December 2024

| Service area | Updates |
| --- | --- |
| **Site security** | - Site association search in Site security page now supports various device types |

### Site association search in Site security page now supports various device types

To support searching across all relevant sites and device types, the **Site security** &gt; **Associate devices** page now supports searching for various device types, including IT, enterprise IoT, and network devices.

The suggested sites list now shows all relevant sites that match the search criteria across all device types. When you expand each site, you can view all relevant devices under the site, including the device name and type.

[![Screenshot showing the associate devices screen and the suggested list of OT devices per location with the Group column in the site set-up page of Microsoft Defender for IoT in the Microsoft Defender portal.](media/set-up-sites/site-security-associate-group.png)](media/set-up-sites/site-security-associate-group.png#lightbox)

For more information, see [Associate devices](set-up-sites#associate-devices).

## November 2024

| Service area | Updates |
| --- | --- |
| **Devices** | - Secure site-linked devices in Microsoft Security Exposure Management Initiatives page |

### Secure site-linked devices in Microsoft Security Exposure Management Initiatives page

You can now review the new **OT Security** initiative in the Microsoft Security Exposure Management **Initiatives** page. This new initiative provides a metric-driven way of tracking exposure about unmanaged OT devices.

[![Screenshot showing the OT Security initiative in Microsoft Defender for IoT in the Microsoft Defender portal.](media/review-security-initiatives/ot-security-initiative.png)](media/review-security-initiatives/ot-security-initiative.png#lightbox)

This new initiative serves as a powerful tool to improve your OT site security posture. The initiative aims to monitor and safeguard OT environments within the organization by employing network layer monitoring. This initiative identifies devices and ensures that systems are working correctly, and data is protected.

For more information, see:

- [Review security initiatives](review-security-initiatives)
- [Microsoft Security Exposure Management release notes](/en-us/security-exposure-management/whats-new#ot-security-initiative).

## September 2024

| Service area | Updates |
| --- | --- |
| **Devices** | - Review unmanaged enterprise IoT devices in Microsoft Security Exposure Management Initiatives page- New Building Management Systems (BMS) device category |

### Review unmanaged enterprise IoT devices in Microsoft Security Exposure Management Initiatives page

You can now review the new **Enterprise IoT Security** initiative in the Microsoft Security Exposure Management **Initiatives** page. This new initiative provides a metric-driven way of tracking exposure about unmanaged enterprise IoT devices.

For more information, see the [Microsoft Security Exposure Management release notes](/en-us/security-exposure-management/whats-new#new-enterprise-iot-security-initiative).

### New Building Management Systems (BMS) device category

We now support the new BMS device category in Defender for IoT that improves BMS device discovery and security. The BMS category includes a subset of Smart Facility and Surveillance devices (previously under the IoT category) such as fire alarms, humidity sensors, security radars, etc. Camera devices remain under the IoT category.

For more information, see [overview of device discovery](device-discovery).

## July 2024

| Service area | Updates |
| --- | --- |
| **Threat investigation** | - Site property added DeviceInfo schema |

### New Site property added DeviceInfo schema

In the advanced hunting tables, the **Site** property is added to the **DeviceInfo** schema. For more information, see [investigate threats](investigate-threats#advanced-hunting).