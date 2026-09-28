---
layout: Conceptual
title: HPE ProLiant DL20 Gen10 Plus (NHP 2LFF) for OT monitoring in SMB/ L500 deployments - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/appliance-catalog/hpe-proliant-dl20-plus-smb
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
description: Learn about the HPE ProLiant DL20 Gen10 Plus appliance when used for OT monitoring with Microsoft Defender for IoT in SMB deployments.
ms.date: 2022-04-24T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: 94c2d822-d9c2-3244-dc07-e2691f9abecb
document_version_independent_id: 62c268af-dcc2-1014-a647-40ec30ccf9a2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/appliance-catalog/hpe-proliant-dl20-plus-smb.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/appliance-catalog/hpe-proliant-dl20-plus-smb
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/appliance-catalog/hpe-proliant-dl20-plus-smb.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/97159432-14a9-4307-a469-d2f2c75f0e33
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/50565c62-5f6b-4687-be38-323113c72c2e
platformId: e2a0c5b3-fb5a-2e83-57cf-d793ae5032f2
---

# HPE ProLiant DL20 Gen10 Plus (NHP 2LFF) for OT monitoring in SMB/ L500 deployments - Microsoft Defender for IoT | Microsoft Learn

This article describes the **HPE ProLiant DL20 Gen10 Plus** appliance for OT sensors monitoring production lines.

| Appliance characteristic | Details |
| --- | --- |
| **Hardware profile** | L500 |
| **Performance** | Max bandwidth: 200 Mbps Max devices: 1,000 Up to 8x Monitoring ports |
| **Physical specifications** | Mounting: 1UMinimum dimensions (H x W x D) 1.70 x 17.11 x 15.05 inMinimum dimensions (H x W x D) 4.32 x 43.46 x 38.22 cm |
| **Status** | Supported; available pre-configured |

The following image shows a sample of the HPE ProLiant DL20 Gen10 front panel:

![Photo of the HPE ProLiant DL20 Gen10 front panel.](../media/tutorial-install-components/hpe-proliant-dl20-front-panel-v2.png)

The following image shows a sample of the HPE ProLiant DL20 Gen10 back panel:

![Photo of the back panel of the HPE ProLiant DL20 Gen10.](../media/tutorial-install-components/hpe-proliant-dl20-back-panel-v2.png)

## Specifications

| Component | Technical specifications |
| --- | --- |
| Chassis | 1U rack server |
| Physical Characteristics | HPE DL20 Gen10+ NHP 2LFF CTO Server |
| Processor | Intel Xeon E-2334  3.4 GHz 4C 65 W |
| Chipset | Intel C256 |
| Memory | 1x 8-GB Dual Rank x8 DDR4-3200 |
| Storage | 1-TB SATA 6G Midline 7.2 K SFF |
| Network controller | On-board: 2x 1 Gb |
| External | 1 x HPE Ethernet 1-Gb 4-port 366FLR Adapter |
| On-board | iLO Port Card 1 Gb |
| Management | HPE iLO Advanced |
| Device access | Front: One USB 3.0 1 x USB iLO Service Port Rear: Two USBs 3.0 |
| Internal | One USB 3.0 |
| Power | Hot Plug Power Supply 290 W |
| Rack support | HPE 1U Short Friction Rail Kit |

## DL20 Gen10 Plus (NHP 2LFF) - Bill of materials

| Quantity | PN | Description |
| --- | --- | --- |
| 1 | P44111-B21 | HPE DL20 Gen10+ NHP 2LFF CTO Server |
| 1 | P45252-B21 | Intel Xeon E-2334 FIO CPU for HPE |
| 1 | P28610-B21 | HPE 1-TB SATA 7.2K SFF BC HDD |
| 1 | P43016-B21 | HPE 8 GB 1Rx8 PC4-3200AA-E Standard Kit |
| 1 | P21106-B21 | INT I350 1GbE 4p BASE-T Adapter |
| 1 | P45948-B21 | HPE DL20 Gen10+ RPS FIO Enable Kit |
| 1 | 865408-B21 | HPE 500W FS Plat Hot Plug LH Power Supply Kit |
| 1 | 775612-B21 | HPE 1U Short Friction Rail Kit |
| 1 | 512485-B21 | HPE iLO Adv 1 Server License 1 year support |
| 1 | P46114-B21 | HPE DL20 Gen10+ 2x8 LP FIO Riser Kit |

## Optional Storage Arrays

| Quantity | PN | Description |
| --- | --- | --- |
| 1 | P26325-B21 | Broadcom MegaRAID MR216i-a x16 Lanes without Cache NVMe/SAS 12G Controller (RAID5)**Note**: This RAID controller occupies the PCIe expansion slot and does not allow expansion of networking port expansion |

