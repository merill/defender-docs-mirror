---
layout: Conceptual
title: Collect Microsoft Defender Antivirus diagnostic data - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/collect-diagnostic-data
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use MpCmdRun to collect Microsoft Defender Antivirus diagnostic data locally or copy support packages to a central location.
ms.service: defender-endpoint
ms.localizationpriority: medium
author: chrisda
ms.author: chrisda
ms.custom: nextgen, msecd-doc-authoring-1015
ms.date: 2026-09-22T00:00:00.0000000Z
ms.reviewer: pahuijbr, yongrhee
ms.subservice: ngp
ms.topic: how-to
ms.collection:
- m365-security
- tier2
- mde-ngp
ai-usage: ai-assisted
locale: en-us
document_id: 4afab059-410a-da21-aea5-e5a40f21f882
document_version_independent_id: 4afab059-410a-da21-aea5-e5a40f21f882
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/collect-diagnostic-data.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: collect-diagnostic-data
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/collect-diagnostic-data.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 902c7782-0926-19ee-b0f3-80f3e67cf7c9
---

# Collect Microsoft Defender Antivirus diagnostic data - Microsoft Defender for Endpoint | Microsoft Learn

Use `MpCmdRun.exe` to collect Microsoft Defender Antivirus diagnostic data when Microsoft support or engineering teams help you troubleshoot device issues. Save the support package on the affected device, or copy packages from multiple devices to a central location.

Note

