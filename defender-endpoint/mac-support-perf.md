---
layout: Conceptual
title: Troubleshoot performance issues for Microsoft Defender for Endpoint on macOS - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/mac-support-perf
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Troubleshoot performance issues in Microsoft Defender for Endpoint on macOS.
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
ms.date: 2025-06-20T00:00:00.0000000Z
locale: en-us
document_id: cea7208d-f47b-813b-df51-a4783b529a39
document_version_independent_id: cea7208d-f47b-813b-df51-a4783b529a39
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/mac-support-perf.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mac-support-perf
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/mac-support-perf.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 11cf9bfb-39ea-bcd6-032c-c0fa6bec71c7
---

# Troubleshoot performance issues for Microsoft Defender for Endpoint on macOS - Microsoft Defender for Endpoint | Microsoft Learn

This article provides some general steps that can be used to narrow down performance issues related to Defender for Endpoint on macOS.

Depending on the applications that you're running and your device characteristics, you might experience suboptimal performance when running Microsoft Defender for Endpoint on macOS. In particular, applications or system processes that access many resources over a short timespan can lead to performance issues in Defender for Endpoint on macOS.

Warning

Before you perform the procedures described in this article, make sure that other security products aren't currently running on the device. Multiple security products can conflict and affect the host performance.

## Troubleshoot performance issues using real-time protection statistics

**Applies to:**

- Only performance issues related to Microsoft Defender Antivirus (`wdavdaemon_unprivileged`).

Real-time protection (RTP) is a feature of Defender for Endpoint on macOS that continuously monitors and protects your device against threats. It consists of file and process monitoring and other heuristics.

Prerequisites:

- Microsoft Defender for Endpoint version (Platform Update) 100.90.70 or newer
- If you have [Tamper protection](tamper-protection-macos-configure) turned on in block mode, use [Troubleshooting mode](mac-troubleshoot-mode) to capture real-time-protection-statistics. Otherwise, you get null results.

Tip

As a general best practice, it's recommended to update the [Microsoft Defender for Endpoint agent to latest available version](microsoft-defender-endpoint-releases#linux-releases) and confirming that the issue still persists before investigating further.

To troubleshoot and mitigate performance issues, follow these steps:

1. Disable real-time protection by using one of the methods in the following table, and then observe whether performance improves. This approach helps narrow down whether Microsoft Defender for Endpoint on macOS is contributing to the performance issues.

    | Device management | Method |
    | --- | --- |
    | Device isn't managed by organization | **User interface**: Open Microsoft Defender for Endpoint on macOS and navigate to **Manage settings**. |
    | Device isn't managed by organization | **Terminal**: In Terminal, run the following command: `mdatp config real-time-protection --value disabled` |
    | Device is managed by organization | See [Set preferences for Microsoft Defender for Endpoint on macOS](mac-preferences). |

    If the performance problem persists while real-time protection is off, the origin of the problem could be the endpoint detection and response component. In this case, contact customer support for further instructions and mitigation.
2. Open Finder and navigate to **Applications** &gt; **Utilities**. Open **Activity Monitor** and analyze which applications are using the resources on your system. Typical examples include software updaters and compilers.
3. This feature requires real-time protection to be enabled. To check the status of real-time protection, run the following command:

    ```bash
    mdatp health --field real_time_protection_enabled
    ```

    Verify that the **real\_time\_protection\_enabled** entry is *true*. Otherwise, run the following command to enable it:

    ```bash
    mdatp config real-time-protection --value enabled
    ```

    ```output
    Configuration property updated
    ```
4. To find the applications that are triggering the most scans, you can use real-time statistics gathered by Defender for Endpoint on macOS. Run the following command to enable it:

    ```bash
    mdatp config real-time-protection-statistics --value enabled
    ```

    Tip

    Before proceeding to capture the data, make sure that the high cpu utilization is occurring in the wdavdaemon\_unprivileged by either running top or opening `activity monitor`.
5. To output to a json file, run the following command:

    ```bash
    mdatp diagnostic real-time-protection-statistics --output json > real_time_protection.json
    ```

    Note

    Using `--output json` (note the double dash) ensures that the output format is ready for parsing. The output of this command shows all processes and their associated scan activity.
6. On your macOS system, download the sample Python parser `high_cpu_parser.py` using the command:

    ```bash
    curl -O https://raw.githubusercontent.com/microsoft/mdatp-xplat/master/linux/diagnostic/high_cpu_parser.py
    ```

    The output of this command should be similar to the following:

    ```Output
    --2020-11-14 11:27:27-- https://raw.githubusercontent.com/microsoft.
    mdatp-xplat/master/linus/diagnostic/high_cpu_parser.py
    Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 151.101.xxx.xxx
    Connecting to raw.githubusercontent.com (raw.githubusercontent.com)| 151.101.xxx.xxx| :443... connected.
    HTTP request sent, awaiting response... 200 OK
    Length: 1020 [text/plain]
    Saving to: 'high_cpu_parser.py'
    100%[===========================================>] 1,020    --.-K/s   in
    0s
    ```
7. Type the following commands:

    ```bash
    chmod +x high_cpu_parser.py
    ```

    ```bash
    cat real_time_protection.json | python high_cpu_parser.py  > real_time_protection.log
    ```

    The output should be a list of the top contributors to performance issues. The first column is the process identifier (PID), the second column is the process name, and the last column is the number of scanned files, sorted by impact. Here's an example:

    ```output
    ... > python ~/repo/mdatp-xplat/linux/diagnostic/high_cpu_parser.py <~Downloads/output.json | head -n 10
    27432 None 76703
    73467 actool     1249
    73914 xcodebuild 1081
    73873 bash 1050
    27475 None 836
    1    launchd    407
    73468 ibtool     344
    549  telemetryd_v1   325
    4764 None 228
    125  CrashPlanService 164
    ```
8. To improve the performance of Defender for Endpoint on macOS, locate the one with the highest number under the **Total files scanned** row, and then add an exclusion for it. For more information, see [Configure and validate exclusions for Defender for Endpoint on macOS](mac-exclusions).

    Note

    The application stores statistics in memory and only keeps track of file activity since it was started and real-time protection was enabled. Processes that were launched before or during periods when real time protection was off aren't counted. Additionally, only events which triggered scans are counted.
9. Configure Microsoft Defender for Endpoint on macOS with exclusions for the processes or disk locations that contribute to the performance issues and re-enable real-time protection.

    See [Configure and validate exclusions for Microsoft Defender for Endpoint on macOS](mac-exclusions).

## Troubleshoot performance issues from Behavior Monitoring

See the guide on our support page for [Behavior Monitoring](behavior-monitor-macos).

## Troubleshoot performance issues using Microsoft Defender for Endpoint Client Analyzer

The Microsoft Defender for Endpoint Client Analyzer (MDECA) can collect traces, logs, and diagnostic information in order to troubleshoot performance issues on [onboarded devices](onboard-configure) on macOS.

To run the client analyzer for troubleshooting performance issues, see [Run the client analyzer on macOS and Linux](overview-client-analyzer).

Note

The Microsoft Defender for Endpoint Client Analyzer tool is regularly used by Microsoft Customer Support Services (CSS) to collect information such as (but not limited to) IP addresses, PC names that help troubleshoot issues you might be experiencing with Microsoft Defender for Endpoint. For more information about our privacy statement, see [Microsoft Privacy Statement](https://privacy.microsoft.com/privacystatement).