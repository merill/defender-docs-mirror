---
layout: Conceptual
title: Configure scanning options for Microsoft Defender Antivirus - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/configure-advanced-scan-types-microsoft-defender-antivirus
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: You can configure Microsoft Defender Antivirus to scan email storage files, back-up or reparse points, network files, and archived files (such as .zip files).
ms.service: defender-endpoint
ms.localizationpriority: medium
author: chrisda
ms.author: chrisda
ms.custom: nextgen, msecd-doc-authoring-1015
ms.reviewer: pahuijbr
ms.subservice: ngp
ms.date: 2026-09-15T00:00:00.0000000Z
ms.collection:
- m365-security
- tier2
- mde-ngp
ms.topic: how-to
ai-usage: ai-assisted
locale: en-us
document_id: 78720825-38aa-829e-caa5-7f6010b40d7a
document_version_independent_id: 78720825-38aa-829e-caa5-7f6010b40d7a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/configure-advanced-scan-types-microsoft-defender-antivirus.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-advanced-scan-types-microsoft-defender-antivirus
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/configure-advanced-scan-types-microsoft-defender-antivirus.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: b85f25ac-7152-c279-5197-b3f184472f4e
---

# Configure scanning options for Microsoft Defender Antivirus - Microsoft Defender for Endpoint | Microsoft Learn

You can configure Microsoft Defender Antivirus to scan email storage files, reparse points, network files, and archived files (such as .zip files).

Use Microsoft Intune, Microsoft Configuration Manager, Group Policy, PowerShell, or WMI to set up these scan options.

> 
> Microsoft Intune is the recommended tool for configuring and distributing Defender for Endpoint features to devices. However, Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have Intune, you can use any of the other methods in this article. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

## Use Microsoft Intune to configure scanning options

In Microsoft Intune, use device restriction profiles to set up scanning options. For details, see the following articles:

