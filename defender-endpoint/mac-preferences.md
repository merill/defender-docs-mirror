---
layout: Conceptual
title: Set preferences for Microsoft Defender for Endpoint on macOS - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/mac-preferences
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Configure Microsoft Defender for Endpoint on macOS in enterprise organizations.
ms.service: defender-endpoint
author: paulinbar
ms.author: painbar
ms.reviewer: joshbregman
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-macos
ms.topic: how-to
ms.subservice: macos
ms.date: 2026-09-18T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 3c6ebe83-8688-0933-0ab9-aa8e6957e196
document_version_independent_id: 3c6ebe83-8688-0933-0ab9-aa8e6957e196
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/mac-preferences.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mac-preferences
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/mac-preferences.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 03a55027-11a1-c2bf-3321-b79f7e6e0d5f
---

# Set preferences for Microsoft Defender for Endpoint on macOS - Microsoft Defender for Endpoint | Microsoft Learn

You can use a configuration profile to manage Microsoft Defender for Endpoint preferences consistently on managed macOS devices. Managed preferences take precedence over preferences configured locally on a device and require administrator privileges to change locally.

This article is for security administrators who deploy configuration profiles through Microsoft Intune, Jamf Pro, or another mobile device management (MDM) solution. It provides reference information and sample profiles for configuring Defender Antivirus, cloud-delivered protection, the user interface, endpoint detection and response (EDR), and tamper protection.

