---
layout: Conceptual
title: Evaluate Microsoft Defender Antivirus using Group Policy - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/evaluate-mdav-using-gp
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use this guide to evaluate and test the protection offered by Microsoft Defender Antivirus using Group Policy.
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
document_id: 076121fc-e5af-3d4f-ac8a-acd0aeb82208
document_version_independent_id: 076121fc-e5af-3d4f-ac8a-acd0aeb82208
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/evaluate-mdav-using-gp.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: evaluate-mdav-using-gp
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/evaluate-mdav-using-gp.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 92260a46-965e-88b6-5698-30b1244e7f80
---

# Evaluate Microsoft Defender Antivirus using Group Policy - Microsoft Defender for Endpoint | Microsoft Learn

This guide helps you turn on and test key protection features in Microsoft Defender Antivirus and Microsoft Defender Exploit Guard. These features include real-time protection, cloud-delivered protection, scan settings, network protection, attack surface reduction rules, and controlled folder access. This guide applies to current versions of Windows and Windows Server. Use the Group Policy settings in this guide to set up these features for evaluation in domain-joined or workgroup environments.

## Prerequisites

### Supported operating systems

The following operating systems are supported for this evaluation:

- Windows 10 or later
- Windows Server 2016 or later

## Use Group Policy to enable Microsoft Defender Antivirus features

A [Group Policy Central Store](/en-us/troubleshoot/windows-client/group-policy/create-and-manage-central-store) is a shared folder on a domain controller that holds Administrative Template files (.admx and .adml). It lets all Group Policy administrators use the same policy definitions. For domain environments, set up a Central Store before you begin. For workgroups, the templates are stored locally and no Central Store is needed.

Use the following steps to configure Microsoft Defender Antivirus for evaluation.

