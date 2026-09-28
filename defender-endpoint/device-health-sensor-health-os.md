---
layout: Conceptual
title: Device health sensor health and OS report in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/device-health-sensor-health-os
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use the Sensor health and OS device health report in Microsoft Defender for Endpoint to monitor sensor health, antivirus status, OS platforms, and Windows version trends.
ms.service: defender-endpoint
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.date: 2026-07-03T00:00:00.0000000Z
ms.collection:
- m365-security
- tier2
ms.topic: how-to
ms.subservice: ngp
ms.reviewer: mkaminska
ms.custom: sfi-ga-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: bbd10119-1597-e3eb-96cd-244cf45adf0a
document_version_independent_id: bbd10119-1597-e3eb-96cd-244cf45adf0a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/device-health-sensor-health-os.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: device-health-sensor-health-os
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/device-health-sensor-health-os.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/e0ffb20c-01c6-407b-a9bd-29111652a1dc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/3904bce4-d817-48cf-85fd-b6146fca83b7
platformId: 0e0d81e0-e8a7-c6b5-2a61-06a363663882
---

# Device health sensor health and OS report in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

The Device Health report provides information about the devices in your organization. The report includes trending information showing the sensor health state, antivirus status, OS platforms, Windows 10 versions, and Microsoft Defender Antivirus update versions.

Important

For Windows Server 2012 R2 and Windows Server 2016 to appear in device health reports, these devices must be onboarded using the modern unified solution package. For more information, see [New functionality in the modern unified solution for Windows Server 2012 R2 and 2016](onboard-server#functionality-in-the-modern-unified-solution-for-windows-server-2016-and-windows-server-2012-r2).

In the Microsoft Defender portal, select **Reports**, and then open **Device health and compliance**.

- The **Sensor health & OS** tabprovides general operating system information, divided into three cards that display the following device attributes:
    - Sensor health card
    - Operating systems and platforms card
    - Windows versions card

## Report access permissions

To access the Device health and antivirus compliance report in the Microsoft Defender portal, the following permissions are required:

| Permission name | Permission type |
| --- | --- |
| View Data | Threat and vulnerability management (TVM) |

Important

Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

To assign these permissions:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com) using account with Security administrator or Global administrator role assigned.
2. In the navigation pane, select **Settings** &gt; **Endpoints** &gt; **Roles** (under **Permissions**).
3. Select the role you'd like to edit.
4. Select **Edit**.
5. In **Edit role**, on the **General** tab, in **Role name**, type a name for the role.
6. In **Description** type a brief summary of the role.
7. In **Permissions**, select **View Data**, and under **View Data** select **Threat and vulnerability management** (TVM).

For more information about user role management, see [Create and manage roles for role-based access control](user-roles).

## Sensor health and operating system tab

Sensor health and operating system (OS) cards report on general operating system health, which includes detection sensor health, up to date versus out-of-date operating systems, and Windows 10 versions.

> 
> [![Shows Sensor health and Operating system information.](media/device-health-sensor-health-os-tab.png)](media/device-health-sensor-health-os-tab.png#lightbox)

Each of the three cards on the **Sensor health** tab has two reporting sections, *Current state* and *device trends*, presented as graphs:

### Current state graph overview

In each card, the Current state (referred to in some documentation as *Device summary*) is the top, horizontal bar graph. Current state is a snapshot that shows information collected about devices in your organization, scoped to the current day. The Current state graph represents the distribution of devices across your organization that report status or are detected to be in a specific state.

> 
> [![Shows the current state graph.](media/device-health-sensor-health-os-current-state-graph.png)](media/device-health-sensor-health-os-current-state-graph.png#lightbox)

### Device trends graph overview

The lower graph on each of the three cards isn't named, but is commonly known as *device trends*. The device trends graph depicts the collection of devices across your organization, throughout the time span indicated directly above the graph. By default, the device trends graph displays device information from the 30-day period, ending in the latest full day. To gain a better perspective about trends occurring in your organization, you can fine-tune the reporting period by adjusting the time period shown. To adjust the time period, open the filter and select a start day and end day.

> 
> [![Shows the Device Health versions trends graph.](media/device-health-sensor-health-os-device-trends-graph.png)](media/device-health-sensor-health-os-device-trends-graph.png#lightbox)

### Use data filters to refine report results

Use the provided filters to include or exclude devices with certain attributes. You can select multiple filters to apply from the device attributes. When filters are applied, they affect all three cards in the report.

For example, to show data about Windows 10 devices with Active sensor health state:

1. Under **Filters** &gt; **Sensor health state** &gt; **Active**.
2. Then select **OS platforms** &gt; **Windows 10**.
3. Select **Apply**.

### Sensor health card overview

The Sensor health card displays information about the sensor state on devices. Sensor health provides an aggregate view of devices that are:

- active
- inactive
- experiencing impaired communications
- or where no sensor data is reported

Devices that are either experiencing impaired communications, or devices from which no sensor data is detected could expose your organization to risks, and warrant investigation. Likewise, devices that are inactive for extended periods of time could expose your organization to threats due to out-of-date software. Devices that are inactive for long periods of time also warrant investigation.

Note

In a small percentage of cases, the numbers and distributions reported when clicking on the horizontal Sensor health bar graph will be out of synch with the values shown in the **Device inventory** page. The disparity in values can occur because the Sensor Health Reports has a different refresh cadence than the Device Inventory page.

### Operating systems and platforms card overview

The Operating systems and platforms card shows the distribution of operating systems and platforms that exist within your organization. *OS systems and platforms* can give useful insights into whether devices in your organization are running current or outdated operating systems. When new operating systems are introduced, security enhancements are frequently included that improve your organization's posture against security threats.

For example, Secure Boot (introduced in Windows 8) practically eliminated the threat from some of the most harmful types of malware. Improvements in Windows 10 provide PC manufacturers the option to prevent users from disabling Secure Boot. Preventing users from disabling Secure Boot removes almost any chance of malicious rootkits or other low-level malware from infecting the boot process.

Ideally, the "Current state" graph shows that the number of operating systems is weighted in favor of more current OS over older versions. If the current state graph is not weighted toward newer operating systems, the trends graph should indicate that new systems are being adopted and/or older systems are being updated or replaced.

### Windows versions card overview

The Windows 10 versions card shows the distribution of Windows devices and their versions in your organization. In the same way that an upgrade from Windows 8 to Windows 10 improves security in your organization, changing from early releases of Windows to more current versions improves your posture against possible threats.

The Windows version trend graph can help you quickly determine whether your organization is keeping current by updating to the most recent, most secure versions of Windows 10.