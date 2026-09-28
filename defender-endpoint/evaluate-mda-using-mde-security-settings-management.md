---
layout: Conceptual
title: Evaluate Microsoft Defender Antivirus with security policies - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/evaluate-mda-using-mde-security-settings-management
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: yongrhee
description: Learn how to evaluate Microsoft Defender Antivirus protection settings on Windows devices by using endpoint security policies in the Microsoft Defender portal.
ms.service: defender-endpoint
ms.author: chrisda
author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.topic: how-to
ms.subservice: edr
ms.date: 2026-09-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
locale: en-us
document_id: 62f641a9-3e7c-0f2b-f0dc-3dcec9c3c601
document_version_independent_id: 62f641a9-3e7c-0f2b-f0dc-3dcec9c3c601
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/evaluate-mda-using-mde-security-settings-management.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: evaluate-mda-using-mde-security-settings-management
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/evaluate-mda-using-mde-security-settings-management.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: a55ecc62-92e9-3008-ee7a-82740381927a
---

# Evaluate Microsoft Defender Antivirus with security policies - Microsoft Defender for Endpoint | Microsoft Learn

Use endpoint security policies in the Microsoft Defender portal to configure and test Microsoft Defender Antivirus and Windows protection features. The evaluation includes real-time protection, cloud-delivered protection, network protection, attack surface reduction (ASR) rules, and tamper protection.

## Prerequisites

If you have any questions about a detection that MDAV makes, or you discover a missed detection, you can submit a file to us at our [sample submission help site](/en-us/defender-xdr/submission-guide).

Before you begin, make sure you have:

- Windows 10 or later, or Windows Server 2016 or later.
- Devices onboarded to Microsoft Defender for Endpoint and managed through [Defender for Endpoint security settings management](/en-us/intune/intune-service/protect/mde-security-integration). The devices don't need to be enrolled in Microsoft Intune.
- The licenses, permissions, and setup described in [Prerequisites for managing endpoint security policies](endpoint-security-policies-configure#prerequisites).

## Configure evaluation policies

Create separate endpoint security policies for Microsoft Defender Antivirus settings, ASR rules, and tamper protection. For the complete steps to create, assign, save, edit, and verify policies, see [Create an endpoint security policy](endpoint-security-policies-configure#create-an-endpoint-security-policy) and [Edit an endpoint security policy](endpoint-security-policies-configure#edit-an-endpoint-security-policy).

Microsoft Defender Antivirus indicates a detection through [standard Windows notifications](configure-notifications-microsoft-defender-antivirus). You can also [review Microsoft Defender Antivirus scan results](review-scan-results-microsoft-defender-antivirus).

The Windows event log also records detection and engine events. For a list of event IDs and their corresponding actions, see [Review event logs and error codes to troubleshoot issues with Microsoft Defender Antivirus](troubleshoot-microsoft-defender-antivirus).

### Configure Microsoft Defender Antivirus settings

To configure the antivirus evaluation settings, use a **Microsoft Defender Antivirus** policy.

When you create the policy on the **Windows policies** tab of the **Endpoint security policies** page in the Defender portal at https://security.microsoft.com/policy-inventory?osPlatform=Windows, use these specific settings:

- **Select platform**: Select **Windows**.
- **Select template**: Select **Microsoft Defender Antivirus**.

When you create or modify the policy, configure the following evaluation settings on the **Configuration settings** tab:

- **Real-time Protection**:

    | Setting | Value |
    | --- | --- |
    | Allow Realtime Monitoring | Allowed. Turns on and runs the real-time monitoring service (default). |
    | Real Time Scan Direction | Monitor all files (bi-directional) (default). |
    | Allow Behavior Monitoring | Allowed. Turns on real-time behavior monitoring (default). |
    | Allow On Access Protection | Allowed (default). |
    | PUA Protection | PUA Protection on. Detected items are blocked. They appear in history along with other threats. |
- **Cloud protection features**:

    | Setting | Value |
    | --- | --- |
    | Allow Cloud Protection | Allowed. Turns on cloud protection (default). |
    | Cloud Block Level | High |
    | Cloud Extended Timeout | Configured, 50 |
    | Submit Samples Consent | Send all samples automatically |

    Standard security intelligence updates can take hours to prepare and deliver. Microsoft cloud-delivered protection can deliver updated protection against emerging threats in seconds. For more information, see [Use next-gen technologies in Microsoft Defender Antivirus through cloud-delivered protection](cloud-protection-microsoft-defender-antivirus).
- **Scans**:

    | Setting | Value |
    | --- | --- |
    | Allow Email Scanning | Allowed. Turns on email scanning. |
    | Allow scanning of all downloaded files and attachments | Allowed (default). |
    | Allow Script Scanning | Allowed (default). |
    | Allow Archive Scanning | Allowed. Scans archive files (default). |
    | Allow Scanning Network Files | Allowed. Scans network files (default). |
    | Allow Full Scan Removable Drive Scanning | Allowed. Scans removable drives. |
- **Network Protection**:

    | Setting | Value |
    | --- | --- |
    | Enable Network Protection | Enabled (block mode) |
    | Allow Network Protection Down Level | Network protection will be enabled downlevel. |
    | Allow Datagram Processing On Win Server | Datagram processing on Windows Server is disabled (default). |
    | Disable DNS over TCP parsing | DNS over TCP parsing is enabled (default). |
    | Disable HTTP parsing | HTTP parsing is enabled (default). |
    | Disable SSH parsing | SSH parsing is enabled (default). |
    | Disable TLS parsing | TLS parsing is enabled (default). |

    Note

    Keep **Allow Datagram Processing On Win Server** disabled on server roles with high UDP traffic. Enabling this setting can affect network performance and reliability. For more information, see [Configure network protection in Microsoft Defender Antivirus](enable-network-protection).
- **Security Intelligence updates**:

    | Setting | Value |
    | --- | --- |
    | Signature Update Interval | Configured, 4 |
    | Signature Update Fallback Order | 1. Select **Add** for as many fallback sources as you want to specify.<br>    2. Enter one of the following values in each box in the order you want:<br>        - `InternalDefinitionUpdateServer`: Your own WSUS server with Microsoft Defender Antivirus updates allowed.<br>        - `MicrosoftUpdateServer`: Microsoft Update.<br>        - `MMPC`: `https://www.microsoft.com/wdsi/definitions`<br><br>To remove a fallback source (populated or empty), select the check box next to the box, and then select **Remove**. |
- **Local administrator AV**:

    Prevent local administrators from changing Microsoft Defender Antivirus settings such as exclusions. Manage the settings through Defender for Endpoint security settings management.

    | Setting | Value |
    | --- | --- |
    | Disable Local Admin Merge | Disable Local Admin Merge |
- **Threat severity default action**:

    | Setting | Value |
    | --- | --- |
    | Remediation action for High severity threats | Quarantine. Move files to quarantine. |
    | Remediation action for Severe threats | Quarantine. Move files to quarantine. |
    | Remediation action for Low severity threats | Quarantine. Move files to quarantine. |
    | Remediation action for Moderate severity threats | Quarantine. Move files to quarantine. |
- **Quarantine options**:

    | Setting | Value |
    | --- | --- |
    | Days to Retain Cleaned Malware | Configured, 60 |
    | Allow User UI Access | Allowed. Lets users access the UI (default). |

### Configure attack surface reduction rules

To configure the ASR rule evaluation settings, use an **Attack Surface Reduction Rules** policy. For more information about ASR rules, see [ASR rules](attack-surface-reduction-rules-overview#asr-rules).

For information about the available rule actions, see [Modes for ASR rules](attack-surface-reduction-rules-overview#modes-for-asr-rules).

When you create the policy on the **Windows policies** tab of the **Endpoint security policies** page in the Defender portal at https://security.microsoft.com/policy-inventory?osPlatform=Windows, use these specific settings:

- **Select platform**: Select **Windows**.
- **Select template**: Select **Attack Surface Reduction Rules**.

When you create or modify the policy, configure the following evaluation settings on the **Configuration settings** tab:

| Setting | Value |
| --- | --- |
| Block executable content from email client and webmail | Audit |
| Block Adobe Reader from creating child processes | Audit |
| Block execution of potentially obfuscated scripts | Audit |
| Block abuse of exploited vulnerable signed drivers (Device) | Audit |
| Block Win32 API calls from Office macros | Audit |
| Block executable files from running unless they meet a prevalence, age, or trusted list criterion | Audit |
| Block Office communication application from creating child processes | Audit |
| Block all Office applications from creating child processes | Audit |
| Block use of copied or impersonated system tools | Audit |
| Block JavaScript or VBScript from launching downloaded executable content | Audit |
| Block credential stealing from the Windows local security authority subsystem | Audit |
| Block Webshell creation for Servers | Audit |
| Block Office applications from creating executable content | Audit |
| Block untrusted and unsigned processes that run from USB | Audit |
| Block Office applications from injecting code into other processes | Audit |
| Block persistence through WMI event subscription | Audit |
| Use advanced protection against ransomware | Audit |
| Block process creations originating from PSExec and WMI commands | Audit |
| Block rebooting machine in Safe Mode | Audit |
| Enable Controlled Folder Access | Audit Mode |

Tip

If audit events identify behavior that's acceptable in your organization, add an **Attack Surface Reduction Only Exclusions** per-rule exclusion. For more information, see [File and folder exclusions for ASR rules](attack-surface-reduction-rules-overview#file-and-folder-exclusions-for-asr-rules).

Review the audit events before you enable ASR rules or controlled folder access in block mode. For more information, see [Test your ASR rules deployment](attack-surface-reduction-rules-deployment-test).

### Configure tamper protection

To configure tamper protection, use a **Windows Security Experience** policy.

When you create the policy on the **Windows policies** tab of the **Endpoint security policies** page in the Defender portal at https://security.microsoft.com/policy-inventory?osPlatform=Windows, use these specific settings:

- **Select platform**: Select **Windows**.
- **Select template**: Select **Windows Security Experience**.

When you create or modify the policy, use this specific setting on the **Configuration settings** tab:

| Setting | Value |
| --- | --- |
| Tamper Protection (Device) | Tamper Protection (On) |

## Validate Microsoft Defender Antivirus protection

Use the following procedures to verify cloud connectivity and update versions on the evaluation devices.

### Check cloud protection network connectivity

Cloud protection uses cloud-based machine learning and analysis to provide faster threat detection. The device must be able to reach Microsoft cloud-delivered protection for this feature to work correctly.

The following procedure applies to Windows 10 or later and Windows Server 2019 or later.

Run the following commands in an elevated Command Prompt (a Command Prompt window you opened by selecting **Run as administrator**):

Tip

The first command changes the directory to the latest version of &lt;antimalware platform version&gt; in `%ProgramData%\Microsoft\Windows Defender\Platform\<antimalware platform version>`. If that path doesn't exist, it goes to `%ProgramFiles%\Windows Defender`.

```dos
(set "_done=" & if exist "%ProgramData%\Microsoft\Windows Defender\Platform\" (for /f "delims=" %d in ('dir "%ProgramData%\Microsoft\Windows Defender\Platform" /ad /b /o:-n 2^>nul') do if not defined _done (cd /d "%ProgramData%\Microsoft\Windows Defender\Platform\%d" & set _done=1)) else (cd /d "%ProgramFiles%\Windows Defender")) >nul 2>&1

MpCmdRun.exe -ValidateMapsConnection
```

For more information, see [Configure and manage Microsoft Defender Antivirus with the MpCmdRun command-line tool](command-line-arguments-microsoft-defender-antivirus).

### Check the platform update version

Run the following command in an elevated PowerShell session to display the Microsoft Defender Antivirus platform version installed on the device:

```powershell
Get-MPComputerStatus | Format-Table AMProductVersion
```

Compare the output with the latest production channel version in the [Microsoft Update Catalog](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4052623).

### Check the security intelligence update version

Run the following command in an elevated PowerShell session to display the security intelligence version installed on the device:

```powershell
Get-MPComputerStatus | Format-Table AntivirusSignatureVersion
```

Compare the output with the **Security intelligence update** version on the [Microsoft Defender Antivirus security intelligence and product updates](https://www.microsoft.com/wdsi/defenderupdates) page.

### Check the engine update version

Run the following command in an elevated PowerShell session to display the Microsoft Defender Antivirus engine version installed on the device:

```powershell
Get-MPComputerStatus | Format-Table AMEngineVersion
```

Compare the output with the **Engine version** on the [Microsoft Defender Antivirus security intelligence and product updates](https://www.microsoft.com/wdsi/defenderupdates) page.

If you find that your settings aren't taking effect, you might have a conflict. For information on how to resolve conflicts, see [Troubleshoot Microsoft Defender Antivirus settings](troubleshoot-settings).

## Submit missed detections

If Microsoft Defender Antivirus doesn't detect a malicious file or activity during your evaluation, submit the undetected file to Microsoft for analysis:

- [Submit files in Microsoft Defender for Endpoint](admin-submissions-mde) if you have Microsoft Defender, Microsoft Defender for Endpoint P2/P1, or Microsoft Defender for Business.
- [Submit files for analysis](/en-us/defender-xdr/submission-guide) if you have Microsoft Defender Antivirus.