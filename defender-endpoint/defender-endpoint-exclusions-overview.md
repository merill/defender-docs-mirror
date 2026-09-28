---
layout: Conceptual
title: Overview of exclusions and indicators in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/defender-endpoint-exclusions-overview
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn when to use exclusions versus allow indicators in Microsoft Defender for Endpoint and Microsoft Defender Antivirus, and which alternatives to try before you create them.
ms.service: defender-endpoint
ms.subservice: ngp
ms.localizationpriority: medium
ms.topic: how-to
author: chrisda
ms.author: chrisda
ms.custom: nextgen, msecd-doc-authoring-1015
ms.date: 2026-07-02T00:00:00.0000000Z
ms.reviewer: joshbregman
ms.collection:
- m365-security
- tier2
- mde-ngp
ai-usage: ai-assisted
locale: en-us
document_id: 59dcf82c-1c31-2643-b8f6-d94e3a43fc80
document_version_independent_id: 59dcf82c-1c31-2643-b8f6-d94e3a43fc80
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/defender-endpoint-exclusions-overview.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-endpoint-exclusions-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/defender-endpoint-exclusions-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 4cb1e7b2-f569-ff06-d1bf-4f12a5ae4cd5
---

# Overview of exclusions and indicators in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

[Microsoft Defender for Endpoint](microsoft-defender-endpoint) and [Defender for Business](/en-us/defender-business/mdb-overview) include a wide range of capabilities to prevent, detect, investigate, and respond to advanced cyberthreats. Microsoft preconfigures the product to perform well on the operating system where it's installed. In most cases, no other changes are needed.

Despite preconfigured settings, sometimes unexpected behavior occurs. For example:

- **False positives**: Files, folders, or processes that aren't threats are detected as malicious by Defender for Endpoint or Microsoft Defender Antivirus. These entities are blocked or sent to quarantine, even though they're not a threat.
- **Performance issues**: Systems experience unexpected performance issues when running with Defender for Endpoint or Microsoft Defender Antivirus.
- **Application compatibility issues**: Applications experience unexpected behavior when running with Defender for Endpoint or Microsoft Defender Antivirus.

The following sections describe the types of exclusions available in Defender for Endpoint and Microsoft Defender Antivirus, along with when to use each one. For a summary of which management tools you can use to configure each exclusion type, see [Exclusions reference for Microsoft Defender for Endpoint](defender-endpoint-exclusions-configuration-reference).

Note

Creating exclusions or indicators is one possible approach for addressing issues with Defender for Endpoint or Microsoft Defender Antivirus, but often there are other steps you can take first.

## Types of exclusions

There are several types of exclusions to consider. Some types of exclusions affect multiple capabilities in Defender for Endpoint, whereas other types are specific to Microsoft Defender Antivirus.

For information about indicators, which are a related but separate mechanism for allowing or blocking specific files, IP addresses, URLs, and certificates, see [Overview of indicators in Microsoft Defender for Endpoint](indicators-overview).

The following tables summarize the types of exclusions you can define, grouped by whether they're available on all platforms or on Windows only. Note the scope for each exclusion type.

- **Cross-platform exclusions**: These exclusions are available on Windows, macOS, and Linux devices.

    | Exclusion type | Scope | Use cases |
    | --- | --- | --- |
    | Custom exclusions | AntivirusAttack surface reduction (ASR) rulesNetwork Protection | A file, folder, or process is identified as malicious, even though it's not a threat.An application encounters unexpected performance or application compatibility issues when running with Defender for Endpoint.In Windows, [some ASR rules](attack-surface-reduction-rules-overview#file-and-folder-exclusions-for-asr-rules) honor Microsoft Defender Antivirus file and folder (path) exclusions. |
    | [File and certificate allow indicators](indicator-certificates) | AntivirusASR rulesControlled folder access (CFA) | A file or process signed by a certificate is identified as malicious even though it's not. |
    | [Domain/URL and IP address indicators](indicator-ip-domain) | Network ProtectionSmartScreenWeb Content Filtering | SmartScreen reports a false positive.You want to override a Web Content Filtering block on a specific site. |
- **Windows-only exclusions**: These exclusions are available on Windows devices only.

    | Exclusion type | Scope | Use cases |
    | --- | --- | --- |
    | Preconfigured antivirus exclusions | Antivirus | Microsoft Defender Antivirus automatically excludes some operating system files and Windows Server roles, so you don't have to define these exclusions yourself. |
    | ASR rule exclusions | ASR rules | An ASR rule causes unexpected behavior. |
    | Automation folder exclusions | Automated investigation and response | Automated investigation and remediation takes an action on a file, extension, or directory that should be handled manually. |
    | CFA exclusions | CFA | CFA blocks an application from accessing a protected folder. |

Note

