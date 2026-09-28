---
layout: Conceptual
title: Configure Microsoft Defender Antivirus with WMI - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/use-wmi-microsoft-defender-antivirus
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use WMI classes and scripts to retrieve, modify, and update local Microsoft Defender Antivirus settings. Learn where WMI fits alongside Group Policy, Configuration Manager, and Intune.
ms.service: defender-endpoint
ms.localizationpriority: medium
author: chrisda
ms.author: chrisda
ms.custom: nextgen, msecd-doc-authoring-1016
ms.date: 2026-07-02T00:00:00.0000000Z
ms.reviewer: pahuijbr
ms.subservice: ngp
ms.topic: how-to
ms.collection:
- m365-security
- tier3
- mde-ngp
ai-usage: ai-assisted
locale: en-us
document_id: 9fc68b65-5694-3d85-a7bd-eb84b1acabe9
document_version_independent_id: 9fc68b65-5694-3d85-a7bd-eb84b1acabe9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/use-wmi-microsoft-defender-antivirus.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: use-wmi-microsoft-defender-antivirus
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/use-wmi-microsoft-defender-antivirus.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 60a4e9e5-6925-6c81-3083-a1e92d657cb1
---

# Configure Microsoft Defender Antivirus with WMI - Microsoft Defender for Endpoint | Microsoft Learn

This article explains how to use Windows Management Instrumentation (WMI) classes and scripts to configure and manage Microsoft Defender Antivirus settings on local Windows endpoints.

WMI is a scripting interface that allows you to retrieve, modify, and update settings.

Read more about WMI at the [Microsoft Developer Network System Administration library](/en-us/windows/win32/wmisdk/wmi-start-page).

Microsoft Defender Antivirus has a number of specific WMI classes that can be used to perform most of the same functions as Group Policy and other management tools. Many of the classes are analogous to [Defender for Cloud PowerShell cmdlets](use-powershell-cmdlets-microsoft-defender-antivirus).

The [MSDN Windows Defender WMIv2 Provider reference library](/en-us/previous-versions/windows/desktop/defender/windows-defender-wmiv2-apis-portal) lists the available WMI classes for Microsoft Defender Antivirus, and includes example scripts.

Changes made with WMI affect only local settings on the endpoint where the changes are deployed or made. Because WMI changes affect only local settings, deployments of policy with Group Policy, Microsoft Configuration Manager, or Microsoft Intune can overwrite changes made with WMI.

You can [configure which settings can be overridden locally with local policy overrides](configure-local-policy-overrides-microsoft-defender-antivirus).

## Prerequisites

### Supported operating systems

The following operating systems are supported:

- Windows

Tip

If you're looking for Antivirus related information for other platforms, see:

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