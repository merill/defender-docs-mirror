---
layout: Conceptual
title: Troubleshoot performance issues - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-performance-issues
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Troubleshoot high CPU usage related to the real-time protection service in Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.date: 2025-10-20T00:00:00.0000000Z
ms.topic: troubleshooting
ms.subservice: ngp
ms.collection:
- m365-security
- tier3
- mde-ngp
locale: en-us
document_id: 3a55c747-995d-7a57-06d7-542b1d4e2029
document_version_independent_id: 3a55c747-995d-7a57-06d7-542b1d4e2029
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/troubleshoot-performance-issues.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: troubleshoot-performance-issues
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/troubleshoot-performance-issues.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: ae28f1cf-14bc-fb9c-5f0c-873a683e907c
---

# Troubleshoot performance issues - Microsoft Defender for Endpoint | Microsoft Learn

If your system is having high CPU usage or performance issues related to the Microsoft Defender Antivirus (Anti-malware Service Executable, MsMpEng.exe, Microsoft Defender Antivirus).

As an admin, you can also troubleshoot these issues on your own.

First, you might want to check if other software is causing the issue. Read Check with the vendor for known issues with antivirus exclusions.

## Prerequisites

### Supported operating systems

- Windows
- Windows Server

## Common reasons for higher CPU utilization by Microsoft Defender Antivirus

