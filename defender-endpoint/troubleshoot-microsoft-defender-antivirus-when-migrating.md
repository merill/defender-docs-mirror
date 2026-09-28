---
layout: FAQ
title: Troubleshoot Microsoft Defender Antivirus while migrating from a non-Microsoft solution - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-microsoft-defender-antivirus-when-migrating
summary: >
  <p><strong>Applies to:</strong></p>

  <ul>

  <li><a href="microsoft-defender-endpoint">Microsoft Defender for Endpoint Plan 1</a></li>

  <li><a href="microsoft-defender-endpoint">Microsoft Defender for Endpoint Plan 2</a></li>

  <li><a href="https://www.microsoft.com/windows/comprehensive-security">Microsoft Defender Antivirus</a></li>

  </ul>

  <p><strong>Platforms</strong></p>

  <ul>

  <li>Windows</li>

  </ul>

  <p>Use this article to resolve issues while migrating from a non-Microsoft security solution to Microsoft Defender Antivirus.</p>
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Troubleshoot common errors when migrating to Microsoft Defender Antivirus.
ms.service: defender-endpoint
ms.localizationpriority: medium
ms.topic: faq
author: chrisda
ms.author: chrisda
ms.custom: nextgen
ms.reviewer: yonghree
ms.subservice: ngp
ms.collection:
- m365-security
- tier1
- mde-ngp
search.appverid: met150
ms.date: 2025-03-26T00:00:00.0000000Z
locale: en-us
document_id: e05a91dd-9a34-6f7b-7714-355016157ada
document_version_independent_id: e05a91dd-9a34-6f7b-7714-355016157ada
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/troubleshoot-microsoft-defender-antivirus-when-migrating.yml
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: troubleshoot-microsoft-defender-antivirus-when-migrating
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/troubleshoot-microsoft-defender-antivirus-when-migrating.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 21d052e6-ed8d-be31-6ce1-a348b021102a
---

# Troubleshoot Microsoft Defender Antivirus while migrating from a non-Microsoft solution - Microsoft Defender for Endpoint | Microsoft Learn

**Applies to:**