To collect a Defender for Endpoint investigation package instead, see [Collect an investigation package from a device](respond-machine-alerts#collect-investigation-package-from-devices).

For Microsoft Defender Antivirus performance issues, use [Performance analyzer for Microsoft Defender Antivirus](tune-performance-defender-antivirus).

## Collect diagnostic data by using MpCmdRun

On each affected device, choose whether to keep the diagnostic package on the device or copy it to a central location:

1. Open an elevated Command Prompt (a Command Prompt window you opened by selecting **Run as administrator**), and then use one of the following options:

    - **Save the diagnostic log files on the local device**: The following commands change to the latest available Microsoft Defender Antivirus platform folder and create the support package:

        Tip

        The first command changes the directory to the latest version of &lt;antimalware platform version&gt; in `%ProgramData%\Microsoft\Windows Defender\Platform\<antimalware platform version>`. If that path doesn't exist, it goes to `%ProgramFiles%\Windows Defender`.

        ```dos
        (set "_done=" & if exist "%ProgramData%\Microsoft\Windows Defender\Platform\" (for /f "delims=" %d in ('dir "%ProgramData%\Microsoft\Windows Defender\Platform" /ad /b /o:-n 2^>nul') do if not defined _done (cd /d "%ProgramData%\Microsoft\Windows Defender\Platform\%d" & set _done=1)) else (cd /d "%ProgramFiles%\Windows Defender")) >nul 2>&1
        
        MpCmdRun.exe -GetFiles
        ```

        By default, `MpCmdRun.exe` generates, compresses, and saves the diagnostic log files to `C:\ProgramData\Microsoft\Windows Defender\Support\MpSupportFiles.cab`.

        The `.cab` filename is the same on every device.
    - **Copy the diagnostic log files to a central location**: The following syntax creates the local support package and copies it to the specified root path:

        ```dos
        (set "_done=" & if exist "%ProgramData%\Microsoft\Windows Defender\Platform\" (for /f "delims=" %d in ('dir "%ProgramData%\Microsoft\Windows Defender\Platform" /ad /b /o:-n 2^>nul') do if not defined _done (cd /d "%ProgramData%\Microsoft\Windows Defender\Platform\%d" & set _done=1)) else (cd /d "%ProgramFiles%\Windows Defender")) >nul 2>&1
        
        MpCmdRun.exe -GetFiles -SupportLogLocation <RootPath>
        ```

        The tool creates `C:\ProgramData\Microsoft\Windows Defender\Support\MpSupportFiles.cab`, and then copies the `.cab` file with a new name into a subfolder of `<RootPath>` (for example, `P:\Data` or `\\Server01\Data`). The copied file uses the following path and filename syntax: `<RootPath>\<MMDD>\MpSupport-<Hostname>-<HHMM>.cab`.

        - `<RootPath>` is the value you specified for `-SupportLogLocation`.
        - `<MMDD>` is the month and day when you ran the MpCmdRun command (for example, 0318 for March 18).
        - `<Hostname>` is the name of the device where you ran the MpCmdRun command (for example, LAPTOP01).
        - `<HHMM>` is the hour and minute when you ran the MpCmdRun command (for example, `2221` for 22:21).

    Note

    If the tool can't copy the `.cab` file to the specified location, check the default local location at `C:\ProgramData\Microsoft\Windows Defender\Support\MpSupportFiles.cab`.

    The following example copies the support package from the device named LAPTOP01 on March 18 at 22:21:

    ```dos
    (set "_done=" & if exist "%ProgramData%\Microsoft\Windows Defender\Platform\" (for /f "delims=" %d in ('dir "%ProgramData%\Microsoft\Windows Defender\Platform" /ad /b /o:-n 2^>nul') do if not defined _done (cd /d "%ProgramData%\Microsoft\Windows Defender\Platform\%d" & set _done=1)) else (cd /d "%ProgramFiles%\Windows Defender")) >nul 2>&1
    
    MpCmdRun.exe -GetFiles -SupportLogLocation "\\SERVER01\Data"
    ```

    The resulting `.cab` file is available at `\\SERVER01\Data\0318\MpSupport-LAPTOP01-2221.cab`. The hostname and time in the filename distinguish files collected from different devices.
2. Wait a few minutes for `MpCmdRun.exe` to generate and compress the diagnostic log files. The resulting `.cab` file includes:

    - Any trace files from Microsoft Antimalware Service.
    - The Windows Update history log.
    - All Microsoft Antimalware Service events from the System event log.
    - All relevant Microsoft Antimalware Service registry locations.
    - The log file of MpCmdRun.
    - The log file of the signature update helper tool.

    Copy the `.cab` files to a secure location that Microsoft support can access, such as a password-protected OneDrive folder.

## Configure the diagnostic file copy location by using Group Policy

Configure the **Define the directory path to copy support log files** policy to copy diagnostic packages to a central location after `MpCmdRun.exe` creates them on each device. When you configure this policy, you don't need to use the `-SupportLogLocation` option with `MpCmdRun.exe -GetFiles`.

Use the procedure in [Configure Microsoft Defender Antivirus using Group Policy](use-group-policy-microsoft-defender-antivirus#configure-microsoft-defender-antivirus-using-group-policy) to open and edit a Group Policy object (GPO) that applies to the target devices. For domain-based Group Policy, you can manage the templates in the [Group Policy Central Store](/en-us/troubleshoot/windows-client/group-policy/create-and-manage-central-store#the-central-store).

To configure the diagnostic file copy location:

1. In the **Group Policy Management Editor**, go to **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus**.

    [![Screenshot of Local Group Policy Editor with Microsoft Defender Antivirus selected in the console tree.](media/gpo1-supportloglocationdefender.png)](media/gpo1-supportloglocationdefender.png#lightbox)
2. Open **Define the directory path to copy support log files**.
3. Select **Enabled**. In **Options**, enter the directory path where you want the tool to copy support packages.

    [![Screenshot of Local Group Policy Editor with Enabled selected and a path value entered in the Options section.](media/gpo3-supportloglocationgppageenabledexample.png)](media/gpo3-supportloglocationgppageenabledexample.png#lightbox)
4. Select **OK**.

The policy configures the `SupportLogLocation` value under `HKLM\Software\Policies\Microsoft\Windows Defender`.