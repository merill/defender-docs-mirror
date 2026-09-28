---
layout: Conceptual
title: Configure Microsoft Defender Antivirus with Group Policy - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/use-group-policy-microsoft-defender-antivirus
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use a Group Policy to configure and manage Microsoft Defender Antivirus on your endpoints in Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.localizationpriority: medium
author: chrisda
ms.author: chrisda
ms.custom: nextgen, msecd-doc-authoring-1015
ms.date: 2026-08-12T00:00:00.0000000Z
ms.reviewer: ksarens, jtoole, pahuijbr, yongrhee
ms.subservice: ngp
ms.topic: how-to
ms.collection:
- m365-security
- tier2
- mde-ngp
ai-usage: ai-assisted
locale: en-us
document_id: 4f34f650-c716-9937-179b-c9500abe8415
document_version_independent_id: 4f34f650-c716-9937-179b-c9500abe8415
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/use-group-policy-microsoft-defender-antivirus.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: use-group-policy-microsoft-defender-antivirus
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/use-group-policy-microsoft-defender-antivirus.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 7912299b-d129-2d66-82e7-9ce255ae66fb
---

# Configure Microsoft Defender Antivirus with Group Policy - Microsoft Defender for Endpoint | Microsoft Learn

## Overview

This article describes how to use [Group Policy](/en-us/windows/win32/srvnodes/group-policy) to configure and manage Microsoft Defender Antivirus settings, including step-by-step instructions and a reference table of commonly used Group Policy settings. Before you begin, review the prerequisites.

We recommend [Microsoft Intune](/en-us/intune/intune-service/fundamentals/what-is-intune) to manage Microsoft Defender Antivirus settings. You can also use Group Policy to set up and manage some of these settings.

Important

