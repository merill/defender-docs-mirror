---
layout: Conceptual
title: Manage Microsoft Defender Antivirus in your business - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/configuration-management-reference-microsoft-defender-antivirus
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use Group Policy, Configuration Manager, PowerShell, WMI, Intune, and the command line to manage Microsoft Defender Antivirus
ms.service: defender-endpoint
ms.localizationpriority: medium
author: chrisda
ms.author: chrisda
ms.custom: nextgen
ms.date: 2025-10-20T00:00:00.0000000Z
ms.reviewer: yongrhee
ms.subservice: ngp
ms.topic: article
ms.collection:
- m365-security
- tier2
- mde-ngp
locale: en-us
document_id: ae69955d-929b-6857-b152-9ede0d36c0b5
document_version_independent_id: ae69955d-929b-6857-b152-9ede0d36c0b5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/configuration-management-reference-microsoft-defender-antivirus.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configuration-management-reference-microsoft-defender-antivirus
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/configuration-management-reference-microsoft-defender-antivirus.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 5efe7f50-92fb-9382-8328-87fecccd13d7
---

# Manage Microsoft Defender Antivirus in your business - Microsoft Defender for Endpoint | Microsoft Learn

Tip

For the best experience, please choose 1 method for configuring the Microsoft Defender Antivirus policies.

Important

Group Policy (GPO) wins over Microsoft Configuration Manager wins over Microsoft Intune wins over Microsoft Defender for Endpoint Security Configuration Management, Powershell, WMI, or MpCmdRun. You can manage and configure Microsoft Defender Antivirus with the following tools:

- [Microsoft Defender for Endpoint Security Configuration Management](/en-us/intune/intune-service/protect/mde-security-integration)
- [Microsoft Intune](/en-us/intune/intune-service/protect/endpoint-security-antivirus-policy)
- [Microsoft Configuration Manager](/en-us/intune/configmgr/protect/deploy-use/endpoint-protection-configure)
- [Group Policy](use-group-policy-microsoft-defender-antivirus)
- [PowerShell cmdlets](use-powershell-cmdlets-microsoft-defender-antivirus)
- [Windows Management Instrumentation (WMI)](use-wmi-microsoft-defender-antivirus)
- The [Microsoft Malware Protection Command Line Utility](command-line-arguments-microsoft-defender-antivirus) (MpCmdRun.exe)

## Prerequisites

### Supported operating systems

- Windows
- Windows Server

The following articles provide further information, links, and resources for using these tools to manage and configure Microsoft Defender Antivirus.

| Article | Description |
| --- | --- |
| [Manage Microsoft Defender Antivirus with Microsoft Defender for Endpoint Security Configuration Management](/en-us/intune/intune-service/protect/mde-security-integration) | Information about using the Microsoft Defender for Endpoint Security Configuration Management to configure, manage, and report, Microsoft Defender Antivirus |
| [Manage Microsoft Defender Antivirus with Microsoft Intune and Microsoft Configuration Manager](use-intune-config-manager-microsoft-defender-antivirus) | Information about using Intune and Configuration Manager to deploy, manage, report, and configure Microsoft Defender Antivirus |
| [Manage Microsoft Defender Antivirus with Group Policy settings](use-group-policy-microsoft-defender-antivirus) | List of all Group Policy settings located in ADMX templates |
| [Manage Microsoft Defender Antivirus with PowerShell cmdlets](use-powershell-cmdlets-microsoft-defender-antivirus) | Instructions for using PowerShell cmdlets to manage Microsoft Defender Antivirus, plus links to documentation for all cmdlets and allowed parameters |
| [Manage Microsoft Defender Antivirus with Windows Management Instrumentation (WMI)](use-wmi-microsoft-defender-antivirus) | Instructions for using WMI to manage Microsoft Defender Antivirus, plus links to documentation for the WMIv2 APIs (including all classes, methods, and properties) |
| [Configure and manage Microsoft Defender Antivirus with the MpCmdRun command-line tool](command-line-arguments-microsoft-defender-antivirus) | Instructions on using the dedicated command-line tool to manage and use Microsoft Defender Antivirus |

If you experience high CPU utilization in Antimalware Service Executable | Microsoft Defender Antivirus Service | MsMpEng.exe, see [Performance analyzer for Microsoft Defender Antivirus](tune-performance-defender-antivirus)

Tip

If you're looking for Antivirus related information for other platforms, see the following articles:

- [Set preferences for Microsoft Defender for Endpoint on macOS](mac-preferences)
- [Microsoft Defender for Endpoint on Mac](microsoft-defender-endpoint-mac)
- [macOS Antivirus policy settings for Microsoft Defender Antivirus for Intune](/en-us/intune/intune-service/protect/antivirus-microsoft-defender-settings-macos)
- [Set preferences for Microsoft Defender for Endpoint on Linux](linux-preferences)
- [Microsoft Defender for Endpoint on Linux](microsoft-defender-endpoint-linux)
- [Configure Defender for Endpoint on Android features](android-configure)
- [Configure Microsoft Defender for Endpoint on iOS features](ios-configure-features)