1. Download the latest Administrative Template files. For download links, see [Administrative Templates files by operating system version](/en-us/troubleshoot/windows-client/group-policy/create-and-manage-central-store#links-to-download-the-administrative-templates-files-based-on-the-operating-system-version).

    Tip

    Check the **System Requirements** section on the individual download pages:

    - Most downloads support Windows clients and Windows servers.
    - Get the latest available and applicable download.
2. Do one of the following procedures to create a Central Store to host the latest .admx and .adml templates:

    - **Domains**:

        1. Create a new OU to block policy inheritance.
        2. Open the Group policy Management Console (gpmc.msc).
        3. Go to **Group Policy Objects** and create a new group policy.
        4. Right-click on the new group policy and then select **Edit**.
        5. Go to **Computer Configuration** &gt; **Policies** &gt; **Administrative Templates** &gt; **Windows Components** &gt; **Microsoft Defender Antivirus**.
    - **Workgroups**:

        1. Open the Group Policy Editor (gpedit.msc).
        2. Go to **Computer Configuration** &gt; **Administrative Templates** &gt; **Windows Components** &gt; **Microsoft Defender Antivirus**.

For more information about creating and managing a Group Policy Central Store, see [Create and manage Central Store - Windows Client](/en-us/troubleshoot/windows-client/group-policy/create-and-manage-central-store#the-central-store).

## Evaluate potentially unwanted application protection in Microsoft Defender Antivirus

**Root**:

| Description | Setting |
| --- | --- |
| Turn off Microsoft Defender Antivirus | Disabled |
| Configure detection for potentially unwanted applications | Enabled - Block |

## Real-time protection (always-on protection, real-time scanning)

**Real-time protection**:

| Description | Setting |
| --- | --- |
| Turn off real-time protection | Disabled |
| Configure monitoring for incoming and outgoing file and program activity | Enabled, bi-directional (full on-access) |
| Turn on Behavior Monitoring | Enabled |
| Monitor file and program activity on your computer | Enabled |

## Cloud protection features

Standard security intelligence updates can take hours to prepare and deliver. Cloud-delivered protection can provide the same coverage in seconds.

For more information, see [Use next-gen technologies in Microsoft Defender Antivirus through cloud-delivered protection](/en-us/windows/threat-protection/windows-defender-antivirus/utilize-microsoft-cloud-protection-windows-defender-antivirus).

Configure the following settings under **MAPS** (Microsoft Active Protection Service), which is the cloud-based service that sends threat data to Microsoft and receives rapid protection updates:

| Description | Setting |
| --- | --- |
| Join Microsoft MAPS | Enabled, Advanced MAPS |
| Configure the 'Block at First Sight' feature | Enabled |
| Send file samples when further analysis is required | Enabled, Send all samples |

**MpEngine**:

| Description | Setting |
| --- | --- |
| Select cloud protection level | Enabled, High blocking level |
| Configure extended cloud check | Enabled, 50 |

## Configure and evaluate scan settings

These scan settings control how files and scripts are checked. Turn on each setting in Group Policy:

| Description | Setting |
| --- | --- |
| Turn on Heuristics | Enabled |
| Turn on e-mail scanning | Enabled |
| Scan all downloaded files and attachments | Enabled |
| Turn on script scanning | Enabled |
| Scan archive files | Enabled |
| Scan packed executables | Enabled |
| Configure scanning of network files (Scan Network Files) | Enabled |
| Scan removable drives | Enabled |
| Turn on reparse point scanning | Enabled |

## Security Intelligence updates

Use these settings to control how the device downloads and applies security updates:

| Description | Setting |
| --- | --- |
| Specify the interval to check for security intelligence updates | Enabled, 4 |
| Define the order of sources for downloading security intelligence updates | Enabled, under 'Define the order of sources for downloading security intelligence updates' <br>- `InternalDefinitionUpdateServer`: WSUS with Microsoft Defender Antivirus updates allowed.<br>- `MicrosoftUpdateServer`: Microsoft Update (formerly Windows Update).<br>- `MMPC`: https://www.microsoft.com/wdsi/defenderupdates |

## Disable local administrator AV settings

Use these settings to block local admin changes like exclusions. The policies are enforced through Microsoft Defender for Endpoint Security Settings Management.

**Root**:

| Description | Setting |
| --- | --- |
| Configure local administrator merge behavior for lists | Disabled |
| Control whether or not exclusions are visible to local admins | Enabled |

## Configure threat severity default actions

These settings control what happens when Microsoft Defender Antivirus finds a threat. They replace the default action at each threat level and quarantine all threats.

**Threats**:

| Description | Setting | Alert level | Action |
| --- | --- | --- | --- |
| Specify threat alert levels at which default action shouldn't be taken when detected | Enabled |  |  |
|  |  | 5 (Severe) | 2 (Quarantine) |
|  |  | 4 (High) | 2 (Quarantine) |
|  |  | 2 (Medium) | 2 (Quarantine) |
|  |  | 1 (Low) | 2 (Quarantine) |

**Quarantine**:

| Description | Setting |
| --- | --- |
| Configure removal of items from Quarantine folder | Enabled, 60 |

**Client Interface**:

| Description | Setting |
| --- | --- |
| Enable headless UI mode | Disabled |

## Configure network protection

Network protection blocks connections to dangerous websites and IP addresses. It helps prevent phishing attacks and malware downloads. Configure the following settings under **Microsoft Defender Exploit Guard\Network Protection** in Group Policy:

| Description | Setting |
| --- | --- |
| Prevent users and apps from accessing dangerous websites | Enabled, Block |
| Allow Network Protection on Windows Server | Enabled |

On Windows Server, use PowerShell to turn on Network Protection:

| OS | PowerShell command |
| --- | --- |
| Windows Server 2012 R2 and later | `Set-MpPreference -AllowNetworkProtectionOnWinServer $true` |
| Windows Server 2016 and Windows Server 2012 R2 [unified MDE client](update-agent-mma-windows#upgrade-to-the-new-agent-for-defender-for-endpoint) | `Set-MpPreference -AllowNetworkProtectionOnWinServer $true -AllowNetworkProtectionDownLevel $true` |

## Configure attack surface reduction rules

Attack surface reduction (ASR) rules block specific behaviors that malware often uses, such as running scripts or launching executable content from email. Use the following steps to enable ASR rules in Group Policy:

1. In the Group Policy Editor, go to **Computer Configuration** &gt; **Administrative Templates** &gt; **Windows Components** &gt; **Microsoft Defender Antivirus** &gt; **Microsoft Defender Exploit Guard** &gt; **Attack Surface Reduction**.
2. Double-click **Configure Attack Surface Reduction rules**, select **Enabled**, and then select **Show** to configure each rule with the values in the following table.

| Value name | ASR rule name | Value |
| --- | --- | --- |
| 01443614-cd74-433a-b99e-2ecdc07bfc25 | [Block executable files from running unless they meet a prevalence, age, or trusted list criterion](attack-surface-reduction-rules-reference#block-executable-files-from-running-unless-they-meet-a-prevalence-age-or-trusted-list-criterion) | 1 (Block) |
| 26190899-1602-49e8-8b27-eb1d0a1ce869 | [Block Office communication application from creating child processes](attack-surface-reduction-rules-reference#block-office-communication-application-from-creating-child-processes) | 1 (Block) |
| 33ddedf1-c6e0-47cb-833e-de6133960387 | [Block rebooting machine in Safe Mode](attack-surface-reduction-rules-reference#block-rebooting-machine-in-safe-mode) | 1 (Block) |
| 3b576869-a4ec-4529-8536-b80a7769e899 | [Block Office applications from creating executable content](attack-surface-reduction-rules-reference#block-office-applications-from-creating-executable-content) | 1 (Block) |
| 56a863a9-875e-4185-98a7-b882c64b5ce5 | [Block abuse of exploited vulnerable signed drivers (Device)](attack-surface-reduction-rules-reference#block-abuse-of-exploited-vulnerable-signed-drivers-device) | 1 (Block) |
| 5beb7efe-fd9a-4556-801d-275e5ffc04cc | [Block execution of potentially obfuscated scripts](attack-surface-reduction-rules-reference#block-execution-of-potentially-obfuscated-scripts) | 1 (Block) |
| 75668c1f-73b5-4cf0-bb93-3ecf5cb7cc84 | [Block Office applications from injecting code into other processes](attack-surface-reduction-rules-reference#block-office-applications-from-injecting-code-into-other-processes) | 1 (Block) |
| 7674ba52-37eb-4a4f-a9a1-f0f9a1619a2c | [Block Adobe Reader from creating child processes](attack-surface-reduction-rules-reference#block-adobe-reader-from-creating-child-processes) | 1 (Block) |
| 92e97fa1-2edf-4476-bdd6-9dd0b4dddc7b | [Block Win32 API calls from Office macros](attack-surface-reduction-rules-reference#block-win32-api-calls-from-office-macros) | 1 (Block) |
| 9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2 | [Block credential stealing from the Windows local security authority subsystem](attack-surface-reduction-rules-reference#block-credential-stealing-from-the-windows-local-security-authority-subsystem) | 1 (Block) |
| a8f5898e-1dc8-49a9-9878-85004b8a61e6 | [Block Webshell creation for Servers](attack-surface-reduction-rules-reference#block-webshell-creation-for-servers) | 1 (Block) |
| b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4 | [Block untrusted and unsigned processes that run from USB](attack-surface-reduction-rules-reference#block-untrusted-and-unsigned-processes-that-run-from-usb) | 1 (Block) |
| be9ba2d9-53ea-4cdc-84e5-9b1eeee46550 | [Block executable content from email client and webmail](attack-surface-reduction-rules-reference#block-executable-content-from-email-client-and-webmail) | 1 (Block) |
| c0033c00-d16d-4114-a5a0-dc9b3a7d2ceb | [Block use of copied or impersonated system tools](attack-surface-reduction-rules-reference#block-use-of-copied-or-impersonated-system-tools) | 1 (Block) |
| c1db55ab-c21a-4637-bb3f-a12568109d35 | [Use advanced protection against ransomware](attack-surface-reduction-rules-reference#use-advanced-protection-against-ransomware) | 1 (Block) |
| d1e49aac-8f56-4280-b9ba-993a6d77406c | [Block process creations originating from PSExec and WMI commands](attack-surface-reduction-rules-reference#block-process-creations-originating-from-psexec-and-wmi-commands) | 1 (Block)^\*^ |
| d3e037e1-3eb8-44c8-a917-57927947596d | [Block JavaScript or VBScript from launching downloaded executable content](attack-surface-reduction-rules-reference#block-javascript-or-vbscript-from-launching-downloaded-executable-content) | 1 (Block) |
| d4f940ab-401b-4efc-aadc-ad5f3c50688a | [Block all Office applications from creating child processes](attack-surface-reduction-rules-reference#block-all-office-applications-from-creating-child-processes) | 1 (Block) |
| e6db77e5-3df2-4cf1-b95a-636979351e5b | [Block persistence through WMI event subscription](attack-surface-reduction-rules-reference#block-persistence-through-wmi-event-subscription) | 1 (Block) |

^\*^ If you use Microsoft Configuration Manager (formerly known as Microsoft Endpoint Configuration Manager and Microsoft System Center Configuration Manager) or other management tools that use WMI, use the value 2 (Audit). The Configuration Manager client relies heavily on WMI.

Tip

Some rules might block behavior you find acceptable in your organization. In these cases, change the rule from 1 (Block) to 2 (Audit) to prevent unwanted blocks.

## Configure Controlled Folder Access

Controlled Folder Access guards your data from harmful apps and ransomware. To turn it on, go to **Computer Configuration** &gt; **Administrative Templates** &gt; **Windows Components** &gt; **Microsoft Defender Antivirus** &gt; **Microsoft Defender Exploit Guard** &gt; **Attack Surface Reduction**.

| Description | Setting |
| --- | --- |
| Configure Controlled Folder Access | Enabled, Block |

Assign the policies to the OU where the test machines are located.

### Enable Tamper Protection

In the [Microsoft Defender portal](https://security.microsoft.com), go to **Settings** &gt; **Endpoints** &gt; **Advanced features** &gt; **Tamper Protection** &gt; **On**.

For more information, see [How do I configure or manage tamper protection?](tamper-protection-overview).

## Check the Cloud Protection network connectivity

Verify that Microsoft Defender Antivirus cloud protection network connectivity is working before you test detections or protections.

To test connectivity to Microsoft Defender cloud protection services, run the following commands in an elevated Command Prompt (right-click Command Prompt and select **Run as administrator**). The first command changes to the latest Defender platform folder, and the second command validates the MAPS cloud connection. A successful result displays `ValidateMapsConnection successfully established a connection to MAPS`:

Tip

The first command changes the directory to the latest version of &lt;antimalware platform version&gt; in `%ProgramData%\Microsoft\Windows Defender\Platform\<antimalware platform version>`. If that path doesn't exist, it goes to `%ProgramFiles%\Windows Defender`.

```dos
(set "_done=" & if exist "%ProgramData%\Microsoft\Windows Defender\Platform\" (for /f "delims=" %d in ('dir "%ProgramData%\Microsoft\Windows Defender\Platform" /ad /b /o:-n 2^>nul') do if not defined _done (cd /d "%ProgramData%\Microsoft\Windows Defender\Platform\%d" & set _done=1)) else (cd /d "%ProgramFiles%\Windows Defender")) >nul 2>&1

MpCmdRun.exe -ValidateMapsConnection
```

The first command finds the newest antimalware platform folder under `%ProgramData%\Microsoft\Windows Defender\Platform\` and changes to that directory. If that path doesn't exist, it falls back to `%ProgramFiles%\Windows Defender`. The second command validates cloud protection connectivity.

For more information about MpCmdRun.exe and the `-ValidateMapsConnection` option, see [Configure and manage Microsoft Defender Antivirus with the MpCmdRun command-line tool](command-line-arguments-microsoft-defender-antivirus).

## Check the Platform Update version

Check the latest 'Platform Update' version for the Production channel (GA) in the Microsoft Update Catalog, then compare it with the version on your device:

[Microsoft Update Catalog](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4052623)

To check the platform version on your device, run this command in an elevated PowerShell session (open PowerShell by selecting **Run as administrator**). The `AMProductVersion` value in the output is the installed platform version:

```powershell
Get-MpComputerStatus | Format-Table AMProductVersion
```

## Check the Security Intelligence Update version

Check the latest 'Security Intelligence Update' version on the Microsoft Security Intelligence updates page, then compare it with the version on your device:

[Latest security intelligence updates for Microsoft Defender Antivirus and other Microsoft anti-malware - Microsoft Security Intelligence](https://www.microsoft.com/wdsi/defenderupdates)

To verify the installed security intelligence version, run this command in an elevated PowerShell session. Compare the `AntivirusSignatureVersion` value in the output with the latest version on the page above:

```powershell
Get-MpComputerStatus | Format-Table AntivirusSignatureVersion
```

## Check the Engine Update version

Check the latest scan 'engine update' version on the Microsoft Security Intelligence updates page, then compare it with the version on your device:

[Latest security intelligence updates for Microsoft Defender Antivirus and other Microsoft anti-malware - Microsoft Security Intelligence](https://www.microsoft.com/wdsi/defenderupdates)

The scan engine is updated separately from the platform. To check the installed engine version, run this command in an elevated PowerShell session:

```powershell
Get-MpComputerStatus | Format-Table AMEngineVersion
```

If your settings don't take effect, you might have a conflict. To resolve conflicts, see [Troubleshoot Microsoft Defender Antivirus settings](troubleshoot-settings).

## Submit files for false negative analysis

If you have any questions about a detection that Microsoft Defender AV makes, or you discover a missed detection, you can submit a file to us.

If you have Microsoft Defender, Microsoft Defender for Endpoint P2/P1, or Microsoft Defender for Business: refer [Submit files in Microsoft Defender for Endpoint](admin-submissions-mde).

If you have Microsoft Defender Antivirus, see [Submit files for analysis](/en-us/defender-xdr/submission-guide).

Microsoft Defender AV indicates a detection through [standard Windows notifications](configure-notifications-microsoft-defender-antivirus). You can also [review detections in the Microsoft Defender AV app](review-scan-results-microsoft-defender-antivirus).

The Windows event log also records detection and engine events. See the [Microsoft Defender Antivirus events article for a list of event IDs](troubleshoot-microsoft-defender-antivirus) and their corresponding actions.

If your settings aren't applied properly, find out if there are conflicting policies that are enabled in your environment. For more information, see [Troubleshoot Microsoft Defender Antivirus settings](troubleshoot-settings).

If you need to open a Microsoft support case: [Contact Microsoft Defender for Endpoint support](contact-support).