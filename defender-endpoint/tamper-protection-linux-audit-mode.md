---
layout: Conceptual
title: Use tamper protection in audit mode for Microsoft Defender for Endpoint on Linux - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/tamper-protection-linux-audit-mode
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to verify, test, and investigate tamper protection in audit mode for Microsoft Defender for Endpoint on supported Linux devices.
ms.service: defender-endpoint
ms.author: monaberdugo
author: mberdugo
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-linux
ms.topic: how-to
ms.subservice: linux
ms.date: 2026-09-09T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: c6d07e33-3117-014e-23c5-ee0b78399ea0
document_version_independent_id: c6d07e33-3117-014e-23c5-ee0b78399ea0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/tamper-protection-linux-audit-mode.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: tamper-protection-linux-audit-mode
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/tamper-protection-linux-audit-mode.md
platformId: 91b05977-f465-5575-e72a-c18bb4bafacb
---

# Use tamper protection in audit mode for Microsoft Defender for Endpoint on Linux - Microsoft Defender for Endpoint | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

Tamper protection in audit mode for Microsoft Defender for Endpoint on Linux detects unauthorized modifications to Defender for Endpoint assets, including configuration files, directories, processes, and services. It detects changes made by any user, including the root user, and generates alerts without blocking the activity.

Use this article to review prerequisites, verify audit mode, investigate alerts, and test tamper detection. For an explanation of tamper protection and how its modes differ by operating system, see [Tamper protection overview](tamper-protection-overview).

On Linux devices, **Audit** mode detects and alerts on the following tampering activities:

- Modification of Defender for Endpoint configuration files.
- Deletion of Defender for Endpoint configuration files, state files, and binaries.
- Renaming or moving Defender for Endpoint configuration files, state files, and binaries.
- Termination of Defender for Endpoint processes, including restarting Defender for Endpoint services.

Audit mode provides visibility into tampering attempts through alerts and advanced hunting in the Microsoft Defender portal.

## Prerequisites

Before you use tamper protection in audit mode, make sure your device meets the following requirements:

- Defender for Endpoint version `101.26072.0004` (September 2026) or later from the Insiders-Slow ring.
- Allow access to `https://config.edge.skype.com/config/v1`. For more information, see [Microsoft Defender for Endpoint streamlined connectivity URLs - commercial](streamlined-device-connectivity-urls-commercial#urls-used-for-core-functionality).
- Tamper protection requires a Linux kernel that supports extended Berkeley Packet Filter (eBPF) with BPF Type Format (BTF). BTF provides the file and process context that Defender for Endpoint uses to detect tampering attempts. The following Linux distributions and kernel versions are supported:

    | Distribution | Supported version | Minimum kernel version |
    | --- | --- | --- |
    | Alma Linux 10 | 10.x | 6.12.0-55 |
    | Alma Linux 9 | 9.2+ | 5.14.0-284 |
    | Alma Linux 8 | 8.8+ | 4.18.0-477 |
    | Amazon Linux | 2023 | 6.1.132-147.221.amzn2023 |
    | Azure Linux 3 | 3 | 6.6.78.1-3.azl3 |
    | CentOS Stream | 10 | 6.12.0 |
    | CentOS Stream | 9 | 5.14.0 |
    | CentOS Stream | 8 | 4.18.0-553 |
    | Debian | 13 | 6.12 |
    | Debian | 12 | 6.1.0-9 |
    | Fedora | arm64: 40-43 | 6.8.5 |
    | Fedora | x86\_64: 33-43 | 5.8.15 |
    | Mariner 2 | 2 | 5.15 |
    | Oracle Linux 10 | 10.x (UEK8) | 6.12.0 |
    | Oracle Linux 10 | 10.x (RHCK) | 6.12.0-55 |
    | Oracle Linux 9 | 9.x (UEK8) | 6.12.0 |
    | Oracle Linux 9 | 9.x (UEK7) | 5.15.0 |
    | Oracle Linux 9 | 9.x (RHCK) | 5.14.0-70 |
    | Oracle Linux 8 | 8.10 (UEK7) | 5.15.0 |
    | Oracle Linux 8 | 8.10 (RHCK) | 4.18.0-553 |
    | RHEL 10 | 10.x | 6.12.0-55 |
    | RHEL 9 | 9.x | 5.14.0-70 |
    | RHEL 8 | 8.4+ | 4.18.0-305 |
    | Rocky Linux 10 | 10.x | 6.12.0-55 |
    | Rocky Linux 9 | 9.3+ | 5.14.0-362 |
    | Rocky Linux 8 | 8.9+ | 4.18.0-513 |
    | SLES 16 | 16 | 6.12.0-160000 |
    | SLES 15 | 15.5+ | 5.14.21-150500 |
    | Ubuntu LTS | 24.04 | 6.8.0 |
    | Ubuntu LTS | 22.04 | 5.15.0^\*^ |
    | Ubuntu LTS | 20.04 | 5.15.0^\*^ |
    | Ubuntu Pro | 24.04 | 6.8.0 |
    | Ubuntu Pro | 22.04 | 5.15.0^\*^ |

    Important

    ^\*^ For Ubuntu 20.04 and Ubuntu 22.04, the following generic kernel versions aren't supported: `5.15.0-144`, `5.15.0-150`, `5.15.0-151`, and `5.15.0-152`.

## Enable tamper protection in audit mode

During Preview, tamper protection in audit mode is enabled by default. No configuration is required.

The feature rolls out gradually over two weeks to eligible devices in the Insiders-Slow ring that meet the prerequisites.

## Verify audit mode enablement

Run the following command to check the tamper protection status and errors:

```bash
mdatp health --details tamper_protection
```

The following output shows that tamper protection is enabled in audit mode without errors:

```console
tamper_protection_enforcement_level : "audit"
tamper_protection_errors            : []
```

If tamper protection can't be enabled, `tamper_protection_enforcement_level` shows `disabled`. For error descriptions and resolution steps, see [Troubleshoot problems with tamper protection](tamper-protection-troubleshoot).

## View tampering alerts in the Microsoft Defender portal

On the **Device inventory** page in the Microsoft Defender portal at https://security.microsoft.com/machines, select the affected Linux device. Then, review **Timeline** and **Incidents and alerts** for tampering activity and alerts.

Open a tampering alert to review the affected assets, process tree, alert timeline, and related activity. For more information, see [Investigate alerts in Microsoft Defender for Endpoint](investigate-alerts).

## Query tampering attempts with advanced hunting

To get the device ID directly from a Linux device, run the following command:

```bash
mdatp health --field edr_device_id
```

Use the device ID to filter the cross-platform queries in [Query tampering attempts with advanced hunting](tamper-protection-overview#query-tampering-attempts-with-advanced-hunting).

## Test a tampering scenario

To generate a test tampering attempt, open the Defender for Endpoint configuration file in `vim`:

```bash
sudo vim /etc/opt/microsoft/mdatp/managed/mdatp_managed.json
```

Modify and save the file. The attempt generates a tampering alert in the Microsoft Defender portal. The alert includes information about the initiating process and target file.

To reduce alert noise from known and approved activity, see [Tune alerts for legitimate tampering activity](tamper-protection-overview#tune-alerts-for-legitimate-tampering-activity).