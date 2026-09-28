---
layout: Conceptual
title: Devices in multitenant management - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/mto-tenant-devices
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about multitenant device view in multitenant management of the Microsoft Defender XDR.
ms.service: defender-xdr
author: guywi-ms
ms.author: guywild
ms.collection:
- m365-security
- highpri
- tier1
ms.topic: article
ms.date: 2024-03-15T00:00:00.0000000Z
locale: en-us
document_id: 06258edf-2b1c-bdd6-96d0-1f77e4e42046
document_version_independent_id: 06258edf-2b1c-bdd6-96d0-1f77e4e42046
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/mto-tenant-devices.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mto-tenant-devices
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/mto-tenant-devices.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 8bbb6363-6e3d-44ff-baa3-a027ba5c7f3d
---

# Devices in multitenant management - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- [Microsoft Defender XDR](/en-us/defender-xdr/microsoft-365-defender)

The **Devices** page in multitenant management enables you to quickly manage tenants and devices.

## Tenant device list

The Tenants page in multitenant management lists each tenant you have access to. Each tenant page includes details such as the number of devices and device types, the number of high value and high exposure devices, and the number of devices available to onboard:

[![Screenshot of the Microsoft Defender XDR tenants list in the Devices page](media/mto-tenant-devices/devices-tenant-view.png)](media/mto-tenant-devices/devices-tenant-view.png#lightbox)

At the top of the page, you can view the number of tenants and the number of devices onboarded or discovered, across all tenants. You can also see the aggregate number of devices identified as:

- High risk
- High exposure
- Internet facing
- Can be onboarded
- Newly discovered
- High value

Select a tenant name to navigate to the device inventory for that tenant in the [Microsoft Defender XDR](https://security.microsoft.com/machines) portal where all data and inventory-related actions are available.

## Device inventory

The Device inventory page lists all the devices in each tenant that you have access to. The page is like the [Defender for Endpoint device inventory](/en-us/defender-endpoint/machines-view-overview) with the addition of the **Tenant name** column. Moreover, the device inventory page doesn't have the network, IOT, and uncategorized devices tabs.

You can navigate to the device inventory page by selecting **Assets &gt; Devices** in Microsoft Defender XDR's navigation menu.

[![Screenshot of the Microsoft Defender XDR Devices page for multitenant management](media/mto-tenant-devices/devices-device-inventory.png)](media/mto-tenant-devices/devices-device-inventory.png#lightbox)

The total number of devices, critical assets, high risk devices, and internet-facing devices for all tenants are shown at the top of the page.

You can search a specific device with the search function. You can sort and filter the device list according to the following fields to customize your view:

- Tenant name
- Risk level
- Criticality level
- Mitigation status
- Cloud platforms
- Operating system (OS) platforms
- Windows OS version
- Sensor health state
- Antivirus status
- Tags
- First seen
- Internet facing
- Group
- Exclusion state
- Managed by

To manage a device, select a specific device from the list. Device management tasks like managing tags, device exclusion, and reporting inaccuracy becomes available at the top of the device list.

[![Screenshot of choosing a device from the device inventory list](media/mto-tenant-devices/devices-choose-device.png)](media/mto-tenant-devices/devices-choose-device.png#lightbox)

Selecting a device by clicking on the device name opens the device page in a new tab. You can further apply other actions on the device in the new tab.