---
layout: Conceptual
title: Evaluate Microsoft Defender Antivirus using PowerShell - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/microsoft-defender-antivirus-using-powershell
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Businesses of all sizes can use this guide to evaluate and test the protection offered by Microsoft Defender Antivirus in Windows using PowerShell.
ms.service: defender-endpoint
ms.localizationpriority: medium
ms.topic: how-to
author: chrisda
ms.author: chrisda
ms.custom: nextgen, msecd-doc-authoring-1016
ms.date: 2026-07-02T00:00:00.0000000Z
ms.reviewer: yongrhee
ms.subservice: ngp
ms.collection:
- m365-security
- tier2
- mde-ngp
ai-usage: ai-assisted
locale: en-us
document_id: 1905b8e0-4e36-f7ce-6324-1ef941453f36
document_version_independent_id: 1905b8e0-4e36-f7ce-6324-1ef941453f36
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/microsoft-defender-antivirus-using-powershell.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: microsoft-defender-antivirus-using-powershell
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/microsoft-defender-antivirus-using-powershell.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 9906bd3d-1919-c090-ed56-ec4df4719d26
---

# Evaluate Microsoft Defender Antivirus using PowerShell - Microsoft Defender for Endpoint | Microsoft Learn

In Windows 10 or later and Windows Server 2016 or later, you can use the next-generation protection features in Microsoft Defender Antivirus with exploit protection.

The following sections explain how to enable and test the key protection features in Microsoft Defender Antivirus with exploit protection.

