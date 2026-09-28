---
layout: Conceptual
title: About regular quick and full scans with Microsoft Defender Antivirus - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/schedule-antivirus-scans
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn about recurring (scheduled) scans, including when they should run and whether they run as full or quick scans
ms.service: defender-endpoint
ms.localizationpriority: medium
author: chrisda
ms.author: chrisda
ms.custom: nextgen, msecd-doc-authoring-1016
ms.date: 2026-07-02T00:00:00.0000000Z
ms.reviewer: pauhijbr, ksarens, yongrhee, bsabetghadam
ms.subservice: ngp
ms.topic: how-to
ms.collection:
- m365-security
- tier3
- mde-ngp
ai-usage: ai-assisted
locale: en-us
document_id: 777b0ec3-4daf-4989-13c2-8f23c107c09c
document_version_independent_id: 777b0ec3-4daf-4989-13c2-8f23c107c09c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/schedule-antivirus-scans.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: schedule-antivirus-scans
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/schedule-antivirus-scans.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 3712fb18-f41f-5c4e-ffc6-4d499887f4d2
---

# About regular quick and full scans with Microsoft Defender Antivirus - Microsoft Defender for Endpoint | Microsoft Learn

You can set up regular, scheduled antivirus scans on devices. These scheduled scans are in addition to always-on, real-time protection and [on-demand antivirus](run-scan-microsoft-defender-antivirus) scans. When you schedule a scan, you can specify the type of scan, when the scan should occur, and if the scan should occur after a [Microsoft Defender Antivirus protection update](manage-protection-updates-microsoft-defender-antivirus) or when a device isn't being used. You can also set up special scans to complete remediation actions if needed.

For scheduled scan instructions, see the following articles:

- [Schedule antivirus scans using PowerShell](schedule-antivirus-scans-powershell)
- [Schedule antivirus scans using Windows Management Instrumentation (WMI)](schedule-antivirus-scans-wmi)
- [Schedule antivirus scans using Windows Task Scheduler](https://support.microsoft.com/windows/schedule-a-scan-in-microsoft-defender-antivirus-54b64e9c-880a-c6b6-2416-0eb330ed5d2d)
- [Schedule antivirus scans using Group Policy](schedule-antivirus-scans-group-policy)
- [Schedule antivirus scans using Microsoft Intune](schedule-antivirus-scans-intune)

## Prerequisites

Before you configure scheduled scans, make sure your device meets the following requirements.

### Supported operating systems

Scheduled antivirus scans are supported on the following operating systems:

- Windows

## Comparing the quick scan, full scan, and custom scan

The following table describes the different types of scans you can configure. For more information, see [Microsoft Defender Antivirus scan considerations and best practices](mdav-scan-best-practices).

| Scan type | Description |
| --- | --- |
| Quick scan (*recommended*) | A quick scan looks at all the locations where there could be malware registered to start with the system, such as registry keys and known Windows startup folders. Quick scans also run on mounted removable devices, such as USB drives. A quick scan helps provide strong protection against malware that starts with the system and kernel-level malware, together with [always-on real-time protection](configure-real-time-protection-microsoft-defender-antivirus), which reviews files when they're opened and closed, and whenever a user navigates to a folder.Preview: In most cases, a quick scan is sufficient and is the recommended option for scheduled scans. Starting with the December 2023 (4.18.2311.x.x) release of [Microsoft Defender Antivirus platform updates](microsoft-defender-antivirus-updates), you have the option named "Quick scan include exclusions" to scan all files and directories that are excluded from real-time protection that is using contextual exclusions. By enabling this policy, the excluded files and folders are scanned during a quick scan. Note: While in preview, management is available in Intune - Settings Catalog. |
| Full scan | A full scan begins with a quick scan and then scans all mounted fixed disks and removable/network drives (if the full scan is configured to do so).A full scan can take a few hours or days to complete, depending on the amount and type of data that needs to be scanned. The full scan uses the security intelligence definitions installed at the time the scan starts. If new updates are released during the full scan, another full scan is required in order to scan for new threat detections contained in the latest update. Due to the time and resources involved, we generally don't recommend scheduling full scans. |
| Custom scan | A custom scan runs on files and folders that you specify. For example, you can choose to scan a USB drive or a specific folder on your device's local drive. |

Tip

If you have a Network-Attached Storage (NAS) or Storage Area Network (SAN), you can use Internet Content Adaptation Protocol (ICAP) scanning, which enables antivirus scanning of network storage traffic, with the Microsoft Defender Antivirus engine. For more information, see [Tech Community Blog: MetaDefender ICAP with Windows Defender Antivirus: World-class security for hybrid environments](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/metadefender-icap-with-windows-defender-antivirus-world-class/ba-p/800234).

## How to choose a scan type

Use the following table to choose a scan type. Also see [Microsoft Defender Antivirus scan considerations and best practices](mdav-scan-best-practices).

| Scenario | Recommended scan type |
| --- | --- |
| You want to set up regular, scheduled scans | Quick scan  A quick scan checks the processes, memory, profiles, and certain locations on the device. Together with [always-on real-time protection](configure-real-time-protection-microsoft-defender-antivirus), a quick scan helps provide strong coverage both for malware that starts with the system and kernel-level malware. Real-time protection reviews files when they're opened and closed, and whenever a user navigates to a folder. |
| Threats, such as malware, are detected on an individual device | Quick scan  In most cases, a quick scan will catch and clean up detected malware. |
| You want to run an [on-demand scan](run-scan-microsoft-defender-antivirus) | Quick scan |
| You want to make sure a portable device, such as a USB drive, doesn't contain malware | Custom scan  A custom scan enables you to select specific locations, folders, or files, and runs a quick scan. |
| You have installed or re-enabled Microsoft Defender Antivirus | Quick scan or full scan A quick scan checks the processes, memory, profiles, and certain locations on the device. If you prefer, you can choose to run a full scan after you have enabled or installed Microsoft Defender Antivirus. Just keep in mind it can take a while to run a full scan. |

## Important points to keep in mind

Keep the following points in mind when configuring scheduled scans:

- You can configure two types of scheduled scans:

    1. **Daily Scan**: Runs once per day and can only be a **quick scan**.
    2. **Weekly Scan**: Runs once per week and can be either a **quick scan** or a **full scan**.
- By default, Microsoft Defender Antivirus checks for an update 15 minutes before the time of any scheduled scans. You can [manage the schedule for when protection updates should be downloaded and applied](manage-protection-update-schedule-microsoft-defender-antivirus) to override this default.
- If a device is unplugged and running on battery during a scheduled full scan, the scheduled scan stops with event 1002, which states that the scan stopped before completion. Microsoft Defender Antivirus runs a full scan at the next scheduled time.
- Scheduled scans run according to the local time zone of the device.
- Malicious files can be stored in locations that aren't included in a quick scan. However, [always-on, real-time protection](configure-protection-features-microsoft-defender-antivirus) reviews all files that are opened & closed, and any files that are in folders that are accessed by a user. The combination of real-time protection and a quick scan helps provide strong protection against malware.
- On-access protection with [cloud-delivered protection](cloud-protection-microsoft-defender-antivirus) helps ensure that all the files accessed on the system are being scanned with the latest security intelligence and cloud machine learning models.
- When real-time protection detects malware and the extent of the affected files isn't determined initially, Microsoft Defender Antivirus initiates a full scan as part of the remediation process.
- If a device is offline for an extended period of time, a full scan can take longer to complete.
- You can configure quick scans to scan real-time protection exclusions by using PowerShell, Intune, or Group Policy.

## Scheduled quick scan performance optimization

As a performance optimization, Microsoft Defender Antivirus skips running scheduled quick scans in some situations. This optimization only applies to a quick scan when initiated by a schedule – this optimization doesn't affect a quick scan initiated by an [on-demand antivirus](run-scan-microsoft-defender-antivirus) scan. The scheduled quick-scan optimization reduces performance degradation by avoiding a scheduled quick scan when that scan isn't necessary and skipping the scan won't affect protection.

With the scheduled quick-scan optimization enabled, Microsoft Defender Antivirus skips a newly scheduled quick scan if a qualified quick scan ran within the last seven days. A quick scan is considered to be *qualified* if:

- The scan occurs after the last [Microsoft Defender Antivirus security intelligence update](microsoft-defender-antivirus-updates) was installed;
- [Real-time protection](configure-protection-features-microsoft-defender-antivirus) wasn't disabled during that time period; and,
- The machine was rebooted.

The scheduled quick-scan optimization *doesn't* apply to the following conditions:

- If Microsoft Defender for Endpoint is [managed by a configuration tool such as Intune or Group Policy](configuration-management-reference-microsoft-defender-antivirus)
- If Microsoft Defender [Endpoint Detection and Response (EDR)](overview-endpoint-detection-response) is installed
- If the computer was restarted since the last quick scan
- If [real-time protection](configure-real-time-protection-microsoft-defender-antivirus) is disabled after the last quick scan occurred
- If the last initiated quick scan wasn't completed

The scheduled quick-scan optimization applies to machines running Windows 10 Anniversary Update (version 1607) and all subsequent Windows releases, as well as Windows Server 2016 (version 1607) and subsequent Windows Server releases, but doesn't apply to Core Server installations.