---
layout: Conceptual
title: Defender for IoT - Update OT monitoring software - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/update-ot-software
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
description: Learn how to update the OT software on your Defender for IoT sensors so that you can manage updates efficiently.
ms.date: 2025-01-20T00:00:00.0000000Z
ms.topic: upgrade-and-migration-article
locale: en-us
document_id: f07fc64a-12f4-0792-861a-15309ad19235
document_version_independent_id: e3bedd28-04b8-16aa-ed9f-44784a6453ed
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/update-ot-software.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/update-ot-software
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/update-ot-software.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 9c2b7f8d-fba2-aef1-54d6-9e4bba0b50e8
---

# Defender for IoT - Update OT monitoring software - Microsoft Defender for IoT | Microsoft Learn

This article describes how to update the OT software on your Defender for IoT sensors so that you can manage updates and stay up to date with the latest version.

You can purchase pre-configured appliances for your sensors, or install software on your own hardware machines. In either case, you'll need to update software versions to use new features for OT sensors.

For more information, see [Which appliances do I need?](ot-appliance-sizing), [Pre-configured physical appliances for OT monitoring](ot-pre-configured-appliances), and [OT monitoring software release notes](release-notes).

Note

Update files are available for [currently supported versions](release-notes) only. If you have OT network sensors with legacy software versions that are no longer supported, open a support ticket to access the relevant files for your update.

## Prerequisites

To perform the procedures described in this article, make sure that you have:

