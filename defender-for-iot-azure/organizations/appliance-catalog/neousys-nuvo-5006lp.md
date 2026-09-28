---
layout: Conceptual
title: Neousys Nuvo-5006LP (SMB) - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/appliance-catalog/neousys-nuvo-5006lp
breadcrumb_path: ../../breadcrumb/toc.json
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
description: Learn about the Neousys Nuvo-5006LP appliance for OT monitoring with Microsoft Defender for IoT.
ms.date: 2022-04-24T00:00:00.0000000Z
ms.topic: reference
ms.custom: sfi-image-nochange
locale: en-us
document_id: a593642e-72f5-53bc-dafc-de2840612bfc
document_version_independent_id: 83e8766d-1040-dd96-1e32-5dd706ac2e4b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/appliance-catalog/neousys-nuvo-5006lp.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/appliance-catalog/neousys-nuvo-5006lp
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/appliance-catalog/neousys-nuvo-5006lp.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 5c8117e3-9401-94fc-5f0a-eda5abcc9171
---

# Neousys Nuvo-5006LP (SMB) - Microsoft Defender for IoT | Microsoft Learn

This article describes the Neousys Nuvo-5006LP appliance for OT sensors.

Note

Neousys Nuvo-5006LP is a legacy appliance, and is supported for Defender for IoT software up to the latest patch for versions [22.2.x](../release-notes-ot-monitoring-sensor-archive#versions-222x). We recommend that you replace these appliances with newer certified models, such as the [YS-FIT2](ys-techsystems-ys-fit2) or [HPE DL20 (NHP 2LFF)](hpe-proliant-dl20-plus-smb).

| Appliance characteristic | Details |
| --- | --- |
| **Hardware profile** | L100 |
| **Performance** | Max bandwidth: 30 MbpsMax devices: 400 |
| **Physical specifications** | Mounting: Mounting kit, Din RailPorts: 5x RJ45 |
| **Status** | Supported up to the latest Defender for IoT software patch for versions [22.2.x](../release-notes-ot-monitoring-sensor-archive#versions-222x) |

![Photo of a Neousys Nuvo-5006LP.](../media/ot-system-requirements/cyberx.png)

The following image shows a view of the Nuvo 5006LP front panel:

![A photo of the front panel of the Nuvo 5006LP device.](../media/tutorial-install-components/nuvo5006lp_frontpanel.png)

In this image, numbers indicate the following components:

1. Power button, Power indicator
2. DVI video connectors
3. HDMI video connectors
4. VGA video connectors
5. Remote on/off Control, and status LED output
6. Reset button
7. Management network adapter
8. Ports to receive mirrored data

The following image shows a view of the Nuvo 5006LP back panel:

![A photo of the back panel of the Nuvo 5006lp.](../media/tutorial-install-components/nuvo5006lp_backpanel.png)

In this image, numbers indicate the following components:

1. SIM card slot
2. Microphone, and speakers
3. COM ports
4. USB connectors
5. DC power port (DC IN)

## Specifications

| Component | Technical Specifications |
| --- | --- |
| **Construction** | Aluminum, fanless and dust-proof design |
| **Dimensions** | 240 mm (W) x 225 mm (D) x 77 mm (H) |
| **Weight** | 3.1 kg (including CPU, memory, and HDD) |
| **CPU** | Intel Core i5-6500TE (6M Cache, up to 3.30 GHz) S1151 |
| **Chipset** | Intel® Q170 Platform Controller Hub |
| **Memory** | 8 GB DDR4 2133 MHz Wide Temperature SODIMM |
| **Storage** | 128 GB 3ME3 Wide Temperature mSATA SSD |
| **Network controller** | Six-Gigabit Ethernet ports by Intel® I219 |
| **Device access** | Four USBs: Two in front, two in the rear, and 1 internal |
| **Power Adapter** | 120/240VAC-20VDC/6A |
| **Mounting** | Mounting kit, Din Rail |
| **Operating Temperature** | -25°C - 70°C |
| **Storage Temperature** | -40°C ~ 85°C |
| **Humidity** | 10%~90%, non-condensing |
| **Vibration** | Operating, 5 Grms, 5-500 Hz, three Axes (w/ SSD, according to IEC60068-2-64) |
| **Shock** | Operating, 50 Grms, Half-sine 11 ms Duration (w/ SSD, according to IEC60068-2-27) |
| **EMC** | CE/FCC Class A, according to EN 55022, EN 55024 & EN 55032 |

## Nuvo 5006LP sensor installation

This section describes how to install OT sensor software on the Nuvo 5006LP appliance. Before installing the OT sensor software, you must adjust the appliance's BIOS configuration.

Note

Installation procedures are only relevant if you need to re-install software on a preconfigured device, or if you buy your own hardware and configure the appliance yourself.

### Prerequisites

Before installing OT sensor software, or updating the BIOS configuration, make sure that the operating system is installed on the appliance.

### Configure the Nuvo 5006LP BIOS

This procedure describes how to update the Nuvo 5006LP BIOS configuration for your OT sensor deployment.

**To configure the Nuvo 5006LP BIOS**:

1. Power on the appliance.
2. Press **F2** to enter the BIOS configuration.
3. Go to **Power** and change the **Power On after Power Failure** setting to **S0-Power On**.

    ![Screenshot of setting your Nuvo 5006 to power on after a power failure.](../media/tutorial-install-components/nuvo-power-on.png)
4. Go to **Boot** and ensure that **PXE Boot to LAN** is set to **Disabled**.
5. Press **F10** to save, and then select **Exit**.

### Install OT sensor software on the Nuvo 5006LP

This procedure describes how to install OT sensor software on the Nuvo 5006LP. The installation takes approximately 20 minutes. After the installation is complete, the system restarts several times.

**To install OT sensor software**:

1. Connect an external CD or disk-on-key that contains the sensor software you downloaded from the Azure portal.
2. Boot the appliance.
3. Select **English**.
4. Select **XSENSE-RELEASE-&lt;version&gt; Office...**.
5. Define the appliance architecture, and network properties as follows:

    | Parameter | Configuration |
    | --- | --- |
    | **Hardware profile** | Select **office**. |
    | **Management interface** | **eth0** |
    | **Management network IP address** | **IP address provided by the customer** |
    | **Management subnet mask** | **IP address provided by the customer** |
    | **DNS** | **IP address provided by the customer** |
    | **Default gateway IP address** | **0.0.0.0** |
    | **Input interface** | The list of input interfaces is generated for you by the system. To mirror the input interfaces, copy all the items presented in the list with a comma separator. |
    | **Bridge interface** | - |

    For example:

    ![Screenshot of the Nuvo's architecture and network properties.](../media/tutorial-install-components/nuvo-profile-appliance.png)
6. Accept the settings and continue by entering `Y`.

After approximately 10 minutes, sign-in credentials are automatically generated. Save the username and passwords; you'll need these credentials to access the platform the first time you use it.