---
layout: Conceptual
title: Schedule Microsoft Defender Antivirus protection updates - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/manage-protection-update-schedule-microsoft-defender-antivirus
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Schedule the day, time, and interval for when protection updates should be downloaded.
ms.service: defender-endpoint
ms.localizationpriority: medium
ms.date: 2026-08-12T00:00:00.0000000Z
ms.topic: how-to
author: chrisda
ms.author: chrisda
ms.custom: nextgen, msecd-doc-authoring-1015
ms.reviewer: pahuijbr
ms.subservice: ngp
ms.collection:
- m365-security
- tier2
ai-usage: ai-assisted
locale: en-us
document_id: f1549e2b-8fcb-5cef-677e-1dc974d3d528
document_version_independent_id: f1549e2b-8fcb-5cef-677e-1dc974d3d528
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/manage-protection-update-schedule-microsoft-defender-antivirus.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: manage-protection-update-schedule-microsoft-defender-antivirus
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/manage-protection-update-schedule-microsoft-defender-antivirus.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 1ee32ebc-6621-7f99-ff46-844c24ea8858
---

# Schedule Microsoft Defender Antivirus protection updates - Microsoft Defender for Endpoint | Microsoft Learn

Important

Customers who applied the March 2022 Microsoft Defender engine update (**1.1.19100.5**) might have encountered high resource utilization (CPU and/or memory). Microsoft has released an update (**1.1.19200.5**) that resolves the bugs introduced in the earlier version. Customers are recommended to update to Microsoft Defender Antivirus Engine build **1.1.19200.5**. To ensure any performance issues are fully fixed, it's recommended to reboot machines after applying Microsoft Defender Antivirus Engine update 1.1.19200.5. For more information, see [Monthly platform and engine versions](microsoft-defender-endpoint-releases#microsoft-defender-antivirus-releases).

This article explains how to configure scheduled protection updates for Microsoft Defender Antivirus using Configuration Manager, Group Policy, PowerShell, or WMI. Microsoft Defender Antivirus lets you determine when it should look for and download updates.

You can schedule updates for your endpoints by:

- Specifying the day of the week to check for protection updates
- Specifying the interval to check for protection updates
- Specifying the time to check for protection updates

You can also randomize the times when each endpoint checks and downloads protection updates. For more information, see [About schedule scans](schedule-antivirus-scans).

## Prerequisites

Before you configure scheduled protection updates, make sure the following requirements are met.

### Supported operating systems

The following operating systems are supported:

- Windows

## Use Configuration Manager to schedule protection updates

To schedule protection updates by using Configuration Manager, perform the following steps:

1. On your Microsoft Configuration Manager console, open the antimalware policy you want to change (select **Assets and Compliance** in the navigation pane on the left, then expand the tree to **Overview** &gt; **Endpoint Protection** &gt; **Antimalware Policies**)
2. Go to the **Security intelligence updates** section.
3. To check and download updates at a certain time:

    - Set **Check for Endpoint Protection security intelligence updates at a specific interval...** to **0**.
    - Set **Check for Endpoint Protection security intelligence updates daily at...** to the time when updates should be checked.
