---
layout: Conceptual
title: Manually deploy Microsoft Defender for Endpoint on macOS - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/mac-install-manually
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to manually install and onboard Microsoft Defender for Endpoint on an individual Mac for evaluation or testing without using an MDM solution.
ms.service: defender-endpoint
author: paulinbar
ms.author: painbar
ms.reviewer: joshbregman
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-macos
ms.custom: admindeeplinkDEFENDER, msecd-doc-authoring-1015
ms.topic: how-to
ms.subservice: macos
ms.date: 2026-09-18T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 98b5e0b1-76ad-e85d-82fc-0804c80ff1f5
document_version_independent_id: 98b5e0b1-76ad-e85d-82fc-0804c80ff1f5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/mac-install-manually.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mac-install-manually
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/mac-install-manually.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: ec0063c9-84f0-d665-d09e-72775318f22b
---

# Manually deploy Microsoft Defender for Endpoint on macOS - Microsoft Defender for Endpoint | Microsoft Learn

> 
> Want to experience Defender for Endpoint? [Sign up for a free trial](https://go.microsoft.com/fwlink/p/?linkid=2225630).

You can use manual deployment to install and onboard Microsoft Defender for Endpoint on an individual evaluation or test Mac without using mobile device management (MDM). For centrally managed production devices, choose an MDM method in [Deploy Defender for Endpoint on macOS](microsoft-defender-endpoint-mac#deploy-defender-for-endpoint-on-macos).

Complete the following tasks:

- Download installation and onboarding packages
- Install the application
- Approve system extensions and macOS permissions
- Onboard the device
- [Verify the deployment](microsoft-defender-endpoint-mac#verify-the-deployment)

## Prerequisites

Before you start, review the [Defender for Endpoint on macOS prerequisites](microsoft-defender-endpoint-mac-prerequisites). You need local administrator privileges and a supported Mac that meets the licensing, system, permission, and network requirements.

Important

Manual installation requires changes to macOS privacy and security settings. For Apple's instructions, see [Change Privacy & Security settings on Mac](https://support.apple.com/guide/mac-help/change-privacy-security-settings-on-mac-mchl211c911f/mac).

## Download installation and onboarding packages

Download the installation and onboarding packages from the Microsoft Defender portal:

Warning

Repackaging the Defender for Endpoint installation package is not a supported scenario. Doing so can negatively impact the integrity of the product and lead to adverse results, including but not limited to triggering tampering alerts and updates failing to apply.

1. On the **Onboarding** page in the Microsoft Defender portal in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/endpoints/onboarding, select the following options:

    - **Step 1: Select an operating system to start deployment**: Select **macOS**.
    - **Connectivity type**: Select **Streamlined**.
    - **Deployment method**: Verify **Local script (for up to 10 devices)** is selected.
2. Select **Download installation package**, to download and save the `wdav.pkg` file.
3. Select **Download onboarding package** to download and save the `WindowsDefenderATPOnboardingPackage.zip` in the same folder.
4. Extract `WindowsDefenderATPOnboardingPackage.zip` to get the `WindowsDefenderATPOnboarding.mobileconfig` file.
5. Confirm that `wdav.pkg` and `WindowsDefenderATPOnboarding.mobileconfig` exist on the Mac where you want to deploy Defender for Endpoint.

## Install the application

Install `wdav.pkg` by using Finder or Terminal.

### Install by using Finder

To use the graphical installer:

1. In Finder, locate and open `wdav.pkg`.
2. Select **Continue**.
3. Review the **Software License Agreement**, and then select **Continue**.
4. Select **Agree** to accept the license agreement.
5. On the **Destination Select** page, select the installation disk, and then select **Continue**.
6. To use a different disk, select **Change Install Location...**.
7. Select **Install**.
8. Enter the local administrator password when prompted.
9. Select **Install Software**.

### Install by using Terminal

If `wdav.pkg` is in `/Users/admin/Downloads`, run the following command to install the application:

```console
sudo installer -pkg /Users/admin/Downloads/wdav.pkg -target /
```

## Approve system extensions and macOS permissions

After installation, [approve the system extensions and grant the applicable macOS permissions](manage-sys-extensions-manual-deployment). The procedure covers Full Disk Access, Accessibility, and notifications. When prompted to allow Microsoft Defender to filter network content, select **Allow**.

When macOS notifies you that Microsoft Defender added background items, keep the Microsoft Defender and Microsoft Corporation items enabled. If you use Bluetooth-based Device Control policies, select **Allow** when macOS prompts you to grant Microsoft Defender Bluetooth access.

For the required extension identifiers and permissions, see [System extensions and macOS permissions](microsoft-defender-endpoint-mac-prerequisites#system-extensions-and-macos-permissions). To resolve extension approval problems, see [Troubleshoot system extension issues](mac-support-sys-ext).

## Onboard the device

Install the onboarding configuration profile:

1. In Finder, open `WindowsDefenderATPOnboarding.mobileconfig`.
2. On the Mac, open the Apple menu, select **System Settings**, select **General** in the sidebar, and then select **Device Management**.
3. In the **Downloaded** section, double-click the onboarding profile.
4. Review the profile, and then select **Continue** or **Install**. Enter the local administrator password if prompted.

For more information about manually installing a configuration profile, see [Use configuration profiles to standardize settings on Mac computers](https://support.apple.com/guide/mac-help/configuration-profiles-standardize-settings-mh35561/mac).

After onboarding, the Microsoft Defender icon appears in the macOS menu bar.

![Screenshot of the Microsoft Defender icon in the macOS menu bar.](media/mdatp-icon-bar.png)

Use the shared [deployment verification procedure](microsoft-defender-endpoint-mac#verify-the-deployment) to confirm the organization identifier and service connectivity. Then run an [antivirus detection test](validate-antimalware) and an [endpoint detection and response (EDR) detection test](edr-detection).

If onboarding doesn't assign a license or connect the device to the service, see [Troubleshoot license issues](mac-support-license) and [Troubleshoot cloud connectivity issues](troubleshoot-cloud-connect-mdemac).

## Troubleshoot installation

The installer writes detailed errors to the [installation log](mac-resources#logging-installation-issues). Use the following resources to troubleshoot manual deployment:

- [Troubleshoot system extension issues in Microsoft Defender for Endpoint on macOS](mac-support-sys-ext)
- [Troubleshoot installation issues for Microsoft Defender for Endpoint on macOS](mac-support-install)
- [Troubleshoot license issues for Microsoft Defender for Endpoint on macOS](mac-support-license)
- [Troubleshoot cloud connectivity issues for Microsoft Defender for Endpoint on macOS](troubleshoot-cloud-connect-mdemac)
- [Troubleshoot performance issues for Microsoft Defender for Endpoint on macOS](mac-support-perf)

## Uninstall Defender for Endpoint

Follow the [Defender for Endpoint uninstallation procedure](mac-resources#uninstalling) to offboard the device and remove the application.

Tip

To share product feedback, open Microsoft Defender on the Mac, and then select **Help** &gt; **Send feedback**.