---
layout: Conceptual
title: Review or Edit Your Next-Generation Protection Policies in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-business/mdb-next-generation-protection
breadcrumb_path: /defender-business/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to view and edit your next-generation protection policies in Defender for Business. These policies pertain to antivirus and anti-malware protection.
author: chrisda
ms.author: chrisda
ms.topic: overview
ms.service: defender-business
ms.localizationpriority: medium
ms.date: 2025-09-24T00:00:00.0000000Z
ms.reviewer: nehabha
ms.collection:
- SMB
- m365-security
- tier1
locale: en-us
document_id: 9da093dd-f499-2a8a-6d09-b0c36ede9d67
document_version_independent_id: 9da093dd-f499-2a8a-6d09-b0c36ede9d67
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-business/mdb-next-generation-protection.md
site_name: Docs
depot_name: Learn.defender-business
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdb-next-generation-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-business/mdb-next-generation-protection.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b11ae577-8d18-47ab-998c-ea182a941e71
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/87b1d24d-826d-4337-90a0-b6c35e4561f2
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
platformId: e37f4198-0418-eb8c-7765-db504124dd52
---

# Review or Edit Your Next-Generation Protection Policies in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn

In Defender for Business, next-generation protection includes robust antivirus and anti-malware protection for computers and mobile devices. Default policies with recommended settings are included in Defender for Business. The default policies are designed to protect your devices and users without hindering productivity. However, you can customize your policies to suit your business needs.

You can choose from several options for managing your next-generation protection policies:

- Use the Microsoft Defender portal at https://security.microsoft.com, which we recommend if you're using the standalone version of Defender for Business without Intune.
- Use the Microsoft Intune admin center at https://intune.microsoft.com. Use this admin center if your subscription includes Intune.

