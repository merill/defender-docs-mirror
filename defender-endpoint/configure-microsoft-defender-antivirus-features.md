---
layout: Conceptual
title: Configure Microsoft Defender Antivirus features - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/configure-microsoft-defender-antivirus-features
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: You can configure Microsoft Defender Antivirus features with Intune, Microsoft Configuration Manager, Group Policy, and PowerShell.
ms.service: defender-endpoint
ms.subservice: ngp
ms.localizationpriority: medium
author: chrisda
ms.author: chrisda
ms.topic: install-set-up-deploy
ms.custom: nextgen
ms.reviewer: yongrhee
ms.collection:
- m365-security
- tier2
- mde-ngp
ms.date: 2025-10-20T00:00:00.0000000Z
locale: en-us
document_id: f6105904-7273-0c6f-0e04-afc5a58a1ff3
document_version_independent_id: f6105904-7273-0c6f-0e04-afc5a58a1ff3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/configure-microsoft-defender-antivirus-features.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-microsoft-defender-antivirus-features
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/configure-microsoft-defender-antivirus-features.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: ba355666-62d5-c03c-1e40-34edf969f8c2
---

# Configure Microsoft Defender Antivirus features - Microsoft Defender for Endpoint | Microsoft Learn

## Prerequisites

### Supported operating systems

- Windows

You can configure Microsoft Defender Antivirus with a number of tools, such as:

- [Microsoft Defender for Endpoint Security Policy Management](/en-us/intune/intune-service/protect/mde-security-integration)
- [Microsoft Intune](use-intune-config-manager-microsoft-defender-antivirus)
- [Microsoft Configuration Manager](preferences-setup)
- Microsoft Configuration Manager [Tenant attach](/en-us/intune/configmgr/tenant-attach/)
- [Group Policy](use-group-policy-microsoft-defender-antivirus)
- [PowerShell cmdlets](use-powershell-cmdlets-microsoft-defender-antivirus)
- [Windows Management Instrumentation (WMI)](use-wmi-microsoft-defender-antivirus)

The following broad categories of features can be configured:

- Cloud-delivered protection. See [Cloud-delivered protection and Microsoft Defender Antivirus](cloud-protection-microsoft-defender-antivirus)
- Always-on real-time protection, including behavioral, heuristic, and machine learning-based protection. See [Configure behavioral, heuristic, and real-time protection](configure-protection-features-microsoft-defender-antivirus).
- How end users interact with the client on individual endpoints. See the following resources:

    - [Prevent users from seeing or interacting with the Microsoft Defender Antivirus user interface](prevent-end-user-interaction-microsoft-defender-antivirus)
    - [Prevent or allow users to locally modify Microsoft Defender Antivirus policy settings](configure-local-policy-overrides-microsoft-defender-antivirus)

Tip

Review [Reference topics for management and configuration tools](configuration-management-reference-microsoft-defender-antivirus). If you're looking for Antivirus related information for other platforms, see:

- [Set preferences for Microsoft Defender for Endpoint on macOS](mac-preferences)
- [Microsoft Defender for Endpoint on Mac](microsoft-defender-endpoint-mac)
- [macOS Antivirus policy settings for Microsoft Defender Antivirus for Intune](/en-us/intune/intune-service/protect/antivirus-microsoft-defender-settings-macos)
- [Set preferences for Microsoft Defender for Endpoint on Linux](linux-preferences)
- [Microsoft Defender for Endpoint on Linux](microsoft-defender-endpoint-linux)
- [Configure Defender for Endpoint on Android features](android-configure)
- [Configure Microsoft Defender for Endpoint on iOS features](ios-configure-features)

Tip

**Performance tip** Due to a variety of factors (examples listed below) Microsoft Defender Antivirus, like other antivirus software, can cause performance issues on endpoint devices. In some cases, you might need to tune the performance of Microsoft Defender Antivirus to alleviate those performance issues. Microsoft's **Performance analyzer** is a PowerShell command-line tool that helps determine which files, file paths, processes, and file extensions might be causing performance issues; some examples are:

- Top paths that impact scan time
- Top files that impact scan time
- Top processes that impact scan time
- Top file extensions that impact scan time
- Combinations – for example:
    - top files per extension
    - top paths per extension
    - top processes per path
    - top scans per file
    - top scans per file per process

You can use the information gathered using Performance analyzer to better assess performance issues and apply remediation actions. See: [Performance analyzer for Microsoft Defender Antivirus](tune-performance-defender-antivirus).