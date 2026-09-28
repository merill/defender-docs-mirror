---
layout: Conceptual
title: Troubleshoot Microsoft Defender for Endpoint NetExt on macOS - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/mac-troubleshoot-netext-mde
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Temporarily disable and restore the Microsoft Defender for Endpoint network extension to investigate network latency on macOS devices.
ms.service: defender-endpoint
author: paulinbar
ms.author: painbar
ms.reviewer: joshbregman
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-macos
ms.topic: troubleshooting-general
ms.subservice: macos
ms.date: 2026-09-18T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: 2b922ef2-729d-edd4-caf5-1f2e78585044
document_version_independent_id: 2b922ef2-729d-edd4-caf5-1f2e78585044
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/mac-troubleshoot-netext-mde.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mac-troubleshoot-netext-mde
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/mac-troubleshoot-netext-mde.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/a72e95ff-4b4f-4cc1-90c6-7dcba67ff05f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/24dc3ccd-591a-4415-a1fe-8759afafcb12
platformId: e0766c78-24d5-f5a1-7146-28839c08ec4e
---

# Troubleshoot Microsoft Defender for Endpoint NetExt on macOS - Microsoft Defender for Endpoint | Microsoft Learn

The Microsoft Defender for Endpoint network extension (NetExt) inspects network traffic for network protection, web content filtering, custom indicators, network events, and Microsoft Defender for Cloud Apps integration. Temporarily disable NetExt on a small set of test devices to determine whether it contributes to network latency.

Disabling NetExt removes the network inspection and enforcement provided by these features. Restore the network extension immediately after testing. For more information about the affected capabilities, see [Network protection for macOS](network-protection-macos).

## Identify network latency symptoms

Use this troubleshooting process when macOS devices experience unexpected network latency during activities such as:

- Browsing websites.
- Copying files over the network.
- Using chat, calling, or meeting applications.

Before disabling NetExt, confirm that the device meets the [Defender for Endpoint on macOS prerequisites](microsoft-defender-endpoint-mac-prerequisites) and uses a supported product version. Investigate other network components, such as virtual private network (VPN), proxy, firewall, and content-filtering software, that might also affect performance.

## Temporarily disable the network extension

Choose the method that matches how the network filter profile is managed:

- Microsoft Intune.
- Jamf Pro.
- Manual configuration.

Important

Limit this test to affected devices and the shortest practical test period. Exclude only the network filter profile that deploys `netfilter.mobileconfig` or an equivalent `com.apple.webcontent-filter` payload for `com.microsoft.wdav.netext`. Don't exclude system extension approval, Full Disk Access, onboarding, antivirus settings, or other Defender profiles.

## Temporarily disable NetExt with Microsoft Intune

> 
> Microsoft Intune is the recommended tool for configuring and distributing Defender for Endpoint features to devices. However, Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have Intune, you can use any of the other methods in this article. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

This procedure uses the Microsoft Intune admin center at https://intune.microsoft.com.

Create a temporary device group, and exclude the group from the Defender network filter profile:

### Create the temporary device group

1. Follow [Add groups to organize users and devices for Microsoft Intune](/en-us/intune/fundamentals/tenant-administration/add-groups) to create an assigned security group named `Devices with NetExt disabled`.
2. Add only the affected macOS devices to the group.

### Exclude the group from the network filter profile

1. On the **Devices | Configuration** page in the Microsoft Intune admin center at [https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/configuration](https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/DevicesMenu/%7E/configuration), select the profile that deploys the Defender network filter. The profile might be named `NetFilter-prod-macOS-Default-MDE`.
2. Open **Properties**, and then edit **Assignments**.
3. Under **Excluded groups**, add `Devices with NetExt disabled`.
4. Select **Review + save**, and then select **Save**.

For more information about profile exclusions, see [Assign device profiles in Microsoft Intune](/en-us/intune/device-configuration/assign-device-profile).

### Synchronize and test the devices

Wait for the affected devices to receive the updated profile assignment. Confirm that the network filter profile is no longer installed, and then try to reproduce the latency.

## Temporarily disable NetExt with Jamf Pro

> 
> Jamf Pro is a separate third-party product that isn't part of Defender for Endpoint and isn't included with Defender for Endpoint subscriptions. To use Jamf Pro, your organization needs a separate Jamf Pro subscription. For product and subscription information, see [Jamf Pro](https://www.jamf.com/products/jamf-pro/). If your organization doesn't use Jamf Pro, use another configuration method in this article, if available.

Use the current Jamf Pro instructions for [creating a static group](https://learn.jamf.com/r/jamf-pro-documentation-current/Creating_a_Static_Group) and [editing the scope of a computer configuration profile](https://learn.jamf.com/r/jamf-pro-documentation-current/Editing_the_Settings_or_Scope_of_a_Configuration_Profile_macOS):

1. Create a static computer group named `Devices with NetExt disabled`, and add the devices where you want to temporarily disable NetExt.
2. Edit the scope of the configuration profile that deploys the Defender network filter.
3. Add `Devices with NetExt disabled` as an excluded computer group.

After Jamf Pro deploys the updated profile scopes, try to reproduce the issue.

## Temporarily disable NetExt manually

Use this method only for an unmanaged test device or when your MDM solution doesn't prevent local changes:

1. On the macOS device, open **System Settings**.
2. Select **General**, select **Login Items & Extensions**, and then open **Network Extensions**. Depending on the product and macOS versions, the list can include:

    - **Microsoft Defender**
    - **Microsoft Defender Network Extension**
3. Turn off **Microsoft Defender Network Extension**.
4. Authenticate as an administrator if macOS prompts you, and then select **OK**.
5. If macOS displays the following message, select **OK**:

    ```console
    Note: Disabling the system extension will make sure that it will not be launched after reboot, but it does not guarantee that it will be terminated immediately.
    ```
6. Select **Done**, and then try to reproduce the issue.

## Restore the network extension

Restore NetExt immediately after the test, regardless of whether disabling it changes the latency:

- **Microsoft Intune**: Remove the device from `Devices with NetExt disabled`, or remove the group from the network filter profile's exclusions. Confirm that the profile is assigned to the device, and then synchronize the device.
- **Jamf Pro**: Remove the device from the temporary static group, or remove the group from the network filter profile's exclusions. Trigger a Jamf Pro check-in so that the profile is deployed again.
- **Manual configuration**: Return to **Network Extensions** in macOS **System Settings**, and turn on **Microsoft Defender Network Extension**.

Verify that the network extension is installed and enabled:

```bash
mdatp health --details system_extensions
```

If network protection is enabled, verify that its status is `started`:

```bash
mdatp health --field network_protection_status
```

If the network extension doesn't return to a healthy state, see [Troubleshoot Microsoft Defender for Endpoint system extensions on macOS](mac-support-sys-ext).

## Submit feedback

If disabling NetExt resolves or changes the latency, collect diagnostic data before you restore the extension. To submit feedback from the Defender app, open **Help**, and then select **Send feedback**.

On the Microsoft Defender portal at https://security.microsoft.com, select **Give feedback**.