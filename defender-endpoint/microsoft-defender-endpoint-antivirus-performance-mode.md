---
layout: Conceptual
title: Protect Dev Drive using performance mode - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/microsoft-defender-endpoint-antivirus-performance-mode
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to configure and manage Microsoft Defender Antivirus performance mode to help protect Dev Drive for developer workloads.
ms.service: defender-endpoint
ms.localizationpriority: high
ms.topic: how-to
author: chrisda
ms.author: chrisda
ms.reviewer: pricci, yongrhee
ms.custom: nextgen02, msecd-doc-authoring-1016
ms.subservice: ngp
ms.collection:
- m365-security
- tier2
ms.date: 2026-09-15T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: cbe3e5dd-a51a-2387-e34f-29b653e91b67
document_version_independent_id: cbe3e5dd-a51a-2387-e34f-29b653e91b67
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/microsoft-defender-endpoint-antivirus-performance-mode.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: microsoft-defender-endpoint-antivirus-performance-mode
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/microsoft-defender-endpoint-antivirus-performance-mode.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/19ec6774-09b8-473e-a17e-b17b518bbad7
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ade36b61-c646-4bd8-87ee-f3a843461962
platformId: 13e66122-441c-3810-30cf-b7776fb54160
---

# Protect Dev Drive using performance mode - Microsoft Defender for Endpoint | Microsoft Learn

## Overview

Note

Want to experience Microsoft Defender XDR? Learn more about how you can [Pilot and deploy Microsoft Defender XDR](/en-us/defender-xdr/pilot-deploy-overview).

Tip

