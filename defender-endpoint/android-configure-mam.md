---
layout: Conceptual
title: Configure Microsoft Defender for Endpoint on Android using MAM - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/android-configure-mam
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Configure Microsoft Defender for Endpoint risk signals and security features on enrolled or unenrolled Android devices using Intune MAM policies.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-android
ms.topic: how-to
ms.subservice: android
ms.date: 2026-09-15T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 7cbcbbc2-12d9-efa3-d7dc-e65e6a5d2a48
document_version_independent_id: 7cbcbbc2-12d9-efa3-d7dc-e65e6a5d2a48
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/android-configure-mam.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: android-configure-mam
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/android-configure-mam.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/a72e95ff-4b4f-4cc1-90c6-7dcba67ff05f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/24dc3ccd-591a-4415-a1fe-8759afafcb12
platformId: 39decf8d-8d50-a369-bd2e-0efaeb2c5efc
---

# Configure Microsoft Defender for Endpoint on Android using MAM - Microsoft Defender for Endpoint | Microsoft Learn

Microsoft Defender for Endpoint on Android supports Microsoft Intune mobile application management (MAM) on devices that are enrolled or aren't enrolled in Intune mobile device management (MDM). Organizations that use another enterprise mobility management solution can also use Intune MAM to protect organizational data in managed apps.

Intune app protection policies use Defender for Endpoint device risk signals to apply conditional launch actions to managed apps. App configuration policies control Defender features such as web protection, network protection, privacy, file scanning, optional permissions, sign-out controls, and device tags.

This article describes the administrator and end-user prerequisites, the Defender settings to use in Intune policies, and the end-user onboarding experience.

Microsoft Intune is the recommended tool for configuring and distributing Defender for Endpoint features to devices. However, Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

Defender for Endpoint on Android supports the following MAM configurations:

- **Intune MDM with MAM**: Intune manages the device and applies app protection policies to managed apps.
- **MAM without device enrollment**: Intune applies [app protection policies](/en-us/intune/intune-service/apps/app-protection-policy) to managed apps on devices that aren't enrolled in Intune. This configuration, also known as MAM-WE, can protect apps on devices enrolled with a third-party enterprise mobility management provider.

Use the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) to manage apps in both configurations.

## Prerequisites

### Administrator prerequisites

Before users can onboard Defender for Endpoint in MAM mode, connect Defender for Endpoint to Intune, enable the connector for Android app protection policies, and create an app protection policy.

To configure the integration, you need the following permissions:

- In Intune, the **Endpoint Security Manager** role or equivalent permissions to manage Mobile Threat Defense settings.
- In Microsoft Entra ID, the **Security Administrator** role, or permission to manage security settings in Defender for Endpoint.

#### Connect Defender for Endpoint to Intune

