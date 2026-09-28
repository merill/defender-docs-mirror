---
layout: Conceptual
title: Troubleshooting issues when moving to Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/switch-to-mde-troubleshooting
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to troubleshoot issues when you migrate to Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365solution-scenario
- m365-security
- highpri
- tier1
ms.topic: troubleshooting-general
ms.custom: migrationguides
ms.date: 2025-02-12T00:00:00.0000000Z
ms.reviewer: jesquive, chventou, jonix, chriggs, owtho
ms.subservice: onboard
locale: en-us
document_id: ef008354-3220-4672-95d5-8162533f4528
document_version_independent_id: ef008354-3220-4672-95d5-8162533f4528
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/switch-to-mde-troubleshooting.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: switch-to-mde-troubleshooting
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/switch-to-mde-troubleshooting.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/00675be6-8413-445a-927c-01fdfb06925d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/fc3f72c2-fb6f-4cea-95ee-b444e52254ee
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/3f4c9937-0bf4-403a-90e9-153dbfe1b4c3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/f12cf087-582d-48ac-a085-0c19adf1e391
platformId: 659d184c-9f05-4a9b-b00a-ea0a9f04b495
---

# Troubleshooting issues when moving to Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

This article provides troubleshooting information for security administrators who are experiencing issues when moving from a non-Microsoft endpoint protection solution to Microsoft Defender for Endpoint.

## Microsoft Defender Antivirus is getting uninstalled on Windows Server

When you migrate to Defender for Endpoint, you begin with your non-Microsoft antivirus/antimalware protection in active mode. As part of the setup process, you configure Microsoft Defender Antivirus in passive mode. Occasionally, your non-Microsoft antivirus/antimalware solution might prevent Microsoft Defender Antivirus from running on Windows Server. In fact, it can look like Microsoft Defender Antivirus has been removed from Windows Server.

To resolve this issue, take the following steps:

1. Add Microsoft Defender for Endpoint to the exclusion list.
2. Set Microsoft Defender Antivirus to passive mode manually.

### Add Microsoft Defender for Endpoint to the exclusion list

