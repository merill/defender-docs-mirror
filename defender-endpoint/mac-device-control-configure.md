---
layout: Conceptual
title: Configure Microsoft Defender for Endpoint Device Control on macOS - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/mac-device-control-configure
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Create, validate, deploy, and verify a Microsoft Defender for Endpoint Device Control policy on macOS by using Microsoft Intune, Jamf Pro, or a local test policy.
ms.service: defender-endpoint
author: limwainstein
ms.author: lwainstein
ms.reviewer: joshbregman
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-macos
ms.topic: how-to
ms.subservice: macos
ms.date: 2026-09-17T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: 0b9c0741-09c8-4719-185b-6f0895331d2a
document_version_independent_id: 0b9c0741-09c8-4719-185b-6f0895331d2a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/mac-device-control-configure.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mac-device-control-configure
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/mac-device-control-configure.md
platformId: 34cd54e8-8e24-6d88-c77b-a749c3a6bcc9
---

# Configure Microsoft Defender for Endpoint Device Control on macOS - Microsoft Defender for Endpoint | Microsoft Learn

Create and validate a Device Control policy, and then deploy it to macOS devices by using Microsoft Intune or Jamf Pro. You can also apply the policy locally on a test Mac before you deploy it to managed devices. For information about Device Control capabilities, policy settings, and requirements, see [Microsoft Defender for Endpoint Device Control for macOS](mac-device-control-overview).

## Prerequisites