As a companion to this article, see our [Microsoft Defender for Endpoint setup guide](https://go.microsoft.com/fwlink/p/?linkid=2268087) to review best practices and learn about essential tools such as attack surface reduction and next-generation protection. For a customized experience based on your environment, you can access the Defender for [Endpoint automated setup guide](https://go.microsoft.com/fwlink/p/?linkid=2268088) in the Microsoft 365 admin center.

## What is performance mode?

Performance mode is now available on Windows 11 as a new Microsoft Defender Antivirus capability. Performance mode reduces the performance impact of Microsoft Defender Antivirus scans for files stored on designated Dev Drive. The goal of performance mode is to improve functional performance for developers who use Windows 11 devices.

It's important to note that performance mode can run only on Dev Drive. Additionally, real-time protection must be turned on for performance mode to function. Enabling performance mode on a Dev Drive doesn't change standard real-time protection running on volumes with operating systems or other volumes formatted as `FAT32` or `NTFS`.

## Prerequisites

### Supported operating systems

Performance mode is supported on the following operating systems:

- Windows 11

### Microsoft Defender Antivirus requirements for performance mode

Ensure the following Microsoft Defender Antivirus requirements are met before you enable performance mode:

1. Review the requirements that are specific to Dev Drive. See [Set up a Dev Drive on Windows 11](/en-us/windows/dev-drive).
2. Make sure Microsoft Defender Antivirus is up to date:

    - Microsoft Defender Antivirus needs to be the primary antivirus/antimalware solution
    - Real-time protection is turned on
    - Antimalware platform version: `4.18.2303.8` (or later)
    - Antimalware security intelligence version: `1.385.1455.0` (or later)

### Dev Drive

Dev Drive is a new form of storage volume available to improve performance for key developer workloads. It builds on ReFS technology to employ targeted file-system optimizations and provide more control over storage volume settings and security, including trust designation, antivirus configuration, and administrative control over which filters are attached.

For more information about Dev Drive, see: [Set up a Dev Drive on Windows 11](/en-us/windows/dev-drive).

### Performance mode compared to real-time protection

To give the best possible performance, creating a Dev Drive automatically grants trust in the new volume by default. A trusted Dev Drive volume causes real-time protection to run in a special asynchronous performance mode for that volume. Running performance mode provides a balance between threat protection and performance. The balance between threat protection and performance is achieved by deferring security scans until after the open file operation has completed, instead of performing the security scan synchronously while the file operation is being processed. Deferring scans until after file open completes inherently provides faster performance, but with less protection. However, enabling performance mode provides significantly better protection than other performance tuning methods, such as using folder exclusions, which block security scans altogether.

Note

Using performance mode doesn't apply to high cpu or high memory usage scenarios with Microsoft Defender Antivirus services (`MsMpEng.exe`, `WinDefend`, or Antimalware Service Executable). If you're troubleshooting a high cpu usage, instead use the Microsoft Defender Antivirus [Performance Analyzer](tune-performance-defender-antivirus) to narrow down to the hot processes/paths and add them to the exclusions.

Tip

Use [Contextual exclusions](microsoft-defender-antivirus-exclusions-overview#contextual-exclusions) to target real-time protection (RTP). The following table summarizes performance mode synchronous and asynchronous scan behavior.

| Performance mode state | Scan type | Description | Summary |
| --- | --- | --- | --- |
| Not enabled (Off) | **Synchronous** (Real-time protection) | Opening a file initiates a real-time protection scan. | Open now, scan now. |
| Enabled (On) | **Asynchronous** | File open operations are scanned asynchronously. | Open now, scan later. |

An untrusted Dev Drive doesn't have the same benefits as a trusted Dev Drive. Security runs in synchronous, real-time protection mode when a Dev Drive is untrusted. Real-time protection scans can affect performance.

## Manage performance mode

Use one of the following methods to manage performance mode:

> 
> Microsoft Intune is the recommended tool for configuring and distributing Defender for Endpoint features to devices. However, Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have Intune, you can use any of the other methods in this article. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

- Performance mode can only run on a *trusted* Dev Drive and is enabled by default when a new Dev Drive is created. For more information about security risks and trust for Dev Drive, see [Understanding security risks and trust in relation to Dev Drive](/en-us/windows/dev-drive#understanding-security-risks-and-trust-in-relation-to-dev-drive).
- Enforce the Microsoft Defender Antivirus Performance Mode by using Intune, Group Policy, or PowerShell.

### Manage performance mode with Intune

Enable performance mode status via the OMA-URI settings shown in the following table.

| Setting | Value |
| --- | --- |
| OMA-URI: | `./Device/Vendor/MSFT/Defender/Configuration/PerformanceModeStatus` |
| Data type | Integer |
| Value | 0 |

`0` = `Enable` (default) `1` = `Disable`

### Manage performance mode with Group Policy

Note

The updated Group Policy Template **Configure performance mode status**, located under **Real-Time Protection** is only available after you install the [Administrative Templates for Windows 11 2024 Update (24H2)](https://www.microsoft.com/download/details.aspx?id=106254).

1. Using your Group Policy Management Console or Group Policy Editor, go to **Computer Configuration** &gt; **Administrative Templates** &gt; **Windows Components** &gt; **Microsoft Defender Antivirus** &gt; **Real-time Protection**.
2. Double-click **Configure performance mode status**.

    [![Screenshot of Defender Performance Mode 10.](media/microsoft-defender-endpoint-antivirus-performance-mode/defender-performance-mode-10.png)](media/microsoft-defender-endpoint-antivirus-performance-mode/defender-performance-mode-10.png#lightbox)
3. Select **Enabled**.

    ![Screenshot of Defender Performance Mode 11.](media/microsoft-defender-endpoint-antivirus-performance-mode/defender-performance-mode-11.png)
4. Select **Apply**, then select **OK**.

### Manage performance mode with PowerShell

Use PowerShell to enable performance mode on the device:

1. Open PowerShell as an administrator on the device.
2. Type `set-MpPreference -PerformanceModeStatus Enabled` and press **Enter**.

    ![Screenshot of Defender Performance Mode 04.](media/microsoft-defender-endpoint-antivirus-performance-mode/defender-performance-mode-5.png)

## Verify performance mode is enabled

To verify that Dev Drive and Defender Performance Mode is enabled, follow these steps:

1. In the Windows Security App, go to **Virus & threat Protection settings** &gt; **Manage settings** and verify that Dev Drive protection is enabled.

    [![Screenshot of Defender Performance Mode 02.](media/microsoft-defender-endpoint-antivirus-performance-mode/defender-performance-mode-02.png)](media/microsoft-defender-endpoint-antivirus-performance-mode/defender-performance-mode-02.png#lightbox)
2. Select **See volumes**.

    [![Screenshot of Defender Performance Mode 03.](media/microsoft-defender-endpoint-antivirus-performance-mode/defender-performance-mode-03.png)](media/microsoft-defender-endpoint-antivirus-performance-mode/defender-performance-mode-03.png#lightbox)

    | Drive | Status |
    | --- | --- |
    | `C:` | Since the system drive (for example, C: or D:) drive is formatted with NTFS, it's not eligible for Defender Performance mode. |
    | `D:` | Dev Drive is enabled but Defender Performance mode isn't enabled. |
    | `F:` | Dev Drive is enabled, and Defender Performance mode is enabled. |