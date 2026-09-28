---
layout: Conceptual
title: Troubleshoot Microsoft Defender Antivirus service startup problems - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-service-startup-problems
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to troubleshoot Microsoft Defender Antivirus service startup problems.
author: chrisda
ms.author: chrisda
ms.reviewer: yongrhee
ms.service: defender-endpoint
ms.topic: troubleshooting-general
ms.date: 2026-01-08T00:00:00.0000000Z
ms.subservice: ngp
ms.localizationpriority: medium
ms.collection: 
ms.custom: partner-contribution
locale: en-us
document_id: 903767b3-92b2-6a96-76b4-2694081fe351
document_version_independent_id: 903767b3-92b2-6a96-76b4-2694081fe351
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/troubleshoot-service-startup-problems.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: troubleshoot-service-startup-problems
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/troubleshoot-service-startup-problems.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 09f1a7fb-8a65-790f-5a67-db9312f43ea5
---

# Troubleshoot Microsoft Defender Antivirus service startup problems - Microsoft Defender for Endpoint | Microsoft Learn

In the following screenshot, **Virus & threat protection** displays a red cross, where it says **Threat service has stopped. Restart it now**.

![Screenshot of virus and threat protection notification.](media/virus-threat-protection.jpg)

Within **Security Providers**, you can see the following result.

**Microsoft Defender Antivirus is turned off**.

![Screenshot of security providers.](media/security-providers.png)

The following screenshot displays the message: **Threat service has stopped. Restart it now.**

![Screenshot of threat service has stopped.](media/virus-threat-protection-2.png)

The following screenshot displays the message: **Unexpected error. Sorry, we ran into a problem. Please try again.**

Select **Close**.

