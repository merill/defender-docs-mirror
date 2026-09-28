---
layout: Conceptual
title: Schedule Microsoft Defender for Endpoint antivirus scans on Linux - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/schedule-antivirus-scans-linux
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to schedule Microsoft Defender for Endpoint antivirus scans on Linux using the Microsoft Defender portal, Microsoft Intune, managed JSON, or the command line.
ms.service: defender-endpoint
ms.mktglfocus: mdatp
ms.author: painbar
author: paulinbar
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 2026-09-10T00:00:00.0000000Z
ai-usage: ai-generated
ms.custom: msecd-doc-authoring-1015
locale: en-us
document_id: e505a632-a2f8-5114-c66f-7d73cca1a0f6
document_version_independent_id: e505a632-a2f8-5114-c66f-7d73cca1a0f6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/schedule-antivirus-scans-linux.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: schedule-antivirus-scans-linux
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/schedule-antivirus-scans-linux.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/a72e95ff-4b4f-4cc1-90c6-7dcba67ff05f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/24dc3ccd-591a-4415-a1fe-8759afafcb12
platformId: fd5ed6a6-b831-c7de-e39e-4c809b506981
---

# Schedule Microsoft Defender for Endpoint antivirus scans on Linux - Microsoft Defender for Endpoint | Microsoft Learn

Built-in scheduled antivirus scans in Microsoft Defender for Endpoint on Linux help IT and security administrators apply consistent scan schedules without custom cron jobs. You can configure daily and interval-based quick scans, weekly quick or full scans, and options that control performance, idle-state behavior, security intelligence updates, exclusions, and randomized start times.

Use the Microsoft Defender portal, Microsoft Intune, managed JSON, or the command line to configure scans. Before you begin, confirm that devices meet the prerequisites, including the required agent version and management permissions.

## Prerequisites

Before configuring scheduled antivirus scans on Linux, ensure the following requirements are met:

- Microsoft Defender for Endpoint is installed and onboarded on supported Linux distributions.
- Devices are running agent version `101.26032.0000` (April 2026) or later in the production ring.
- Devices are healthy and reporting correctly to the Microsoft Defender service.

Depending on your configuration method, the following prerequisites also need to be met:

- **Managed JSON configuration**:

    - Ability to deploy configuration files to `/etc/opt/microsoft/mdatp/managed`.
    - Permissions to manage system configuration files.
    - If you already use managed configuration for other antivirus settings, append to your existing configuration file instead of replacing it.
