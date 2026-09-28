---
layout: Conceptual
title: Configure Microsoft Defender for Endpoint on macOS with Jamf Pro - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/mac-jamfpro-policies
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use Jamf Pro to deploy Microsoft Defender for Endpoint on macOS and configure onboarding, security settings, permissions, and updates.
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
ms.date: 2026-09-17T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: d0a5c0da-765c-aac8-97ec-7d54ee8bc24f
document_version_independent_id: d0a5c0da-765c-aac8-97ec-7d54ee8bc24f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/mac-jamfpro-policies.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mac-jamfpro-policies
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/mac-jamfpro-policies.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: a1f67ead-5751-141a-7f72-3f0efe1432af
---

# Configure Microsoft Defender for Endpoint on macOS with Jamf Pro - Microsoft Defender for Endpoint | Microsoft Learn

You can use Jamf Pro, a third-party mobile device management (MDM) platform for Apple devices, to deploy and manage Microsoft Defender for Endpoint on organization-owned macOS devices.

Jamf Pro is a separate product that isn't part of Defender for Endpoint and isn't included with Defender for Endpoint subscriptions. To use these procedures, your organization needs a separate Jamf Pro subscription. For product and subscription information, see [Jamf Pro](https://www.jamf.com/products/jamf-pro/). If your organization doesn't use Jamf Pro, you can [deploy Defender for Endpoint with Microsoft Intune](mac-install-with-intune) or [use another MDM solution](mac-install-with-other-mdm).

The procedures configure onboarding, antivirus and endpoint detection and response (EDR) settings, notifications, Microsoft AutoUpdate, Full Disk Access, system extensions, network extensions, background services, Bluetooth permissions, and package deployment.

Important

Microsoft provides information about Jamf Pro to support integration scenarios but doesn't provide troubleshooting support for this third-party product. For issues specific to Jamf Pro, contact Jamf support.

## Prerequisites

Before you configure Defender for Endpoint policies in Jamf Pro, make sure you meet the following requirements:

- Review the [Defender for Endpoint on macOS prerequisites](microsoft-defender-endpoint-mac-prerequisites), including licensing, supported macOS versions, and network connectivity.
- Verify that your organization has a Jamf Pro subscription and that you have permission to create configuration profiles, policies, packages, scripts, and smart computer groups.
- [Set up the macOS device groups in Jamf Pro](mac-jamfpro-device-groups).

## Step 1: Get the Defender for Endpoint packages

Important

You must have an appropriate role assigned to view, manage, and onboard devices. For more information, see [Manage access to Microsoft Defender XDR with Microsoft Entra global roles](/en-us/defender-xdr/m365d-permissions#manage-access-to-microsoft-defender-xdr-with-microsoft-entra-global-roles).

To download the onboarding and installation packages, follow these steps:

1. On the **Onboarding** page in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/endpoints/onboarding, configure the following settings:

    - **Step 1: Select an operating system to start deployment**: Select **macOS**.
    - **Connectivity type**: Select **Streamlined**. Before continuing, verify that the devices and network meet the [streamlined connectivity prerequisites](configure-device-connectivity#prerequisites).
    - **Deployment method**: Select **Mobile Device Management / Microsoft Intune**.
2. Select **Download onboarding package**, and save `GatewayWindowsDefenderATPOnboardingPackage.zip` to a location that's easy to find.
3. Extract the contents of `GatewayWindowsDefenderATPOnboardingPackage.zip`. In the extracted package, open the `jamf` folder, which contains `WindowsDefenderATPOnboarding.plist`.
4. Select **Download installation package**, and save `wdav.pkg` for use in Step 12: Deploy Microsoft Defender for Endpoint on macOS.

## Step 2: Create a configuration profile in Jamf Pro using the onboarding package

Create and assign a Jamf Pro configuration profile that contains the Defender for Endpoint onboarding information. For current Jamf Pro instructions, see [Deploying Custom Computer Configuration Profiles Using the Application & Custom Settings Payload](https://learn.jamf.com/r/technical-articles/Deploying_Custom_Computer_Configuration_Profiles_Using_the_Application_and_Custom_Settings_Payload).

Use these Defender-specific values:

- **Configuration file**: In the extracted onboarding package, use `jamf\WindowsDefenderATPOnboarding.plist`.
- **Name**: Enter a descriptive name, such as `MDE onboarding for macOS`.
- **Description**: Enter a description, such as `MDE EDR onboarding for macOS`.
- **Category**: Select an organization-defined category, or leave this value set to `None`.
- **Distribution Method**: Select `Install Automatically`.
- **Level**: Select `Computer Level`.
- **Payload**: Select **Application & Custom Settings**, and upload the property list.
- **Preference Domain**: Enter `com.microsoft.wdav.atp`.
- **Scope**: Select the computer group that contains the target macOS devices.

## Step 3: Configure Microsoft Defender for Endpoint settings

Configure antivirus and EDR settings in either the Microsoft Defender portal or Jamf Pro.

Important

Defender for Endpoint security settings management policies take precedence over conflicting settings configured in Jamf Pro or another third-party MDM solution.

### Configure policies in the Microsoft Defender portal

Before you begin, complete the setup described in [Configure Microsoft Defender for Endpoint in Intune](/en-us/intune/device-security/microsoft-defender/configure-integration).

Use the Microsoft Defender portal to create and assign macOS security policies to your devices.

For detailed instructions, see [Create an endpoint security policy](endpoint-security-policies-configure#create-an-endpoint-security-policy) (link opens in a new tab).

When you create a policy on the **macOS policies** tab of the **Endpoint security policies** page in the Defender portal at https://security.microsoft.com/policy-inventory?osPlatform=Mac, use these specific settings:

- **Select platform**: Select **macOS**.
- **Select template**: Select one of the following values, depending on the settings you want to configure:
    - **Microsoft Defender Antivirus**
    - **Endpoint detection and response**

In the policy creation wizard, use these settings:

- **Configuration settings** tab: Configure the settings you want to manage with this profile.
- **Assignments** tab: Assignment group limitations apply to devices managed through Defender for Endpoint security settings management. For details, see the [Assignments step](endpoint-security-policies-configure#create-an-endpoint-security-policy).

For more information about managing security settings, see the following articles:

- [Manage Microsoft Defender for Endpoint on devices with Microsoft Intune](/en-us/intune/device-security/microsoft-defender/security-settings-management)
- [Manage security settings for Windows, macOS, and Linux natively in Defender for Endpoint](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/manage-security-settings-for-windows-macos-and-linux-natively-in/ba-p/3870617)

### Configure policies in Jamf Pro

Use the Jamf Pro graphical user interface (GUI) to configure individual Defender for Endpoint settings. Alternatively, use the legacy method to create a property list (`.plist`) file in a text editor and upload the file to Jamf Pro.

- Use the exact value `com.microsoft.wdav` as the **Preference Domain**. Defender for Endpoint uses this domain and `com.microsoft.wdav.ext` to load managed settings.
- Use `com.microsoft.wdav.ext` only when you use the GUI method and need to configure a setting that isn't yet available in the schema.

### Configure Defender settings using the Jamf Pro GUI

Use this method to import Defender's JSON schema into Jamf Pro and configure settings through the GUI.

1. Download the Defender for Endpoint `schema.json` file from the [Microsoft Defender for Endpoint GitHub repository](https://github.com/microsoft/mdatp-xplat/tree/master/macos/schema). Jamf Pro uses the schema to populate the available configuration settings in the GUI:

    ```bash
    curl -o ~/Documents/schema.json https://raw.githubusercontent.com/microsoft/mdatp-xplat/master/macos/schema/schema.json
    ```
2. Follow the Jamf instructions to [deploy a custom computer configuration profile](https://learn.jamf.com/r/technical-articles/Deploying_Custom_Computer_Configuration_Profiles_Using_the_Application_and_Custom_Settings_Payload). Use these Defender-specific values:

    - **Name**: Enter a descriptive name, such as `MDATP MDAV configuration settings`.
    - **Category**: Select an organization-defined category, or leave this value set to `None`.
    - **Level**: Select `Computer Level`.
    - **Distribution Method**: Select `Install Automatically`.
    - **Payload**: Select **Application & Custom Settings** &gt; **External Applications**.
    - **Source**: Select **Custom Schema**, and upload `schema.json`.
    - **Preference Domain**: Enter `com.microsoft.wdav`.
    - **Preference Domain Properties**: Select the settings you want Jamf Pro to manage. Settings you don't select remain available for users to configure locally.
    - **Scope**: Select the computer group that contains the target macOS devices.

Microsoft Defender for Endpoint adds new settings over time. New Defender for Endpoint settings are added to the schema, and a new version is published to GitHub. To get updates, download an updated schema and edit your existing configuration profile. On the **Application & Custom Settings** tab, select **Edit schema**.

### Configure Defender settings using the legacy method

Use this legacy method to manually create a configuration plist in a text editor and upload it to Jamf Pro.

Important

Upload the Jamf Pro property list, not the Intune property list. Jamf Pro displays an error if you upload the Intune file.

1. Include the following Defender for Endpoint settings in the property list:

    - `enableRealTimeProtection`
    - `passiveMode` (This setting is off by default. If you plan to run non-Microsoft antivirus software on the Mac, set it to `true`.)
    - `exclusions`
    - `excludedPath`
    - `excludedFileExtension`
    - `excludedFileName`
    - `exclusionsMergePolicy`
    - `allowedThreats` (The sample includes EICAR. Remove the EICAR entry for a proof of concept, especially if you plan to use EICAR to verify protection.)
    - `disallowedThreatActions`
    - `potentially_unwanted_application`
    - `archive_bomb`
    - `cloudService`
    - `automaticSampleSubmission`
    - `tags`
    - `hideStatusMenuIcon`

    For more information, see [Property list for Jamf full configuration profile](mac-preferences#property-list-for-jamf-full-configuration-profile).

    ```XML
      <?xml version="1.0" encoding="UTF-8"?>
      <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
      <plist version="1.0">
      <dict>
          <key>antivirusEngine</key>
          <dict>
              <key>enableRealTimeProtection</key>
              <true/>
              <key>passiveMode</key>
              <false/>
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
          <key>userInterface</key>
          <dict>
              <key>hideStatusMenuIcon</key>
              <false/>
          </dict>
      </dict>
      </plist>
    ```
2. Save the file as `MDATP_MDAV_configuration_settings.plist`.
3. Follow the Jamf instructions to [deploy a custom computer configuration profile](https://learn.jamf.com/r/technical-articles/Deploying_Custom_Computer_Configuration_Profiles_Using_the_Application_and_Custom_Settings_Payload). Use these Defender-specific values:

    - **Name**: Enter a descriptive name, such as `MDATP MDAV configuration settings`.
    - **Category**: Select an organization-defined category, or leave this value set to `None`.
    - **Distribution Method**: Select `Install Automatically`.
    - **Level**: Select `Computer Level`.
    - **Payload**: Select **Application & Custom Settings**, and upload `MDATP_MDAV_configuration_settings.plist`.
    - **Preference Domain**: Enter `com.microsoft.wdav`.
    - **Scope**: Select the computer group that contains the target macOS devices.

## Step 4: Configure notification settings

Note

Use a [supported version of macOS](microsoft-defender-endpoint-mac-prerequisites#system-requirements). Defender for Endpoint uses macOS notification settings introduced in macOS 11 (Big Sur).

Create a Jamf Pro configuration profile that allows notifications from Defender for Endpoint and Microsoft AutoUpdate.

1. Download [notif.mobileconfig](https://raw.githubusercontent.com/microsoft/mdatp-xplat/master/macos/mobileconfig/profiles/notif.mobileconfig).
2. Follow the Jamf instructions to [upload a configuration profile](https://learn.jamf.com/r/jamf-pro-documentation-current/Uploading_a_Configuration_Profile_macOS).
3. Scope the profile to the computer group that contains the target macOS devices.

The profile enables banners, badges, sounds, and Notification Center notifications. It hides notifications on the lock screen and disables critical alerts for these bundle IDs:

- `com.microsoft.wdav.tray`
- `com.microsoft.autoupdate2`

## Step 5: Configure Microsoft AutoUpdate (MAU)

Microsoft AutoUpdate (MAU) keeps Microsoft applications up to date on macOS, including Microsoft Defender for Endpoint. Configure the following settings to manage how updates are delivered to your devices.

1. Use the following Microsoft Defender for Endpoint configuration settings:

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
     <key>SendAllTelemetryEnabled</key>
     <true/>
    </dict>
    </plist>
    ```
2. Save the property list as `MDATP_MDAV_MAU_settings.plist`.
3. Follow the Jamf instructions to [deploy a custom computer configuration profile](https://learn.jamf.com/r/technical-articles/Deploying_Custom_Computer_Configuration_Profiles_Using_the_Application_and_Custom_Settings_Payload). Use these Defender-specific values:

    - **Name**: Enter a descriptive name, such as `MDATP MDAV MAU settings`.
    - **Category**: Select an organization-defined category, or leave this value set to `None`.
    - **Distribution Method**: Select `Install Automatically`.
    - **Level**: Select `Computer Level`.
    - **Payload**: Select **Application & Custom Settings**, and upload `MDATP_MDAV_MAU_settings.plist`.
    - **Preference Domain**: Enter `com.microsoft.autoupdate2`.
    - **Scope**: Select the computer group that contains the target macOS devices.

For descriptions of the available settings and supported values, see [Microsoft AutoUpdate preferences](/en-us/microsoft-365-apps/mac/mau-preferences).

## Step 6: Grant Full Disk Access to Microsoft Defender for Endpoint

Create a Jamf Pro configuration profile that grants Full Disk Access to Defender for Endpoint.

1. Download [fulldisk.mobileconfig](https://github.com/microsoft/mdatp-xplat/blob/master/macos/mobileconfig/profiles/fulldisk.mobileconfig).
2. Follow the Jamf instructions to [upload a configuration profile](https://learn.jamf.com/r/jamf-pro-documentation-current/Uploading_a_Configuration_Profile_macOS).
3. Scope the profile to the computer group that contains the target macOS devices.

The profile grants `SystemPolicyAllFiles` access to these bundle IDs:

- `com.microsoft.wdav`
- `com.microsoft.wdav.epsext`
- `com.microsoft.dlp.daemon`

Note

Full Disk Access granted through an Apple MDM configuration profile doesn't appear in the **Full Disk Access** list in macOS System Settings.

## Step 7: Approve system extensions for Microsoft Defender for Endpoint

Create a Jamf Pro configuration profile that approves the Defender for Endpoint system extensions.

1. Download [sysext.mobileconfig](https://github.com/microsoft/mdatp-xplat/blob/master/macos/mobileconfig/profiles/sysext.mobileconfig).
2. Follow the Jamf instructions to [upload a configuration profile](https://learn.jamf.com/r/jamf-pro-documentation-current/Uploading_a_Configuration_Profile_macOS).
3. Scope the profile to the computer group that contains the target macOS devices.

The profile uses Microsoft Team ID `UBF8T346G9` to approve these system extensions:

- `com.microsoft.wdav.epsext`
- `com.microsoft.wdav.netext`

## Step 8: Configure the network extension

The Defender for Endpoint network extension inspects network traffic to support Network Protection, web content filtering, and custom network indicators.

Note

Use a [supported version of macOS](microsoft-defender-endpoint-mac-prerequisites#system-requirements). Defender for Endpoint uses the system extension framework introduced in macOS 11 (Big Sur).

1. Download [netfilter.mobileconfig](https://github.com/microsoft/mdatp-xplat/blob/master/macos/mobileconfig/profiles/netfilter.mobileconfig).
2. Follow the Jamf instructions to [upload a configuration profile](https://learn.jamf.com/r/jamf-pro-documentation-current/Uploading_a_Configuration_Profile_macOS).
3. Scope the profile to the computer group that contains the target macOS devices.

The profile configures these Defender-specific values:

- **Filter name**: `Microsoft Defender Content Filter`
- **Identifier**: `com.microsoft.wdav`
- **Filter order**: `Inspector`
- **Socket filter**: `com.microsoft.wdav.netext`
- **Microsoft Team ID**: `UBF8T346G9`

## Step 9: Configure background services

Important

macOS 13 (Ventura) introduced privacy controls for apps that run in the background. Defender for Endpoint requires its daemon processes to run in the background.

This configuration profile grants the required background-service permissions. If you configured Defender for Endpoint through Jamf Pro before macOS 13, update the deployment with this profile.

Download [background_services.mobileconfig](https://raw.githubusercontent.com/microsoft/mdatp-xplat/master/macos/mobileconfig/profiles/background_services.mobileconfig) from the [Microsoft Defender for Endpoint macOS mobileconfig profiles repository](https://github.com/microsoft/mdatp-xplat/tree/master/macos/mobileconfig/profiles).

Follow the Jamf instructions to [upload a configuration profile](https://learn.jamf.com/r/jamf-pro-documentation-current/Uploading_a_Configuration_Profile_macOS), and scope the profile to the computer group that contains the target macOS devices.

## Step 10: Grant Bluetooth permissions

Important

macOS 14 (Sonoma) introduced a requirement for explicit consent before apps can access Bluetooth. Defender for Endpoint requires this access only when you configure Bluetooth policies for device control.

Download [bluetooth.mobileconfig](https://github.com/microsoft/mdatp-xplat/blob/master/macos/mobileconfig/profiles/bluetooth.mobileconfig) from the [Microsoft Defender for Endpoint macOS mobileconfig profiles repository](https://github.com/microsoft/mdatp-xplat/tree/master/macos/mobileconfig/profiles).

Important

Confirm whether your Jamf Pro version supports the Bluetooth payload before uploading the profile. If Jamf Pro removes the unsupported payload, sign the downloaded configuration profile first so Jamf Pro treats it as sealed and doesn't modify it.

You need at least one signing certificate in your macOS keychain. A self-signed certificate is sufficient. List the available code-signing identities to find the certificate name:

```bash
> /usr/bin/security find-identity -p codesigning -v

  1) 70E46A47F552EA8D58521DAC1E7F5144BA3012BC "DevCert"
  2) 67FC43F3FAB77662BB7688C114585BAA37CA8175 "Mac Developer: John Doe (1234XX234)"
  3) E142DFD879E5EB60FA249FB5B24CEAE3B370394A "Apple Development: Jane Doe 7XX7778888)"
  4) 21DE31645BBF1D9F5C46E82E87A6968111E41C75 "Apple Development: me@example.com (8745XX123)"
     4 valid identities found
```

Choose one of the listed signing identities, and provide the quoted certificate name as the `-N` parameter. The command signs the Bluetooth configuration profile so Jamf Pro doesn't modify its payload:

```bash
/usr/bin/security cms -S -N "DevCert" -i bluetooth.mobileconfig -o bluetooth-signed.mobileconfig
```

Follow the Jamf instructions to [upload a configuration profile](https://learn.jamf.com/r/jamf-pro-documentation-current/Uploading_a_Configuration_Profile_macOS). Upload `bluetooth-signed.mobileconfig`, and scope the profile to the computer group that contains the target macOS devices.

Note

Bluetooth access granted through an Apple MDM configuration profile doesn't appear in the **Bluetooth** list in macOS System Settings.

## Step 11: Schedule scans with Microsoft Defender for Endpoint on macOS

To configure recurring quick or full scans, see [Schedule scans with Microsoft Defender for Endpoint on macOS](mac-schedule-scan).

## Step 12: Deploy Microsoft Defender for Endpoint on macOS

Upload the Microsoft Defender for Endpoint package to Jamf Pro and create a deployment policy to distribute it to your macOS devices.

For current Jamf Pro instructions, see [Package Deployment](https://learn.jamf.com/r/jamf-pro-documentation-current/Package_Deployment). Use these Defender-specific values:

- **Package**: Upload the `wdav.pkg` file that you downloaded in Step 1.
- **Display Name**: Enter a descriptive name, such as `Microsoft Defender for Endpoint`.
- **Manifest File**: Leave this value blank. Defender for Endpoint doesn't require a manifest file.
- **Options** and **Limitations**: Defender for Endpoint doesn't require specific values. Configure these settings based on your organization's package deployment requirements.
- **Policy trigger**: Select **Recurring Check-in**.
- **Packages payload**: Add the Defender for Endpoint package, and configure it to install.
- **Scope**: Select the smart computer group described in Create a smart computer group for devices with Defender profiles.
- **Self Service**: Optionally make the policy available in Self Service for on-demand installation.

### Create a smart computer group for devices with Defender profiles

Install the required configuration profiles on enrolled devices before you install the Defender for Endpoint package. Jamf Pro typically pushes configuration profiles immediately, but policies run when the device checks in. Profile deployment might be delayed, for example, when a device is locked.

To enforce the correct deployment order, create a smart computer group for devices that received a Defender for Endpoint configuration profile. Scope the package policy to that group so Jamf Pro installs Defender for Endpoint only after the profile is present.

For current Jamf Pro instructions, see [Creating a Smart Group](https://learn.jamf.com/r/jamf-pro-documentation-current/Creating_a_Smart_Group). Use these Defender-specific settings:

- Add a **Profile Name** criterion for each required Defender for Endpoint configuration profile.
- Combine the profile criteria with `AND` so the group includes only devices that received all required profiles.
- Scope the Defender for Endpoint package policy to this smart computer group.

## Verify configuration profile scope for all Defender profiles

Jamf Pro requires a scope for each configuration profile. Make sure every device that receives the Defender for Endpoint package also receives all applicable profiles:

- Onboarding (Step 2)
- Defender for Endpoint settings (Step 3)
- Notifications (Step 4)
- Microsoft AutoUpdate (Step 5)
- Full Disk Access (Step 6)
- System extensions (Step 7)
- Network extension (Step 8)
- Background services (Step 9)
- Bluetooth permissions (Step 10)

Important

Jamf Pro smart computer groups dynamically include devices that match specified criteria. You can use these groups to deploy configuration profiles and policies.

Don't use the presence of Defender for Endpoint as a smart computer group criterion. This dependency can cause deployment problems that are difficult to diagnose.

Defender for Endpoint requires all applicable configuration profiles when it's installed.

If profile deployment depends on Defender for Endpoint already being installed, the profiles are delayed. The device might become unhealthy, or users might be prompted to approve permissions that the profiles would otherwise approve automatically. Deploy the Defender for Endpoint package only after all required configuration profiles are in place.