For the complete connection procedure, see [Connect Microsoft Defender for Endpoint to Intune](/en-us/intune/intune-service/protect/advanced-threat-protection-configure#connect-microsoft-defender-for-endpoint-to-intune).

Verify the following settings:

- On the **Other options** page in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/endpoints/integration, **Microsoft Intune Connection** is ![](media/toggle-on.png)**On**.
- On the **Endpoint security | Microsoft Defender for Endpoint** page in the Microsoft Intune admin center at [https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/~/atp](https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/%7E/atp), verify the following settings:
    - At the top of the page, **Connection status** is **Enabled**.
    - **App protection policy evaluation** section: **Connect Android devices to Defender for Endpoint** is **On**.

#### Create an app protection policy

App protection policies are rules that protect organizational data in managed apps. An app integrated with the [Intune App SDK](/en-us/intune/intune-service/developer/app-sdk) or wrapped by the [Intune App Wrapping Tool](/en-us/intune/intune-service/developer/apps-prepare-mobile-application-management) can be managed by Intune. For supported public apps, see [Microsoft Intune protected apps](/en-us/intune/intune-service/apps/apps-supported-intune-apps).

For the complete procedure to create and assign an Android app protection policy, see [App protection policies overview](/en-us/intune/intune-service/apps/app-protection-policy) (opens in a new tab in the Intune documentation).

When you create the policy, configure these Defender-specific settings:

- **Policy type**: On the **Apps | Protection** page in the Microsoft Intune admin center at [https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/AppsMenu/~/protection](https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/AppsMenu/%7E/protection), select ![](media/defender-portal-icon-create.png)**Create** &gt; **Android**.
- **Apps** tab: Add at least one managed app. You can target apps on managed devices, unmanaged devices, or devices in any management state.
- **Conditional launch** tab: In the **Device conditions** section, select **Max allowed device threat level**and then configure the following settings for it:
    - **Value**: Select the maximum threat level your organization allows (**Secured**, **Low**, **Medium**, or **High**).
    - **Action**: Select **Block access** or **Wipe data**.

Defender for Endpoint shares the device threat level with Intune. When users sign in to a targeted managed app, Intune evaluates the Defender device risk signal and applies the configured action.

Note

For unenrolled devices, deploy general app configuration settings using **Managed apps** policies instead of **Managed devices** policies.

Intune doesn't resolve conflicts when multiple app configuration policies assign different values for the same key to the same app and user. To prevent conflicts, assign only one value for each configuration key to the same app and user.

### End-user prerequisites

Before users start onboarding, ensure the following requirements are met:

- The device runs Android 10.0 or later.
- The Intune Company Portal broker app is installed.
- Users have the required licenses for the managed app.
- The managed app is installed.

## End-user onboarding

Note

Users can start onboarding by downloading or opening the Defender app. Onboarding is enabled by default when no policy explicitly changes this behavior.

When a targeted managed app detects that Defender for Endpoint isn't activated, Intune guides the user to install and activate the Defender app. For general Android installation and activation instructions, see [Install mobile threat defense app on your mobile device](/en-us/intune/user-help/security/setup-mobile-threat-defense#activation-for-android-app). After activation, the user returns to the managed app and selects **Continue** to sign in.

## Create a Managed apps app configuration policy

The Defender settings in the remaining sections use an Intune **Managed apps** app configuration policy. You can add multiple Defender configuration keys to one policy when the keys apply to the same assignments. Create separate policies when you need different settings or assignments.

For the complete procedure, see [Add an app configuration policy for managed apps](/en-us/intune/app-management/configuration/configure-managed-apps#add-an-app-configuration-policy-for-managed-apps-on-iosipados-and-android-devices) (opens in a new tab in the Intune documentation).

When you create the policy, use these specific settings:

- **Policy type**: On the **Apps | Configuration** page in the Microsoft Intune admin center at [https://intune.microsoft.com/#view/Microsoft_Intune_Apps/ConfigPoliciesMenu/~/appConfigurationPolicies](https://intune.microsoft.com/#view/Microsoft_Intune_Apps/ConfigPoliciesMenu/%7E/appConfigurationPolicies), select **Create** &gt; **Managed apps**.
- **Basics**tab: Configure the following settings:
    - **Target policy to**: Verify **Selected apps** is selected.
    - **Public apps**: Select **+ Select public apps**, find and select **Microsoft Defender Endpoint Android**, and then select **Select**.
- **Settings** tab: In the **General configuration settings**section, do the following steps:
    - Add the names and values specified in the applicable sections of this article.
    - Add `DefenderMAMConfigs` with a value of `1` to every **Managed apps** policy that configures Defender for Endpoint. The exception is a policy that disables end-user onboarding, where the value is `0`. Don't add this key to a **Managed devices** policy.

## Configure web protection

[Web protection](web-protection-overview) helps secure devices against web threats and phishing attacks. Anti-phishing and custom indicators for URLs and domains are supported. Web content filtering is currently not supported on mobile platforms.

Use the Managed apps app configuration policy procedure, and add the following configuration keys in the **General configuration settings** section on the **Settings** tab:

- **Name**: `antiphishing`
- **Value**:

    - `1`: Enable anti-phishing protection.
    - `0`: Disable anti-phishing protection.
- **Name**: `vpn`
- **Value**:

    - `1`: Enable the local virtual private network (VPN) used by web protection.
    - `0`: Disable the VPN.

To disable all web protection, set both keys to `0`. To keep anti-phishing protection enabled without the VPN, set `antiphishing` to `1` and `vpn` to `0`.

## Configure network protection

Network protection detects threats from rogue Wi-Fi networks and certificates. For an overview of the feature behavior, supported detection modes, privacy controls, and current event experience, see [Configure network protection](android-configure#configure-network-protection).

Use the Managed apps app configuration policy procedure, and add the applicable configuration keys in the **General configuration settings** section on the **Settings** tab:

- **Name**: `DefenderNetworkProtectionEnable`. Enables or disables network protection. The remaining network protection keys take effect only when this key is set to `1`.
- **Value**:

    - `0`: Disable.
    - `1`: Enable (default).
- **Name**: `DefenderAllowlistedCACertificates`. Establishes trust for root certification authority (CA) and self-signed certificates.
- **Value**: Enter a string containing certificate thumbprints, or enter no value (default).
- **Name**: `DefenderCertificateDetection`. Controls malicious certificate detection. In audit mode, events are sent to the device timeline without notifying users. When enabled, users receive notifications, and events are sent to the device timeline.
- **Value**:

    - `0`: Disable (default).
    - `1`: Audit.
    - `2`: Enable.
- **Name**: `DefenderOpenNetworkDetection`. Controls open network detection. In audit mode, events are sent to the device timeline without notifying users. When enabled, users receive notifications, and events are sent to the device timeline.
- **Value**:

    - `0`: Disable.
    - `1`: Audit.
    - `2`: Enable (default).
- **Name**: `DefenderEndUserTrustFlowEnable`. Controls the in-app experience for trusting or removing trust from unsecured networks and malicious certificates.
- **Value**:

    - `0`: Disable (default).
    - `1`: Enable.
- **Name**: `DefenderNetworkProtectionAutoRemediation`. Controls remediation alerts when users take actions such as switching to a safer Wi-Fi access point or deleting a suspicious certificate.
- **Value**:

    - `0`: Disable.
    - `1`: Enable (default).
- **Name**: `DefenderNetworkProtectionPrivacy`. Controls the collection of network protection data. When privacy is disabled, users are prompted for consent to share malicious Wi-Fi or certificate data. When privacy is enabled, users aren't prompted, and app data isn't collected.
- **Value**:

    - `0`: Disable.
    - `1`: Enable (default).

Note

For comprehensive protection against Wi-Fi threats, users should grant location permission and select **Allow all the time**. If users select **While using the app** or deny location permission, Defender for Endpoint protects against rogue certificates but can't detect threats on open or suspicious Wi-Fi networks.

## Configure privacy controls

Privacy controls can prevent Defender for Endpoint from collecting domain information in phishing reports and app details in malware reports. Network information is controlled separately by `DefenderNetworkProtectionPrivacy` in Configure network protection.

Use the Managed apps app configuration policy procedure, and add one or both of the following configuration keys in the **General configuration settings** section on the **Settings** tab:

- **Name**: `DefenderExcludeURLInReport`
- **Value**:

    - `1`: Don't collect domain names or unsafe website details in phishing reports.
    - `0`: Collect domain names and unsafe website details (default).
- **Name**: `DefenderExcludeAppInReport`
- **Value**:

    - `1`: Don't collect app names or package information in malware reports.
    - `0`: Collect app names and package information (default).

## Configure non-APK file scanning

In addition to scanning Android application packages (APK files), Defender for Endpoint on Android can scan non-APK files, such as documents, compressed archives, and scripts. Defender for Endpoint respects Android profile boundaries and can't access files in the user's personal profile.

Use the Managed apps app configuration policy procedure, and add the following configuration key in the **General configuration settings** section on the **Settings** tab:

- **Name**: `EnableNonAPKFileScan`
- **Value**:
    - `1`: Enable non-APK file scanning.
    - `0`: Disable non-APK file scanning (default).

## Optional permissions

Optional permissions let users complete onboarding without granting VPN or accessibility permissions. Users can review and grant these permissions later.

### Configure optional permissions

Use the Managed apps app configuration policy procedure, and add one or both of the following configuration keys in the **General configuration settings** section on the **Settings** tab:

- **Name**: `DefenderOptionalVPN`
- **Value**:

    - `1`: Let users skip VPN permission during onboarding.
    - `0`: Require VPN permission during onboarding (default).
- **Name**: `DefenderOptionalAccessibility`
- **Value**:

    - `1`: Let users skip accessibility permission during onboarding.
    - `0`: Require accessibility permission during onboarding (default).

### User flow for optional permissions during onboarding

When optional permissions are enabled, users experience the following behavior:

1. Users can skip the VPN permission, the accessibility permission, or both, and complete onboarding.
2. The device onboards and sends a heartbeat even when the user skips the permissions.
3. Web protection isn't active when both permissions are disabled. Web protection is partially active when the user grants one of the permissions.
4. Users can later enable web protection from the Defender app. Enabling web protection installs the VPN configuration on the device.

Note

Optional permissions and disabling web protection have different effects. Optional permissions let users skip permissions during onboarding and grant them later. Disabling web protection lets users onboard without web protection, but they can't enable it later.

## Disable sign out

Hiding the sign-out button helps prevent users from signing out of the Defender app so that Defender for Endpoint continues running.

Use the Managed apps app configuration policy procedure, and add the following configuration key in the **General configuration settings** section on the **Settings** tab:

- **Name**: `DisableSignOut`
- **Value**:
    - `1`: Hide the sign-out button.
    - `0`: Show the sign-out button (default).

## Configure device tagging

Defender for Endpoint on Android supports bulk tagging of mobile devices during onboarding. After users install and activate Defender, the client app sends the device tags to the Microsoft Defender portal. The tags appear with the devices in the device inventory.

Use the Managed apps app configuration policy procedure, and add the following configuration key in the **General configuration settings** section on the **Settings** tab:

- **Name**: `DefenderDeviceTag`
- **Value**:
    - To assign a new tag, enter a string value for the device tag.
    - To edit an existing tag, change the value.
    - To delete an existing tag, remove the key from the policy.

Note

Users must open the Defender app before tags can sync with Intune and pass to the Microsoft Defender portal. Tags might take up to 18 hours to appear in the portal.

## Disable end-user onboarding

Defender for Endpoint on Android is enabled by default in MAM mode. To prevent users from downloading and setting up Defender on unenrolled devices, use the Managed apps app configuration policy procedure, and add the following configuration key in the **General configuration settings** section on the **Settings** tab:

- **Name**: `DefenderMAMConfigs`
- **Value**:
    - `0`: Disable end-user onboarding.
    - `1`: Enable end-user onboarding (default).