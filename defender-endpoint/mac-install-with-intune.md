---
layout: Conceptual
title: Deploy Microsoft Defender for Endpoint on macOS with Intune - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/mac-install-with-intune
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to deploy, configure, onboard, and verify Microsoft Defender for Endpoint on macOS devices by using Microsoft Intune.
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
document_id: 73237dd8-0601-1c01-f33f-70495fe88584
document_version_independent_id: 73237dd8-0601-1c01-f33f-70495fe88584
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/mac-install-with-intune.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mac-install-with-intune
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/mac-install-with-intune.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/a72e95ff-4b4f-4cc1-90c6-7dcba67ff05f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/24dc3ccd-591a-4415-a1fe-8759afafcb12
platformId: 08bde703-9ea4-f848-ee55-feb4b0bd0be1
---

# Deploy Microsoft Defender for Endpoint on macOS with Intune - Microsoft Defender for Endpoint | Microsoft Learn

Use Microsoft Intune to deploy Microsoft Defender for Endpoint to managed macOS devices. Create the required configuration profiles, deploy the app and onboarding package, and verify the deployment. Before you begin, review the prerequisites and system requirements.

The procedures in this article require Microsoft Intune. Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. You need a subscription that includes Intune, or you can buy it separately. For licensing information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses). To compare this method with [Jamf Pro](mac-install-with-jamf), [another mobile device management solution](mac-install-with-other-mdm), or [manual deployment](mac-install-manually), see [Deploy Defender for Endpoint on macOS](microsoft-defender-endpoint-mac#deploy-defender-for-endpoint-on-macos).

## Prerequisites and system requirements

Before you start, review the [Defender for Endpoint on macOS prerequisites](microsoft-defender-endpoint-mac-prerequisites), including the product, administrator, system, permission, and network requirements. For product capabilities and shared deployment verification, see [Microsoft Defender for Endpoint on macOS](microsoft-defender-endpoint-mac).

Important

If you want to run multiple security solutions side by side, see [Considerations for performance, configuration, and support](/en-us/defender-endpoint/mde-side-by-side).

You might have already configured mutual security exclusions for devices onboarded to Microsoft Defender for Endpoint. If you still need to set mutual exclusions to avoid conflicts, see [Add Microsoft Defender for Endpoint to the exclusion list for your existing solution](/en-us/defender-endpoint/switch-to-mde-phase-2#step-2-add-microsoft-defender-for-endpoint-to-the-exclusion-list-for-your-existing-solution).

## Deployment overview

The following table summarizes the profiles and packages used to deploy Defender for Endpoint on macOS with Intune.

| Step | Sample file name | Bundle identifier |
| --- | --- | --- |
| Approve system extensions | Not applicable | `com.microsoft.wdav.epsext` and `com.microsoft.wdav.netext` |
| Network extension policy | `netfilter.mobileconfig` | `com.microsoft.wdav.netext` |
| Full Disk Access | `fulldisk.mobileconfig` | `com.microsoft.wdav`, `com.microsoft.wdav.epsext`, and `com.microsoft.dlp.daemon` |
| Defender for Endpoint preferences If you plan to run a non-Microsoft antivirus product on macOS, configure passive mode in the preferences profile. | `com.microsoft.wdav.xml` | `com.microsoft.wdav` |
| Background services | `background_services.mobileconfig` | Not applicable |
| Notifications | `notif.mobileconfig` | `com.microsoft.wdav.tray` and `com.microsoft.autoupdate2` |
| Accessibility settings | `accessibility.mobileconfig` | `com.microsoft.dlp.daemon` |
| Bluetooth permissions | `bluetooth.mobileconfig` | `com.microsoft.dlp.agent` |
| Microsoft AutoUpdate | `com.microsoft.autoupdate2.mobileconfig` | `com.microsoft.autoupdate2` |
| Onboarding package | `WindowsDefenderATPOnboarding.xml` | `com.microsoft.wdav.atp` |
| Defender for Endpoint app | Not applicable | Not applicable |

## Create system configuration profiles

Create the system configuration profiles that Microsoft Defender for Endpoint needs.

Most steps in this section use a custom macOS configuration profile. For detailed instructions, see [Add custom settings to Apple devices in Microsoft Intune](/en-us/intune/device-configuration/templates/configure-custom-settings-apple) (link opens in a new tab).

When a step tells you to create a **custom configuration profile**, on the **Policies** tab of the **Devices | Configuration** page in the Microsoft Intune admin center at [https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/configuration](https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/DevicesMenu/%7E/configuration), by selecting **Create** &gt; ![](media/defender-portal-icon-create.png)**New policy**, use these common settings:

- **Platform**: Select **macOS**.
- **Profile type**: Select **Templates**.
- **Template name**: Select **Custom**.

In the **Custom** wizard, configure the following settings:

- **Configuration settings** tab: Use the profile-specific settings described in each applicable step.
- **Assignments** tab: Assign the profile to the user or device groups that should receive it. You can also add scope tags and exclude groups from the assignment.

### Step 1: Approve system extensions

Use the Intune settings catalog to approve the required system extensions. For detailed instructions, see [Approve Microsoft Defender for Endpoint macOS extensions using the Intune settings catalog](manage-profiles-approve-sys-extensions-intune).

In the **Create profile** wizard, configure the following settings on the **Configuration settings** tab:

- **System configuration** &gt; **System extensions** &gt; **Allowed System Extensions**:
    - **Allowed System Extensions**: Add `com.microsoft.wdav.epsext` and `com.microsoft.wdav.netext`.
    - **Team identifier**: Enter `UBF8T346G9`.
- **System configuration** &gt; **System extensions** &gt; **Allowed System Extension Types**:
    - **Allowed System Extension Types**: Add `Network` and `EndpointSecurity`.
    - **Team identifier**: Enter `UBF8T346G9`.

### Step 2: Network filter

Defender for Endpoint uses the network extension for network content inspection. The network filter profile allows the extension to inspect socket traffic.

Download [netfilter.mobileconfig](https://raw.githubusercontent.com/microsoft/mdatp-xplat/master/macos/mobileconfig/profiles/netfilter.mobileconfig) from the [Defender for Endpoint macOS configuration profile repository](https://github.com/microsoft/mdatp-xplat/tree/master/macos/mobileconfig/profiles).

Important

macOS supports only one network filter `.mobileconfig` file. Adding multiple network filters can cause network connectivity issues. This limitation isn't specific to Defender for Endpoint.

Create a **custom configuration profile** by using the common settings described in Create system configuration profiles. Use these profile-specific settings:

- **Basics**tab:
    - **Name**: Enter a descriptive name, such as `macOS network filter`.
- **Configuration settings**tab:
    - **Configuration profile name**: Enter a descriptive name for the profile.
    - **Deployment channel**: Select **Device channel**.
    - **Configuration profile file**: Select the `netfilter.mobileconfig` file that you downloaded.

### Step 3: Full Disk Access

Note

macOS Catalina 10.15 and later use Transparency, Consent, and Control (TCC) to protect access to sensitive user data. Deploying the Full Disk Access profile through mobile device management (MDM) prevents local users from revoking the permissions that Defender for Endpoint needs.

This profile grants Full Disk Access to Defender for Endpoint. If you configured Defender for Endpoint through Intune without this profile, update the deployment to include it.

Download [fulldisk.mobileconfig](https://raw.githubusercontent.com/microsoft/mdatp-xplat/master/macos/mobileconfig/profiles/fulldisk.mobileconfig) from the [Defender for Endpoint macOS configuration profile repository](https://github.com/microsoft/mdatp-xplat/tree/master/macos/mobileconfig/profiles).

Create a **custom configuration profile** by using the common settings described in Create system configuration profiles. Use these profile-specific settings:

- **Basics**tab:
    - **Name**: Enter a descriptive name, such as `macOS full disk access`.
- **Configuration settings**tab:
    - **Configuration profile name**: Enter a descriptive name for the profile.
    - **Deployment channel**: Select **Device channel**.
    - **Configuration profile file**: Select the `fulldisk.mobileconfig` file that you downloaded.

Note

Full Disk Access granted through an Apple MDM configuration profile isn't shown in **System Settings** &gt; **Privacy & Security** &gt; **Full Disk Access**.

### Step 4: Background services

Caution

Starting in macOS 13 (Ventura), apps need explicit permission to run in the background. Defender for Endpoint must run background processes. This profile grants the required background service permissions. If you configured Defender for Endpoint through Intune without this profile, update the deployment to include it.

Download [background_services.mobileconfig](https://raw.githubusercontent.com/microsoft/mdatp-xplat/master/macos/mobileconfig/profiles/background_services.mobileconfig) from the [Defender for Endpoint macOS configuration profile repository](https://github.com/microsoft/mdatp-xplat/tree/master/macos/mobileconfig/profiles).

Create a **custom configuration profile** by using the common settings described in Create system configuration profiles. Use these profile-specific settings:

- **Basics**tab:
    - **Name**: Enter a descriptive name, such as `macOS background services`.
- **Configuration settings**tab:
    - **Configuration profile name**: Enter a descriptive name for the profile.
    - **Deployment channel**: Select **Device channel**.
    - **Configuration profile file**: Select the `background_services.mobileconfig` file that you downloaded.

### Step 5: Notifications

This profile allows Defender for Endpoint and Microsoft AutoUpdate to display notifications.

Download [notif.mobileconfig](https://raw.githubusercontent.com/microsoft/mdatp-xplat/master/macos/mobileconfig/profiles/notif.mobileconfig) from the [Defender for Endpoint macOS configuration profile repository](https://github.com/microsoft/mdatp-xplat/tree/master/macos/mobileconfig/profiles).

To hide notifications from users, change `ShowInNotificationCenter` from `true` to `false` for the applicable app in [notif.mobileconfig](https://raw.githubusercontent.com/microsoft/mdatp-xplat/master/macos/mobileconfig/profiles/notif.mobileconfig).

[![Screenshot of notif.mobileconfig with ShowInNotificationCenter set to true.](media/macos-notification-profile-setting.png)](media/macos-notification-profile-setting.png#lightbox)

Create a **custom configuration profile** by using the common settings described in Create system configuration profiles. Use these profile-specific settings:

- **Basics**tab:
    - **Name**: Enter a descriptive name, such as `macOS notifications consent`.
- **Configuration settings**tab:
    - **Configuration profile name**: Enter a descriptive name for the profile.
    - **Deployment channel**: Select **Device channel**.
    - **Configuration profile file**: Select the `notif.mobileconfig` file that you downloaded.

### Step 6: Accessibility settings

This profile grants Accessibility permission to the `com.microsoft.dlp.daemon` component.

Download [accessibility.mobileconfig](https://raw.githubusercontent.com/microsoft/mdatp-xplat/refs/heads/master/macos/mobileconfig/profiles/accessibility.mobileconfig) from the [Defender for Endpoint macOS configuration profile repository](https://github.com/microsoft/mdatp-xplat/tree/master/macos/mobileconfig/profiles).

Create a **custom configuration profile** by using the common settings described in Create system configuration profiles. Use these profile-specific settings:

- **Basics**tab:
    - **Name**: Enter a descriptive name, such as `macOS accessibility settings`.
- **Configuration settings**tab:
    - **Configuration profile name**: Enter a descriptive name for the profile.
    - **Deployment channel**: Select **Device channel**.
    - **Configuration profile file**: Select the `accessibility.mobileconfig` file that you downloaded.

### Step 7: Bluetooth permissions (optional)

Caution

Starting in macOS 14 (Sonoma), apps need explicit permission to access Bluetooth. Deploy this profile if you configure Bluetooth policies for Device Control.

Download [bluetooth.mobileconfig](https://raw.githubusercontent.com/microsoft/mdatp-xplat/refs/heads/master/macos/mobileconfig/profiles/bluetooth.mobileconfig) from the [GitHub repository](https://github.com/microsoft/mdatp-xplat/tree/master/macos/mobileconfig/profiles).

Create a **custom configuration profile** by using the common settings described in Create system configuration profiles. Use these profile-specific settings:

- **Basics**tab:
    - **Name**: Enter a descriptive name, such as `macOS Bluetooth consent`.
- **Configuration settings**tab:
    - **Configuration profile name**: Enter a descriptive name for the profile.
    - **Deployment channel**: Select **Device channel**.
    - **Configuration profile file**: Select the `bluetooth.mobileconfig` file that you downloaded.

Note

Bluetooth access granted through an Apple MDM configuration profile isn't shown in **System Settings** &gt; **Privacy & Security** &gt; **Bluetooth**.

### Step 8: Microsoft AutoUpdate

This profile configures Microsoft AutoUpdate to update Defender for Endpoint. Select one of the following update channels:

- `Beta`
- `Preview`
- `Current`

For more information, see [Deploy updates for Microsoft Defender for Endpoint on macOS](mac-updates).

Download [com.microsoft.autoupdate2.mobileconfig](https://raw.githubusercontent.com/microsoft/mdatp-xplat/refs/heads/master/macos/settings/microsoft_auto_update/com.microsoft.autoupdate2.mobileconfig) from the [Microsoft AutoUpdate settings repository](https://github.com/microsoft/mdatp-xplat/tree/master/macos/settings/microsoft_auto_update).

Note

The sample `com.microsoft.autoupdate2.mobileconfig` file is configured for Current Channel (Production).

Create a **custom configuration profile** by using the common settings described in Create system configuration profiles. Use these profile-specific settings:

- **Basics**tab:
    - **Name**: Enter a descriptive name, such as `macOS Microsoft AutoUpdate`.
- **Configuration settings**tab:
    - **Configuration profile name**: Enter a descriptive name for the profile.
    - **Deployment channel**: Select **Device channel**.
    - **Configuration profile file**: Select the `com.microsoft.autoupdate2.mobileconfig` file that you downloaded.

### Step 9: Microsoft Defender for Endpoint configuration settings

Configure antimalware and EDR policies by using either the Microsoft Defender portal in step 9a or the Microsoft Intune admin center in step 9b.

Note

Complete only one of the following steps: 9a or 9b.

#### 9a. Set policies in the Microsoft Defender portal

If your organization [manages endpoint security policies in the Microsoft Defender portal](endpoint-security-policies-configure), you can configure antivirus and endpoint detection and response (EDR) settings with the same endpoint security policies that Intune uses.

For detailed instructions, see [Create an endpoint security policy](endpoint-security-policies-configure#create-an-endpoint-security-policy) or [Edit an endpoint security policy](endpoint-security-policies-configure#edit-an-endpoint-security-policy) (links open in new tabs).

Before you create the policies, [configure the connection between Microsoft Defender for Endpoint and Intune](/en-us/intune/intune-service/protect/advanced-threat-protection-configure).

When you create the endpoint security **Antivirus** policy on the **macOS policies** tab of the **Endpoint security policies** page in the Defender portal at https://security.microsoft.com/policy-inventory?osPlatform=Mac, use these specific settings:

- **Select platform**: Select **macOS**.
- **Select template**: Select **Microsoft Defender Antivirus**.

Configure the antivirus settings required by your organization. Then, create another policy with the following settings:

- **Select platform**: Select **macOS**.
- **Select template**: Select **Endpoint detection and response**.

#### 9b. Set policies in Microsoft Intune

To create this profile, copy the code for the [Intune recommended profile](mac-preferences#intune-recommended-profile) (recommended) or the [Intune full profile](mac-preferences#intune-full-profile) (for advanced scenarios), and save the file as `com.microsoft.wdav.xml`.

Create a custom configuration profile by using the common settings described in Create system configuration profiles. Use these profile-specific settings:

- **Basics**tab:
    - **Name**: Enter a descriptive name, such as `macOS Microsoft Defender preferences`.
- **Configuration settings**tab:
    - **Configuration profile name**: Enter `com.microsoft.wdav`.
    - **Deployment channel**: Select **Device channel**.
    - **Configuration profile file**: Select the `com.microsoft.wdav.xml` file that you created.

Caution

Enter `com.microsoft.wdav` as the **Configuration profile name**. Defender for Endpoint doesn't recognize the preferences if you use another value.

For more information, see [Set preferences for Microsoft Defender for Endpoint on macOS](mac-preferences).

For more information about managing security settings, see:

- [Manage Microsoft Defender for Endpoint on devices with Microsoft Intune](/en-us/intune/intune-service/protect/mde-security-integration?pivots=mdssc-ga)
- [Manage security settings for Windows, macOS, and Linux natively in Defender for Endpoint](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/manage-security-settings-for-windows-macos-and-linux-natively-in/ba-p/3870617)

### Step 10: Network protection for Microsoft Defender for Endpoint on macOS (optional)

Configure network protection in the Microsoft Defender Antivirus policy or the Defender for Endpoint preferences profile that you created in step 9.

For requirements, configuration options, and verification steps, see [Network protection for macOS](network-protection-macos).

### Step 11: Device Control for Microsoft Defender for Endpoint on macOS (optional)

Device Control requires Full Disk Access for `com.microsoft.dlp.daemon` and separate Device Control settings and policies. The `fulldisk.mobileconfig` profile in step 3 includes the required Full Disk Access permission.

For requirements and configuration instructions, see [Device Control for macOS](mac-device-control-overview).

Important

Deploy the required configuration profiles before you deploy the Defender for Endpoint app and onboarding package.

### Step 12: Publish the Microsoft Defender application

Important

The Microsoft Defender app for macOS supports both Defender for Endpoint and Microsoft Purview Endpoint Data Loss Prevention. If you also plan to onboard the macOS devices to Microsoft Purview in step 18, enable device monitoring as part of the Purview onboarding process. In the Microsoft Purview portal at https://purview.microsoft.com, go to **Settings** &gt; **Device onboarding** &gt; **Devices**, and select **Enable device monitoring**.

Publish the Microsoft Defender app to devices enrolled in Intune. For detailed instructions, see [Add Microsoft Defender for Endpoint to macOS devices using Microsoft Intune](/en-us/intune/app-management/deployment/add-defender-macos) (link opens in a new tab).

On the **Apps | All apps** page in the Microsoft Intune admin center at [https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/AppsMenu/~/allApps](https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/AppsMenu/%7E/allApps), select ![](media/defender-portal-icon-create.png)**Create**. In the **Select app type** pane, under **Microsoft Defender for Endpoint**, select **macOS**.

In the **Add app** wizard, configure the following settings:

- **App information** tab: Keep the default values.
- **Assignments** tab: Assign the app to the user or device groups that should receive it.

### Step 13: Download the Microsoft Defender for Endpoint onboarding package

To download the onboarding package from the Microsoft Defender portal:

1. On the **Onboarding** page in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/endpoints/onboarding, configure the following settings:

    1. **Select operating system to start onboarding process**: Select **macOS**.
    2. **Connectivity type**: Verify **Streamlined** is selected.
    3. **Deployment method**: Select **Mobile Device Management / Microsoft Intune**.

        [![Screenshot of the Onboarding page with macOS, Streamlined, and Mobile Device Management or Microsoft Intune selected.](media/mac-install-with-intune/macos-download-onboarding-package.png)](media/mac-install-with-intune/macos-download-onboarding-package.png#lightbox)
2. Select **Download onboarding package**, and save `GatewayWindowsDefenderATPOnboardingPackage.zip`.
3. Extract the contents of the ZIP file so that you can deploy `WindowsDefenderATPOnboarding.xml` through Intune:

    ```bash
    unzip GatewayWindowsDefenderATPOnboardingPackage.zip
    ```

    ```console
    Archive:  GatewayWindowsDefenderATPOnboardingPackage.zip
    warning:  GatewayWindowsDefenderATPOnboardingPackage.zip appears to use backslashes as path separators
     inflating: intune/kext.xml
     inflating: intune/WindowsDefenderATPOnboarding.xml
     inflating: jamf/WindowsDefenderATPOnboarding.plist
    ```

### Step 14: Deploy the Microsoft Defender for Endpoint onboarding package for macOS

This profile contains license information for Microsoft Defender for Endpoint.

Create a **custom configuration profile** by using the common settings described in Create system configuration profiles. Use these profile-specific settings:

- **Basics**tab:
    - **Name**: Enter a descriptive name, such as `Microsoft Defender for Endpoint onboarding for macOS`.
- **Configuration settings**tab:
    - **Configuration profile name**: Enter a descriptive name for the profile.
    - **Deployment channel**: Select **Device channel**.
    - **Configuration profile file**: Select the `WindowsDefenderATPOnboarding.xml` file that you extracted from the onboarding package.

### Step 15: Check device and configuration status

#### Step 15a. View status

Use the policy report in the Intune admin center to view device and user check-in status:

1. On the **Devices | Configuration** page in the Intune admin center at [https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/configuration](https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/DevicesMenu/%7E/configuration), select a policy.
2. On **Device and user check-in status**, select **View report**.

#### Step 15b. Enroll a client device

Use Company Portal to enroll the macOS device:

1. Follow the steps in [Enroll your Mac with Intune Company Portal](/en-us/intune/user-help/enrollment/enroll-company-portal-macos).
2. After enrollment is complete, verify that the device is listed on the **All devices** page in the Intune admin center at [https://intune.microsoft.com/#view/Microsoft_Intune_Devices/DevicesMenu/~/allDevices](https://intune.microsoft.com/#view/Microsoft_Intune_Devices/DevicesMenu/%7E/allDevices).

#### Step 15c. Verify client device state

Verify the profiles and app on the managed device:

1. After the configuration profiles are deployed, open **System Settings** &gt; **General** &gt; **Device Management** on the macOS device.
2. Verify that the configuration profiles for your deployment are present and installed:

    - `accessibility.mobileconfig`, if deployed.
    - `background_services.mobileconfig`
    - `bluetooth.mobileconfig`, if deployed.
    - `com.microsoft.autoupdate2.mobileconfig`
    - `fulldisk.mobileconfig`
    - **Management Profile**, which is the Intune system profile.
    - `WindowsDefenderATPOnboarding.xml`, which is the Defender for Endpoint onboarding package.
    - `netfilter.mobileconfig`
    - `notif.mobileconfig`
3. Verify that the **Microsoft Defender** icon appears in the menu bar.

    [![Screenshot of the Microsoft Defender icon in the macOS menu bar.](media/mdatp-icon-bar.png)](media/mdatp-icon-bar.png#lightbox)

### Step 16: Verify antimalware detection

Run an [antivirus detection test](validate-antimalware) to verify that the device is onboarded and reporting correctly.

### Step 17: Verify EDR detection

Run an [EDR detection test](edr-detection) to verify that endpoint detection and response is working and reporting correctly.

### Step 18: Microsoft Purview Endpoint Data Loss Prevention for macOS (strongly recommended)

To onboard the device to Microsoft Purview and configure Endpoint Data Loss Prevention (DLP), see [Get started with Endpoint DLP](/en-us/purview/endpoint-dlp-getting-started).

## Troubleshooting

- **Issue**: Defender for Endpoint reports that no license was found.
- **Cause**: Device onboarding isn't complete.
- **Resolution**: Download the onboarding package as described in step 13, and deploy it as described in step 14.

## Logging installation issues

See [Logging installation issues](mac-resources#logging-installation-issues) to find the log that the installer automatically creates when an error occurs.

For information on troubleshooting procedures, see:

- [Troubleshoot system extension issues in Microsoft Defender for Endpoint on macOS](mac-support-sys-ext)
- [Troubleshoot installation issues for Microsoft Defender for Endpoint on macOS](mac-support-install)
- [Troubleshoot license issues for Microsoft Defender for Endpoint on macOS](mac-support-license)
- [Troubleshoot cloud connectivity issues for Microsoft Defender for Endpoint on macOS](troubleshoot-cloud-connect-mdemac)
- [Troubleshoot performance issues for Microsoft Defender for Endpoint on macOS](mac-support-perf)

## Uninstall Defender for Endpoint

See [Uninstall Defender for Endpoint on macOS](mac-resources#uninstalling) for instructions.