---
layout: Conceptual
title: Overview of file integrity monitoring in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/file-integrity-monitoring-overview
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Learn about tracking file change with file integrity monitoring in Microsoft Defender for Cloud.
ms.topic: concept-article
ms.date: 2026-03-22T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 0935e2d5-7c57-4c30-b820-1ad99a8f8e3c
document_version_independent_id: 645d90a9-0cf1-c014-da23-fe5a447f769b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/file-integrity-monitoring-overview.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/file-integrity-monitoring-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/file-integrity-monitoring-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: b09a7edc-aaca-746a-b6c5-832047ac406b
---

# Overview of file integrity monitoring in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

The file integrity monitoring feature in Microsoft Defender for Cloud's [Defender for Servers Plan 2](plan-defender-for-servers-select-plan), scans operating system files, Windows registries, application software, and Linux system files. It analyzes these files for changes that might indicate an attack.

File integrity monitoring helps you to:

- Meet compliance requirements. Regulatory compliance standards such as PCI-DSS and ISO 17799 often require file integrity monitoring.
- Improve posture and identify potential security issues by detecting suspicious changes to files.

## Monitor suspicious activity

File integrity monitoring examines operating system files, Windows registries, application software, and Linux system files to detect suspicious activity such as:

- File and registry key creation or deletion.
- File modifications, such as changes in file size, access control lists, and hash of the content.
- Registry modifications such as changes in size, access control lists, type, and content.

## Data collection

File integrity monitoring uses the Microsoft Defender for Endpoint agent and agentless scanning to collect data from machines.

- Data collected by the Defender for Endpoint agent and agentless scanning is analyzed for file and registry changes and change logs are stored for access and analysis in a Log Analytics workspace.
- The **Defender for Endpoint agent** collects data from machines in accordance with the files and resources defined for file integrity monitoring. Change events collected via Defender for Endpoint are streamed to your selected workspace in **near realtime**.
- **Agentless scanning** provides insights into file integrity monitoring events in accordance with the files and resources defined for file integrity monitoring. Change events collected via agentless scanning are streamed to your selected workspace on a **24-hour cadence**.
- Collected file integrity monitoring data is part of the [500-MB benefit included in Defender for Servers Plan 2](data-ingestion-benefit).
- File integrity monitoring gives information about file and resource changes. It includes the source of the change, account details, indication of who made the changes, and information about the initiating process.

## Version requirements

To ensure proper file integrity monitoring functionality, machines must run the **Defender for Servers Windows client (Microsoft Defender for Endpoint agent) version 10.8799 or above**. This requirement is especially important for:

- Legacy Windows machines (downlevel clients)
- Environments transitioning from MMA or AMA-based FIM

Important

Due to a pipeline change in Microsoft Defender for Endpoint, users with existing FIM deployments on legacy Windows machines must update their MDE agent to version 10.8799 or above to continue receiving file integrity monitoring data.

### Migrate legacy AMA/MMA clients to MDE-based file integrity monitoring

If you're currently using file integrity monitoring with legacy agent-based methods (Log Analytics agent/Microsoft Monitoring Agent (MMA) or Azure Monitor Agent (AMA)), you need to migrate to the MDE-based (Microsoft Defender for Endpoint) approach. This migration ensures continued functionality and access to enhanced capabilities. Learn how to [migrate file integrity monitoring](migrate-file-integrity-monitoring) from legacy AMA/MMA clients to the MDE-based solution.

## Configure file integrity monitoring

After enabling Defender for Servers Plan 2, you enable and configure file integrity monitoring. It isn't enabled by default.

- You select a Log Analytics workspace in which to store change events for monitored files/resources. You can use an existing workspace, or define a new one.
- Defender for Cloud recommends resources to monitor with file integrity monitoring. With agentless scanning, you can define custom paths for monitoring in addition to recommended resources.

## Choose what to monitor

Defender for Cloud recommends entities to monitor with file integrity monitoring. You can choose items from the recommendations. When choosing which files to monitor:

- Consider the files that are critical for your system and applications.
- Monitor files that you don’t expect to change without planning.
- Select files that applications or the operating system frequently change (such as log files and text files) creates noise and makes it hard to identify an attack.
- Monitor any file located in a folder `/folder/path/*`.

Note

The maximum number of rules that can be applied is 500.

### Recommended items to monitor

When using file integrity monitoring with the Defender for Endpoint agent, we recommend monitoring these items with based on known attack patterns.

| **Linux file** | **Windows files** | **Windows registry keys (HKEY\_LOCAL\_MACHINE)** |
| --- | --- | --- |
| /bin | C:\config.sys | HKLM\SOFTWARE\Microsoft\Cryptography\OID\* |
| /bin/passwd | C:\Windows\regedit.exe | HKLM\SOFTWARE\WOW6432Node\Microsoft\Cryptography\OID\* |
| /boot | C:\Windows\System32\userinit.exe | **Key**: HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Windows**Values**: loadappinit\_dlls, appinit\_dlls, iconservicelib |
| /etc/\*.conf | C:\Windows\explorer.exe | **Key**: HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders**Values**: common startup, startup |
| /etc/cron.daily | C:\autoexec.bat | **Key**: HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders**Values**: common startup, startup |
| /etc/cron.hourly | C:\boot.ini | HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run |
| /etc/cron.monthly | C:\Windows\system.ini | HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce |
| /etc/cron.weekly | C:\Windows\win.ini | HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\RunServicesOnce |
| /etc/crontab |  | **Key**: HKLM\SOFTWARE\WOW6432Node\Microsoft\Windows\NT\CurrentVersion\Windows **Values**: appinit\_dlls, loadappinit\_dlls |
| /etc/init.d |  | **Key**: HKLM\SOFTWARE\WOW6432Node\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders **Values**: common startup, startup |
| /opt/sbin |  | **Key**: HKLM\SOFTWARE\WOW6432Node\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders **Values**: common startup, startup |
| /sbin |  | HKLM\SOFTWARE\WOW6432Node\Microsoft\Windows\CurrentVersion\Run |
| /usr/bin |  | HKLM\SOFTWARE\WOW6432Node\Microsoft\Windows\CurrentVersion\RunOnce |
| /usr/local/bin |  | HKLM\SECURITY\POLICY\SECRETS |
| /usr/local/sbin |  |  |
| /usr/sbin |  |  |
| /opt/bin |  |  |

## Custom rules

You can create custom rules to monitor specific files or folders as long as they meet the following validation criteria:

- A maximum of three asterisks `*` are allowed in the path (maximum depth). Wildcards (`*`) are allowed only at the start or end of a path segment.
- Paths with three asterisks must not end with `/` or `\`.
- Windows registry paths must start with `HKLM` or `hklm` and may only contain letters, numbers, spaces, `_`, `.`, `\`, `:`. Wildcards (`*`) are allowed only at the start or end of a path segment.
- Windows file paths may only contain letters, numbers, spaces, `_`, `.`, `\`, `*`, `?`, `:` and must not contain `/`. Wildcards (`*`) are allowed only at the start or end of a path segment.
- Linux file paths must be absolute (start with `/`) and may only contain letters, numbers, spaces, `_`, `.`, `/`, `*`, `:`. Wildcards (`*`) are allowed only at the start or end of a path segment.
- All paths must meet the system’s maximum path length (260 characters) and maximum depth (three asterisks) rules.

### Rule definition validations

- A rule name is required.
- A rule name must contain only letters (a–z, A–Z), digits (0–9), and underscores (\_), and can be up to 128 characters.
- Rule name and rule ID must be unique.
- Rule description is optional. If provided:

    - Maximum length is 260 characters.
    - Allowed characters: `letters`, `digits`, and `? ! ) ( . ,`.
- At least one change type (from change management and documentation rRequest (CMDR)) must be selected.
- Between 1 and 500 custom rules are supported per subscription.