## Port expansion

Optional modules for port expansion include:

| Location | Type | Specifications |
| --- | --- | --- |
| PCI Slot 1 (Low profile) | DP F/O NIC | P26262-B21 - Broadcom BCM57414 Ethernet 10/25-Gb 2-port SFP28 Adapter for HPE |
| PCI Slot 1 (Low profile) | DP F/O NIC | P28787-B21 - Intel X710-DA2 Ethernet 10-Gb 2-port SFP+ Adapter for HPE |
| PCI Slot 2 (High profile) | Quad Port Ethernet NIC | P21106-B21 - Intel I350-T4 Ethernet 1-Gb 4-port BASE-T Adapter for HPE |
| PCI Slot 2 (High profile) | DP F/O NIC | P26262-B21 - Broadcom BCM57414 Ethernet 10/25 Gb 2-port SFP28 Adapter for HPE |
| PCI Slot 2 (High profile) | DP F/O NIC | P28787-B21 - Intel X710-DA2 Ethernet 10 Gb 2-port SFP+ Adapter for HPE |
| SFPs for Fiber Optic NICs | MultiMode, Short Range | 455883-B21 - HPE BLc 10G SFP+ SR Transceiver |
| SFPs for Fiber Optic NICs | SingleMode, Long Range | 455886-B21 - HPE BLc 10G SFP+ LR Transceiver |

## HPE ProLiant DL20 Gen10 Plus installation

This section describes how to install Defender for IoT software on the HPE ProLiant DL20 Gen10 Plus appliance.

Installation includes:

- Enabling remote access and updating the default administrator password
- Configuring iLO port on network port 1
- Configuring BIOS settings
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
3. Change **Boot Mode** to **UEFI BIOS Mode**, and then select **F10: Save**.
4. Select **Esc** twice to close the **System Configuration** form.
5. Select **Proceed to Next Form**.
6. In the **Logical Drive Label** form, enter **Logical Drive 1**.
7. Select **Submit Changes**.
8. In the **Submit** form, select **Back to Main Menu**.
9. Select **F10: Save** and then press **Esc** twice.
10. In the **System Utilities** window, select **One-Time Boot Menu**.
11. In the **One-Time Boot Menu** form, select **Legacy BIOS One-Time Boot Menu**.
12. The **Booting in Legacy** and **Boot Override** windows appear. Choose a boot override option; for example, to a CD-ROM, USB, HDD, or UEFI shell.

    ![Screenshot that shows the first Boot Override window.](../media/tutorial-install-components/boot-override-window-one-v2.png)

    ![Screenshot that shows the second Boot Override window.](../media/tutorial-install-components/boot-override-window-two-v2.png)

### Install iLO remotely from a virtual drive

This procedure describes how to install iLO software remotely from a virtual drive.

Before installing the iLO software, we recommend changing the iLO idle connection timeout setting to **infinite**, as the installation might take longer than the 30 minutes it is set to by default, depending on your network connection and if the sensor is in a remote location.

**To change the iLO idle connection timeout settings**:

1. Sign in to the iLO console, and go to **Overview** on the top menu.
2. On the left, select **Security**, and then select **Access settings** from the top menu.
3. Select the pencil icon next to **iLO** and then select **Show advanced settings**.
4. On the **Idle connection timeout** row, select the triangle icon to open the timeout options, and then select **Infinite**.

Continue the iLO installation with the following steps.

**To install sensor software with iLO**:

1. When signed into the iLO console, select the servers' screen on the bottom left.
2. Select **HTML5 Console**.
3. In the console, select the **Virtual media** CD icon on the right, and choose the CD/DVD option.
4. Select **Local ISO file**.
5. In the dialog box, choose the Defender for IoT sensor installation ISO file.
6. Go to the left menu icon, select **Power**, and then select **Reset**.
7. The appliance will restart, and run the sensor installation process.

### Install Defender for IoT software on the HPE ProLiant DL20 Gen10 Plus

This procedure describes how to install Defender for IoT software on the HPE ProLiant DL20 Gen10 Plus.

The installation process takes about 20 minutes. After the installation, the system is restarted several times.

**To install Defender for IoT software**:

1. Connect the screen and keyboard to the appliance, and then connect to the CLI.
2. Connect an external CD or disk-on-key that contains the software you downloaded from the Azure portal.
3. Start the appliance.
4. Continue by installing your Defender for IoT software. For more information, see [Defender for IoT software installation](../how-to-install-software).