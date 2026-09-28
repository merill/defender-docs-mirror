---
layout: Conceptual
title: Troubleshoot Microsoft Defender Antivirus settings - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-settings
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Find out where settings for Microsoft Defender Antivirus are coming from.
author: chrisda
ms.author: chrisda
ms.reviewer: yongrhee
ms.service: defender-endpoint
ms.topic: troubleshooting-general
ms.date: 2026-07-17T00:00:00.0000000Z
ms.subservice: ngp
ms.localizationpriority: medium
ms.collection: 
ms.custom: partner-contribution
locale: en-us
document_id: 33f27b48-f667-c302-5fb8-4eaeb4e6a01b
document_version_independent_id: 33f27b48-f667-c302-5fb8-4eaeb4e6a01b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/troubleshoot-settings.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: troubleshoot-settings
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/troubleshoot-settings.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/4c50f262-d533-4ba4-9d4a-08899ec3a3d1
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/6a8c83be-f1de-4e90-bde0-bd097999a60c
platformId: 4ffcf2d3-867b-d301-6ea9-630a942f2f8b
---

# Troubleshoot Microsoft Defender Antivirus settings - Microsoft Defender for Endpoint | Microsoft Learn

Microsoft Defender Antivirus provides numerous ways to manage the product, which provides small and medium-sized businesses and enterprise organizations with flexibility by working with the management tools that they already have.

- Microsoft Defender for Endpoint security settings management
- Microsoft Intune (MDM)
- Microsoft Configuration Manager with Tenant Attaches
- Microsoft Configuration Manager co-management
- Microsoft Configuration Manager (standalone)
- Group Policy (GPO)
- PowerShell
- Windows Management Instrumentation (WMI)
- Registry

Tip

For best results, use one method of managing Microsoft Defender Antivirus.

## Troubleshooting Microsoft Defender Antivirus settings

Suppose that migrating from a non-Microsoft antivirus product, and when you try enabling Microsoft Defender Antivirus, it won't start. Most likely, you're experiencing a policy conflict.

To remove policy conflicts, here's our current, recommended process:

1. Understand the order of precedence.
2. Determine where Microsoft Defender Antivirus settings are configured.
3. Identify policies and settings.
4. Work with your security team to remove or revise conflicting policies.

Tip

In versions of the Microsoft Defender antimalware platform before 4.18.2108.4 (September 2021), the dword registry key `DisableAntispyware` with the value 1 at `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Defender` could also prevent Microsoft Defender Antivirus from starting.

## Step 1: Understand the order of precedence

Note

Microsoft Defender for Endpoint attach configurations can be overridden by other configuration tools that write to the same registry location.

Starting in February 2026, Microsoft Defender Antivirus on Windows is changing how antivirus settings (like exclusions) are stored when Microsoft Defender for Endpoint configuration management is enabled in an organization. Starting with the 4.18.25110.6 release, organizations using Microsoft Defender for Endpoint configuration management can no longer read exclusion values directly from the local device registry. Instead, setting configuration must be retrieved using supported Microsoft Defender PowerShell cmdlets. Organizations using Defender for Endpoint configuration management must use supported Defender PowerShell cmdlets (such as Get-MpPreference).

When policies and settings are configured in multiple tools, in general, here's the order of precedence:

1. Microsoft Defender for Endpoint security settings management
2. Group Policy (GPO)
3. Microsoft Configuration Manager co-management
4. Microsoft Configuration Manager (standalone)
5. Microsoft Intune (MDM)
6. Microsoft Configuration Manager with Tenant Attaches
7. PowerShell ([Set-MpPreference](/en-us/powershell/module/defender/set-mppreference)), [MpCmdRun command-line tool](command-line-arguments-microsoft-defender-antivirus), or [Windows Management Instrumentation](use-wmi-microsoft-defender-antivirus) (WMI).

Warning

[MDMWinsOverGP](/en-us/windows/client-management/mdm/policy-csp-controlpolicyconflict) is a Policy CSP setting that doesn't apply for all settings, such as [attack surface reduction (ASR) rules](attack-surface-reduction-rules-overview) in Windows 10.

## Step 2: Determine where Microsoft Defender Antivirus settings are configured

Find out whether Microsoft Defender Antivirus settings are coming through a policy, MDM, or a local setting. The following table describes policies, settings, and relevant tools.

| Policy or setting | Registry location | Tools |
| --- | --- | --- |
| Policy | `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Defender` | - Microsoft Defender for Endpoint security settings management<br>- Microsoft Configuration Manager co-management<br>- Microsoft Configuration Manager<br>- GPO |
| MDM | `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Defender\Policy Manager` | - Microsoft Intune (MDM)<br>- Microsoft Configuration Manager with Tenant Attaches |
| Local setting | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Defender` | - PowerShell (Set-MpPreference)<br>- MpCmdRun command-line tool<br>- Windows Management Instrumentation (WMI) |

Tip

To see the actual value of each security setting on a device and the source that configured it, use the **Effective settings** tab on the device page. For more information, see [Configuration management - Effective settings](investigate-machines#configuration-management---effective-settings).

## Step 3: Identify policies or settings

The following table describes how to identify policies and settings.

| Method used | What to check |
| --- | --- |
| Policy | - **If you're using GPO**: Run the following command in an elevated Command Prompt (a Command Prompt window you opened by selecting **Run as administrator**): `GpResult.exe /h C:\temp\GpResult_output.html`.<br>- If you're using Microsoft Configuration Manager co-management or Microsoft Configuration Manager (standalone), go to `C:\Windows\CCM\Logs`. |
| MDM | If you're using Intune, on your device, select **Start**, open Command Prompt as an administrator, and then run the command `mdmdiagnosticstool.exe -out "c:\temp\MDMDiagReport.zip"`. For more information, see [Collect MDM logs - Windows Client Management](/en-us/windows/client-management/mdm-collect-logs). |
| Local setting | Determine whether the policy or setting was deployed during the imaging (sysprep), via PowerShell (for example, Set-MpPreference), Windows Management Instrumentation (WMI), or through a direct modification to the registry. |

## Step 4: Remove or revise conflicting policies

Once you have identified the conflicting policy, work with your security administrators to change device targeting so that devices receive the correct Microsoft Defender Antivirus settings.