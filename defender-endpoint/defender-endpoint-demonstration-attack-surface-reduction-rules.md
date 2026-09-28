---
layout: Conceptual
title: Microsoft Defender for Endpoint attack surface reduction rules demonstrations - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/defender-endpoint-demonstration-attack-surface-reduction-rules
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to test and demonstrate attack surface reduction (ASR) rules in Microsoft Defender for Endpoint by using test files, scripts, and procedures.
ms.service: defender-endpoint
ms.author: chrisda
author: chrisda
ms.reviewer: yongrhee
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- demo
ms.topic: how-to
ms.subservice: asr
ms.custom: msecd-doc-authoring-1015
ms.date: 2026-08-12T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 5c449c70-0017-abab-c56a-3e7971c23413
document_version_independent_id: 5c449c70-0017-abab-c56a-3e7971c23413
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/defender-endpoint-demonstration-attack-surface-reduction-rules.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-endpoint-demonstration-attack-surface-reduction-rules
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/defender-endpoint-demonstration-attack-surface-reduction-rules.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bba62c59-6b53-4be4-8b9d-6624f9184c22
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f3a81ffb-ee36-4ec7-b54a-01b6681aff65
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: d94cd0ad-17e3-b573-04ef-b7f1dba08428
---

# Microsoft Defender for Endpoint attack surface reduction rules demonstrations - Microsoft Defender for Endpoint | Microsoft Learn

Use the test files, scripts, and procedures in this article to demonstrate specific attack surface reduction (ASR) rules in Microsoft Defender for Endpoint.

ASR rules target risky software behavior on Windows devices that attackers commonly exploit through malware (for example, launching scripts that download files, running obfuscated scripts, and injecting code into other processes). For more information about ASR rules, see [Attack surface reduction (ASR) rules overview](attack-surface-reduction-rules-overview).

Important

The scripts and test files in this article intentionally simulate malicious behavior, so Microsoft Defender Antivirus and Windows Security detect them (for example, as `Trojan:Win32/Vigorf.A`) and might block, quarantine, or delete them. Use these files only on a test device, and exclude the download folder before you download the files. Even with a folder exclusion, your browser or Microsoft Defender SmartScreen might still warn you when you download the scripts or `ASRSamplesAll.zip`. The exclusion applies only after the files reach the folder, so you might need to choose **Keep** (or the equivalent allow option) to complete the download.

## Prerequisites

Before you begin, make sure your test device meets the following requirements:

- Windows 10, version 1709 (October 2017) or later.
- Microsoft Defender Antivirus enabled and in active mode.

