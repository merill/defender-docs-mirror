---
layout: Conceptual
title: Apply Microsoft Defender Antivirus protection updates to out of date endpoints - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/manage-outdated-endpoints-microsoft-defender-antivirus
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Define when and how updates should be applied for out of date endpoints in Microsoft Defender Antivirus.
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
- tier3
ms.date: 2026-08-21T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: cd49e2f4-537a-f7fb-54b3-a0312618881d
document_version_independent_id: cd49e2f4-537a-f7fb-54b3-a0312618881d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/manage-outdated-endpoints-microsoft-defender-antivirus.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: manage-outdated-endpoints-microsoft-defender-antivirus
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/manage-outdated-endpoints-microsoft-defender-antivirus.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: c6ce276b-4cd1-9fea-2bb0-e3ba27407e30
---

# Apply Microsoft Defender Antivirus protection updates to out of date endpoints - Microsoft Defender for Endpoint | Microsoft Learn

With Microsoft Defender Antivirus, your security team can define how long an endpoint can avoid an update or how many scans it can miss before it's required to receive the update and run a scan. This article shows how to configure catch-up protection updates, set the out-of-date reporting threshold, and enable catch-up scans for endpoints that have missed scheduled updates or scans. This capability is especially useful in environments where devices aren't often connected to a corporate or external network, or for devices that aren't used on a daily basis.

For example, an employee who uses a particular computer takes three days off of work, and doesn't sign on their computer during that time. When the employee returns to work and signs into their computer, Microsoft Defender Antivirus will immediately check and download the latest protection updates, and then run a scan.

## Prerequisites

### Supported operating systems

The following operating systems support catch-up protection updates and catch-up scans:

- Windows

## Set up catch-up protection updates for endpoints that haven't updated for a while

If Microsoft Defender Antivirus didn't download protection updates for a specified period, you can set it up to automatically check and download the latest update the next time someone signs in on an endpoint. Configuring catch-up protection updates to check for updates at sign-in is useful if you have [globally disabled automatic update downloads on startup](manage-event-based-updates-microsoft-defender-antivirus).

You can use one of several methods to set up catch-up protection updates:

- Use Configuration Manager to configure catch-up protection updates
- Use Group Policy to enable and configure the catch-up update feature
- Use PowerShell cmdlets to configure catch-up protection updates
- Use Windows Management Instrumentation (WMI) to configure catch-up protection updates

### Use Configuration Manager to configure catch-up protection updates

To configure catch-up protection updates in Configuration Manager, use the following steps:

1. On your Microsoft Configuration Manager console, open the anti-malware policy you want to change (select **Assets and Compliance** in the navigation pane on the left, then expand the tree to **Overview** &gt; **Endpoint Protection** &gt; **Antimalware Policies**)
2. Go to the **Security intelligence updates** section and configure the following settings:

    - Set **Force a security intelligence update if the client computer is offline for more than two consecutive scheduled updates** to **Yes**.
    - For the **If Configuration Manager is used as a source for security intelligence updates...**, specify the hours before which the security intelligence updates delivered by Configuration Manager should be considered out of date. When the updates are considered out of date, the **If Configuration Manager is used as a source for security intelligence updates...** setting causes the endpoint to download updates from the next source in the configured [fallback source order](manage-protection-updates-microsoft-defender-antivirus#fallback-order).
3. Select **OK**.
4. [Deploy the antimalware policy to client computers](/en-us/sccm/protect/deploy-use/endpoint-antimalware-policies#deploy-an-antimalware-policy-to-client-computers).

### Use Group Policy to enable and configure the catch-up update feature

To enable and configure the catch-up update feature in Group Policy, use the following steps:

1. In Centralized Group Policy, open the [Group Policy Management Console (GPMC)](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-management-console) on your Group Policy management computer.
2. In the GPMC console tree, expand Group Policy Objects in the forest and domain containing the GPO you want to edit.
3. Right-click the GPO, and then select **Edit**.
4. In the **Group Policy Management Editor**, go to **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Security Intelligence Updates**.

    Note

    Group Policy paths before Windows 10, version 2004 (May 2020) might use *Windows* Defender Antivirus instead of *Microsoft* Defender Antivirus. Group Policy paths before Windows 10, version 1909 (November 2019) might use *Signature Updates* instead of *Security Intelligence Updates*. The older and newer names refer to the same policy locations.
5. In the details pane of **Security Intelligence Updates**, open the **Define the number of days after which a catch-up security intelligence update is required** setting. To open the setting, use any of the following methods:

    - Double-click the setting.
    - Right-click the setting, and then select **Edit**.
    - Select the setting, and then select **Action** &gt; **Edit**.
6. In the setting window that opens, configure the following options:

    1. Select **Enabled**.
    2. Enter the number of days after which you want Microsoft Defender Antivirus to check for and download the latest protection update.

    When you're finished, select **OK**.

Tip

You can also configure Group Policy locally on individual devices by using the Local Group Policy Editor (`gpedit.msc`). Navigate to the same path: **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Security Intelligence Updates**.

### Use PowerShell cmdlets to configure catch-up protection updates

Use the following cmdlet to set the number of days after which a catch-up security intelligence update is required:

```PowerShell
Set-MpPreference -SignatureUpdateCatchupInterval
```

For more information about using PowerShell with Microsoft Defender Antivirus, see the following articles:

- [Use PowerShell cmdlets to configure and run Microsoft Defender Antivirus](use-powershell-cmdlets-microsoft-defender-antivirus)
- [Defender Antivirus cmdlets](/en-us/powershell/module/defender/)

### Use Windows Management Instrumentation (WMI) to configure catch-up protection updates

Use the [**Set** method of the **MSFT\_MpPreference**](/en-us/previous-versions/windows/desktop/legacy/dn455323%28v=vs.85%29) class with the following property to configure the number of days after which a catch-up security intelligence update is required:

```WMI
SignatureUpdateCatchupInterval
```

For more information and allowed parameters, see [Windows Defender WMIv2 APIs](/en-us/previous-versions/windows/desktop/defender/windows-defender-wmiv2-apis-portal).

## Set the number of days before protection is reported as out of date

You can also specify the number of days after which Microsoft Defender Antivirus protection is considered old or out of date. After the specified number of days, the client will report itself as "out of date" and will show an error to the endpoint user. When an endpoint is considered out of date, Microsoft Defender Antivirus might attempt to download an update from other sources (based on the defined [fallback source order](manage-protection-updates-microsoft-defender-antivirus#fallback-order)).

You can use Group Policy to specify the number of days after which endpoint protection is considered to be out of date.

### Use Group Policy to specify the number of days before protection is considered out of date

To specify when protection is considered out of date by using Group Policy, use the following steps:

1. In Centralized Group Policy, open the [Group Policy Management Console (GPMC)](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-management-console) on your Group Policy management computer.
2. In the GPMC console tree, expand Group Policy Objects in the forest and domain containing the GPO you want to edit.
3. Right-click the GPO, and then select **Edit**.
4. In the **Group Policy Management Editor**, go to **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Security Intelligence Updates**.

    Note

    Group Policy paths before Windows 10, version 2004 (May 2020) might use *Windows* Defender Antivirus instead of *Microsoft* Defender Antivirus. Group Policy paths before Windows 10, version 1909 (November 2019) might use *Signature Updates* instead of *Security Intelligence Updates*. The older and newer names refer to the same policy locations.
5. In the details pane of **Security Intelligence Updates**, the available settings are:

    - Define the number of days before spyware security intelligence is considered out of date
    - Define the number of days before virus security intelligence is considered out of date

    To open and configure a security intelligence age setting, use any of the following methods:

    - Double-click the setting.
    - Right-click the setting, and then select **Edit**.
    - Select the setting, and then select **Action** &gt; **Edit**.

Tip

You can also configure Group Policy locally on individual devices by using the Local Group Policy Editor (`gpedit.msc`). Navigate to the same path: **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Security Intelligence Updates**.

#### Enable and configure the spyware security intelligence age setting

1. In the details pane of **Security Intelligence Updates**, open the **Define the number of days before spyware security intelligence is considered out of date** setting.
2. In the setting window that opens, configure the following options:

    1. Select **Enabled**.
    2. **Define the number of days before spyware security intelligence is considered out of date** in the **Options** section: Enter the number of days after which you want Microsoft Defender Antivirus to consider spyware security intelligence to be out of date.

    When you're finished, select **OK**.

#### Enable and configure the virus security intelligence age setting

1. In the details pane of **Security Intelligence Updates**, open the **Define the number of days before virus security intelligence is considered out of date** setting.
2. In the setting window that opens, configure the following options:

    1. Select **Enabled**.
    2. **Define the number of days before virus security intelligence is considered out of date** in the **Options** section: Enter the number of days after which you want Microsoft Defender Antivirus to consider virus security intelligence to be out of date.

    When you're finished, select **OK**.

## Set up catch-up scans for endpoints that haven't been scanned for a while

You can set the number of consecutive scheduled scans that can be missed before Microsoft Defender Antivirus forces a scan.

The process for enabling catch-up scans is:

1. Set up at least one scheduled scan.
2. Enable the catch-up scan feature.
3. Define the number of scans that can be skipped before a catch-up scan occurs.

Catch-up scans can be enabled for both full and quick scans.

Important

Before you configure catch-up scans, set up at least one scheduled scan. Catch-up scans depend on an existing scheduled scan configuration.

Tip

We recommend using quick scans for most situations. To learn more, see [About scheduled scans](schedule-antivirus-scans#comparing-the-quick-scan-full-scan-and-custom-scan).

You can use one of several methods to set up catch-up scans:

- Use Group Policy to enable and configure the catch-up scan feature
- Use PowerShell cmdlets to configure catch-up scans
- Use Windows Management Instrumentation (WMI) to configure catch-up scans
- Use Configuration Manager to configure catch-up scans

### Use Group Policy to enable and configure the catch-up scan feature

To enable and configure the catch-up scan feature in Group Policy, use the following steps:

1. Ensure you set up at least one scheduled scan.
2. In Centralized Group Policy, open the [Group Policy Management Console (GPMC)](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-management-console) on your Group Policy management computer.
3. In the GPMC console tree, expand Group Policy Objects in the forest and domain containing the GPO you want to edit.
4. Right-click the GPO, and then select **Edit**.
5. In the **Group Policy Management Editor**, go to **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Scan**.

    Note

    Group Policy paths before Windows 10, version 2004 (May 2020) might use *Windows* Defender Antivirus instead of *Microsoft* Defender Antivirus. Both names refer to the same policy location.
6. In the details pane of **Scan**, the available settings are:

    - Turn on catch-up quick scan
    - Turn on catch-up full scan
    - Define the number of days after which a catch-up scan is forced

    To open and configure a catch-up scan setting, use any of the following methods:

    - Double-click the setting.
    - Right-click the setting, and then select **Edit**.
    - Select the setting, and then select **Action** &gt; **Edit**.

Tip

You can also configure Group Policy locally on individual devices by using the Local Group Policy Editor (`gpedit.msc`). Navigate to the same path: **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Scan**.

#### Enable and configure catch-up quick scans

1. In the details pane of **Scan**, open the **Turn on catch-up quick scan** setting.
2. In the setting window that opens, select **Enabled**, and then select **OK**.

#### Enable and configure catch-up full scans

1. In the details pane of **Scan**, open the **Turn on catch-up full scan** setting.
2. In the setting window that opens, select **Enabled**, and then select **OK**.

#### Enable and configure forced catch-up scans

1. In the details pane of **Scan**, open the **Define the number of days after which a catch-up scan is forced** setting.
2. In the setting window that opens, configure the following options:

    1. Select **Enabled**.
    2. Enter the number of scans that can be missed before a scan automatically runs when the user next signs in on the endpoint.

    The type of scan that runs is determined by the **Specify the scan type to use for a scheduled scan** setting. For more information, see [About scheduled scans](schedule-antivirus-scans).

    When you're finished, select **OK**.

Note

The Group Policy setting title refers to the number of days. The setting, however, is applied to the number of scans (not days) before the catch-up scan will be run.

### Use PowerShell cmdlets to configure catch-up scans

Use the following cmdlets to enable or disable catch-up scans for full and quick scheduled scans. By default, catch-up full and quick scans are disabled. Set the corresponding value to `$false` to enable catch-up behavior and force a scan after missed scheduled scans:

```PowerShell
Set-MpPreference -DisableCatchupFullScan
Set-MpPreference -DisableCatchupQuickScan

```

For more information about using PowerShell with Microsoft Defender Antivirus, see the following articles:

- [Use PowerShell cmdlets to manage Microsoft Defender Antivirus](use-powershell-cmdlets-microsoft-defender-antivirus)
- [Defender Antivirus cmdlets](/en-us/powershell/module/defender/)

### Use Windows Management Instrumentation (WMI) to configure catch-up scans

Use the [**Set** method of the **MSFT\_MpPreference**](/en-us/previous-versions/windows/desktop/legacy/dn455323%28v=vs.85%29) class with the following properties to enable or disable catch-up behavior for full and quick scheduled scans:

```WMI
DisableCatchupFullScan
DisableCatchupQuickScan
```

For more information and allowed parameters, see [Windows Defender WMIv2 APIs](/en-us/previous-versions/windows/desktop/defender/windows-defender-wmiv2-apis-portal).

### Use Configuration Manager to configure catch-up scans

To configure catch-up scans in Configuration Manager, use the following steps:

1. On your Microsoft Configuration Manager console, open the anti-malware policy you want to change (select **Assets and Compliance** in the navigation pane on the left, then expand the tree to **Overview** &gt; **Endpoint Protection** &gt; **Antimalware Policies**)
2. Go to the **Scheduled scans** section and **Force a scan of the selected scan type if client computer is offline...** to **Yes**.
3. Select **OK**.
4. [Deploy the antimalware policy to client computers](/en-us/sccm/protect/deploy-use/endpoint-antimalware-policies#deploy-an-antimalware-policy-to-client-computers).

### Use Group Policy to configure security intelligence updates over a metered connection

To configure security intelligence updates over a metered connection by using Group Policy, use the following steps:

1. In Centralized Group Policy, open the [Group Policy Management Console (GPMC)](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-management-console) on your Group Policy management computer.
2. In the GPMC console tree, expand Group Policy Objects in the forest and domain containing the GPO you want to edit.
3. Right-click the GPO, and then select **Edit**.
4. In the **Group Policy Management Editor**, go to **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Security Intelligence Updates**.
5. In the details pane of **Security Intelligence Updates**, open the **Allows Microsoft Defender Antivirus to update and communicate over a metered connection.** setting. To open the setting, use any of the following methods:

    - Double-click the setting.
    - Right-click the setting, and then select **Edit**.
    - Select the setting, and then select **Action** &gt; **Edit**.

Tip

You can also configure Group Policy locally on individual devices by using the Local Group Policy Editor (`gpedit.msc`). Navigate to the same path: **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus** &gt; **Security Intelligence Updates**.

1. In the setting window that opens, select **Enabled**, and then select **OK**.

| Settings | Description | Default |
| --- | --- | --- |
| Allows Microsoft Defender Antivirus to update and communicate over a metered connection. | Enabling this policy automatically downloads updates, even over metered data connections (charges might apply). | Disabled |

Tip

If you're looking for Antivirus related information for other platforms, see:

- [Set preferences for Microsoft Defender for Endpoint on macOS](mac-preferences)
- [Microsoft Defender for Endpoint on Mac](microsoft-defender-endpoint-mac)
- [macOS Antivirus policy settings for Microsoft Defender Antivirus for Intune](/en-us/intune/intune-service/protect/antivirus-microsoft-defender-settings-macos)
- [Set preferences for Microsoft Defender for Endpoint on Linux](linux-preferences)
- [Microsoft Defender for Endpoint on Linux](microsoft-defender-endpoint-linux)
- [Configure Defender for Endpoint on Android features](android-configure)
- [Configure Microsoft Defender for Endpoint on iOS features](ios-configure-features)