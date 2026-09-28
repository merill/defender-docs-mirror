---
layout: Conceptual
title: Migrating from non-Microsoft HIPS to attack surface reduction rules - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/migrating-asr-rules
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to map rules from a non-Microsoft Host Intrusion Prevention System (HIPS) solution to attack surface reduction rules in Microsoft Defender for Endpoint.
ms.topic: upgrade-and-migration-article
ms.service: defender-endpoint
ms.localizationpriority: medium
audience: ITPro
author: chrisda
ms.author: chrisda
ms.custom: asr, msecd-doc-authoring-1012
ms.subservice: asr
ms.collection:
- m365-security
- tier2
- mde-asr
ms.date: 2026-05-04T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 1eb42cac-5c41-0c77-e8c9-a728488e1acd
document_version_independent_id: 1eb42cac-5c41-0c77-e8c9-a728488e1acd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/migrating-asr-rules.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: migrating-asr-rules
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/migrating-asr-rules.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
- https://authoring-docs-microsoft.poolparty.biz/devrel/bba62c59-6b53-4be4-8b9d-6624f9184c22
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
- https://authoring-docs-microsoft.poolparty.biz/devrel/f3a81ffb-ee36-4ec7-b54a-01b6681aff65
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 5aed856e-17ce-a236-dc98-e05ece60755a
---

# Migrating from non-Microsoft HIPS to attack surface reduction rules - Microsoft Defender for Endpoint | Microsoft Learn

This article helps you map common rules to Microsoft Defender for Endpoint. For more information about ASR rules, see [Attack surface reduction (ASR) rules overview](attack-surface-reduction-rules-overview).

## Scenarios when migrating from a non-Microsoft HIPS product to attack surface reduction rules

### Block creation of specific files

- **Applies to**: All processes
- **Processes**: N/A
- **Operation**: File Creation
- **Examples of Files/Folders, Registry Keys/Values, Processes, or Services**:
    - `.jaff`
    - `.krab`
    - `.locky`
    - `.lukitus`
    - `.odin`
    - `.wnry`
    - `.zepto`
- **Attack surface reduction rules**:
    - ASR rules block attack techniques, not indicators of compromise (IOC).
    - Blocking a specific file extension isn't always useful, because it doesn't prevent a device from compromise. It only partially thwarts an attack until attackers create a new type of extension for the payload.
