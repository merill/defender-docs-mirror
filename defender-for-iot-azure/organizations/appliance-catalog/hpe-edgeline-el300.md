---
layout: Conceptual
title: HPE Edgeline EL300 (SMB) - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/appliance-catalog/hpe-edgeline-el300
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
description: Learn about the HPE Edgeline EL300 appliance for IoT in SMB rugged deployments.
ms.date: 2022-04-24T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: 31d17205-00e3-0f7f-490b-4bd298e5a150
document_version_independent_id: 96ccc3e8-3620-3214-4f52-e722652f4940
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/appliance-catalog/hpe-edgeline-el300.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/appliance-catalog/hpe-edgeline-el300
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/appliance-catalog/hpe-edgeline-el300.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
platformId: 79fd5cd7-920d-5316-aa71-f696839e625b
---

# HPE Edgeline EL300 (SMB) - Microsoft Defender for IoT | Microsoft Learn

This article describes the HPE Edgeline EL300 appliance for OT sensors.

Note

Legacy appliances are certified but aren't currently offered as pre-configured appliances.

| Appliance characteristic | Details |
| --- | --- |
| **Hardware profile** | L100 |
| **Performance** | Max bandwidth: 100 MbpsMax devices: 800 |
| **Physical specifications** | Mounting: Mounting kit, Din RailPorts: 5x RJ45 |
| **Status** | Supported, Not available pre-configured |

The following image shows a view of the back panel of the HPE Edgeline EL300.

![Photo of the back panel of the EL300](../media/tutorial-install-components/edgeline-el300-panel.png)

## Specifications

| Component | Technical specifications |
| --- | --- |
| Construction | Aluminum, fanless and dust-proof design |
| Dimensions (height x width x depth) | 200.5 mm (7.9”) tall, 232 mm (9.14”) wide by 100 mm (3.9”) deep |
| Weight | 4.91 KG (10.83 lbs.) |
| CPU | Intel Core i7-8650U (1.9GHz/4-core/15W) |
| Chipset | Intel® Q170 Platform Controller Hub |
| Memory | 8 GB DDR4 2133 MHz Wide Temperature SODIMM |
| Storage | 256-GB SATA 6G Read Intensive M.2 2242 3 year warranty wide temperature SSD |
| Network controller | 6x Gigabit Ethernet ports by Intel® I219 |
| Device access | 4 USBs: Two fronts; two rears; 1 internal |
| Power Adapter | 250V/10A |
| Mounting | Mounting kit, Din Rail |
| Operating Temperature | 0C to +70C |
| Humidity | 10%~90%, non-condensing |
| Vibration | 0.3 gram 10 Hz to 300 Hz, 15 minutes per axis - Din rail |
| Shock | 10G 10 ms, half-sine, three for each axis. (Both positive and negative pulse) – Din Rail |

### HPE Edgeline EL300 - Bill of materials

| Product | Description |
| --- | --- |
| P25828-B21 | HPE Edgeline EL300 v2 Converged Edge System |
| P25828-B21 B19 | HPE EL300 v2 Converged Edge System |
| P25833-B21 | Intel Core i7-8650U (1.9GHz/4-core/15W) FIO Basic Processor Kit for HPE Edgeline EL300 |
| P09176-B21 | HPE Edgeline 8 GB (1x8 GB) Dual Rank x8 DDR4-2666 SODIMM WT CAS-19-19-19 Registered Memory FIO Kit |
| P09188-B21 | HPE Edgeline 256-GB SATA 6G Read Intensive M.2 2242 3 year warranty wide temperature SSD |
| P04054-B21 | HPE Edgeline EL300 SFF to M.2 Enablement Kit |
| P08120-B21 | HPE Edgeline EL300 12VDC FIO Transfer Board |
| P08641-B21 | HPE Edgeline EL300 80W 12VDC Power Supply |
| AF564A | HPE C13 - SI-32 IL 250 V 10 Amp 1.83 m Power Cord |
| P25835-B21 | HPE EL300 v2 FIO Carrier Board |
| R1P49AAE | HPE EL300 iSM Adv 3 yr 24x7 Sup\_Upd E-LTU |
| P08018-B21 optional | HPE Edgeline EL300 Low Profile Bracket Kit |
| P08019-B21 optional | HPE Edgeline EL300 DIN Rail Mount Kit |
| P08020-B21 optional | HPE Edgeline EL300 Wall Mount Kit |
| P03456-B21 optional | HPE Edgeline 1-GbE 4-port TSN FIO Daughter Card |

## HPE EdgeLine 300 installation

This section describes how to install Defender for IoT software on the HPE EdgeLine 300 appliance.

Installation includes:

- Enabling remote access
- Configuring BIOS settings
- Installing Defender for IoT software

A default administrative user is provided. We recommend that you change the password during the network configuration.

Note

Installation procedures are only relevant if you need to re-install software on a preconfigured device, or if you buy your own hardware and configure the appliance yourself.

### Enable remote access

1. Enter the iSM IP Address into your web browser.
2. Sign in using the default username and password found on your appliance.
3. Navigate to **Wired and Wireless Network** &gt; **IPV4**

    ![Screenshot of the Wired and Wireless Network screen.](../media/tutorial-install-components/wired-and-wireless.png)
4. Toggle off the **DHCP** option.
5. Configure the IPv4 addresses as such:

    - **IPV4 Address**: `192.168.1.125`
    - **IPV4 Subnet Mask**: `255.255.255.0`
    - **IPV4 Gateway**: `192.168.1.1`
6. Select **Apply**.
7. Sign out and reboot the appliance.

### Configure the BIOS

This procedure describes how to update the HPE BIOS configuration for your OT deployment.

**To configure the BIOS**:

1. Turn on the appliance, and push **F9** to enter the BIOS.
2. Select **Advanced**, and scroll down to **CSM Support**.

    ![Screenshot showing the CSM Support menu.](../media/tutorial-install-components/csm-support.png)
3. Push **Enter** to enable CSM Support.
4. Go to **Storage**, and press **+/-** to change it to **Legacy**.
5. Go to **Video**, and press **+/-** to change it to **Legacy**.

    ![Screenshot showing the Storage and Video options](../media/tutorial-install-components/storage-and-video.png)
6. Go to **Boot** &gt; **Boot mode select**.
7. Press **+/-** to change it to **Legacy**.

    ![Screenshot of the Boot mode.](../media/tutorial-install-components/boot-mode.png)
8. Go to **Save & Exit**.
9. Select **Save Changes and Exit**.

    ![Screenshot of the Save Changes and Exit option.](../media/tutorial-install-components/save-and-exit.png)
10. Select **Yes**, and the appliance will reboot.
11. Press **F11** to enter the **Boot Menu**.
12. Select the device with the sensor image. Either **DVD** or **USB**.
13. Continue by installing your Defender for IoT software. For more information, see [Defender for IoT software installation](../how-to-install-software).