- **Microsoft Intune**:

    - The [Endpoint Security Manager](/en-us/intune/fundamentals/role-based-access-control/ref-built-in-roles#endpoint-security-manager) role, or a custom role with equivalent permissions to create and assign endpoint security policies.
- **Microsoft Defender portal**:

    - The **Authorization and settings/Security settings/Core Security settings (manage)** permission in Microsoft Defender XDR Unified role-based access control (RBAC). Alternatively, use the Intune **Endpoint Security Manager** role or the Microsoft Entra **Security Administrator** or **Intune Administrator** role. For more information, see [Prerequisites for managing endpoint security policies](endpoint-security-policies-configure#prerequisites).

## Scheduled antivirus scan types

Defender for Endpoint on Linux supports the following scan types for scheduled scans:

- **Quick scans**: Quick scans examine locations where malware is likely to be registered and run, such as startup paths and system services. They complete faster and are recommended for frequent scheduling, such as daily or interval-based scans.
- **Full scans**: Full scans examine files and folders within `/`. They provide more comprehensive coverage but can take longer to complete, depending on system size and workload. They're typically scheduled less frequently, such as weekly.

### Scheduling options

Scheduled scans can be configured using the following scheduling options:

- **Hourly quick scans**: Run quick scans at periodic intervals (every *N* hours).
- **Daily quick scans**: Run quick scans at a specific time each day.
- **Weekly scans**: Run a scan on a specified day and time, with the option to choose either a quick scan or a full scan.

These scheduling options can be configured independently and combined. For example, you can run daily quick scans along with a weekly full scan.

## Scheduled scan settings

The following table describes the available settings for configuring scheduled antivirus scans:

| Category | Setting | Description | Possible values | Default |
| --- | --- | --- | --- | --- |
| Daily scan settings | interval | Runs a quick scan every N hours (interval-based scheduling). | 0 through 24 hours. 0 = disabled. | 0 |
| Daily scan settings | timeOfDay (daily) | Runs a quick scan once daily at a specific time. The value is the number of minutes after midnight in the device's local time. | 0 through 1440 (for example, 120 = 2:00 AM) | 0 |
| Weekly scan settings | dayOfWeek | Specifies the day a scheduled scan runs. | 0 through 80 = disabled1 through 7 = Sunday through Saturday8 = every day | 0 |
| Weekly scan settings | timeOfDay (weekly) | Specifies when the weekly scan runs. The value is the number of minutes after midnight in the device's local time. | 0 through 1440 | 120 (2:00 AM) |
| Weekly scan settings | scanType | Specifies the scan type for weekly scans. | `quick`, `full` | `quick` |
| Advanced settings (optional) | runScanWhenIdle | Delays the scan until the system is idle. | `true`, `false` | `false` |
| Advanced settings (optional) | lowPriorityScheduledScan | Runs scans with reduced CPU priority. | `true`, `false` | `false` |
| Advanced settings (optional) | checkForDefinitionsUpdate | Checks for the latest security intelligence updates before starting the scan. | `true`, `false` | `false` |
| Advanced settings (optional) | randomizeScanStartTime | Randomizes the scan start time within a defined window, in hours, to avoid simultaneous scans. | 0 through 23 | 0 |
| Advanced settings (optional) | ignoreExclusions | Runs scans without honoring configured exclusions. | `true`, `false` | `false` |

Note

`interval` and `timeOfDay` (daily) are independent settings. If both are configured, they create separate quick scan schedules and can result in multiple scans per day.

## Configure scheduled antivirus scans

You can configure scheduled scans using the Microsoft Defender portal, Microsoft Intune, managed JSON, or the command line, depending on how you manage device settings.

If scheduled scan settings are configured using multiple methods, Microsoft Defender portal policies (security settings management) take precedence over local configuration (managed JSON or the command line).

### Use Microsoft Intune to configure scheduled scans

Microsoft Intune is the recommended tool for configuring and distributing Defender for Endpoint features to devices. However, Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have Intune, you can use any of the other methods in this article. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

To configure scheduled antivirus scans in Microsoft Intune, use an endpoint security **Antivirus** policy. For detailed instructions, see [Create endpoint security policies](/en-us/intune/intune-service/protect/endpoint-security-policy#create-endpoint-security-policies) or [Modify existing policies](/en-us/intune/device-configuration/endpoint-security/manage-policies#modify-existing-policies) (links open new tabs in the Intune documentation).

When you create the policy, use these specific settings:

- **Policy type**: Go to **Manage** &gt; **Antivirus** on the **Endpoint security | Overview** page at [https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/~/overview](https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/%7E/overview), and then select ![](media/defender-portal-icon-create.png)**Create policy**.
- **Platform**: Select **Linux**.
- **Profile**: Select **Microsoft Defender Antivirus**.

When you create or modify the policy, configure the scheduled scan settings in the **Schedule Scan** section on the **Configuration settings** tab.

If you use Intune endpoint security policies to manage Linux devices that aren't enrolled in Intune, first configure [Defender for Endpoint security settings management](/en-us/intune/intune-service/protect/mde-security-integration). Assign the policy to a Microsoft Entra device group that contains the Linux devices you want to manage.

### Use the Microsoft Defender portal to configure scheduled scans

If your organization [manages endpoint security policies in the Microsoft Defender portal](endpoint-security-policies-configure), you can configure scheduled antivirus scans with the same endpoint security policies that Intune uses.

For detailed instructions, see [Create an endpoint security policy](endpoint-security-policies-configure#create-an-endpoint-security-policy) or [Edit an endpoint security policy](endpoint-security-policies-configure#edit-an-endpoint-security-policy) (links open new tabs).

When you create the policy, use these specific settings:

- **Policy type**: On the **Linux policies** tab of the **Endpoint security policies** page in the Microsoft Defender portal at https://security.microsoft.com/policy-inventory, select ![](media/defender-portal-icon-create.png)**Create new policy**.
- **Platform**: Select **Linux**.
- **Template**: Select **Microsoft Defender Antivirus**.

When you create or modify the policy, configure the scheduled scan settings in the **Schedule Scan** section on the **Configuration settings** page.

For devices that aren't enrolled in Intune, first configure [Defender for Endpoint security settings management](/en-us/intune/intune-service/protect/mde-security-integration). Assign the policy to a Microsoft Entra device group that contains the Linux devices you want to manage.

### Use mdatp managed JSON configuration

In enterprise environments, schedule antivirus scans through a configuration profile. Use a configuration management tool such as Puppet, Ansible, or another management console to push a file named `mdatp_managed.json` to `/etc/opt/microsoft/mdatp/managed`.

If you already use `mdatp_managed.json` to configure other Defender for Endpoint settings, such as exclusions or antivirus preferences, don't replace the file. Add the scheduled scan settings to the existing managed JSON. For more information, see [Configure security settings in Microsoft Defender for Endpoint on Linux](linux-preferences).

The following example configures:

- A weekly full scan every Saturday at 3:00 AM.
- A daily quick scan every day at 3:00 AM.
- Runs scans only when the device is idle.
- Reduces CPU impact by using low-priority scheduling.
- Checks for security intelligence updates before scanning.
- Ignores exclusions during scans.
- Randomizes scan start times by up to 3 hours.

```json
{
  "antivirusEngine": {
    "scheduledScan": "enabled"
  },
  "scheduledScan": {
    "weeklyConfiguration": {
      "dayOfWeek": 7,
      "scanType": "full",
      "timeOfDay": 180
    },
    "dailyConfiguration": {
      "timeOfDay": 180
    },
    "runScanWhenIdle": true,
    "lowPriorityScheduledScan": true,
    "checkForDefinitionsUpdate": true,
    "ignoreExclusions": true,
    "randomizeScanStartTime": 3
  }
}
```

### Use the command line to configure scheduled scans

You can configure scheduled antivirus scans directly on a Linux device using the Microsoft Defender for Endpoint command-line tool (`mdatp`). This approach is useful for testing or single-device configuration.

- **Enable scheduled scans**:

    ```bash
    mdatp config scheduled-scan settings feature --value enabled
    ```
- **Configure daily quick scan**: Run a daily quick scan at a specific time (in minutes from midnight).

    Example: Daily quick scan at 2:00 AM

    ```bash
    mdatp config scheduled-scan quick-scan time-of-day --value 120
    ```
- **Configure interval-based quick scan**: Run quick scans at regular hourly intervals.

    Example: Run a quick scan every 6 hours

    ```bash
    mdatp config scheduled-scan quick-scan hourly-interval --value 6
    ```
- **Configure weekly scan**: Schedule a weekly scan with a specific day, time, and scan type.

    Example: Weekly full scan every Wednesday at 3:00 AM

    ```bash
    mdatp config scheduled-scan weekly-scan --day-of-week 4 --time-of-day 180 --scan-type full
    ```

Note

Command-line configuration is recommended for testing or ad hoc setup. For large-scale deployment, use managed JSON configuration or Microsoft Defender portal policies.

## Verify scheduled antivirus scans

After you configure scheduled scans, verify that the configuration is applied correctly and that scans run as expected.

### Verify configuration status

Run the following command to confirm that scheduled scan settings are applied:

```bash
mdatp health --details scheduled_scan
```

### Check scheduled scan execution

Use the following command to view the scan history:

```bash
mdatp scan list
```

You can also verify scan activity on the device page in the Defender portal. The page shows the last full scan and the last quick scan:

1. On the **Device inventory** page in the Microsoft Defender portal at https://security.microsoft.com/machines, select the target Linux device.
2. In the **Overview** tab, locate the **Device health status** section.

The scan information helps confirm whether scheduled scans are running as expected on the device.

## Frequently asked questions

**Do scheduled scans require real-time protection to be enabled?**

No. Scheduled scans operate independently of real-time protection. They can run even when real-time protection is disabled or the device is in passive or on-demand mode.

**Can daily and weekly scans be configured together?**

Yes. Daily and weekly configurations can coexist. A common pattern is daily scans for regular coverage and a weekly full scan for deeper inspection.

**What scan type is used for daily scans?**

Daily scans follow the engine default behavior. They're always quick scans. You can explicitly configure the scan type for weekly scans.

**Are exclusions applied during scheduled scans?**

By default, scheduled scans respect configured exclusions. If `ignoreExclusions` is set to true, scheduled scans will ignore exclusions during execution.

**What time zone is used for scan scheduling?**

All scheduled scan times are evaluated using the device's local time zone.

**What happens if neither daily nor weekly configuration is specified?**

If no daily or weekly configuration is defined, scheduled scans will not run.

**Can I stagger scan start times on devices?**

Use `randomizeScanStartTime` to randomize the scan start within a defined window, which helps reduce simultaneous load on your devices.

**What happens if the server is offline?**

Scheduled scans do not run at the scheduled time while the device is asleep. Instead, scheduled scans run when the device resumes from sleep mode. If the device is turned off, the scan runs at the next scheduled scan time.