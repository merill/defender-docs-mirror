---
layout: Conceptual
title: Troubleshoot ASR rules - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-asr
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Troubleshoot false positives, false negatives, and other issues with attack surface reduction (ASR) rules in Microsoft Defender Antivirus. Includes self-service diagnostic steps and guidance for collecting data before opening a support case.
ms.service: defender-endpoint
ms.localizationpriority: medium
audience: ITPro
author: chrisda
ms.author: chrisda
ms.date: 2026-07-17T00:00:00.0000000Z
ms.reviewer: 
ms.custom: asr, msecd-doc-authoring-1016
ms.subservice: asr
ms.topic: how-to
ms.collection:
- m365-security
- tier3
- mde-asr
ai-usage: ai-assisted
locale: en-us
document_id: e677262d-eddb-48ab-2196-77228467623c
document_version_independent_id: e677262d-eddb-48ab-2196-77228467623c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/troubleshoot-asr.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: troubleshoot-asr
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/troubleshoot-asr.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bba62c59-6b53-4be4-8b9d-6624f9184c22
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f3a81ffb-ee36-4ec7-b54a-01b6681aff65
platformId: 310daffa-ffdf-10e7-6201-e29dd4d5d2f7
---

# Troubleshoot ASR rules - Microsoft Defender for Endpoint | Microsoft Learn

Even after you carefully follow the [Attack surface reduction (ASR) rules deployment guide](attack-surface-reduction-rules-deployment), you still might run into issues with ASR rules in Microsoft Defender Antivirus. For example:

- An ASR rule blocks a file or process, or does some other action that it shouldn't (false positive).
- An ASR rule doesn't work as described, or doesn't block a file or process that it should (false negative).

This article describes the steps you can take yourself to troubleshoot the issues, including collecting data to open a support case with Microsoft if you are unable to fix the problem yourself. For more information about ASR rules, see [Attack surface reduction (ASR) rules overview](attack-surface-reduction-rules-overview).

## Confirm ASR rule prerequisites

