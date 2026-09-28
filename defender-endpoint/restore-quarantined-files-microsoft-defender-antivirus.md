---
layout: Conceptual
title: Restore quarantined files in Microsoft Defender Antivirus - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/restore-quarantined-files-microsoft-defender-antivirus
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: You can restore quarantined files and folders in Microsoft Defender Antivirus.
ms.service: defender-endpoint
ms.localizationpriority: medium
author: chrisda
ms.author: chrisda
ms.custom: nextgen, msecd-doc-authoring-1016
ms.date: 2026-07-02T00:00:00.0000000Z
ms.reviewer: yongrhee, pahuijbr
ms.subservice: ngp
ms.topic: how-to
ms.collection:
- m365-security
- tier2
- mde-ngp
ai-usage: ai-assisted
locale: en-us
document_id: db8a5da2-3562-e9ca-3348-bb9d741305b4
document_version_independent_id: db8a5da2-3562-e9ca-3348-bb9d741305b4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/restore-quarantined-files-microsoft-defender-antivirus.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: restore-quarantined-files-microsoft-defender-antivirus
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/restore-quarantined-files-microsoft-defender-antivirus.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/691e3042-55ad-4ce1-b5e9-649b1cc47b5c
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b7d11190-096c-4ddb-87db-63764f603aac
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 07a441a5-8d8a-8937-4c65-7adadf1682b2
---

# Restore quarantined files in Microsoft Defender Antivirus - Microsoft Defender for Endpoint | Microsoft Learn

Depending on how Microsoft Defender Antivirus is configured, it quarantines suspicious files. If you're certain a quarantined file isn't a threat, you can restore it on your Windows device. This article describes how to restore quarantined files by using the Windows Security app, the MpCmdRun command-line utility, or the Microsoft Defender for Endpoint portal.

## Prerequisites

Before you restore quarantined files, verify that your environment meets the following requirements.

### Supported operating systems

The following operating systems support restoring quarantined files:

- Windows

## Restore quarantined files using the Windows Security app

To restore a quarantined file by using the Windows Security app, perform the following steps:

1. On your Windows device, open **Windows Security**.
2. Select **Virus & threat protection** and then, under **Current threats**, select **Protection history**.
3. If you have a list of items, you can filter on **Quarantined Items**.
4. Select an item you want to keep, and choose an action, such as **Restore**.

## Restore quarantined files using MpCmdRun

Use the following steps to restore quarantined files from the command line using the MpCmdRun utility:

1. **Show all quarantined files**:

    In an elevated Command Prompt (a Command Prompt window you opened by selecting **Run as administrator**), run the following commands:

    Tip

    The first command changes the directory to the latest version of &lt;antimalware platform version&gt; in `%ProgramData%\Microsoft\Windows Defender\Platform\<antimalware platform version>`. If that path doesn't exist, the command changes the directory to `%ProgramFiles%\Windows Defender`.

    ```dos
    (set "_done=" & if exist "%ProgramData%\Microsoft\Windows Defender\Platform\" (for /f "delims=" %d in ('dir "%ProgramData%\Microsoft\Windows Defender\Platform" /ad /b /o:-n 2^>nul') do if not defined _done (cd /d "%ProgramData%\Microsoft\Windows Defender\Platform\%d" & set _done=1)) else (cd /d "%ProgramFiles%\Windows Defender")) >nul 2>&1
    
    MpCmdRun.exe -Restore -ListAll
    ```
2. **Restore a quarantined file**: After identifying the quarantined item from the list, you can restore a specific file by name. Replace &lt;filename&gt; with the name of the quarantined file you want to restore (as shown in the previous command's output), and then run the following command:

    ```dos
    MpCmdRun.exe -Restore -Name <filename>
    ```

For more information about MpCmdRun, see [Configure and manage Microsoft Defender Antivirus with the MpCmdRun command-line tool](command-line-arguments-microsoft-defender-antivirus).

## Download or collect the file

In the Microsoft Defender for Endpoint portal, you can download or collect a quarantined file from a device's file page. Selecting **Download file** from the response actions allows you to download a local, password-protected .zip archive containing your file. A flyout appears where you can record a reason for downloading the file, and set a password. By default, you should be able to download quarantined files using this response action.

The **Download file** button can have the following states:

- **Active** - You're able to collect the file.
- **Disabled** - If the button is grayed out or disabled during an active collection attempt, you might not have appropriate permissions to collect files.

For more information, see [Download or collect file](respond-file-alerts#download-or-collect-file).