---
layout: Conceptual
title: HPE ProLiant DL20 Gen10 (NHP 2LFF) for OT monitoring in SMB deployments- Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/appliance-catalog/hpe-proliant-dl20-smb-legacy
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
description: Learn about the HPE ProLiant DL20 Gen10 appliance when used for OT monitoring with Microsoft Defender for IoT in SMB deployments.
ms.date: 2022-10-30T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: a3ca40ca-669c-b351-d75a-bb4de506931b
document_version_independent_id: adce83c1-86c6-4d4f-f874-bfb8975681c5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/appliance-catalog/hpe-proliant-dl20-smb-legacy.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/appliance-catalog/hpe-proliant-dl20-smb-legacy
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/appliance-catalog/hpe-proliant-dl20-smb-legacy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: e61a3c7f-6c55-3ba4-1a02-5f8d90b5fa51
---

# HPE ProLiant DL20 Gen10 (NHP 2LFF) for OT monitoring in SMB deployments- Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn

This article describes the **HPE ProLiant DL20 Gen10** appliance for OT sensors for monitoring production lines.

Note

Legacy appliances are certified but aren't currently offered as pre-configured appliances.

| Appliance characteristic | Details |
| --- | --- |
| **Hardware profile** | L500 |
| **Performance** | Max bandwidth: 200Mbps Max devices: 1,000 |
| **Physical specifications** | Mounting: 1UPorts: 4x RJ45 |
| **Status** | Supported, not available pre-configured |

The following image shows a sample of the HPE ProLiant DL20 Gen10 front panel:

![Photo of the HPE ProLiant DL20 Gen10 front panel.](../media/tutorial-install-components/hpe-proliant-dl20-front-panel-v2.png)

The following image shows a sample of the HPE ProLiant DL20 Gen10 back panel:

![Photo of the back panel of the HPE ProLiant DL20 Gen10.](../media/tutorial-install-components/hpe-proliant-dl20-back-panel-v2.png)

## Specifications

| Component | Technical specifications |
| --- | --- |
| Chassis | 1U rack server |
| Dimensions | 4.32 x 43.46 x 38.22 cm / 1.70 x 17.11 x 15.05 in |
| Weight | 7.88 kg / 17.37 lb |
| Processor | Intel Xeon E-2224  3.4 GHz 4C 71 W |
| Chipset | Intel C242 |
| Memory | One 8-GB Dual Rank x8 DDR4-2666 |
| Storage | Two 1-TB SATA 6G Midline 7.2 K SFF (2.5 in) – RAID 1 with Smart Array P208i-a |
| Network controller | On-board: Two 1 Gb |
| On-board | iLO Port Card 1 Gb |
| External | 1 x HPE Ethernet 1-Gb 4-port 366FLR Adapter |
| Management | HPE iLO Advanced |
| Device access | Front: One USB 3.0 1 x USB iLO Service Port Rear: Two USBs 3.0 |
| Internal | One USB 3.0 |
| Power | Hot Plug Power Supply 290 W |
| Rack support | HPE 1U Short Friction Rail Kit |

## HPE ProLiant DL20 Gen10 (NHP 2LFF) - Bill of materials

| PN | Description | Quantity |
| --- | --- | --- |
| P06961-B21 | HPE DL20 Gen10 NHP 2LFF CTO Server | 1 |
| P17102-L21 | HPE DL20 Gen10 E-2224 FIO Kit | 1 |
| 879505-B21 | HPE 8-GB 1Rx8 PC4-2666V-E Standard Kit | 1 |
| 801882-B21 | HPE 1-TB SATA 7.2 K LFF RW HDD | 2 |
| P06667-B21 | HPE DL20 Gen10 x8x16 FLOM Riser Kit | 1 |
| 665240-B21 | HPE Ethernet 1-Gb 4-port 366FLR Adapter | 1 |
| 869079-B21 | HPE Smart Array E208i-a SR G10 LH Controller | 1 |
| P21649-B21 | HPE DL20 Gen10 Plat 290 W FIO PSU Kit | 1 |
| P06683-B21 | HPE DL20 Gen10 M.2 SATA/LFF AROC Cable Kit | 1 |
| 512485-B21 | HPE iLO Adv 1-Server License 1 Year Support | 1 |
| 775612-B21 | HPE 1U Short Friction Rail Kit | 1 |

