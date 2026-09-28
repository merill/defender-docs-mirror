---
layout: Conceptual
title: Troubleshooting mode scenarios in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/troubleshooting-mode-scenarios
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use Microsoft Defender for Endpoint troubleshooting mode to diagnose application, performance, attack surface reduction, and network protection issues.
ms.service: defender-endpoint
ms.author: chrisda
author: chrisda
ms.reviewer: pricci
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-ngp
ms.topic: troubleshooting-general
ms.subservice: ngp
ms.date: 2026-09-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: c399e3fd-7b8b-4ce9-6b18-7eada18740f6
document_version_independent_id: c399e3fd-7b8b-4ce9-6b18-7eada18740f6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/troubleshooting-mode-scenarios.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: troubleshooting-mode-scenarios
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/troubleshooting-mode-scenarios.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 4dcc05a3-0ea4-5d43-0c26-fb68d73e1163
---

# Troubleshooting mode scenarios in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Troubleshooting mode in Microsoft Defender for Endpoint lets local administrators temporarily test certain policy-managed Microsoft Defender Antivirus settings on individual Windows devices. Use the scenarios in this article to determine whether antivirus scanning, exclusions, attack surface reduction (ASR) rules, or network protection contribute to an issue.

Before testing a scenario, review the requirements and [enable troubleshooting mode in the Microsoft Defender portal](troubleshooting-mode-enable#enable-troubleshooting-mode-in-the-microsoft-defender-portal). Changes made during troubleshooting mode are temporary. When troubleshooting mode expires, policy-managed settings return to their previous values.

For Microsoft Defender Antivirus performance investigations, start with the [Microsoft Defender Antivirus performance analyzer](tune-performance-defender-antivirus).

Tip

- If tamper protection blocks a temporary setting change, follow the [PowerShell procedure to temporarily disable tamper protection and verify that it's off](troubleshooting-mode-enable#temporarily-disable-tamper-protection-using-powershell).

## Scenario 1: Troubleshoot a blocked application installation

Use this scenario when Microsoft Defender Antivirus blocks an application installation that you believe is safe.

1. [Capture process logs using Process Monitor](troubleshoot-av-performance-issues-with-procmon#capture-process-logs-using-process-monitor) and review the guidance for [troubleshooting performance issues related to real-time protection](troubleshoot-performance-issues).
2. If the investigation indicates that real-time protection is blocking the installation, enable troubleshooting mode and [temporarily disable tamper protection](troubleshooting-mode-enable#temporarily-disable-tamper-protection).
3. Run the following command in an elevated PowerShell session to temporarily disable real-time protection:

    ```powershell
    Set-MpPreference -DisableRealtimeMonitoring $true
    ```
4. Retry the installation. Only test applications that your organization has independently validated as safe.
5. If the installation succeeds only while real-time protection is off, use the diagnostic results to determine whether you need a narrowly scoped [Microsoft Defender Antivirus exclusion](microsoft-defender-antivirus-exclusions-configure).
6. To restore real-time protection immediately instead of waiting for troubleshooting mode to expire, run the following command in an elevated PowerShell session:

    ```powershell
    Set-MpPreference -DisableRealtimeMonitoring $false
    ```

## Scenario 2: Investigate high CPU usage by MsMpEng.exe

Use this scenario when the Microsoft Defender Antivirus process `MsMpEng.exe` uses high CPU during a scan or while an application is running.

1. Use the [Microsoft Defender Antivirus performance analyzer](tune-performance-defender-antivirus#run-the-microsoft-defender-antivirus-performance-analyzer) to identify the files, file extensions, and processes that contribute most to scan time.
2. If you need more process-level detail, [capture process logs using Process Monitor](troubleshoot-av-performance-issues-with-procmon#capture-process-logs-using-process-monitor).
3. After you identify the cause, [enable troubleshooting mode](troubleshooting-mode-enable#enable-troubleshooting-mode-in-the-microsoft-defender-portal) and test the smallest appropriate [file, folder, file type, or process exclusion](microsoft-defender-antivirus-exclusions-overview). To create the temporary exclusion without overwriting existing exclusions, follow [Configure Microsoft Defender Antivirus exclusions in PowerShell](microsoft-defender-antivirus-exclusions-configure#configure-microsoft-defender-antivirus-exclusions-in-powershell).
4. Only keep an exclusion if testing confirms that it's necessary. Before deploying an exclusion broadly, review [Common mistakes to avoid when defining exclusions](defender-endpoint-exclusions-common-mistakes).

## Scenario 3: Investigate slow application performance

Use this scenario when an application takes longer than expected to open files, save data, compile code, or complete another file-intensive action.

1. Use the [Microsoft Defender Antivirus performance analyzer](tune-performance-defender-antivirus#record-and-analyze-events-with-the-microsoft-defender-antivirus-performance-analyzer) to identify the affected paths and processes.
2. If the results suggest that real-time scanning contributes to the delay, [enable troubleshooting mode](troubleshooting-mode-enable#enable-troubleshooting-mode-in-the-microsoft-defender-portal) and [temporarily disable tamper protection](troubleshooting-mode-enable#temporarily-disable-tamper-protection).
3. Run the following command in an elevated PowerShell session to temporarily disable real-time protection:

    ```powershell
    Set-MpPreference -DisableRealtimeMonitoring $true
    ```
4. Repeat the affected application action.
5. If performance improves, use the analyzer results to evaluate a narrow exclusion instead of leaving real-time protection disabled. For configuration guidance, see [Configure Microsoft Defender Antivirus exclusions](microsoft-defender-antivirus-exclusions-configure).
6. To restore real-time protection immediately instead of waiting for troubleshooting mode to expire, run the following command in an elevated PowerShell session:

    ```powershell
    Set-MpPreference -DisableRealtimeMonitoring $false
    ```

## Scenario 4: Investigate an Office add-in blocked by an ASR rule

Use this scenario when the [Block all Office applications from creating child processes](attack-surface-reduction-rules-reference#block-all-office-applications-from-creating-child-processes) ASR rule prevents a trusted Office add-in from working.

1. [Enable troubleshooting mode](troubleshooting-mode-enable#enable-troubleshooting-mode-in-the-microsoft-defender-portal).
2. Use [Configure ASR rules in PowerShell](attack-surface-reduction-rules-configure#configure-asr-rules-in-powershell) to temporarily set the affected rule to `Disabled`.
3. Test the add-in again to determine whether the rule causes the issue.
4. If disabling the rule resolves the issue, don't leave the rule disabled. Evaluate whether `Warn` mode, `Audit` mode, or a scoped exclusion meets your organization's security and business requirements. For planning and testing guidance, see [Operationalize attack surface reduction rules](attack-surface-reduction-rules-deployment-operationalize).

## Scenario 5: Investigate a domain blocked by network protection

Use this scenario when network protection blocks access to a domain that your organization expects to allow.

1. [Review network protection events in the Microsoft Defender portal](network-protection#review-network-protection-events-in-the-microsoft-defender-portal) or [Windows Event Viewer](network-protection#review-network-protection-events-in-windows-event-viewer) to confirm that network protection generated the block.
2. [Enable troubleshooting mode](troubleshooting-mode-enable#enable-troubleshooting-mode-in-the-microsoft-defender-portal).
3. Follow [Configure network protection by using PowerShell](enable-network-protection#configure-network-protection-by-using-powershell) to temporarily set network protection to `Disabled`.
4. Test access to the domain again.
5. If disabling network protection resolves the issue, turn network protection back on and follow [Troubleshoot network protection](troubleshoot-np) to evaluate audit events, report an incorrect detection, or configure an appropriate exclusion.