Process exclusions directly affect [network protection](network-protection) on all platforms and ASR rules in Windows. A process exclusion on any operating system (Windows, macOS, or Linux) prevents network protection from inspecting traffic or enforcing rules for that specific process.

### Preconfigured antivirus exclusions

You don't have to define these exclusion types, but it's helpful to know what they are and how they work. Microsoft Defender Antivirus preconfigures the following exclusion types:

- **Built-in Microsoft Defender Antivirus exclusions**:
    - Microsoft Defender Antivirus includes built-in exclusions for operating system files on all supported client and server versions of Windows. The list is kept up to date as the threat landscape changes. For more information, see [Built-in exclusions](microsoft-defender-antivirus-exclusions-overview#built-in-exclusions).
    - On supported versions of Windows Server, more built-in exclusions apply to server features such as Windows Internet Name Service (WINS) and File Replication Service (FRS). For more information, see [Built-in exclusions on Windows Server](microsoft-defender-antivirus-exclusions-windows-server#built-in-exclusions).

- **Automatic Microsoft Defender Antivirus exclusions**: Automatic exclusions for server roles and features in Windows Server 2016 or later (for example, File Replication Service, Hyper-V, SYSVOL, Active Directory, and DNS Server). When you install a role, Microsoft Defender Antivirus includes automatic exclusions for the server role and any files that are added while installing the role.

    These exclusions aren't scanned by [real-time protection](configure-protection-features-microsoft-defender-antivirus) but are still subject to [quick, full, or custom antivirus scans](schedule-antivirus-scans#comparing-the-quick-scan-full-scan-and-custom-scan).

    For more information, see [Automatic server role exclusions](microsoft-defender-antivirus-exclusions-windows-server#automatic-server-role-exclusions).

    Automatic exclusions apply only to built-in Windows Server roles. If you run other server workloads, such as Exchange Server, SharePoint Server, or SQL Server, you likely need to define custom antivirus exclusions for them. For more information, see the following articles:

    - [Running Windows antivirus software on Exchange Server](/en-us/exchange/antispam-and-antimalware/windows-antivirus-software)
    - [Folders to exclude from antivirus scans on SharePoint Server](https://support.microsoft.com/SharePoint/admin/certain-folders-may-have-to-be-excluded-from-antivirus-scanning-when-you-use-file-level-antivirus-so)
    - [Configure antivirus software to work with SQL Server](/en-us/troubleshoot/sql/database-engine/security/antivirus-and-sql-server)

    You can also refer to the software publisher's documentation.

### Custom exclusions

Microsoft Defender for Endpoint and Microsoft Defender Antivirus let you configure custom exclusions to optimize performance and avoid false positives. The custom exclusions you can define vary by operating system.

- **macOS**: You can define exclusions that apply to antivirus scanning only (on-demand scans, real-time protection, and monitoring). These exclusions don't apply to endpoint detection and response (EDR), so excluded files can still trigger EDR alerts and other detections. The supported exclusion types include:

    - **File extension exclusions**: Exclude all files with a specific extension.
    - **File exclusions**: Exclude a specific file identified by its full path.
    - **Folder exclusions**: Exclude all files under a specified folder recursively.
    - **Process exclusions**: Exclude a specific process and all files opened by it.

    For more information, see [Configure and validate exclusions for Microsoft Defender for Endpoint on macOS](mac-exclusions).
- **Linux**: You can configure exclusions as *antivirus exclusions* (applied to real-time protection, on-demand scans, and behavior monitoring, while keeping EDR visibility) or as *global exclusions* (applied at the sensor level, muting both antivirus detections and EDR alerts). The supported exclusion types include:

    - **File extension exclusions**: Exclude all files with a specific extension (not available for global exclusions).
    - **File exclusions**: Exclude a specific file identified by its full path.
    - **Folder exclusions**: Exclude all files under a specified folder recursively.
    - **Process exclusions**: Exclude a specific process (by full path or file name) and all files opened by it.

    For more information, see [Configure and validate exclusions for Microsoft Defender for Endpoint on Linux](linux-exclusions).
- **Windows**: You can configure Microsoft Defender Antivirus to exclude combinations of processes, files, folders (paths), and extensions from scheduled scans, on-demand scans, real-time protection, and potentially unwanted app (PUA) detections. These exclusions apply to antivirus scanning only. They don't apply to EDR, so excluded files can still trigger EDR alerts. To exclude files for all Defender for Endpoint capabilities, use [custom indicators](indicators-overview). The supported exclusion types include:

    - **File and folder exclusions**: Exclude a specific file or everything in a folder. Also known as *path exclusions*.
    - **File extension exclusions**: Exclude any file that has a specific extension, regardless of location.
    - **Process exclusions**: Exclude all files that a specific process opens.
    - **Contextual exclusions**: Narrow a path exclusion so that it applies only in a specific context, such as only when a specific process opens the file.

    For more information, see [Exclusions in Microsoft Defender Antivirus](microsoft-defender-antivirus-exclusions-overview).

### Attack surface reduction rule exclusions

[Attack surface reduction (ASR) rules](attack-surface-reduction-rules-overview) block risky software behavior, but some legitimate apps engage in this risky behavior (for example, launching executable files that download and run other files). Some ASR rules honor Microsoft Defender Antivirus exclusions. ASR rules also support global ASR rule exclusions and per-ASR rule exclusions.

For more information, see [File and folder exclusions for ASR rules](attack-surface-reduction-rules-overview#file-and-folder-exclusions-for-asr-rules).

### Automation folder exclusions

Automation folder exclusions apply to [automated investigation and remediation](automated-investigations) in Microsoft Defender for Endpoint Plan 2, which examines alerts and takes immediate action to resolve detected breaches. When an alert triggers an automated investigation, the investigation reaches a verdict (Malicious, Suspicious, or No threats found) for each piece of evidence. Depending on the [automation level](automation-levels) and other security settings, remediation actions occur automatically or after your security operations team approves them.

For more information, see [Manage automation folder exclusions](automation-folder-exclusions-configure).

### Controlled folder access exclusions

[Controlled folder access (CFA)](controlled-folder-access-overview) protects your data by blocking untrusted apps from changing files in [protected folders](controlled-folder-access-overview#default-folders-protected-by-cfa) on Windows devices. By default, CFA protects common system folders, and you can [add other folders](controlled-folder-access-overview#add-other-folders-to-cfa). If CFA blocks an app that you trust, you can define an exclusion to [allow the app to modify files in protected folders](controlled-folder-access-overview#allow-apps-to-modify-files-in-protected-folders).

For more information, see [Configure controlled folder access](controlled-folder-access-configure).

### Custom remediation actions

When Microsoft Defender Antivirus detects a potential threat while running a scan, it attempts to remediate or remove the detected threat. You can define custom remediation actions to configure how Microsoft Defender Antivirus should address certain threats, whether a restore point should be created before remediating, and when threats should be removed.

For more information, see [Configure remediation actions for Microsoft Defender Antivirus detections](configure-remediation-microsoft-defender-antivirus).

## How exclusions and indicators are evaluated

Most organizations have several types of exclusions and indicators to determine whether users should be able to access and use a file or process. On Windows devices, these exclusions and indicators are processed in a particular order so that [policy conflicts are handled systematically](indicator-file#policy-conflict-handling).

Here's how it works. Evaluation stops at the first condition that applies:

1. If the file isn't allowed by Windows Defender Application Control and AppLocker enforce mode policies, it's **blocked**.
2. Otherwise, if the file is allowed by a Microsoft Defender Antivirus exclusion, it's **allowed**.
3. Otherwise, if the file has a block or warn file indicator, it's **blocked or warned**.
4. Otherwise, if the file is blocked by SmartScreen, it's **blocked**.
5. Otherwise, if the file is allowed by an allow file indicator, it's **allowed**.
6. Otherwise, if the file is blocked by attack surface reduction rules, controlled folder access, or antivirus protection, it's **blocked**.
7. Otherwise, the file is **allowed**.

### How policy conflicts are handled

In cases where Defender for Endpoint indicators conflict, here's what to expect:

- If there are conflicting file indicators, the indicator that uses the most secure hash is applied. For example, SHA256 takes precedence over SHA-1, which takes precedence over MD5.
- If there are conflicting URL indicators, the more specific indicator is used.

    - For [Microsoft Defender SmartScreen](/en-us/windows/security/operating-system-security/virus-and-threat-protection/microsoft-defender-smartscreen/), an indicator that uses the longest URL path is applied. For example, `www.contoso.com/admin/` takes precedence over `www.contoso.com`.
    - [Network protection](network-protection) primarily enforces at the domain level, although it can block specific URL paths in some scenarios.
- If there are similar indicators for a file or process that have different actions, the indicator that is scoped to a specific device group takes precedence over an indicator that targets all devices.

### How automated investigation and remediation works

[Automated investigation and remediation capabilities](automated-investigations) in Defender for Endpoint first determine a verdict for each piece of evidence, and then take an action depending on Defender for Endpoint indicators. As a result, a file or process could get a verdict of "good" (which means no threats were found) and still be blocked if there's an indicator with that action. Similarly, an entity could get a verdict of "bad" (which means it's determined to be malicious) and still be allowed if there's an indicator with that action.

For more information, see [Automated investigation and remediation engine](indicators-overview#automated-investigation-and-remediation-engine).

## Alternatives and steps to consider before you create an exclusion

Creating an exclusion or an allow indicator creates a protection gap. Use these techniques only after you determine the root cause of the issue. Until then, consider alternatives such as submitting a file to Microsoft for analysis or suppressing an alert.

The following list describes common scenarios and the steps to consider before creating an exclusion or allow indicator.

- **[False positive](defender-endpoint-false-positives-negatives)**: An entity, such as a file or a process, was detected and identified as malicious, even though the entity isn't a threat. Steps to consider:

    1. [Review and classify alerts](defender-endpoint-false-positives-negatives#part-1-review-and-classify-alerts) that were generated as a result of the detected entity.
    2. Suppress an alert for a known entity.
    3. [Review remediation actions](defender-endpoint-false-positives-negatives#part-2-review-remediation-actions) that were taken for the detected entity.
    4. Submit the false positive to Microsoft for analysis.
    5. [Define an indicator or an exclusion](defender-endpoint-false-positives-negatives#part-3-review-or-define-exclusions) for the entity (only if necessary).
- **[Performance issues](troubleshoot-performance-issues)**. For example:

    - A system has high CPU usage or other performance issues.
    - A system has memory leak issues.
    - An app is slow to load on devices.
    - An app is slow to open a file on devices.

    Steps to consider:

    1. [Collect diagnostic data](collect-diagnostic-data) for Microsoft Defender Antivirus.
    2. If you're using a non-Microsoft antivirus solution, [check with the vendor for known issues with antivirus products](troubleshoot-performance-issues#check-with-the-vendor-for-known-issues-with-antivirus-products).
    3. Review performance logs (see [Troubleshoot Microsoft Defender Antivirus performance issues with WPRUI](troubleshoot-av-performance-issues-with-wprui)) to determine the estimated performance impact. For performance-specific issues related to Microsoft Defender Antivirus, use the [Performance analyzer for Microsoft Defender Antivirus](tune-performance-defender-antivirus).
    4. [Define an exclusion for Microsoft Defender Antivirus](microsoft-defender-antivirus-exclusions-overview) (if necessary).
    5. [Create an indicator for Defender for Endpoint](indicators-overview) (only if necessary).
- **[Compatibility issues with non-Microsoft antivirus products](microsoft-defender-antivirus-compatibility)**. For example, Defender for Endpoint relies on security intelligence updates for devices, whether they're running Microsoft Defender Antivirus or a non-Microsoft antivirus solution. Steps to consider:

    1. If you're using a non-Microsoft antivirus product as your primary antivirus/antimalware solution, [set Microsoft Defender Antivirus to passive mode](microsoft-defender-antivirus-compatibility#requirements-for-microsoft-defender-antivirus-to-run-in-passive-mode).
    2. If you're switching from a non-Microsoft antivirus/antimalware solution to Defender for Endpoint, see [Make the switch to Defender for Endpoint](switch-to-mde-overview). This guidance includes [Exclusions you might need to define for Microsoft Defender Antivirus](switch-to-mde-phase-2#step-4-add-your-existing-solution-to-the-exclusion-list-for-microsoft-defender-antivirus) and [Troubleshooting information](switch-to-mde-troubleshooting) (just in case something goes wrong while migrating).
- **Compatibility with applications**. For example, applications are crashing or experiencing unexpected behaviors after a device is onboarded to Microsoft Defender for Endpoint. See [Address unwanted behaviors in Microsoft Defender for Endpoint with exclusions, indicators, and other techniques](address-unwanted-behaviors-mde).

### Submit files for analysis

If you have a file that you think is wrongly detected as malware (a false positive), or a file that you suspect might be malware even though it wasn't detected (a false negative), you can submit the file to Microsoft for analysis. Your submission is scanned immediately and then reviewed by Microsoft security analysts. You can check the status of your submission on the [submission history page](https://www.microsoft.com/wdsi/submissionhistory).

Submitting files for analysis helps reduce false positives and false negatives for all customers. For more information, see the following articles:

- [Submit files for analysis](/en-us/defender-xdr/submission-guide)
- [Submit files in the Microsoft Defender portal](admin-submissions-mde) (Defender for Endpoint Plan 2 or Microsoft Defender XDR only)

### Suppress alerts

If you're getting alerts in the Microsoft Defender portal for tools or processes that you know aren't actually a threat, you can suppress those alerts.

To suppress an alert, you create a suppression rule and specify what actions to take for that alert on other identical alerts. You can create suppression rules for a specific alert on a single device, or for all alerts that have the same title in your organization.

For more information, see the following articles:

- [Suppress alerts](/en-us/defender-xdr/investigate-alerts?toc=/defender-endpoint/toc.json&amp;bc=/defender-endpoint/breadcrumb/toc.json#built-in-alert-tuning-rules)
- [Tech Community Blog: Introducing the new alert suppression experience](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/introducing-the-new-alert-suppression-experience/ba-p/3562719) (for Defender for Endpoint)