| OS | Exclusions |
| --- | --- |
| [Windows 11](/en-us/windows/whats-new/windows-11-overview)Windows 10, [version 1803](/en-us/lifecycle/announcements/windows-server-1803-end-of-servicing) or later (See [Windows 10 release information](/en-us/windows/release-health/release-information))Windows 10, version 1703 or 1709 with [KB4493441](https://support.microsoft.com/servicing/os/windows-10/2019/04/april-9-2019-kb4493441-os-build-16299-1087) installed | `C:\Program Files\Windows Defender Advanced Threat Protection\MsSense.exe``C:\Program Files\Windows Defender Advanced Threat Protection\SenseCncProxy.exe``C:\Program Files\Windows Defender Advanced Threat Protection\SenseSampleUploader.exe``C:\Program Files\Windows Defender Advanced Threat Protection\SenseIR.exe``C:\Program Files\Windows Defender Advanced Threat Protection\SenseCM.exe``C:\Program Files\Windows Defender Advanced Threat Protection\SenseNdr.exe``C:\Program Files\Windows Defender Advanced Threat Protection\Classification\SenseCE.exe``C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\DataCollection` |
| Windows Server 2025 [Windows Server 2022](/en-us/windows/release-health/status-windows-server-2022)[Windows Server 2019](/en-us/windows/release-health/status-windows-10-1809-and-windows-server-2019)[Windows Server 2016](/en-us/windows/release-health/status-windows-10-1607-and-windows-server-2016)[Windows Server 2012 R2](/en-us/windows/release-health/status-windows-8.1-and-windows-server-2012-r2)[Windows Server, version 1803](/en-us/windows-server/get-started/whats-new-in-windows-server-1803) Azure Stack HCI OS, version 23H2 and later | On Windows Server 2012 R2 and Windows Server 2016 running the [modern unified solution](onboard-server#functionality-in-the-modern-unified-solution-for-windows-server-2016-and-windows-server-2012-r2), the following exclusions are required after updating the Sense EDR component using [KB5005292](https://support.microsoft.com/servicing/Management-Tools/microsoft-defender/update/microsoft-defender-for-endpoint-update-for-edr-sensor):`C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Platform\*\MsSense.exe``C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Platform\*\SenseCnCProxy.exe``C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Platform\*\SenseIR.exe``C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Platform\*\SenseCE.exe``C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Platform\*\SenseSampleUploader.exe``C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Platform\*\SenseCM.exe``C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\DataCollection` |
| [Windows 8.1](/en-us/windows/release-health/status-windows-8.1-and-windows-server-2012-r2)[Windows 7](/en-us/windows/release-health/status-windows-7-and-windows-server-2008-r2-sp1)[Windows Server 2008 R2 SP1](/en-us/windows/release-health/status-windows-7-and-windows-server-2008-r2-sp1) | `C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Monitoring Host Temporary Files 6\45\MsSenseS.exe`**NOTE**: Monitoring Host Temporary Files 6\45 can be different numbered subfolders.`C:\Program Files\Microsoft Monitoring Agent\Agent\AgentControlPanel.exe``C:\Program Files\Microsoft Monitoring Agent\Agent\HealthService.exe``C:\Program Files\Microsoft Monitoring Agent\Agent\HSLockdown.exe``C:\Program Files\Microsoft Monitoring Agent\Agent\MOMPerfSnapshotHelper.exe``C:\Program Files\Microsoft Monitoring Agent\Agent\MonitoringHost.exe``C:\Program Files\Microsoft Monitoring Agent\Agent\TestCloudConnection.exe` |

Important

As a best practice, keep your organization's devices and endpoints up to date. Make sure to get the [latest updates for Microsoft Defender for Endpoint and Microsoft Defender Antivirus](microsoft-defender-antivirus-updates), and keep your organization's operating systems and productivity apps up to date.

### Set Microsoft Defender Antivirus to passive mode manually

Tip

If you're planning to keep Microsoft Defender Antivirus in passive mode for your Windows Servers, the `ForceDefenderPassiveMode` setting needs to be set **before** onboarding the device to Microsoft Defender for Endpoint.

## Prerequisites

You must set Microsoft Defender Antivirus to passive mode manually on Windows Server 2012 R2 and later, Windows Server, version 1803 and later, or Azure Stack HCI OS, version 23H2 and later. This action helps prevent problems caused by having multiple antivirus products installed on a server. You can set Microsoft Defender Antivirus to passive mode using a registry key.

You can set Microsoft Defender Antivirus to passive mode by setting the following registry key:

- Path: `HKLM\SOFTWARE\Policies\Microsoft\Windows Advanced Threat Protection`
- Name: `ForceDefenderPassiveMode`
- Type: `REG_DWORD`
- Value: `1`

Note

For passive mode to work on endpoints running Windows Server 2016 and Windows Server 2012 R2, those endpoints must be onboarded using the instructions in [Onboard Windows Server 2012 R2 and Windows Server 2016 to Microsoft Defender for Endpoint](onboard-server).

For more information, see [Microsoft Defender Antivirus in Windows](microsoft-defender-antivirus-windows).

## Microsoft Defender Antivirus seems to be stuck in passive mode

If Microsoft Defender Antivirus is stuck in passive mode, set it to active mode manually by following these steps:

1. On your Windows device, open Registry Editor as an administrator.
2. Go to `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Advanced Threat Protection`.
3. Set or define a **REG\_DWORD** entry called `ForceDefenderPassiveMode`, and set its value to `0`.
4. Reboot the device.

Important

If you're still having trouble setting Microsoft Defender Antivirus to active mode after following this procedure, [contact support](/en-us/Microsoft-365/admin/get-help-support).

## I'm having trouble re-enabling Microsoft Defender Antivirus on Windows Server 2016

If you're using a non-Microsoft antivirus/antimalware solution on Windows Server 2016, your existing solution might have required you to disable or uninstall Microsoft Defender Antivirus.

- **Disabled**: Use the `-WdEnable` option on the MpCmdRun command-line tool to enable Microsoft Defender Antivirus on Windows Server 2016:

    1. In an elevated Command Prompt (a Command Prompt window you opened by selecting **Run as administrator**), run the following commands:

        Tip

        The first command changes the directory to the latest version of &lt;antimalware platform version&gt; in `%ProgramData%\Microsoft\Windows Defender\Platform\<antimalware platform version>`. If that path doesn't exist, it goes to `%ProgramFiles%\Microsoft Defender`.

        ```dos
        (set "_done=" & if exist "%ProgramData%\Microsoft\Windows Defender\Platform\" (for /f "delims=" %d in ('dir "%ProgramData%\Microsoft\Windows Defender\Platform" /ad /b /o:-n 2^>nul') do if not defined _done (cd /d "%ProgramData%\Microsoft\Windows Defender\Platform\%d" & set _done=1)) else (cd /d "%ProgramFiles%\Windows Defender")) >nul 2>&1
        
        MpCmdRun.exe -WdEnable
        ```
    2. Restart the device.
- **Uninstalled**: In an elevated Command Prompt, do the following steps to reinstall Microsoft Defender Antivirus on Windows Server 2016:

    1. In an elevated Command Prompt, run the following commands:

        ```dos
        Dism /Online /Enable-Feature /FeatureName:Windows-Defender-Features
        
        Dism /Online /Enable-Feature /FeatureName:Windows-Defender
        
        Dism /Online /Enable-Feature /FeatureName:Windows-Defender-Gui
        ```

        Tip

        You can also use [Server Manager or PowerShell to install the Microsoft Defender Antivirus feature](microsoft-defender-antivirus-windows-server-configure#install-microsoft-defender-antivirus-on-windows-server).
    2. Reboot the system.