---
layout: Conceptual
title: Dell PowerEdge R340 XL for OT monitoring (legacy) - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/appliance-catalog/dell-poweredge-r340-xl-legacy
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
description: Learn about the Dell PowerEdge R340 XL appliance's legacy configuration when used for OT monitoring with Microsoft Defender for IoT in enterprise deployments.
ms.date: 2023-03-02T00:00:00.0000000Z
ms.topic: reference
ms.custom: sfi-image-nochange
locale: en-us
document_id: 3ac32c95-2aad-de45-001b-22511a151439
document_version_independent_id: b641f8b1-bf09-2ee9-a380-c69bb38010c9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/appliance-catalog/dell-poweredge-r340-xl-legacy.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/appliance-catalog/dell-poweredge-r340-xl-legacy
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/appliance-catalog/dell-poweredge-r340-xl-legacy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: b5622aed-dddc-6921-e049-0bf011e5a102
---

# Dell PowerEdge R340 XL for OT monitoring (legacy) - Microsoft Defender for IoT | Microsoft Learn

This article describes the Dell PowerEdge R340 XL appliance, supported for OT sensors.

Note

Legacy appliances are certified but aren't currently offered as pre-configured appliances.

| Appliance characteristic | Description |
| --- | --- |
| **Hardware profile** | E1800 |
| **Performance** | Max bandwidth: 1 GbpsMax devices: 10,000 |
| **Physical Specifications** | Mounting: 1UPorts: 8x RJ45 or 6x SFP (OPT) |
| **Status** | Supported, not available as a preconfigured appliance |

The following image shows a view of the Dell PowerEdge R340 front panel:

![Photo of the Dell PowerEdge R340 front panel.](../media/tutorial-install-components/view-of-dell-poweredge-r340-front-panel.jpg)

In this image, numbers refer to the following components:

1. Left control panel
2. Optical drive (optional)
3. Right control panel
4. Information tag
5. Drives

The following image shows a view of the Dell PowerEdge R340 back panel:

![Photo of the Dell PowerEdge R340 back panel.](../media/tutorial-install-components/view-of-dell-poweredge-r340-back-panel.jpg)

In this image, numbers refer to the following components:

1. Serial port
2. NIC port (Gb 1)
3. NIC port (Gb 1)
4. Half-height PCIe
5. Full-height PCIe expansion card slot
6. Power supply unit 1
7. Power supply unit 2
8. System identification
9. System status indicator cable port (CMA) button
10. USB 3.0 port (2)
11. iDRAC9 dedicated network port
12. VGA port

## Specifications

