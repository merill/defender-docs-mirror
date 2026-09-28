---
layout: Conceptual
title: Use PowerShell cmdlets to configure and run Microsoft Defender Antivirus - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/use-powershell-cmdlets-microsoft-defender-antivirus
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: In Windows 10 and Windows 11, you can use PowerShell cmdlets to run scans, update Security intelligence, and change settings in Microsoft Defender Antivirus.
ms.service: defender-endpoint
ms.localizationpriority: medium
author: chrisda
ms.author: chrisda
ms.custom: nextgen, msecd-doc-authoring-1016
ms.date: 2026-07-02T00:00:00.0000000Z
ms.reviewer: yongrhee
ms.subservice: ngp
ms.topic: how-to
ms.collection:
- m365-security
- tier2
- mde-ngp
ai-usage: ai-assisted
locale: en-us
document_id: 79e16831-ec05-a285-3b53-f30ce33963d3
document_version_independent_id: 79e16831-ec05-a285-3b53-f30ce33963d3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/use-powershell-cmdlets-microsoft-defender-antivirus.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: use-powershell-cmdlets-microsoft-defender-antivirus
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/use-powershell-cmdlets-microsoft-defender-antivirus.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: a1b63d53-f95f-39b2-8812-6d10ea09a742
---

# Use PowerShell cmdlets to configure and run Microsoft Defender Antivirus - Microsoft Defender for Endpoint | Microsoft Learn

You can use PowerShell to perform various functions in Microsoft Defender Antivirus. Similar to the command prompt or command line, PowerShell is a task-based command-line shell and scripting language designed especially for system administration. You can read more about it in the [PowerShell documentation](/en-us/powershell/scripting/overview).

For a list of the cmdlets and their functions and available parameters, see the [Microsoft Defender Antivirus cmdlets](/en-us/powershell/module/defender) topic.

PowerShell cmdlets are most useful in Windows Server environments that don't rely on a graphical user interface (GUI) to configure software.

Note

PowerShell cmdlets should not be used as a replacement for a full network policy management infrastructure, such as [Microsoft Configuration Manager](/en-us/intune/configmgr), [Group Policy Management Console](use-group-policy-microsoft-defender-antivirus), or [Microsoft Defender Antivirus Group Policy ADMX templates](/en-us/troubleshoot/windows-client/group-policy/create-and-manage-central-store).

Changes made with PowerShell will affect local settings on the endpoint where the changes are deployed or made. Because PowerShell changes only local settings on the endpoint, deployments of policy with Microsoft Defender for Endpoint security settings management, Microsoft Intune, Microsoft Configuration Manager Tenant Attach, or Group Policy can overwrite changes made with PowerShell.

You can [configure which settings can be overridden locally with local policy overrides](configure-local-policy-overrides-microsoft-defender-antivirus).

PowerShell is typically installed under the folder `%SystemRoot%\system32\WindowsPowerShell`.

## Prerequisites

### Supported operating systems

The following operating systems are supported:

- Windows

## Use Microsoft Defender Antivirus PowerShell cmdlets

Use the following steps to run Microsoft Defender Antivirus PowerShell cmdlets:

1. In the Windows search bar, type **powershell**.
2. Select **Windows PowerShell** from the results to open the interface.
3. Enter the PowerShell command and any parameters.

Note

You may need to open PowerShell in administrator mode. Right-click the item in the Start menu, click **Run as administrator** and click **Yes** at the permissions prompt.

To view the full online documentation for any Defender PowerShell cmdlet, including additional parameters and examples, use the following command:

```PowerShell
Get-Help <cmdlet> -Online
```

Omit the `-online` parameter to get locally cached help.

### Common Microsoft Defender Antivirus PowerShell cmdlets

Microsoft Defender Antivirus can be configured using PowerShell cmdlets. These are task-based commands for configuration and management. Common cmdlets include:

- [Get-MpComputerStatus](/en-us/powershell/module/defender/get-mpcomputerstatus): Check Microsoft Defender Antivirus status and protection settings.
- [Set-MpPreference](/en-us/powershell/module/defender/set-mppreference): Configure preferences, such as exclusions, scan schedules, and cloud-delivered protection.
- [Update-MpSignature](/en-us/powershell/module/defender/update-mpsignature): Update security intelligence.
- [Start-MpScan](/en-us/powershell/module/defender/start-mpscan): Trigger quick, full, or custom scans.
- [Get-MpThreat](/en-us/powershell/module/defender/get-mpthreat) or [Get-MpThreatDetection](/en-us/powershell/module/defender/get-mpthreatdetection): Review detected and remediated threats.

For full syntax and parameter options, see [Microsoft Defender Antivirus cmdlets](/en-us/powershell/module/defender).

Tip

- If you're looking for Antivirus related information for other platforms, see:

    - [Set preferences for Microsoft Defender for Endpoint on macOS](mac-preferences)
    - [Microsoft Defender for Endpoint on Mac](microsoft-defender-endpoint-mac)
    - [macOS Antivirus policy settings for Microsoft Defender Antivirus for Intune](/en-us/intune/intune-service/protect/antivirus-microsoft-defender-settings-macos)
    - [Set preferences for Microsoft Defender for Endpoint on Linux](linux-preferences)
    - [Microsoft Defender for Endpoint on Linux](microsoft-defender-endpoint-linux)
    - [Configure Defender for Endpoint on Android features](android-configure)
    - [Configure Microsoft Defender for Endpoint on iOS features](ios-configure-features)
- **Performance tip**: Due to a variety of factors, anti-virus software (including Microsoft Defender Antivirus) can cause performance issues on endpoint devices. In some cases, you might need to tune the performance of Microsoft Defender Antivirus to alleviate those performance issues. Microsoft's **Performance analyzer** is a PowerShell command-line tool that helps determine which files, file paths, processes, and file extensions might be causing performance issues. For example:

    - Top paths that impact scan time.
    - Top files that impact scan time.
    - Top processes that impact scan time.
    - Top file extensions that impact scan time.
    - Combinations. For example:
        - Top files per extension.
        - Top paths per extension.
        - Top processes per path.
        - Top scans per file.
        - Top scans per file per process.

    You can use this information to better assess performance issues and apply remediation actions. For more information, see [Performance analyzer for Microsoft Defender Antivirus](tune-performance-defender-antivirus).