---
layout: Conceptual
title: Explore devices in the device inventory - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/machines-view-overview
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to view, customize, and manage devices in the Microsoft Defender for Endpoint device inventory.
keywords: device inventory, explore devices, view devices, filter devices, device list, device management, device details
ms.service: defender-endpoint
ms.author: lwainstein
author: limwainstein
ms.reviewer: yongrhee
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.topic: how-to
search.appverid: met150
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: b4db3314-8cea-fa8e-2043-fd83a062e1ec
document_version_independent_id: b4db3314-8cea-fa8e-2043-fd83a062e1ec
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/machines-view-overview.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: machines-view-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/machines-view-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 186f6aa2-b99e-f08b-8364-2ffb7afd020c
---

# Explore devices in the device inventory - Microsoft Defender for Endpoint | Microsoft Learn

The **Device inventory** is the authoritative source for all devices visible to Microsoft Defender for Endpoint. It shows devices that are onboarded (with the full agent installed) and devices discovered on your network through the [device discovery overview](device-discovery).

This article explains how to view, customize, and manage devices in your device inventory.

To understand how devices appear in the inventory through onboarding and discovery, including IoT/OT devices and discovery sources, see [Devices in Microsoft Defender for Endpoint](devices-overview).

## View devices in the device inventory

Access the device inventory and review the devices in your environment.

### Navigate to the device inventory

In the Defender portal, go to **Assets** &gt; **Devices** or, to go directly to the **Device inventory** page, use https://security.microsoft.com/machines.

### Review device information and counts

The device inventory opens on the **All devices** tab. You can see information such as device name, domain, risk level, exposure level, OS platform, criticality level, onboarding status, sensor health state, mitigation status, and other details for easy identification of devices most at risk.

Note

The device inventory is available in Microsoft Defender services. The available information might differ depending on your license. To get the most complete set of device inventory capabilities, use [Microsoft Defender for Endpoint Plan 2](microsoft-defender-endpoint).

Risk Level, which can influence enforcement of Conditional Access and other security policies in Microsoft Intune, is available for Windows devices.

When you open the device inventory, you can:

- **View device categories**: Switch between tabs (All devices, Computers & mobile, Network devices, IoT/OT, Uncategorized) to focus on specific device types.
- **Review device counts**: Check the count pills at the top of each tab (total, critical assets, high risk, high exposure, not onboarded, newly discovered) to prioritize your work.
- **View special cards**: Classify critical assets or check for attack path warnings.
- **Check device details**: View columns like risk level, exposure level, onboarding status, sensor health, managed by, tags, and more for each device.

Note

Device discovery integration with [Microsoft Defender for IoT in the Defender portal (Preview)](/en-us/defender-for-iot/microsoft-defender-iot) is available to help locate, identify, and secure your complete OT/IOT asset inventory. Devices discovered with this integration appear on the **IoT/OT devices** tab.

With Defender for IoT, you can also view and manage Enterprise IoT devices (like printers, smart TVs, and conferencing systems) as part of enterprise IoT monitoring. For more information, see [Enable Enterprise IoT security with Defender for Endpoint](/en-us/azure/defender-for-iot/organizations/eiot-defender-for-endpoint/).

## Customize device inventory views

Customize how you view devices in the inventory by adding or removing columns, applying filters, searching, and exporting data.

### Search for devices

Use the following search options to find devices in the inventory.

| Task | Steps |
| --- | --- |
| **Search by device name** | Use the search box at the top of the device inventory to find a device by name. |
| **Search by IP address** | Search for a device by the most recently used IP address or IP address prefix. |
| **Search by MAC address** | Search for a device by its MAC address. |

### Customize columns

Choose which columns to display in your device inventory view.

1. Select ![](media/defender-portal-icon-customize.png)**Customize columns** at the top of the device inventory.
2. Select or clear the checkboxes for columns you want to show or hide. The changes apply immediately.

Default columns vary by tab.

Tip

To see all columns, you likely need to do one or more of the following steps:

- Horizontally scroll in your web browser.
- Narrow the width of appropriate columns.
- Zoom out in your web browser.

### Apply filters

Use filters to narrow down the list of devices and focus on specific device categories.

