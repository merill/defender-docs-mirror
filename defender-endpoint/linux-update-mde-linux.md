---
layout: Conceptual
title: How to schedule an update for Microsoft Defender for Endpoint on Linux - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/linux-update-mde-linux
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use crontab to schedule Microsoft Defender for Endpoint updates on Linux, with examples for RHEL, SLES, Ubuntu, and configuration management tools.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.reviewer: gopkr
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-linux
ms.topic: how-to
ms.subservice: linux
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: da14b8a7-93b2-8f8e-2153-67ec15316107
document_version_independent_id: da14b8a7-93b2-8f8e-2153-67ec15316107
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/linux-update-mde-linux.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: linux-update-mde-linux
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/linux-update-mde-linux.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: c8e8814a-1ebe-69db-6e41-7bffcad02a43
---

# How to schedule an update for Microsoft Defender for Endpoint on Linux - Microsoft Defender for Endpoint | Microsoft Learn

To run an update on Microsoft Defender for Endpoint on Linux, see [Deploy updates for Microsoft Defender for Endpoint on Linux](linux-updates).

Linux and Unix have a tool called **crontab** (similar to Task Scheduler) to be able to run scheduled tasks.

## Prerequisites

Note

To get a list of all the time zones, run the following command: `timedatectl list-timezones`

Examples for timezones:

- `America/Los_Angeles`
- `America/New_York`
- `America/Chicago`
- `America/Denver`

## Set the cron job

Use the following commands:

### Backup crontab entries

Use the following command to back up the current crontab entries before making changes:

```bash
sudo crontab -l > /var/tmp/cron_backup_201118.dat
```

Note

In our example, `201118` == `YYMMDD`.

Tip

Back up your crontab entries before you edit or remove them.

To edit the root user's crontab and add a new job:

```bash
sudo crontab -e
```

Note

The default editor is VIM.

You might see:

```console
0 * * * * /etc/opt/microsoft/mdatp/logrorate.sh
```

And

```console
0 2 * * sat /bin/mdatp scan quick>~/mdatp_cron_job.log
```

For instructions on creating a scheduled antivirus scan job, see [Schedule scans with Microsoft Defender for Endpoint (Linux)](schedule-antivirus-scan-crontab).

Press "Insert"

Add the following entries. Use the `CRON_TZ` setting to ensure the scheduled cron jobs run in the intended time zone:

```bash
CRON_TZ=America/Los_Angeles
```

> 
> #!RHEL and variants (CentOS and Oracle Linux)
> 
> 
> ```bash
> 0 6 * * sun [ $(date +\%d) -le 15 ] && sudo yum update mdatp -y >> ~/mdatp_cron_job.log
> ```

> 
> #!SLES and variants
> 
> 
> ```bash
> 0 6 * * sun [ $(date +\%d) -le 15 ] && sudo zypper update mdatp >> ~/mdatp_cron_job.log
> ```

> 
> #!Ubuntu and Debian systems
> 
> 
> ```bash
> 0 6 * * sun [ $(date +\%d) -le 15 ] && sudo apt-get install --only-upgrade mdatp >> ~/mdatp_cron_job.log
> ```

Note

In the RHEL, SLES, Ubuntu, and Debian cron entries, `0 6 * * sun` specifies 00 minutes, 6 a.m. (hour using the 24-hour format), any day of the month, any month, on Sundays. `[$(date +\%d) -le 15]` doesn't run unless it's equal or less than the 15th day (third week). The full cron entry means the job runs at 6 a.m. every Sunday, but only if the day of the month is the 15th or earlier.

Press "Esc"

Type "`:wq`" w/o the double quotes.

Note

w == write, q == quit

To view your cron jobs, type `sudo crontab -l`

![update Defender for Endpoint on Linux.](media/update-mde-linux-4634577.jpg)

To verify that Defender-related cron jobs have run, search the cron log for `mdatp` entries:

```bash
sudo grep mdatp /var/log/cron
```

To open the log file and review output from scheduled Defender update tasks:

```bash
sudo nano mdatp_cron_job.log
```

## Configure scheduled updates with Ansible, Chef, or Puppet

Use the following commands:

### To set cron jobs in Ansible

Use Ansible's cron module to manage cron jobs:

```text
cron - Manage cron.d and crontab entries
```

See https://docs.ansible.com/ansible/latest for more information.

### To set crontabs in Chef

Use Chef's cron resource to manage cron jobs:

```text
cron resource
```

See https://docs.chef.io/resources/cron/ for more information.

### To set cron jobs in Puppet

Resource Type: cron

See https://puppet.com/docs/puppet/5.5/types/cron.html for more information.

Automating with Puppet: Cron jobs and scheduled tasks

See https://puppet.com/blog/automating-puppet-cron-jobs-and-scheduled-tasks/ for more information.

## Common crontab commands and examples

The following commands cover common crontab tasks such as listing, backing up, editing, and removing cron entries.

### To get help with crontab

Run the following command to view the crontab manual page:

```bash
man crontab
```

### To get a list of crontab file of the current user

Run the following command to list the current user's crontab entries:

```bash
crontab -l
```

### To get a list of crontab file of another user

Run the following command to list another user's crontab entries:

```bash
crontab -u username -l
```

### To back up crontab entries

Use the following command to back up the current crontab entries:

```bash
crontab -l > /var/tmp/cron_backup.dat
```

Tip

Do this before you edit or remove.

### To restore crontab entries

Run the following command to restore crontab entries from a backup file:

```bash
crontab /var/tmp/cron_backup.dat
```

### To edit the crontab and add a new job as a root user

Use the following command to edit the root user's crontab and add a new job:

```bash
sudo crontab -e
```

### To edit the crontab and add a new job

Run the following command to edit the current user's crontab and add a new job:

```bash
crontab -e
```

### To edit other user's crontab entries

Run the following command to edit another user's crontab entries:

```bash
crontab -u username -e
```

### To remove all crontab entries

Warning

This command removes all crontab entries for the current user without prompting for confirmation. Back up your crontab first with `crontab -l > /var/tmp/cron_backup.dat` if you might need to restore it.

Use the following command to remove all crontab entries for the current user:

```bash
crontab -r
```

### To remove other user's crontab entries

Warning

This command permanently removes all crontab entries for the specified user without prompting for confirmation. Back up the user's crontab before running this command.

Use the following command to remove all scheduled tasks for a specific user by deleting that user's crontab entries:

```bash
crontab -u username -r
```

### Cron expression field reference

The following diagram explains the fields in a cron expression:

```

+—————- minute (values: 0 - 59) (special characters: , - * /)  
| +————- hour (values: 0 - 23) (special characters: , - * /) 
| | +———- day of month (values: 1 - 31) (special characters: , - * / L W C)  
| | | +——- month (values: 1 - 12) (special characters: ,- * / )  
| | | | +—- day of week (values: 0 - 6) (Sunday=0 or 7) (special characters: , - * / L W C) 
| | | | |*****command to be executed
```