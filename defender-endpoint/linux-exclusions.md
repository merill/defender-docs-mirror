---
layout: Conceptual
title: Linux exclusions for Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/linux-exclusions
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to configure and validate antivirus and global exclusions for files, folders, processes, and file extensions in Microsoft Defender for Endpoint on Linux.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.reviewer: ratujdange, ardeshmukh
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-linux
ms.topic: how-to
ms.subservice: linux
ms.date: 2026-09-16T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
locale: en-us
document_id: e889b94c-08af-03af-60af-2d1fa81a6a5e
document_version_independent_id: e889b94c-08af-03af-60af-2d1fa81a6a5e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/linux-exclusions.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: linux-exclusions
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/linux-exclusions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: b131a608-0e92-4f7b-3406-626713f27d41
---

# Linux exclusions for Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Use exclusions to prevent Microsoft Defender for Endpoint on Linux from scanning or monitoring trusted files, folders, processes, and file extensions. Exclusions can help avoid incorrect detections for files or software unique to your organization.

Defender for Endpoint on Linux supports the following exclusion scopes:

- **Antivirus** (scope `epp`): Exclusions apply to on-demand scans, real-time protection (RTP), and behavior monitoring (BM), while retaining endpoint detection and response (EDR) visibility.

    - Files excluded from antivirus scanning can still result in EDR alerts and other detections. To request an EDR-only exclusion, [contact Microsoft Support through the Microsoft 365 admin center](/en-us/microsoft-365/admin/get-help-support).
- **Global** (scope `global`): Exclusions apply to RTP, BM, and EDR, which stops associated antivirus detections, EDR alerts, and visibility for the excluded item. Global exclusions apply at the sensor level and mute events that match exclusion conditions before processing.

    - Global exclusions are available in Defender for Endpoint on Linux version `101.24092.0001` (October 2024) or later.
    - Global exclusions don't apply to network protection. Process exclusions can affect network protection by preventing it from inspecting traffic or enforcing rules for the excluded process. For more information, see [Overview of exclusions and indicators in Microsoft Defender for Endpoint](defender-endpoint-exclusions-overview#types-of-exclusions).
    - Global exclusions can be useful for mitigating performance issues caused by Defender for Endpoint on Linux.

Warning

Defining exclusions lowers the protection offered by Defender for Endpoint on Linux. You should always evaluate the risks that are associated with implementing exclusions, and you should only exclude files that you're confident aren't malicious.

Important

If you want to run multiple security solutions side by side, see [Considerations for performance, configuration, and support](/en-us/defender-endpoint/mde-side-by-side).

