---
layout: Conceptual
title: Install OT sensor software - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/ot-deploy/install-software-ot-sensor
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
description: Learn how to install agentless monitoring software on an OT sensor for Microsoft Defender for IoT, including initial setup settings.
ms.date: 2025-01-30T00:00:00.0000000Z
ms.topic: install-set-up-deploy
locale: en-us
document_id: 45d9875a-b6c8-e9d7-94c0-75a46a73dd8a
document_version_independent_id: 4254bded-ce87-667f-f3e0-04c6c32b4ba5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/ot-deploy/install-software-ot-sensor.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/ot-deploy/install-software-ot-sensor
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/ot-deploy/install-software-ot-sensor.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: f39b6484-9150-dabe-83e6-e0a8afde11d3
---

# Install OT sensor software - Microsoft Defender for IoT | Microsoft Learn

This article is one in a series of articles describing the [deployment path](ot-deploy-path) for OT monitoring with Microsoft Defender for IoT, and describes how to install Defender for IoT software on OT sensors and configure initial setup settings.

[![Diagram of a progress bar with Deploy your sensors highlighted.](../media/deployment-paths/progress-deploy-your-sensors.png)](../media/deployment-paths/progress-deploy-your-sensors.png#lightbox)

Use the procedures in this article when installing Microsoft Defender for IoT software on your own appliances. You might be reinstalling software on a [preconfigured appliance](../ot-pre-configured-appliances), or you may be installing software on your own appliance. If you're using a new preconfigured appliance, skip this step and continue directly with [configuring and activating your sensor](activate-deploy-sensor) instead.

Caution

Only documented configuration parameters on the OT network sensor are supported for customer configuration. Do not change any undocumented configuration parameters or system properties, as changes may cause unexpected behavior and system failures.

Removing packages from your sensor without Microsoft approval can cause unexpected results. All packages installed on the sensor are required for correct sensor functionality.

## Prerequisites

Before installing, configuring, and activating your OT sensor, make sure that you have:

- A [plan](../best-practices/plan-prepare-deploy) for your OT site deployment with Defender for IoT, including the appliance you're using for your OT sensor.
- Access to the Azure portal as a [Security Reader](/en-us/azure/role-based-access-control/built-in-roles#security-reader), [Security Admin](/en-us/azure/role-based-access-control/built-in-roles#security-admin), [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor), or [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) user.
- Performed extra procedures per appliance type. Each appliance type also comes with its own set of instructions that are required before installing Defender for IoT software.

    Make sure that you've completed any specific procedures required for your appliance before installing Defender for IoT software. If your appliance has a RAID storage array, make sure to configure it before you continue installation.

    For more information, see:

    - The [OT monitoring appliance catalog](../appliance-catalog/)
    - [Which appliances do I need?](../ot-appliance-sizing)
    - [OT monitoring with virtual appliances](../ot-virtual-appliances)
- Access to the physical or virtual appliance where you're installing your sensor. For more information, see [Which appliances do I need?](../ot-appliance-sizing)

This step is performed by your deployment teams.

Note

There is no need to pre-install an operating system on the VM. The sensor installation includes the operating system image.

### Configure network adapters for a VM deployment

Before deploying an OT sensor on a [virtual appliance](../ot-virtual-appliances), configure at least two network adapters on your VM: one to connect to the Azure portal, and another to connect to traffic mirroring ports.

**On your virtual machine**:

1. Open your VM settings for editing.
2. Together with the other hardware defined for your VM, such as memory, CPUs, and hard disk, add the following network adapters:

    - **Network adapter 1**, to connect to the Azure portal for cloud management.
    - **Network adapter 2**, to connect to a traffic mirroring port that's configured to allow promiscuous mode traffic. If you're connecting your sensor to multiple traffic mirroring ports, make sure there's a network adapter configured for each port.

For more information, see:

- Your virtual machine software documentation
- [OT network sensor VM (VMware ESXi)](../appliance-catalog/virtual-sensor-vmware)
- [OT network sensor VM (Microsoft Hyper-V)](../appliance-catalog/virtual-sensor-hyper-v)
- [Networking requirements](../networking-requirements)

## Download software files from the Azure portal

Download the OT sensor software from Defender for IoT in the Azure portal.

In Defender for IoT on the Azure portal, select **Getting started** &gt; **Sensor**, and then select the software version you want to download.

Important

If you're updating software from a previous version, use the options from the **Sites and sensors** &gt; **Sensor update** menu. For more information, see [Update Defender for IoT OT monitoring software](../update-ot-software).

## Install Defender or IoT software on OT sensors

This procedure describes how to install the Defender for IoT software you'd downloaded from the Azure portal.

Tip

While you can run this procedure and watch the installation from a deployment workstation, after you boot your sensor machine from the physical media or virtual mount, the installation can also run automatically on its own.

If you choose to do this without a keyboard or screen, note the default IP address listed at the end of this procedure. Use the default IP address to access the sensor from a browser and [continue the deployment process](activate-deploy-sensor) from there.

**To install your software**:

1. Mount the downloaded ISO file onto your hardware appliance or VM using one of the following options:

    - **Physical media** – burn the ISO file to your external storage, and then boot from the media.

        - DVDs: First burn the software to the DVD as an image.
        - USB drive: First make sure that you’ve created a bootable USB drive with software such as [Rufus](https://rufus.ie/en/), and then save the software to the USB drive. USB drives must have USB version 3.0 or later.
        - Select the **DD Image mode** setting when creating your image, for example:

        ![Screenshot of the DD image settings.](media/rufus-4-4-dd-image-mode.png)

        ![Screenshot of the drive properties.](media/rufus-4-4-drive-properties.png)

        Your physical media must have a minimum of 4-GB storage.
    - **Virtual mount** – use iLO for HPE appliances, or iDRAC for Dell appliances to boot the ISO file.
2. When the installation boots, you're prompted to start the installation process. Either select the **Install iot-sensor-`<version number>`** item to continue, or leave the wizard to make the selection automatically on its own.

    The wizard automatically selects to install the software after 30 seconds of waiting. For example:

    ![Screenshot of the initial installation screen.](../media/install-software-ot-sensor/initial-install-screen.png)

    Note

    If you're using a legacy BIOS version, you're prompted to select a language and the installation options are presented at the top left instead of in the center. When prompted, select `English` and then the **Install iot-sensor-`<version number>`** option to continue.

    The installation begins, giving you updated status messages as it goes. The entire installation process takes up to 20-30 minutes, and may vary depending on the type of media you're using.

    When the installation is complete, you're shown the following a set of default networking details. While the default IP, subnet, and gateway addresses are identical with each installation, the UID is unique for each appliance. For example:

    ```bash
    IP: 192.168.0.101, 
    SUBNET: 255.255.255.0, 
    GATEWAY: 192.168.0.1,
    UID: 91F14D56-C1E4-966F-726F-006A527C61D
    ```

Use the default IP address provided to access your sensor for initial setup and activation.