If your organization uses [tamper protection](tamper-protection-overview), changes to [tamper-protected settings](tamper-protection-overview#what-happens-when-tamper-protection-is-turned-on) are ignored. You also can't turn off tamper protection with Group Policy.

If tamper protection blocks changes on a device, use [troubleshooting mode](troubleshooting-mode-enable) to turn it off on that device. When troubleshooting mode ends, tamper-protected settings go back to their set values.

## Prerequisites

To use Group Policy to set up Microsoft Defender Antivirus, make sure your environment meets these requirements.

### Supported operating systems

You can use Group Policy to set up Microsoft Defender Antivirus on these operating systems:

- Windows
- Windows Server

## Configure Microsoft Defender Antivirus using Group Policy

In general, you can use the following procedure to configure or change some settings for Microsoft Defender Antivirus.

1. In Centralized Group Policy, open the [Group Policy Management Console (GPMC)](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-management-console) on your Group Policy management computer.
2. In the GPMC console tree, expand Group Policy Objects in the forest and domain containing the GPO you want to edit.
3. Right-click the GPO, and then select **Edit**.
4. In the **Group Policy Management Editor**, go to **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus**.

    Note

    Group Policy paths before Windows 10, version 2004 (May 2020) might use *Windows* Defender Antivirus instead of *Microsoft* Defender Antivirus. Both names refer to the same policy location.
5. In the details pane of **Microsoft Defender Antivirus**, find the section that contains the setting you want to change. These sections are listed as **Location** in the Group Policy settings and resources table.
6. In the details pane of the selected section, open the setting. To open and configure a setting, use any of the following methods:

    - Double-click the setting.
    - Right-click the setting, and then select **Edit**.
    - Select the setting, and then select **Action** &gt; **Edit**.
7. In the setting window that opens, configure the setting, and then select **OK**.

Tip

You can also configure Group Policy locally on individual devices by using the Local Group Policy Editor (`gpedit.msc`). Navigate to the same path: **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus**.

## Group Policy settings and resources

The following table lists commonly used Group Policy settings that are available in Windows 10 and later, Windows Server 2016 and later, including if you are running Windows Server 2012 R2 with the unified Microsoft Defender for Endpoint client.

Tip

For the most current settings, get the latest ADMX files in your central store to access the correct policy options. See [How to create and manage the Central Store for Group Policy Administrative Templates in Windows](/en-us/troubleshoot/windows-client/group-policy/create-and-manage-central-store) and download the latest files.

| Location | Setting | Article |
| --- | --- | --- |
| Client interface | Enable headless UI mode | [Prevent users from seeing or interacting with the Microsoft Defender Antivirus user interface](prevent-end-user-interaction-microsoft-defender-antivirus) |
| Client interface | Display more text to clients when they need to perform an action | [Configure the notifications that appear on endpoints](configure-notifications-microsoft-defender-antivirus) |
| Client interface | Suppress all notifications | [Configure the notifications that appear on endpoints](configure-notifications-microsoft-defender-antivirus) |
| Client interface | Suppresses reboot notifications | [Configure the notifications that appear on endpoints](configure-notifications-microsoft-defender-antivirus) |
| Exclusions | Extension Exclusions | [Configure and validate exclusions in Microsoft Defender Antivirus scans](microsoft-defender-antivirus-exclusions-configure) |
| Exclusions | IP Address Exclusions | [Add network protection exclusions](troubleshoot-np#add-exclusions) |
| Exclusions | Path Exclusions | [Configure and validate exclusions in Microsoft Defender Antivirus scans](microsoft-defender-antivirus-exclusions-configure) |
| Exclusions | Process Exclusions | [Configure and validate exclusions in Microsoft Defender Antivirus scans](microsoft-defender-antivirus-exclusions-configure) |
| Exclusions | Turn off Auto Exclusions | [Configure and validate exclusions in Microsoft Defender Antivirus scans](microsoft-defender-antivirus-exclusions-configure) |
| Features | Device Control | [Configure device control in Microsoft Defender for Endpoint using Group Policy](device-control-configure#configure-device-control-with-group-policy) |
| Features | Enable EDR in Block Mode | [EDR in block mode: Group Policy](edr-in-block-mode#group-policy) |
| MAPS | Configure the "Block at First Sight" feature | [Enable block at first sight](configure-block-at-first-sight-microsoft-defender-antivirus) |
| MAPS | Join Microsoft MAPS | [Enable cloud-delivered protection](cloud-protection-configure) |
| MAPS | Send file samples when further analysis is required | [Enable cloud-delivered protection](cloud-protection-configure) |
| MAPS | Configure local setting override for reporting to Microsoft MAPS | [Prevent or allow users to locally modify policy settings](configure-local-policy-overrides-microsoft-defender-antivirus) |
| MpEngine | Configure extended cloud check | [Configure the cloud block time-out period](configure-cloud-block-timeout-period-microsoft-defender-antivirus) |
| MpEngine | Disable gradual rollout of Microsoft Defender updates | [Configure updates: Group Policy](configure-updates#group-policy) |
| MpEngine | Enable file hash computation feature | [Create indicators for files](indicator-file#windows-prerequisites)This drives the ability to enforce Indicators of Compromise (IoC) by using file hash allow/block indicators, available in Defender for Endpoint Plan 1 and Plan 2, and in Defender for Business. Note that Microsoft Defender Antivirus automatically does hash-based computation for the antimalware engine, so you don't have to do anything extra unless it is a [VDI non-persistent image](deployment-vdi-microsoft-defender-antivirus). |
| MpEngine | Select cloud protection level | [Specify the cloud-delivered protection level](cloud-protection-configure#specify-the-cloud-protection-level) |
| Network inspection system | Convert warn verdict to block | [Network protection: Warn experience](network-protection#warn-experience) |
| Network inspection system | Specify more definition sets for network traffic inspection | Not used (deprecated) |
| Network inspection system | Turn on asynchronous inspection | [Optimizing network protection performance](network-protection#optimizing-network-protection-performance) |
| Network inspection system | Turn on definition retirement | Not used (deprecated) |
| Network inspection system | Turn on protocol recognition | Not used (deprecated) |
| Quarantine | Configure local setting override for the removal of items from Quarantine folder | [Prevent or allow users to locally modify policy settings](configure-local-policy-overrides-microsoft-defender-antivirus) |
| Quarantine | Configure removal of items from Quarantine folder | [Configure remediation for Microsoft Defender Antivirus scans](configure-remediation-microsoft-defender-antivirus) |
| Real-time protection | Configure local setting override for monitoring file and program activity on your computer | [Prevent or allow users to locally modify policy settings](configure-local-policy-overrides-microsoft-defender-antivirus) |
| Real-time protection | Configure local setting override for monitoring for incoming and outgoing file activity | [Prevent or allow users to locally modify policy settings](configure-local-policy-overrides-microsoft-defender-antivirus) |
| Real-time protection | Configure local setting override for scanning all downloaded files and attachments | [Prevent or allow users to locally modify policy settings](configure-local-policy-overrides-microsoft-defender-antivirus) |
| Real-time protection | Configure local setting override to turn on behavior monitoring | [Prevent or allow users to locally modify policy settings](configure-local-policy-overrides-microsoft-defender-antivirus) |
| Real-time protection | Configure local setting override to turn on real-time protection | [Prevent or allow users to locally modify policy settings](configure-local-policy-overrides-microsoft-defender-antivirus) |
| Real-time protection | Define the maximum size of downloaded files and attachments to be scanned | [Enable and configure Microsoft Defender Antivirus always-on protection and monitoring](configure-real-time-protection-microsoft-defender-antivirus) |
| Real-time protection | Configure performance mode status | [Performance mode: Group Policy](microsoft-defender-endpoint-antivirus-performance-mode#group-policy) |
| Real-time protection | Configure real-time protection and Security Intelligence Updates during OOBE | [Enable and configure Microsoft Defender Antivirus always-on protection](configure-real-time-protection-microsoft-defender-antivirus) |
| Real-time protection | Monitor file and program activity on your computer | [Enable and configure Microsoft Defender Antivirus always-on protection and monitoring](configure-real-time-protection-microsoft-defender-antivirus) |
| Real-time protection | Scan all downloaded files and attachments | [Enable and configure Microsoft Defender Antivirus always-on protection and monitoring](configure-real-time-protection-microsoft-defender-antivirus) |
| Real-time protection | Turn off real-time protection | [Enable and configure Microsoft Defender Antivirus always-on protection and monitoring](configure-real-time-protection-microsoft-defender-antivirus) |
| Real-time protection | Turn on behavior monitoring | [Enable and configure Microsoft Defender Antivirus always-on protection and monitoring](configure-real-time-protection-microsoft-defender-antivirus) |
| Real-time protection | Turn on process scanning whenever real-time protection is enabled | [Enable and configure Microsoft Defender Antivirus always-on protection and monitoring](configure-real-time-protection-microsoft-defender-antivirus) |
| Real-time protection | Turn on raw volume write notifications | [Enable and configure Microsoft Defender Antivirus always-on protection and monitoring](configure-real-time-protection-microsoft-defender-antivirus) |
| Real-time protection | Configure monitoring for incoming and outgoing file and program activity | [Enable and configure Microsoft Defender Antivirus always-on protection and monitoring](configure-real-time-protection-microsoft-defender-antivirus) |
| Remediation | Configure local setting override for the time of day to run a scheduled full scan to complete remediation | [Prevent or allow users to locally modify policy settings](configure-local-policy-overrides-microsoft-defender-antivirus) |
| Remediation | Specify the day of the week to run a scheduled full scan to complete remediation | [About scheduled quick or full Microsoft Defender Antivirus scans](schedule-antivirus-scans) |
| Remediation | Specify the time of day to run a scheduled full scan to complete remediation | [About scheduled quick or full Microsoft Defender Antivirus scans](schedule-antivirus-scans) |
| Reporting | Configure time interval for service health reports | [Configure Microsoft Defender Antivirus notifications that appear on endpoints](configure-notifications-microsoft-defender-antivirus) |
| Reporting | Configure time out for detections in critically failed state | [Configure Microsoft Defender Antivirus notifications that appear on endpoints](configure-notifications-microsoft-defender-antivirus) |
| Reporting | Configure time out for detections in noncritical failed state | [Configure Microsoft Defender Antivirus notifications that appear on endpoints](configure-notifications-microsoft-defender-antivirus) |
| Reporting | Configure time out for detections in recently remediated state | [Configure Microsoft Defender Antivirus notifications that appear on endpoints](configure-notifications-microsoft-defender-antivirus) |
| Reporting | Configure time out for detections in requiring additional action | [Configure Microsoft Defender Antivirus notifications that appear on endpoints](configure-notifications-microsoft-defender-antivirus) |
| Reporting | Configure Watson events | [Configure Microsoft Defender Antivirus notifications that appear on endpoints](configure-notifications-microsoft-defender-antivirus) |
| Reporting | Configure whether to report Dynamic Signature dropped events | [Configure Microsoft Defender Antivirus notifications that appear on endpoints](configure-notifications-microsoft-defender-antivirus) |
| Reporting | Configure Windows software trace preprocessor components | [Configure Microsoft Defender Antivirus notifications that appear on endpoints](configure-notifications-microsoft-defender-antivirus) |
| Reporting | Configure WPP tracing level | [Configure Microsoft Defender Antivirus notifications that appear on endpoints](configure-notifications-microsoft-defender-antivirus) |
| Reporting | Turn off enhanced notifications | [Configure the notifications that appear on endpoints](configure-notifications-microsoft-defender-antivirus) |
| Root | Turn off Microsoft Defender Antivirus | Not used. If you're using or planning to use a non-Microsoft antivirus product, see [Microsoft Defender Antivirus compatibility with other security products](microsoft-defender-antivirus-compatibility). |
| Root | Define addresses to bypass proxy server | [Configure device proxy and Internet connectivity settings](configure-proxy-internet#configure-a-static-proxy-for-microsoft-defender-antivirus) |
| Root | Define proxy autoconfig (.pac) for connecting to the network | [Configure device proxy and Internet connectivity settings](configure-proxy-internet#configure-a-static-proxy-for-microsoft-defender-antivirus) |
| Root | Define proxy server for connecting to the network | [Configure device proxy and Internet connectivity settings](configure-proxy-internet#configure-a-static-proxy-for-microsoft-defender-antivirus) |
| Root | Define the directory path to copy support log files | [Configure device proxy and Internet connectivity settings](configure-proxy-internet) |
| Root | Configure local administrator merge behavior for lists | [Prevent or allow users to locally modify policy settings](configure-local-policy-overrides-microsoft-defender-antivirus) |
| Root | Allow anti-malware service to start up with normal priority | [Configure remediation for Microsoft Defender Antivirus scans](configure-remediation-microsoft-defender-antivirus) |
| Root | Allow anti-malware service to remain running always | [Configure remediation for Microsoft Defender Antivirus scans](configure-remediation-microsoft-defender-antivirus) |
| Root | Turn off routine remediation | [Configure remediation for Microsoft Defender Antivirus scans](configure-remediation-microsoft-defender-antivirus) |
| Root | Randomize scheduled task times | [About scheduled quick or full Microsoft Defender Antivirus scans](schedule-antivirus-scans) |
| Root | Select the channel for Microsoft Defender daily security intelligence updates | [Update channels for security intelligence updates](manage-gradual-rollout#update-channels-for-security-intelligence-updates) |
| Root | Select the channel for Microsoft Defender monthly engine updates | [Update channels for monthly updates](manage-gradual-rollout#update-channels-for-monthly-updates) |
| Root | Select the channel for Microsoft Defender monthly platform updates | [Update channels for monthly updates](manage-gradual-rollout#update-channels-for-monthly-updates) |
| Scan | Allow users to pause scan | [Prevent users from seeing or interacting with the Microsoft Defender Antivirus user interface](prevent-end-user-interaction-microsoft-defender-antivirus) (Not supported on Windows 10 or newer, and Windows Server 2016 and later) |
| Scan | Check for the latest virus and spyware definitions before running a scheduled scan | [Manage event-based forced updates](manage-event-based-updates-microsoft-defender-antivirus) |
| Scan | Define the number of days after which a catch-up scan is forced | [Manage updates for endpoints that are out of date](manage-outdated-endpoints-microsoft-defender-antivirus) |
| Scan | Turn on catch up full scan | [Manage updates for endpoints that are out of date](manage-outdated-endpoints-microsoft-defender-antivirus) |
| Scan | Turn on catch up quick scan | [Manage updates for endpoints that are out of date](manage-outdated-endpoints-microsoft-defender-antivirus) |
| Scan | Configure local setting override for maximum percentage of CPU utilization | [Prevent or allow users to locally modify policy settings](configure-local-policy-overrides-microsoft-defender-antivirus) |
| Scan | Configure local setting override for schedule scan day | [Prevent or allow users to locally modify policy settings](configure-local-policy-overrides-microsoft-defender-antivirus) |
| Scan | Configure local setting override for scheduled quick scan time | [Prevent or allow users to locally modify policy settings](configure-local-policy-overrides-microsoft-defender-antivirus) |
| Scan | Configure local setting override for scheduled scan time | [Prevent or allow users to locally modify policy settings](configure-local-policy-overrides-microsoft-defender-antivirus) |
| Scan | Configure local setting override for the scan type to use for a scheduled scan | [Prevent or allow users to locally modify policy settings](configure-local-policy-overrides-microsoft-defender-antivirus) |
| Scan | Configure low CPU priority for scheduled scans | [Configure Microsoft Defender Antivirus scanning options](configure-advanced-scan-types-microsoft-defender-antivirus) |
| Scan | Configure scanning of network files | [Configure Microsoft Defender Antivirus scanning options](configure-advanced-scan-types-microsoft-defender-antivirus) |
| Scan | CPU throttling type | [Configure Microsoft Defender Antivirus scanning options](configure-advanced-scan-types-microsoft-defender-antivirus) |
| Scan | Create a system restore point | [Configure remediation for Microsoft Defender Antivirus scans](configure-remediation-microsoft-defender-antivirus) |
| Scan | Turn on removal of items from scan history folder | [Configure remediation for Microsoft Defender Antivirus scans](configure-remediation-microsoft-defender-antivirus) |
| Scan | Turn on heuristics | [Enable and configure Microsoft Defender Antivirus always-on protection and monitoring](configure-real-time-protection-microsoft-defender-antivirus) |
| Scan | Turn on e-mail scanning | [Configure scanning options in Microsoft Defender Antivirus](configure-advanced-scan-types-microsoft-defender-antivirus) |
| Scan | Turn on reparse point scanning | [Configure scanning options in Microsoft Defender Antivirus](configure-advanced-scan-types-microsoft-defender-antivirus) |
| Scan | Run full scan on mapped network drives | [Configure scanning options in Microsoft Defender Antivirus](configure-advanced-scan-types-microsoft-defender-antivirus) |
| Scan | Scan archive files | [Configure scanning options in Microsoft Defender Antivirus](configure-advanced-scan-types-microsoft-defender-antivirus) |
| Scan | Scan excluded files and directories during quick scan | [Configure scanning options: Settings and locations](configure-advanced-scan-types-microsoft-defender-antivirus#settings-and-locations) |
| Scan | Scan packed executables | [Configure scanning options in Microsoft Defender Antivirus](configure-advanced-scan-types-microsoft-defender-antivirus) |
| Scan | Scan scripts | [Configure scanning options in Microsoft Defender Antivirus](configure-advanced-scan-types-microsoft-defender-antivirus)<br>Also see [Defender/AllowScriptScanning](/en-us/windows/client-management/mdm/policy-csp-defender). |
| Scan | Scan removable drives | [Configure scanning options in Microsoft Defender Antivirus](configure-advanced-scan-types-microsoft-defender-antivirus) |
| Scan | Specify the maximum depth to scan archive files | [Configure scanning options in Microsoft Defender Antivirus](configure-advanced-scan-types-microsoft-defender-antivirus) |
| Scan | Specify the maximum percentage of CPU utilization during a scan | [Configure scanning options in Microsoft Defender Antivirus](configure-advanced-scan-types-microsoft-defender-antivirus) |
| Scan | Specify the maximum size of archive files to be scanned | [Configure scanning options in Microsoft Defender Antivirus](configure-advanced-scan-types-microsoft-defender-antivirus) |
| Scan | Specify the day of the week to run a scheduled scan | [About scheduled quick or full Microsoft Defender Antivirus scans](schedule-antivirus-scans) |
| Scan | Specify the interval to run quick scans per day | [About scheduled quick or full Microsoft Defender Antivirus scans](schedule-antivirus-scans) |
| Scan | Specify the scan type to use for a scheduled scan | [About scheduled quick or full Microsoft Defender Antivirus scans](schedule-antivirus-scans) |
| Scan | Specify the time for a daily quick scan | [About scheduled quick or full Microsoft Defender Antivirus scans](schedule-antivirus-scans) |
| Scan | Specify the time of day to run a scheduled scan | [About scheduled quick or full Microsoft Defender Antivirus scans](schedule-antivirus-scans) |
| Scan | Start the scheduled scan only when computer is on but not in use | [About scheduled quick or full Microsoft Defender Antivirus scans](schedule-antivirus-scans) |
| Scan | Trigger a quick scan after X days without any scans | [Configure scanning options: Settings and locations](configure-advanced-scan-types-microsoft-defender-antivirus#settings-and-locations) |
| Security intelligence updates | Allow security intelligence updates from Microsoft Update | [Manage updates for mobile devices and virtual machines (VMs)](manage-updates-mobile-devices-vms-microsoft-defender-antivirus) |
| Security intelligence updates | Allow security intelligence updates when running on battery power | [Manage updates for mobile devices and virtual machines (VMs)](manage-updates-mobile-devices-vms-microsoft-defender-antivirus) |
| Security intelligence updates | Allow Microsoft Defender Antivirus to update and communicate over a metered connection | [Manage Microsoft Defender Antivirus updates and scans for endpoints that are out of date](manage-outdated-endpoints-microsoft-defender-antivirus) |
| Security intelligence updates | Allow notifications to disable definitions-based reports to Microsoft MAPS | [Manage event-based forced updates](manage-event-based-updates-microsoft-defender-antivirus) |
| Security intelligence updates | Allow real-time security intelligence updates based on reports to Microsoft MAPS | [Manage event-based forced updates](manage-event-based-updates-microsoft-defender-antivirus) |
| Security intelligence updates | Check for the latest virus and spyware security intelligence on startup | [Manage event-based forced updates](manage-event-based-updates-microsoft-defender-antivirus) |
| Security intelligence updates | Define file shares for downloading security intelligence updates | [Manage Microsoft Defender Antivirus protection and security intelligence updates](manage-protection-updates-microsoft-defender-antivirus) |
| Security intelligence updates | Define security intelligence location for VDI clients | [Configure Microsoft Defender Antivirus on a remote desktop or VDI: Group Policy](deployment-vdi-microsoft-defender-antivirus#group-policy) |
| Security intelligence updates | Define the number of days after which a catch up security intelligence update is required | [Manage updates for endpoints that are out of date](manage-outdated-endpoints-microsoft-defender-antivirus) |
| Security intelligence updates | Define the number of days before spyware security intelligence are considered out of date | [Manage updates for endpoints that are out of date](manage-outdated-endpoints-microsoft-defender-antivirus) |
| Security intelligence updates | Define the number of days before virus security intelligence are considered out of date | [Manage updates for endpoints that are out of date](manage-outdated-endpoints-microsoft-defender-antivirus) |
| Security intelligence updates | Define the order of sources for downloading security intelligence updates | [Manage Microsoft Defender Antivirus protection and security intelligence updates](manage-protection-updates-microsoft-defender-antivirus) |
| Security intelligence updates | Initiate security intelligence update on startup | [Manage event-based forced updates](manage-event-based-updates-microsoft-defender-antivirus) |
| Security intelligence updates | Specify the day of the week to check for security intelligence updates | [Manage when protection updates should be downloaded and applied](manage-protection-update-schedule-microsoft-defender-antivirus) |
| Security intelligence updates | Specify the interval to check for security intelligence updates | [Manage when protection updates should be downloaded and applied](manage-protection-update-schedule-microsoft-defender-antivirus) |
| Security intelligence updates | Specify the time to check for security intelligence updates | [Manage when protection updates should be downloaded and applied](manage-protection-update-schedule-microsoft-defender-antivirus) |
| Security intelligence updates | Turn on scan after Security intelligence update | [About scheduled quick or full Microsoft Defender Antivirus scans](schedule-antivirus-scans) |
| Threats | Specify threat alert levels at which default action shouldn't be taken when detected | [Configure remediation for Microsoft Defender Antivirus scans](configure-remediation-microsoft-defender-antivirus) |
| Threats | Specify threats upon which default action shouldn't be taken when detected | [Configure remediation for Microsoft Defender Antivirus scans](configure-remediation-microsoft-defender-antivirus) |

Tip

Instead of using "Run full scan on mapped network drives", if you have a Network-Attached Storage (NAS) or Storage Area Network (SAN), you can use Internet Content Adaption Protocol (ICAP) scanning with the Microsoft Defender Antivirus engine. For more information, see **[Tech Community Blog: MetaDefender ICAP with Windows Defender Antivirus: World-class security for hybrid environments](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/metadefender-icap-with-windows-defender-antivirus-world-class/ba-p/800234)**.

**Performance tip**: Due to a variety of factors, Microsoft Defender Antivirus, like other antivirus software, can cause performance issues on endpoint devices. In some cases, you might need to tune the performance of Microsoft Defender Antivirus to alleviate those performance issues. Microsoft's **Performance analyzer** is a PowerShell command-line tool that helps determine which files, file paths, processes, and file extensions might be causing performance issues. You can use the information gathered using Performance analyzer to better assess performance issues and apply remediation actions. For more information, see: [Performance analyzer for Microsoft Defender Antivirus](tune-performance-defender-antivirus).