1. Select the **Filter** icon at the top-right of the device inventory.
2. In the filter panel, select a filter category (for example, **Risk level**, **Onboarding status**, **Tags**).
3. Select or enter the values you want to filter by.
4. Select **Apply**. Active filters appear as pills at the top of the device inventory. Select the **X** on a pill to remove that specific filter, or select **Clear all filters** in the filter panel to reset.

Note

If you're not seeing some devices, try clearing your filters.

To clear your filters, navigate to the top-right of the **Devices list** and select the **Filter** icon. On the flight-out pane, select the **Clear all filters** button.

### Recommendation and device inventory sync considerations

Here are a few common filter scenarios to get you started:

- Filter by **Risk level** &gt; **High** to find devices that need immediate investigation.
- Filter by **Onboarding status** &gt; **Can be onboarded** to find discovered devices ready for agent deployment.
- Filter by **Tags** to scope the view to a specific business group (for example, `Finance` or `HQ-Building-A`).
- Filter by **Managed by** &gt; **Unknown** to identify unmanaged devices.

### Sort devices

Use column headers to sort the device list by one or more fields.

1. Select any column header to sort devices by that column. Select the header again to reverse the sort order.
2. To sort by multiple columns, hold **Shift** and select additional column headers.

### Export device list

Export the device inventory to a CSV file for offline review or reporting.

1. Select **Export** at the top of the device inventory.
2. Wait for the export to complete. For large organizations, the export might take time.
3. Download the CSV file containing all devices in your organization.

Note

The exported CSV contains unfiltered data for all devices in the organization, regardless of any filters applied in the UI.

Antivirus status shows as `Not-Supported` in the export. For antivirus status, use the [Microsoft Defender Antivirus health report](device-health-microsoft-defender-antivirus-health) instead.

Tip

The API, UI, export, and Advanced Hunting (AH) interfaces all draw from a single authoritative data source. However, because each is powered by separate backend systems with different update frequencies, slight variations may appear across views—especially in short-term queries or recently reactivated devices. The export interface is optimized for large data retrieval, the UI for fast interactive tasks like tag management, and Advanced Hunting for tracking device update history over time.

## Common device inventory tasks

Use the device inventory to perform common security tasks.

| Task | Description | Steps |
| --- | --- | --- |
| **Identify high-risk devices** | Find devices with active alerts or high risk levels | 1. Sort by **Risk level** column (descending)2. Or use **Risk level** filter to show only High risk devices3. Review devices and take appropriate actions |
| **Track onboarding progress** | Monitor which devices are onboarded vs. discovered | 1. Use **Onboarding status** filter2. Select **Can be onboarded** to see discovered devices that should be onboarded3. Initiate onboarding for high-priority devices |
| **Find devices needing attention** | Identify devices with security configuration issues | 1. Sort by **Exposure level** column (descending)2. Review devices with High exposure3. Check security recommendations on device pages |
| **Monitor sensor health** | Check which devices have healthy sensors | 1. Use **Sensor health state** filter2. Select **Inactive** or **Misconfigured** to find problem devices3. Follow [Fix unhealthy sensors](fix-unhealthy-sensors) guidance |
| **View internet-facing devices** | Identify devices exposed to the internet | 1. Use **Tags** column or filter to find devices with "internet-facing" tag2. Or use **Internet facing** filter (if available)3. Review these devices for additional security measures |
| **Manage transient devices** | View or hide devices that appear intermittently | 1. Use **Transient device** filter2. Select **Yes** to view only transient devices3. Select **No** to exclude them from view4. See [Manage device scope and relevance](manage-device-scope-relevance) |
| **Review excluded devices** | Check which devices are excluded from vulnerability management | 1. Use **Exclusion state** filter2. Select **Excluded** to view excluded devices3. Review exclusion details and stop exclusion if needed |
| **Organize devices by tags** | Group and filter devices using custom tags | 1. Use **Tags** filter to view devices with specific tags2. Add **Tags** column to see all device tags3. See [Create and manage device tags](machine-tags) |
| **Focus on critical assets** | View only business critical devices | 1. Use **Criticality level** filter2. Select **Very high** to see business critical assets3. Review critical asset counts at the top of the tab |
| **Filter by management method** | View devices managed by specific tools | 1. Use **Managed by** filter2. Select Intune, ConfigMgr, MDE, or Unknown3. Review management status for compliance |