---
layout: Conceptual
title: Address unwanted behaviors in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/address-unwanted-behaviors-mde
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use exclusions, indicators, and other techniques to address false positives, performance issues, and app incompatibilities in Microsoft Defender for Endpoint.
author: limwainstein
ms.author: lwainstein
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.service: defender-endpoint
ms.subservice: onboard
ms.localizationpriority: medium
ms.reviewer: joshbregman
ms.custom:
- msecd-doc-authoring-1016
- partner-contribution
- msecd-doc-authoring-1012
ms.collection:
- m365-security
- tier2
ai-usage: ai-assisted
locale: en-us
document_id: 7d4981d0-52d4-4515-12ec-00912db4194a
document_version_independent_id: 7d4981d0-52d4-4515-12ec-00912db4194a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/address-unwanted-behaviors-mde.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: address-unwanted-behaviors-mde
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/address-unwanted-behaviors-mde.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: ce0c58e0-8742-2989-50f4-adbe09531303
---

# Address unwanted behaviors in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Microsoft Defender for Endpoint helps prevent and detect malicious processes and files. It protects your organization from threats while keeping productivity intact. Sometimes, unwanted behaviors can occur, such as:

- **False positives**: A file or process is flagged as malicious even though it isn't a threat
- **Poor performance**: Apps run slower when certain Defender for Endpoint features are active
- **Application incompatibility**: Apps don't work correctly when certain Defender for Endpoint features are active

This article explains how to address these unwanted behaviors and includes example scenarios.

Note

Creating an indicator or an exclusion should only be considered after thoroughly understanding the root cause of the unexpected behavior.

## General process for addressing unwanted behaviors

At a high level, the process for addressing an unwanted behavior in Defender for Endpoint is as follows:

1. Identify which capability is causing the unwanted behavior. To make your determination, determine if there's a misconfiguration with Microsoft Defender Antivirus, endpoint detection and response, attack surface reduction (ASR) rules, or controlled folder access (CFA). Use information in the Microsoft Defender portal or on the device.

    | Location | What to do |
    | --- | --- |
    | The [Microsoft Defender portal](https://security.microsoft.com) | To help identify what's happening, take one or more of the following actions: - [Investigate alerts](alerts-queue)- [Use advanced hunting](/en-us/defender-xdr/advanced-hunting-overview)- [View reports](threat-protection-reports) |
    | On the device | To identify the issue, take one or more of the following steps: - [Use performance analyzer tools](tune-performance-defender-antivirus)- [Review event logs and error codes](troubleshoot-microsoft-defender-antivirus)- [Check your protection history](microsoft-defender-security-center-antivirus) |
2. Depending on your findings about which capability is causing the unwanted behavior, you might take one or more of the following actions:

    - [Suppress alerts in the Microsoft Defender portal](manage-suppression-rules)
    - [Define custom remediation actions](configure-remediation-microsoft-defender-antivirus)
    - [Submit a file to Microsoft for analysis](admin-submissions-mde)
    - [Define exclusions for Microsoft Defender Antivirus](microsoft-defender-antivirus-exclusions-configure)
    - [Create indicators for Defender for Endpoint](indicator-manage)

    Tamper protection affects whether exclusions can be modified or added. See [What happens when tamper protection is turned on](tamper-protection-overview#what-happens-when-tamper-protection-is-turned-on).
3. Verify that your changes addressed the issue.

## Examples of unwanted behaviors

The following example scenarios show cases that can be addressed by using exclusions and indicators. For more information about exclusions, see [Exclusions overview](defender-endpoint-exclusions-overview).

### An app is detected by Microsoft Defender Antivirus when the application runs

In this scenario, whenever a user runs a certain application, the application is detected by Microsoft Defender Antivirus as a potential threat.

**How to address**: Create an "allow" indicator for Microsoft Defender for Endpoint. For example, you can create an "allow" indicator for a file, such as an executable. See [Create indicators for files](indicator-file).

### A custom, self-signed app is detected by Microsoft Defender Antivirus when the application runs

In this scenario, Microsoft Defender Antivirus detects a custom app as a potential threat. The app is updated periodically and is self-signed.

**How to address**: Create "allow" indicators for certificates or files. See the following articles:

- [Create indicators based on certificates](indicator-certificates)
- [Create indicators for files](indicator-file)

### A custom app accesses a set of file types that is detected as malicious when the application runs

In this scenario, a custom app accesses a set of file types, and the set is detected as malicious by Microsoft Defender Antivirus whenever the application runs.

**How to observe**: When the application is running, behavior monitoring in Microsoft Defender Antivirus detects it.

**How to address**: Define exclusions for Microsoft Defender Antivirus, such as a file or path exclusion that might include wildcards. Or define a custom file path exclusion. See the following articles:

- [Address false positives/negatives in Microsoft Defender for Endpoint](defender-endpoint-false-positives-negatives)
- [Configure and validate exclusions based on file extension and folder location](microsoft-defender-antivirus-exclusions-configure)

### An application is detected by Microsoft Defender Antivirus as a "behavior" detection

In this scenario, Microsoft Defender Antivirus detects an application because of certain behavior, even though the application isn't a threat.

**How to address**: Define a process exclusion. See the following articles:

- [Configure and validate exclusions based on file extension and folder location](microsoft-defender-antivirus-exclusions-configure)
- [Configure exclusions for files opened by processes](microsoft-defender-antivirus-exclusions-configure)

### An app is considered a potentially unwanted application (PUA)

In this scenario, an app is detected as PUA, and you want to allow it to run.

**How to address**: Define an exclusion for the app. See the following articles:

- [Exclude files from PUA protection](detect-block-potentially-unwanted-apps-microsoft-defender-antivirus#exclude-files-from-pua-protection)
- [Configure and validate exclusions based on file extension and folder location](microsoft-defender-antivirus-exclusions-configure)

### An app is blocked from writing to a protected folder

In this scenario, a legitimate app is blocked from writing to folders that are protected by controlled folder access.

**How to address**: Add the app to the "allowed" list for controlled folder access. See [Allow apps to modify files in protected folders](controlled-folder-access-configure#allow-apps-to-modify-files-in-protected-folders-in-the-windows-security-app).

### A third-party app is detected as malicious by Microsoft Defender Antivirus

In this scenario, a third-party app that isn't a threat is detected and identified as malicious by Microsoft Defender Antivirus.

**How to address**: Submit the app to Microsoft for analysis. See [How to submit a file to Microsoft for analysis](/en-us/defender-xdr/submission-guide#how-do-i-submit-a-file-to-microsoft-for-analysis).

### An app is incorrectly detected and identified as malicious by Defender for Endpoint

In this scenario, a legitimate app is detected and identified as malicious by an [attack surface reduction (ASR) rule](attack-surface-reduction-rules-overview) in Microsoft Defender Antivirus. The ASR rule [Block JavaScript or VBScript from launching downloaded executable content](attack-surface-reduction-rules-reference#block-javascript-or-vbscript-from-launching-downloaded-executable-content) blocks any downloaded content when the user tries to use the app.

To learn how to view ASR rule detections in Defender for Endpoint, see [Monitor attack surface reduction (ASR) rule activity](attack-surface-reduction-rules-monitor).

**How to address**:

Use the **Attack surface reduction rules** report to see the detections, affected devices, and affected files. In particular, you can download the full file and path information for the affected files to exclude from the ASR rule on the [Add exclusions tab](attack-surface-reduction-rules-report#manage-exclusions-on-the-add-exclusions-tab) of the report.

To learn how to configure ASR rule exclusions, see [File and folder exclusions for ASR rules](attack-surface-reduction-rules-overview#file-and-folder-exclusions-for-asr-rules).

### Word templates that contain macros that launch other apps are blocked

In this scenario, the ASR rule [Block Win32 API calls from Office macros](attack-surface-reduction-rules-reference#block-win32-api-calls-from-office-macros) blocks Microsoft Word when a user opens documents created from Microsoft Word templates that contain macros, and those macros launch other applications.

To learn how to view ASR rule detections in Defender for Endpoint, see [Monitor attack surface reduction (ASR) rule activity](attack-surface-reduction-rules-monitor).

**How to address**:

Use the **Attack surface reduction rules** report to see the detections, affected devices, and affected files. In particular, you can download the full file and path information for the affected files to exclude from the ASR rule on the [Add exclusions tab](attack-surface-reduction-rules-report#manage-exclusions-on-the-add-exclusions-tab) of the report.

To learn how to configure ASR rule exclusions, see [File and folder exclusions for ASR rules](attack-surface-reduction-rules-overview#file-and-folder-exclusions-for-asr-rules).