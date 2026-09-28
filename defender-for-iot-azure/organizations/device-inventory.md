---
layout: Conceptual
title: Device inventory - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/device-inventory
breadcrumb_path: ../breadcrumb/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-iot-blog/bg-p/MicrosoftDefenderIoTBlog
feedback_help_link_type: ask-the-community
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
ms.service: defender-for-iot
author: limwainstein
manager: bagol
ms.author: lwainstein
description: Learn about the Defender for IoT device inventory features available from the Azure portal, and OT sensor console.
ms.date: 2023-02-19T00:00:00.0000000Z
ms.topic: concept-article
locale: en-us
document_id: a0fb36f7-3008-168d-abe5-7f6c404f2066
document_version_independent_id: 06644ddc-83b5-9448-60da-ed15224bd7e9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/device-inventory.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/device-inventory
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/device-inventory.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: d50beabe-85b1-74e8-0075-cd11b3d620eb
---

# Device inventory - Microsoft Defender for IoT | Microsoft Learn

Defender for IoT's device inventory helps you identify details about specific devices, such as manufacturer, type, serial number, firmware, and more. Gathering details about your devices helps your teams proactively investigate vulnerabilities that can compromise your most critical assets.

- **Manage all your IoT/OT devices** by building up-to-date inventory that includes all your managed and unmanaged devices
- **Protect devices with risk-based approach** to identify risks such as missing patches, vulnerabilities, and prioritize fixes based on risk scoring and automated threat modeling
- **Update your inventory** by deleting irrelevant devices and adding organization-specific information to emphasize your organization preferences

For example:

