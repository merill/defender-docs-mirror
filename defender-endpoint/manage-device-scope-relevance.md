---
layout: Conceptual
title: Manage device scope and relevance in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/manage-device-scope-relevance
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Control which devices are relevant to your security operations through automatic transient tagging and manual device exclusion.
keywords: device scope, device relevance, exclude devices, transient devices, device exclusion, transient tagging, device inventory, manage devices
ms.service: defender-endpoint
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
audience: ITPro
ms.collection:
- m365-security
- tier2
ms.topic: how-to
search.appverid: met150
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 2806b448-0e7c-63cf-5ff3-a6bf0c55590c
document_version_independent_id: 2806b448-0e7c-63cf-5ff3-a6bf0c55590c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/manage-device-scope-relevance.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: manage-device-scope-relevance
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/manage-device-scope-relevance.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cd48b104-e308-4e08-a405-66f04a7df418
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ac23bdb5-c078-4620-8ee2-60eba45e97f8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: dedab41d-6951-459b-c12a-eca004460e07
---

# Manage device scope and relevance in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Not all devices discovered in your network require the same level of security attention. Some devices appear briefly on the network (guests, test devices), while others are permanently out of scope for vulnerability management (isolated labs, decommissioned systems). This article explains how to use transient device tagging and device exclusions to manage which devices are in scope for vulnerability management. Managing device scope with these tools keeps your security team focused on relevant devices, ensures accurate exposure and secure scores, and produces cleaner reports that reflect your true production environment.

## Use tags or exclusions

Defender for Endpoint provides two complementary mechanisms for managing device relevance. Use the following table to determine which approach fits your situation.

| Situation | Approach | How it works | Impact |
| --- | --- | --- | --- |
| Devices appear and disappear frequently (guests, test VMs, short-lived containers) | **Transient device tagging** (automatic) | An internal algorithm detects intermittent network patterns and tags matching devices. Servers, network devices, printers, industrial and smart-facility devices are never tagged as transient. | Transient devices are filtered out of the default inventory view but remain visible if you change the filter. Exposure score, secure score, vulnerability reports, and advanced hunting still include these devices. |
| Permanent lab or sandbox environment | **Device exclusion** (manual) | You exclude devices individually or in bulk with a documented justification. | Excluded devices don't appear in vulnerability management pages or reports, and don't contribute to exposure or secure scores. They remain in the device inventory but are marked as excluded. |
| Devices scheduled for decommissioning | **Device exclusion** (manual) | Exclude with a justification and note about the planned retirement date. | Excluded devices don't appear in vulnerability management pages or reports, and don't contribute to exposure or secure scores. Historical records remain in the inventory. |
| Duplicate entries after reimaging | **Device exclusion** (manual) | Exclude the obsolete entries with a "Duplicate device" justification; keep the active device in scope. | Cleans up inventory and ensures accurate device counts. |
| Devices offline for extended periods | Check if already transient-tagged; if not, consider exclusion | Transient tagging might already handle this scenario. Exclude manually only if the device won't return. | Depends on chosen approach. |
| Active devices you want to ignore temporarily | **Device filters or custom tags** | Use inventory filters or [create and manage device tags](machine-tags) to create targeted views. | Full visibility is maintained. Never exclude active devices—that creates blind spots. |
| Devices managed by a different team | **Device filters or custom tags** | Use device tags and filters to scope views per team. | Full visibility is maintained across the organization. |

Important

Review transient-tagged and excluded devices regularly. Always add meaningful notes when excluding devices. Never exclude active, network-connected devices—exclusion only affects vulnerability management visibility, not actual risk.

## View and manage transient devices

Transient device tagging is automatic and can't be disabled. You control visibility through filters.

### View transient devices in the inventory

To view transient devices in the device inventory, follow these steps:

1. In the [Microsoft Defender portal](https://security.microsoft.com), go to **Assets** &gt; **Devices**.
2. Select the **Filter** icon.
3. In the **Transient device** filter, select **Yes** to view only transient devices, or select **No** to exclude them from the list.

You can also add the **Transient device** column to your inventory view to see the transient status alongside other device details.

### How transient tagging works

The following points explain how transient tagging behaves in Defender for Endpoint:

- **Automatic detection**: An internal algorithm identifies transient devices based on network appearance patterns.
- **Excluded device types**: Servers, network devices, printers, industrial devices, surveillance equipment, smart facility devices, and smart appliances are never tagged as transient.
- **Default filtering**: Transient devices are filtered out of the device inventory by default.
- **No manual override**: You can't manually tag or untag a device as transient. Adjust filter settings to control visibility.

## Exclude devices

Device exclusion lets you manually remove specific devices from vulnerability management visibility. Excluded devices remain in the device inventory (marked as excluded) but don't appear in vulnerability management pages or reports, and don't contribute to exposure or secure scores.

Warning

Excluded devices remain connected to the network and can still present security risks. Device exclusion only affects vulnerability management visibility—it doesn't prevent attacks or reduce actual risk. If you attempt to exclude an active device, Defender for Endpoint displays a warning and asks for confirmation.

### Exclude a single device

To exclude a single device from vulnerability management visibility, follow these steps:

1. In the [Microsoft Defender portal](https://security.microsoft.com), go to **Assets** &gt; **Devices**.
2. Select the device you want to exclude.
3. In the device flyout or on the device page, select **Exclude**.
4. Select a justification:
    - Inactive device
    - Duplicate device
    - Device doesn't exist
    - Out of scope
    - Other
5. Type a note explaining the reason for exclusion.
6. Select **Exclude device**.

![Screenshot of the exclude device dialog with justification options.](media/exclude-device.png)

### Exclude multiple devices

Note

It can take up to 10 hours for devices to be fully excluded from vulnerability management views and data.

To exclude multiple devices at once, complete the following steps:

1. In the **Device inventory**, select multiple devices using the checkboxes.
2. From the action bar, select **Exclude**.
3. Choose a justification and add a note.
4. Select **Exclude devices**.

If you select devices with mixed exclusion statuses, the dialog shows how many are already excluded. You can re-exclude devices, but the new justification overrides previous values.

![Screenshot of bulk device exclusion showing multiple selected devices.](media/exclude-device-bulk.png)

### View and manage excluded devices

To view excluded devices in the inventory, use the following steps:

1. In the **Device inventory**, select the **Filter** icon.
2. Use the **Exclusion state**filter to view:
    - **Not excluded**: Normal devices
    - **Excluded**: Devices removed from vulnerability management

You can also add the **Exclusion state** column to your inventory view.

### Stop excluding a device

Note

After you stop excluding a device, vulnerability data reappears in vulnerability management pages, reports, and advanced hunting. Changes can take up to 8 hours to take effect.

To restore a device to active vulnerability management:

1. In the **Device inventory**, select the excluded device.
2. In the device flyout, select **Exclusion details**.
3. Select **Stop exclusion**.

![Screenshot showing exclusion details with option to stop exclusion.](media/exclusion-details.png)