We recommend you use our [evaluation PowerShell script](https://aka.ms/wdeppscript) to configure these features, but you can individually enable each feature as described in this article.

For more information about our endpoint protection products and services, see the following resources:

- [Next-generation protection overview](next-generation-protection)
- [Microsoft Defender Antivirus in Windows](microsoft-defender-antivirus-windows)
- [Microsoft Defender Antivirus on Windows Server](microsoft-defender-antivirus-windows-server-configure)
- [Protect devices from exploits](exploit-protection)

If you have any questions about a detection by Microsoft Defender Antivirus, or you discover a missed detection, you can submit the file to us. For more information, see [Submit files for analysis](/en-us/defender-xdr/submission-guide).

## Use PowerShell to enable the features

This guide provides the [Microsoft Defender Antivirus cmdlets](/en-us/powershell/module/defender/) that configure the features you should use to evaluate our protection.

Use these cmdlets in an elevated PowerShell session (a PowerShell window you opened by selecting **Run as administrator**).

Before you make changes, you should view and record the current status of all settings by using one or both of the following methods:

- Use the [Get-MpPreference](/en-us/powershell/module/defender/get-mppreference) cmdlet.
- Install the [DefenderEval](https://www.powershellgallery.com/packages/DefenderEval/) module from the PowerShell Gallery, and then use the **Get-DefenderEvaluationReport** cmdlet.

Microsoft Defender Antivirus uses [standard Windows notifications](configure-notifications-microsoft-defender-antivirus) for detections. You can also [review detections in the Microsoft Defender Antivirus app](review-scan-results-microsoft-defender-antivirus).

The Windows Event Log also records detection and engine events. For more information, see [Review event logs and error codes to troubleshoot issues with Microsoft Defender Antivirus](troubleshoot-microsoft-defender-antivirus).

## Use PowerShell to configure cloud protection features

Standard definition updates can take hours to prepare and deliver. Our cloud-delivered protection service can deliver updated malware protection in seconds. For more information, see [Cloud protection and Microsoft Defender Antivirus](cloud-protection-microsoft-defender-antivirus).

- **Enable the Microsoft Defender Cloud for near-instant protection and increased protection**:

    ```powershell
    Set-MpPreference -MAPSReporting Advanced
    ```
- **Automatically submit samples to increase group protection**:

    ```powershell
    Set-MpPreference -SubmitSamplesConsent Always
    ```
- **Always use the cloud to block new malware within seconds**:

    ```powershell
    Set-MpPreference -DisableBlockAtFirstSeen 0
    ```
- **Scan all downloaded files and attachments**:

    ```powershell
    Set-MpPreference -DisableIOAVProtection 0
    ```
- **Set the cloud block level to High**:

    ```powershell
    Set-MpPreference -CloudBlockLevel High
    ```
- **Set the cloud block time-out to 1 minute**:

    ```powershell
    Set-MpPreference -CloudExtendedTimeout 50
    ```

## Use PowerShell to enable always-on protection (real-time scanning)

Microsoft Defender Antivirus scans files as Windows sees them, and monitors running processes for malicious behavior (known or suspected). If the antivirus engine discovers malicious activity, the engine immediately blocks the process or file from running. For more information on behavioral, heuristic, and real-time protection options, see [Configure behavioral, heuristic, and real-time protection](configure-protection-features-microsoft-defender-antivirus).

- **Constantly monitor files and processes for known malware activity**:

    ```powershell
    Set-MpPreference -DisableRealtimeMonitoring 0
    ```
- \*\*Constantly monitor for known malware behavior in running programs, even in files that aren't considered to be a threat:

    ```powershell
    Set-MpPreference -DisableBehaviorMonitoring 0
    ```
- **Scan scripts as soon as they're seen or run**:

    ```powershell
    Set-MpPreference -DisableScriptScanning 0
    ```
- **Scan removable drives as soon as they're inserted or mounted**:

    ```powershell
    Set-MpPreference -DisableRemovableDriveScanning 0
    ```

## Use PowerShell to enable potentially unwanted application protection

[Potentially unwanted applications](detect-block-potentially-unwanted-apps-microsoft-defender-antivirus) are files and apps that aren't traditionally classified as malicious. These types of apps include:

- Non-Microsoft installers.
- Apps that do ad injection.
- Some types of browser toolbars.

**Prevent grayware, adware, and other potentially unwanted apps from installing**:

```powershell
Set-MpPreference -PUAProtection Enabled
```

## Use PowerShell to configure email and archive scanning

You can set Microsoft Defender Antivirus to automatically scan certain types of email files and archive files (such as .zip files) when Windows see them. For more information, see [Managed email scans in Microsoft Defender](configure-advanced-scan-types-microsoft-defender-antivirus).

**Scan email files and archives**:

```powershell
Set-MpPreference -DisableArchiveScanning 0 -DisableEmailScanning 0
```

## Manage product and protection updates

Typically, you get Microsoft Defender Antivirus updates from Windows update once per day. You can increase the update frequency by setting the following options and [ensuring Microsoft Configuration Manager, Group Policy, or Microsoft Intune manages your updates](deploy-manage-report-microsoft-defender-antivirus).

- **Update signatures every day (default)**:

    ```powershell
    Set-MpPreference -SignatureUpdateInterval
    ```
- **Update signatures before running a scheduled scan**:

    ```powershell
    Set-MpPreference -CheckForSignaturesBeforeRunningScan 1
    ```

## Use PowerShell to configure advanced threat mitigation features

Exploit protection provides features that help protect devices from known malicious behaviors and attacks on vulnerable technologies. Controlled folder access (CFA) protects sensitive data in specific folders by preventing untrusted apps from writing to those locations.

- **Prevent malicious and suspicious apps (such as ransomware) from making changes to protected folders with [controlled folder access (CFA)](controlled-folder-access-overview)**:

    ```powershell
    Set-MpPreference -EnableControlledFolderAccess Enabled
    ```
- **Block connections to known bad IP addresses and other network connections with [Network protection](network-protection)**:

    ```powershell
    Set-MpPreference -EnableNetworkProtection Enabled
    ```
- **Apply a standard set of mitigations with [Exploit protection](exploit-protection)**:

    ```powershell
    Invoke-WebRequest https://demo.wd.microsoft.com/Content/ProcessMitigation.xml -OutFile ProcessMitigation.xml
    
    Set-ProcessMitigation -PolicyFilePath ProcessMitigation.xml
    ```
- **Block known malicious attack vectors with [attack surface reduction (ASR) rules](attack-surface-reduction-rules-overview)**:

    Important

    Typically, you can enable the [standard protection rules](attack-surface-reduction-rules-overview#asr-rules) in **Block** or **Warn** mode without testing. You should test other ASR rules in **Audit** mode before you switch them to **Block** or **Warn** mode. For more information, see the [ASR rules deployment guide](attack-surface-reduction-rules-deployment).

    ```powershell
    Add-MpPreference -AttackSurfaceReductionRules_Ids 56a863a9-875e-4185-98a7-b882c64b5ce5,9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2,e6db77e5-3df2-4cf1-b95a-636979351e5b -AttackSurfaceReductionRules_Actions Enabled,Enabled,Enabled
    
    Add-MpPreference -AttackSurfaceReductionRules_Ids 01443614-cd74-433a-b99e-2ecdc07bfc25,26190899-1602-49e8-8b27-eb1d0a1ce869 ,33ddedf1-c6e0-47cb-833e-de6133960387,3b576869-a4ec-4529-8536-b80a7769e899,5beb7efe-fd9a-4556-801d-275e5ffc04cc,75668c1f-73b5-4cf0-bb93-3ecf5cb7cc84,7674ba52-37eb-4a4f-a9a1-f0f9a1619a2c,92e97fa1-2edf-4476-bdd6-9dd0b4dddc7b,b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4,be9ba2d9-53ea-4cdc-84e5-9b1eeee46550,c1db55ab-c21a-4637-bb3f-a12568109d35,d1e49aac-8f56-4280-b9ba-993a6d77406c,d3e037e1-3eb8-44c8-a917-57927947596d,d4f940ab-401b-4efc-aadc-ad5f3c50688a,a8f5898e-1dc8-49a9-9878-85004b8a61e6,c0033c00-d16d-4114-a5a0-dc9b3a7d2ceb -AttackSurfaceReductionRules_Actions AuditMode,AuditMode,AuditMode,AuditMode,AuditMode,AuditMode,AuditMode,AuditMode,AuditMode,AuditMode,AuditMode,AuditMode,AuditMode,AuditMode,AuditMode,AuditMode
    ```

### Enable tamper protection

Tamper protection prevents unauthorized changes to your security settings. For more information about configuring tamper protection, see [How do I configure or manage tamper protection](tamper-protection-overview).

#### Check the Cloud Protection network connectivity

Cloud Protection is the cloud-delivered protection service in Microsoft Defender Antivirus. It's important to verify that Cloud Protection network connectivity is working during your penetration testing by doing the following steps:

In an elevated Command Prompt (a Command Prompt window you opened by selecting **Run as administrator**), run the following commands:

Tip

The first command changes the directory to the latest version of &lt;antimalware platform version&gt; in `%ProgramData%\Microsoft\Windows Defender\Platform\<antimalware platform version>`. If that path doesn't exist, it goes to `%ProgramFiles%\Windows Defender`.

```dos
(set "_done=" & if exist "%ProgramData%\Microsoft\Windows Defender\Platform\" (for /f "delims=" %d in ('dir "%ProgramData%\Microsoft\Windows Defender\Platform" /ad /b /o:-n 2^>nul') do if not defined _done (cd /d "%ProgramData%\Microsoft\Windows Defender\Platform\%d" & set _done=1)) else (cd /d "%ProgramFiles%\Windows Defender")) >nul 2>&1

MpCmdRun.exe -ValidateMapsConnection
```

For more information, see [Configure and manage Microsoft Defender Antivirus with the MpCmdRun command-line tool](command-line-arguments-microsoft-defender-antivirus).

## One-select Microsoft Defender Offline Scan

Microsoft Defender Offline Scan is a specialized tool that allows you to boot a machine into a dedicated environment outside of the normal operating system. It's especially useful for potent malware, such as rootkits.

For more information, see [Microsoft Defender Offline](microsoft-defender-offline).

**Ensure notifications allow you to boot the device into a specialized malware removal environment**:

```powershell
Set-MpPreference -UILockdown 0
```