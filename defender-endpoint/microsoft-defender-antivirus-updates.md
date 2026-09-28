---
layout: Conceptual
title: Microsoft Defender Antivirus security intelligence and product updates and support - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/microsoft-defender-antivirus-updates
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn about security intelligence updates, platform updates, and engine updates for Microsoft Defender Antivirus, including rollback and support options.
ms.service: defender-endpoint
ms.localizationpriority: high
ms.date: 2026-05-14T00:00:00.0000000Z
ms.topic: reference
author: chrisda
ms.author: chrisda
ms.subservice: ngp
ms.custom: msecd-doc-authoring-1012
locale: en-us
document_id: ad5e7a79-a1eb-6bb6-ef03-4a2aea5a3763
document_version_independent_id: ad5e7a79-a1eb-6bb6-ef03-4a2aea5a3763
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/microsoft-defender-antivirus-updates.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: microsoft-defender-antivirus-updates
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/microsoft-defender-antivirus-updates.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 70a41e49-2d07-50c5-31d1-9cc2fbfc9225
---

# Microsoft Defender Antivirus security intelligence and product updates and support - Microsoft Defender for Endpoint | Microsoft Learn

Keeping Microsoft Defender Antivirus up to date is critical to ensure your devices are protected against new malware and attack techniques. Update your antivirus protection, even if Microsoft Defender Antivirus is running in [passive mode](microsoft-defender-antivirus-compatibility). You can find the latest engine, platform, and signature date in [Security intelligence updates for Microsoft Defender Antivirus and other Microsoft anti-malware](https://www.microsoft.com/wdsi/defenderupdates).

This article is aimed at **Windows** devices, and includes information about security intelligence updates and product updates.

For a list of the latest **security intelligence and product versions**, see [Microsoft Defender for Endpoint supported releases](microsoft-defender-endpoint-releases#microsoft-defender-antivirus-releases).

## Security intelligence updates

Microsoft Defender Antivirus uses [cloud-delivered protection](cloud-protection-microsoft-defender-antivirus), also known as *Microsoft Advanced Protection Service*, or *MAPS*. Defender Antivirus periodically downloads dynamic security [intelligence updates](https://www.microsoft.com/wdsi/defenderupdates). These updates don't replace regular security intelligence updates. Engine updates are included with security intelligence updates and are released monthly.

Updates are released under the following KBs:

- Microsoft Defender Antivirus: KB2267602
- System Center Endpoint Protection: KB2461484

[Cloud-delivered protection](cloud-protection-microsoft-defender-antivirus) is always on and requires an active connection to the internet. Security intelligence updates occur on a scheduled cadence that you can configure using a policy.

## Product updates

Microsoft Defender Antivirus requires monthly updates (KB4052623) known as *platform updates*.

You can manage the distribution of updates using one of the following methods:

- [Windows Server Update Service (WSUS)](/en-us/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus)
- [Microsoft Configuration Manager](/en-us/intune/configmgr/sum/understand/software-updates-introduction)
- The usual methods you use to deploy Microsoft and Windows updates to endpoints in your network.
- UNC file share

For more information, see [Manage the sources for Microsoft Defender Antivirus protection updates](manage-protection-updates-microsoft-defender-antivirus).

### Important points about product updates

- Monthly updates are released in phases, resulting in multiple packages visible in your [Windows Server Update Services](/en-us/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus).
- The following section lists changes included in the broad release channel. See the [latest broad channel release](https://definitionupdates.microsoft.com/packages?action=info).
- To learn more about the gradual rollout process, and to see more information about the next release, see [Manage the gradual rollout process for Microsoft Defender updates](manage-gradual-rollout).
- To learn more about security intelligence updates, see [Security intelligence updates for Microsoft Defender Antivirus and other Microsoft anti-malware](https://www.microsoft.com/wdsi/defenderupdates).
- If you're looking for a list of Microsoft Defender processes, see the spreadsheet provided at [Enable access to Microsoft Defender for Endpoint service URLs in the proxy server](configure-environment#enable-access-to-microsoft-defender-for-endpoint-service-urls-in-the-proxy-server). The sheet also lists the services and their associated URLs that your network must be able to connect to.
- Platform updates can be temporarily postponed if other protection features, such as [Endpoint DLP](/en-us/purview/endpoint-dlp-getting-started) or [Device Control](device-control-report), are actively monitoring running processes. Platform updates are retried after a reboot or when all monitored services are stopped.
- In the **Microsoft Configuration Manager / Windows Server Update Services** (ConfigMgr/WSUS) catalog, the category **Microsoft Defender for Endpoint** includes updates for the `MSSense` service in [KB5005292](https://www.catalog.update.microsoft.com/Search.aspx?q=KB5005292). KB5005292 includes updates and fixes to the Microsoft Defender for Endpoint **endpoint detection and response** (EDR) sensor. For more information, see [Microsoft Defender for Endpoint update for EDR Sensor](https://support.microsoft.com/servicing/management-tools/microsoft-defender/update/microsoft-defender-for-endpoint-update-for-edr-sensor) and [What's new in Microsoft Defender for Endpoint on Windows](microsoft-defender-endpoint-releases#windows-releases).

### Previous version updates: Technical upgrade support only

After a new package version is released, support for the previous two versions is reduced to technical upgrade support only. For more information about previous versions, see [Microsoft Defender Antivirus updates: Previous versions for technical upgrade support](msda-updates-previous-versions-technical-upgrade-support).

## Microsoft Defender Antivirus platform and engine support

Platform and engine updates are provided on a monthly cadence. To be fully supported, keep current with the latest platform and engine updates. The support structure is dynamic, with two phases based on the availability of the latest platform and engine version:

- **Security and Critical Updates servicing phase** - When running the latest platform and engine version, you're eligible to receive both Security and Critical updates to the anti-malware platform.
- **Technical Upgrade Support (Only) phase** - After a new platform and engine version is released, support for older versions (N-2) reduces to [technical upgrade support only](msda-updates-previous-versions-technical-upgrade-support). Platform and engine versions older than N-2 are no longer supported. Technical upgrade support continues to be provided for upgrades from the Windows 10 release version (see Platform version included with Windows 10 releases) to the latest platform version.

During the technical upgrade support (only) phase, commercially reasonable support incidents are provided through Microsoft Customer Service & Support and Microsoft's managed support offerings (such as Premier Support). If a support incident requires escalation to development for further guidance, requires a nonsecurity update, or requires a security update, customers are asked to upgrade to the latest platform version or an intermediate update.

Note

If you're manually deploying Microsoft Defender Antivirus Platform Update, or if you're using a script or a non-Microsoft management product to deploy Microsoft Defender Antivirus Platform Update, make sure that version `4.18.2001.10` is installed from the [Microsoft Update Catalog](https://www.catalog.update.microsoft.com/Search.aspx?q=4.18.2001.10) before the latest version of Platform Update (N-2) is installed.

## How to install an update

To install the latest security intelligence and antivirus engine updates, you can use any of the following methods:

- Windows Update
- Windows Update server (WSUS)
- Software Update Point (SUP)
- [File server](manage-protection-updates-microsoft-defender-antivirus)
- Windows Security app: See [Microsoft Defender Antivirus in the Windows Security app](microsoft-defender-security-center-antivirus).
- [MpCmdRun command-line utility](command-line-arguments-microsoft-defender-antivirus):

    1. In an elevated Command Prompt (a Command Prompt window you opened by selecting **Run as administrator**), run the following command:

        Tip

        This command changes the directory to the latest version of &lt;antimalware platform version&gt; in `%ProgramData%\Microsoft\Windows Defender\Platform\<antimalware platform version>`. If that path doesn't exist, it goes to `%ProgramFiles%\Windows Defender`.

        ```dos
        (set "_done=" & if exist "%ProgramData%\Microsoft\Windows Defender\Platform\" (for /f "delims=" %d in ('dir "%ProgramData%\Microsoft\Windows Defender\Platform" /ad /b /o:-n 2^>nul') do if not defined _done (cd /d "%ProgramData%\Microsoft\Windows Defender\Platform\%d" & set _done=1)) else (cd /d "%ProgramFiles%\Windows Defender")) >nul 2>&1
        ```
    2. Run one of the following commands:

        ```dos
        MpCmdRun.exe -SignatureUpdate
        
        MpCmdRun.exe -SignatureUpdate -UNC \\FileServer\ShareName
        
        MpCmdRun.exe -SignatureUpdate -MMPC
        ```

    For more information, see [Manage the sources for Microsoft Defender Antivirus protection updates](manage-protection-updates-microsoft-defender-antivirus).

To get the latest platform updates, you can use any of the following methods:

- Windows Update
- Windows Update server (WSUS)
- Software Update Point (SUP)
- Windows Security app: See [Microsoft Defender Antivirus in the Windows Security app](microsoft-defender-security-center-antivirus)
- The [Windows Update Catalog](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4052623)

## How to roll back an update

If you encounter issues after an update, you can roll back to the previous or inbox version.

| Scenario | Command |
| --- | --- |
| Roll security intelligence updates back to the previous or to the original inbox version | `MpCmdRun.exe -RemoveDefinitions -All` |
| Roll the engine version back to the previous version | `MpCmdRun.exe -RemoveDefinitions -Engine` |
| Remove only dynamically downloaded security intelligence updates | `MpCmdRun.exe -RemoveDefinitions -DynamicSignatures` |
| Roll a platform update back to the previous version | `MpCmdRun.exe -RevertPlatform` |
| Roll updates back to the version shipped with the operating system (`%ProgramFiles%\Windows Defender`) | `MpCmdRun.exe -ResetPlatform` |

For more information, see [Configure and manage Microsoft Defender Antivirus with the MpCmdRun command-line tool](command-line-arguments-microsoft-defender-antivirus).

## Platform version included with Windows 10 releases

The table provides the Microsoft Defender Antivirus platform and engine versions that are shipped with the latest Windows 10 releases:

| Windows 10 release | Platform version | Engine version | Support phase |
| --- | --- | --- | --- |
| 2004 (20H1/20H2) | `4.18.1909.6` | `1.1.17000.2` | Technical upgrade support (only) |
| 1909 (19H2) | `4.18.1902.5` | `1.1.16700.3` | Technical upgrade support (only) |
| 1903 (19H1) | `4.18.1902.5` | `1.1.15600.4` | Technical upgrade support (only) |
| 1809 (RS5) | `4.18.1807.5` | `1.1.15000.2` | Technical upgrade support (only) |
| 1803 (RS4) | `4.13.17134.1` | `1.1.14600.4` | Technical upgrade support (only) |
| 1709 (RS3) | `4.12.16299.15` | `1.1.14104.0` | Technical upgrade support (only) |
| 1703 (RS2) | `4.11.15603.2` | `1.1.13504.0` | Technical upgrade support (only) |
| 1607 (RS1) | `4.10.14393.3683` | `1.1.12805.0` | Technical upgrade support (only) |

For Windows 10 release information, see the [Windows lifecycle fact sheet](/en-us/lifecycle/faq/windows).

Note

- Windows Server 2016 ships with the same platform version as RS1 and falls under the same support phase: Technical upgrade support (only).
- Windows Server 2019 ships with the same platform version as RS5 and falls under the same support phase: Technical upgrade support (only).

## Updates for Deployment Image Servicing and Management (DISM)

To avoid a gap in protection, keep your OS installation images up to date with the latest antivirus and anti-malware updates. Updates are available for:

- Windows 10 and 11 (Enterprise, Pro, and Home editions)
- Windows Server 2012 R2 and later
- Azure Stack HCI OS, version 23H2 and later
- WIM and VHD(x) files

Updates are released for x86, x64, and Arm64 Windows architecture.

For more information, see [Microsoft Defender update for Windows operating system installation images](https://support.microsoft.com/servicing/Management-Tools/microsoft-defender/update/microsoft-defender-update-for-windows-operating-system-installation-images).

After a new package version is released, support for the previous two versions is reduced to technical support only. To view a list of previous versions, see [Previous DISM updates](msda-updates-previous-versions-technical-upgrade-support#previous-dism-updates-no-longer-supported).

### 1.431.97.0

- Defender version: `1.431.97.0`
- Security intelligence version: `1.431.97.0`
- Platform version: `4.18.25050.5`
- Engine version: `1.25050.6`

#### 1.431.97.0 Fixes

- None

#### 1.431.97.0 Additional information

- None

### 1.431.54.0

- Defender version: `1.431.54.0`
- Security intelligence version: `1.431.54.0`
- Platform version: `4.18.25050.5`
- Engine version: `1.25050.2`

#### 1.431.54.0 Fixes

- None

#### 1.431.54.0 Additional information

- None

### 1.429.122.0

- Defender version: `1.429.122.0`
- Security intelligence version: `1.429.122.0`
- Platform version: `4.18.25040.2`
- Engine version: `1.25040.1`

#### 1.429.122.0 Fixes

- None

#### 1.429.122.0 Additional information

- None