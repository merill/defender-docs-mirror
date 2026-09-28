---
layout: Conceptual
title: Schedule antivirus scans using Windows Management Instrumentation - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/schedule-antivirus-scans-wmi
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use Windows Management Instrumentation (WMI) to configure scheduled Microsoft Defender Antivirus scans, including scan timing, idle-only scans, remediation scheduling, and daily quick scan settings.
ms.service: defender-endpoint
ms.localizationpriority: medium
author: chrisda
ms.author: chrisda
ms.custom: nextgen, msecd-doc-authoring-1016
ms.date: 2026-07-02T00:00:00.0000000Z
ms.reviewer: pauhijbr, ksarens, yongrhee
ms.subservice: ngp
ms.topic: how-to
ms.collection:
- m365-security
- tier3
- mde-ngp
ai-usage: ai-assisted
locale: en-us
document_id: b348cfeb-d6a7-965f-dde6-7bebfd136a85
document_version_independent_id: b348cfeb-d6a7-965f-dde6-7bebfd136a85
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/schedule-antivirus-scans-wmi.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: schedule-antivirus-scans-wmi
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/schedule-antivirus-scans-wmi.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: b143236a-2d56-6f1e-395b-7193493718af
---

# Schedule antivirus scans using Windows Management Instrumentation - Microsoft Defender for Endpoint | Microsoft Learn

This article describes how to configure scheduled Microsoft Defender Antivirus scans using Windows Management Instrumentation (WMI). WMI is useful for administrators who manage scan schedules programmatically or in environments where Group Policy isn't available. You'll learn how to set scan timing, configure idle-only scans, schedule remediation, and define daily quick scan times. To learn more about scheduling scans and about scan types, see [Configure scheduled quick or full Microsoft Defender Antivirus scans](schedule-antivirus-scans).

## Prerequisites

### Supported operating systems

WMI-based scan scheduling is supported on the following operating systems:

- Windows
- Windows Server

## Use Windows Management Instrumentation (WMI) to schedule scans

**MSFT\_MpPreference** is the WMI class used to configure Microsoft Defender Antivirus preferences. Use the [**Set** method of the **MSFT\_MpPreference**](/en-us/previous-versions/windows/desktop/legacy/dn455323%28v=vs.85%29) class for the following properties:

The following WMI properties control scan scheduling and behavior in the Defender configuration class:

```WMI
ScanParameters
ScanScheduleDay
ScanScheduleTime
RandomizeScheduleTaskTimes
```

For more information and allowed parameters, see [Windows Defender WMIv2 APIs](/en-us/previous-versions/windows/desktop/defender/windows-defender-wmiv2-apis-portal)

## WMI for scheduling scans when an endpoint isn't in use

Caution

When you schedule scans for times when endpoints aren't in use, scans don't honor the CPU throttling configuration and will take full advantage of the resources available to complete the scan as fast as possible.

Use the [Set method of the MSFT_MpPreference class](/en-us/previous-versions/windows/desktop/legacy/dn455323%28v=vs.85%29) for the following properties:

The following WMI property controls whether scans run only when the device is idle:

```WMI
ScanOnlyIfIdleEnabled
```

For more information about APIs and allowed parameters, see [Windows Defender WMIv2 APIs](/en-us/previous-versions/windows/desktop/defender/windows-defender-wmiv2-apis-portal).

## WMI for scheduling scans to complete remediation

Remediation is the follow-up action that Microsoft Defender Antivirus takes to address detected threats after a scan, such as quarantining or removing malicious files. You can schedule when remediation occurs by using the [**Set** method of the **MSFT\_MpPreference**](/en-us/previous-versions/windows/desktop/legacy/dn455323%28v=vs.85%29) class for the following properties:

The following WMI properties define the remediation schedule day and time:

```WMI
RemediationScheduleDay
RemediationScheduleTime
```

For more information and allowed parameters, see [Windows Defender WMIv2 APIs](/en-us/previous-versions/windows/desktop/defender/windows-defender-wmiv2-apis-portal).

## WMI for scheduling daily scans

Use the [**Set** method of the **MSFT\_MpPreference**](/en-us/previous-versions/windows/desktop/legacy/dn455323%28v=vs.85%29) class for the following properties:

Use this WMI property to specify the scheduled daily quick scan time:

```WMI
ScanScheduleQuickScanTime
```

For more information and allowed parameters, see [Windows Defender WMIv2 APIs](/en-us/previous-versions/windows/desktop/defender/windows-defender-wmiv2-apis-portal).

Tip

If you're looking for Antivirus related information for other platforms, see:

- [Set preferences for Microsoft Defender for Endpoint on macOS](mac-preferences)
- [Microsoft Defender for Endpoint on Mac](microsoft-defender-endpoint-mac)
- [macOS Antivirus policy settings for Microsoft Defender Antivirus for Intune](/en-us/intune/intune-service/protect/antivirus-microsoft-defender-settings-macos)
- [Set preferences for Microsoft Defender for Endpoint on Linux](linux-preferences)
- [Microsoft Defender for Endpoint on Linux](microsoft-defender-endpoint-linux)
- [Configure Defender for Endpoint on Android features](android-configure)
- [Configure Microsoft Defender for Endpoint on iOS features](ios-configure-features)