| Reason | Solution |
| --- | --- |
| 1. **Binaries not signed** (`.exe`, `.dll`, and so on) Anytime that a binary (such as `.exe`,`.dll`, and so on) is launched/started, if it's not digitally signed, Microsoft Defender Antivirus starts a real-time protection scan or when you're running a scheduled scan, and/or on-demand scan. | You should consider signing the binaries using an internal PKI. And/or reaching out to the vendor so they could sign the binary. And adding the certificate to the [Indicators – Certificate - allow](indicator-certificates)We recommend that software vendors follow the various guidelines in [Partnering with the industry to minimize false positives](https://www.microsoft.com/security/blog/2018/08/16/partnering-with-the-industry-to-minimize-false-positives/). The software vendor or software developer can submit the application, service, or script in the [Microsoft Security Intelligence portal](https://www.microsoft.com/wdsi/filesubmission?persona=SoftwareDeveloper).As a work-around, you can follow these steps: 1. (Preferred) For .exe's and dll's use [Indicators – File hash - allow](indicator-file)2. (Alternative) Add [Antivirus exclusions (process+path)](microsoft-defender-antivirus-exclusions-configure). |
| 2. **Using HTA's, CHM's and different files as databases**. Anytime that Microsoft Defender Antivirus must extract and/or scan complex file formats, higher CPU utilization can occur. | Consider switching to using actual databases if you need to save info and query it. As a workaround, add [Antivirus exclusions (process+path)](microsoft-defender-antivirus-exclusions-configure). |
| 3. **Using obfuscations on scripts**. If you obfuscate scripts, Microsoft Defender Antivirus in order to check if the script contains malicious payloads, it can use more CPU utilization while scanning. | Use script obfuscation only when necessary.As a workaround, add [Antivirus exclusions (process+path)](microsoft-defender-antivirus-exclusions-configure). |
| 4. **Not letting the Microsoft Defender Antivirus cache finish before sealing the image**. | If you're creating a VDI image such as for a non-persistent image, make sure that cache maintenance completes before the image is sealed.  For more information, see [Configure Microsoft Defender Antivirus on a remote desktop or virtual desktop infrastructure environment](deployment-vdi-microsoft-defender-antivirus). |
| 5. **Misspelled exclusions**. | Use `MpCmdRun.exe -CheckExclusion -Path <PathAndFile or Path>` to validate path-based exclusions. For more information, see [Verify whether a file or folder is excluded by using MpCmdRun](microsoft-defender-antivirus-exclusions-configure#verify-whether-a-file-or-folder-is-excluded-by-using-mpcmdrun). |
| 6. **When a path exclusion is added, it works for scanning flows**. Behavior Monitoring (BM) and Network Real-time Inspection (NRI) can still cause performance issues. | As a workaround, take these steps: 1. (Preferred) For .exe's and dll's use [Indicators – File hash - allow](indicator-file) or [Indicators – Certificate - allow](indicator-certificates)2. (Alternative) [Add Antivirus exclusions (process+path)](microsoft-defender-antivirus-exclusions-configure). |
| 7. **File hash computation**. If you enable file hash computation, which is used for [file indicators](indicator-file), there's more performance overhead. For example, copying large files from a network share onto your local device, especially over a VPN connection, might have an effect on device performance. | This is where you, and your leadership team will have to make a decision, of having more security or less CPU utilization. One possible solution is to disable the File hash computation feature. Go to **Computer Configuration** &gt; **Administrative Templates** &gt; **Windows Components** &gt; **Microsoft Defender Antivirus** &gt; **MpEngine**, and then enable file hash computation features. **Note**: To enable Indicators - File hash functionality, this feature must be activated. |

### To help determine which component might be contributing to higher CPU utilization

| Component | Solution |
| --- | --- |
| Real-time protection (RTP) scanning | You can use [Troubleshooting mode](troubleshooting-mode-enable) to turn off [Tamper Protection](tamper-protection-troubleshoot). Once Tamper Protection is turned off, you could turn off the "Real-time protection" temporarily, in order to rule it out.See the previous section, Common reasons for higher CPU utilization by Microsoft Defender Antivirus. |
| Scheduled scanning | Check your default scheduled scan settings**General scheduled scan settings**.- Configure low CPU priority for scheduled scans (Use low CPU priority for scheduled scans). The thread priority in Windows for normal scans has two values: `8` (lower) and `9` (higher). By setting this to `enabled`, you're lowering the scheduled scan thread priority from `9` to `8`, which enables other application threads to run with a higher priority, thus getting more CPU time than Microsoft Defender Antivirus. - Specify the maximum percentage of CPU utilization during a scan (CPU usage limit per scan). `50` is the default setting; you can lower it to `20` or `30`. If you have a change control window, by modifying the amount of CPU that can be used, causes the scan to take longer. - Start the scheduled scan only when computer is on but not in use by setting `ScanOnlyIfIdle` to `Not configured` (it's enabled by default). It requires the machine to be idle, meaning the CPU usage overall of the device has to be lower than 80%. **Daily quick scan settings**- Set `Specify the interval to run quick scans per day` to `Not configured` (How many hours have elapsed, before the next quick scan runs - 0 to 24 hours)- Set `Specify the time for a daily quick scan (Run daily quick scan at)` to `12 PM`. **Run a weekly scheduled scan (quick or full) settings**- Specify the scan type to use for a scheduled scan (Set `Scan type` to `Not configured`). - Specify the time of day to run a scheduled scan (Set `Day of week to run scheduled scan` to `Not configured`). - Specify the day of the week to run a scheduled scan (Set `Time of day to run a scheduled scan` to `Not configured`). |
| Scan after a security intelligence update. | By default, Microsoft Defender Antivirus scans after a security intelligence update for optimal protection purposes. If scheduled scans are enabled, you might think that there are scans that are run outside of the schedule. This is where you, and your leadership team will have to make a decision, of having more security or less CPU utilization. As a workaround, in Group Policy (or another management tool, such as MDM), go to **Computer Configuration** &gt; **Administrative Templates** &gt; **Microsoft Defender Antivirus** &gt; **Security Intelligence Updates**, and set **Turn on scan after security intelligence update** to `Disabled`. |
| Conflicts with other security software | If you have non-Microsoft security software, such as antivirus, EDR, DLP, endpoint privilege management, VPN, and so on, add the that software to the Microsoft Defender Antivirus exclusions (path + processes), and vice-versa. To get the list of the Microsoft Defender Antivirus binaries, see [Configure your network environment to ensure connectivity with Defender for Endpoint service](configure-environment). |
| Scanning a large number of files or folders | If you have a large file such as an .iso, .vhdx, and so on, sitting in your user profile (desktop, downloads, documents, and so on) and that profile is being redirected to network shares, such as Offline Files (CSC) or OneDrive (or similar products), scans can take longer to run. This is because you're scanning a network, where there's more latency compared to files stored locally on a device.If you don't need the .iso/.vhd/.vhdx, etc. sitting on your profile, move it to a different folder where it's not sitting on a network share (mapped drive, unc share, smb share). |

## What's triggering and causing higher CPU utilization in Microsoft Defender Antivirus

After the proa\ctive steps are complete, you can identify what is triggering and causing the higher CPU utilization:

| # | Tools to help narrow down what's triggering the high CPU utilization | Comments |
| --- | --- | --- |
| 1 | [Collect Microsoft Defender Antivirus diagnostic data](collect-diagnostic-data) | Microsoft Defender Antivirus diagnostic data that you want to include whenever troubleshooting an issue with Microsoft Defender Antivirus. |
| 2 | [Performance analyzer for Microsoft Defender Antivirus](tune-performance-defender-antivirus) | For performance-specific issues related to Microsoft Defender Antivirus, see Performance analyzer for Microsoft Defender Antivirus. This allows you to run the data collection and parse the data, where it's easy to understand. **Note**: Make sure that the issue is reproducing when you collect this data. |
| 3 | [Troubleshoot Microsoft Defender Antivirus performance issues with Process Monitor](troubleshoot-av-performance-issues-with-procmon) | If for some reason that the Microsoft Defender Antivirus performance analyzer doesn't provide with the details that you need to narrow down on what's triggering the high CPU utilization, you can use Process Monitor (ProcMon). Tip: You can collect for 5-10 minutes. **Note**: Make sure that the issue is reproducing when you collect this data. |
| 4 | [Troubleshoot Microsoft Defender Antivirus performance issues with WPRUI](troubleshoot-av-performance-issues-with-wprui) | For more advanced troubleshooting, you can utilize the Windows Performance Recorder UI (WPRUI) or Windows Performance Recorder (WPR). Keep in mind that due to the verbosity of this trace, it should be limited to a maximum of 3 to 5 minutes. Ensure that the issue is actively occurring when you collect this data. |

## Check with the vendor for known issues with antivirus products

If you can readily identify the software affecting system performance, go to the software vendor's knowledge base or support center. Check to see if there are any known issues with antivirus products. If necessary, you can open a support ticket with them and ask them to publish one.

We recommend that software vendors follow the various guidelines in [Partnering with the industry to minimize false positives](https://www.microsoft.com/security/blog/2018/08/16/partnering-with-the-industry-to-minimize-false-positives/). The vendor can submit their software through the [Microsoft Security Intelligence portal](https://www.microsoft.com/wdsi/filesubmission?persona=SoftwareDeveloper).