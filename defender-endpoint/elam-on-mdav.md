---
layout: Conceptual
title: Early Launch Antimalware (ELAM) and Microsoft Defender Antivirus - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/elam-on-mdav
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how Microsoft Defender Antivirus uses the Early Launch Antimalware (ELAM) driver to detect rootkits and malicious drivers during boot.
author: chrisda
ms.author: chrisda
ms.reviewer: yongrhee
ms.service: defender-endpoint
ms.topic: overview
ms.date: 2026-05-14T00:00:00.0000000Z
ms.subservice: ngp
ms.localizationpriority: medium
ms.custom: partner-contribution, msecd-doc-authoring-1012
locale: en-us
document_id: ee544ebb-4534-4f82-3ae5-f29e9c5ba0e1
document_version_independent_id: ee544ebb-4534-4f82-3ae5-f29e9c5ba0e1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/elam-on-mdav.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: elam-on-mdav
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/elam-on-mdav.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 03db7ef5-2e34-ddfc-60ec-423d80a8dfe8
---

# Early Launch Antimalware (ELAM) and Microsoft Defender Antivirus - Microsoft Defender for Endpoint | Microsoft Learn

Detecting malware that starts early in the boot cycle was a challenge before Windows 8. Starting with Windows 8 and Windows Server 2012, Windows introduced the [Early Launch Antimalware (ELAM)](/en-us/windows/compatibility/early-launch-antimalware) driver. Microsoft Defender Antivirus uses the ELAM driver (Wdboot.sys) to combat early boot threats (for example, rootkits or malicious drivers that can hide from detection). The Wdboot.sys driver starts before other boot-start drivers. ELAM evaluates other drivers and helps the Windows kernel decide whether to initialize them.

## Supported operating systems

- Windows 8 or later
- Windows Server 2012 or later

## ELAM detection logging

ELAM detections are logged in the same location as other Microsoft Defender Antivirus detections, for example, [Event ID 1006](troubleshoot-microsoft-defender-antivirus).

## Keep the ELAM driver up to date

The ELAM driver is included in the monthly [platform update](microsoft-defender-antivirus-updates).

## Modify the ELAM policy

To modify the ELAM policy, use Group Policy:

**Computer Configuration** &gt; **Administrative Templates** &gt; **System** &gt; **Early Launch Antimalware** &gt; **Boot-Start Driver Initialization Policy**

## Verify the ELAM driver is loaded

Open **Registry Editor** and go to **HKEY\_LOCAL\_MACHINE** &gt; **SYSTEM** &gt; **CurrentControlSet** &gt; **Control** &gt; **EarlyLaunch**.

The string key named **BackupPath** should have the value `C:\Windows\ELAMBKUP`.

For more information, see [ELAM Driver Requirements](/en-us/windows-hardware/drivers/install/elam-driver-requirements).

## Revert the ELAM driver to a previous version

In an elevated Command Prompt (a Command Prompt window you opened by selecting **Run as administrator**), run the following commands:

Tip

The first command changes the directory to the latest version of &lt;antimalware platform version&gt; in `%ProgramData%\Microsoft\Windows Defender\Platform\<antimalware platform version>`. If that path doesn't exist, it goes to `%ProgramFiles%\Microsoft Defender`.

```dos
(set "_done=" & if exist "%ProgramData%\Microsoft\Windows Defender\Platform\" (for /f "delims=" %d in ('dir "%ProgramData%\Microsoft\Windows Defender\Platform" /ad /b /o:-n 2^>nul') do if not defined _done (cd /d "%ProgramData%\Microsoft\Windows Defender\Platform\%d" & set _done=1)) else (cd /d "%ProgramFiles%\Windows Defender")) >nul 2>&1

MpCmdRun.exe -RevertPlatform
```

For more information, see [Manage the sources for Microsoft Defender Antivirus protection updates](manage-protection-updates-microsoft-defender-antivirus).