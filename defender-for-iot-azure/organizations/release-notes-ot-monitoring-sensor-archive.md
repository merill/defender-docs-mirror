---
layout: Conceptual
title: OT monitoring software versions archive for Microsoft Defender for IoT for organizations - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/release-notes-ot-monitoring-sensor-archive
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
description: This article lists Microsoft Defender for IoT on-premises OT monitoring software versions archive released more than six months ago, including release and support dates and highlights for new features.
ms.topic: concept-article
ms.date: 2025-04-06T00:00:00.0000000Z
locale: en-us
document_id: e31b6efc-504f-a7a8-c4ed-01c5f89ab193
document_version_independent_id: ca9085f9-446a-f1c5-a9c7-0af704f4a49e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/release-notes-ot-monitoring-sensor-archive.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/release-notes-ot-monitoring-sensor-archive
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/release-notes-ot-monitoring-sensor-archive.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 836927df-1ae2-e760-017d-fecd6011a1e9
---

# OT monitoring software versions archive for Microsoft Defender for IoT for organizations - Microsoft Defender for IoT | Microsoft Learn

This article serves as an archive for OT monitoring software versions released for Microsoft Defender for IoT for organizations more than six months ago.

For more recent updates, see [OT monitoring software versions in Microsoft Defender for IoT?](release-notes)

Noted features listed below are in PREVIEW. The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include other legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

## Versioning and support for on-premises software versions

This section describes the servicing information, timelines, and guidance for the available on-premises software versions.

Note

If you have an on-premises management console, make sure to also update your on-premises management console to the same version as your sensors.

For more information, see [Update Defender for IoT OT monitoring software](update-ot-software).

### OT monitoring software versions (sensor versions)

Cloud features may be dependent on a specific sensor version. Such features are listed below for the relevant software versions, and are only available for data coming from sensors that have the required version installed, or higher.

Important

The on-premises management console isn't supported or available for download after January 1st, 2025. For more information, see [on-premises management console retirement](ot-deploy/on-premises-management-console-retirement).

| Version / Patch | Release date | Scope | Supported until |
| --- | --- | --- | --- |
| **23.2** |  |  |  |
| 23.2.0 | 12/2023 | Major | 12/2024 |
| **23.1** |  |  |  |
| 23.1.3 | 09/2023 | Patch | 08/2024 |
| 23.1.2 | 07/2023 | Major | 06/2024 |
| **22.3** |  |  |  |
| 22.3.10 | 07/2023 | Patch | 06/2024 |
| 22.3.9 | 05/2023 | Patch | 04/2024 |
| 22.3.8 | 04/2023 | Patch | 03/2024 |
| 22.3.7 | 03/2023 | Patch | 02/2024 |
| 22.3.6 | 03/2023 | Patch | 02/2024 |
| 22.3.5 | 01/2023 | Patch | 12/2023 |
| 22.3.4 | 01/2023 | Major | 12/2023 |
| **22.2** |  |  |  |
| 22.2.9 | 01/2023 | Patch | 12/2023 |

### Threat intelligence updates

Threat intelligence updates are continuously available and are independent of specific sensor versions. You don't need to update your sensor version in order to get the latest threat intelligence updates.

For more information, see [Threat intelligence research and packages](how-to-work-with-threat-intelligence-packages).

### Support model

Defender for IoT provides **1 year of support** for every new version, starting with versions **22.1.7** and **22.2.7**. For example, version **22.2.7** was released in **October 2022** and is supported through **September 2023**.

Earlier versions use a legacy support model, with support dates detailed for each version.

### On-premises appliance security

The OT network sensor and the on-premises management console are designed as a *locked-down* security appliance with a hardened attack surface. Appliance access and control are allowed only through the [management port](best-practices/understand-network-architecture), via HTTP for web access and SSH for the support shell.

