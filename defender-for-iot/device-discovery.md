---
layout: Conceptual
title: Device discovery for Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-iot/device-discovery
breadcrumb_path: /defender-for-iot/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: This article describes device discovery for Microsoft Defender for IoT in the Defender portal.
ms.service: defender-for-iot
author: limwainstein
ms.author: lwainstein
ms.localizationpriority: medium
ms.date: 2024-08-19T00:00:00.0000000Z
ms.topic: concept-article
locale: en-us
document_id: 3682890f-48ec-cfe0-7c73-976b7d83f0da
document_version_independent_id: 3682890f-48ec-cfe0-7c73-976b7d83f0da
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot/device-discovery.md
site_name: Docs
depot_name: Learn.defender-for-iot
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: device-discovery
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot/device-discovery.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 5bd576d9-47c0-e6d0-cb51-063a160608d1
---

# Device discovery for Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn

To protect your environment, you need to take inventory of the devices in your network. However, mapping these devices can often be expensive, challenging, and time-consuming.

Microsoft Defender for IoT in the Microsoft Defender portal integrates with [Microsoft Defender for Endpoint device discovery](/en-us/defender-endpoint/machines-view-overview#device-inventory-overview), allowing you to discover devices connected to your operational technologies (OT) network without using extra appliances or complex process changes. Defender for IoT uses onboarded endpoints to collect, probe, or scan your network to discover devices.

This article describes the benefits and capabilities of device discovery in Defender for IoT.

Learn how to [discover and manage your IoT/OT devices](manage-devices-inventory) in the device inventory.

Important

This article discusses Microsoft Defender for IoT in the Defender portal (Preview).

Some features are not yet available in the Defender portal. If you're interested in these features, or you're an existing customer working on the Azure portal, see the [Defender for IoT on Azure documentation](/en-us/azure/defender-for-iot/organizations/overview).

Learn more about the [Defender for IoT management portals](/en-us/defender-for-iot/microsoft-defender-iot#what-are-the-different-management-portals-for-microsoft-defender-for-iot).

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Device inventory: initial view

If you don't yet have a Defender for IoT license, the **Device inventory** page detects your OT devices and lists them with regular device data, but without security data. For example, the device name, IP, and category are visible, while the risk level isn't visible. The device inventory also displays a note at the top of the page that indicates the number of unprotected OT devices.

To enable protection and get the full security value for your OT devices, [onboard Defender for IoT](get-started) to get security value for your OT devices.

If you're seeing the message that indicates the number of unprotected OT devices, and you've already set up Defender for IoT, [set up a site](set-up-sites) and associate the relevant devices with it.

## Device inventory page

The **Device inventory** page helps you identify details about specific devices, such as manufacturer, type, serial number, firmware, and more. Using these details, you can track your devices, dive into device information, and identify potential threats or incompatibilities.

Learn how to [discover and manage your IoT/OT devices](manage-devices-inventory) in the device inventory.

Learn more about the [device inventory in Microsoft Defender for Endpoint](/en-us/defender-endpoint/machines-view-overview#device-inventory-overview).

## Device discovery capabilities

The key device discovery capabilities are:

| Capability | Description |
| --- | --- |
| OT device management | [Manage OT devices](manage-devices-inventory):- Build an up-to-date inventory that includes all your managed and unmanaged devices.- Discover your organization Building Management Systems (BMS) devices such as **Motion detector**, **Fire Alarm**, and **Elevators**.- Classify critical devices to ensure that the most important assets in your organization are protected.- Add organization-specific information to emphasize your organization preferences. |
| Device protection with risk-based approach | Identify risks such as missing patches, vulnerabilities and prioritize fixes based on risk scoring and automated threat modeling. |
| Device alignment with physical sites | Allows contextual security monitoring. Use the **Site** filter to manage each site separately. Learn more about [filters](/en-us/defender-endpoint/machines-view-overview#sort-and-filter-the-device-list). |
| Device groups | Allows different teams in your organization to monitor and manage relevant assets only. Learn more about [creating a device group](/en-us/defender-endpoint/machine-groups#create-a-device-group). |
| Device criticality | Reflects how critical a device is for your organization and allows you to identify a device as a business critical asset. Learn more about [device criticality](/en-us/defender-endpoint/machines-view-overview#device-inventory-overview). |

## Supported devices

Defender for IoT's device inventory supports the following device categories:

| Devices | Example |
| --- | --- |
| **Manufacturing** | Industrial and operational devices, such as pneumatic devices, packaging systems, industrial packaging systems, industrial robots |
| **Building** | Access panels, surveillance devices, HVAC systems, elevators, smart lighting systems |
| **Health care** | Glucose meters, monitors |
| **Transportation / Utilities** | Turnstiles, people counters, motion sensors, fire and safety systems, intercoms |
| **Energy and resources** | DCS controllers, PLCs, historian devices, HMIs |
| **Retail** | Barcode scanners, humidity sensor, punch clocks |

For Enterprise device discovery information, see [Enterprise device discovery](/en-us/defender-for-iot/enterprise-iot).

For Endpoint device discovery information, see [Endpoint device discovery](/en-us/defender-endpoint/device-discovery).

### Identified, unique devices

Defender for IoT can discover all devices, of any type, across all environments. Devices are listed in the Defender for IoT **Device inventory** pages based on a unique IP and MAC address coupling.

Defender for IoT identifies single and unique devices as follows:

| Type | Description |
| --- | --- |
| **Identified as individual devices** | Devices identified as *individual* devices include:**OT or BMS unmanaged devices with one or more NICs**, including network infrastructure devices such as switches and routers**Note**: A device with modules or backplane components, such as racks or slots, is counted as a single device, including all modules or backplane components. |
| **Not identified as individual devices** | The following items *aren't* considered as individual devices, and don't count against your license:- **Public internet IP addresses**- **Multi-cast groups**- **Broadcast groups**- **Inactive devices** Network-monitored devices are marked as *inactive* when there's no network activity detected within a specified time: - **OT networks**: No network activity detected for more than 60 days**Note**: Endpoints already managed by Defender for Endpoint aren't considered as separate devices by Defender for IoT. |