- **Other recommended features**:
    - Microsoft highly recommends enabling Microsoft Defender Antivirus, [cloud protection](cloud-protection-microsoft-defender-antivirus) and [behavioral blocking](client-behavioral-blocking).
    - Microsoft recommends other prevention measures, such as the ASR rule [Use advanced protection against ransomware](attack-surface-reduction-rules-reference#use-advanced-protection-against-ransomware) (`c1db55ab-c21a-4637-bb3f-a12568109d35`), which provides a greater level of protection against ransomware attacks.
    - Microsoft Defender for Endpoint monitors many of these registry keys, such as Autostart Extension Points (ASEP) techniques, which trigger specific alerts. The registry keys used require a minimum of Local Admin or Trusted Installer privileges. Microsoft recommends using a locked-down environment with minimum administrative accounts or rights. You can enable other system configurations, including disabling the `SeDebugPrivilege` as part of wider security recommendations.

### Block creation of specific registry keys

- **Applies to**: All Processes
- **Processes**: N/A
- **Operation**: Registry Modifications
- **Examples of Files/Folders, Registry Keys/Values, Processes, or Services**:
    - `HKCU\Environment\UserInitMprLogonScript`
    - `HKCU\Software\Microsoft\HtmlHelp Author\location`
    - `HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Accessibility\ATs*\StartExe`
    - `HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options*\Debugger`
    - `HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SilentProcessExit*\MonitorProcess`
- **Attack surface reduction rules**:
    - ASR rules block attack techniques, not indicators of compromise (IOC).
    - Blocking a specific file extension isn't always useful, because it doesn't prevent a device from compromise. It only partially thwarts an attack until attackers create a new type of extension for the payload.
- **Other recommended features**:
    - Microsoft highly recommends enabling Microsoft Defender Antivirus, [cloud protection](cloud-protection-microsoft-defender-antivirus) and [behavioral blocking](client-behavioral-blocking).
    - Microsoft recommends other prevention measures, including the ASR rule [Use advanced protection against ransomware](attack-surface-reduction-rules-reference#use-advanced-protection-against-ransomware) (`c1db55ab-c21a-4637-bb3f-a12568109d35`), which provides a greater level of protection against ransomware attacks.
    - Microsoft Defender for Endpoint monitors many of these registry keys, such as Autostart Extension Points (ASEP) techniques, which trigger specific alerts. The registry keys used require a minimum of Local Admin or Trusted Installer privileges. Microsoft recommends using a locked-down environment with minimum administrative accounts or rights. You can enable other system configurations, including disabling the `SeDebugPrivilege` as part of wider security recommendations.

### Block untrusted programs from running from removable drives

- **Applies to**: Untrusted Programs from USB
- **Processes**:
    - `*`
- **Operation**: Process Execution
- **Examples of Files/Folders, Registry Keys/Values, Processes, or Services**:
- **Attack surface reduction rules**:
    - Use the ASR rule named [Block untrusted and unsigned processes that run from USB](attack-surface-reduction-rules-reference#block-untrusted-and-unsigned-processes-that-run-from-usb) (`b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4`)
- **Other recommended features**:
    - For more information about controls for USB devices and other removable media using Defender for Endpoint, see [Device control in Microsoft Defender for Endpoint](device-control-overview).

### Block Mshta from launching certain child processes

- **Applies to**: Mshta
- **Processes**:
    - `mshta.exe`
- **Operation**: Process Execution
- **Examples of Files/Folders, Registry Keys/Values, Processes, or Services**:
    - `cmd.exe`
    - `powershell.exe`
    - `regsvr32.exe`
- **Attack surface reduction rules**: There are no specific ASR rules to prevent child processes from mshta.exe. This type of control is available in [exploit protection](exploit-protection) or [Application Control for Windows](/en-us/windows/security/application-security/application-control/app-control-for-business/appcontrol).
- **Other recommended features**:
    - Enable application control to prevent mshta.exe from running at all. If your organization requires *mshta.exe* for line of business apps, configure a specific exploit protection rule to prevent mshta.exe from launching child processes.

### Block Outlook from launching child processes

- **Applies to**: Outlook
- **Processes**:
    - `outlook.exe`
- **Operation**: Process Execution
- **Examples of Files/Folders, Registry Keys/Values, Processes, or Services**:
    - `powershell.exe`
- **Attack surface reduction rules**:
    - The ASR rule [Block Office communication application from creating child processes](attack-surface-reduction-rules-reference#block-office-communication-application-from-creating-child-processes) (`26190899-1602-49e8-8b27-eb1d0a1ce869`) prevents Office communication apps (Outlook, Skype, and Teams) from launching child processes.
- **Other recommended features**:
    - Microsoft recommends enabling [PowerShell constrained language mode](https://devblogs.microsoft.com/powershell/powershell-constrained-language-mode/) to minimize the attack surface from PowerShell.

### Block Office apps from launching child processes

- **Applies to**: Office
- **Processes**:
    - `excel.exe`
    - `powerpnt.exe`
    - `winword.exe`
- **Operation**: Process Execution
- **Examples of Files/Folders, Registry Keys/Values, Processes, or Services**:
    - `EQNEDT32.EXE`
    - `cmd.exe`
    - `mshta.exe`
    - `powershell.exe`
    - `regsrv32.exe`
    - `wscript.exe`
- **Attack surface reduction rules**:
    - The ASR rule [Block all Office applications from creating child processes](attack-surface-reduction-rules-reference#block-all-office-applications-from-creating-child-processes) (`d4f940ab-401b-4efc-aadc-ad5f3c50688a`) prevents Office apps from launching child processes.
- **Other recommended features**: N/A

### Block Office apps from creating executable content

- **Applies to**: Office
- **Processes**:
    - `winword.exe`
    - `powerpnt.exe`
    - `excel.exe`
- **Operation**: File Creation
- **Examples of Files/Folders, Registry Keys/Values, Processes, or Services**:
    - `C:\ProgramData**.com`
    - `C:\ProgramData**.exe`
    - `C:\ProgramData**.scf`
    - `C:\Users*AppData\Local\Temp**.com`
    - `C:\Users*\AppData**.exe`
    - `C:\Users*\AppData**.scf`
    - `C:\Users*\Desktop**.exe`
    - `C:\Users*\Downloads**.exe`
    - `C:\Users\Public**.exe`
- **Attack surface reduction rules**:
    - The ASR rule [Block Office applications from creating executable content](attack-surface-reduction-rules-reference#block-office-applications-from-creating-executable-content) (`3b576869-a4ec-4529-8536-b80a7769e899`) prevents Office apps from saving malicious executable content to disk.

### Block Wscript from reading certain types of files

- **Applies to**: Wscript
- **Processes**:
    - `wscript.exe`
- **Operation**: File Read
- **Examples of Files/Folders, Registry Keys/Values, Processes, or Services**:
- `C:\Users*\AppData**.js`
- `C:\Users*\Downloads**.js`
- **Attack surface reduction rules**:
    - Due to reliability and performance issues, ASR rules can't prevent a process from reading specific types of script files. But the following ASR rules can help prevent attack vectors that might originate from these scenarios:
        - [Block JavaScript or VBScript from launching downloaded executable content](attack-surface-reduction-rules-reference#block-javascript-or-vbscript-from-launching-downloaded-executable-content) (`d3e037e1-3eb8-44c8-a917-57927947596d`)
        - [Block execution of potentially obfuscated scripts](attack-surface-reduction-rules-reference#block-execution-of-potentially-obfuscated-scripts) (`5beb7efe-fd9a-4556-801d-275e5ffc04cc`)
- **Other recommended features**:
    - By default, the Antimalware Scan Interface (AMSI) can inspect various scripts in real time (for example, PowerShell, Windows Script Host, JavaScript, VBScript, and more). For more information, see [Antimalware Scan Interface (AMSI)](/en-us/windows/win32/amsi/antimalware-scan-interface-portal).

### Block launch of child processes

- **Applies to**: Adobe Acrobat
- **Processes**:
    - `AcroRd32.exe`
    - `Acrobat.exe`
- **Operation**: Process Execution
- **Examples of Files/Folders, Registry Keys/Values, Processes, or Services**:
    - `cmd.exe`
    - `powershell.exe`
    - `wscript.exe`
- **Attack surface reduction rules**:
    - The ASR rule [Block Adobe Reader from creating child processes](attack-surface-reduction-rules-reference#block-adobe-reader-from-creating-child-processes) (`7674ba52-37eb-4a4f-a9a1-f0f9a1619a2c`) prevents Adobe Reader from launching child processes.
- **Other recommended features**: N/A

### Block download or creation of executable content

- **Applies to**: CertUtil
- **Processes**:
    - `certutil.exe`
- **Operation**: File Creation
- **Examples of Files/Folders, Registry Keys/Values, Processes, or Services**:
    - `*.exe`
- **Attack surface reduction rules**:
    - ASR rules don't support these scenarios because they're included in Microsoft Defender Antivirus protection.
- **Other recommended features**:
    - Microsoft Defender Antivirus prevents CertUtil from creating or downloading executable content.

### Block processes from stopping critical System components

- **Applies to**: All Processes
- **Processes**:
    - `*`
- **Operation**: Process Termination
- **Examples of Files/Folders, Registry Keys/Values, Processes, or Services**:
    - `MsMpEng.exe`
    - `MsSense.exe`
    - `NisSrv.exe`
    - `csrss.exe`
    - `services.exe`
    - `smss.exe`
    - `svchost.exe`
    - `wininit.exe`
    - and more
- **Attack surface reduction rules**: ASR rules don't support these scenarios because they're included in Windows built-in security protections.
- **Other recommended features**:
    - [Early Launch AntiMalware (ELAM)](/en-us/defender-endpoint/elam-on-mdav)
    - [Protection Process Light (PPL) and PPL AntiMalware Light](/en-us/windows/win32/services/protecting-anti-malware-services-)
    - [System Guard](/en-us/windows/security/hardware-security/how-hardware-based-root-of-trust-helps-protect-windows)

### Block specific launch Process Attempt

- **Applies to**: Specific processes
- **Processes**: Specific processes
- **Operation**: Process Execution
- **Examples of Files/Folders, Registry Keys/Values, Processes, or Services**:
    - `tor.exe`
    - `bittorrent.exe`
    - `cmd.exe`
    - `powershell.exe`
    - and more
- **Attack surface reduction rules**:
    - Overall, ASR rules aren't designed to act as an application manager.
- **Other recommended features**:
    - To prevent users from launching specific processes or programs, use [Application Control for Windows](/en-us/windows/security/application-security/application-control/app-control-for-business/appcontrol).
    - Although it isn't an application control mechanism, you can use Microsoft Defender for Endpoint indicators of compromise (IOCs) for [files](indicator-file) and [certificates](indicator-certificates) in incident response scenarios.

### Block unauthorized changes to Microsoft Defender Antivirus configurations

- **Applies to**: All Processes
- **Processes**:
    - `*`
- **Operation**: Registry Modifications
- **Examples of Files/Folders, Registry Keys/Values, Processes, or Services**:
    - `HKLM\SOFTWARE\Policies\Microsoft\Windows Defender\DisableAntiSpyware`
    - `HKLM\SOFTWARE\Policies\Microsoft\Windows Defender\Policy Manager\AllowRealTimeMonitoring`
    - and more
- **Attack surface reduction rules**: ASR rules don't support these scenarios because they're included in Microsoft Defender for Endpoint built-in protection.
- **Other recommended features**:
    - [Tamper protection in Microsoft Defender for Endpoint](tamper-protection-overview) prevents unauthorized changes to the registry keys associated with Microsoft Defender Antivirus. For example:
    - DisableAntiVirus
    - DisableAntiSpyware
    - DisableRealtimeMonitoring
    - DisableOnAccessProtection
    - DisableBehaviorMonitoring
    - DisableIOAVProtection
    - and more