Defender for IoT adheres to the [Microsoft Security Development Lifecycle](https://www.microsoft.com/securityengineering/sdl/) throughout the entire development lifecycle, including activities like training, compliance, code reviews, threat modeling, design requirements, component governance, and pen testing. All appliances are locked down according to industry best practices and shouldn't be modified.

Maintain your sensors and on-premises management consoles, for activities like backups, log exports, or health monitoring, via the web interface, or the Defender for IoT [CLI commands](references-work-with-defender-for-iot-cli-commands).

Important

Manual changes to software packages or additions of external packages may have detrimental security or functional effects on the sensor and on-premises management console. Microsoft is unable to support deployments with manual changes made to software packages.

### Feature documentation per versions

Version numbers are listed only in this article and in the [What's new in Microsoft Defender for IoT?](whats-new) article, and not in detailed descriptions elsewhere in the documentation.

To understand whether a feature is supported in your sensor version, check the relevant version section below and its listed features.

## Versions 23.2.x

### Version 23.2.0

**Release date**: 12/2023

**Supported until**: 12/2024

This version includes the following updates and enhancements:

- [Sensor software runs on a Debian 11 operating system](ot-deploy/install-software-ot-sensor) and [updates to this version may be heavier and longer than usual](whats-new-archive#ot-network-sensors-now-run-on-debian-11)
- [The legacy, privileged default *support* user is replaced by the default *admin* user](roles-on-premises#legacy-users)

Important

If you're updating your software from a legacy version and have the *support* credentials saved, such as in CLI scripts, we recommend that you update those credentials to use the *admin* user instead.

## Versions 23.1.x

### Version 23.1.3

**Release date**: 09/2023

**Supported until**: 08/2024

This version includes the following updates and enhancements:

- [Connectivity troubleshooting enhancements from the OT sensor](how-to-troubleshoot-sensor#check-sensor---cloud-connectivity-issues)
- [Read Only users can access the Event Timeline](roles-on-premises)

### Version 23.1.2

**Release date**: 07/2023

**Supported until**: 06/2024

This version includes the following updates and enhancements:

- [Simplified installation process](ot-deploy/install-software-ot-sensor)
- [A new sensor setup wizard from the UI](ot-deploy/activate-deploy-sensor)
- [Analyze sensor connectivity](how-to-manage-individual-sensors)
- [UI enhancements for downloading PCAP files from the sensor](how-to-view-alerts#access-alert-pcap-data)
- [*cyberx* and *cyberx\_host* users aren't enabled by default](roles-on-premises#default-privileged-on-premises-users)

Note

Due to internal improvements to the OT sensor's device inventory, column edits made to your device inventory aren't retained after updating to version 23.1.2. If you'd previously edited the columns shown in your device inventory, you'll need to make those same edits again after updating your sensor.

## Versions 22.3.x

### 22.3.10

**Release date**: 07/2023

**Supported until**: 06/2024

This version includes bug fixes for stability improvements.

### 22.3.9

**Release date**: 05/2023

**Supported until**: 04/2024

This version includes:

- [Improved monitoring and support for OT sensor logs](whats-new-archive#improved-monitoring-and-support-for-ot-sensor-logs)
- Bug fixes for stability improvements.

### 22.3.8

**Release date**: 04/2023

**Supported until**: 03/2024

- [Enrich Windows workstation and server data with a local script (Public preview)](detect-windows-endpoints-script)
- [Automatically resolved notifications for operating system changes and device type changes](how-to-work-with-the-sensor-device-map#device-notification-responses)
- [UI enhancements when uploading SSL/TLS certificates](how-to-deploy-certificates#deploy-a-certificate-on-an-ot-sensor)

### 22.3.6 / 22.3.7

**Release date**: 03/2023

**Supported until**: 02/2024

Version 22.3.7 includes the same features as 22.3.6. If you have version 22.3.6 installed, we strongly recommend that you update to version 22.3.7, which also includes important bug fixes.

- [Support for transient devices](device-inventory#supported-devices)
- [Autoresolved notifications](how-to-work-with-the-sensor-device-map#device-notification-responses)
- [Device data retention updated to 90 days](references-data-retention#device-data-retention-periods)
- [Merging](how-to-investigate-sensor-detections-in-a-device-inventory#merge-devices) and [deleting](how-to-investigate-sensor-detections-in-a-device-inventory#delete-devices) devices on OT sensors now include confirmation messages when the action has completed
- Support for [deleting multiple devices](how-to-investigate-sensor-detections-in-a-device-inventory#delete-devices) on OT sensors
- An enhanced [editing device details](how-to-investigate-sensor-detections-in-a-device-inventory#edit-device-details) process on the OT sensor, using an **Edit** button in the toolbar at the top of the page
- [Enhanced UI on the OT sensor for uploading an SSL/TLS certificate](ot-deploy/activate-deploy-sensor#define-ssltls-certificate-settings)
- [Activation files for locally managed sensors no longer expire](how-to-manage-individual-sensors#upload-a-new-activation-file)
- Severity for all [**Suspicion of Malicious Activity**](alert-engine-messages#malware-engine-alerts) alerts is now **Critical**
- [Allow internet connections on an OT network in bulk](how-to-accelerate-alert-incident-response#allow-internet-connections-on-an-ot-network)
- [Security recommendations for OT networks for insecure or missing passwords](recommendations#supported-security-recommendations)

### 22.3.5

**Release date**: 01/2023

**Supported until**: 12/2023

This version includes bug fixes for stability improvements.

### 22.3.4

**Release date**: 01/2021

**Supported until**: 12/2023

- [Azure connectivity status shown on OT sensors](how-to-manage-individual-sensors#validate-connectivity-status)
- [Configure Active Directory and NTP settings in the Azure portal](configure-sensor-settings-portal#active-directory)

## Versions 22.2.x

To update to 22.2.x versions:

- **From version 22.1.x**, update directly to the latest **22.2.x** version
- **From version 10.x**, first update to the latest **22.1.x** version, and then update again to the latest **22.2.x** version.

For more information, see [Update Defender for IoT OT monitoring software](update-ot-software).

### 22.2.9

**Release date**: 01/2023

**Supported until**: 12/2023

This version includes bug fixes for stability improvements.

### 22.2.8

**Release date**: 11/2022

**Supported until**: 10/2023

This version includes bug fixes for stability improvements.

### 22.2.7

**Release date**: 10/2022

**Supported until**: 09/2023

This version includes bug fixes for stability improvements.

### 22.2.6

**Release date**: 09/2022

**Supported until**: 04/2023

This version includes the following new updates and fixes:

- Bug fixes and stability improvements
- Enhancements to the device type classification algorithm

### 22.2.5

**Release date**: 08/2022

**Supported until**: 04/2023

This version includes minor stability improvements.

### 22.2.4

**Release date**: 07/2022

**Supported until**: 04/2023

This version includes the following new updates and fixes:

- [Device inventory enhancements in the sensor console](how-to-investigate-sensor-detections-in-a-device-inventory):

    - Merge duplicate devices, delete single devices, and delete inactive devices by admin users
    - **Last seen** value in the device details pane is replaced by **Last activity**
- [New parameters for the *devicecves* API](api/management-integration-apis): `sensorId`, `score`, and `deviceIds`
- [New alert columns with timestamp data](how-to-view-alerts): **Last detection**, **First detection**, and **Last activity**

### 22.2.3

**Release date**: 07/2022

**Supported until**: 04/2023

This version includes the following new updates and fixes:

- [Define and view OT sensor settings from the Azure portal](configure-sensor-settings-portal)
- [Update your sensors from the Azure portal](update-ot-software#update-ot-sensors-with-the-latest-ot-monitoring-software)
- [New naming convention for hardware profiles](ot-appliance-sizing)
- [PCAP access from the Azure portal](how-to-manage-cloud-alerts)
- [Bi-directional alert synch between OT sensors and the Azure portal](alerts#managing-ot-alerts-in-a-hybrid-environment)
- [Sensor connections restored after certificate rotation](how-to-manage-individual-sensors#manage-ssltls-certificates)
- [Upload diagnostic logs for support tickets from the Azure portal](how-to-manage-sensors-on-the-cloud#upload-a-diagnostics-log-for-support)
- [Improved security for uploading protocol plugins](resources-manage-proprietary-protocols)
- [Sensor names shown in browser tabs](how-to-manage-individual-sensors)
- [Site-based access control on the Azure portal](manage-users-portal#manage-site-based-access-control-public-preview)

## Versions 22.1.x

Software versions 22.1.x support direct updates to the latest OT monitoring software versions available. For more information, see [Update Defender for IoT OT monitoring software](update-ot-software).

### 22.1.7

**Release date**: 07/2022

**Supported until**: 06/2023

This version includes the following new updates and fixes:

- [Identical passwords for *cyberx\_host* and *cyberx* users created during installations and updates](how-to-install-software)

### 22.1.6

**Release date**: 06/2022

**Supported until**: 10/2022

This version minor maintenance updates for internal sensor components.

### 22.1.5

**Release date**: 06/2022

**Supported until**: 10/2022

This version minor updates to improve TI installation packages and software updates.

### 22.1.4

**Release date**: 04/2022

**Supported until**: 10/2022

This version includes the following new updates and fixes:

- [Extended device property data in the **Device inventory** page on the Azure portal](how-to-manage-device-inventory-for-organizations), for the **Description**, **Tags**. **Protocols**, **Scanner**, and **Last Activity** fields

### 22.1.3

**Release date**: 03/2022

**Supported until**: 10/2022

This version includes the following new updates and fixes:

- [Diagnostic logs automatically available to support for cloud-connected sensors](how-to-troubleshoot-sensor#download-a-diagnostics-log-for-support)
- [Rockwell protocol: Device inventory shows PLC operating mode key state, run state, and security mode](how-to-manage-device-inventory-for-organizations)
- [Automatic CLI session timeouts](references-work-with-defender-for-iot-cli-commands)
- [Sensor health widgets in the Azure portal](how-to-manage-sensors-on-the-cloud#understand-sensor-health)

### 22.1.1

**Release date**: 02/2022

**Supported until**: 10/2022

This version includes the following new updates and fixes:

- [New sensor installation wizard](how-to-install-software)
- [Sensor redesign and unified Microsoft product experience](how-to-manage-individual-sensors)
- [Enhanced sensor Overview page](how-to-manage-individual-sensors)
- [New sensor diagnostics log](how-to-troubleshoot-sensor#download-a-diagnostics-log-for-support)
- [Alert updates](how-to-view-alerts):

    - Contextual data for each alert
    - Refreshed alert statuses
    - Alert storage updates
    - A new **Backup Activity with Antivirus Signatures** alert
    - Alert management changes during software updates
- [Enhancements for creating custom alerts on the sensor](how-to-accelerate-alert-incident-response#create-custom-alert-rules-on-an-ot-sensor): Hit count data, advanced scheduling options, and more supported fields and protocols
- [Modified CLI commands](cli-ot-sensor): Including the following new commands:

    - `sudo dpkg-reconfigure iot-sensor`
    - `sudo dpkg-reconfigure iot-sensor`
    - `sudo dpkg-reconfigure iot-sensor`
- [Refreshed update process and update log](update-ot-software)
- [New connectivity models](architecture-connections)
- [New firewall requirements](networking-requirements#sensor-access-to-azure-portal)
- [Improved support for Profinet DCP, Honeywell, and Windows endpoint detection protocols](concept-supported-protocols)
- [Sensor reports now accessible from the **Data Mining** page](how-to-create-data-mining-queries)
- [Updated process for sensor name changes](how-to-manage-individual-sensors#upload-a-new-activation-file)
- [Site-based access control on the Azure portal](manage-users-portal#manage-site-based-access-control-public-preview)