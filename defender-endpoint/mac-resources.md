---
layout: Conceptual
title: Resources for Microsoft Defender for Endpoint on macOS - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/mac-resources
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use Microsoft Defender for Endpoint commands on macOS, collect diagnostics, manage quarantine, enable autocompletion, and uninstall the app.
ms.service: defender-endpoint
author: paulinbar
ms.author: painbar
ms.reviewer: joshbregman
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-macos
ms.topic: troubleshooting-general
ms.subservice: macos
ms.date: 2026-09-18T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: 914adc50-1385-c3a7-0d6e-255c27f83661
document_version_independent_id: 914adc50-1385-c3a7-0d6e-255c27f83661
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/mac-resources.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mac-resources
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/mac-resources.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 92019f28-c375-874e-69ef-f905395ce088
---

# Resources for Microsoft Defender for Endpoint on macOS - Microsoft Defender for Endpoint | Microsoft Learn

Use the `mdatp` command-line tool to configure Microsoft Defender for Endpoint, run scans, manage detected threats, and check product health on macOS devices. You can also collect diagnostic information, enable command autocompletion, manage quarantined files, and uninstall Defender for Endpoint.

For product requirements and deployment methods, see [Prerequisites for Microsoft Defender for Endpoint on macOS](microsoft-defender-endpoint-mac-prerequisites) and [Microsoft Defender for Endpoint on macOS](microsoft-defender-endpoint-mac).

## Collect diagnostic information

If you can reproduce a problem, increase the logging level, run the system for some time, and then restore the logging level to the default.

1. Set the logging level to `debug`:

    ```bash
    mdatp log level set --level debug
    ```

    ```Output
    Log level configured successfully
    ```
2. Reproduce the problem.
3. Create a `.zip` archive that contains the Defender for Endpoint diagnostic logs. The command displays the archive path after it succeeds:

    Tip

    By default, diagnostic logs are saved to `/Library/Application Support/Microsoft/Defender/wdavdiag/`. To use another directory, add `--path [directory]` to the command and replace `[directory]` with the destination.

    ```bash
    sudo mdatp diagnostic create
    ```

    ```console
    Diagnostic file created: "/Library/Application Support/Microsoft/Defender/wdavdiag/932e68a8-8f2e-4ad0-a7f2-65eb97c0de01.zip"
    ```
4. Restore the logging level to the default value, `info`:

    ```bash
    mdatp log level set --level info
    ```

    ```console
    Log level configured successfully
    ```

## Review installation logs

If installation fails, the installer might report only a general failure. Detailed information is available in `/Library/Logs/Microsoft/mdatp/install.log`. Include this file when you open a Microsoft support case.

For more troubleshooting guidance, see [Troubleshoot installation issues for Microsoft Defender for Endpoint on macOS](mac-support-install).

## Configure from the command line

### Configure the output format

The command-line tool supports table and JSON output. Use one of the following global options with a command:

- `--output json`
- `--output table`

### Supported commands

The following table lists commands for common scenarios. To view the complete list of commands supported by your installed product version, run `mdatp help` in Terminal.