- Completion of the [Device Control requirements](mac-device-control-overview#requirements) and [endpoint preparation](mac-device-control-overview#prepare-your-endpoints).
- Review the [permissions required for your management tool](mac-device-control-overview#permissions).
- The requirements for your deployment method:
    - **Microsoft Intune**: An Intune subscription and [Defender for Endpoint installed and onboarded by using Intune](mac-install-with-intune).

        Microsoft Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).
    - **Jamf Pro**: A Jamf Pro subscription, [Defender for Endpoint installed and onboarded by using Jamf Pro](mac-install-with-jamf), and [Full Disk Access granted by using Jamf Pro](mac-jamfpro-policies#step-6-grant-full-disk-access-to-microsoft-defender-for-endpoint).

        Jamf Pro is a separate product that isn't part of Defender for Endpoint and isn't included with Defender for Endpoint subscriptions. For product and subscription information, see [Jamf Pro](https://www.jamf.com/products/jamf-pro/).

        Important

        Microsoft provides information about Jamf Pro to support integration scenarios but doesn't provide troubleshooting support for this third-party product. For issues specific to Jamf Pro, contact Jamf support.
    - **Manual testing**: Defender for Endpoint version `101.23082.0018` or later [installed and onboarded manually](mac-install-manually) on a test Mac that doesn't have a Device Control policy managed by mobile device management (MDM).

## Create and validate the Device Control policy

A Device Control policy for macOS is one JSON object that contains settings, device groups, and rules. For descriptions of the policy properties, see [Understand Device Control policies](mac-device-control-overview#understanding-policies).

1. Use the [deny removable media except Kingston sample](https://github.com/microsoft/mdatp-devicecontrol/blob/main/macOS/policy/samples/deny_removable_media_except_kingston.json) or another [Device Control policy sample](https://github.com/microsoft/mdatp-devicecontrol/tree/main/macOS/policy/samples) as a starting point.
2. Validate the policy structure against the [Device Control policy JSON schema](https://github.com/microsoft/mdatp-devicecontrol/blob/main/macOS/policy/device_control_policy_schema.json).
3. Save the policy as `device-control-policy.json` in the `~/Downloads` folder on a test Mac that has Defender for Endpoint installed.
4. Run the following command in Terminal:

    ```bash
    mdatp device-control policy validate --path ~/Downloads/device-control-policy.json
    ```
5. Resolve any validation errors before you deploy or apply the policy.

## Deploy the policy by using Microsoft Intune

Use a custom macOS configuration profile to deploy the policy through Intune.

### Create the Apple configuration profile

1. Download the [Device Control sample configuration profile](https://github.com/microsoft/mdatp-devicecontrol/blob/main/macOS/mobileconfig/demo.mobileconfig).
2. In the `deviceControl` dictionary, replace the JSON value in the `policy` string with your validated Device Control policy.
3. Keep the `dlp` settings that enable the `DC_in_dlp` feature.
4. Save the file as `device-control.mobileconfig`.

### Deploy the configuration profile

Create a custom macOS configuration profile in Intune. For detailed instructions, see [Add custom settings to Apple devices in Microsoft Intune](/en-us/intune/device-configuration/templates/configure-custom-settings-apple) (link opens in a new tab).

1. On the **Policies** tab of the **Devices | Configuration** page in the Microsoft Intune admin center at [https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/configuration](https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/DevicesMenu/%7E/configuration), select ![](media/defender-portal-icon-create.png)**Create** &gt; ![](media/defender-portal-icon-create.png)**New policy**.
2. Use the following settings:

    - **Platform**: Select **macOS**.
    - **Profile type**: Select **Templates**.
    - **Template name**: Select **Custom**.
3. In the **Custom** wizard, use the following settings on the **Configuration settings** tab:

    - **Configuration profile name**: Enter a descriptive name, such as `Microsoft Defender device control`.
    - **Deployment channel**: Select **Device channel**.
    - **Configuration profile file**: Select the `device-control.mobileconfig` file that you created.

## Deploy the policy by using Jamf Pro

Use the Defender for Endpoint preference schema to add the Device Control policy to a Jamf Pro computer configuration profile.

1. Download the current [Defender for Endpoint preference schema](https://github.com/microsoft/mdatp-xplat/blob/master/macos/schema/schema.json).
2. Follow the Jamf instructions to [deploy a custom computer configuration profile](https://learn.jamf.com/r/technical-articles/Deploying_Custom_Computer_Configuration_Profiles_Using_the_Application_and_Custom_Settings_Payload).
3. Use the following Defender-specific settings:

    - **Preference Domain**: Enter `com.microsoft.wdav`.
    - **Schema**: Upload the downloaded `schema.json` file.
    - **Property**: Add **Device Control**, and then add **Device Control Policy**.
    - **Value**: Paste the complete Device Control policy JSON.
    - **Scope**: Select the computer group that contains the target macOS devices.
4. Save and deploy the configuration profile.

## Test the policy manually

Use manual policy deployment only in preproduction environments. For production environments, deploy Device Control by using Microsoft Intune or Jamf Pro.

1. Apply the validated policy to the test Mac:

    ```bash
    mdatp config device-control policy set --path ~/Downloads/device-control-policy.json
    ```
2. To test policy changes, edit the JSON file, validate it, and then rerun the command to apply the updated policy.

## Verify Device Control

After you deploy or apply the policy, use the following commands in Terminal to verify Device Control on a target Mac.

1. Inspect Device Control status:

    ```bash
    mdatp health --details device_control
    ```

    The command returns output similar to the following example:

    ```console
    active                                      : ["v2"]
    v1_configured                               : false
    v1_enforcement_level                        : unavailable
    v2_configured                               : true
    v2_state                                    : "enabled"
    v2_sensor_connection                        : "created_ok"
    v2_full_disk_access                         : "approved"
    ```

    Review the following values:

    - `active`: Lists the active policy versions:
        - `[]`: Device Control isn't configured.
        - `["v1"]`: Version 1 is active. Version 1 is obsolete and isn't covered in this documentation.
        - `["v2"]`: Version 2 is active.
        - `["v1", "v2"]`: Both versions are active. Remove the version 1 configuration.
    - `v1_configured`: Indicates whether a version 1 configuration is applied.
    - `v1_enforcement_level`: Shows the enforcement level when version 1 is enabled.
    - `v2_configured`: Indicates whether a version 2 configuration is applied. A working configuration reports `true`.
    - `v2_state`: Shows the version 2 state. A working configuration reports `enabled`.
    - `v2_sensor_connection`: Shows the connection to the system extension. A working connection reports `created_ok`.
    - `v2_full_disk_access`: Shows whether Full Disk Access is approved. If the value isn't `approved`, Device Control might not prevent some or all operations.
2. View the effective Device Control preferences:

    ```bash
    mdatp device-control policy preferences list
    ```

    The command returns output similar to the following example:

    ```console
    .Preferences
    |-o UX
    | |-o Navigation Target: "https://www.microsoft.com"
    |-o Features
    | |-o Removable Media
    |   |-o Disable: false
    |-o Global
      |-o Default Enforcement: "allow"
    ```

    Review the **Default Enforcement** value in the output.
3. View the deployed rules:

    ```bash
    mdatp device-control policy rules list
    ```
4. View the groups referenced by the policy:

    ```bash
    mdatp device-control policy groups list
    ```
5. Test the protected operations that the policy allows, denies, or audits.

## Remove a manually applied policy

Remove the local policy from the test Mac when you finish testing:

```bash
mdatp config device-control policy reset
```