- [Microsoft Defender for Endpoint Plan 1](microsoft-defender-endpoint)
- [Microsoft Defender for Endpoint Plan 2](microsoft-defender-endpoint)
- [Microsoft Defender Antivirus](https://www.microsoft.com/windows/comprehensive-security)

**Platforms**

- Windows

Use this article to resolve issues while migrating from a non-Microsoft security solution to Microsoft Defender Antivirus.

## Review event logs

1. Open the Event viewer app by selecting the Search icon in the taskbar, and searching for *event viewer*.

    Information about Microsoft Defender Antivirus can be found under **Applications and Services Logs** &gt; **Microsoft** &gt; **Windows** &gt; **Windows Defender**.
2. From there, select **Open** underneath **Operational**.

    Selecting an event from the details pane shows you more information about an event in the lower pane, under the **General** and **Details** tabs.

## Microsoft Defender Antivirus doesn't start.

This issue can manifest in the form of several different event IDs, all of which have the same underlying cause.

### Associated event IDs

#### Event ID 15

- **Log name**: Application
- **Description**: Updated Windows Defender status successfully to SECURITY\_PRODUCT\_STATE\_OFF.
- **Source**: Security Center

#### Event ID 5007

- **Log name**: Microsoft-Windows-Windows Defender/Operational
- **Description**: Microsoft Defender Antivirus Configuration has changed. If this is an unexpected event, you should review the settings as this issue could be due to malware. **Old value:** Default\IsServiceRunning = 0x0 **New value:** HKLM\SOFTWARE\Microsoft\Windows Defender\IsServiceRunning = 0x1
- **Source**: Windows Defender

#### Event ID 5010

- **Log name**: Microsoft-Windows-Windows Defender/Operational
- **Description**: Microsoft Defender Antivirus scanning for spyware and other potentially unwanted software is disabled.
- **Source**: Windows Defender

### How to tell if Microsoft Defender Antivirus doesn't start because a non-Microsoft antivirus is installed.

On a Windows 10 or Windows 11 device, if you aren't using Microsoft Defender for Endpoint, and you have a non-Microsoft antivirus installed, then Microsoft Defender Antivirus is automatically turned off. If you're using Microsoft Defender for Endpoint with a non-Microsoft antivirus installed, Microsoft Defender Antivirus starts in passive mode, with reduced functionality.

Tip

The scenario described earlier applies only to Windows 10 and Windows 11. Other versions of Windows have [different responses](microsoft-defender-antivirus-compatibility) to Microsoft Defender Antivirus being run alongside non-Microsoft security software.

#### Use Services app to check if Microsoft Defender Antivirus is turned off.

To open the Services app, select the Search icon from the taskbar and search for *services*. You can also open the app from the command-line by typing *services.msc*.

Information about Microsoft Defender Antivirus is listed within the Services app under **Windows Defender** &gt; **Operational**. The antivirus service name is *Microsoft Defender Antivirus Service*.

While checking the app, you might see that *Microsoft Defender Antivirus Service* is set to manual, but when you try to start this service manually, you get a warning. The warning might say, *The Microsoft Defender Antivirus Service service on Local Computer started and then stopped. Some services stop automatically if they aren't in use by other services or programs.*

This issue indicates that Microsoft Defender Antivirus was automatically turned off to preserve compatibility with a non-Microsoft antivirus.

#### Generate a detailed report

You can generate a detailed report about currently active group policies by opening a command prompt in **Run as admin** mode, then entering the following command:

```console
GPresult.exe /h gpresult.html
```

This command generates a report located at *./gpresult.html*. Open this file and you might see the following results, depending on how Microsoft Defender Antivirus was turned off.

##### Group policy results

##### If security settings are implemented via group policy (GPO) at the domain or local level, or through System center configuration manager (SCCM)

Within the GPResults report, under the heading, *Windows Components/Microsoft Defender Antivirus*, you might see something like the following entry, indicating that Microsoft Defender Antivirus is turned off.

- **Policy**: Turn off Microsoft Defender Antivirus
- **Setting**: Enabled
- **Winning GPO**: Win10-Workstations

###### If security settings are implemented via Group policy preference (GPP)

Under the heading, *Registry item (Key path: HKEY\_LOCAL\_MACHINE\SOFTWARE\Policies\Microsoft\Windows Defender, Value name: DisableAntiSpyware)*, you might see something like the following entry, indicating that Microsoft Defender Antivirus is turned off.

- **DisableAntiSpyware**
- Winning GPO: Win10-Workstations
- Result: Success
- **General**
- Action: Update
- **Properties**
- Hive: HKEY\_LOCAL\_MACHINE
- Key path: SOFTWARE\Policies\Microsoft\Windows Defender
- Value name: DisableAntiSpyware
- Value type: REG\_DWORD
- Value data: 0x1 (1)

###### If security settings are implemented via registry key

The report might contain the following text, indicating that Microsoft Defender Antivirus is turned off:

> 
> Registry (regedit.exe)
> 
> HKEY\_LOCAL\_MACHINE\SOFTWARE\Policies\Microsoft\Windows Defender DisableAntiSpyware (dword) 1 (hex)

###### If security settings are set in Windows or your Windows Server image

Your imagining admin might have set the security policy, [DisableAntiSpyware](/en-us/windows-hardware/customize/desktop/unattend/security-malware-windows-defender-disableantispyware), locally via *GPEdit.exe*, *LGPO.exe*, or by modifying the registry in their task sequence. You can [configure a Trusted Image Identifier](/en-us/windows-hardware/manufacture/desktop/configure-a-trusted-image-identifier-for-windows-defender) for Microsoft Defender Antivirus.

### Turn Microsoft Defender Antivirus back on

Microsoft Defender Antivirus automatically turns on if no other antivirus is currently active. You need to turn the non-Microsoft antivirus off to ensure Microsoft Defender Antivirus can run with full functionality.

Warning

Solutions suggesting that you edit the Windows Defender start values for `wdboot`, `wdfilter`, `wdnisdrv`, `wdnissvc`, and `windefend` in `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services` are unsupported, and might force you to reimage your system.

Passive mode is available if you start using Microsoft Defender for Endpoint and a non-Microsoft antivirus together with Microsoft Defender Antivirus. Passive mode allows Microsoft Defender Antivirus to scan files and update itself, but it doesn't remediate threats in passive mode. In addition, behavior monitoring via [Real Time Protection](configure-real-time-protection-microsoft-defender-antivirus) isn't available in passive mode, unless [Endpoint data loss prevention (DLP)](/en-us/purview/endpoint-dlp-getting-started) is deployed.

Another feature, known as [limited periodic scanning](limited-periodic-scanning-microsoft-defender-antivirus), is available to end-users when Microsoft Defender Antivirus is set to turn off automatically. This feature allows Microsoft Defender Antivirus to scan files periodically alongside a non-Microsoft antivirus, using a limited number of detections.

Important

Limited periodic scanning isn't recommended in enterprise environments. The detection, management, and reporting capabilities available when running Microsoft Defender Antivirus in this mode are reduced as compared to active mode.

Tip

If you're looking for Antivirus related information for other platforms, see:

- [Set preferences for Microsoft Defender for Endpoint on macOS](mac-preferences)
- [Microsoft Defender for Endpoint on Mac](microsoft-defender-endpoint-mac)
- [macOS Antivirus policy settings for Microsoft Defender Antivirus for Intune](/en-us/intune/intune-service/protect/antivirus-microsoft-defender-settings-macos)
- [Set preferences for Microsoft Defender for Endpoint on Linux](linux-preferences)
- [Microsoft Defender for Endpoint on Linux](microsoft-defender-endpoint-linux)
- [Configure Defender for Endpoint on Android features](android-configure)
- [Configure Microsoft Defender for Endpoint on iOS features](ios-configure-features)