---
layout: Conceptual
title: Back up and restore OT network sensors from the sensor console - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/back-up-restore-sensor
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
description: Learn how to back up and restore Microsoft Defender for IoT OT network sensors from the sensor console.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-ropc-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: d7b5949e-49e4-71ed-5559-3240de43b73e
document_version_independent_id: 419d5ac3-0766-da06-4cf9-809cce6643d9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/back-up-restore-sensor.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/back-up-restore-sensor
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/back-up-restore-sensor.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/aebdc4a3-c54b-4eea-94e3-663d5e166f57
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1baec8e6-ab38-4b56-bb59-f6282d94f311
platformId: 46f7a5d3-42d6-897b-2aa0-3532f8590444
---

# Back up and restore OT network sensors from the sensor console - Microsoft Defender for IoT | Microsoft Learn

OT sensor data can be backed up and restored from the sensor console to help protect against hard drive failures and data loss. In this article, learn how to:

- Set up automatic backup files from the sensor console GUI or via CLI
- Back up files manually via sensor console GUI and CLI
- Use an SMB server to save your backup file to an external server
- Restore an OT sensor from the GUI or via CLI

## Set up backup and restore files

OT sensors are automatically backed up daily at 3:00 AM, including configuration and detected data. Backup files do *not* include PCAP or log files, which must be manually backed up if needed.

We recommend that you configure your OT sensor to automatically transfer backup files to your own internal network.

For more information, see [On-premises backup file capacity](references-data-retention#backup-file-capacity).

Note

Backup files can be used to restore an OT sensor only if the OT sensor's current software version is the same as the version in the backup file.

### Turn on backup functionality

If your OT sensor is configured *not* to run automatic backups, you can turn automatic backups back on manually in the `/var/cyberx/properties/backup.properties` file on the OT sensor machine.

## Create a manual backup file

You may want to create a manual backup file, such as just after updating your OT sensor software, or when troubleshooting with customer support.

To create a backup file that you can use to restore your sensor, use the CLI and run the `cyberx-xsense-system-backup` CLI command. For more information, see the [OT sensor CLI reference](cli-ot-sensor#start-an-immediate-unscheduled-backup).

To create a protected backup file to send to the support team, use the sensor GUI. Backup files created from the sensor GUI can be opened only together with assistance from Microsoft support.

**To create a manual backup file from the sensor GUI**:

1. Sign into the OT sensor GUI and select **System settings** &gt; **Sensor management** &gt; **Health and troubleshooting** &gt; **Backup & restore**.
2. In the **Backup & restore pane**:

    - Enter a meaningful filename for your backup file.
    - Select the content you want to back up.
    - Select **Export**.

Your new, protected backup file is listed in the **Archived files** area of the backup pane.

## Save your backup to an external server (SMB)

We recommend saving your OT sensor backup files on your internal network. To do this, you may want to use an SMB server. For example:

1. Create a shared folder on the external SMB server, and make sure that you have the folder's path and the credentials required to access the SMB server.
2. Sign into your OT sensor via SSH using the [*admin*](roles-on-premises#access-per-privileged-user) user.

    Note

    If you're using a sensor version earlier than 23.2.0, use the [*cyberx\_host*](roles-on-premises#legacy-users) user instead. Skip the step where you run `system shell` and go directly to the step to create a directory for your backup files.
3. Access the host by running the `system shell` command. Enter the admin user's password when prompted and press **ENTER**.
4. Create a directory for your backup files. Run:

    ```bash
    sudo mkdir /<backup_folder_name>
    
    sudo chmod 777 /<backup_folder_name>/
    ```
5. Edit the `fstab` file with details about your backup folder. Run:

    ```bash
    sudo nano /etc/fstab
    
    add - //<server_IP>/<folder_path> /<backup_folder_name_on_cyberx_server> cifs rw,credentials=/etc/samba/user,vers=X.X,file_mode=0777,dir_mode=0777
    ```

    Make sure you replace `vers=X.X` with the correct version of your external SMB server. For example `vers=3.0`.
6. Edit and create credentials to share for the SMB server. Run:

    ```bash
    sudo nano /etc/samba/user
    ```
7. Add the SMB server credentials used to authenticate with the shared backup folder, in the following format:

    ```text
    username=<user name>
    password=<password>
    ```
8. Mount the backup directory. Run:

    ```bash
    sudo mount -a
    ```
9. Configure your backup directory on the SMB server to use the shared file on the OT sensor. Run:

    ```bash
    sudo dpkg-reconfigure iot-sensor
    ```

    Follow the instructions on screen and validate that the backup-folder and SMB-mount settings are correct at each prompt.

    To continue to the next prompt without making changes, press **ENTER**.

    You'll be prompted to `Enter path to the mounted backups folder`. For example:

    ![Screenshot of the sensor configuration dialog prompting for the mounted backups folder path.](media/back-up-restore-sensor/screenshot-of-enter-path-to-mounted-backups-folder-prompt.png)

    The factory default value is `/opt/sensor/persist/backups`.

    Set the value to the folder you created in the first few steps, using the following syntax: `/<backup_folder_name>`. For example:

    ![Screenshot of the sensor configuration dialog with the mounted backups folder path entered.](media/back-up-restore-sensor/screenshot-of-enter-path-to-mounted-backups-folder-with-updated-value.png)

    Press **ENTER** to confirm the change, then continue through the remaining `dpkg-reconfigure iot-sensor` prompts until the command finishes.

## Restore an OT sensor

Use the procedures in this section to restore your OT sensor from an automatically generated or CLI-created backup file. Restoring your sensor using backup files created via the sensor GUI is supported only together with customer support.

### Restore an OT sensor from the sensor GUI

To restore an OT sensor from a backup file using the sensor GUI, perform the following steps:

1. Sign into the OT sensor via SFTP and download the backup file you want to use to a location accessible from the OT sensor GUI. Backup files are saved on your OT sensor machine, at `/var/cyberx/backups`, and are named using the following syntax: `<sensor name>-backup-version-<version>-<date>.tar`.

    For example: `Sensor_1-backup-version-2.6.0.102-2019-06-24_09:24:55.tar`

    Important

    Make sure that the backup file you select uses the same OT sensor software version that's currently installed on your OT sensor.

    Your backup file must be one that had been generated automatically or manually via the CLI. If you're using a backup file generated manually by the GUI, contact support to use it to restore your sensor.
2. Sign into the OT sensor GUI and select **System settings** &gt; **Sensor management** &gt; **Health and troubleshooting** &gt; **Backup & restore** &gt; **Restore**.
3. Select **Browse** to select your downloaded backup file. The sensor will start to restore from the selected backup file.
4. When the restore process is complete, select **Close**.

### Restore an OT sensor from the latest backup via CLI

To restore your OT sensor from the latest, automatically generated backup file via CLI:

1. Make sure that your backup file has the same OT sensor software version as the current software version on the OT sensor.
2. Use the `cyberx-xsense-system-restore` CLI command to restore your OT sensor.

For more information, see the [OT sensor CLI reference](cli-ot-sensor#restore-data-from-the-most-recent-backup).