# [Microsoft Defender portal](#tab/M365D)
1. Go to the [Microsoft Defender portal](https://security.microsoft.com), and sign in.
2. In the navigation pane, go to **Endpoints** &gt; **Configuration management** &gt; **Device configuration**. Policies are organized by operating system and policy type.
3. Select an operating system tab, such as **Windows**.
4. Under **Next-generation protection**, view your list of policies. At a minimum, it lists a default policy that uses recommended settings. This default policy is assigned to all onboarded devices running the operating system you selected in the previous step, such as **Windows**. You can:

    - Keep your default policy as currently configured.
    - Edit your default policy to make any needed adjustments.
    - Create a new policy.
5. Use one of the following procedures:

    | Task | Procedure |
    | --- | --- |
    | Edit your default policy | 1. In the **Next-generation protection** section, select your default policy, and then choose **Edit**.2. On the **General information** step, review the information. If necessary, edit the description, and then select **Next**.3. On the **Device groups** step, either use an existing group, or set up a new group. Then choose **Next**.4. On the **Configuration settings** step, review and if necessary, edit your security settings, and then choose **Next**. For more information about the settings, see Next-generation protection settings and options (in this article).5. On the **Review your policy** step, review your current settings. Select **Edit** to make any needed changes. Then select **Update policy**. |
    | Create a new policy | 1. In the **Next-generation protection** section, select **Add**.2. On the **General information** step, specify a name and description for your policy. You can also keep or change a policy order. See [Understand policy order in Microsoft Defender for Business](mdb-policy-order). Then select **Next**.3. On the **Device groups** step, you can either use an existing group, or create a new group. See [Device groups in Microsoft Defender for Business](mdb-create-edit-device-groups). Then choose **Next**.4. On the **Configuration settings** step, review and edit your security settings, and then choose **Next**. For more information about the settings, see Next-generation protection settings and options.5. On the **Review your policy** step, review your current settings. Select **Edit** to make any needed changes. Then select **Create policy**. |

# [Intune admin center](#tab/Intune)
1. Go to the [Microsoft Intune admin center](https://intune.microsoft.com) and sign in.
2. Select **Endpoint security**.
3. Select **Antivirus** to view your policies in that category.
4. Select an individual policy to edit.

    For help with managing your security settings in Intune, start with [Manage endpoint security in Microsoft Intune](/en-us/intune/intune-service/protect/endpoint-security).

---

## Next-generation protection settings and options

The following table lists settings and options for next-generation protection in Defender for Business.

| Setting | Description |
| --- | --- |
| **Real-time protection** |  |
| **Turn on real-time protection** | Enabled by default. Locates and stops malware from running on devices. *We recommend keeping real-time protection turned on.* When real-time protection is turned on, it configures the following settings: <br>- Behavior monitoring is turned on ([AllowBehaviorMonitoring](/en-us/windows/client-management/mdm/policy-csp-defender#defender-allowbehaviormonitoring)).<br>- All downloaded files and attachments are scanned ([AllowIOAVProtection](/en-us/windows/client-management/mdm/policy-csp-defender#defender-allowioavprotection)).<br>- Scripts used in Microsoft browsers are scanned ([AllowScriptScanning](/en-us/windows/client-management/mdm/policy-csp-defender#defender-allowscriptscanning)). |
| **Block at first sight** | Enabled by default. Blocks malware within seconds of detection, increases the time (in seconds) allowed to submit sample files for analysis, and sets your detection level to High. *We recommend keeping block at first sight turned on.* When block at first sight is turned on, it configures the following settings for Microsoft Defender Antivirus: <br>- Blocking and scanning of suspicious files is set to the High blocking level ([CloudBlockLevel](/en-us/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)).<br>- The number of seconds for a file to be blocked and checked is set to 50 seconds ([CloudExtendedTimeout](/en-us/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout)).<br><br>**Important** If block at first sight is turned off, it affects `CloudBlockLevel` and `CloudExtendedTimeout` for Microsoft Defender Antivirus. |
| **Turn on network protection** | Enabled in Block mode by default. Protects against phishing scams, exploit-hosting sites, and malicious content on the internet. It also prevents users from turning network protection off.  Network protection can be set to the following modes: <br>- **Block mode** is the default setting. It prevents users from visiting sites considered unsafe. *We recommend keeping network protection set to Block mode.*<br>- **Audit mode** allows users to visit sites that might be unsafe and tracks network activity to/from such sites.<br>- **Disabled mode** doesn't block users from visiting sites that might be unsafe and doesn't track network activity to or from such sites. |
| **Remediation** |  |
| **Action to take on potentially unwanted apps (PUA)** | Enabled by default. Blocks items detected as PUA. PUA can include advertising software, bundling software that offers to install other, unsigned software, and evasion software that attempts to evade security features. Although PUA isn't necessarily a virus, malware, or other type of threat, it can affect device performance. You can set PUA protection to the following modes: <br>- **Enabled** is the default setting. It blocks items detected as PUA on devices. *We recommend keeping PUA protection enabled.*<br>- **Audit mode** takes no action on items detected as PUA.<br>- **Disabled** doesn't detect or take action on items that might be PUA. |
| **Scan** |  |
| **Scheduled scan type** | Enabled in Quickscan mode by default. Specify a day and time to run weekly antivirus scans. The following scan type options are available: <br>- **Quickscan** checks locations, such as registry keys and startup folders, where malware could be registered to start along with a device. *We recommend using the quickscan option.*<br>- **Fullscan** checks all files and folders on a device.<br>- **Disabled** means no scheduled scans take place. Users can still run scans on their own devices. In general, we don't recommend disabling scheduled scans.<br><br>[Learn more about scan types](/en-us/defender-endpoint/schedule-antivirus-scans). |
| **Day of week to run a scheduled scan** | Select a day for your regular, weekly antivirus scans to run. |
| **Time of day to run a scheduled scan** | Select a time to run your regularly scheduled antivirus scans to run. |
| **Use low performance** | This setting is turned off by default. *We recommend keeping this setting turned off.* However, you can turn on this setting to limit the device memory and resources used during scheduled scans. **Important**: If you turn on **Use low performance**, it configures the following settings for Microsoft Defender Antivirus: <br>- [AllowArchiveScanning](/en-us/windows/client-management/mdm/policy-csp-defender#defender-allowarchivescanning): Archive files aren't scanned.<br>- [EnableLowCPUPriority](/en-us/windows/client-management/mdm/policy-csp-defender#defender-enablelowcpupriority): Scans are assigned a low CPU priority.<br>- [DisableCatchupFullScan](/en-us/windows/client-management/mdm/policy-csp-defender#defender-disablecatchupfullscan): No catch-ups scans if a full antivirus scan is missed.<br>- [DisableCatchupQuickScan](/en-us/windows/client-management/mdm/policy-csp-defender#defender-disablecatchupquickscan): No catch-ups scans if a quick antivirus scan is missed.<br>- [AvgCPULoadFactor](/en-us/windows/client-management/mdm/policy-csp-defender#defender-avgcpuloadfactor): Reduce the average CPU load factor during an antivirus scan from 50 percent to 20 percent. |
| **User experience** |  |
| **Allow users to access the Windows Security app** | Enable users to open the Windows Security app on their devices. Users can't override settings that you configure in Defender for Business, but they can run a quick scan or view any detected threats. |
| **Antivirus exclusions** | Exclusions are processes, files, or folders skipped by Microsoft Defender Antivirus scans. *In general, you shouldn't need to define exclusions.* Microsoft Defender Antivirus includes many automatic exclusions based on known operating system behavior and typical management files. Every exclusion reduces your level of protection, so it's important to consider carefully what exclusions to define. Before you add any exclusions, see [Manage exclusions for Microsoft Defender for Endpoint and Microsoft Defender Antivirus](/en-us/defender-endpoint/defender-endpoint-exclusions-overview). |
| **Process exclusions** | Prevent Microsoft Defender Antivirus from scanning files opened by specific processes. When you add a process to the process exclusion list, Microsoft Defender Antivirus doesn't scan files opened by that process. The process itself is scanned unless it's in the file exclusion list. For more information, see [Process exclusions](/en-us/defender-endpoint/microsoft-defender-antivirus-exclusions-overview#process-exclusions). |
| **File and folder exclusions** | Prevent Microsoft Defender Antivirus from scanning files by name, location, or extension. For more information, see [File and folder exclusions](/en-us/defender-endpoint/microsoft-defender-antivirus-exclusions-overview#file-and-folder-exclusions). |
| **Contextual exclusions** | Prevent Microsoft Defender Antivirus from scanning the file or folder only in a specific context, for example, a specific process accesses the file or only during a specific type of scan. For more information, see [Contextual exclusions](/en-us/defender-endpoint/microsoft-defender-antivirus-exclusions-overview#contextual-exclusions). |

## Other preconfigured settings in Defender for Business

Defender for Business preconfigures the following security settings:

- Scanning of removable drives is turned on ([AllowFullScanRemovableDriveScanning](/en-us/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanremovabledrivescanning)).
- Daily quick scans don't have a preset time ([ScheduleQuickScanTime](/en-us/windows/client-management/mdm/policy-csp-defender#defender-schedulequickscantime)).
- Security intelligence updates are checked before an antivirus scan runs ([CheckForSignaturesBeforeRunningScan](/en-us/windows/client-management/mdm/policy-csp-defender#defender-checkforsignaturesbeforerunningscan)).
- Security intelligence checks occur every four hours ([SignatureUpdateInterval](/en-us/windows/client-management/mdm/policy-csp-defender#defender-signatureupdateinterval)).

## How default settings in Defender for Business correspond to settings in Microsoft Intune

The following table describes preconfigured settings for Defender for Business and how those settings correspond to what you might see in Intune. If you use the [simplified configuration process in Defender for Business](mdb-setup-configuration), you don't need to edit these settings.

| Setting | Description |
| --- | --- |
| [Cloud protection](/en-us/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection) | Also known as cloud-delivered protection or Microsoft Advanced Protection Service (MAPS). Cloud protection works with Microsoft Defender Antivirus and the Microsoft cloud to identify new threats, sometimes even before any devices are affected. By default, [AllowCloudProtection](/en-us/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection) is turned on. [Learn more about cloud protection](/en-us/defender-endpoint/cloud-protection-microsoft-defender-antivirus). |
| [Monitoring for incoming and outgoing files](/en-us/windows/client-management/mdm/policy-csp-defender#defender-realtimescandirection) | To monitor incoming and outgoing files, [RealTimeScanDirection](/en-us/windows/client-management/mdm/policy-csp-defender#defender-realtimescandirection) is set to monitor all files. |
| [Scan network files](/en-us/windows/client-management/mdm/policy-csp-defender#defender-allowscanningnetworkfiles) | By default, [AllowScanningNetworkFiles](/en-us/windows/client-management/mdm/policy-csp-defender#defender-allowscanningnetworkfiles) isn't enabled, and network files aren't scanned. |
| [Scan email messages](/en-us/windows/client-management/mdm/policy-csp-defender#defender-allowemailscanning) | By default, [AllowEmailScanning](/en-us/windows/client-management/mdm/policy-csp-defender#defender-allowemailscanning) isn't enabled, and email messages aren't scanned. |
| [Number of days (0-90) to keep quarantined malware](/en-us/windows/client-management/mdm/policy-csp-defender#defender-daystoretaincleanedmalware) | By default, the [DaysToRetainCleanedMalware](/en-us/windows/client-management/mdm/policy-csp-defender#defender-daystoretaincleanedmalware) setting is set to zero (0) days. Artifacts that are in quarantine aren't removed automatically. |
| [Submit samples consent](/en-us/windows/client-management/mdm/policy-csp-defender#defender-submitsamplesconsent) | By default, [SubmitSamplesConsent](/en-us/windows/client-management/mdm/policy-csp-defender#defender-submitsamplesconsent) is set to send safe samples automatically. Examples of safe samples include `.bat`, `.scr`, `.dll`, and `.exe` files that don't contain personal data. If a file contains personal data, the user receives a request to allow the sample submission to proceed. [Learn more about cloud protection and sample submission](/en-us/defender-endpoint/cloud-protection-microsoft-antivirus-sample-submission). |
| [Scan removable drives](/en-us/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanremovabledrivescanning) | By default, [AllowFullScanRemovableDriveScanning](/en-us/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanremovabledrivescanning) is configured to scan removable drives, such as USB thumb drives on devices. [Learn more about anti-malware policy settings](/en-us/intune/configmgr/protect/deploy-use/endpoint-antimalware-policies#list-of-antimalware-policy-settings). |
| [Run daily quick scan time](/en-us/windows/client-management/mdm/policy-csp-defender#defender-schedulequickscantime) | By default, [ScheduleQuickScanTime](/en-us/windows/client-management/mdm/policy-csp-defender#defender-schedulequickscantime) is set to 2:00 AM. [Learn more about scan settings](/en-us/intune/configmgr/protect/deploy-use/endpoint-antimalware-policies#scan-settings). |
| [Check for signature updates before running scan](/en-us/windows/client-management/mdm/policy-csp-defender#defender-checkforsignaturesbeforerunningscan) | By default, [CheckForSignaturesBeforeRunningScan](/en-us/windows/client-management/mdm/policy-csp-defender#defender-checkforsignaturesbeforerunningscan) is configured to check for security intelligence updates before running antivirus/antimalware scans. [Learn more about scan settings](/en-us/intune/configmgr/protect/deploy-use/endpoint-antimalware-policies#scan-settings) and [Security intelligence updates](/en-us/defender-endpoint/microsoft-defender-antivirus-updates#security-intelligence-updates). |
| [How often (0-24 hours) to check for security intelligence updates](/en-us/windows/client-management/mdm/policy-csp-defender#defender-signatureupdateinterval) | By default, [SignatureUpdateInterval](/en-us/windows/client-management/mdm/policy-csp-defender#defender-signatureupdateinterval) is configured to check for security intelligence updates every four hours. [Learn more about scan settings](/en-us/intune/configmgr/protect/deploy-use/endpoint-antimalware-policies#scan-settings) and [Security intelligence updates](/en-us/defender-endpoint/microsoft-defender-antivirus-updates#security-intelligence-updates). |