---
layout: Conceptual
title: Microsoft Defender for Endpoint Device Control for macOS - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/mac-device-control-overview
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how Device Control for macOS manages removable storage and peripheral access, including requirements, policies, status, reporting, and limitations.
ms.service: defender-endpoint
author: limwainstein
ms.author: lwainstein
ms.reviewer: joshbregman
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-macos
ms.topic: overview
ms.subservice: macos
ms.date: 2026-09-17T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: 90235246-3247-435b-3070-b3be21dbf669
document_version_independent_id: 90235246-3247-435b-3070-b3be21dbf669
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/mac-device-control-overview.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mac-device-control-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/mac-device-control-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: cf75b793-8fa9-b809-1821-63f036b41cfa
---

# Microsoft Defender for Endpoint Device Control for macOS - Microsoft Defender for Endpoint | Microsoft Learn

Device control in Microsoft Defender for Endpoint on macOS helps protect organizational data by managing access to removable storage and connected devices. You can use device control to:

- Audit, allow, or prevent read, write, or execute access to removable storage.
- Manage access to iOS devices, portable devices, Apple File System (APFS)-encrypted devices, and Bluetooth media, with or without exclusions.

## Requirements

Before you configure device control, make sure you meet the following requirements:

- A subscription that includes Defender for Endpoint Plan 1 capabilities. For more licensing information, see:
    - [Microsoft 365 Enterprise plans comparison](https://go.microsoft.com/fwlink/p/?LinkID=2139145&amp;clcid=0x409&amp;culture=&amp;country=us)
    - [Understand subscriptions and licenses in Microsoft 365 for business](/en-us/microsoft-365/commerce/licenses/subscriptions-and-licenses)
- A supported version of macOS. For more information, see [Microsoft Defender for Endpoint on macOS system requirements](microsoft-defender-endpoint-mac-prerequisites#system-requirements).
- Defender for Endpoint version `101.96.85` (January 2023) or later.
- Defender for Endpoint installed and onboarded on the target macOS devices.

### Permissions

The permissions required to deploy a Device Control policy depend on the management tool:

- **Microsoft Intune**: An account with the **Policy and Profile Manager** role and scope over the users or devices that receive the policy. For more information, see [Policy and Profile Manager permissions](/en-us/intune/fundamentals/role-based-access-control/ref-built-in-roles#policy-and-profile-manager).
- **Jamf Pro**: An account that can update and deploy computer configuration profiles.

## Prepare your endpoints

Before you deploy a device control policy:

- Grant Full Disk Access to `com.microsoft.dlp.daemon`. The current [Full Disk Access configuration profile](https://github.com/microsoft/mdatp-xplat/blob/master/macos/mobileconfig/profiles/fulldisk.mobileconfig) includes this permission.
- In the Defender for Endpoint preferences, enable the Data Loss Prevention (DLP) feature named `DC_in_dlp` by setting its state to `enabled`.

Run the following command in Terminal to verify the Defender for Endpoint version:

```bash
mdatp version
```

## Choose a deployment method

Use one of the following methods to deploy or test a Device Control policy:

- **[Microsoft Intune](mac-device-control-configure#deploy-the-policy-by-using-microsoft-intune)**: Deploy the policy to managed devices by using an Intune custom macOS configuration profile.

    Microsoft Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).
- **[Jamf Pro](mac-device-control-configure#deploy-the-policy-by-using-jamf-pro)**: Deploy the policy to managed devices by using the Defender for Endpoint preference schema in a Jamf Pro computer configuration profile.

    Jamf Pro is a separate product that isn't part of Defender for Endpoint and isn't included with Defender for Endpoint subscriptions. For product and subscription information, see [Jamf Pro](https://www.jamf.com/products/jamf-pro/).
- **[Manual testing](mac-device-control-configure#test-the-policy-manually)**: Apply a local policy to one test Mac before you deploy the policy to managed devices.

## Understand device control policies

A device control policy for macOS is one JSON object with three required top-level properties:

- `settings`: Defines enabled device types, default enforcement, and the notification link.
- `groups`: Defines collections of devices based on properties such as device family, vendor ID, product ID, serial number, or encryption state.
- `rules`: Defines the access behavior for one or more device groups.

Note

Use the [Device Control policy samples](https://github.com/microsoft/mdatp-devicecontrol/tree/main/macOS/policy/samples) to understand the policy properties.

You can also use the [Device Control policy conversion scripts](https://github.com/microsoft/mdatp-devicecontrol/tree/main/python#readme) to translate a Windows policy to macOS or a macOS version 1 policy to version 2.

There are known issues with device control for macOS that customers should consider when creating policies.

### Best practices

Device Control for macOS and Device Control for Windows have similar capabilities, but the operating systems provide different ways to manage devices:

- macOS doesn't have a centralized Device Manager or device view. Device Control allows or denies access for applications that interact with devices. As a result, macOS provides more granular access types. For example, a `portableDevice` policy can allow or deny `download_photos_from_device`.
- Use `generic_read`, `generic_write`, and `generic_execute` unless you need to control a specific operation. Policies that use generic access types continue to cover more specific access types added later.
- To block all operations for a device type, create a `deny` policy that uses generic access types. Some operations might remain available if the application performing the operation isn't supported by Device Control for macOS.

## Device Control policy reference

Use the following sections to define the settings, groups, queries, clauses, rules, enforcement behavior, and access types in a Device Control policy.

### Settings

Use the `settings` object to enable device types, configure default enforcement, and add a link to notifications.

| Property | Description | Options |
| --- | --- | --- |
| `features` | Enables or disables Device Control for specific device types. | For each device type, set `disable` to `false` to enable protection or `true` to disable it. This article describes `removableMedia`, `appleDevice`, `portableDevice`, and `bluetoothDevice`. The default value is `true`. |
| `global` | Sets the action to use when no rule matches. | Set `defaultEnforcement` to `allow` (the default) or `deny`. |
| `ux` | Adds a link to Device Control notifications. | Set `navigationTarget` to a URL, such as `https://support.contoso.com`. |

### Group

The `groups` array contains one or more device-group objects.

| Property | Description | Options |
| --- | --- | --- |
| `$type` | Identifies the group type. | Use `device`. |
| `id` | Specifies the unique identifier for the group. | Use a universally unique identifier (UUID). Generate one by using the [New-Guid](/en-us/powershell/module/microsoft.powershell.utility/new-guid) cmdlet or the `uuidgen` command on macOS. |
| `name` | Specifies a friendly name for the group. | Use a string. |
| `query` | Defines the devices included in the group. | Use a binary or unary query. |

### Query

Device Control supports binary queries that combine clauses and unary queries that negate another query.

| `$type`value | Required property | Behavior |
| --- | --- | --- |
| `all` or `and` | `clauses` | The device must match every clause. |
| `any` or `or` | `clauses` | The device must match at least one clause. |
| `not` | `query` | Negates the nested query. |

You can nest queries. For more examples, see [sample policies](https://github.com/microsoft/mdatp-devicecontrol/blob/ae2e00ee7f12e024f931357b6e5a22bf589c4053/macOS/policy/samples/deny_removable_media_sc_cards.json#L17-L43).

### Clause

Each clause requires a `$type` property and a corresponding `value`.

| Clause`$type` | Value | Description |
| --- | --- | --- |
| `primaryId` | `apple_devices`, `removable_media_devices`, `portable_devices`, or `bluetooth_devices` | Matches a supported device family. |
| `vendorId` | Four-digit hexadecimal string | Matches a device's vendor ID. |
| `productId` | Four-digit hexadecimal string | Matches a device's product ID. |
| `serialNumber` | String | Matches a device's serial number. The clause doesn't match a device that has no serial number. |
| `mediaSerialNumber` | Integer | Matches the serial number of a Secure Digital card. Available in version `101.26021` or later. |
| `mediaProductName` | String | Matches the product name of a Secure Digital card. Available in version `101.26021` or later. |
| `mediaApplicationId` | String | Matches the application ID of a Secure Digital card. Available in version `101.26021` or later. |
| `encryption` | `apfs` | Matches an APFS-encrypted removable media device. |
| `groupId` | UUID string | Matches a device that belongs to another group. Define the referenced group earlier in the policy. |

The `serialNumber` clause applies to a connected device. The `mediaSerialNumber`, `mediaProductName`, and `mediaApplicationId` clauses apply to media inserted into a device, such as a Secure Digital card in a built-in card reader.

### Access policy rule

The `rules` array contains one or more access-policy rule objects.

| Property | Description | Options |
| --- | --- | --- |
| `id` | Specifies the unique identifier for the rule. | Use a UUID generated with [New-Guid](/en-us/powershell/module/microsoft.powershell.utility/new-guid) or `uuidgen`. |
| `name` | Specifies the rule name. The name can appear in a user notification. | Use a string. |
| `includeGroups` | Identifies groups that a device must belong to for the rule to apply. If omitted, the rule applies to all devices. | Use group `id` values. Multiple groups use AND logic. |
| `excludeGroups` | Identifies groups that prevent the rule from applying. | Use group `id` values. Multiple groups use OR logic. |
| `entries` | Defines the enforcement behavior and controlled access types. | Use one or more entry objects. |

Each entry supports the following properties:

| Property | Required | Description |
| --- | --- | --- |
| `$type` | Yes | Specifies `removableMedia`, `appleDevice`, `portableDevice`, `bluetoothDevice`, or `generic`. |
| `enforcement` | Yes | Specifies an `allow`, `deny`, `auditAllow`, or `auditDeny` enforcement object. |
| `access` | Yes | Specifies one or more device-specific or generic access types. |
| `id` | No | Specifies an optional UUID for the entry. |

### Enforcement

An enforcement object requires a `$type` property. Some enforcement types also support or require an `options` array.

| Enforcement`$type` | Supported`options`values | Behavior |
| --- | --- | --- |
| `allow` | `disable_audit_allow` | Allows access. The option prevents an event when a matching `auditAllow` entry is also configured. |
| `deny` | `disable_audit_deny` | Denies access. The option prevents a notification or event when a matching `auditDeny` entry is also configured. |
| `auditAllow` | `send_event` | Sends an event for allowed access. |
| `auditDeny` | `send_event` and `show_notification` | Sends an event or displays a notification for denied access. |

### Access types

The supported access types depend on the entry `$type`.

| Entry`$type` | Access value | Generic access | Description |
| --- | --- | --- | --- |
| `appleDevice` | `backup_device` | `generic_read` |  |
| `appleDevice` | `update_device` | `generic_write` |  |
| `appleDevice` | `download_photos_from_device` | `generic_read` | Downloads photos from an iOS device to the local device. |
| `appleDevice` | `download_files_from_device` | `generic_read` | Downloads files from an iOS device to the local device. |
| `appleDevice` | `sync_content_to_device` | `generic_write` | Syncs content from the local device to an iOS device. |
| `portableDevice` | `download_files_from_device` | `generic_read` |  |
| `portableDevice` | `send_files_to_device` | `generic_write` |  |
| `portableDevice` | `download_photos_from_device` | `generic_read` |  |
| `portableDevice` | `debug` | `generic_execute` | Controls Android Debug Bridge (ADB) access. |
| `removableMedia` | `read` | `generic_read` |  |
| `removableMedia` | `write` | `generic_write` |  |
| `removableMedia` | `execute` | `generic_execute` |  |
| `bluetoothDevice` | `download_files_from_device` | `generic_read` |  |
| `bluetoothDevice` | `send_files_to_device` | `generic_write` |  |
| `generic` | `generic_read` |  | Applies to every access type mapped to generic read. |
| `generic` | `generic_write` |  | Applies to every access type mapped to generic write. |
| `generic` | `generic_execute` |  | Applies to every access type mapped to generic execute. |

## End-user experience

When a policy denies an operation and the matching `auditDeny` entry includes `show_notification`, the user sees a Device Control notification that identifies the restricted device.

If the policy defines `settings.ux.navigationTarget`, the notification includes a link to that URL.

## Verify Device Control

After you deploy a policy, verify Device Control status and confirm that the expected preferences, rules, and groups are active. For instructions, see [Verify Device Control](mac-device-control-configure#verify-device-control).

## View Device Control reports

Device Control policy events are available in advanced hunting and the Device Control report. For more information, see [View device control events and information](device-control-report).

## Use policy samples

The [Device Control policy samples](https://github.com/microsoft/mdatp-devicecontrol/tree/main/macOS/policy/samples) provide complete policies for common scenarios.

### Deny removable media except approved USB devices

The [deny removable media except Kingston sample](https://github.com/microsoft/mdatp-devicecontrol/blob/main/macOS/policy/samples/deny_removable_media_except_kingston.json) demonstrates how to:

- Enable removable-media protection and set default enforcement to `allow`.
- Create one group for all removable media and another group for approved devices.
- Deny read, write, and execute access to removable media except devices in the approved group.
- Audit denied operations, send events, and show user notifications.

## Known issues

Warning

On macOS 27, a local user can turn off Bluetooth access for Microsoft Defender for Endpoint even when a mobile device management (MDM) profile grants the `BluetoothAlways` permission to `com.microsoft.dlp.agent`. If the user turns off this permission, Device Control can't enforce policies that restrict Bluetooth file transfers, although the MDM profile might continue to report that the permission is allowed.

If your organization relies on Device Control to restrict Bluetooth file transfers:

- Validate Bluetooth policy enforcement in your environment before broadly deploying macOS 27.
- Don't use the MDM profile's installed or allowed status as the only confirmation that Bluetooth enforcement is active.
- Advise users not to change the Microsoft Defender Bluetooth permission in **System Settings &gt; Privacy & Security &gt; Bluetooth**.

For information about related user-controllable permissions in macOS 27 and protection options for browser and website context, see [Microsoft Purview Endpoint DLP changes in macOS 27 overview (preview)](/en-us/purview/endpoint-dlp-macos-27-changes). The protection modes described in the Purview guidance don't prevent users from disabling the Bluetooth permission.

Warning

Device Control on macOS restricts Android devices only when they're connected in Picture Transfer Protocol (PTP) mode. Device Control doesn't restrict File Transfer, USB Tethering, or MIDI modes.

Device Control on macOS doesn't prevent software developed in Xcode from being transferred to an external device.