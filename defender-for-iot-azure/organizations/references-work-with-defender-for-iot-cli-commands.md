---
layout: Conceptual
title: CLI command users and access for OT monitoring - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/references-work-with-defender-for-iot-cli-commands
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
description: Learn about the users supported for the Microsoft Defender for IoT CLI commands and how to access the CLI.
ms.date: 2023-12-19T00:00:00.0000000Z
ms.topic: concept-article
locale: en-us
document_id: dc3edb4e-8123-b4a3-34b6-6e1f072063cb
document_version_independent_id: 4b7ab735-4cd4-eb6f-71e8-d626d49064a5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/references-work-with-defender-for-iot-cli-commands.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/references-work-with-defender-for-iot-cli-commands
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/references-work-with-defender-for-iot-cli-commands.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/aebdc4a3-c54b-4eea-94e3-663d5e166f57
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/1baec8e6-ab38-4b56-bb59-f6282d94f311
platformId: 2aa15f51-b3e7-9fb2-b5cd-a545ab5abcea
---

# CLI command users and access for OT monitoring - Microsoft Defender for IoT | Microsoft Learn

This article provides an introduction to the Microsoft Defender for IoT command line interface (CLI). The CLI is a text-based user interface that allows you to access your OT sensors for advanced configuration, troubleshooting, and support.

To access the Defender for IoT CLI, you need access to the sensor.

- For OT sensors, you need to sign in as a privileged user.
- For Enterprise IoT sensors, you can sign in as any user.

Caution

Only documented configuration parameters on the OT network sensor are supported for customer configuration. Do not change any undocumented configuration parameters or system properties, as changes may cause unexpected behavior and system failures.

Removing packages from your sensor without Microsoft approval can cause unexpected results. All packages installed on the sensor are required for correct sensor functionality.

## Privileged user access for OT monitoring

Use the *admin* user when using the Defender for IoT CLI, which is an administrative account with access to all CLI commands.

If you're using a legacy software version, you may have one or more of the following users:

| Legacy scenario | Description |
| --- | --- |
| **Sensor versions earlier than 23.2.0** | In sensor versions earlier than [23.2.0](whats-new-archive#default-privileged-user-is-now-admin-instead-of-support), the default *admin* user is named *support*. The *support* user is available and supported only on versions earlier than 23.2.0.Documentation refers to the *admin* user to match the latest version of the software. |

Other CLI users cannot be added.

For more information, see [On-premises users and roles for OT monitoring with Defender for IoT](roles-on-premises).

### Supported users by CLI actions

The following tables list the activities available by CLI and the privileged users supported for each activity. The *cyberx* and *cyberx\_host* users are only supported in versions earlier than [23.1.x](release-notes).

### Appliance maintenance commands

| Service area | Users | Actions |
| --- | --- | --- |
| Sensor health | *admin*, *cyberx* | [Check OT monitoring services health](cli-ot-sensor#check-ot-monitoring-services-health) |
| Reboot and shutdown | *admin*, *cyberx*, *cyberx\_host* | [Restart an appliance](cli-ot-sensor#restart-an-appliance)[Shut down an appliance](cli-ot-sensor#shut-down-an-appliance) |
| Software versions | *admin*, *cyberx* | [Show installed software version](cli-ot-sensor#show-installed-software-version)[Update software version](update-ot-software) |
| Date and time | *admin*, *cyberx*, *cyberx\_host* | [Show current system date/time](cli-ot-sensor#show-current-system-datetime) |
| NTP | *admin*, *cyberx* | [Turn on NTP time sync](cli-ot-sensor#turn-on-ntp-time-sync)[Turn off NTP time sync](cli-ot-sensor#turn-off-ntp-time-sync) |

### Backup and restore commands

| Service area | Users | Actions |
| --- | --- | --- |
| List backup files | *admin*, *cyberx* | [List current backup files](cli-ot-sensor#list-current-backup-files)[Start an immediate, unscheduled backup](cli-ot-sensor#start-an-immediate-unscheduled-backup) |
| Restore | *admin*, *cyberx* | [Restore data from the most recent backup](cli-ot-sensor#restore-data-from-the-most-recent-backup) |
| Backup disk space | *cyberx* | [Display backup disk space allocation](cli-ot-sensor#display-backup-disk-space-allocation) |

### Local user management commands

| Service area | Users | Actions |
| --- | --- | --- |
| Password management | *cyberx*, *cyberx\_host* | [Change local user passwords](cli-ot-sensor#change-local-user-passwords) |
| Sign-in configuration | *cyberx* | [Define maximum number of failed sign-ins](manage-users-sensor#define-maximum-number-of-failed-sign-ins) |

### Network configuration commands

| Service area | Users | Actions |
| --- | --- | --- |
| Network setting configuration | *cyberx\_host* | [Change networking configuration or reassign network interface roles](cli-ot-sensor#change-networking-configuration-or-reassign-network-interface-roles) |
| Network setting configuration | *admin* | [Validate and show network interface configuration](cli-ot-sensor#validate-and-show-network-interface-configuration) |
| Network connectivity | *admin*, *cyberx* | [Check network connectivity from the OT sensor](cli-ot-sensor#check-network-connectivity-from-the-ot-sensor) |
| Physical interfaces management | *admin* | [Locate a physical port by blinking interface lights](cli-ot-sensor#locate-a-physical-port-by-blinking-interface-lights) |
| Physical interfaces management | *admin*, *cyberx* | [List connected physical interfaces](cli-ot-sensor#list-connected-physical-interfaces) |

### Traffic capture filter commands

| Service area | Users | Actions |
| --- | --- | --- |
| Capture filter management | *admin*, *cyberx* | [Create a basic filter for all components](cli-ot-sensor#create-a-basic-filter-for-all-components)[Create an advanced filter for specific components](cli-ot-sensor#create-an-advanced-filter-for-specific-components)[List current capture filters for specific components](cli-ot-sensor#list-current-capture-filters-for-specific-components)[Reset all capture filters](cli-ot-sensor#reset-all-capture-filters) |

## Defender for IoT CLI access

To access the Defender for IoT CLI, sign in to your OT or Enterprise IoT sensor using a terminal emulator and SSH.

- **On a Windows system**, use PuTTY or another similar application.
- **On a Mac system**, use Terminal.
- **On a virtual appliance**, access the CLI via SSH, the vSphere client, or Hyper-V Manager. Connect to the virtual appliance's management interface IP address via port 22.

Each CLI command on an OT network sensor is supported a different set of privileged users, as noted in the relevant CLI descriptions. Make sure you sign in as the user required for the command you want to run. For more information, see Privileged user access for OT monitoring.

## Access the system root as an *admin* user

When signing in as the *admin* user, run the following command to access the host machine as the root user. Access the host machine as the root user enables you to run CLI commands that aren't available to the *admin* user.

Run:

```support
system shell
```

## Sign out of the CLI

Make sure to properly sign out of the CLI when you're done using it. You're automatically signed out after an inactive period of 300 seconds.

To sign out manually on an OT sensor, run one of the following commands:

| User | Command |
| --- | --- |
| **admin** | `logout` |
| **cyberx** | `cyberx-xsense-logout` |
| **cyberx\_host** | `logout` |