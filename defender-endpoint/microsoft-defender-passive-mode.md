---
layout: Conceptual
title: Defender for Endpoint with Defender Antivirus in passive mode - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/microsoft-defender-passive-mode
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.topic: article
description: Understand how Defender Antivirus in passive mode works and when to use it.
ms.service: defender-endpoint
author: chrisda
ms.author: chrisda
ms.localizationpriority: high
ms.collection:
- m365-security
- tier1
- mde-ngp
ms.subservice: ngp
ms.date: 2025-03-26T00:00:00.0000000Z
locale: en-us
document_id: 28069ee4-0b3a-9939-99f0-69087fa97acb
document_version_independent_id: 28069ee4-0b3a-9939-99f0-69087fa97acb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/microsoft-defender-passive-mode.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: microsoft-defender-passive-mode
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/microsoft-defender-passive-mode.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 0b544d83-6645-a3d5-13ab-794757322f40
---

# Defender for Endpoint with Defender Antivirus in passive mode - Microsoft Defender for Endpoint | Microsoft Learn

Important

If you want to run multiple security solutions side by side, see [Considerations for performance, configuration, and support](/en-us/defender-endpoint/mde-side-by-side).

You might have already configured mutual security exclusions for devices onboarded to Microsoft Defender for Endpoint. If you still need to set mutual exclusions to avoid conflicts, see [Add Microsoft Defender for Endpoint to the exclusion list for your existing solution](/en-us/defender-endpoint/switch-to-mde-phase-2#step-2-add-microsoft-defender-for-endpoint-to-the-exclusion-list-for-your-existing-solution).

Microsoft Defender for Endpoint is a comprehensive security solution designed to protect your devices from evolving threats. One of its key features enables Microsoft Defender Antivirus to coexist with non-Microsoft antimalware solutions while still providing valuable endpoint detection and response capabilities.

Some of the key benefits of Defender Antivirus in passive mode are:

- **EDR Block mode** - Post-breach protection by detecting and remediating threats missed by the active antimalware solution
- **Security intelligence updates** - Microsoft Defender Antivirus continues to receive updates to stay aware of the latest threats.
- **Data Loss Prevention (DLP)** - Endpoint DLP functionalities operate normally, ensuring sensitive data is safeguarded.

For more information, see [How Microsoft Defender Antivirus affects Defender for Endpoint functionality](microsoft-defender-antivirus-compatibility#how-microsoft-defender-antivirus-affects-defender-for-endpoint-functionality).

Note

Passive mode disables Microsoft Defender Antivirus scheduled scans unless specific configurations are applied.

## Prerequisites

- Operating system

    - Windows 10 or newer
    - Windows Server 2012 R2 or newer
- The device must be onboarded to Microsoft Defender for Endpoint
- Microsoft Defender Antivirus has to be installed and enabled

## Configure passive mode

On Windows 10 or newer, Defender Antivirus automatically enters passive mode when a non-Microsoft antimalware solution is installed and registered.

For Windows Server operating systems, follow the instructions in this section to configure passive mode for Microsoft Defender for Endpoint.

### Set the registry key

To avoid conflicts between Microsoft Defender Antivirus and a third-party antivirus solution, if you're using Windows Server, set the following registry key before onboarding the device to Microsoft Defender for Endpoint:

- **Path** - HKLM\SOFTWARE\Policies\Microsoft\Windows Advanced Threat Protection
- **Name** - ForceDefenderPassiveMode
- **Type** - REG\_DWORD
- **Value** - 1

### Enable EDR in block mode

When Microsoft Defender Antivirus is in passive mode, EDR in block mode can provide post-breach protection by detecting and remediating threats. Ensure this feature is enabled in Defender for Endpoint.

### Avoid service modifications

Don't disable, stop, or modify associated services such as `wscsvc`, `WinDefend`, or `MsMpEng`. Stopping these services can cause instability and make your device vulnerable to threats.

### Exclude Defender binaries in third-party antivirus

To prevent performance issues or conflicts, add Microsoft Defender Antivirus and Defender for Endpoint binaries to the exclusion list of your third-party antivirus solution.

## Verify that passive mode is enabled

This section describes how to confirm whether Microsoft Defender Antivirus is in passive mode.

### Windows PowerShell

Run the following PowerShell cmdlet:

```powershell
Get-MpComputerStatus | select AMRunningMode
```

The `AMRunningMode` value indicates the current Defender Antivirus state:

- **Normal** - Active mode
- **Passive** - Passive mode
- **EDR Block Mode** - EDR is operating in block mode

### Windows security app

Follow these steps to verify that Microsoft Defender Antivirus is in passive mode (Windows 10 and later only).

1. Open the Windows Security app.
2. Select **Virus & threat protection**.
3. Under **Who’s protecting me?**, select **Manage providers**.
4. On the *Security providers* page, verify the antivirus provider and state.