| Component | Technical specifications |
| --- | --- |
| Chassis | 1U rack server |
| Dimensions | 42.8 x 434.0 x 596 (mm) /1.67” x 17.09” x 23.5” (in) |
| Weight | Max 29.98 lb/13.6 Kg |
| Processor | Intel Xeon E-2144G 3.6 GHz 8M cache  4C/8T  turbo (71 W |
| Chipset | Intel C246 |
| Memory | 32 GB = Two 16 GB 2666MT/s DDR4 ECC UDIMM |
| Storage | Three 2 TB 7.2 K RPM SATA 6 Gbps 512n 3.5in Hot-plug Hard Drive - RAID 5 |
| Network controller | On-board: Two 1 Gb Broadcom BCM5720 On-board LOM: iDRAC Port Card 1 Gb Broadcom BCM5720 External: One Intel Ethernet i350 QP 1 Gb Server Adapter Low Profile |
| Management | iDRAC nine Enterprise |
| Device access | Two rear USB 3.0 |
| One front | USB 3.0 |
| Power | Dual Hot Plug Power Supplies 350 W |
| Rack support | ReadyRails™ II sliding rails for tool-less mounting in four-post racks with square or unthreaded round holes. Or tooled mounting in four-post threaded hole racks with support for optional tool-less cable management arm. |

## Dell PowerEdgeR340XL installation

This section describes how to install Defender for IoT software on the Dell PowerEdgeR340XL appliance.

Before installing the software on the Dell appliance, you need to adjust the appliance's BIOS configuration.

Note

Installation procedures are only relevant if you need to re-install software on a preconfigured device, or if you buy your own hardware and configure the appliance yourself.

### Prerequisites

To install the Dell PowerEdge R340XL appliance, you need:

- An Enterprise license for Dell Remote Access Controller (iDRAC)
- A BIOS configuration XML
- One of the following server firmware versions:

    - BIOS version 2.1.6 or later
    - iDRAC version 3.23.23.23 or later

### Configure the Dell BIOS

An integrated iDRAC manages the Dell appliance with Lifecycle Controller (LC). The LC is embedded in every Dell PowerEdge server and provides functionality that helps you deploy, update, monitor, and maintain your Dell PowerEdge appliances.

To establish the communication between the Dell appliance and the management computer, you need to define the iDRAC IP address and the management computer's IP address on the same subnet.

When the connection is established, the BIOS is configurable.

**To configure the iDRAC IP address**:

1. Power up the sensor.
2. If the OS is already installed, select the F2 key to enter the BIOS configuration.
3. Select **iDRAC Settings**.
4. Select **Network**.

    Note

    During the installation, you must configure the default iDRAC IP address and password mentioned in the following steps. After the installation, you change these definitions.
5. Change the static IPv4 address to **10.100.100.250**.
6. Change the static subnet mask to **255.255.255.0**.

    ![Screenshot that shows the static subnet mask.](../media/tutorial-install-components/idrac-network-settings-screen-v2.png)
7. Select **Back** &gt; **Finish**.

**To configure the Dell BIOS**:

This procedure describes how to update the Dell PowerEdge R340 XL configuration for your OT deployment.

Configure the appliance BIOS only if you didn't purchase your appliance from Arrow or if you have an appliance, but don't have access to the XML configuration file.

1. Access the appliance's BIOS directly by using a keyboard and screen, or use iDRAC.

    - If the appliance isn't a Defender for IoT appliance, open a browser and go to the IP address configured beforehand. Sign in with the Dell default administrator privileges. Use **root** for the username and **calvin** for the password.
    - If the appliance is a Defender for IoT appliance, sign in by using **XXX** for the username and **XXX** for the password.
2. After you access the BIOS, go to **Device Settings**.
3. Choose the RAID-controlled configuration by selecting **Integrated RAID controller 1: Dell PERC&lt;PERC H330 Adapter&gt; Configuration Utility**.
4. Select **Configuration Management**.
5. Select **Create Virtual Disk**.
6. In the **Select RAID Level** field, select **RAID5**. In the **Virtual Disk Name** field, enter **ROOT** and select **Physical Disks**.
7. Select **Check All** and then select **Apply Changes**
8. Select **Ok**.
9. Scroll down and select **Create Virtual Disk**.
10. Select the **Confirm** check box and select **Yes**.
11. Select **OK**.
12. Return to the main screen and select **System BIOS**.
13. Select **Boot Settings**.
14. For the **Boot Mode** option, select **UEFI**.
15. Select **Back**, and then select **Finish** to exit the BIOS settings.

### Install Defender for IoT software on the Dell R340

This procedure describes how to install Defender for IoT software on the HPE DL360.

The installation process takes about 20 minutes. After the installation, the system restarts several times.

**To install the software**:

1. Verify that the version media is mounted to the appliance in one of the following ways:

    - Connect an external CD or disk-on-key that contains the sensor software you downloaded from the Azure portal.
    - Mount the ISO image by using iDRAC. After signing in to iDRAC, select the virtual console, and then select **Virtual Media**.
2. In the **Map CD/DVD** section, select **Choose File**.
3. Choose the version ISO image file for this version from the dialog box that opens.
4. Select the **Map Device** button.

    ![Screenshot that shows a mapped device.](../media/tutorial-install-components/mapped-device-on-virtual-media-screen-v2.png)
5. The media is mounted. Select **Close**.
6. Start the appliance. When you're using iDRAC, you can restart the servers by selecting the **Consul Control** button. Then, on the **Keyboard Macros**, select the **Apply** button, which will start the Ctrl+Alt+Delete sequence.
7. Continue by installing OT sensor or on-premises management software. For more information, see [Defender for IoT software installation](../how-to-install-software).