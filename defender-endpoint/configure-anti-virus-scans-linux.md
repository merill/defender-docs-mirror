---
layout: Conceptual
title: Configure and run antivirus scans with Microsoft Defender for Endpoint on Linux - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/configure-anti-virus-scans-linux
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Describes how to set up and run antivirus scans using Microsoft Defender for Endpoint on Linux.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.reviewer: gopkr; meghapriya; lakshmyav
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-linux
ms.topic: how-to
ms.subservice: linux
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: b8271a35-7e8a-d39d-de85-0ffdf0d91e27
document_version_independent_id: b8271a35-7e8a-d39d-de85-0ffdf0d91e27
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/configure-anti-virus-scans-linux.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-anti-virus-scans-linux
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/configure-anti-virus-scans-linux.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 08dd8b41-0c5d-8a93-ee2c-7ef8251b528f
---

# Configure and run antivirus scans with Microsoft Defender for Endpoint on Linux - Microsoft Defender for Endpoint | Microsoft Learn

Microsoft Defender for Endpoint on Linux offers robust antivirus scanning capabilities to help identify and mitigate malicious files on your system. You can run these scans on-demand or schedule them at regular intervals, ensuring continuous protection and peace of mind. Three ways of running the scans are supported:

- Command line interface (CLI) (on-demand scans)
- crontab / anacron (scheduled scans)
- Through the Microsoft Defender portal (on-demand scans)

## Prerequisites

To launch a scan from the Defender portal, you must have at least **Alerts (manage)** permission. This permission requirement does not apply to manual scans triggered via the CLI.

## Supported scan types

With Defender for Endpoint on Linux, you can perform three types of on-demand scans on individual devices: *quick scan*, *full scan*, and *custom scan*.

These scans start right away, letting you specify parameters such as the location or type of scan. They also honor any configured [antivirus exclusions](linux-exclusions), ensuring that excluded files and folders aren't scanned.

The following table describes each type of scan:

| Scan type | Description |
| --- | --- |
| **Quick scan (recommended)** | A quick scan examines locations where malware is likely to be registered and executed, such as startup scripts, cron jobs, and system service directories (for example, `/etc/rc.local`, `/etc/init.d/`, and `systemd` service files). It also checks common directories where malware could reside, such as `/tmp`, `/var`, etc. The list of scanned locations is subject to change based on various factors such as threat landscape or evolving malware techniques. |
| **Full scan** | A full scan scans all files and folders within `/`.  A full scan with Defender for Endpoint on Linux can take several hours or even days to complete. The duration depends on the volume and type of data being scanned and the availability of CPU resources. |
| **Custom scan** | A custom scan runs on files and folders specified with the `--path` parameter.  By default, custom scans in Defender for Endpoint on Linux ignore files and folders specified in the antivirus exclusions. However, you can override this behavior by using the `--ignore-exclusions` flag, to ensure the excluded files and folders are scanned during a custom scan. |

Note

For optimal performance, we recommend using quick scans to secure your devices.

Based on the enforcement level configured, Defender for Endpoint takes remediation actions accordingly when a scan detects a malicious file. For more information, see [Enforcement level for Microsoft Defender Antivirus](linux-preferences#enforcement-level-for-microsoft-defender-antivirus).

If multiple scans are initiated, they get queued one after the other.

## Run on-demand scans via CLI

The following commands can be used to run quick, full, or custom scans:

| Description | Command |
| --- | --- |
| Run a quick scan | `mdatp scan quick` |
| Run a full scan | `mdatp scan full` |
| Run a custom scan on a path | `mdatp scan custom --path [path] [--ignore-exclusions]` |
| Cancel an ongoing on-demand scan | `mdatp scan cancel` |
| List the completed / canceled on-demand scans | `mdatp scan list` |

## Run scheduled scans via crontab/anacron

The following articles describe how to schedule antivirus scans using crontab or anacron:

- [Schedule an antivirus scan using crontab with Microsoft Defender for Endpoint on Linux](schedule-antivirus-scan-crontab)
- [Schedule an antivirus scan using Anacron with Microsoft Defender for Endpoint on Linux](schedule-antivirus-scan-anacron)

## Run on-demand scans via the Defender portal

Before you begin, ensure you have at least **Alerts (manage)** permission in the Defender portal.

To trigger an antivirus scan on a device from the Defender portal:

1. Go to the Microsoft Defender portal (https://security.microsoft.com) and sign-in.
2. Navigate to **Assets** &gt; **Devices**, and select the device you want to scan.
3. On the device's page, select More options (**...**), and then select **Run Antivirus Scan**.

    [![Screenshot showing where to access the run antivirus scan option.](media/schedule-anti-virus-scans-linux/run-anti-virus-scan.png)](media/schedule-anti-virus-scans-linux/run-anti-virus-scan.png#lightbox)
4. Under **Select scan type**, select either the **Quick Scan** or **Full Scan** radio button, add a comment, and then select **Confirm**.

    ![Screenshot how to choose type of antivirus scan to run.](media/schedule-anti-virus-scans-linux/choose-anti-virus-scan-type.png)

## Performance optimizations

Antivirus scans are crucial for security, but they can affect device performance. A full scan on a device with large or complex content uses more system resources and takes longer to finish.

You can adjust settings to balance performance and protection. To improve scan performance in Microsoft Defender for Endpoint on Linux, consider changing the following settings:

| Flag | Description |
| --- | --- |
| **Scan after definitions update** | Controls whether a process scan runs after new security updates download to the device. When enabled, it scans active processes. |
| **Scan archives (on-demand antivirus scans only)** | Controls whether to scan archive files (such as *.zip*, *.rar*, *.7z*) during on-demand scans. |
| **Maximum on-demand scan threads** | Sets how many threads run on-demand scans. More threads use more CPU but finish faster. |

For detailed instructions on configuring scan-after-definition-update, archive scanning, and maximum on-demand scan threads using CLI or managed JSON, see [Configure security settings in Microsoft Defender for Endpoint on Linux](linux-preferences#antivirus-engine-preferences).

## Best practices

Starting from version 101.23062.0001, Defender for Endpoint on Linux operates in passive mode by default, meaning real-time protection (RTP) is turned off. In passive mode, it's recommended to use scheduled scans as needed to ensure the system is periodically protected.

After installing Defender for Endpoint on Linux, it's a good practice to run a full scan (or a quick scan) to help identify and remediate any existing threats on the system.

Running a scan after installation is especially important before switching from passive mode to RTP mode, as enabling RTP primarily provides protection against newly introduced malware, and not the threats already present on the system. Running a scan beforehand helps ensure the device starts from a known clean state.

For continuous protection, incorporate quick scans into your regular scheduled scans. Quick scans offer comprehensive coverage for malware that starts with the system and kernel-level threats, all while maintaining minimal impact on your device's performance.