## HPE ProLiant DL20 Gen10 installation

This section describes how to install Defender for IoT software on the HPE ProLiant DL20 Gen10 appliance.

Installation includes:

- Enabling remote access and updating the default administrator password
- Configuring iLO port on network port 1
- Configuring BIOS and RAID settings
- Installing Defender for IoT software

Note

Installation procedures are only relevant if you need to re-install software on a pre-configured device, or if you buy your own hardware and configure the appliance yourself.

### Enable remote access and update the password

Use the following procedure to set up network options and update the default password.

**To enable and update the password**:

1. Connect a screen, and a keyboard to the HPE appliance, turn on the appliance, and press **F9**.

    ![Screenshot that shows the HPE ProLiant window.](../media/tutorial-install-components/hpe-proliant-screen-v2.png)
2. Go to **System Utilities** &gt; **System Configuration** &gt; **iLO 5 Configuration Utility** &gt; **Network Options**.

    ![Screenshot that shows the System Configuration window.](../media/tutorial-install-components/system-configuration-window-v2.png)

    1. Select **Shared Network Port-LOM** from the **Network Interface Adapter** field.
    2. Set **Enable DHCP** to **Off**.
    3. Enter the IP address, subnet mask, and gateway IP address.
3. Select **F10: Save**.
4. Select **Esc** to get back to the **iLO 5 Configuration Utility**, and then select **User Management**.
5. Select **Edit/Remove User**. The administrator is the only default user defined.
6. Change the default password and select **F10: Save**.

### Configure the HPE BIOS

This procedure describes how to update the HPE BIOS configuration for your OT deployment.

**To configure the HPE BIOS**:

1. Select **System Utilities** &gt; **System Configuration** &gt; **BIOS/Platform Configuration (RBSU)**.
2. In the **BIOS/Platform Configuration (RBSU)** form, select **Boot Options**.
3. Change **Boot Mode** to **Legacy BIOS Mode**, and then select **F10: Save**.
4. Select **Esc** twice to close the **System Configuration** form.
5. Select **Embedded RAID 1: HPE Smart Array P208i-a SR Gen 10** &gt; **Array Configuration** &gt; **Create Array**.
6. Select **Proceed to Next Form**.
7. In the **Set RAID Level** form, set the level to **RAID 5** for enterprise deployments and **RAID 1** for SMB deployments.
8. Select **Proceed to Next Form**.
9. In the **Logical Drive Label** form, enter **Logical Drive 1**.
10. Select **Submit Changes**.
11. In the **Submit** form, select **Back to Main Menu**.
12. Select **F10: Save** and then press **Esc** twice.
13. In the **System Utilities** window, select **One-Time Boot Menu**.
14. In the **One-Time Boot Menu** form, select **Legacy BIOS One-Time Boot Menu**.
15. The **Booting in Legacy** and **Boot Override** windows appear. Choose a boot override option; for example, to a CD-ROM, USB, HDD, or UEFI shell.

    ![Screenshot that shows the first Boot Override window.](../media/tutorial-install-components/boot-override-window-one-v2.png)

    ![Screenshot that shows the second Boot Override window.](../media/tutorial-install-components/boot-override-window-two-v2.png)

### Install Defender for IoT software on the HPE ProLiant DL20 Gen10

This procedure describes how to install Defender for IoT software on the HPE ProLiant DL20 Gen10.

The installation process takes about 20 minutes. After the installation, the system is restarted several times.

**To install Defender for IoT software**:

1. Connect the screen and keyboard to the appliance, and then connect to the CLI.
2. Connect an external CD or disk-on-key that contains the software you downloaded from the Azure portal.
3. Start the appliance.
4. Continue by installing your Defender for IoT software. For more information, see [Defender for IoT software installation](../how-to-install-software).