4. To check and download updates on a continual interval, Set **Check for Endpoint Protection security intelligence updates at a specific interval...** to the number of hours that should occur between updates.
5. [Deploy the updated policy as usual](/en-us/sccm/protect/deploy-use/endpoint-antimalware-policies#deploy-an-antimalware-policy-to-client-computers).

## Use Group Policy to schedule protection updates

Important

By default, the update schedule day (`SignatureScheduleDay`) is set to "8" (no day specified) and the update check interval (`SignatureUpdateInterval`) is set to "0" (disabled), so Microsoft Defender Antivirus doesn't schedule protection updates automatically. Enabling `SignatureScheduleDay` or `SignatureUpdateInterval` overrides that default.

To schedule protection updates by using Group Policy, perform the following steps:

1. In Centralized Group Policy, open the [Group Policy Management Console (GPMC)](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-management-console) on your Group Policy management computer.
2. In the GPMC console tree, expand Group Policy Objects in the forest and domain containing the GPO you want to edit.
3. Right-click the GPO, and then select **Edit**.
4. In the **Group Policy Management Editor**, go to **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Security Intelligence Updates**.

    Note

    Group Policy paths before Windows 10, version 2004 (May 2020) might use *Windows* Defender Antivirus instead of *Microsoft* Defender Antivirus. Group Policy paths before Windows 10, version 1909 (November 2019) might use *Signature Updates* instead of *Security Intelligence Updates*. The older and newer names refer to the same policy locations.
5. In the details pane of **Security Intelligence Updates**, the available settings are:

    - Specify the day of the week to check for security intelligence updates
    - Specify the interval to check for security intelligence updates
    - Specify the time to check for security intelligence updates

    To open and configure a security intelligence update schedule setting, use any of the following methods:

    - Double-click the setting.
    - Right-click the setting, and then select **Edit**.
    - Select the setting, and then select **Action** &gt; **Edit**.

Tip

You can also configure Group Policy locally on individual devices by using the Local Group Policy Editor (`gpedit.msc`). Navigate to the same path: **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Security Intelligence Updates**.

### Enable and configure the security intelligence update day

1. In the details pane of **Security Intelligence Updates**, open the **Specify the day of the week to check for security intelligence updates** setting.
2. In the setting window that opens, configure the following options:

    1. Select **Enabled**.
    2. **Specify the day of the week to check for security intelligence updates** in the **Options** section: Select the day of the week to check for updates.

    When you're finished, select **OK**.

### Enable and configure the security intelligence update interval

1. In the details pane of **Security Intelligence Updates**, open the **Specify the interval to check for security intelligence updates** setting.
2. In the setting window that opens, configure the following options:

    1. Select **Enabled**.
    2. **Specify the interval to check for security intelligence updates** in the **Options** section: Enter a value from `1` to `24` for the number of hours between updates.

    When you're finished, select **OK**.

### Enable and configure the security intelligence update time

1. In the details pane of **Security Intelligence Updates**, open the **Specify the time to check for security intelligence updates** setting.
2. In the setting window that opens, configure the following options:

    1. Select **Enabled**.
    2. **Specify the time to check for security intelligence updates** in the **Options** section: Enter the number of minutes after midnight when updates should be checked. For example, enter `120` for 2:00 AM. The schedule is based on the local time of the endpoint.

    When you're finished, select **OK**.

## Use PowerShell cmdlets to schedule protection updates

Use the following cmdlets to set the day, time, and interval for protection update checks:

```PowerShell
Set-MpPreference -SignatureScheduleDay
Set-MpPreference -SignatureScheduleTime
Set-MpPreference -SignatureUpdateInterval
```

See [Use PowerShell cmdlets to configure and run Microsoft Defender Antivirus](use-powershell-cmdlets-microsoft-defender-antivirus) and [Defender Antivirus cmdlets](/en-us/powershell/module/defender/) for more information on how to use PowerShell with Microsoft Defender Antivirus.

## Use Windows Management Instrumentation (WMI) to schedule protection updates

Use the [**Set** method of the **MSFT\_MpPreference**](/en-us/previous-versions/windows/desktop/legacy/dn455323%28v=vs.85%29) class for the following properties to configure the signature update schedule day, time, and interval:

```WMI
SignatureScheduleDay
SignatureScheduleTime
SignatureUpdateInterval
```

See the following for more information and allowed parameters:

- [Windows Defender WMIv2 APIs](/en-us/previous-versions/windows/desktop/defender/windows-defender-wmiv2-apis-portal)

Tip

If you're looking for Antivirus related information for other platforms, see:

- [Set preferences for Microsoft Defender for Endpoint on macOS](mac-preferences)
- [Microsoft Defender for Endpoint on Mac](microsoft-defender-endpoint-mac)
- [macOS Antivirus policy settings for Microsoft Defender Antivirus for Intune](/en-us/intune/intune-service/protect/antivirus-microsoft-defender-settings-macos)
- [Configure Microsoft Defender for Endpoint on iOS features](ios-configure-features)
- [Configure Defender for Endpoint on Android features](android-configure)
- [Set preferences for Microsoft Defender for Endpoint on Linux](linux-preferences)
- [Microsoft Defender for Endpoint on Linux](microsoft-defender-endpoint-linux)