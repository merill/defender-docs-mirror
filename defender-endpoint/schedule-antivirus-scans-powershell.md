---
layout: Conceptual
title: Schedule antivirus scans using PowerShell - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/schedule-antivirus-scans-powershell
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use the Set-MpPreference PowerShell cmdlet to configure scheduled Microsoft Defender Antivirus scans, including scan timing, scan type, and CPU usage settings.
ms.service: defender-endpoint
ms.localizationpriority: medium
author: chrisda
ms.author: chrisda
ms.custom: nextgen, msecd-doc-authoring-1015
ms.date: 2026-08-21T00:00:00.0000000Z
ms.reviewer: pauhijbr, ksarens
ms.subservice: ngp
ms.topic: how-to
ms.collection:
- m365-security
- tier2
- mde-ngp
ai-usage: ai-assisted
locale: en-us
document_id: 4d6393b9-e43b-9e6d-2782-65187ac34a69
document_version_independent_id: 4d6393b9-e43b-9e6d-2782-65187ac34a69
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/schedule-antivirus-scans-powershell.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: schedule-antivirus-scans-powershell
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/schedule-antivirus-scans-powershell.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: bcb7536e-34b9-8af7-5381-96c46d108a91
---

# Schedule antivirus scans using PowerShell - Microsoft Defender for Endpoint | Microsoft Learn

This article describes how to use the [Set-MpPreference](/en-us/powershell/module/defender/set-mppreference) PowerShell cmdlet to configure scheduled scans on Windows devices. Security administrators can use these parameters to control scan type, timing, frequency, CPU usage, and catch-up behavior for Microsoft Defender Antivirus. To learn more about scheduling scans and about scan types, see [About scheduled quick or full Microsoft Defender Antivirus scans](schedule-antivirus-scans).

## Prerequisites

The procedures in this article have the following requirements:

**Supported operating systems**:

- Windows
- Windows Server

## Important PowerShell parameters for scheduled scans

The following **Set-MpPreference** parameters are important for scheduled scans:

- *ScanParameters*: Specifies the scan type to use for scheduled scans. Valid values are:

    - 1 or QuickScan (default)
    - 2 or FullScan
- *ScanScheduleDay*: Specifies the day of the week to run scheduled scans. Valid values are:

    - 0 or Everyday (default)
    - 1 or Sunday
    - 2 or Monday
    - 3 or Tuesday
    - 4 or Wednesday
    - 5 or Thursday
    - 6 or Friday
    - 7 or Saturday
    - 8 or Never
- *ScanScheduleQuickScanTime*: Specifies the time on the local computer to run scheduled **quick scans**. To specify a value, enter it as a time span: `hh:mm:ss` where `hh` = hours, `mm` = minutes and `ss` = seconds. For example, `13:30:00` indicates 1:30 PM. The default value is 02:00:00 (2:00 AM).
- *ScanScheduleTime*: Specifies the time on the local computer to run scheduled **full scans**. To specify a value, enter it as a time span: `hh:mm:ss` where `hh` = hours, `mm` = minutes and `ss` = seconds. For example, `13:30:00` indicates 1:30 PM. The default value is 02:00:00 (2:00 AM).
- *ScanScheduleOffset*: Specifies the fixed number of minutes to delay scheduled scan start times on the device. The default value is 120, which means scheduled scans start 2 hours after the times specified by the *ScanScheduleTime* and *ScanScheduleQuickScanTime* parameters.
- *RandomizeScheduleTaskTimes*: Specifies whether to select a random time for the scheduled tasks (including scheduled scans). Valid values are:

    - $true: Scheduled tasks begin within 30 minutes before or after the scheduled time. This value is the default.
    - $false: Scheduled tasks begin on the scheduled time.

    Randomized start times can distribute the effects of scanning. For example, if several virtual machines share the same host, randomized start times prevent all virtual machines from starting the scheduled tasks at the same time.
- *SchedulerRandomizationTime*: Specifies the time window, in minutes, within which scheduled tasks in Microsoft Defender (including scheduled scans) can randomly start. Scheduled tasks can start within the specified number of minutes before or after the time of the scheduled task. A valid value is an integer from 0 to 4294967295.

    The randomization time window is used around specific start time values (for example, *ScanScheduleTime* and *ScanScheduleQuickScanTime* parameters) or around the number of minutes specified by the *ScanScheduleOffset* parameter.
- *ScanOnlyIfIdleEnabled*: Specifies whether to start scheduled scans only when the computer isn't in use. Valid values are:

    - $true: Windows Defender runs schedules scans when the computer is on, but not in use. This value is the default.
    - $false: Windows Defender runs schedules scans when the computer is in use.

Tip

We recommend the following settings for scheduled quick scans:

- Real-time protection enabled (`-DisableRealtimeMonitoring $false`, which is the default value).
- Cloud Protection enabled.
- Network connectivity to the Cloud Protection backend.

## Use PowerShell to schedule daily quick scans

This `Set-MpPreference` command sets the daily scheduled quick scan to ±4 minutes of 12:30 PM. The device is likely on, but activity on the device is likely minimal (lunch).

```powershell
Set-MpPreference -ScanScheduleQuickScanTime 12:30:00 -ScanScheduleOffset 0 -RandomizeScheduleTaskTimes $false -ScanOnlyIfIdleEnabled $false
```

The preceding **Set-MpPreference** command doesn't require the following parameters because their default values already match the desired behavior:

- *ScanParameters*: The default value is 0 (QuickScan).
- *ScanScheduleDay*: The default value is 0 (Everyday).

## Use PowerShell to schedule weekly full scans

This `Set-MpPreference` command schedules a weekly full scan every Wednesday at ±4 minutes of 12:30 PM.

```powershell
Set-MpPreference -ScanParameters FullScan -ScanScheduleDay Wednesday -ScanScheduleTime 12:30:00 -ScanScheduleOffset 0 -RandomizeScheduleTaskTimes $false
```

## General PowerShell parameters for scheduled scans

The following **Set-MpPreference** parameters are also available for scheduled scans:

- *CheckForSignaturesBeforeRunningScan*: Specifies whether to check for new virus and spyware definitions before Windows Defender runs **scheduled** scans. Valid values are:

    - $true: Windows Defender checks for new definitions before running a scheduled scan.
    - $false: The scheduled scan begins with the existing definitions. This value is the default.
- *ScanAvgCPULoadFactor*: Specifies the maximum percentage CPU usage for a scan. A valid value is an integer from 5 to 100. The default value is 50. The value 0 disables CPU throttling. This value isn't a hard limit, but rather guidance for the scanning engine to not exceed the specified value on average.

    The value of this parameter is ignored if both of the following conditions are true:

    - The value of the *ScanOnlyIfIdleEnabled* parameter is $true (scan only when the computer isn't in use).
    - The value of the *DisableCpuThrottleOnIdleScans* parameter is $true (disable CPU throttling on idle scans).
- *DisableCpuThrottleOnIdleScans*: Specifies whether to disable CPU throttling for scheduled scans while the device is idle (less than 90% CPU utilization). Valid values are:

    - $true: The CPU isn't throttled for scheduled scans, regardless of the value of the *ScanAvgCPULoadFactor* parameter. This value is the default.
    - $false: The CPU is throttled for scheduled scans.
- *EnableLowCpuPriority*: Specifies whether to enable using low CPU priority for scheduled scans. Valid values are:

    - $true: Windows Defender uses low CPU priority for scheduled scans. This value is the default.
    - $false: Windows Defender doesn't use low CPU priority for scheduled scans.
- *DisableCatchupFullScan*: Specifies whether to disable catch-up scans for missed scheduled full scans. Valid values are:

    - $true: Windows Defender doesn't run catch-up scans for missed scheduled full scans. This value is the default.
    - $false: After two missed scheduled full scans, Windows Defender runs a catch-up scan the next time someone signs in to the computer.
- *DisableCatchupQuickScan*: Specifies whether to disable catch-up scans for missed scheduled quick scans. Valid values are:

    - $true: Windows Defender doesn't run catch-up scans for missed scheduled quick scans. This value is the default.
    - $false: After two missed scheduled quick scans, Windows Defender runs a catch-up scan the next time the device powers on or resumes from sleep or hibernation.
- *EnableFullScanOnBatteryPower*: Specifies whether to enable full scans while on battery power. Valid values are:

    - $true: Windows Defender does full scans while on battery power.
    - $false: Windows Defender doesn't do full scans while on battery power. This value is the default

For more information, see [Use PowerShell cmdlets to configure and manage Microsoft Defender Antivirus](use-powershell-cmdlets-microsoft-defender-antivirus) and [Defender Antivirus cmdlets](/en-us/powershell/module/defender/).

## PowerShell parameters for scheduled scans to complete remediation

Scheduled full scans to complete remediation use the following parameters:

- *RemediationScheduleDay*: Specifies the day of the week to run the scan. Valid values are:

    - 0 or Everyday (default)
    - 1 or Sunday
    - 2 or Monday
    - 3 or Tuesday
    - 4 or Wednesday
    - 5 or Thursday
    - 6 or Friday
    - 7 or Saturday
    - 8 or Never
- *RemediationScheduleTime*: Specifies the time on the local computer to run the scan. To specify a value, enter it as a time span: `hh:mm:ss` where `hh` = hours, `mm` = minutes and `ss` = seconds. For example, `13:30:00` indicates 1:30 PM. The default value is 02:00:00 (2:00 AM).