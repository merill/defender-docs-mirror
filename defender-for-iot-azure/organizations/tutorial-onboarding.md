---
layout: Conceptual
title: Onboard and activate a virtual OT sensor - Microsoft Defender for IoT. - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/tutorial-onboarding
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
description: This tutorial describes how to set up a virtual OT network sensor to monitor your OT network traffic.
ms.topic: tutorial
ms.date: 2023-12-19T00:00:00.0000000Z
locale: en-us
document_id: 258abb86-9fb2-a07a-40c1-fc1025a538d5
document_version_independent_id: dedd61ce-8b10-c4cf-68d0-5af3178f619b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/tutorial-onboarding.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/tutorial-onboarding
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/tutorial-onboarding.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 87deae87-bc17-9944-bd04-373f5048d7a9
---

# Onboard and activate a virtual OT sensor - Microsoft Defender for IoT. - Microsoft Defender for IoT | Microsoft Learn

This tutorial describes the basics of setting up a Microsoft Defender for IoT OT sensor, using a subscription of Microsoft Defender for IoT and your own virtual machine.

For a full, end-to-end deployment, make sure to follow steps to plan and prepare your system, and also fully calibrate and fine-tune your settings. For more information, see [Deploy Defender for IoT for OT monitoring](ot-deploy/ot-deploy-path).

Note

If you're looking to set up security monitoring for enterprise IoT systems, see [Enable Enterprise IoT security in Defender for Endpoint](eiot-defender-for-endpoint).

In this tutorial, you learn how to:

- Create a VM for the sensor
- Onboard a virtual sensor
- Configure a virtual SPAN port
- Provision for cloud management
- Download software for a virtual sensor
- Install the virtual sensor software
- Activate the virtual sensor

## Prerequisites

Before you start, make sure that you have the following:

- Completed [Quickstart: Get started with Defender for IoT](getting-started) so that you have an Azure subscription added to Defender for IoT.
- Access to the Azure portal as a [Security Admin](/en-us/azure/role-based-access-control/built-in-roles#security-admin), [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor), or [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner). For more information, see [Azure user roles for OT and Enterprise IoT monitoring with Defender for IoT](roles-azure).
- Make sure that you have a network switch that supports traffic monitoring via a SPAN port. You'll also need at least one device to monitor, connected to the switch's SPAN port.
- VMware, ESXi 5.5 or later, installed and operational on your sensor.
- Available hardware resources for your VM as follows:

    | Deployment type | Corporate | Enterprise | SMB |
    | --- | --- | --- | --- |
    | **Maximum bandwidth** | 2.5 Gb/sec | 800 Mb/sec | 160 Mb/sec |
    | **Maximum protected devices** | 12,000 | 10,000 | 800 |
- An understanding of [OT monitoring with virtual appliances](ot-virtual-appliances).
- Details for the following network parameters to use for your sensor appliance:

    - A management network IP address
    - A sensor subnet mask
    - An appliance hostname
    - A DNS address
    - A default gateway
    - Any input interfaces

## Create a VM for your sensor

This procedure describes how to create a VM for your sensor with VMware ESXi.

Defender for IoT also supports other processes, such as using Hyper-V or physical sensors. For more information, see [Defender for IoT installation](how-to-install-software).

**To create a VM for your sensor**:

1. Make sure that VMware is running on your machine.
2. Sign in to the ESXi, choose the relevant **datastore**, and select **Datastore Browser**.
3. **Upload** the image and select **Close**.
4. Go to **Virtual Machines**, and then select **Create/Register VM**.
5. Select **Create new virtual machine**, and then select **Next**.
6. Add a sensor name and then define the following options:

    - Compatibility: **&lt;latest ESXi version&gt;**
    - Guest OS family: **Linux**
    - Guest OS version: **Debian**
7. Select **Next**.
8. Choose the relevant datastore and select **Next**.
9. Change the virtual hardware parameters according to the required specifications for your needs. For more information, see the table in the Prerequisites section above.

Your VM is now prepared for your Defender for IoT software installation. You'll continue by installing the software later on in this tutorial, after you've onboarded your sensor in the Azure portal, configured traffic mirroring, and provisioned the machine for cloud management.

## Onboard the virtual sensor

Before you can start using your Defender for IoT sensor, you need to onboard your new virtual sensor to your Azure subscription.

**To onboard the virtual sensor:**

1. In the Azure portal, go to the [**Defender for IoT &gt; Getting started**](https://portal.azure.com/#blade/Microsoft_Azure_IoT_Defender/IoTDefenderDashboard/Getting_Started) page.
2. At the bottom left, select **Set up OT/ICS Security**.

    Alternately, from the Defender for IoT **Sites and sensors** page, select **Onboard OT sensor** &gt; **OT**.

    By default, on the **Set up OT/ICS Security** page, **Step 1: Did you set up a sensor?** and **Step 2: Configure SPAN port or TAP​** of the wizard are collapsed.

    You'll install software and configure traffic mirroring later on in the deployment process, but should have your appliances ready and traffic mirroring method planned.
3. In **Step 3: Register this sensor with Microsoft Defender for IoT**, define the following values:

    | Field name | Description |
    | --- | --- |
    | **Resource name** | Select the site you want to attach your sensors to, or select **Create site** to create a new site. If you're creating a new site: 1. In the **New site** field, enter your site's name and select the checkmark button. 2. From the **Site size** menu, select your site's size. The sizes listed in this menu are the sizes that you're licensed for, based on the licenses [you'd purchased](how-to-manage-subscriptions) in the Microsoft 365 admin center. |
    | **Display name** | Enter a meaningful name for your site to be shown across Defender for IoT. |
    | **Tags** | Enter tag key and values to help you identify and locate your site and sensor in the Azure portal. |
    | **Zone** | Select the zone you want to use for your OT sensor, or select **Create zone** to create a new one. |

    For more information, see [Plan OT sites and zones](best-practices/plan-corporate-monitoring#plan-ot-sites-and-zones).
4. When you're done with all other fields, select **Register** to add your sensor to Defender for IoT. A success message is displayed and your activation file is automatically downloaded. The activation file is unique for your sensor and contains instructions about your sensor's management mode.

    All files downloaded from the Azure portal are signed by root of trust so that your machines use signed assets only.
5. Save the downloaded activation file in a location that will be accessible to the user signing into the console for the first time so they can activate the sensor.

    You can also download the file manually by selecting the relevant link in the **Activate your sensor** box. You'll use this file to activate your sensor, as described below.
6. In the **Add outbound allow rules** box, select the **Download endpoint details** link to download a JSON list of the endpoints you must configure as secure endpoints from your sensor.

    Save the downloaded file locally. Use the endpoints listed in the downloaded file later in this tutorial to ensure that your new sensor can successfully connect to Azure.

    Tip

    You can also access the list of required endpoints from the **Sites and sensors** page. For more information, see [Sensor management options from the Azure portal](how-to-manage-sensors-on-the-cloud#sensor-management-options-from-the-azure-portal).
7. At the bottom left of the page, select **Finish**. You can now see your new sensor listed on the Defender for IoT **Sites and sensors** page.

    Until you activate your sensor, the sensor's status shows as **Pending Activation**.

For more information, see [Manage sensors with Defender for IoT in the Azure portal](how-to-manage-sensors-on-the-cloud).

## Configure a SPAN port

Virtual switches don't have mirroring capabilities. However, for the sake of this tutorial you can use *promiscuous mode* in a virtual switch environment to view all network traffic that goes through the virtual switch.

This procedure describes how to configure a SPAN port using a workaround with VMware ESXi.

Note

Promiscuous mode is an operating mode and a security monitoring technique for a VM's interfaces in the same portgroup level as the virtual switch to view the switch's network traffic. Promiscuous mode is disabled by default but can be defined at the virtual switch or portgroup level.

**To configure a monitoring interface with Promiscuous mode on an ESXi v-Switch**:

1. Open the vSwitch properties page and select **Add standard virtual switch**.
2. Enter **SPAN Network** as the network label.
3. In the MTU field, enter **4096**.
4. Select **Security**, and verify that the **Promiscuous Mode** policy is set to **Accept** mode.
5. Select **Add** to close the vSwitch properties.
6. Highlight the vSwitch you've created, and select **Add uplink**.
7. Select the physical NIC you'll use for the SPAN traffic, change the MTU to **4096**, then select **Save**.
8. Open the **Port Group** properties page and select **Add Port Group**.
9. Enter **SPAN Port Group** as the name, enter **4095** as the VLAN ID, and select **SPAN Network** in the vSwitch drop down, then select **Add**.
10. Open the **OT Sensor VM** properties.
11. For **Network Adapter 2**, select the **SPAN** network.
12. Select **OK**.
13. Connect to the sensor, and verify that mirroring works.

## Validate traffic mirroring

After configuring traffic mirroring, make an attempt to receive a sample of recorded traffic (PCAP file) from the switch SPAN or mirror port.

A sample PCAP file will help you:

- Validate the switch configuration
- Confirm that the traffic going through your switch is relevant for monitoring
- Identify the bandwidth and an estimated number of devices detected by the switch

1. Use a network protocol analyzer application, such as [Wireshark](https://www.wireshark.org/), to record a sample PCAP file for a few minutes. For example, connect a laptop to a port where you've configured traffic monitoring.
2. Check that *Unicast packets* are present in the recording traffic. Unicast traffic is traffic sent from address to another.

    If most of the traffic is ARP messages, your traffic mirroring configuration isn't correct.
3. Verify that your OT protocols are present in the analyzed traffic.

    For example:

    ![Screenshot of Wireshark validation.](media/how-to-set-up-your-network/wireshark-validation.png)

## Provision for cloud management

This section describes how to configure endpoints to define in firewall rules, ensuring that your OT sensors can connect to Azure.

For more information, see [Methods for connecting sensors to Azure](architecture-connections).

**To configure endpoint details**:

Open the file you'd downloaded earlier to view the list of required endpoints. Configure your firewall rules so that your sensor can access each of the required endpoints, over port 443.

Tip

You can also download the list of required endpoints from the **Sites and sensors** page in the Azure portal. Go to **Sites and sensors** &gt; **More actions** &gt; **Download endpoint details**. For more information, see [Sensor management options from the Azure portal](how-to-manage-sensors-on-the-cloud#sensor-management-options-from-the-azure-portal).

For more information, see [Provision sensors for cloud management](ot-deploy/provision-cloud-management).

## Download software for your virtual sensor

This section describes how to download and install the sensor software on your own machine.

**To download software for your virtual sensors**:

1. In the Azure portal, go to the [**Defender for IoT &gt; Getting started**](https://portal.azure.com/#blade/Microsoft_Azure_IoT_Defender/IoTDefenderDashboard/Getting_Started) page, and select the **Sensor** tab.
2. In the **Purchase an appliance and install software** box, ensure that the default option is selected for the latest and recommended software version, and then select **Download**.
3. Save the downloaded software in a location that's accessible from your VM.

All files downloaded from the Azure portal are signed by root of trust so that your machines use signed assets only.

## Install sensor software

This procedure describes how to install the sensor software on your VM.

Note

Towards the end of this process you will be presented with the usernames and passwords for your device. Make sure to copy these down as these passwords will not be presented again.

**To install the software on the virtual sensor**:

1. If you closed your VM, sign into the ESXi again and open your VM settings.
2. For **CD/DVD Drive 1**, select **Datastore ISO file** and select the Defender for IoT software you'd downloaded earlier.
3. Select **Next** &gt; **Finish**.
4. Power on the VM, and open a console.
5. When the installation boots, you're prompted to start the installation process. Select the **Install iot-sensor-`<version number>`** item to continue or let it start automatically after 30 seconds. For example:

    ![Screenshot of the initial installation screen.](media/install-software-ot-sensor/initial-install-screen.png)

    Note

    If you're using a legacy BIOS version, you're prompted to select a language and the installation options are presented at the top left instead of in the center. When prompted, select `English` and then the **Install iot-sensor-`<version number>`** option to continue.

    The installation begins, giving you updated status messages as it goes. The entire installation process takes up to 20-30 minutes, and may vary depending on the type of media you're using.

    When the installation is complete, you're shown the following set of default networking details.

    ```bash
    IP: 172.23.41.83,
    SUBNET: 255.255.255.0,
    GATEWAY: 172.23.41.1,
    UID: 91F14D56-C1E4-966F-726F-006A527C61D
    ```

Use the default IP address provided to access your sensor for [initial setup and activation](ot-deploy/activate-deploy-sensor).

### Post-installation validation

This procedure describes how to validate your installation using the sensor's own system health checks and is available to the default *admin* user.

**To validate your installation**:

1. Sign in to the OT sensor as the `admin` user.
2. Select **System Settings** &gt; **Sensor management** &gt; **System Health Check**.
3. Select the following commands:

    - **Appliance** to check that the system is running. Verify that each line item shows **Running** and that the last line states that the **System is up**.
    - **Version** to verify that you have the correct version installed.
    - **ifconfig** to verify that all input interfaces configured during installation are running.

For more post-installation validation tests, such as gateway, DNS or firewall checks, see [Validate an OT sensor software installation](ot-deploy/post-install-validation-ot-software).

## Define initial setup

The following procedure describes how to configure your sensor's initial setup settings, including:

- Signing into the sensor console and changing the *admin* user password
- Defining network details for your sensor
- Defining the interfaces you want to monitor
- Activating your sensor
- Configuring SSL/TLS certificate settings

### Sign in to the sensor console and change the default password

This procedure describes how to sign into the OT sensor console for the first time. You're prompted to change the default password for the *admin* user.

**To sign in to your sensor**:

1. In a browser, go the `192.168.0.101` IP address, which is the default IP address provided for your sensor at the end of the installation.

    The initial sign-in page appears. For example:

    ![Screenshot of the initial sensor sign-in page.](media/install-software-ot-sensor/ui-sign-in.png)
2. Enter the following credentials and select **Login**:

    - **Username**: `support`
    - **Password**: `support`

    You're asked to define a new password for the *admin* user.
3. In the **New password** field, enter your new password. Your password must contain lowercase and uppercase alphabetic characters, numbers, and symbols.

    In the **Confirm new password** field, enter your new password again, and then select **Get started**.

    For more information, see [Default privileged users](manage-users-sensor#default-privileged-users).

The **Defender for IoT | Overview** page opens to the **Management interface** tab.

### Define sensor networking details

In the **Management interface** tab, use the following fields to define network details for your new sensor:

| Name | Description |
| --- | --- |
| **Management interface** | Select the interface you want to use as the management interface and connect to the Azure portal. To identify a physical interface on your machine, select an interface and then select **Blink physical interface LED**. The port that matches the selected interface lights up so that you can connect your cable correctly. |
| **IP Address** | Enter the IP address you want to use for your sensor. This is the IP address your team will use to connect to the sensor via the browser or CLI. |
| **Subnet Mask** | Enter the address you want to use as the sensor's subnet mask. |
| **Default Gateway** | Enter the address you want to use as the sensor's default gateway. |
| **DNS** | Enter the sensor's DNS server IP address. |
| **Hostname** | Enter the hostname you want to assign to the sensor. Make sure that you use the same hostname as is defined in the DNS server. |

For the sake of this tutorial, leave the skip the proxy configurations in the **Enable proxy for cloud connectivity (Optional)** area.

When you're done, select **Next: Interface configurations** to continue.

### Define the interfaces you want to monitor

The **Interface connections** tab shows all interfaces detected by the sensor by default. Use this tab to turn monitoring on or off per interface, or define specific settings for each interface.

Tip

We recommend that you optimize performance on your sensor by configuring your settings to monitor only the interfaces that are actively in use.

In the **Interface configurations** tab, do the following to configure settings for your monitored interfaces:

1. Select the **Enable/Disable** toggle for any interfaces you want the sensor to monitor. You must select at least one interface to continue.

    If you're not sure about which interface to use, select the ![](media/install-software-ot-sensor/blink-interface.png)**Blink physical interface LED** button to have the selected port blink on your machine. Select any of the interfaces that you've connected to your switch.
2. For the sake of this tutorial, skip any advanced settings and select **Next: Reboot &gt;** to continue.
3. When prompted, select **Start reboot** to reboot your sensor machine. After the sensor starts again, you're automatically redirected to the IP address you'd defined earlier as your sensor IP address.

    Select **Cancel** to wait for the reboot.

### Activate your OT sensor

This procedure describes how to activate your new OT sensor.

**To activate your sensor**:

1. In the **Activation** tab, select **Upload** to upload the sensor's activation file that you'd downloaded from the Azure portal.
2. Select the terms and conditions option and then select **Next: Certificates**.

### Define SSL/TLS certificate settings

Use the **Certificates** tab to deploy an SSL/TLS certificate on your OT sensor. While we recommend that you use a [CA-signed certificate](ot-deploy/create-ssl-certificates) for all production environments, for the sake of this tutorial, select to use a self-signed certificate.

**To define SSL/TLS certificate settings**:

1. In the **Certificates** tab, select **Use Locally generated self-signed certificate (Not recommended)**, and then select the **Confirm** option.

    For more information, see [SSL/TLS certificate requirements for on-premises resources](best-practices/certificate-requirements) and [Create SSL/TLS certificates for OT appliances](ot-deploy/create-ssl-certificates).
2. Select **Finish** to complete the initial setup and open your sensor console.