[![Screenshot of the Defender for IoT Device inventory page in the Azure portal.](media/device-inventory/azure-device-inventory.png)](media/device-inventory/azure-device-inventory.png#lightbox)

## Supported devices

Defender for IoT's device inventory supports the following device classes:

| Devices | For example ... |
| --- | --- |
| **Manufacturing** | Industrial and operational devices, such as pneumatic devices, packaging systems, industrial packaging systems, industrial robots |
| **Building** | Access panels, surveillance devices, HVAC systems, elevators, smart lighting systems |
| **Health care** | Glucose meters, monitors |
| **Transportation / Utilities** | Turnstiles, people counters, motion sensors, fire and safety systems, intercoms |
| **Energy and resources** | DCS controllers, PLCs, historian devices, HMIs |
| **Endpoint devices** | Workstations, servers, or mobile devices |
| **Enterprise** | Smart devices, printers, communication devices, or audio/video devices |
| **Retail** | Barcode scanners, humidity sensor, punch clocks |

A *transient* device type indicates a device that was detected for only a short time. We recommend investigating these devices carefully to understand their impact on your network.

*Unclassified* devices are devices that don't otherwise have an out-of-the-box category defined.

## Device management options

Defender for IoT device inventory is available in the following locations:

| Location | Description | Extra inventory support |
| --- | --- | --- |
| **Azure portal** | OT devices detected from all cloud-connected OT sensors. | - If you also use [Microsoft Sentinel](iot-solution), incidents in Microsoft Sentinel are linked to related devices in Defender for IoT. - Use Defender for IoT [workbooks](workbooks) for visibility into all cloud-connected device inventory, including related alerts and vulnerabilities. |
| **Microsoft Defender** | Enterprise IoT devices detected by Microsoft Defender for Endpoint agents | Correlate devices in Microsoft Defender in purpose-built alerts, vulnerabilities, and recommendations. |
| **OT network sensor consoles** | Devices detected by that OT sensor | - View all detected devices across a network device map- View related events on the **Event timeline** |

For more information, see:

- [Manage your device inventory from the Azure portal](how-to-manage-device-inventory-for-organizations)
- [Defender for Endpoint device discovery](/en-us/microsoft-365/security/defender-endpoint/device-discovery)
- [Manage your OT device inventory from a sensor console](how-to-investigate-sensor-detections-in-a-device-inventory)

## Automatically consolidated devices

When you deploy Defender for IoT at scale, with several OT sensors, each sensor might detect different aspects of the same device. To prevent duplicated devices in your device inventory, Defender for IoT assumes that any devices found in the same zone, with a logical combination of similar characteristics, is the same device. Defender for IoT automatically consolidates these devices and lists them only once in the device inventory.

For example, any devices with the same IP and MAC address detected in the same zone are consolidated and identified as a single device in the device inventory. If you have separate devices from recurring IP addresses that are detected by multiple sensors, you want each of these devices to be identified separately. In such cases, [onboard your OT sensors](onboard-sensors) to different zones so that each device is identified as a separate and unique device, even if they have the same IP address. Devices that have the same MAC addresses, but different IP addresses aren't merged, and continue to be listed as unique devices.

A *transient* device type indicates a device that was detected for only a short time. We recommend investigating these devices carefully to understand their impact on your network.

*Unclassified* devices are devices that don't otherwise have an out-of-the-box category defined.

Tip

Define [sites and zones](best-practices/plan-corporate-monitoring#plan-ot-sites-and-zones) in Defender for IoT to harden overall network security, follow principles of [Zero Trust](/en-us/security/zero-trust/), and gain clarity in the data detected by your sensors.

## Unauthorized devices

When you're first working with Defender for IoT, during the learning period just after deploying a sensor, all devices detected are identified as *authorized* devices.

After the learning period is over, any new devices detected are considered to be *unauthorized* and *new* devices. We recommend checking these devices carefully for risks and vulnerabilities. For example, in the Azure portal, filter the device inventory for `Authorization == **Unauthorized**`. On the device details page, drill down and check for related vulnerabilities, alerts, and recommendations.

The *new* status is removed as soon as you edit any of the device details or move the device on an OT sensor device map. In contrast, the *unauthorized* label remains until you manually edit the device details and mark it as *authorized*.

On an OT sensor, unauthorized devices are also included in the following reports:

- [Attack vector reports](how-to-create-attack-vector-reports): Devices marked as *unauthorized* are included in an attack vector simulation as suspected rogue devices that might be a threat to the network.
- [Risk assessment reports](how-to-create-risk-assessment-reports): Devices marked as *unauthorized* are listed in risk assessment reports as their risks to your network require investigation.

## Important OT devices

Mark OT devices as *important* to highlight them for extra tracking. On an OT sensor, important devices are included in the following reports:

- [Attack vector reports](how-to-create-attack-vector-reports): Devices marked as *important* are included in an attack vector simulation as possible attack targets.
- [Risk assessment reports](how-to-create-risk-assessment-reports): Devices marked as *important* are counted in risk assessment reports when calculating security scores.

## Device inventory column data

The following table lists the columns available in the Defender for IoT device inventory on the Azure portal and the OT sensor, a description of each column and whether and in which platform it is editable. Starred items **(\*)** are also available from the OT sensor.

Note

Noted features listed below are in PREVIEW. The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include other legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

| Name | Description | Editable |
| --- | --- | --- |
| **Authorization** \* | Determines whether or not the device is marked as *authorized*. This value might need to change as the device security changes. Toggle **Authorized device**. | Editable in Azure and OT Sensor |
| **Business Function** | Describes the device's business function. | Editable in Azure |
| **Class** | The device's class. Default: `IoT` | Editable in Azure |
| **Data source** | The source of the data, such as a micro agent, OT sensor, or Microsoft Defender for Endpoint. Default: `MicroAgent` | Not editable |
| **Description** \* | The device's description. | Editable in both Azure and the OT Sensor |
| **Device Id** | The device's Azure-assigned ID number. | Not editable |
| **Firmware model** | The device's firmware model. | Editable in Azure |
| **Firmware vendor** | The vendor of the device's firmware. | Not editable |
| **Firmware version** \* | The device's firmware version. | Editable in Azure |
| **First seen** \* | The date and time the device was first seen. Shown in `MM/DD/YYYY HH:MM:SS AM/PM` format. On the OT sensor, shown as **Discovered**. | Not editable |
| **Importance** | The device's important level: `Low`, `Medium`, or `High`. | Editable in Azure |
| **IPv4 Address** \* | The device's IPv4 address. | Not editable |
| **IPv6 Address** | The device's IPv6 address. | Not editable |
| **Last activity** \* | The date and time the device last sent an event through to Azure or to the OT sensor, depending on where you're viewing the device inventory. Shown in `MM/DD/YYYY HH:MM:SS AM/PM` format. | Not editable |
| **Location** | The device's physical location. | Editable in Azure |
| **MAC Address** \* | The device's MAC address. | Not editable |
| **Model** \* | The device's hardware model. | Editable in Azure |
| **Name** \* | Mandatory. The device's name as the sensor discovered it, or as entered by the user. | Editable in Azure and OT sensor |
| **Network location** (Public preview) \* | The device's network location. Displays whether the device is defined as *local* or *routed*, according to the configured subnets. | Not editable |
| **OS architecture** | The device's operating system architecture. | Not editable |
| **OS distribution** | The device's operating system distribution, such as Android, Linux, and Haiku. | Not editable |
| **OS platform** \* | The device's operating system, if detected. On the OT sensor, shown as **Operating System**. | Editable in OT Sensor |
| **OS version** | The device's operating system version, such as Windows 10 or Ubuntu 20.04.1. | Not editable |
| **PLC mode** \* | The device's PLC operating mode, including both the *Key* state (physical / logical) and the *Run* state (logical). If both states are the same, then only one state is listed.- Possible *Key* states include: `Run`, `Program`, `Remote`, `Stop`, `Invalid`, and `Programming Disabled`. - Possible *Run* states are `Run`, `Program`, `Stop`, `Paused`, `Exception`, `Halted`, `Trapped`, `Idle`, or `Offline`. | Editable in OT Sensor |
| **Programming device** \* | Defines whether the device is defined as a *Programming Device*, performing programming activities for PLCs, RTUs, and controllers, which are relevant to engineering stations. | Editable in Azure and OT sensor |
| **Protocols** \* | The protocols that the device uses. | Not editable |
| **Purdue level** | The Purdue level in which the device exists. | Editable in OT sensor |
| **Scanner device** \* | Defines whether the device performs scanning-like activities in the network. | Editable in OT Sensor |
| **Sensor** | The sensor the device is connected to. | Not editable |
| **Serial number** \* | The device's serial number. | Not editable |
| **Site** | The device's site. All Enterprise IoT sensors are automatically added to the **Enterprise network** site. | Not editable |
| **Slots** \* | The number of slots the device has. | Not editable |
| **Subtype** | The device's subtype, such as *Speaker* or *Smart TV*. **Default**: `Managed Device` | Editable in Azure |
| **Tags** | The device's tags. | Editable in Azure |
| **Type** \* | The device type, such as *Communication* or *Industrial*. **Default**: `Miscellaneous` | Editable in Azure and OT sensor |
| **Vendor** \* | The name of the device's hardware vendor, as defined in the MAC address. | Editable in Azure |
| **VLAN** \* | The device's VLAN. | Not editable |
| **Zone** | The device's zone. | Not editable |

The following columns are available in the OT sensors only, and aren't editable.

- The device's **DHCP Address**.
- The device's **FQDN** address and **FQDN Last Lookup Time**.
- The device **Groups** that include the device, as [defined on the OT sensor's device map](how-to-work-with-the-sensor-device-map#create-a-custom-device-group).
- The device's **Module address**.
- The device's **Rack**.
- The number of **Unacknowledged Alerts** alerts associated with the device.

Note

The additional **Agent type** and **Agent version** columns are used for by device builders. For more information, see [Microsoft Defender for IoT for device builders documentation](../device-builders/).