For the full list of requirements, supported operating systems, and modes, see [Attack surface reduction (ASR) rules overview](attack-surface-reduction-rules-overview#requirements-for-asr-rules). For the methods you can use to enable ASR rules, see [Deployment and configuration methods for ASR rules](attack-surface-reduction-rules-overview#deployment-and-configuration-methods-for-asr-rules).

## Set up the demonstration

Important

The setup script and the mode scripts enable the demonstration ASR rules in **Enabled** (block) mode. To see the current state of the ASR rules before you start, run the following command in an elevated PowerShell window (a PowerShell window you opened by selecting **Run as administrator**):

```powershell
$p = Get-MpPreference;0..([math]::Min($p.AttackSurfaceReductionRules_Ids.Count,$p.AttackSurfaceReductionRules_Actions.Count)-1) | % {[pscustomobject]@{Id=$p.AttackSurfaceReductionRules_Ids[$_];Action=$p.AttackSurfaceReductionRules_Actions[$_]}} | Format-Table -AutoSize
```

Note the rules and their [mode values](attack-surface-reduction-rules-overview#modes-for-asr-rules) so that you can restore them during cleanup when you're finished with the demonstration.

1. Before you run the setup script, allow it to run by setting the execution policy to `RemoteSigned` for the current session. Run the following command in an elevated PowerShell window:

    ```powershell
    Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned
    ```

    `RemoteSigned` is safer than `Unrestricted` because it still blocks unsigned scripts that are downloaded from the internet, and the `Process` scope reverts the change when you close the session.

    Tip

    Because the setup script is unsigned, `RemoteSigned` blocks it if the script still carries the "downloaded from the internet" mark (the mark-of-the-web). If that happens, confirm that the script is from a trusted source, and then unblock it before you run it:

    ```powershell
    Unblock-File -Path "<path>\WindowsDefender_ASR_SetupScript.ps1"
    ```
2. Download and extract `WindowsDefender_ASR_SetupScript.ps1` from https://demo.wd.microsoft.com/Content/ASR_SetupScript.zip. The setup script automates the following steps:

    - Removes `c:\demo` from the controlled folder access (CFA) protected folders list to reset any previous demonstration configuration (without affecting your other protected folders).
    - Creates the `c:\demo` folder and adds it to the Microsoft Defender Antivirus exclusion list (without affecting your other exclusions).
    - Downloads a clean test file (`testfile_safe.txt`) to `c:\demo`, and downloads and extracts the ASR test files (`ASRSamplesAll.zip`) to `c:\demo\ASRSamplesAll`. The `ASRSamplesAll.zip`package contains these test files:
        - `ransomware_testfile_doc.docm` (also available directly at https://demo.wd.microsoft.com/Content/ransomware_testfile_doc.docm)
        - `ransomware_testfile_exe.exe` (also available directly at https://demo.wd.microsoft.com/Content/ransomware_testfile_exe.exe)
        - `TestFile_OfficeChildProcess_D4F940AB-401B-4EFC-AADC-AD5F3C50688A.docm` (also available directly at https://demo.wd.microsoft.com/Content/TestFile_OfficeChildProcess_D4F940AB-401B-4EFC-AADC-AD5F3C50688A.docm)
        - `TestFile_PsexecAndWMICreateProcess_D1E49AAC-8F56-4280-B9BA-993A6D77406C.vbs` (also available directly at https://demo.wd.microsoft.com/Content/TestFile_PsexecAndWMICreateProcess_D1E49AAC-8F56-4280-B9BA-993A6D77406C.vbs)
        - `TestFile_ScriptInternetContent_D3E037E1-3EB8-44C8-A917-57927947596D.js` (also available directly at https://demo.wd.microsoft.com/Content/TestFile_ScriptInternetContent_D3E037E1-3EB8-44C8-A917-57927947596D.js)
        - `TestFile_ScriptObfuscatedContent_5BEB7EFE-FD9A-4556-801D-275E5FFC04CC.js` (also available directly at https://demo.wd.microsoft.com/Content/TestFile_ScriptObfuscatedContent_5BEB7EFE-FD9A-4556-801D-275E5FFC04CC.js)
        - `UNSIGNED_ransomware_test_exe.exe` (also available directly at https://demo.wd.microsoft.com/Content/UNSIGNED_ransomware_test_exe.exe)
    - Enables the demonstration ASR rules in **Enabled** (block) mode.
    - Adds `c:\demo` to the CFA protected folders list (without affecting your other protected folders).

    Important

    The setup script adds `c:\demo` to the Microsoft Defender Antivirus exclusion list. Don't run ASR test files from `c:\demo` or one of its subfolders when you're testing for an ASR block or detection. ASR rules that honor Microsoft Defender Antivirus exclusions, including **Use advanced protection against ransomware**, might not generate the expected block or detection. Before you run a test file, copy it to a folder that isn't excluded from Microsoft Defender Antivirus or ASR rules. For more information, see [File and folder exclusions for ASR rules](attack-surface-reduction-rules-overview#file-and-folder-exclusions-for-asr-rules).

    The setup and cleanup scripts adjust CFA because they're shared with the [CFA block app](defender-endpoint-demonstration-controlled-folder-access-block-app) and [CFA ransomware](defender-endpoint-demonstration-controlled-folder-access-ransomware) demonstrations. None of the ASR rule scenarios in this article use CFA. The setup script adds `c:\demo` to the CFA protected folders list but doesn't enable CFA, so the entry has no effect on this demonstration. The cleanup script disables CFA, so before you run the setup script, check your current [CFA mode](controlled-folder-access-overview#modes-for-cfa) and note the value so that you can restore it in the Clean up the demonstration section:

    ```powershell
    Get-MpPreference | Format-List EnableControlledFolderAccess
    ```

    Or, you can do the following manual steps instead:

    1. Create the folder `c:\demo`.
    2. Add `c:\demo` to the Microsoft Defender Antivirus exclusion list so that real-time protection doesn't quarantine the test files while you download and extract them. Run the following command in an elevated PowerShell window:

        ```powershell
        Add-MpPreference -ExclusionPath C:\demo
        ```
    3. Save the [clean test file](https://demo.wd.microsoft.com/Content/testfile_safe.txt) (`testfile_safe.txt`) in `c:\demo`.
    4. Download `ASRSamplesAll.zip` from https://demo.wd.microsoft.com/Content/ASRSamplesAll.zip and extract it to `c:\demo\ASRSamplesAll`.
    5. Enable the demonstration ASR rules in **Enabled** (block) mode by running the following command in an elevated PowerShell window:

        ```powershell
        Add-MpPreference -AttackSurfaceReductionRules_Ids 01443614-cd74-433a-b99e-2ecdc07bfc25,3b576869-a4ec-4529-8536-b80a7769e899,5beb7efe-fd9a-4556-801d-275e5ffc04cc,75668c1f-73b5-4cf0-bb93-3ecf5cb7cc84,92e97fa1-2edf-4476-bdd6-9dd0b4dddc7b,b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4,be9ba2d9-53ea-4cdc-84e5-9b1eeee46550,c1db55ab-c21a-4637-bb3f-a12568109d35,d1e49aac-8f56-4280-b9ba-993a6d77406c,d3e037e1-3eb8-44c8-a917-57927947596d,d4f940ab-401b-4efc-aadc-ad5f3c50688a -AttackSurfaceReductionRules_Actions Enabled,Enabled,Enabled,Enabled,Enabled,Enabled,Enabled,Enabled,Enabled,Enabled,Enabled
        ```

        The ASR rule names and associated GUID values are listed in the ASR rules in this demonstration section.
3. Download and extract the mode scripts from https://demo.wd.microsoft.com/Content/WindowsDefender_ASR_scripts.zip. The `WindowsDefender_ASR_Block.ps1`, `WindowsDefender_ASR_Audit.ps1`, and `WindowsDefender_ASR_Disabled.ps1` scripts switch the same demonstration ASR rules to **Enabled** (block), **AuditMode**, or **Disabled** mode, respectively. Run them to switch the demonstration ASR rules between **Enabled** (block), **AuditMode**, and **Disabled** modes during testing and cleanup.

    Note

    All three mode scripts display the same console message, `Enabling Exploit Guard ASR rules and setting to audit mode`, regardless of the mode they actually apply. This message is hardcoded and is incorrect for the `WindowsDefender_ASR_Block.ps1` and `WindowsDefender_ASR_Disabled.ps1` scripts. Rely on the script name, not the message, to confirm which mode you applied.

### ASR rules in this demonstration

The following table lists the ASR rules that this demonstration enables, their GUID values, and the test file that triggers each rule (where one is available). The setup script downloads several of these test files in `ASRSamplesAll.zip` and extracts them to `c:\demo\ASRSamplesAll`.

Tip

The **Rule name** links to the rule details. Some test files trigger more than one rule.

| GUID value | Rule name | Test files |
| --- | --- | --- |
| `01443614-cd74-433a-b99e-2ecdc07bfc25` | [Block executable files from running unless they meet a prevalence, age, or trusted list criterion](attack-surface-reduction-rules-reference#block-executable-files-from-running-unless-they-meet-a-prevalence-age-or-trusted-list-criterion) | None available |
| `3b576869-a4ec-4529-8536-b80a7769e899` | [Block Office applications from creating executable content](attack-surface-reduction-rules-reference#block-office-applications-from-creating-executable-content) | [TestFile_Block_Office_applications_from_creating_executable_content_3b576869-a4ec-4529-8536-b80a7769e899.docm](https://demo.wd.microsoft.com/Content/TestFile_Block_Office_applications_from_creating_executable_content_3b576869-a4ec-4529-8536-b80a7769e899.docm) |
| `5beb7efe-fd9a-4556-801d-275e5ffc04cc` | [Block execution of potentially obfuscated scripts](attack-surface-reduction-rules-reference#block-execution-of-potentially-obfuscated-scripts) | `TestFile_ScriptObfuscatedContent_5BEB7EFE-FD9A-4556-801D-275E5FFC04CC.js` in `ASRSamplesAll.zip` |
| `75668c1f-73b5-4cf0-bb93-3ecf5cb7cc84` | [Block Office applications from injecting code into other processes](attack-surface-reduction-rules-reference#block-office-applications-from-injecting-code-into-other-processes) | None available |
| `92e97fa1-2edf-4476-bdd6-9dd0b4dddc7b` | [Block Win32 API calls from Office macros](attack-surface-reduction-rules-reference#block-win32-api-calls-from-office-macros) | [Block_Win32_imports_from_Macro_code_in_Office_92e97fa1-2edf-4476-bdd6-9dd0b4dddc7b.docm](https://demo.wd.microsoft.com/Content/Block_Win32_imports_from_Macro_code_in_Office_92e97fa1-2edf-4476-bdd6-9dd0b4dddc7b.docm) |
| `b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4` | [Block untrusted and unsigned processes that run from USB](attack-surface-reduction-rules-reference#block-untrusted-and-unsigned-processes-that-run-from-usb) | `UNSIGNED_ransomware_test_exe.exe` in `ASRSamplesAll.zip` |
| `be9ba2d9-53ea-4cdc-84e5-9b1eeee46550` | [Block executable content from email client and webmail](attack-surface-reduction-rules-reference#block-executable-content-from-email-client-and-webmail)^\*^ | None available |
| `c1db55ab-c21a-4637-bb3f-a12568109d35` | [Use advanced protection against ransomware](attack-surface-reduction-rules-reference#use-advanced-protection-against-ransomware) | `ransomware_testfile_exe.exe` in `ASRSamplesAll.zip` |
| `d1e49aac-8f56-4280-b9ba-993a6d77406c` | [Block process creations originating from PSExec and WMI commands](attack-surface-reduction-rules-reference#block-process-creations-originating-from-psexec-and-wmi-commands) | `TestFile_PsexecAndWMICreateProcess_D1E49AAC-8F56-4280-B9BA-993A6D77406C.vbs` in `ASRSamplesAll.zip` |
| `d3e037e1-3eb8-44c8-a917-57927947596d` | [Block JavaScript or VBScript from launching downloaded executable content](attack-surface-reduction-rules-reference#block-javascript-or-vbscript-from-launching-downloaded-executable-content)^\*^ | `TestFile_ScriptInternetContent_D3E037E1-3EB8-44C8-A917-57927947596D.js` in `ASRSamplesAll.zip` |
| `d4f940ab-401b-4efc-aadc-ad5f3c50688a` | [Block all Office applications from creating child processes](attack-surface-reduction-rules-reference#block-all-office-applications-from-creating-child-processes) | `TestFile_OfficeChildProcess_D4F940AB-401B-4EFC-AADC-AD5F3C50688A.docm` in `ASRSamplesAll.zip` |

^\*^ In **Block** or **Warn** mode, EDR alerts and user notifications for this rule have extra [cloud protection level requirements](cloud-protection-microsoft-defender-antivirus) in Microsoft Defender Antivirus. For details, select the rule name to open its section in the [ASR rules reference](attack-surface-reduction-rules-reference).

Note

This demonstration doesn't enable or test the following ASR rules. Some of them can't be triggered by a sample file, such as **Block rebooting machine in Safe Mode**. For details about each rule, select its link:

- [Block abuse of exploited vulnerable signed drivers](attack-surface-reduction-rules-reference#block-abuse-of-exploited-vulnerable-signed-drivers-device) (`56a863a9-875e-4185-98a7-b882c64b5ce5`)
- [Block Adobe Reader from creating child processes](attack-surface-reduction-rules-reference#block-adobe-reader-from-creating-child-processes) (`7674ba52-37eb-4a4f-a9a1-f0f9a1619a2c`)
- [Block credential stealing from the Windows local security authority subsystem](attack-surface-reduction-rules-reference#block-credential-stealing-from-the-windows-local-security-authority-subsystem) (`9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2`)
- [Block Office communication application from creating child processes](attack-surface-reduction-rules-reference#block-office-communication-application-from-creating-child-processes) (`26190899-1602-49e8-8b27-eb1d0a1ce869`)
- [Block persistence through WMI event subscription](attack-surface-reduction-rules-reference#block-persistence-through-wmi-event-subscription) (`e6db77e5-3df2-4cf1-b95a-636979351e5b`)
- [Block rebooting machine in Safe Mode](attack-surface-reduction-rules-reference#block-rebooting-machine-in-safe-mode) (`33ddedf1-c6e0-47cb-833e-de6133960387`)
- [Block use of copied or impersonated system tools](attack-surface-reduction-rules-reference#block-use-of-copied-or-impersonated-system-tools) (`c0033c00-d16d-4114-a5a0-dc9b3a7d2ceb`)
- [Block Webshell creation for Servers](attack-surface-reduction-rules-reference#block-webshell-creation-for-servers) (`a8f5898e-1dc8-49a9-9878-85004b8a61e6`)

## Scenarios

Use the following scenarios to verify how the demonstration ASR rules behave in different modes.

### Scenario 1: All demonstration ASR rules block the test files

Do the following steps to confirm that all demonstration ASR rules block their corresponding test files:

1. Enable the demonstration ASR rules in **Block** mode. Run the `WindowsDefender_ASR_Block.ps1` script (see Set up the demonstration), or use the PowerShell command.
2. Before you open or run a test file, make sure the file is in a folder that isn't excluded from Microsoft Defender Antivirus or ASR rules. If you use a test file that the setup script extracted to `c:\demo\ASRSamplesAll`, copy it to a folder that isn't excluded. Don't run the test file from `c:\demo` or one of its subfolders. If prompted, enable editing and content.

You should immediately see an "Action blocked" notification.

### Scenario 2: An individual ASR rule blocks its matching test file

Use this scenario to test a single ASR rule and verify that it blocks its corresponding test file.

1. Configure the individual rule you want to test. For example, to enable the **Block all Office applications from creating child processes** rule, run the following command in an elevated PowerShell window:

    ```powershell
    Add-MpPreference -AttackSurfaceReductionRules_Ids d4f940ab-401b-4efc-aadc-ad5f3c50688a -AttackSurfaceReductionRules_Actions Enabled
    ```
2. Find the test file for the rule in the ASR rules in this demonstration table. Files marked *in `ASRSamplesAll.zip`* are already extracted to `c:\demo\ASRSamplesAll`.
3. Copy the test file to a folder that isn't excluded from Microsoft Defender Antivirus or ASR rules. Don't open or run the test file from `c:\demo` or one of its subfolders. For example, for the **Block all Office applications from creating child processes** rule, copy `TestFile_OfficeChildProcess_D4F940AB-401B-4EFC-AADC-AD5F3C50688A.docm` from `c:\demo\ASRSamplesAll` to a folder that isn't excluded.
4. Open or run the copied test file. If prompted, enable editing and content.

You should immediately see an "Action blocked" notification.

### Scenario 3: An ASR rule blocks an unsigned file that runs from a USB drive

Do the following steps to verify that the USB execution rule blocks an unsigned file.

1. Enable the **Block untrusted and unsigned processes that run from USB** ASR rule by running the following command in an elevated PowerShell window:

    ```powershell
    Add-MpPreference -AttackSurfaceReductionRules_Ids b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4 -AttackSurfaceReductionRules_Actions Enabled
    ```
2. Copy `UNSIGNED_ransomware_test_exe.exe` from `c:\demo\ASRSamplesAll` to a USB drive.
3. Run the file from the USB drive.

You should immediately see an "Action blocked" notification.

### Scenario 4: Without ASR rules, the ransomware test file encrypts files

Turn off the demonstration ASR rules to observe how the ransomware test file behaves when ASR rules are disabled.

1. Do either of the following steps to disable the ASR rules:
    - Run the `WindowsDefender_ASR_Disabled.ps1` script (see Set up the demonstration).
    - Use the `Add-MpPreference` PowerShell command to disable the rules (see Clean up the demonstration).
2. Run the ransomware test file (`ransomware_testfile_exe.exe`) from `c:\demo\ASRSamplesAll`.

As a result, the files in `c:\demo` are encrypted and you get a warning message.

Run the test file again to decrypt the files.

## Clean up the demonstration

If you ran the setup script, undo the demonstration by running the cleanup script:

Important

The cleanup script disables the demonstration ASR rules and two other ASR rules, even if you enabled some of those rules for other reasons. Before you run the script, check your current ASR rule states with the verification command in Set up the demonstration so that you can re-enable any rules you want to keep.

1. Download and extract the cleanup script `WindowsDefender_ASR_CFA_CleanupScript.ps1` from this ZIP file: https://demo.wd.microsoft.com/Content/ASR_CFA_CleanupScript.zip. The cleanup script does the following tasks:

    - Disables the demonstration ASR rules. The cleanup script also disables two more ASR rules that this demonstration doesn't enable:
        - [Block Adobe Reader from creating child processes](attack-surface-reduction-rules-reference#block-adobe-reader-from-creating-child-processes) (`7674ba52-37eb-4a4f-a9a1-f0f9a1619a2c`)
        - [Block Office communication application from creating child processes](attack-surface-reduction-rules-reference#block-office-communication-application-from-creating-child-processes) (`26190899-1602-49e8-8b27-eb1d0a1ce869`)
    - Turns off CFA and removes `c:\demo` from the CFA protected folders list that the setup script added (without affecting your other protected folders).
    - Downloads a decryption tool (`ransomware_cleanup_encrypt_decrypt.exe`) to `c:\demo\CleanupTools`, and uses it to decrypt `testfile_safe.txt` if Scenario 4 encrypted it.
2. The cleanup script is unsigned, so set the execution policy and unblock the script as described in Set up the demonstration. Then run the cleanup script in an elevated PowerShell window.

    The cleanup script sets CFA to **Disabled**. If you recorded the original [CFA mode](controlled-folder-access-overview#modes-for-cfa) before starting the demonstration (by running `Get-MpPreference | Format-List EnableControlledFolderAccess`), restore that value now. Replace `<mode>` with the original CFA mode value (for example, `Enabled`, `AuditMode`, or `Disabled`), and then run the following command in an elevated PowerShell window:

    ```powershell
    Set-MpPreference -EnableControlledFolderAccess <mode>
    ```

Or, if you used the manual method, do the following steps:

1. Disable the demonstration ASR rules. Run the `WindowsDefender_ASR_Disabled.ps1` script (see Set up the demonstration), or run the following command in an elevated PowerShell window:

    ```powershell
    Add-MpPreference -AttackSurfaceReductionRules_Ids 01443614-cd74-433a-b99e-2ecdc07bfc25,3b576869-a4ec-4529-8536-b80a7769e899,5beb7efe-fd9a-4556-801d-275e5ffc04cc,75668c1f-73b5-4cf0-bb93-3ecf5cb7cc84,92e97fa1-2edf-4476-bdd6-9dd0b4dddc7b,b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4,be9ba2d9-53ea-4cdc-84e5-9b1eeee46550,c1db55ab-c21a-4637-bb3f-a12568109d35,d1e49aac-8f56-4280-b9ba-993a6d77406c,d3e037e1-3eb8-44c8-a917-57927947596d,d4f940ab-401b-4efc-aadc-ad5f3c50688a -AttackSurfaceReductionRules_Actions Disabled,Disabled,Disabled,Disabled,Disabled,Disabled,Disabled,Disabled,Disabled,Disabled,Disabled
    ```
2. If Scenario 4 encrypted the files in `c:\demo`, decrypt them by using the [decryption tool](https://demo.wd.microsoft.com/Content/ransomware_cleanup_encrypt_decrypt.exe) (`ransomware_cleanup_encrypt_decrypt.exe`).

Whichever method you used, the cleanup script doesn't delete the test files or remove the `c:\demo` Microsoft Defender Antivirus exclusion that the setup script (or the manual steps) added. To fully revert the changes:

1. Delete any test files that you copied outside `c:\demo`.
2. Delete the `c:\demo` folder and the test files it contains. Do this step *before* you remove the exclusion in the next step. Otherwise, when real-time protection resumes for the folder, Microsoft Defender Antivirus detects the leftover test files (for example, as `Trojan:Win32/Vigorf.A`) and quarantines them. Run the following command in an elevated PowerShell window:

    ```powershell
    Remove-Item -Path C:\demo -Recurse -Force
    ```
3. Remove the `c:\demo` Microsoft Defender Antivirus exclusion by running the following command in an elevated PowerShell window:

    ```powershell
    Remove-MpPreference -ExclusionPath C:\demo
    ```