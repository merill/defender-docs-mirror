---
layout: Conceptual
title: Troubleshoot Microsoft Defender for Endpoint macOS extensions - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/mac-support-sys-ext
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Diagnose and resolve Microsoft Defender for Endpoint system extension approval, profile deployment, and permission issues on macOS devices.
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
ms.custom: sfi-image-nochange, msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: 73c0c3f9-cafe-7b84-856b-e1664827793a
document_version_independent_id: 73c0c3f9-cafe-7b84-856b-e1664827793a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/mac-support-sys-ext.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mac-support-sys-ext
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/mac-support-sys-ext.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: e9d35351-31e6-b216-60fd-96f291e5d8a0
---

# Troubleshoot Microsoft Defender for Endpoint macOS extensions - Microsoft Defender for Endpoint | Microsoft Learn

Microsoft Defender for Endpoint uses endpoint security and network system extensions to protect macOS devices. If macOS doesn't approve or start an extension, real-time protection, network event inspection, or related features might be unavailable.

Use the symptoms and commands in this article to identify extension and profile problems. Then use the deployment-specific guidance to correct the configuration.

## Identify system extension symptoms

The Microsoft Defender shield in the macOS menu bar might display an **x** badge when Defender for Endpoint requires attention.

[![Screenshot of the macOS menu bar with an x badge on the Microsoft Defender shield.](media/mde-screen-with-x-symbol.png)](media/mde-screen-with-x-symbol.png#lightbox)

Select the shield to open the Defender menu. The **Action needed** option indicates that Defender requires configuration or user approval.

[![Screenshot of the Microsoft Defender menu with the Action needed option selected.](media/options-on-clicking-x-symbol.png)](media/options-on-clicking-x-symbol.png#lightbox)

Select **Action needed** to open the **Virus & threat protection** page. The page might display **Microsoft Defender needs attention** and a **Fix** button.

[![Screenshot of the Microsoft Defender Virus and threat protection page with the Fix button.](media/screen-on-clicking-action-needed.png)](media/screen-on-clicking-action-needed.png#lightbox)

Run the following command in Terminal to review the overall Defender health state:

```bash
mdatp health
```

When extensions or permissions aren't ready, the output can report an unhealthy state, unavailable protection, or missing Full Disk Access:

```output
healthy                            : false
health_issues                    : ["no active event provider", "network event provider not running", "full disk access has not been granted"]
...
real_time_protection_enabled    : true
real_time_protection_available: false
...
full_disk_access_enabled        : false
```

The following screenshot shows an unhealthy result with unavailable protection subsystems and Full Disk Access disabled:

[![Screenshot of mdatp health output showing unavailable protection subsystems and Full Disk Access disabled.](media/screen-on-clicking-fix.png)](media/screen-on-clicking-fix.png#lightbox)

For descriptions of the health fields, see [Troubleshoot agent health issues with Defender for Endpoint on macOS](mac-health-status).

## Diagnose the system extensions

On supported macOS versions, a mobile device management (MDM) profile or a local administrator must approve system extensions before they can run. Defender for Endpoint uses Microsoft Team ID `UBF8T346G9` and the following system extensions:

- Endpoint security extension: `com.microsoft.wdav.epsext`.
- Network extension: `com.microsoft.wdav.netext`.

Use the following commands to determine whether the extensions are installed, approved, and running:

1. List the registered system extensions:

    ```bash
    systemextensionsctl list
    ```

    [![Screenshot of systemextensionsctl output showing both Defender extensions waiting for user approval.](media/check-system-extension.png)](media/check-system-extension.png#lightbox)

    The `[activated waiting for user]` state indicates that macOS installed the extensions but is waiting for local approval. A healthy active extension reports `[activated enabled]`.
2. Review the Defender-specific system extension health details:

    ```bash
    mdatp health --details system_extensions
    ```

    When the extensions are installed but not approved or ready, the output can resemble the following example:

    ```output
    network_extension_enabled                 : false
    network_extension_installed                 : true
    endpoint_security_extension_ready           : false
    endpoint_security_extension_installed        : true
    ```

The following screenshot shows both extensions installed, but the network extension isn't enabled and the endpoint security extension isn't ready:

[![Screenshot of Defender system extension health showing installed extensions that aren't enabled or ready.](media/details-system-extensions-command.png)](media/details-system-extensions-command.png#lightbox)

The extension health result doesn't identify every required macOS permission. For example, `mdatp health` can separately report that Full Disk Access isn't granted. Review the [system extensions and macOS permissions](microsoft-defender-endpoint-mac-prerequisites#system-extensions-and-macos-permissions) required for your enabled Defender and Microsoft Purview features.

## Resolve extension and permission issues

Use the procedure for your deployment method to approve the extensions and grant the required permissions:

- **Microsoft Intune**: [Approve Defender for Endpoint system extensions in Intune](manage-profiles-approve-sys-extensions-intune). New policies must use the settings catalog because the older macOS **Extensions** template is deprecated. For general settings catalog guidance, see [Use the Intune settings catalog to configure settings](/en-us/intune/intune-service/configuration/settings-catalog). For the complete deployment sequence, see [Approve System Extensions](mac-install-with-intune).
- **Jamf Pro**: [Configure Defender for Endpoint system extensions using Jamf Pro](manage-sys-extensions-using-jamf).
- **Another MDM solution**: [Deploy Defender for Endpoint with another MDM solution](mac-install-with-other-mdm).
- **Manual deployment**: [Approve system extensions and permissions manually](manage-sys-extensions-manual-deployment).

For managed deployments, deploy system configuration profiles before the Defender application package. This sequence allows macOS to approve the extensions and permissions without relying on user prompts.

## Verify profile delivery

Before troubleshooting individual profiles, review the shared [Defender for Endpoint on macOS prerequisites](microsoft-defender-endpoint-mac-prerequisites).

### Check MDM profile delivery

Use your MDM solution to confirm that the required device-level profiles are assigned and successfully delivered to the affected Mac device. On the device, open **System Settings**, select **General**, and then select **Device Management** to review installed profiles.

If you use Jamf Pro, `sudo jamf policy` triggers applicable policies. For information about Jamf policy triggers and execution, see [Policy Management](https://learn.jamf.com/r/jamf-pro-documentation-current/Policy_Management).

Note

Use recognizable names for Defender configuration profiles so you can identify their purpose and deployment ring. For example, use `FullDiskAccess (piloting) - macOS - Default - MDE`.

### Verify the required profiles

Download current Microsoft-maintained profiles instead of manually recreating payloads. This approach prevents typing errors in bundle identifiers, Team IDs, code requirements, and payload values.

For the profile list and purpose of each payload, see Review maintained Defender profiles.

In Terminal, use the following syntax to download a profile to the current directory:

```bash
curl -O https://URL
```

For example, download the maintained system extensions profile:

```bash
curl -O https://raw.githubusercontent.com/microsoft/mdatp-xplat/master/macos/mobileconfig/profiles/sysext.mobileconfig
```

#### Review maintained Defender profiles

The [Defender for Endpoint macOS profile repository](https://github.com/microsoft/mdatp-xplat/tree/master/macos/mobileconfig/profiles) contains these relevant profiles:

- **System extension approval**: [`sysext.mobileconfig`](https://github.com/microsoft/mdatp-xplat/blob/master/macos/mobileconfig/profiles/sysext.mobileconfig) approves `com.microsoft.wdav.epsext` and `com.microsoft.wdav.netext` for Team ID `UBF8T346G9`.
- **Network filter**: [`netfilter.mobileconfig`](https://github.com/microsoft/mdatp-xplat/blob/master/macos/mobileconfig/profiles/netfilter.mobileconfig) configures the network extension as the Microsoft Defender Content Filter.
- **Full Disk Access**: [`fulldisk.mobileconfig`](https://github.com/microsoft/mdatp-xplat/blob/master/macos/mobileconfig/profiles/fulldisk.mobileconfig) grants access to the required Defender components.
- **Background services**: [`background_services.mobileconfig`](https://github.com/microsoft/mdatp-xplat/blob/master/macos/mobileconfig/profiles/background_services.mobileconfig) allows Defender services to run in the background.
- **Notifications**: [`notif.mobileconfig`](https://github.com/microsoft/mdatp-xplat/blob/master/macos/mobileconfig/profiles/notif.mobileconfig) configures Defender and Microsoft AutoUpdate notifications.
- **Accessibility**: [`accessibility.mobileconfig`](https://github.com/microsoft/mdatp-xplat/blob/master/macos/mobileconfig/profiles/accessibility.mobileconfig) grants Accessibility access to the Microsoft Purview data loss prevention daemon when that capability is used.

Don't use the presence of files under `/Library/Managed Preferences` as the only test for these Apple payloads. Verify profile delivery through the MDM solution, inspect the installed configuration profiles, and review the Defender health output.

## Analyze installed profiles

The Microsoft `analyze_profiles.py` script compares installed configuration payloads with the maintained Defender profile template. It reports missing, duplicate, or mismatched payloads and checks for onboarding and Defender preference profiles.

1. Review the script in the [Defender for Endpoint macOS MDM tools directory](https://github.com/microsoft/mdatp-xplat/tree/master/macos/mdm).
2. Select **Raw** to open https://raw.githubusercontent.com/microsoft/mdatp-xplat/master/macos/mdm/analyze_profiles.py.
3. From the directory where you want to save `analyze_profiles.py`, download the script by running the following command in Terminal:

    ```bash
    curl -O https://raw.githubusercontent.com/microsoft/mdatp-xplat/master/macos/mdm/analyze_profiles.py
    ```
4. Run the script with elevated permissions by using one of the following methods:

    - Run the downloaded script:

        ```bash
        cd ~/Downloads
        
        sudo python3 analyze_profiles.py
        ```

        Or
    - Run the script directly from the web:

        ```bash
        curl -sS https://raw.githubusercontent.com/microsoft/mdatp-xplat/master/macos/mdm/analyze_profiles.py | sudo python3 -
        ```

Review every reported issue in the context of your deployment. The script might report intentional profile choices that don't require changes.