[![Screenshot of unexpected error.](media/unexpected-error.png)](media/unexpected-error.png#lightbox)

## Events

The *Windows Defender – Operational* event log might display the following events:

### Event 5007

The configuration of Microsoft Defender Antivirus changed. If you expected this event, review the settings, as it might be the result of malware.

| Old value | New value |
| --- | --- |
| `HKLM\SOFTWARE\Microsoft\Windows Defender\Diagnostics\RolledbackPlatformHealthData = <OVERALL>:<BAD>, <AGE>:<36>, <DIRTY_SHUTDOWNS>:<22>` | `Default\Diagnostics\RolledbackPlatformHealthData = 0` |
| `Default\ServiceStartStates = 0x0` | `HKLM\SOFTWARE\Microsoft\Windows Defender\ServiceStartStates = 0x1` |
| `HKLM\SOFTWARE\Microsoft\Windows Defender\ServiceStartStates = 0x1` | `Default\ServiceStartStates = 0x0` |
| `Default\ProductAppDataPath = C:\ProgramData\Microsoft\Windows Defender` | `HKLM\SOFTWARE\Microsoft\Windows Defender\ProductAppDataPath = C:\ProgramData\Microsft\Windows Defender` |
| `Default\IsServiceRunning = 0x0` | `HKLM\SOFTWARE\Microsoft\Windows Defender\IsServiceRunning = 0x1` |
| `Default\ProductAppDataPath = C:\ProgramData\Microsoft\Windows Defender` | `HKLM\SOFTWARE\Microsoft\Windows Defender\ProductAppDataPath = C:\ProgramData\Microsoft\Windows Defender` |
| `Default\IsServiceRunning = 0x0` | `HKLM\SOFTWARE\Microsoft\Windows Defender\IsServiceRunning = 0x1` |

### Event 5001

Microsoft Defender Antivirus Real-time Protection scanning for malware and other potentially unwanted software was disabled.

## Resolution

To resolve the issue, do the following steps:

1. Check the services and filter drivers for Microsoft Defender Antivirus.

    Run the following command in an elevated PowerShell window (a PowerShell window you opened by selecting **Run as administrator**):

    ```powershell
    Get-Service WinDefend, WdBoot, WdFilter, WdNisSvc, WdNisDrv, SecurityHealthService, wscsvc | Format-Table -Auto DisplayName, Name, StartType, Status
    ```

    | Display Name | Name | StartType | Status | Comments |
    | --- | --- | --- | --- | --- |
    | Windows Security Service | SecurityHealthService | Manual | Running |  |
    | Microsoft Defender Antivirus Boot Driver | WdBoot | Boot | Stopped | It's normal to be stopped after boot. |
    | Microsoft Defender Antivirus Mini-Filter Driver | WdFilter | Boot | Running | If stopped, check steps 3, 6, 7. |
    | Microsoft Defender Antivirus Network Inspection System Driver | WdNisDrv | Manual | Running | If stopped, check steps 3, 6, 7. |
    | Microsoft Defender Antivirus Network Inspection Service | WdNisSvc | Manual | Running | If stopped, check steps 3, 6, 7. |
    | Microsoft Defender Antivirus Service | WinDefend | Automatic | Running | If stopped, check steps 3, 6, 7. |
    | wscsvc | Security Center | Automatic | Running |  |
2. Download and run the [Microsoft Safety Scanner](safety-scanner-download) to rule out any malware.
3. If you're using Microsoft Defender Antivirus as your primary antivirus, make sure to uninstall non-Microsoft antivirus software.
4. Remove the Security Intelligence and engine and reset the platform:

    1. In an elevated Command Prompt (a Command Prompt window you opened by selecting **Run as administrator**), run the following command:

        Tip

        This command changes the directory to the latest version of &lt;antimalware platform version&gt; in `%ProgramData%\Microsoft\Windows Defender\Platform\<antimalware platform version>`. If that path doesn't exist, it goes to `%ProgramFiles%\Microsoft Defender`.

        ```dos
        (set "_done=" & if exist "%ProgramData%\Microsoft\Windows Defender\Platform\" (for /f "delims=" %d in ('dir "%ProgramData%\Microsoft\Windows Defender\Platform" /ad /b /o:-n 2^>nul') do if not defined _done (cd /d "%ProgramData%\Microsoft\Windows Defender\Platform\%d" & set _done=1)) else (cd /d "%ProgramFiles%\Windows Defender")) >nul 2>&1
        ```
    2. Remove the **Security Intelligence** and **engine**:

        ```dos
        MpCmdRun.exe -RemoveDefinitions -All
        ```
    3. Reset the **Platform**:

        ```dos
        MpCmdRun.exe -ResetPlatform
        ```

    For more information, see [Manage the sources for Microsoft Defender Antivirus protection updates](manage-protection-updates-microsoft-defender-antivirus).
5. Backup Microsoft Defender Antivirus policies.

    In an elevated PowerShell session (a PowerShell window you opened by selecting **Run as administrator**), run the following command:

    ```powershell
    New-Item -Path "C:\DefenderTemp" -ItemType Directory; Invoke-Command {reg export 'HKLM\SOFTWARE\Policies\Microsoft\Windows Defender' C:\DefenderTemp\_DefenderAVBackup.reg}
    ```
6. Delete any policies that are set for Microsoft Defender Antivirus.

    Run the following command in an elevated PowerShell session:

    ```powershell
    Remove-Item -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows Defender' -Force
    ```

    For more information, see: [Troubleshoot Microsoft Defender Antivirus settings](troubleshoot-settings).
7. Re-enable Microsoft Defender Antivirus.

    Run the following commands in an elevated Command Prompt:

    ```dos
    (set "_done=" & if exist "%ProgramData%\Microsoft\Windows Defender\Platform\" (for /f "delims=" %d in ('dir "%ProgramData%\Microsoft\Windows Defender\Platform" /ad /b /o:-n 2^>nul') do if not defined _done (cd /d "%ProgramData%\Microsoft\Windows Defender\Platform\%d" & set _done=1)) else (cd /d "%ProgramFiles%\Windows Defender")) >nul 2>&1
    
    MpCmdRun.exe" -WdEnable
    ```
8. Update Security Intelligence.

    Run the following commands in an elevated Command Prompt:

    ```dos
    (set "_done=" & if exist "%ProgramData%\Microsoft\Windows Defender\Platform\" (for /f "delims=" %d in ('dir "%ProgramData%\Microsoft\Windows Defender\Platform" /ad /b /o:-n 2^>nul') do if not defined _done (cd /d "%ProgramData%\Microsoft\Windows Defender\Platform\%d" & set _done=1)) else (cd /d "%ProgramFiles%\Windows Defender")) >nul 2>&1
    
    MpCmdRun.exe -SignatureUpdate -MMPC
    ```
9. Verify **Tamper Protection** is enabled.

    ![Screenshot of Tamper Protection is enabled.](media/tamper-protection.png)
10. Run **Microsoft Update**.