| Group | Scenario | Command |
| --- | --- | --- |
| Configuration | Turn passive mode on or off | `mdatp config passive-mode --value [enabled/disabled]` |
| Configuration | Turn real-time protection on or off | `mdatp config real-time-protection --value [enabled/disabled]` |
| Configuration | Turn behavior monitoring on or off | `mdatp config behavior-monitoring --value [enabled/disabled]` |
| Configuration | Turn cloud protection on or off | `mdatp config cloud --value [enabled/disabled]` |
| Configuration | Turn cloud diagnostics on or off | `mdatp config cloud-diagnostic --value [enabled/disabled]` |
| Configuration | Turn automatic sample submission on or off | `mdatp config cloud-automatic-sample-submission --value [enabled/disabled]` |
| Configuration | Block, audit, or turn off potentially unwanted application protection | `mdatp threat policy set --type potentially_unwanted_application --action [block\|audit\|off]` |
| Configuration | Add or remove an antivirus exclusion for a process | `mdatp exclusion process [add\|remove] --path [path-to-process]`<br>`mdatp exclusion process [add\|remove] --name [process-name]` |
| Configuration | Add or remove an antivirus exclusion for a file | `mdatp exclusion file [add/remove] --path [path-to-file]` |
| Configuration | Add or remove an antivirus exclusion for a directory | `mdatp exclusion folder [add/remove] --path [path-to-directory]` |
| Configuration | Add or remove an antivirus exclusion for a file extension | `mdatp exclusion extension [add/remove] --name [extension]` |
| Configuration | List all antivirus exclusions | `mdatp exclusion list` |
| Configuration | Configure degree of parallelism for on-demand scans | `mdatp config maximum-on-demand-scan-threads --value [numerical-value-between-1-and-64]` |
| Configuration | Turn scans after security intelligence updates on or off | `mdatp config scan-after-definition-update --value [enabled/disabled]` |
| Configuration | Turn archive scanning on or off for on-demand scans | `mdatp config scan-archives --value [enabled/disabled]` |
| Configuration | Turn file hash computation on or off | `mdatp config enable-file-hash-computation --value [enabled/disabled]` |
| Protection | Scan a path | `mdatp scan custom --path [path] [--ignore-exclusions]` |
| Protection | Run a quick scan | `mdatp scan quick` |
| Protection | Run a full scan | `mdatp scan full` |
| Protection | Cancel an ongoing on-demand scan | `mdatp scan cancel` |
| Protection | Request a security intelligence update | `mdatp definitions update` |
| Configuration | Add a threat name to the allowed list | `mdatp threat allowed add --name [threat-name]` |
| Configuration | Remove a threat name from the allowed list | `mdatp threat allowed remove --name [threat-name]` |
| Configuration | List all allowed threat names | `mdatp threat allowed list` |
| Protection history | Print the full protection history | `mdatp threat list` |
| Protection history | Get threat details | `mdatp threat get --id [threat-id]` |
| Quarantine management | List all quarantined files | `mdatp threat quarantine list` |
| Quarantine management | Remove all files from the quarantine | `mdatp threat quarantine remove-all` |
| Quarantine management | Add a file detected as a threat to the quarantine | `mdatp threat quarantine add --id [threat-id]` |
| Quarantine management | Remove a file detected as a threat from the quarantine | `mdatp threat quarantine remove --id [threat-id]` |
| Quarantine management | Restore a file from quarantine. Available in Defender for Endpoint versions earlier than `101.23092.0012`. | `mdatp threat quarantine restore --id [threat-id] --path [destination-folder]` |
| Quarantine management | Restore a file from quarantine by using the threat ID. Available in Defender for Endpoint version `101.23092.0012` or later. | `mdatp threat quarantine restore threat-id --id [threat-id] --destination-path [destination-folder]` |
| Quarantine management | Restore a file from quarantine by using its original path. Available in Defender for Endpoint version `101.23092.0012` or later. | `mdatp threat quarantine restore threat-path --path [threat-original-path] --destination-path [destination-folder]` |
| Network protection configuration | Configure the network protection enforcement level | `mdatp config network-protection enforcement-level --value [block\|audit\|disabled]` |
| Network protection management | Verify that network protection started successfully | `mdatp health --field network_protection_status` |
| Device Control management | View whether Device Control is enabled and its default enforcement level | `mdatp device-control policy preferences list` |
| Device Control management | View the active Device Control rules | `mdatp device-control policy rules list` |
| Device Control management | View the groups referenced by the Device Control policy | `mdatp device-control policy groups list` |
| Configuration | Turn data loss prevention on or off | `mdatp config data_loss_prevention --value [enabled/disabled]` |
| Diagnostics | Change the log level | `mdatp log level set --level [error\|warning\|info\|debug]` |
| Diagnostics | Generate diagnostic logs | `mdatp diagnostic create --path [directory]` |
| Health | Check the product's health | `mdatp health` |
| Health | Check a specific product attribute, such as `healthy`, `licensed`, or `engine_version` | `mdatp health --field [attribute]` |
| EDR | Set a device tag. Only `GROUP` is supported. | `mdatp edr tag set --name GROUP --value [name]` |
| EDR | Remove a group tag from the device | `mdatp edr tag remove --tag-name [name]` |
| EDR | Add a group ID | `mdatp edr group-ids --group-id [group]` |

