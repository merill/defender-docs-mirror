---
layout: Conceptual
title: Discover and manage devices in the device inventory for Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-iot/manage-devices-inventory
breadcrumb_path: /defender-for-iot/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use the device inventory in Microsoft Defender for IoT to find OT devices, filter and explore inventory data, investigate device details, and manage device site associations in the Defender portal.
ms.service: defender-for-iot
author: limwainstein
ms.author: lwainstein
ms.localizationpriority: medium
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: a2017b74-35e4-84ae-412a-8b2e8d6498c1
document_version_independent_id: a2017b74-35e4-84ae-412a-8b2e8d6498c1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot/manage-devices-inventory.md
site_name: Docs
depot_name: Learn.defender-for-iot
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: manage-devices-inventory
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot/manage-devices-inventory.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 1b079808-6018-8fde-5a49-85c2a7767abc
---

# Discover and manage devices in the device inventory for Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn

Microsoft Defender for IoT in the Microsoft Defender portal includes the device inventory, which helps you identify details about specific OT devices. Gathering details about your devices helps your teams proactively investigate vulnerabilities that can compromise your most critical assets. This article describes how to discover and manage your devices in the device inventory. You can filter data in the inventory, explore the inventory, investigate device details, and more. Before you start, review the prerequisites.

Learn more about the benefits of OT [device discovery](device-discovery).

Important

This article discusses Microsoft Defender for IoT in the Defender portal (Preview).

Some features are not yet available in the Defender portal. If you're interested in these features, or you're an existing customer working on the Azure portal, see the [Defender for IoT on Azure documentation](/en-us/azure/defender-for-iot/organizations/overview).

Learn more about the [Defender for IoT management portals](/en-us/defender-for-iot/microsoft-defender-iot#what-are-the-different-management-portals-for-microsoft-defender-for-iot).

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Access the Device inventory page

Access the **Device inventory** page by selecting **Devices** from the **Assets** navigation menu in the [Microsoft Defender portal](https://security.microsoft.com/machines).

## Prerequisites

Review the [Defender for IoT prerequisites](prerequisites).

Note

If you don't yet have a Defender for IoT license, the **Device inventory** page lists OT devices without security data. For example, the device name, IP, and category are visible, while the risk level isn't visible. The device inventory also displays a note at the top of the page that indicates the number of unprotected OT devices.

In this case, [onboard Defender for IoT](get-started) to get security value for your OT devices.

## View OT devices

View OT devices as part of the [device inventory](/en-us/defender-endpoint/machines-view-overview#device-inventory-overview).

To customize the device inventory views:

- [Use filters](/en-us/defender-endpoint/machines-view-overview#sort-and-filter-the-device-list)
- [Use columns](/en-us/defender-endpoint/machines-view-overview#use-columns-to-customize-the-device-inventory-views)

Note

Currently, devices discovered in the Defender portal aren't synchronized with the Azure portal, and therefore the list of devices discovered could be different in each portal.

### OT network tag

When a Defender for Endpoint agent is associated with a site, all devices discovered by that agent automatically receive the **Network type: OT** tag in the **Tags** column to show that these devices are part of the site. This tag helps users focus on devices that belong to their OT network.

## Manage OT devices

Use the following options to manage OT devices from the device inventory:

- [Explore the device inventory](/en-us/defender-endpoint/machines-view-overview#explore-the-device-inventory) including search, export to CSV, and more.
- [Onboard devices](/en-us/defender-endpoint/onboarding#onboard-devices-using-any-of-the-supported-management-tools).
- [Offboard devices](/en-us/defender-endpoint/offboard-machines).
- [Investigate the device details](/en-us/defender-endpoint/investigate-machines) to identify behaviors or events that might be related to a specific alert.
- In the device details pane, select the ellipsis on the top right to [take response actions on a device](/en-us/defender-endpoint/respond-machine-alerts).
- [Manually update the site associated with a device](manage-sites#manually-update-device-site-association) to maintain accurate monitoring of the network traffic.