- [Configure device restriction settings in Microsoft Intune](/en-us/intune/intune-service/configuration/device-restrictions-configure)
- [Microsoft Defender Antivirus device restriction settings for Windows 10 in Intune](/en-us/intune/intune-service/configuration/device-restrictions-windows-10#microsoft-defender-antivirus)

## Prerequisites

### Supported operating systems

These scanning options are supported on the following operating systems:

- Windows

## Use Microsoft Configuration Manager to configure scanning options

For details on configuring Microsoft Configuration Manager (current branch), see [How to create and deploy anti-malware policies: Scan settings](/en-us/intune/configmgr/protect/deploy-use/endpoint-antimalware-policies#scan-settings).

## Use Group Policy to configure scanning options

Tip

Download the Group Policy Reference Spreadsheet. It lists policy settings for computer and user setups in the Administrative template files for Windows. Use it when you edit Group Policy Objects. Here are the most recent versions:

- [Group Policy Settings Reference Spreadsheet for Windows 10 2022 Update (22H2)](https://www.microsoft.com/download/details.aspx?id=104678)
- [Group Policy Settings Reference Spreadsheet for Windows 11 2025 Update (25H2)](https://www.microsoft.com/download/details.aspx?id=108395)

1. In Centralized Group Policy, open the [Group Policy Management Console (GPMC)](/en-us/windows-server/identity/ad-ds/manage/group-policy/group-policy-management-console) on your Group Policy management computer.
2. In the GPMC console tree, expand Group Policy Objects in the forest and domain containing the GPO you want to edit.
3. Right-click the GPO, and then select **Edit**.
4. In the **Group Policy Management Editor**, go to **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus**.

    Note

    Group Policy paths before Windows 10, version 2004 (May 2020) might use *Windows* Defender Antivirus instead of *Microsoft* Defender Antivirus. Both names refer to the same policy location.
5. In the details pane of **Microsoft Defender Antivirus**, select a location from the Settings and locations section.
6. In the details pane of the selected location, open the setting you want to configure. To open and configure a setting, use any of the following methods:

    - Double-click the setting.
    - Right-click the setting, and then select **Edit**.
    - Select the setting, and then select **Action** &gt; **Edit**.
7. In the setting window that opens, configure the setting, and then select **OK**.

    Repeat this step as many times as necessary.

Tip

You can also configure Group Policy locally on individual devices by using the Local Group Policy Editor (`gpedit.msc`). Navigate to the same path: **Computer configuration** &gt; **Administrative templates** &gt; **Windows components** &gt; **Microsoft Defender Antivirus**.

### Settings and locations

The following table lists the available scanning policy settings, their Group Policy locations, and the corresponding PowerShell parameters.

| Policy item and location | Default setting(if not configured) | PowerShell`Set-MpPreference`parameteror WMI property for`MSFT_MpPreference`class |
| --- | --- | --- |
| Email scanning **Scan** &gt; **Turn on e-mail scanning**See Email scanning limitations (in this article) | Disabled | `-DisableEmailScanning` |
| Script scanning | Enabled | This policy setting allows you to configure script scanning. If you enable or don't configure this setting, script scanning is enabled. See [Defender/AllowScriptScanning](/en-us/windows/client-management/mdm/policy-csp-defender) |
| Scan [reparse points](/en-us/windows/win32/fileio/reparse-points)**Scan** &gt; **Turn on reparse point scanning** | Disabled | Not available See [Reparse points](/en-us/windows/win32/fileio/reparse-points) |
| Scan mapped network drives**Scan** &gt; **Run full scan on mapped network drives** | Disabled | `-DisableScanningMappedNetworkDrivesForFullScan` |
| Scan archive files (such as .zip or .rar files). **Scan** &gt; **Scan archive files** | Enabled | `-DisableArchiveScanning`The [extensions exclusion list](microsoft-defender-antivirus-exclusions-overview) takes precedence over this setting. |
| Scan files on the network **Scan** &gt; **Scan network files** | Disabled | `-DisableScanningNetworkFiles` |
| Scan packed executables**Scan** &gt; **Scan packed executables** | Enabled | Not available Scan packed executables were removed from the following templates:- Administrative Templates (.admx) for Windows 11 2023 Update (23H2)- Administrative Templates (.admx) for Windows 11 2022 Update (22H2) - v3.0 - Administrative Templates (.admx) for Windows 11 2022 Update (22H2)- Administrative Templates (.admx) for Windows 11 October 2021 Update (21H2) |
| Scan removable drives during full scans only**Scan** &gt; **Scan removable drives** | Disabled | `-DisableRemovableDriveScanning` |
| Specify the level of subfolders within an archive folder to scan <br>**Scan** &gt; **Specify the maximum depth to scan archive files** | 0 | Not available |
| Specify the maximum CPU load (as a percentage) during a scan. <br>**Scan** &gt; **Specify the maximum percentage of CPU utilization during a scan** | 50 | `-ScanAvgCPULoadFactor` The maximum CPU load isn't a hard limit, but is guidance for the scanning engine to not exceed the maximum on average. Manual scans ignore this setting and run without any CPU limits. |
| Specify the maximum size (in kilobytes) of archive files that should be scanned.**Scan** &gt; **Specify the maximum size of archive files to be scanned** | No limit | Not available The default value of 0 applies no limit |
| Configure low CPU priority for scheduled scans**Scan** &gt; **Configure low CPU priority for scheduled scans** | Disabled | Not available |
| Configure scanning of network files **Scan** &gt; **Configure scanning of network files** | Disabled | -DisableScanningNetworkFiles |
| CPU throttling type **Scan** &gt; **CPU throttling type** | Disabled | -ThrottleForScheduledScanOnly |
| Scan excluded files and directories during quick scan **Scan** &gt; **Scan excluded files and directories during quick scan** | Disabled | Not available |

Note

If real-time protection is turned on, files are scanned before they're accessed and executed. The scanning scope includes all files, such as files on mounted removable media, like USB drives. If the device performing the scan has real-time protection or on-access protection turned on, the scan also includes network shares.

Tip

If you have a Network-Attached Storage (NAS) or Storage Area Network (SAN), you can use Internet Content Adaption Protocol (ICAP) scanning with the Microsoft Defender Antivirus engine. For more information, see **[Tech Community Blog: MetaDefender ICAP with Windows Defender Antivirus: World-class security for hybrid environments](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/metadefender-icap-with-windows-defender-antivirus-world-class/ba-p/800234)**.

## Use PowerShell to configure scanning options

For more information on how to use PowerShell with Microsoft Defender Antivirus, see the following articles:

- [Manage Microsoft Defender Antivirus with PowerShell cmdlets](use-powershell-cmdlets-microsoft-defender-antivirus)
- [Microsoft Defender Antivirus cmdlets](/en-us/powershell/module/defender/)

## Use WMI to configure scanning options

See [Windows Defender WMIv2 APIs](/en-us/previous-versions/windows/desktop/defender/windows-defender-wmiv2-apis-portal).

## Email scanning limitations

Email scanning enables scanning of email files used by Outlook and other mail clients during on-demand and scheduled scans. Embedded objects within email (such as attachments and archived files) are also scanned. The following file format types can be scanned and remediated:

- `DBX`
- `MBX`
- `MIME`

`PST` files used by Outlook 2003 or older (where the archive type is set to nonunicode) are also scanned, but Microsoft Defender Antivirus can't remediate threats that are detected inside `PST` files.

If Microsoft Defender Antivirus detects a threat inside an email message, the following information is displayed to assist you in identifying the compromised email so you can remediate the threat manually:

- Email subject
- Attachment name

## Scanning mapped network drives

On all supported operating systems, only the network drives that are mapped at system level are scanned. User-level mapped network drives aren't scanned. User-level mapped network drives are those that a user maps in their session manually and using their own credentials.