You might have already configured mutual security exclusions for devices onboarded to Microsoft Defender for Endpoint. If you still need to set mutual exclusions to avoid conflicts, see [Add Microsoft Defender for Endpoint to the exclusion list for your existing solution](/en-us/defender-endpoint/switch-to-mde-phase-2#step-2-add-microsoft-defender-for-endpoint-to-the-exclusion-list-for-your-existing-solution).

## Supported exclusion types

Defender for Endpoint on Linux supports the following exclusion types:

- **File extension**: All files with the specified extension anywhere on the device.

    - File extension exclusions aren't available for global exclusions.
    - **Example**: `.test`
- **File**: A specific file identified by its full path.

    - For global exclusions, the file path must exist before you add or remove the exclusion.
    - **Examples**:
        - `/var/log/test.log`
        - `/var/log/*.log`
        - `/var/log/install.?.log`
- **Folder**: All files in the specified folder, recursively.

    - **Examples**:
        - `/var/log/`
        - `/var/*/`
- **Process**: A specific process, identified by its full path or file name, and all files opened by the process.

    - For antivirus exclusions, you can specify either a full path or file name. We recommend using the full path.
    - For global exclusions, exclude only what's needed for system reliability and security. Verify that the process is known and trusted, specify its full path, and confirm that it consistently starts from that trusted path.
    - **Examples**:
        - `/bin/cat`
        - `cat`
        - `c?t`

Important

Exclusion paths must be hard links, not symbolic links. To check whether a path is a symbolic link, run `file <path-name>`.

### Supported wildcards for file, folder, and process exclusions

You can use the following wildcard patterns when defining antivirus file, folder, and process exclusions. Wildcards aren't supported for global exclusions.

- **Asterisk (`*`)**: Matches any number of characters, including no characters. If this wildcard isn't used at the end of the path, it substitutes for only one folder.

    - For antivirus exclusions, an `*` wildcard at the end of the path matches all files and subdirectories under the parent of the wildcard.
    - **Examples**:
        - `/var/*/tmp`:
            - **Includes**: Any file in `/var/abc/tmp` and `/var/def/tmp` and their subfolders.
            - **Doesn't include**: `/var/abc/log` or `/var/def/log`.
        - `/var/*/`:
            - **Includes**: Files in subdirectories such as `/var/abc/`
            - **Doesn't include**: Files directly in `/var`.
- **Question mark (`?`)**: Matches any single character.

    - **Example**: `file?.log`
        - **Includes**: `file1.log` and `file2.log`.
        - **Doesn't include**: `file123.log`.

## Configure exclusions

Use one of the following methods to configure exclusions.

### Configure exclusions using managed JSON

In enterprise environments, use a configuration management tool such as Puppet or Ansible to deploy a configuration profile named `mdatp_managed.json` to `/etc/opt/microsoft/mdatp/managed/`. For more information, see [Set preferences for Defender for Endpoint on Linux](linux-preferences).

The following `mdatp_managed.json` example shows how to configure antivirus and global exclusions for files, folders, extensions, and processes:

```JSON
{
   "exclusionSettings":{
     "exclusions":[
        {
           "$type":"excludedPath",
           "isDirectory":true,
           "path":"/home/*/git<EXAMPLE DO NOT USE>",
           "scopes": [
              "epp"
           ]
        },
        {
           "$type":"excludedPath",
           "isDirectory":true,
           "path":"/run<EXAMPLE DO NOT USE>",
           "scopes": [
              "global"
           ]
        },
        {
           "$type":"excludedPath",
           "isDirectory":false,
           "path":"/var/log/system.log<EXAMPLE DO NOT USE><EXCLUDED IN ALL SCENARIOS>",
           "scopes": [
              "epp", "global"
           ]
        },
        {
           "$type":"excludedFileExtension",
           "extension":".pdf<EXAMPLE DO NOT USE>",
           "scopes": [
              "epp"
           ]
        },
        {
           "$type":"excludedFileName",
           "name":"/bin/cat<EXAMPLE DO NOT USE><NO SCOPE PROVIDED - GLOBAL CONSIDERED>"
        }
     ],
     "mergePolicy":"admin_only"
   }
}
```

### Configure exclusions using Defender for Endpoint security settings management

Note

Before you begin, review the [Defender for Endpoint security settings management prerequisites](/en-us/intune/device-security/microsoft-defender/security-settings-management#prerequisites).

You can use the Microsoft Intune admin center or the Microsoft Defender portal to manage exclusions as endpoint security policies and assign the policies to Microsoft Entra groups. If you're using security settings management for the first time, complete the following steps:

#### Step 1: Enable security settings management for Linux

1. Go to the **Endpoints** &gt; **Configuration Management** &gt; **Enforcement scope** page in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/endpoints/configuration_management.
2. On the **Enforcement scope** page, verify the following setting in the **Enable configuration management**section:
    - Select **Linux devices**and then select one of the following values:
        - Select **On tagged devices** to test security settings management with selected devices. Add the `MDE-Management` tag to each test device. For instructions and other tagging methods, see [Create and manage device tags](machine-tags#create-tags).
        - Select **All devices** to enroll all eligible Linux devices.

Most devices enroll and apply assigned policies within a few minutes, although some devices might take up to 24 hours.

#### Step 2: Create a Microsoft Entra device group

Create a dynamic Microsoft Entra device group based on the Linux operating system type. Dynamic membership automatically adds matching devices, so you don't need to maintain group membership manually. For more information, see [Create Microsoft Entra groups for security settings management](/en-us/intune/device-security/microsoft-defender/security-settings-management#create-microsoft-entra-groups).

#### Step 3: Create a Linux exclusions policy

For detailed instructions, see [Create an endpoint security policy](endpoint-security-policies-configure#create-an-endpoint-security-policy) (link opens in a new tab).

When you create the policy on the **Linux policies** tab of the **Endpoint security policies** page in the Defender portal at https://security.microsoft.com/policy-inventory?osPlatform=Linux, use these specific settings:

- **Select platform**: Select **Linux**.
- **Select template**:
    - For global antivirus and EDR exclusions, select **Microsoft Defender Global Exclusions (AV+EDR)**.
    - For antivirus exclusions, select **Microsoft Defender Antivirus exclusions**.

In the policy creation wizard, use these settings:

- **Configuration settings** tab: Configure the settings you want to manage with this profile.
- **Assignments** tab: Assignment group limitations apply to devices managed through Defender for Endpoint security settings management. For details, see the [Assignments step](endpoint-security-policies-configure#create-an-endpoint-security-policy).

### Configure exclusions using the command line

To view the available subcommands and options for managing exclusions, run the `mdatp exclusion` command:

```bash
mdatp exclusion
```

#### Command syntax

The following syntax summarizes the available exclusion subcommands, options, and values:

```text
mdatp exclusion {extension {add|remove} --name <extension> | file {add|remove} --path <file-path> [--scope {epp|global}] | folder {add|remove} --path <folder-path> [--scope {epp|global}] | process {add|remove} {--path <process-path> [--scope {epp|global}] | --name <process-name> [--scope epp]} | list}
```

Note

When you remove an exclusion, specify the same scope that you used when you added it.

The default value for the `--scope` option is `epp`, so specify the option only for `global` exclusions.

Before the `--scope` option was introduced, all command-line exclusions used the `epp` scope. Those existing exclusions continue to use `epp`.

When an exclusion value contains a wildcard, enclose the value in double quotation marks. This syntax prevents the shell from expanding the wildcard before `mdatp` processes it.

#### Add or remove file extension exclusions

File extension exclusions support only the antivirus (`epp`) scope. The following commands add and remove the `.txt` extension exclusion:

```bash
mdatp exclusion extension add --name .txt

mdatp exclusion extension remove --name .txt
```

#### Add or remove file exclusions

The file must exist before you add or remove an exclusion with the `global` scope.

The following commands add and remove an antivirus (`epp`) file exclusion:

```bash
mdatp exclusion file add --path /var/log/dummy.log

mdatp exclusion file remove --path /var/log/dummy.log
```

The following commands add and remove a global file exclusion:

```bash
mdatp exclusion file add --path /var/log/dummy.log --scope global

mdatp exclusion file remove --path /var/log/dummy.log --scope global
```

#### Add or remove folder exclusions

The following commands add and remove an antivirus (`epp`) folder exclusion:

```bash
mdatp exclusion folder add --path /var/log/

mdatp exclusion folder remove --path /var/log/
```

The following commands add and remove a global folder exclusion:

```bash
mdatp exclusion folder add --path /var/log/ --scope global

mdatp exclusion folder remove --path /var/log/ --scope global
```

Run the command once for each folder that you want to exclude. You can assign different scopes to different folders.

Antivirus folder exclusions support wildcards. The following command excludes paths under `*/var/*/tmp/*`, but not sibling folders such as `*/var/this-subfolder/log*`:

```bash
mdatp exclusion folder add --path "/var/*/tmp"
```

To exclude all paths under `/var/`, use either of the following commands:

```bash
mdatp exclusion folder add --path "/var/"

mdatp exclusion folder add --path "/var/*/"
```

#### Add or remove process exclusions

For global process exclusions, specify the full process path by using `--path`. The following commands add and remove a global process exclusion:

```bash
mdatp exclusion process add --path /usr/bin/cat --scope global

mdatp exclusion process remove --path /usr/bin/cat  --scope global
```

For antivirus (`epp`) process exclusions, you can specify the process name or full path. The following commands add and remove an antivirus process exclusion by name:

```bash
mdatp exclusion process add --name cat

mdatp exclusion process remove --name cat
```

Run the command once for each process that you want to exclude. You can assign different scopes to different processes.

## Validate exclusions with the EICAR test file

The [EICAR test file](https://www.eicar.org/download-anti-malware-testfile/) is a small, harmless text file that contains a standard string recognized by antivirus products as malware. You can use it to safely confirm that an exclusion works without using real malware. Defender for Endpoint on Linux detects the file by its content, not its file name.

Before testing an exclusion, verify that real-time protection is enabled. Run the following command and confirm that it returns `true`:

```bash
mdatp health --field real_time_protection_enabled
```

Create the EICAR test file so that its file name, extension, or location matches the exclusion that you want to validate:

- Use a specific file name or create the file in a specific folder to validate file and folder exclusions.
- Use any file name with the excluded extension to validate a file extension exclusion.

If Defender for Endpoint detects the file, the exclusion doesn't work. If the file exists and Defender for Endpoint doesn't detect it, the exclusion works.

These steps are designed to validate file, folder, and file extension exclusions. They don't provide a general test for process exclusions, which depend on the process that creates or opens the file.

Use one of the following methods to create an EICAR test file that matches your exclusion:

- **With internet access**: Use the following `curl` syntax to download the test file:

    ```bash
    curl -o <file-name-or-path> https://secure.eicar.org/eicar.com.txt
    ```

    For example, if you excluded the `.testing` extension, download the test file with that extension:

    ```bash
    curl -o test.testing https://secure.eicar.org/eicar.com.txt
    ```

    To test a folder exclusion, run the command in that folder.
- **Without internet access**: Create the EICAR test file locally. For example, change `test.txt` to a file name or path that matches your exclusion:

    ```bash
    echo 'X5O!P%@AP[4\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*' > test.txt
    ```