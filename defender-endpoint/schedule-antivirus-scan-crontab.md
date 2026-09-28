---
layout: Conceptual
title: Schedule an antivirus scan using crontab with Microsoft Defender for Endpoint on Linux - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/schedule-antivirus-scan-crontab
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to schedule an automatic scanning time for Microsoft Defender for Endpoint (Linux) to better protect your organization's assets.
ms.service: defender-endpoint
ms.author: chrisda
author: chrisda
ms.reviewer: gopkr
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-linux
ms.topic: article
ms.subservice: linux
ms.date: 2025-05-04T00:00:00.0000000Z
locale: en-us
document_id: f45e2538-9992-ef5d-4995-ee5c6ebee791
document_version_independent_id: f45e2538-9992-ef5d-4995-ee5c6ebee791
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/schedule-antivirus-scan-crontab.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: schedule-antivirus-scan-crontab
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/schedule-antivirus-scan-crontab.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: f12e06d2-c1d5-8c85-bbfe-9ef6b55f4862
---

# Schedule an antivirus scan using crontab with Microsoft Defender for Endpoint on Linux - Microsoft Defender for Endpoint | Microsoft Learn

To run a scan for Linux, see [Supported commands](linux-resources#supported-commands).

For Linux (and Unix), you can use a tool called **crontab** (similar to Task Scheduler in Windows) to run scheduled tasks.

## Prerequisite

Note

To get a list of all the time zones, run the following command: `timedatectl list-timezones` Examples for time zones:

- `America/Los_Angeles`
- `America/New_York`
- `America/Chicago`
- `America/Denver`

## Set the Cron job

To set the cron job, use the commands in this article.

### Backup crontab entries

Tip

Do this step before you edit or remove entries.

```bash
sudo crontab -l > /var/tmp/cron_backup_200919.dat
```

Where 200919 = YYMMDD

To edit the crontab and add a new job as a root user:

```bash
sudo crontab -e
```

Note

The default editor is VIM.

You might see:

```console
0 * * * * /etc/opt/microsoft/mdatp/logrorate.sh
```

Press **Insert**, and then add the following entries:

```bash
CRON_TZ=America/Los_Angeles

0 2 * * sat /usr/bin/mdatp scan quick > ~/mdatp_cron_job.log
```

Note

In this example, we have set it to 00 minutes, 2 a.m. (hour in 24-hour format), any day of the month, any month, on Saturdays. This setting means the job runs Saturdays at 2:00 a.m. Pacific (UTC -8).

Press **Esc**, and then type "`:wq`" without the double quotes.

Note

w == write, q == quit

To view your cron jobs, type `sudo crontab -l`

![Screenshot of the linux mdatp page.](/en-us/defender/media/linux-mdatp-1.png)

#### To inspect cron job runs

```bash
sudo grep mdatp /var/log/cron
```

#### To inspect the mdatp\_cron\_job.log\*

```bash
sudo nano mdatp_cron_job.log
```

## Verify scan execution

Linux doesn't provide a direct way to confirm that a scheduled scan ran.

Scheduled scans configured through crontab don't surface a status field or dedicated confirmation in Microsoft Defender for Endpoint on Linux.

To verify that a scan ran, run the following command:

```bash
mdatp scan list
```

`mdatp scan list` returns a history of the last 7 scans performed on the device by Microsoft Defender for Endpoint. For each scan entry, you can see:

- Scan Type - Quick or Full
- Scan Start Time - For example, Jan 05 2023 at 03:18:39 PM
- Scan State - For example, Succeeded, Failed, or Cancelled

Use this command to verify that scheduled scans ran at the expected date, time, and frequency.

The output only covers the last seven scans. If you need to check whether both quick and full scans are running regularly, monitor it over time or script around it.

You can also verify the scan ran by:

**Running on-demand scans:**

- Quick scan

    ```bash
    mdatp scan quick
    ```
- Full scan

    ```bash
     mdatp scan full
    ```
- Scan a specific path

    ```bash
    mdatp scan custom --path /home/user/downloads
    ```

**Checking scan results**

- List all detected threats.

    ```bash
    mdatp threat list
    ```
- Get details on a specific threat.

    ```bash
    mdatp threat get --id [threat-id]
    ```

## If you're using Ansible, Chef, Puppet, or SaltStack

Use the following commands:

### To set cron jobs in Ansible

```bash
cron - Manage cron.d and crontab entries
```

For more information, see [Ansible documentation](https://docs.ansible.com/ansible/latest).

### To set crontabs in Chef

```bash
cron resource
```

For more information, see [Chef documentation](https://docs.chef.io/resources/cron).

### To set cron jobs in Puppet

```bash
Resource Type: cron
```

For more information, see [Puppet documentation: Resource Type: cron](https://puppet.com/docs/puppet/5.5/types/cron.html).

**Automating with Puppet: Cron jobs and scheduled tasks**

For more information, see [Puppet documentation about jobs and scheduled tasks](https://puppet.com/blog/automating-puppet-cron-jobs-and-scheduled-tasks/).

### To manage cron jobs in SaltStack

```bash
Resource Type: salt.states.cron
```

**Example:**

```yaml
mdatp scan quick > /tmp/mdatp_scan_log.log:
  cron.present:
    - special: '@hourly'
```

For more information, see the [Salt.States.Cron documentation](https://docs.saltproject.io/en/latest/ref/states/all/salt.states.cron.html).

## Additional information

### To get help with crontab

```bash
man crontab
```

### To get a list of crontab files for the current user

```bash
crontab -l
```

### To get a list of crontab files for another user

```bash
crontab -u username -l
```

### To back up crontab entries

Tip

Do this step before you edit or remove entries.

```bash
crontab -l > /var/tmp/cron_backup.dat
```

### To restore crontab entries

```bash
crontab /var/tmp/cron_backup.dat
```

### To edit the crontab and add a new job as a root user

```bash
sudo crontab -e
```

### To edit the crontab and add a new job

```bash
crontab -e
```

### To edit other user's crontab entries

```bash
crontab -u username -e
```

### To remove all crontab entries

```bash
crontab -r
```

### To remove other user's crontab entries

```bash
crontab -u username -r
```

### Explanation

```console
+—————- minute (values: 0 - 59) (special characters: , \- \* /)  <br>
| +————- hour (values: 0 - 23) (special characters: , \- \* /) <br>
| | +———- day of month (values: 1 - 31) (special characters: , \- \* / L W C)  <br>
| | | +——- month (values: 1 - 12) (special characters: , \- \* /)  <br>
| | | | +—- day of week (values: 0 - 6) (Sunday=0 or 7) (special characters: , \- \* / L W C) <br>
| | | | |*****command to be executed
```