Before you configure preferences, review the [prerequisites for Defender for Endpoint on macOS](microsoft-defender-endpoint-mac-prerequisites). For complete deployment workflows, see [Deploy Microsoft Defender for Endpoint on macOS](microsoft-defender-endpoint-mac#deploy-defender-for-endpoint-on-macos). To configure preferences locally from the command-line interface, see [Configure from the command line](mac-resources#configuring-from-the-command-line).

## Configuration profile structure

The configuration profile uses Apple property list XML made up of key-value pairs. Each key is a preference name. Values can be simple, such as a number, or complex, such as a nested list of preferences. Save or upload the XML in the format required by your management tool.

Important

Test configuration profiles with a limited group of devices before you deploy them broadly. The profile layout depends on the management console that you use. This article includes examples for Jamf Pro and Microsoft Intune.

The top level of the configuration profile includes product-wide preferences and dictionaries for Defender for Endpoint features, the antivirus engine, cloud-delivered protection, the user interface, endpoint detection and response (EDR), and tamper protection.

### Features preferences

Use the `features` dictionary to manage individual Defender for Endpoint features.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `features` |
| **Data type** | Dictionary (nested preference) |
| **Comments** | The dictionary includes settings for features such as behavior monitoring. |

#### Configure behavior monitoring

Specify whether behavior monitoring and blocking are enabled on the device.

Note

Behavior monitoring applies only when real-time protection is enabled.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `behaviorMonitoring` |
| **Data type** | String |
| **Possible values** | `disabled`<br>`enabled` (default) |
| **Comments** | Available in Microsoft Defender for Endpoint version 101.24042.0002 or later. |

### Antivirus engine preferences

Use the `antivirusEngine` dictionary to manage Defender Antivirus preferences.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `antivirusEngine` |
| **Data type** | Dictionary (nested preference) |
| **Comments** | The dictionary includes settings for enforcement level, file hash computation, scan exclusions, allowed threats, threat type settings, and scan history retention. |

#### Enforcement level for antivirus engine

Specify the antivirus engine enforcement level:

- `real_time` (default): Enable real-time protection and scan files as they're accessed.
- `on_demand`: Turn off real-time protection and scan files only on demand.
- `passive`: Turn off real-time protection and automatic threat remediation, turn on on-demand scanning and security intelligence updates, and hide the status menu icon.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `enforcementLevel` |
| **Data type** | String |
| **Possible values** | `real_time` (default) <br>`on_demand`<br><br>`passive` |
| **Comments** | Available in Microsoft Defender for Endpoint version 101.10.72 or later. |

#### Configure file hash computation feature

Specify whether Defender for Endpoint computes hashes for files that it scans. File hash computation improves matching against file indicator rules but might affect device performance. On macOS, this feature supports scripts and 32-bit and 64-bit Mach-O files beginning with engine version 1.1.20000.2. For more information, see [Create indicators for files](indicator-file).

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `enableFileHashComputation` |
| **Data type** | Boolean |
| **Possible values** | `false` (default) <br>`true` |
| **Comments** | Available in Defender for Endpoint version 101.86.81 or later. |

#### Run a scan after definitions are updated

Specify whether to start a process scan after new security intelligence updates are downloaded on the device. Enabling this setting triggers an antivirus scan on the running processes of the device.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `scanAfterDefinitionUpdate` |
| **Data type** | Boolean |
| **Possible values** | `true` (default) <br>`false` |
| **Comments** | Available in Microsoft Defender for Endpoint version 101.41.10 or later. |

#### Scan archives (on-demand antivirus scans only)

Specify whether to scan archives during on-demand antivirus scans.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `scanArchives` |
| **Data type** | Boolean |
| **Possible values** | `true` (default) <br>`false` |
| **Comments** | Available in Microsoft Defender for Endpoint version 101.41.10 or later. |

#### Degree of parallelism for on-demand scans

Specify the number of threads used for on-demand scans. The value affects CPU usage and scan duration.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `maximumOnDemandScanThreads` |
| **Data type** | Integer |
| **Possible values** | `2` (default). Use an integer from `1` through `64`. |
| **Comments** | Available in Microsoft Defender for Endpoint version 101.41.10 or later. |

#### Exclusion merge policy

Specify whether to combine administrator-defined and user-defined exclusions or use only administrator-defined exclusions. Use `admin_only` to prevent local users from defining exclusions.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `exclusionsMergePolicy` |
| **Data type** | String |
| **Possible values** | `merge` (default) <br>`admin_only` |
| **Comments** | Available in Microsoft Defender for Endpoint version 100.83.73 or later. |

#### Scan exclusions

Specify files, folders, file extensions, or processes to exclude from scanning. The `exclusions` array can contain multiple entries in any order.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `exclusions` |
| **Data type** | Array of dictionaries |
| **Comments** | Each dictionary can contain `$type` (exclusion type), `path` (file or folder path), `isDirectory` (path type), `extension` (file extension), or `name` (process name). |

##### Type of exclusion

Specify content excluded from being scanned by type.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `$type` |
| **Data type** | String |
| **Possible values** | `excludedPath`<br>`excludedFileExtension`<br><br>`excludedFileName` |

##### Path to excluded content

Specify content excluded from being scanned by full file path.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `path` |
| **Data type** | String |
| **Possible values** | valid paths |
| **Comments** | Applies only when `$type` is `excludedPath`. |

#### Supported exclusion types

Defender for Endpoint on macOS supports the following antivirus scan exclusion types:

| Exclusion | Definition | Examples |
| --- | --- | --- |
| File extension | All files with the extension, anywhere on the device | `.test` |
| File | A specific file identified by the full path | `/var/log/test.log`<br>`/var/log/*.log`<br><br>`/var/log/install.?.log` |
| Folder | All files under the specified folder (recursively) | `/var/log/`<br>`/var/*/` |
| Process | A specific process (specified either by the full path or file name) and all files opened by it | `/bin/cat`<br>`cat`<br><br>`c?t` |

Important

Exclusion paths must be hard links, not symbolic links. To determine whether a path is a symbolic link, run `file <path-name>`.

File, folder, and process exclusions support the following wildcards:

| Wildcard | Description | Example | Matches | Doesn't match |
| --- | --- | --- | --- | --- |
| \* | Matches any number of any characters including none (note that when this wildcard is used inside a path it substitutes only one folder) | `/var/\*/\*.log` | `/var/log/system.log` | `/var/log/nested/system.log` |
| ? | Matches any single character | `file?.log` | `file1.log`<br>`file2.log` | `file123.log` |

##### Scan exclusion path type (file or directory)

In an antivirus scan exclusion entry, use `isDirectory` to indicate whether the `path` value refers to a file or a directory.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `isDirectory` |
| **Data type** | Boolean |
| **Possible values** | `false` (default) <br>`true` |
| **Comments** | Applies only when `$type` is `excludedPath`. |

##### Scan exclusion: file extension

In an antivirus scan exclusion entry, use `extension` to exclude files by file extension.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `extension` |
| **Data type** | String |
| **Possible values** | valid file extensions |
| **Comments** | Applies only when `$type` is `excludedFileExtension`. |

##### Scan exclusion: process name or path

In an antivirus scan exclusion entry, use `name` to exclude a process and all files opened by that process from scanning. Specify the process by its name, such as `cat`, or its full path, such as `/bin/cat`.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `name` |
| **Data type** | String |
| **Possible values** | any string |
| **Comments** | Applies only when `$type` is `excludedFileName`. |

#### Allowed threats

Specify by name the threats that Defender for Endpoint allows to run.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `allowedThreats` |
| **Data type** | Array of strings |

#### Disallowed threat actions

Restrict the actions that local users can take when threats are detected. Actions in this list don't appear in the user interface.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `disallowedThreatActions` |
| **Data type** | Array of strings |
| **Possible values** | `allow` (prevents users from allowing threats) <br>`restore` (prevents users from restoring threats from quarantine) |
| **Comments** | Available in Microsoft Defender for Endpoint version 100.83.73 or later. |

#### Threat type settings

Specify how certain threat types are handled by Microsoft Defender for Endpoint on macOS.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `threatTypeSettings` |
| **Data type** | Array of dictionaries |
| **Comments** | Each entry in the array contains a `key` (threat type, such as `potentially_unwanted_application` or `archive_bomb`) and a `value` (action to take: `audit`, `block`, or `off`). |

##### Threat type

Specify threat types.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `key` |
| **Data type** | String |
| **Possible values** | `potentially_unwanted_application`<br>`archive_bomb` |

##### Action to take

Specify what action to take when a threat of the type identified by the `key` setting is detected. Choose from the following options:

- `audit`: The device isn't protected against this threat type, but Defender for Endpoint logs the threat.
- `block`: Defender for Endpoint blocks the threat and notifies you in the user interface and the Microsoft Defender portal.
- `off`: The device isn't protected against this threat type, and Defender for Endpoint doesn't log the threat.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `value` |
| **Data type** | String |
| **Possible values** | `audit` (default) <br>`block`<br><br>`off` |

#### Threat type settings merge policy

Specify whether to combine administrator-defined and user-defined threat type settings or use only administrator-defined settings. Use `admin_only` to prevent local users from defining threat type settings.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `threatTypeSettingsMergePolicy` |
| **Data type** | String |
| **Possible values** | `merge` (default) <br>`admin_only` |
| **Comments** | Available in Microsoft Defender for Endpoint version 100.83.73 or later. |

#### Antivirus scan history retention (in days)

Specify how many days to retain results in the scan history on the device. When results expire, Defender for Endpoint removes the scan results from the history and removes associated quarantined files from the disk.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `scanResultsRetentionDays` |
| **Data type** | Integer |
| **Possible values** | `90` (default). Use an integer from `1` through `180`. |
| **Comments** | Available in Microsoft Defender for Endpoint version 101.07.23 or later. |

#### Maximum number of items in the antivirus scan history

Specify the maximum number of entries to keep in the scan history. Entries include all on-demand scans performed in the past and all antivirus detections.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `scanHistoryMaximumItems` |
| **Data type** | Integer |
| **Possible values** | `10000` (default). Use an integer from `5000` through `15000`. |
| **Comments** | Available in Microsoft Defender for Endpoint version 101.07.23 or later. |

### Cloud-delivered protection preferences

Configure the cloud-delivered protection features of Microsoft Defender for Endpoint on macOS.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `cloudService` |
| **Data type** | Dictionary (nested preference) |
| **Comments** | The dictionary contents include settings for cloud-delivered protection, diagnostic collection level, cloud block level, automatic sample submissions, security intelligence updates, and proxy configuration. |

#### Configure cloud-delivered protection

Specify whether to enable cloud-delivered protection on the device. Keep this feature enabled for better protection.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `enabled` |
| **Data type** | Boolean |
| **Possible values** | `true` (default) <br>`false` |

#### Diagnostic collection level

Specify the level of diagnostic data that Defender for Endpoint sends to Microsoft. Diagnostic data helps keep the product secure and up to date, diagnose and fix problems, and improve the product.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `diagnosticLevel` |
| **Data type** | String |
| **Possible values** | `optional` (default) <br>`required` |

#### Configure cloud block level

Specify how aggressively Defender for Endpoint blocks and scans suspicious files:

- `normal`: Use the default blocking level.
- `moderate`: Deliver verdicts only for high-confidence detections.
- `high`: Aggressively block unknown files while optimizing for performance. This level increases the chance of blocking nonharmful files.
- `high_plus`: Aggressively block unknown files and apply more protection measures. This level might affect device performance.
- `zero_tolerance`: Block all unknown programs.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `cloudBlockLevel` |
| **Data type** | String |
| **Possible values** | `normal` (default) <br>`moderate`<br><br>`high`<br><br>`high_plus`<br><br>`zero_tolerance` |
| **Comments** | Available in Defender for Endpoint version 101.56.62 or later. |

#### Configure automatic sample submission

Specify which suspicious samples that might contain threats are sent to Microsoft:

- `none`: Don't submit suspicious samples automatically.
- `safe`: Automatically submit only suspicious samples that don't contain personally identifiable information. This value is the default.
- `all`: Automatically submit all suspicious samples.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `automaticSampleSubmissionConsent` |
| **Data type** | String |
| **Possible values** | `none`<br>`safe` (default) <br><br>`all` |

Note

macOS also supports the legacy Boolean key `automaticSampleSubmission`. If a profile contains both keys, `automaticSampleSubmissionConsent` takes precedence.

#### Configure automatic security intelligence updates

Specify whether to install security intelligence updates automatically.

| Section | Value |
| --- | --- |
| **Key** | `automaticDefinitionUpdateEnabled` |
| **Data type** | Boolean |
| **Possible values** | `true` (default) <br>`false` |

#### Duration for security intelligence updates due (in days)

Specify the number of days after which the last installed security intelligence updates are considered outdated.

| Section | Value |
| --- | --- |
| **Key** | `definitionUpdateDue` |
| **Data type** | Integer |
| **Possible values** | `7` (default). Use an integer from `1` through `30`. |

#### Security intelligence update interval (in seconds)

Specify how often Defender for Endpoint checks for security intelligence updates, in seconds.

| Section | Value |
| --- | --- |
| **Key** | `definitionUpdatesInterval` |
| **Data type** | Integer |
| **Possible values** | `28800` (default, 8 hours). Use an integer from `60` (1 minute) through `86400` (24 hours). |
| **Comments** | Setting the value too low might lead to repeated or unnecessary security intelligence update checks. |

#### Proxy for Defender for Endpoint communication

Configure a proxy for Defender for Endpoint cloud communication. If you don't configure this setting, Defender for Endpoint uses the system-wide proxy.

| Section | Value |
| --- | --- |
| **Key** | `proxy` |
| **Data type** | String |
| **Comments** | Use the format `http://proxy.server:port` or `https://proxy.server:port`. |

Important

An incorrect proxy configuration can disrupt Defender for Endpoint functionality. After you apply proxy settings, run `mdatp connectivity test` on the device to test connectivity.

### User interface preferences

Manage the preferences for the user interface of Microsoft Defender for Endpoint on macOS.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `userInterface` |
| **Data type** | Dictionary (nested preference) |
| **Comments** | The dictionary contents include settings for the status menu icon visibility, the feedback option, and consumer version sign-in control. |

#### Configure the status menu icon

Specify whether to show or hide the status menu icon in the top-right corner of the screen.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `hideStatusMenuIcon` |
| **Data type** | Boolean |
| **Possible values** | `false` (default) <br>`true` |

#### Configure the feedback option

Specify whether users can submit feedback to Microsoft by selecting **Help** &gt; **Send Feedback**.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `userInitiatedFeedback` |
| **Data type** | String |
| **Possible values** | `enabled` (default) <br>`disabled` |
| **Comments** | Available in Microsoft Defender for Endpoint version 101.19.61 or later. |

#### Control sign-in to consumer version of Microsoft Defender

Specify whether users can sign into the consumer version of Microsoft Defender.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `consumerExperience` |
| **Data type** | String |
| **Possible values** | `enabled` (default) <br>`disabled` |
| **Comments** | Available in Microsoft Defender for Endpoint version 101.60.18 or later. |

### Endpoint detection and response preferences

Manage preferences for the endpoint detection and response (EDR) component of Microsoft Defender for Endpoint on macOS.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `edr` |
| **Data type** | Dictionary (nested preference) |
| **Comments** | The dictionary contents include settings for device tags and group identifiers. |

#### Device tags

Specify a tag name and value. The `GROUP` tag adds the specified value to the device page in the Microsoft Defender portal, where you can use it to filter and group devices.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `tags` |
| **Data type** | Array of dictionaries |
| **Comments** | Each entry in the array contains a `key` (tag type, such as `GROUP`) and a `value` (the tag string assigned to the device). |

##### Type of tag

Specify the tag type.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `key` |
| **Data type** | String |
| **Possible values** | `GROUP` |

##### Value of tag

Specify the tag value.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `value` |
| **Data type** | String |
| **Possible values** | any string |

Important

- Set only one value for each tag type.
- Don't repeat a tag type in the same configuration profile.

#### Group identifier

Specify the EDR group identifier.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `groupIds` |
| **Data type** | String |
| **Comments** | The group identifier assigned to the device. |

### Tamper protection

Manage preferences for the tamper protection component of Microsoft Defender for Endpoint on macOS.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `tamperProtection` |
| **Data type** | Dictionary (nested preference) |
| **Comments** | The dictionary contents include settings for enforcement level and exclusions. |

#### Enforcement level

Specify the tamper protection enforcement level.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `enforcementLevel` |
| **Data type** | String |
| **Possible values** | `disabled`<br>`audit`<br><br>`block` (default) |

- `disabled`: Turn off tamper protection. Defender for Endpoint doesn't block or report tampering attempts.
- `audit`: Report tampering attempts to the cloud without blocking them.
- `block`: Block and report tampering attempts to the cloud.

#### Exclusions

Define processes that can modify Microsoft Defender assets without the activity being considered tampering. Specify `path`, `teamId`, `signingId`, or a combination of these values. You can also specify `args` to identify the allowed process more precisely.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `exclusions` |
| **Data type** | Array of dictionaries |
| **Comments** | Each dictionary can contain a path, team ID, signing ID, and process arguments. |

##### Path

Specify the exact path of the process executable.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `path` |
| **Data type** | String |
| **Comments** | For a shell script, specify the exact path to the interpreter binary, such as `/bin/zsh`. Wildcards aren't supported. |

##### Team ID

Specify the vendor's Apple team ID.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `teamId` |
| **Data type** | String |
| **Comments** | For example, the Microsoft team ID is `UBF8T346G9`. |

##### Signing ID

Specify the package's Apple signing ID.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `signingId` |
| **Data type** | String |
| **Comments** | For example, the Ruby interpreter signing ID is `com.apple.ruby`. |

##### Process arguments

Specify arguments that, in combination with the other values, identify the process.

| Section | Value |
| --- | --- |
| **Domain** | `com.microsoft.wdav` |
| **Key** | `args` |
| **Data type** | Array of strings |
| **Comments** | Process arguments must match the specified arguments exactly and are case-sensitive. |

## Recommended configuration profile

The recommended configuration profile provides a baseline of commonly used protection settings. Both the Jamf Pro property list and the Intune XML profile in the following sections apply these settings.

This configuration profile (or, for Jamf Pro, a property list uploaded into custom settings) applies the following settings:

- Enable real-time protection.
- Specify how the following threat types are handled:
    - Block potentially unwanted applications.
    - Audit archive bombs, which are files with a high compression rate, in Defender for Endpoint logs.
- Enable automatic security intelligence updates.
- Enable cloud-delivered protection.
- Enable automatic sample submission.

### Property list for Jamf Pro recommended configuration profile

Use the following property list in Jamf Pro for the recommended configuration profile:

```XML
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>antivirusEngine</key>
    <dict>
        <key>enforcementLevel</key>
        <string>real_time</string>
        <key>threatTypeSettings</key>
        <array>
            <dict>
                <key>key</key>
                <string>potentially_unwanted_application</string>
                <key>value</key>
                <string>block</string>
            </dict>
            <dict>
                <key>key</key>
                <string>archive_bomb</string>
                <key>value</key>
                <string>audit</string>
            </dict>
        </array>
    </dict>
    <key>cloudService</key>
    <dict>
        <key>enabled</key>
        <true/>
        <key>automaticSampleSubmission</key>
        <true/>
        <key>automaticDefinitionUpdateEnabled</key>
        <true/>
    </dict>
    <key>tamperProtection</key>
    <dict>
        <key>enforcementLevel</key>
        <string>block</string>
    </dict>
</dict>
</plist>
```

### Intune recommended profile

Use the following XML for the recommended Intune profile:

```XML
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1">
    <dict>
        <key>PayloadUUID</key>
        <string>C4E6A782-0C8D-44AB-A025-EB893987A295</string>
        <key>PayloadType</key>
        <string>Configuration</string>
        <key>PayloadOrganization</key>
        <string>Microsoft</string>
        <key>PayloadIdentifier</key>
        <string>C4E6A782-0C8D-44AB-A025-EB893987A295</string>
        <key>PayloadDisplayName</key>
        <string>Microsoft Defender for Endpoint settings</string>
        <key>PayloadDescription</key>
        <string>Microsoft Defender for Endpoint configuration settings</string>
        <key>PayloadVersion</key>
        <integer>1</integer>
        <key>PayloadEnabled</key>
        <true/>
        <key>PayloadRemovalDisallowed</key>
        <true/>
        <key>PayloadScope</key>
        <string>System</string>
        <key>PayloadContent</key>
        <array>
            <dict>
                <key>PayloadUUID</key>
                <string>99DBC2BC-3B3A-46A2-A413-C8F9BB9A7295</string>
                <key>PayloadType</key>
                <string>com.microsoft.wdav</string>
                <key>PayloadOrganization</key>
                <string>Microsoft</string>
                <key>PayloadIdentifier</key>
                <string>99DBC2BC-3B3A-46A2-A413-C8F9BB9A7295</string>
                <key>PayloadDisplayName</key>
                <string>Microsoft Defender for Endpoint configuration settings</string>
                <key>PayloadDescription</key>
                <string/>
                <key>PayloadVersion</key>
                <integer>1</integer>
                <key>PayloadEnabled</key>
                <true/>
                <key>antivirusEngine</key>
                <dict>
                    <key>enforcementLevel</key>
                    <string>real_time</string>
                    <key>threatTypeSettings</key>
                    <array>
                        <dict>
                            <key>key</key>
                            <string>potentially_unwanted_application</string>
                            <key>value</key>
                            <string>block</string>
                        </dict>
                        <dict>
                            <key>key</key>
                            <string>archive_bomb</string>
                            <key>value</key>
                            <string>audit</string>
                        </dict>
                    </array>
                </dict>
                <key>cloudService</key>
                <dict>
                    <key>enabled</key>
                    <true/>
                    <key>automaticSampleSubmission</key>
                    <true/>
                    <key>automaticDefinitionUpdateEnabled</key>
                    <true/>
                    <key>definitionUpdateDue</key>
                    <integer>7</integer>
                </dict>
                <key>tamperProtection</key>
                <dict>
                    <key>enforcementLevel</key>
                    <string>block</string>
                </dict>
            </dict>
        </array>
    </dict>
</plist>
```

## Full configuration profile example

The following Jamf Pro and Intune templates demonstrate an expanded set of Microsoft Defender for Endpoint preferences. Use them as examples for advanced scenarios, and include only the settings required by your organization.

Caution

The templates contain example values for exclusions, allowed threats, tags, group identifiers, and tamper protection exclusions. Review and replace or remove these values before deployment. In particular, the `allowedThreats` entry permits the EICAR test file to run.

### Property list for Jamf Pro full configuration profile

The following property list shows an expanded Defender for Endpoint configuration profile for Jamf Pro, including antivirus engine, cloud service, EDR, tamper protection, and user interface preferences:

```XML
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>antivirusEngine</key>
    <dict>
        <key>enforcementLevel</key>
        <string>real_time</string>
        <key>scanAfterDefinitionUpdate</key>
        <true/>
        <key>scanArchives</key>
        <true/>
        <key>maximumOnDemandScanThreads</key>
        <integer>2</integer>
        <key>exclusions</key>
        <array>
            <dict>
                <key>$type</key>
                <string>excludedPath</string>
                <key>isDirectory</key>
                <false/>
                <key>path</key>
                <string>/var/log/system.log</string>
            </dict>
            <dict>
                <key>$type</key>
                <string>excludedPath</string>
                <key>isDirectory</key>
                <true/>
                <key>path</key>
                <string>/home</string>
            </dict>
            <dict>
                <key>$type</key>
                <string>excludedPath</string>
                <key>isDirectory</key>
                <true/>
                <key>path</key>
                <string>/Users/*/git</string>
            </dict>
            <dict>
                <key>$type</key>
                <string>excludedFileExtension</string>
                <key>extension</key>
                <string>pdf</string>
            </dict>
            <dict>
                <key>$type</key>
                <string>excludedFileName</string>
                <key>name</key>
                <string>cat</string>
            </dict>
        </array>
        <key>exclusionsMergePolicy</key>
        <string>merge</string>
        <key>allowedThreats</key>
        <array>
            <string>EICAR-Test-File (not a virus)</string>
        </array>
        <key>disallowedThreatActions</key>
        <array>
            <string>allow</string>
            <string>restore</string>
        </array>
        <key>threatTypeSettings</key>
        <array>
            <dict>
                <key>key</key>
                <string>potentially_unwanted_application</string>
                <key>value</key>
                <string>block</string>
            </dict>
            <dict>
                <key>key</key>
                <string>archive_bomb</string>
                <key>value</key>
                <string>audit</string>
            </dict>
        </array>
        <key>threatTypeSettingsMergePolicy</key>
        <string>merge</string>
    </dict>
    <key>cloudService</key>
    <dict>
        <key>enabled</key>
        <true/>
        <key>diagnosticLevel</key>
        <string>optional</string>
        <key>automaticSampleSubmission</key>
        <true/>
        <key>automaticDefinitionUpdateEnabled</key>
        <true/>
        <key>cloudBlockLevel</key>
        <string>normal</string>
        <key>definitionUpdateDue</key>
        <integer>7</integer>
    </dict>
    <key>edr</key>
    <dict>
        <key>tags</key>
        <array>
            <dict>
                <key>key</key>
                <string>GROUP</string>
                <key>value</key>
                <string>ExampleTag</string>
            </dict>
        </array>
    </dict>
    <key>tamperProtection</key>
    <dict>
        <key>enforcementLevel</key>
        <string>block</string>
        <key>exclusions</key>
        <array>
        <dict>
            <key>path</key>
            <string>/bin/zsh</string>
            <key>teamId</key>
            <string/>
            <key>signingId</key>
            <string>com.apple.zsh</string>
            <key>args</key>
            <array>
            <string>/usr/local/bin/test.sh</string>
            </array>
        </dict>
        <dict>
            <key>path</key>
            <string>/usr/local/jamf/bin/jamf</string>
            <key>teamId</key>
            <string>483DWKW443</string>
            <key>signingId</key>
            <string>com.jamfsoftware.jamf</string>
        </dict>
        </array>
    </dict>
    <key>userInterface</key>
    <dict>
        <key>hideStatusMenuIcon</key>
        <false/>
        <key>userInitiatedFeedback</key>
        <string>enabled</string>
    </dict>
</dict>
</plist>
```

### Intune full profile

The following mobile configuration payload wraps all available Defender for Endpoint macOS settings into a deployable Intune profile. It includes antivirus engine, cloud service, EDR, tamper protection, and user interface preferences:

```XML
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1">
    <dict>
        <key>PayloadUUID</key>
        <string>C4E6A782-0C8D-44AB-A025-EB893987A295</string>
        <key>PayloadType</key>
        <string>Configuration</string>
        <key>PayloadOrganization</key>
        <string>Microsoft</string>
        <key>PayloadIdentifier</key>
        <string>C4E6A782-0C8D-44AB-A025-EB893987A295</string>
        <key>PayloadDisplayName</key>
        <string>Microsoft Defender for Endpoint settings</string>
        <key>PayloadDescription</key>
        <string>Microsoft Defender for Endpoint configuration settings</string>
        <key>PayloadVersion</key>
        <integer>1</integer>
        <key>PayloadEnabled</key>
        <true/>
        <key>PayloadRemovalDisallowed</key>
        <true/>
        <key>PayloadScope</key>
        <string>System</string>
        <key>PayloadContent</key>
        <array>
            <dict>
                <key>PayloadUUID</key>
                <string>99DBC2BC-3B3A-46A2-A413-C8F9BB9A7295</string>
                <key>PayloadType</key>
                <string>com.microsoft.wdav</string>
                <key>PayloadOrganization</key>
                <string>Microsoft</string>
                <key>PayloadIdentifier</key>
                <string>99DBC2BC-3B3A-46A2-A413-C8F9BB9A7295</string>
                <key>PayloadDisplayName</key>
                <string>Microsoft Defender for Endpoint configuration settings</string>
                <key>PayloadDescription</key>
                <string/>
                <key>PayloadVersion</key>
                <integer>1</integer>
                <key>PayloadEnabled</key>
                <true/>
                <key>antivirusEngine</key>
                <dict>
                    <key>enforcementLevel</key>
                    <string>real_time</string>
                    <key>behaviorMonitoring</key>
                    <string>enabled</string>
                    <key>scanAfterDefinitionUpdate</key>
                    <true/>
                    <key>scanArchives</key>
                    <true/>
                    <key>maximumOnDemandScanThreads</key>
                    <integer>1</integer>
                    <key>exclusions</key>
                    <array>
                        <dict>
                            <key>$type</key>
                            <string>excludedPath</string>
                            <key>isDirectory</key>
                            <false/>
                            <key>path</key>
                            <string>/var/log/system.log</string>
                        </dict>
                        <dict>
                            <key>$type</key>
                            <string>excludedPath</string>
                            <key>isDirectory</key>
                            <true/>
                            <key>path</key>
                            <string>/home</string>
                        </dict>
                        <dict>
                            <key>$type</key>
                            <string>excludedPath</string>
                            <key>isDirectory</key>
                            <true/>
                            <key>path</key>
                            <string>/Users/*/git</string>
                        </dict>
                        <dict>
                            <key>$type</key>
                            <string>excludedFileExtension</string>
                            <key>extension</key>
                            <string>pdf</string>
                        </dict>
                        <dict>
                            <key>$type</key>
                            <string>excludedFileName</string>
                            <key>name</key>
                            <string>cat</string>
                        </dict>
                    </array>
                    <key>exclusionsMergePolicy</key>
                    <string>merge</string>
                    <key>allowedThreats</key>
                    <array>
                        <string>EICAR-Test-File (not a virus)</string>
                    </array>
                    <key>disallowedThreatActions</key>
                    <array>
                        <string>allow</string>
                        <string>restore</string>
                    </array>
                    <key>threatTypeSettings</key>
                    <array>
                        <dict>
                            <key>key</key>
                            <string>potentially_unwanted_application</string>
                            <key>value</key>
                            <string>block</string>
                        </dict>
                        <dict>
                            <key>key</key>
                            <string>archive_bomb</string>
                            <key>value</key>
                            <string>audit</string>
                        </dict>
                    </array>
                    <key>threatTypeSettingsMergePolicy</key>
                    <string>merge</string>
                </dict>
                <key>cloudService</key>
                <dict>
                    <key>enabled</key>
                    <true/>
                    <key>diagnosticLevel</key>
                    <string>optional</string>
                    <key>automaticSampleSubmission</key>
                    <true/>
                    <key>automaticDefinitionUpdateEnabled</key>
                    <true/>
                    <key>cloudBlockLevel</key>
                    <string>normal</string>
                    <key>definitionUpdateDue</key>
                    <integer>7</integer>
                </dict>
                <key>edr</key>
                <dict>
                    <key>tags</key>
                    <array>
                        <dict>
                            <key>key</key>
                            <string>GROUP</string>
                            <key>value</key>
                            <string>ExampleTag</string>
                        </dict>
                    </array>
                </dict>
                <key>tamperProtection</key>
                <dict>
                    <key>enforcementLevel</key>
                    <string>block</string>
                    <key>exclusions</key>
                    <array>
                    <dict>
                        <key>path</key>
                        <string>/bin/zsh</string>
                        <key>teamId</key>
                        <string/>
                        <key>signingId</key>
                        <string>com.apple.zsh</string>
                        <key>args</key>
                        <array>
                        <string>/usr/local/bin/test.sh</string>
                        </array>
                    </dict>
                    <dict>
                        <key>path</key>
                        <string>/Library/Intune/Microsoft Intune Agent.app/Contents/MacOS/IntuneMdmDaemon</string>
                        <key>teamId</key>
                        <string>UBF8T346G9</string>
                        <key>signingId</key>
                        <string>IntuneMdmDaemon</string>
                    </dict>
                    </array>
                </dict>
                <key>userInterface</key>
                <dict>
                    <key>hideStatusMenuIcon</key>
                    <false/>
                    <key>userInitiatedFeedback</key>
                    <string>enabled</string>
                </dict>
            </dict>
        </array>
    </dict>
</plist>
```

## Property list validation

The property list must be a valid `.plist` file. Before you upload or deploy the profile, validate its syntax by running the following command:

```bash
plutil -lint com.microsoft.wdav.plist
```

If the property list is valid, the command returns exit code `0` and output similar to the following:

```console
com.microsoft.wdav.plist: OK
```

If the property list isn't valid, the command returns exit code `1` and displays an error that describes the issue.

## Configuration profile deployment

After you create and validate the configuration profile, deploy it by using your management tool. Use `com.microsoft.wdav` as the preference domain or custom configuration profile name. Defender for Endpoint doesn't recognize the preferences if you use another value.

### Jamf Pro deployment

> 
> Jamf Pro is a separate third-party product that isn't part of Defender for Endpoint and isn't included with Defender for Endpoint subscriptions. To use Jamf Pro, your organization needs a separate Jamf Pro subscription. For product and subscription information, see [Jamf Pro](https://www.jamf.com/products/jamf-pro/). If your organization doesn't use Jamf Pro, use another configuration method in this article, if available.

To deploy preferences by using the current Jamf Pro schema or the legacy property-list method, see [Configure Defender settings in Jamf Pro](mac-jamfpro-policies#configure-defender-settings-using-the-jamf-pro-gui). For more information from Jamf, see [Deploying Custom Computer Configuration Profiles Using the Application and Custom Settings Payload](https://learn.jamf.com/r/technical-articles/Deploying_Custom_Computer_Configuration_Profiles_Using_the_Application_and_Custom_Settings_Payload).

### Intune deployment

> 
> Microsoft Intune is the recommended tool for configuring and distributing Defender for Endpoint features to devices. However, Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have Intune, you can use any of the other methods in this article. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

To create and deploy the custom configuration profile in Intune, see [Set policies in Microsoft Intune](mac-install-with-intune#9b-set-policies-using-microsoft-intune).

### Other MDM solutions

To deploy the configuration profile by using another MDM solution, see [Deploy Defender for Endpoint settings](mac-install-with-other-mdm#deploy-defender-for-endpoint-settings).