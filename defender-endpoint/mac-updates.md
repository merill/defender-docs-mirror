---
layout: Conceptual
title: Deploy updates for Microsoft Defender for Endpoint on macOS - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/mac-updates
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use Microsoft AutoUpdate and msupdate to manage Microsoft Defender for Endpoint software updates and update channels on macOS.
ms.service: defender-endpoint
author: paulinbar
ms.author: painbar
ms.reviewer: joshbregman
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-macos
ms.topic: install-set-up-deploy
ms.subservice: macos
ms.date: 2026-09-18T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: 09c95937-e34b-f256-98b2-898f7846070a
document_version_independent_id: 09c95937-e34b-f256-98b2-898f7846070a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/mac-updates.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mac-updates
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/mac-updates.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 6634e88a-2db6-2d82-9eaf-3876830092f3
---

# Deploy updates for Microsoft Defender for Endpoint on macOS - Microsoft Defender for Endpoint | Microsoft Learn

Microsoft Defender for Endpoint on macOS receives software updates through Microsoft AutoUpdate (MAU). Security administrators can use MAU configuration profiles to control automatic updates and update channels, or use the `msupdate` command-line tool to start updates on demand.

By default, MAU regularly checks for updates and automatically downloads and installs them. Deploy managed preferences to configure update behavior for the macOS devices in your organization.

Warning

Each version of Defender for Endpoint on macOS is set to expire automatically after six months. While expired versions continue to receive security intelligence updates, we recommend that you install the latest version to get all available improvements and enhancements. To check when the installed product version expires, use the `product_expiration` health field:

```bash
mdatp health --field product_expiration
```

## Use msupdate

MAU includes the `msupdate` command-line tool, which gives IT administrators more precise control over when updates start. For complete command syntax and requirements, see [Update Microsoft applications for Mac by using msupdate](/en-us/deployoffice/mac/update-office-for-mac-using-msupdate).

The MAU application identifier for Defender for Endpoint is `WDAV00`. Run the following commands in Terminal to download and install the latest available Defender for Endpoint update:

```bash
cd /Library/Application\ Support/Microsoft/MAU2.0/Microsoft\ AutoUpdate.app/Contents/MacOS
./msupdate --install --apps wdav00
```

## Set preferences for Microsoft AutoUpdate

Deploy MAU preferences in a device-level configuration profile through your mobile device management (MDM) solution. The following settings control the update channel and the update options available to local users.

### Set the channel name

