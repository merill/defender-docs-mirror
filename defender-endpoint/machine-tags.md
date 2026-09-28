---
layout: Conceptual
title: Create and manage device tags and target devices - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/machine-tags
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use device tags, device groups, and targeting to organize devices and apply security actions at scale in Microsoft Defender for Endpoint.
keywords: device tags, device groups, target devices, manage tags, organize devices, device targeting, security actions, dynamic tags
ms.service: defender-endpoint
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.topic: how-to
ms.custom: api
ms.subservice: reference
search.appverid: met150
ms.date: 2026-02-25T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 5d9f7855-ca12-701e-9710-d9c0646d908b
document_version_independent_id: 5d9f7855-ca12-701e-9710-d9c0646d908b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/machine-tags.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: machine-tags
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/machine-tags.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
platformId: c2b5a7f9-e95a-86d8-5d46-47d76a89d153
---

# Create and manage device tags and target devices - Microsoft Defender for Endpoint | Microsoft Learn

Device targeting in Microsoft Defender for Endpoint follows two stages: first you **create tags** to label devices with business context, then you **form device groups** based on those tags to target security operations at scale — such as role-based access, custom data collection, automation rules, and attack surface reduction policies.

## Prerequisites

Before you create tags and target devices, review the following requirements.

### Permissions

- **Dynamic tags**: Requires appropriate permissions in [Asset Rule Management](/en-us/defender-xdr/configure-asset-rules).
- **Manual tags**: Requires device-level permissions in the Defender portal.
- **Automation rules**: Requires rule creation permissions.
- **Device groups**: Requires Security Administrator role to create and manage groups.

### Supported operating systems

Device tagging is supported on:

- Windows 11, Windows 10 (version 1709 or later), Windows 8.1, Windows 7 SP1
- Windows Server (version 1803 or later), Windows Server 2016, Windows Server 2012 R2, Windows Server 2008 R2 SP1
- macOS, Linux, iOS, Android

### Performance notes

- Each device can have multiple tags.
- Dynamic tags update approximately every hour.
- There might be some latency between the time a tag is added to a device and its availability in the devices list and device page.
- Large numbers of tags don't significantly affect performance.
- Custom data collection rules can target multiple tag combinations.

For background on tags vs. groups, dynamic vs. manual tags, and targeting scenarios, see [Device targeting](devices-overview#device-targeting).

## Create tags

You can add tags to devices using the following methods. Each method is suited for different scenarios and device platforms.

| Method | Platform | Steps |
| --- | --- | --- |
| **Portal** | All supported platforms | Manually add tags to individual devices or small groups. See Add device tags using the portal. |
| **Dynamic rules** | All supported platforms | Create rules in the Defender portal that automatically assign and remove tags based on device properties. See [Asset rule management - Dynamic rules for devices](/en-us/defender-xdr/configure-asset-rules). |
| **Registry key** | Windows | Set registry key `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Advanced Threat Protection\DeviceTagging\` with REG\_SZ value `Group` containing the tag name (max 200 characters). Tags sync once daily; restart the device for immediate sync. To remove a tag, clear the value data instead of deleting the `Group` key. |
| **Security settings management** | macOS, Linux | Create an Endpoint detection and response security policy. See [Manage endpoint security policies on MDE-onboarded devices](/en-us/mem/intune/protect/mde-security-integration) and [Manage endpoint security policies in Defender for Endpoint](endpoint-security-policies-configure). |
| **Configuration profile** | macOS, Linux | **macOS**: Create a `.plist` configuration profile and deploy it manually or through a management tool. See [Set preferences for MDE on macOS](mac-preferences) and [Custom settings for macOS in Intune](/en-us/mem/intune/configuration/custom-settings-macos). **Linux**: Create a `.json` configuration profile. See [Set preferences for MDE on Linux](linux-preferences). |
| **Custom Intune profile** | Windows 10 or later | Create a device configuration profile with custom settings in Intune. Use OMA-URI `./Device/Vendor/MSFT/WindowsAdvancedThreatProtection/DeviceTagging/Group` with data type **String**. See [Create a profile with custom settings in Intune](/en-us/mem/intune/configuration/custom-settings-configure). |
| **App configuration policy in Intune** | iOS, Android | Create an app configuration profile in Intune to define and apply tags for mobile devices. **For iOS**, see [Configure Microsoft Defender for Endpoint on iOS features](ios-configure-features). **For Android**, see [Configure Defender for Endpoint on Android features](android-configure). For more information, see [Tag mobile devices with Microsoft Defender for Endpoint](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/announcing-mobile-device-tagging-for-ios-and-android/ba-p/3897368). |

Note

Device group creation is supported in Defender for Endpoint Plan 1 and Plan 2.

To add device tags using API, see [Add or remove device tags API](api/add-or-remove-machine-tags).

### Add device tags using the portal

To add tags to a device in the Defender portal, follow these steps:

1. Select the device that you want to manage tags on. You can select or search for a device from any of the following views:

    - **Alerts queue** - Select the device name beside the device icon from the alerts queue.
    - **Devices inventory** - Select the device name from the list of devices.
    - **Search box** - Select Device from the drop-down menu and enter the device name.

        You can also select a device from the file and IP address views.
2. Select **Manage tags** from the row of Response actions.

    [![Image of manage tags button](media/manage-tags-option.png)](media/manage-tags-option.png#lightbox)
3. Type to find or create tags.

    [![Adding tags on device1](media/create-new-tag.png)](media/create-new-tag.png#lightbox)

Tags are added to the device view and are also reflected on the **Devices inventory** view. You can then use the **Tags** filter to see the relevant list of devices.

Note

Filtering might not work on tag names that contain parenthesis or commas.

When you create a new tag, a list of existing tags is displayed. The list only shows tags created through the portal. Existing tags created from client devices aren't displayed.

You can also delete tags from the device page.

[![Adding tags on device2](media/new-tag-label-display.png)](media/new-tag-label-display.png#lightbox)

## Create device groups

After you tag devices, use device groups to control which security teams can access and manage specific sets of devices. Device groups use matching rules — often based on tags — to determine membership, and they enable role-based access control, automated remediation levels, and scoped security policies.

For step-by-step instructions on creating, ranking, and managing device groups, see [Create and manage device groups](machine-groups).

## Apply security actions

Once your devices are organized with tags and groups, you can target security operations at scale. Device groups and tags power capabilities including investigations and threat hunting, custom data collection, automation rules, role-based access, attack surface reduction rules, and Conditional Access policies.

For the full list of security actions you can target to device groups, including scenarios and links, see [Security actions powered by targeting](devices-overview#security-actions-powered-by-targeting).