For ASR rule requirements, see [Requirements for ASR rules](attack-surface-reduction-rules-overview#requirements-for-asr-rules).

## Verify the active ASR rules and actions on devices

Run the following command in PowerShell on the device to list the configured ASR rule IDs and their current action values. The output helps you identify which rules are active and whether they're set to **Block**, **Audit**, or another mode:

```powershell
$p = Get-MpPreference;0..([math]::Min($p.AttackSurfaceReductionRules_Ids.Count,$p.AttackSurfaceReductionRules_Actions.Count)-1) | % {[pscustomobject]@{Id=$p.AttackSurfaceReductionRules_Ids[$_];Action=$p.AttackSurfaceReductionRules_Actions[$_]}} | Format-Table -AutoSize
```

The following sample output shows ASR rule GUIDs in the **Id** column and their configured action values in the **Action** column. Use this output to confirm which rules are set to **Block** mode (action value 1) or **Audit** mode (action value 2):

```powershell
Id                                   Action
--                                   ------
01443614-cd74-433a-b99e-2ecdc07bfc25      2
26190899-1602-49e8-8b27-eb1d0a1ce869      1
3b576869-a4ec-4529-8536-b80a7769e899      1
5beb7efe-fd9a-4556-801d-275e5ffc04cc      1
75668c1f-73b5-4cf0-bb93-3ecf5cb7cc84      1
7674ba52-37eb-4a4f-a9a1-f0f9a1619a2c      1
92e97fa1-2edf-4476-bdd6-9dd0b4dddc7b      1
9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2      2
b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4      1
be9ba2d9-53ea-4cdc-84e5-9b1eeee46550      1
c1db55ab-c21a-4637-bb3f-a12568109d35      2
d1e49aac-8f56-4280-b9ba-993a6d77406c      1
d3e037e1-3eb8-44c8-a917-57927947596d      2
d4f940ab-401b-4efc-aadc-ad5f3c50688a      2
e6db77e5-3df2-4cf1-b95a-636979351e5b      1
```

In this example, the [ASR rules listed in the overview](attack-surface-reduction-rules-overview#asr-rules) are active in [different ASR rule modes](attack-surface-reduction-rules-overview#modes-for-asr-rules) on the device (2 = **Audit** mode, 1 = **Block** mode).

Note

If you used [Group Policy to configure ASR rules](attack-surface-reduction-rules-configure#configure-asr-rules-and-exclusions-in-group-policy), verify there are no extra characters like quotation marks or spaces in the ASR rule GUID value.

Tip

To see the actual value of each ASR rule setting on a device and the source that configured it, use the **Effective settings** tab on the device page. For more information, see [Configuration management - Effective settings](investigate-machines#configuration-management---effective-settings).

## Switch misbehaving ASR rules to Audit mode for testing

ASR rules in **Audit mode** don't block files or processes, but the actions that the rule would have taken in **Block** or **Warn** mode are recorded.

Use the same method you originally used to distribute ASR rules to devices (for example, Group Policy, Intune, or PowerShell) to set the problematic rules to **Audit** mode. For instructions, see [Configure attack surface reduction rules](attack-surface-reduction-rules-configure).

Tip

If the ASR rule was already in **Audit** mode, that explains why it wasn't blocking the files or processes you expected it to block (false negative). ASR rules can accidentally get into **Audit** mode in the following scenarios:

- You were testing another feature and forgot to set the ASR rule back into **Block** or **Warn** mode.
- An automated PowerShell script changed the rule mode.

After you configure the rule in **Audit** mode, do the following steps:

1. Do the action on the device that causes the issue. For example, open the file or run the process that isn't blocked but should be blocked (false negative).
2. [Review the ASR rule activity](attack-surface-reduction-rules-monitor).

    Specifically, filter **Event ID** values in Windows Event viewer by the following values in the **Applications and Services Logs** &gt; **Microsoft** &gt; **Windows** &gt; **Windows Defender** &gt; **Operational** log:

    - **Block events**: 1121
    - **Audit events**: 1122
    - **User override events in Warn mode**: 1129
    - **Configuration changes**: 5007

    For detailed information, see [View attack surface reduction events in Windows Event Viewer](attack-surface-reduction-windows-events#browse-attack-surface-reduction-events-in-windows-event-viewer).

    [![Screenshot of the Event Viewer page.](media/eventviewerscrnew.png)](media/eventviewerscrnew.png#lightbox)

## Steps to take if the ASR rule still doesn't work as expected

If the ASR rule still isn't working as expected, do one of the following steps:

- For false positives, add the file or path as an exclusion to the ASR rule. For more information, see [File and folder exclusions for ASR rules](attack-surface-reduction-rules-overview#file-and-folder-exclusions-for-asr-rules).
- Use the [Microsoft Security Intelligence web-based submission form](https://www.microsoft.com/wdsi/support/report-exploit-guard) to report a false negative or false positive for ASR rules. With a Windows E5 subscription, you can also provide a link to any associated alert from the [Alerts queue](alerts-queue).
- When you report a problem involving ASR rules to Microsoft, you need to collect and submit diagnostic data to help troubleshoot the issue. See the following diagnostic data collection sections for instructions on using the MDE Client Analyzer or MpCmdRun.

## Collect diagnostic data for Microsoft support

When you open a support case with Microsoft for an ASR rule issue, you need to collect diagnostic data from the affected device. You can use either the MDE Client Analyzer or the MpCmdRun command-line tool to generate the required diagnostic files.

### Collect diagnostic data with the MDE Client Analyzer

Follow these steps to collect diagnostic data with the MDE Client Analyzer:

1. Download the [MDE Client Analyzer](overview-client-analyzer).
2. Close any apps on the device that aren't essential to reproducing the issue.
3. Run MDE Client Analyzer in verbose mode to collect detailed diagnostic data for troubleshooting ASR-related behavior. The `-v` switch enables verbose logging, which captures the additional detail that Microsoft Support needs to diagnose ASR rule issues. You can run the analyzer [locally or using Live Response](run-analyzer-windows):

    ```dos
    C:\Work\tools\MDEClientAnalyzer\MDEClientAnalyzer.cmd -v
    ```

    Tip

    Ensure that log collection takes place during the reproduction attempt.

### Collect diagnostic data with MpCmdRun

To use `MpCmdRun.exe -GetFiles` to manually generate the diagnostic log files to `C:\ProgramData\Microsoft\Windows Defender\Support\MpSupportFiles.cab`, see the instructions at [Collect Microsoft Defender Antivirus diagnostic data](collect-diagnostic-data).

In the `MpSupportFiles.cab` file, the following files are most relevant:

- `MPOperationalEvents.txt`: Contains the same level of information found in Event Viewer for the Microsoft Defender Antivirus Operational log.
- `MPRegistry.txt`: Analyze all the current Microsoft Defender Antivirus configurations from when you generated the .cab file.
- `MPLog.txt`: Verbose information about all the actions and operations of Microsoft Defender Antivirus.