### Enable command-line autocompletion

To enable autocompletion in Bash, add the Defender for Endpoint completion script to your Bash profile, and then restart the Terminal session:

```bash
echo "source /Applications/Microsoft\ Defender.app/Contents/Resources/Tools/mdatp_completion.bash" >> ~/.bash_profile
```

To enable autocompletion in Z shell (zsh), follow these steps:

1. Check whether autocompletion is enabled on your device:

    ```zsh
    cat ~/.zshrc | grep autoload
    ```
2. If the command doesn't produce any output, enable autocompletion in your zsh profile:

    ```zsh
    echo "autoload -Uz compinit && compinit" >> ~/.zshrc
    ```
3. Create the completion directory and link the Defender for Endpoint completion script:

    ```zsh
    sudo mkdir -p /usr/local/share/zsh/site-functions
    
    sudo ln -svf "/Applications/Microsoft Defender.app/Contents/Resources/Tools/mdatp_completion.zsh" /usr/local/share/zsh/site-functions/_mdatp
    ```

## Manage the client quarantine directory

Defender for Endpoint stores quarantined files in `/Library/Application Support/Microsoft/Defender/quarantine/`. File names use the threat tracking ID. To view current tracking IDs, run `mdatp threat list`. Use the `mdatp threat quarantine` commands to manage quarantined files instead of modifying the files directly.

## Uninstall Defender for Endpoint

Before you uninstall Defender for Endpoint, offboard the device and remove or update the policies that manage it. For the optional device-retirement tags, tamper protection requirements, offboarding package, and system extension policy cleanup, see [Offboard Mac devices](offboard-machines#offboard-mac-devices).

You can uninstall the app interactively or from the command line. If you manage devices with Jamf Pro, deploy the offboarding profile before you remove the application. Centrally managed uninstallation isn't currently available in Microsoft Intune.

### Uninstall interactively

In Finder, open **Applications**, Control-click **Microsoft Defender**, and then select **Move to Trash**.

### Uninstall from the command line

Run `sudo '/Library/Application Support/Microsoft/Defender/uninstall/uninstall'` in Terminal.

### Offboard with Jamf Pro before uninstalling

> 
> Jamf Pro is a separate third-party product that isn't part of Defender for Endpoint and isn't included with Defender for Endpoint subscriptions. To use Jamf Pro, your organization needs a separate Jamf Pro subscription. For product and subscription information, see [Jamf Pro](https://www.jamf.com/products/jamf-pro/). If your organization doesn't use Jamf Pro, use another configuration method in this article, if available.

To offboard a device through Jamf Pro before you remove the application, follow the Jamf instructions to [upload a configuration profile](https://learn.jamf.com/r/jamf-pro-documentation-current/Uploading_a_Configuration_Profile_macOS). Upload the Defender for Endpoint offboarding profile without modifying it, and set **Preference Domain** to `com.microsoft.wdav.atp.offboarding`.

Note

If you have trouble uninstalling Defender for Endpoint and reports contain an item for *Microsoft Defender Endpoint Security Extension*, follow these steps:

1. Reinstall the Microsoft Defender app.
2. Drag **Microsoft Defender.app** to **Trash**.
3. Run the following command in Terminal:

    ```bash
    sudo '/Library/Application Support/Microsoft/Defender/uninstall/install_helper' execute --path '/Library/Application Support/Microsoft/Defender/uninstall/uninstall' --args --post-uninstall-hook
    ```
4. Restart the device.

## Use the Microsoft Defender portal

Use the [Microsoft Defender portal](https://security.microsoft.com) to review detections and take response actions on devices. For more information, see the following resources:

- [Overview of endpoint detection and response](overview-endpoint-detection-response)
- [Tech Community blog: EDR capabilities for macOS have now arrived](https://techcommunity.microsoft.com/blog/microsoftdefenderatpblog/edr-capabilities-for-macos-have-now-arrived/1047801)
- [Microsoft Defender portal overview](/en-us/defender-xdr/microsoft-365-defender-portal)