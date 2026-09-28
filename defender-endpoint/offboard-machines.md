---
layout: Conceptual
title: Offboard devices - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/offboard-machines
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Onboard Windows devices, servers, non-Windows devices from the Microsoft Defender for Endpoint service
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.topic: article
ms.subservice: onboard
ms.date: 2026-08-11T00:00:00.0000000Z
locale: en-us
document_id: 40d4b6e5-bad6-ec8f-94f6-45da80596554
document_version_independent_id: 40d4b6e5-bad6-ec8f-94f6-45da80596554
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/offboard-machines.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: offboard-machines
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/offboard-machines.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 9e9462b4-ab59-e1bb-7a01-048875fcc7ec
---

# Offboard devices - Microsoft Defender for Endpoint | Microsoft Learn

When you offboard a device from Defender for Endpoint, no new detections, vulnerability, or security data are sent to the Microsoft Defender portal. Seven days after offboarding a device, its status changes to [inactive](fix-unhealthy-sensors#inactive-devices). Devices that weren't active within the past 30 days are not factored into your organization's [exposure score](/en-us/defender-vulnerability-management/tvm-exposure-score).

Past data, such as alerts, vulnerabilities, and the device timeline, for an offboarded device is displayed in the Microsoft Defender portal until the [configured retention period](data-storage-privacy#data-retention) expires. You also see the device profile (without data) in the device inventory for up to 180 days. To view data for active devices only, you can use filters, such as [sensor health state](machines-view-overview#apply-filters), [device tags](machine-tags), or [device groups](machine-groups).

## Prerequisites

### Supported operating systems

- Windows client devices
- Windows Server 2012 R2 and later
- Azure Stack HCI OS, version 23H2 and later
- Mac devices
- Linux devices

For information about offboarding and uninstalling Microsoft Defender for Endpoint on Linux, see [Offboard Microsoft Defender for Endpoint on Linux](linux-off-board-endpoints).

In the [Microsoft Defender portal](https://security.microsoft.com), in the navigation pane, select **Settings** &gt; **Offboard**, and then select an operating system to start the offboarding process.

You can also use other methods, such as:

- [Offboard devices using a local script](configure-endpoints-script#offboard-devices-using-a-local-script)
- [Offboard devices using Group Policy](configure-endpoints-gp#offboard-devices-using-group-policy)
- [Offboard devices using Mobile Device Management tools](configure-endpoints-mdm#offboard-devices-using-mobile-device-management-tools)
- [Offboard devices using the API](api/offboard-machine-api)

## Offboard servers

In the [Microsoft Defender portal](https://security.microsoft.com), in the navigation pane, select **Settings** &gt; **Offboard**, and then select an operating system to start the offboarding process.

You can also use other methods, such as:

- [Offboard devices using Group Policy](configure-endpoints-gp#offboard-devices-using-group-policy)
- [Offboard devices using Configuration Manager](configure-endpoints-sccm#offboard-devices-using-configuration-manager)
- [Offboard devices using Mobile Device Management tools](configure-endpoints-mdm#offboard-devices-using-mobile-device-management-tools)
- [Offboard devices using a local script](configure-endpoints-script#offboard-devices-using-a-local-script)
- [Offboard devices using the API](api/offboard-machine-api)

## Offboard Mac devices

In the following procedure, steps 1 and 2 are optional if you do not want to see these devices that are retired in the "Device inventory" for 180 days.

1. Create a [device tag](machine-tags), and name the tag `decommissioned`. Assign the tag to the Mac devices that you want to offboard from Defender for Endpoint.
2. Create a [Device group](machine-groups) and name it something like, `Decommissioned Mac`. Assign this tag to an appropriate user group.
3. Remove policies for [Tamper Protection](tamper-protection-macos-configure). See [Set preferences on Mac: Tamper protection](mac-preferences#tamper-protection), or turn off tamper protection by using [local configuration](tamper-protection-macos-configure#configure-tamper-protection-locally).
4. In the [Microsoft Defender portal](https://security.microsoft.com), navigate to, **System** &gt; **Settings** &gt; **Endpoints** &gt; **Device management** &gt; **Offboarding**. Select **macOS** in Step 1, then choose your preferred deployment method, and select **Download package** to download the offboarding package.

    Or, if you're using a non-Microsoft device management solution, disable integration with Defender for Endpoint.
5. Uninstall the Defender for Endpoint app on Mac devices.
6. Remove Mac devices from the group for system extension policies if an MDM was used to set them.

## Offboard Android or iOS devices

To offboard an Android or iOS device, uninstall the Microsoft Defender app on the device.