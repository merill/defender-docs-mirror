---
layout: Conceptual
title: Define how mobile devices are updated by Microsoft Defender Antivirus - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/manage-updates-mobile-devices-vms-microsoft-defender-antivirus
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Configure Microsoft Defender Antivirus protection update behavior for mobile devices and VMs, including Microsoft Update fallback and battery-power settings.
ms.service: defender-endpoint
ms.localizationpriority: medium
ms.topic: how-to
author: chrisda
ms.author: chrisda
ms.custom: nextgen, msecd-doc-authoring-1015
ms.reviewer: yongrhee
ms.subservice: ngp
ms.collection:
- m365-security
- tier2
ms.date: 2026-08-12T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: e8abf703-2db5-178d-5504-8da4e2ece8ad
document_version_independent_id: e8abf703-2db5-178d-5504-8da4e2ece8ad
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/manage-updates-mobile-devices-vms-microsoft-defender-antivirus.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: manage-updates-mobile-devices-vms-microsoft-defender-antivirus
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/manage-updates-mobile-devices-vms-microsoft-defender-antivirus.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 35bdc124-0af8-b03d-9fcc-3b4c2b1013cc
---

# Define how mobile devices are updated by Microsoft Defender Antivirus - Microsoft Defender for Endpoint | Microsoft Learn

This article explains how to configure Microsoft Defender Antivirus update settings for mobile devices and virtual machines (VMs) to reduce performance impact during updates. Mobile devices and VMs may require more configuration to ensure performance is not impacted by updates.

For Microsoft Defender Antivirus, two update-related settings are especially useful for mobile devices and VMs:

- Opt in to Microsoft Update on mobile computers without a WSUS connection
- Prevent Security intelligence updates when running on battery power

The following articles may also be useful in these situations:

- [About scheduled scans](schedule-antivirus-scans)
- [Manage updates for endpoints that are out of date](manage-outdated-endpoints-microsoft-defender-antivirus)
- [Deployment guide for Microsoft Defender Antivirus in a virtual desktop infrastructure (VDI) environment](deployment-vdi-microsoft-defender-antivirus)

## Prerequisites

Before you configure the update settings described in this article, make sure your environment meets the following requirements.

### Supported operating systems

The following operating systems are supported:

- Windows

## Opt in to Microsoft Update on mobile computers without a WSUS connection

You can use Microsoft Update to keep Security intelligence on mobile devices running Microsoft Defender Antivirus up to date when they are not connected to the corporate network or don't otherwise have a WSUS connection.

Opting in to Microsoft Update means that protection updates can be delivered to devices (via Microsoft Update) even if you have set WSUS to override Microsoft Update.

You can opt in to Microsoft Update on the mobile device in one of the following ways:

- Change the setting with Group Policy.
- Use a VBScript to create a script, then run it on each computer in your network.
- Manually opt in every computer on your network through the **Settings** menu.

### Use Group Policy to opt in to Microsoft Update

Perform the following steps to enable Microsoft Update by using Group Policy:

1. In Centralized Group Policy, open the [Group Policy Management Console (GPMC)](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-management-console) on your Group Policy management computer.
2. In the GPMC console tree, expand Group Policy Objects in the forest and domain containing the GPO you want to edit.
3. Right-click the GPO, and then select **Edit**.
4. In the **Group Policy Management Editor**, go to **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Security Intelligence Updates**.

    Note

    Group Policy paths before Windows 10, version 2004 (May 2020) might use *Windows* Defender Antivirus instead of *Microsoft* Defender Antivirus. Group Policy paths before Windows 10, version 1909 (November 2019) might use *Signature Updates* instead of *Security Intelligence Updates*. The older and newer names refer to the same policy locations.
5. In the details pane of **Security Intelligence Updates**, open the **Allow security intelligence updates from Microsoft Update** setting. To open the setting, use any of the following methods:

    - Double-click the setting.
    - Right-click the setting, and then select **Edit**.
    - Select the setting, and then select **Action** &gt; **Edit**.
6. In the setting window that opens, select **Enabled**, and then select **OK**.

Tip

You can also configure Group Policy locally on individual devices by using the Local Group Policy Editor (`gpedit.msc`). Navigate to the same path: **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Security Intelligence Updates**.

### Use a VBScript to opt in to Microsoft Update

Use the following process to create and run a VBScript that opts devices in to Microsoft Update:

1. Use the instructions in the MSDN article [Opt-In to Microsoft Update](/en-us/windows/win32/wua_sdk/opt-in-to-microsoft-update) to create the VBScript.
2. Run the VBScript you created on each computer in your network.

### Manually opt in to Microsoft Update

To manually opt a device in to Microsoft Update, complete the following steps:

1. Open **Windows Update** in **Update & security** settings on the computer you want to opt in.
2. Select **Advanced** options.
3. Select the checkbox for **Give me updates for other Microsoft products when I update Windows**.

## Prevent Security intelligence updates when running on battery power

You can configure Microsoft Defender Antivirus to only download protection updates when the PC is connected to a wired power source.

### Use Group Policy to prevent security intelligence updates on battery power

Perform the following steps to prevent security intelligence updates when devices are running on battery power:

1. In Centralized Group Policy, open the [Group Policy Management Console (GPMC)](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-management-console) on your Group Policy management computer.
2. In the GPMC console tree, expand Group Policy Objects in the forest and domain containing the GPO you want to edit.
3. Right-click the GPO, and then select **Edit**.
4. In the **Group Policy Management Editor**, go to **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Security Intelligence Updates**.

    Note

    Group Policy paths before Windows 10, version 2004 (May 2020) might use *Windows* Defender Antivirus instead of *Microsoft* Defender Antivirus. Group Policy paths before Windows 10, version 1909 (November 2019) might use *Signature Updates* instead of *Security Intelligence Updates*. The older and newer names refer to the same policy locations.
5. In the details pane of **Security Intelligence Updates**, open the **Allow security intelligence updates when running on battery power** setting. To open the setting, use any of the following methods:

    - Double-click the setting.
    - Right-click the setting, and then select **Edit**.
    - Select the setting, and then select **Action** &gt; **Edit**.

Tip

You can also configure Group Policy locally on individual devices by using the Local Group Policy Editor (`gpedit.msc`). Navigate to the same path: **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Security Intelligence Updates**.

1. In the setting window that opens, select **Disabled**, and then select **OK**.

Disabling **Allow security intelligence updates when running on battery power** prevents protection updates from downloading when the PC is on battery power.

Tip

If you're looking for Antivirus related information for other platforms, see:

- [Set preferences for Microsoft Defender for Endpoint on macOS](mac-preferences)
- [Microsoft Defender for Endpoint on Mac](microsoft-defender-endpoint-mac)
- [macOS Antivirus policy settings for Microsoft Defender Antivirus for Intune](/en-us/intune/intune-service/protect/antivirus-microsoft-defender-settings-macos)
- [Set preferences for Microsoft Defender for Endpoint on Linux](linux-preferences)
- [Microsoft Defender for Endpoint on Linux](microsoft-defender-endpoint-linux)
- [Configure Defender for Endpoint on Android features](android-configure)
- [Configure Microsoft Defender for Endpoint on iOS features](ios-configure-features)