---
layout: Conceptual
title: Deploy Microsoft Defender for Endpoint on macOS with another MDM solution - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/mac-install-with-other-mdm
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to deploy Microsoft Defender for Endpoint on macOS with an MDM solution other than Microsoft Intune or Jamf Pro.
ms.service: defender-endpoint
ms.reviewer: joshbregman
author: paulinbar
ms.author: painbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-macos
ms.topic: how-to
ms.subservice: macos
ms.date: 2026-09-18T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: 39244152-12e1-f3db-d8ca-834889bcd1f3
document_version_independent_id: 39244152-12e1-f3db-d8ca-834889bcd1f3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/mac-install-with-other-mdm.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mac-install-with-other-mdm
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/mac-install-with-other-mdm.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 16a77687-4acf-80a3-7182-c6faacf2f008
---

# Deploy Microsoft Defender for Endpoint on macOS with another MDM solution - Microsoft Defender for Endpoint | Microsoft Learn

You can use the guidance in this article to adapt the Microsoft Defender for Endpoint installation package, onboarding information, and Apple configuration profiles for a mobile device management (MDM) solution other than Microsoft Intune or Jamf Pro. Your MDM provider's terminology and procedures might differ.

To compare this method with [Microsoft Intune](mac-install-with-intune), [Jamf Pro](mac-install-with-jamf), or [manual deployment](mac-install-manually), see [Deploy Defender for Endpoint on macOS](microsoft-defender-endpoint-mac#deploy-defender-for-endpoint-on-macos).

Important

This article contains information about third-party tools. This is provided to help complete integration scenarios, however, Microsoft does not provide troubleshooting support for third-party tools.  Contact the third-party vendor for support.

## Prerequisites

Before you start, review the [Defender for Endpoint on macOS prerequisites](microsoft-defender-endpoint-mac-prerequisites), especially the [managed deployment requirements](microsoft-defender-endpoint-mac-prerequisites#managed-deployment-requirements). You also need:

- Your MDM provider's instructions for deploying signed `.pkg` files and device-level Apple configuration profiles.
- An MDM administrator account that can assign apps and profiles to managed Mac devices.

## Understand the support boundary

Defender for Endpoint doesn't depend on Intune-specific or Jamf Pro-specific features. You can use another MDM solution that meets the managed deployment requirements. Microsoft supports Defender for Endpoint, its installation package, and its documented configuration. Contact the MDM provider for support with the provider's deployment workflow and product behavior.

## Deploy Defender for Endpoint

Complete these tasks by using the equivalent package and profile deployment features in your MDM solution.

### Download the deployment packages

Download the installation and onboarding packages from the Microsoft Defender portal:

1. On the **Onboarding** page in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/endpoints/onboarding, configure the following settings:

    - **Step 1: Select an operating system to start deployment**: Select **macOS**.
    - **Connectivity type**: Select **Streamlined**. Before continuing, verify that your devices and network meet the [streamlined connectivity prerequisites](configure-device-connectivity#prerequisites).
    - **Deployment method**: Select **Mobile Device Management / Microsoft Intune**.
2. Select **Download onboarding package**, and save `GatewayWindowsDefenderATPOnboardingPackage.zip`.
3. Extract `GatewayWindowsDefenderATPOnboardingPackage.zip`. The extracted package contains:

    - `intune/WindowsDefenderATPOnboarding.xml`.
    - `jamf/WindowsDefenderATPOnboarding.plist`.
4. Select **Download installation package**, and save `wdav.pkg`.

### Deploy system configuration profiles

Download the Apple configuration profiles required for your macOS version and enabled Defender features from the [Defender for Endpoint macOS configuration profile repository](https://github.com/microsoft/mdatp-xplat/tree/master/macos/mobileconfig/profiles).

Import the required `.mobileconfig` files by using your MDM provider's custom profile workflow. Deploy the profiles at the device, computer, or system scope, and assign them to the applicable device groups. The profiles grant the [system extension and macOS permissions](microsoft-defender-endpoint-mac-prerequisites#system-extensions-and-macos-permissions) that Defender for Endpoint requires.

Apple configuration profiles use property list XML. You can inspect or adapt profiles by using tools such as [Apple Configurator](https://support.apple.com/apple-configurator) or [iMazing Profile Editor](https://imazing.com/profile-editor), but don't change Microsoft identifiers, payload types, or required values.

Review [What's new in Defender for Endpoint on macOS](microsoft-defender-endpoint-releases#macos-releases) for changes that require updated profiles.

### Deploy Defender for Endpoint settings

Use a device-level application configuration profile to deploy managed Defender settings. Defender for Endpoint reads managed settings from:

- `/Library/Managed Preferences/com.microsoft.wdav.plist`
- `/Library/Managed Preferences/com.microsoft.wdav.ext.plist`

Use `com.microsoft.wdav` or `com.microsoft.wdav.ext` as the preference domain, depending on the settings that you deploy. For the supported settings and required data structure, see [Set preferences for Defender for Endpoint on macOS](mac-preferences).

After the MDM solution delivers the profile, check that the corresponding managed preferences file exists. You can also inspect `/Library/Managed Preferences/com.microsoft.wdav.plist` and compare its structure with the profile that you deployed:

```shell
plutil -p "/Library/Managed Preferences/com.microsoft.wdav.plist"
```

The output resembles the following example:

```console
{
  "antivirusEngine" => {
    "scanHistoryMaximumItems" => 10000
  }
  "edr" => {
    "groupIds" => "my_favorite_group"
    "tags" => [
      0 => {
        "key" => "GROUP"
        "value" => "my_favorite_tag"
      }
    ]
  }
  "tamperProtection" => {
    "enforcementLevel" => "audit"
    "exclusions" => [
      0 => {
        "args" => [
          0 => "/usr/local/bin/test.sh"
        ]
        "path" => "/bin/zsh"
        "signingId" => "com.apple.zsh"
        "teamId" => ""
      }
    ]
  }
}
```

Setting names, nesting, and data types must match the documented structure. Defender ignores invalid or misspelled settings.

### Deploy the onboarding profile

If your MDM solution accepts an arbitrary property list, import `jamf/WindowsDefenderATPOnboarding.plist` from the extracted `GatewayWindowsDefenderATPOnboardingPackage.zip` file.

Configure the onboarding profile as a device-level profile. If the MDM workflow requires an application identifier, preference domain, or payload domain, use `com.microsoft.wdav.atp`. The profile must deliver the onboarding information to `/Library/Managed Preferences/com.microsoft.wdav.atp.plist`.

If your MDM solution requires another input format, follow the provider's instructions to convert or import the onboarding property list without changing its data structure.

### Deploy the application package

Warning

Repackaging the Defender for Endpoint installation package is not a supported scenario. Doing so can negatively impact the integrity of the product and lead to adverse results, including but not limited to triggering tampering alerts and updates failing to apply.

Deploy the signed `wdav.pkg` installation package without modification by using your MDM provider's app or package deployment procedure. Assign the package to the applicable device groups.

## Check profile deployment

Download and run [analyze_profiles.py](https://github.com/microsoft/mdatp-xplat/blob/master/macos/mdm/analyze_profiles.py) to identify potential problems with the profiles installed on a Mac device. The script provides diagnostic guidance and might report intentional configuration choices. Investigate each reported issue in the context of your deployment.

## Verify the deployment

Use the shared [Defender for Endpoint deployment verification](microsoft-defender-endpoint-mac#verify-the-deployment) to confirm onboarding, connectivity, antivirus detection, and EDR reporting.