- **A list of the OT sensors you'll want to update**, and the update methods you want to use. Each sensor that you want to update must be both [onboarded](onboard-sensors) to Defender for IoT and activated.

    | Update scenario | Method details |
    | --- | --- |
    | **Cloud-connected sensors** | Cloud connected sensors can be updated remotely, directly from the Azure portal, or manually using a downloaded update package. Remote updates require that your OT sensor has version [22.2.3](release-notes#2223) or later already installed. |
    | **Locally managed sensors** | Locally managed sensors can be updated using a downloaded update package directly on an OT sensor console. |
- **Required access permissions**:

    - **To download update packages or push updates from the Azure portal**, you need access to the Azure portal as a [Security Admin](/en-us/azure/role-based-access-control/built-in-roles#security-admin), [Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor), or [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) user.
    - **To run updates on an OT sensor**, you need access as an **Admin** user.
    - **To update an OT sensor via CLI**, you need access to the sensor as a [privileged user](roles-on-premises#default-privileged-on-premises-users).

    For more information, see [Azure user roles and permissions for Defender for IoT](roles-azure) and [On-premises users and roles for OT monitoring with Defender for IoT](roles-on-premises).

Important

We recommend verifying that you have sensor backups running regularly, and especially before updating sensor software.

For more information, see [Back up and restore OT network sensors from the sensor console](back-up-restore-sensor).

## Verify network requirements

- Make sure that your sensors can reach the Azure data center address ranges and set up any extra resources required for the connectivity method your organization is using.

    For more information, see [OT sensor cloud connection methods](architecture-connections) and [Connect your OT sensors to the cloud](connect-sensors).
- Make sure that your firewall rules are configured as needed for the new version you're updating to.

    For example, the new version might require a new or modified firewall rule to support sensor access to the Azure portal. From the **Sites and sensors** page, select **More actions &gt; Download sensor endpoint details** for the full list of endpoints required to access the Azure portal.

    For more information, see [Networking requirements](networking-requirements) and [Sensor management options from the Azure portal](how-to-manage-sensors-on-the-cloud#sensor-management-options-from-the-azure-portal).

## Update OT sensors with the latest OT monitoring software

This section describes how to update Defender for IoT OT sensors using any of the supported methods.

**Sending or downloading an update package** and **running the update** are two separate steps. Each step can be done one right after the other or at different times.

For example, you might want to first send the update to your sensor or download an update package, and then have an administrator run the update later on, during a planned maintenance window.

Select the update method you want to use:

# [Azure portal (Preview)](#tab/portal)
This procedure describes how to send a software version update to OT sensors at one or more sites, and run the updates remotely using the Azure portal. We recommend that you update the sensor by selecting sites and not individual sensors.

### Send the software update to your OT sensor

1. In [Defender for IoT](https://portal.azure.com/#view/Microsoft_Azure_IoT_Defender/IoTDefenderDashboard/%7E/Getting_started) in the Azure portal, select **Sites and sensors**.

    If you know your site and sensor name, you can browse or search for it directly, or apply a filter to help locate the site you need.
2. Select one or more sites to update, and then select **Sensor update** &gt; **Remote update** &gt; **Step one: Send package to sensor**. [![Screenshot of the Send package option.](media/update-ot-software/sensor-updates-1.png)](media/update-ot-software/sensor-updates-1.png#lightbox)

    For one or more individual sensors, select **Step one: Send package to sensor**. This option is also available from the **...** options menu to the right of the sensor row.
3. In the **Send package** pane that appears, under **Available versions**, select the software version from the list. If the version you need doesn't appear, select **Show more** to list all available versions.

    To jump to the release notes for the new version, select **Learn more** at the top of the pane.

    The lower half of the page shows the sensors you selected and their status. Verify the status of the sensors. A sensor might not be available for update for various reasons, for example, the sensor is already updated to the version you want to send, or there's a problem with the sensor, such as it's disconnected.

    [![Screenshot of sensor update pane with option to choose sensor update version.](media/update-ot-software/send-package-pane-400.png)](media/update-ot-software/send-package-pane.png#lightbox)
4. Once you've checked the list of sensors to be updated, select **Send package**, and the software transfer to your sensor machine is started. You can see the transfer progress in the **Sensor version** column, with the percentage completed automatically updating in the progress bar, so you can see that the process has started and letting you track its progress until the transfer is complete. For example:

    [![Screenshot of the update bar in the Sensor version column.](media/update-ot-software/sensor-version-update-bar.png)](media/update-ot-software/sensor-version-update-bar.png#lightbox)

    When the transfer is complete, the **Sensor version** column changes to ![](media/update-ot-software/ready-to-update.png)**Ready to update**.

    Hover over the **Sensor version** value to see the source and target version for your update.

### Install your sensor from the Azure portal

To install the sensor software update, ensure that you see the ![](media/update-ot-software/ready-to-update.png)**Ready to update** icon in the **Sensor version** column.

1. Select one or more sites to update, and then select **Sensor update** &gt; **Remote update** &gt; **Step 2: Update sensor** from the toolbar. The **Update sensor** pane opens in the right side of the screen.

    [![Screenshot of the package update option.](media/update-ot-software/sensor-updates-2.png)](media/update-ot-software/sensor-updates-2.png#lightbox)

    For an individual sensor, the **Step 2: Update sensor** option is also available from the **...** options menu.
2. In the **Update sensor** pane that appears, verify your update details.

    When you're ready, select **Update now** &gt; **Confirm update** to install the update on the sensor. In the grid, the **Sensor version** value changes to ![](media/update-ot-software/installing.png)**Installing**, and an update progress bar appears showing you the percentage complete. The bar automatically updates, so that you can track the progress until the installation is complete.

    [![Screenshot of the install bar in the Sensor version column.](media/update-ot-software/sensor-version-install-bar.png)](media/update-ot-software/sensor-version-install-bar.png#lightbox)

    When completed, the sensor value switches to the newly installed sensor version number.

If a sensor update fails to install for any reason, the software reverts back to the previous version installed, and a sensor health alert is triggered. For more information, see [Understand sensor health](how-to-manage-sensors-on-the-cloud#understand-sensor-health) and [Sensor health message reference](sensor-health-messages).

# [OT sensor UI](#tab/sensor)
This procedure describes how to manually download the new sensor software version and then run your update directly on the sensor console's UI.

### Download the update package from the Azure portal

1. In [Defender for IoT](https://portal.azure.com/#view/Microsoft_Azure_IoT_Defender/IoTDefenderDashboard/%7E/Getting_started) on the Azure portal, select **Sites and sensors** &gt; **Sensor update (Preview)**.
2. In the **Local update** pane, select the software version that's currently installed on your sensors.
3. In the **Available versions** area of the **Local update** pane, select the version you want to download for your software update.

    The **Available versions** area lists all update packages available for your specific update scenario. You might have multiple options, but one specific version is marked as **Recommended** for you. For example:

    [![Screenshot highlighting the recommended update version for the selected update scenario.](media/update-ot-software/recommended-version.png)](media/update-ot-software/recommended-version.png#lightbox)
4. Scroll down further in the **Local update** pane and select **Download** to download the update package.

    The update package is downloaded with a file syntax name of `sensor-secured-patcher-<Version number>.tar`, where `version number` is the version you're updating to.

    All files downloaded from the Azure portal are signed by root of trust so that your machines use signed assets only.

### Update the OT sensor software from the sensor UI

1. Sign into your OT sensor and select **System Settings** &gt; **Sensor management** &gt; **Software Update**.
2. On the **Software Update** pane on the right, select **Upload file**, and then navigate to and select your downloaded update package.

    [![Screenshot of the Software update pane on the OT sensor.](media/update-ot-software/sensor-upload-file.png)](media/update-ot-software/sensor-upload-file.png#lightbox)

    The update process starts, and might take about 30 minutes and include one or two reboots. If your machine reboots, make sure to sign in again as prompted.

# [OT sensor CLI](#tab/cli)
This procedure describes how to update OT sensor software via the CLI, directly on the OT sensor.

### Download the update package from the Azure portal

1. In [Defender for IoT](https://portal.azure.com/#view/Microsoft_Azure_IoT_Defender/IoTDefenderDashboard/%7E/Getting_started) on the Azure portal, select **Sites and sensors** &gt; **Sensor update (Preview)**.
2. In the **Local update** pane, select the software version that's currently installed on your sensors.
3. In the **Available versions** area of the **Local update** pane, select the version you want to download for your software update.

    The **Available versions** area lists all update packages available for your specific update scenario. You may have multiple options, but there will always be one specific version marked as **Recommended** for you. For example:

    [![Screenshot highlighting the recommended update version for the selected update scenario.](media/update-ot-software/recommended-version.png)](media/update-ot-software/recommended-version.png#lightbox)
4. Scroll down further in the **Local update** pane and select **Download** to download the software file.

    The update package is downloaded with a file syntax name of `sensor-secured-patcher-<Version number>.tar`, where `version number` is the version you're updating to.

All files downloaded from the Azure portal are signed by root of trust so that your machines use signed assets only.

### Update sensor software directly from the sensor via CLI

1. Use SFTP or SCP to copy the update package you'd downloaded from the Azure portal to the OT sensor machine.
2. Sign in to the sensor as the `cyberx_host` user, and copy the update file to a location accessible for the update process. For example:

    ```bash
    cd /var/host-logs/ 
    mv <filename> /var/cyberx/media/device-info/update_agent.tar
    ```
3. Sign into the sensor as the `cyberx` user and start running the software update. Run:

    ```bash
    curl -H "X-Auth-Token: $(python3 -c 'from cyberx.credentials.credentials_wrapper import CredentialsWrapper;creds_wrapper = CredentialsWrapper();print(creds_wrapper.get("api.token"))')" -X POST http://127.0.0.1:9090/core/api/v1/configuration/agent
    ```

    At some point during the update process, your SSH connection will disconnect. This is a good indication that your update is running.
4. Continue to monitor the update process by checking the `install.log` file.

    Sign back into the sensor as the `cyberx_host` user and run:

    ```bash
    tail -f /opt/sensor/logs/install.log
    ```

---

### Confirm that your update succeeded

To confirm that the update process completed successfully, check the sensor version in the following locations for the new version number:

- In the Azure portal, on the **Sites and sensors** page, in the **Sensor version** column
- On the OT sensor console:

    - In the title bar
    - On the **Overview** page &gt; **General Settings** area
    - In the **System settings** &gt; **Sensor management** &gt; **Software update** pane

Upgrade log files are located on the OT sensor machine at `/opt/sensor/logs/legacy-upgrade.log`, and are accessible to the *[cyberx_host](roles-on-premises#default-privileged-on-premises-users)* user via SSH.