For the complete preference definition, see [`ChannelName`](/en-us/deployoffice/mac/mau-preferences#channelname).

The channel determines the type and frequency of updates offered through MAU. Devices assigned to `Beta` receive new Defender for Endpoint features before devices assigned to `Preview` and `Current`.

The `Current` channel contains the most stable product version and is the default. If `ChannelName` is missing or invalid, MAU uses `Current`.

Important

Before Microsoft AutoUpdate version 4.29 (November 2020), the channels used different names:

- `Beta` was named `InsiderFast`.
- `Preview` was named `External`.
- `Current` was named `Production`.

Tip

Assign a small set of test devices to `Beta` or `Preview` to evaluate new features and provide early feedback before broader deployment.

- **Domain**: `com.microsoft.autoupdate2`
- **Key**: `ChannelName`
- **Data type**: String
- **Supported Defender for Endpoint values**:
    - `Beta`: Receives the latest features in development. Use this channel only for testing and reporting issues.
    - `Preview`: Receives a preview of official releases.
    - `Current`: Receives official releases and is the default channel.

Warning

The global `ChannelName` setting changes the channel for all applications updated through MAU. To change only the Defender for Endpoint channel, replace `[channel-name]` with `Beta`, `Preview`, or `Current`, and then run the following command:

```bash
defaults write com.microsoft.autoupdate2 Applications -dict-add "/Applications/Microsoft Defender.app" " { 'Application ID' = 'WDAV00' ; 'App Domain' = 'com.microsoft.wdav' ; ChannelName = '[channel-name]' ; }"
```

Administrators can also deploy the per-app setting by using the Defender-specific configuration profile in Deploy example configuration profiles.

### Control manual update checks

For the complete preference definition, see [`EnableCheckForUpdatesButton`](/en-us/deployoffice/mac/mau-preferences#enablecheckforupdatesbutton).

The `EnableCheckForUpdatesButton` preference controls whether local users can start an update check or select **Update All** in the MAU user interface.

- **Domain**: `com.microsoft.autoupdate2`
- **Key**: `EnableCheckForUpdatesButton`
- **Data type**: Boolean
- **Possible values**:
    - `true` (default): Enables manual update controls.
    - `false`: Disables manual update controls.

### Control update channel selection

For the complete preference definition, see [`DisableInsiderCheckbox`](/en-us/deployoffice/mac/mau-preferences#disableinsidercheckbox).

The historical `DisableInsiderCheckbox` preference controls whether local users can select the `Beta` or `Preview` channel in the MAU user interface.

- **Domain**: `com.microsoft.autoupdate2`
- **Key**: `DisableInsiderCheckbox`
- **Data type**: Boolean
- **Possible values**:
    - `false` (default): Allows users to select an update channel.
    - `true`: Disables update channel selection.

## Deploy example configuration profiles

Use one of the following example profiles based on your MDM solution and whether you want to configure a global MAU channel or a Defender-specific channel. The global examples:

- Assign the device to the `Current` channel.
- Automatically download and install updates.
- Enable manual update controls in the MAU user interface.
- Allow users to select an update channel.

Warning

Review and tailor these example settings before you deploy a profile in production.

### Jamf Pro

> 
> Jamf Pro is a separate third-party product that isn't part of Defender for Endpoint and isn't included with Defender for Endpoint subscriptions. To use Jamf Pro, your organization needs a separate Jamf Pro subscription. For product and subscription information, see [Jamf Pro](https://www.jamf.com/products/jamf-pro/). If your organization doesn't use Jamf Pro, use another configuration method in this article, if available.

For Jamf Pro, use the following property list to configure global MAU settings in the `com.microsoft.autoupdate2` preference domain:

```XML
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>ChannelName</key>
    <string>Current</string>
    <key>HowToCheck</key>
    <string>AutomaticDownload</string>
    <key>EnableCheckForUpdatesButton</key>
    <true/>
    <key>DisableInsiderCheckbox</key>
    <false/>
</dict>
</plist>
```

### Intune

> 
> Microsoft Intune is the recommended tool for configuring and distributing Defender for Endpoint features to devices. However, Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have Intune, you can use any of the other methods in this article. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

For Intune, use the following complete configuration profile to configure global MAU settings:

```XML
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1">
    <dict>
        <key>PayloadUUID</key>
        <string>B762FF60-6ACB-4A72-9E72-459D00C936F3</string>
        <key>PayloadType</key>
        <string>Configuration</string>
        <key>PayloadOrganization</key>
        <string>Microsoft</string>
        <key>PayloadIdentifier</key>
        <string>com.microsoft.autoupdate2</string>
        <key>PayloadDisplayName</key>
        <string>Microsoft AutoUpdate settings</string>
        <key>PayloadDescription</key>
        <string>Microsoft AutoUpdate configuration settings</string>
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
            <string>5A6F350A-CC2C-440B-A074-68E3F34EBAE9</string>
            <key>PayloadType</key>
            <string>com.microsoft.autoupdate2</string>
            <key>PayloadOrganization</key>
            <string>Microsoft</string>
            <key>PayloadIdentifier</key>
            <string>com.microsoft.autoupdate2</string>
            <key>PayloadDisplayName</key>
            <string>Microsoft AutoUpdate configuration settings</string>
            <key>PayloadDescription</key>
            <string/>
            <key>PayloadVersion</key>
            <integer>1</integer>
            <key>PayloadEnabled</key>
            <true/>
            <key>ChannelName</key>
            <string>Current</string>
            <key>HowToCheck</key>
            <string>AutomaticDownload</string>
            <key>EnableCheckForUpdatesButton</key>
            <true/>
            <key>DisableInsiderCheckbox</key>
            <false/>
            </dict>
        </array>
    </dict>
</plist>
```

### Configure a Defender-specific channel with Intune

To leave other Microsoft applications on their existing channels and assign Defender for Endpoint to `Current`, use the following profile instead of the preceding global profile. To configure a global channel and a Defender-specific override, combine both settings in one managed profile.

```XML
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1">
    <dict>
        <key>PayloadUUID</key>
        <string>B762FF60-6ACB-4A72-9E72-459D00C936F3</string>
        <key>PayloadType</key>
        <string>Configuration</string>
        <key>PayloadOrganization</key>
        <string>Microsoft</string>
        <key>PayloadIdentifier</key>
        <string>com.microsoft.autoupdate2</string>
        <key>PayloadDisplayName</key>
        <string>Microsoft AutoUpdate settings</string>
        <key>PayloadDescription</key>
        <string>Microsoft AutoUpdate configuration settings</string>
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
            <string>5A6F350A-CC2C-440B-A074-68E3F34EBAE9</string>
            <key>PayloadType</key>
            <string>com.microsoft.autoupdate2</string>
            <key>PayloadOrganization</key>
            <string>Microsoft</string>
            <key>PayloadIdentifier</key>
            <string>com.microsoft.autoupdate2</string>
            <key>PayloadDisplayName</key>
            <string>Microsoft AutoUpdate configuration settings</string>
            <key>PayloadDescription</key>
            <string/>
            <key>PayloadVersion</key>
            <integer>1</integer>
            <key>PayloadEnabled</key>
            <true/>
            <key>Applications</key>
            <dict>
                <key>/Applications/Microsoft Defender.app</key>
                <dict>
                    <key>App Domain</key>
                    <string>com.microsoft.wdav</string>
                    <key>Application ID</key>
                    <string>WDAV00</string>
                    <key>ChannelName</key>
                    <string>Current</string>
                </dict>
            </dict>
            </dict>
        </array>
    </dict>
</plist>
```

Deploy the appropriate profile by using the maintained procedure for your management method:

- **Jamf Pro**: Follow the instructions to [deploy a custom computer configuration profile](https://learn.jamf.com/r/technical-articles/Deploying_Custom_Computer_Configuration_Profiles_Using_the_Application_and_Custom_Settings_Payload). Upload the Jamf Pro property list and set **Preference Domain** to `com.microsoft.autoupdate2`.
- **Microsoft Intune**: Follow [Step 8: Microsoft AutoUpdate](mac-install-with-intune#step-8-microsoft-autoupdate) to deploy the selected complete configuration profile as a device-channel custom profile.

To assign a different channel to Defender for Endpoint, add the `ChannelName` key under the Defender entry in the `Applications` dictionary. The supported Defender for Endpoint values are `Beta`, `Preview`, and `Current`.

For complete preference details, see [Configure preferences for Microsoft AutoUpdate](/en-us/deployoffice/mac/mau-preferences#howtocheck).