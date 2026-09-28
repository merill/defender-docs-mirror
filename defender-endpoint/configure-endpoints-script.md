---
layout: Conceptual
title: Onboard Windows devices to Microsoft Defender for Endpoint with a local script - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/configure-endpoints-script
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use a local script to onboard, verify, and offboard a limited number of Windows devices in Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.reviewer: pahuijbr
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.custom: admindeeplinkDEFENDER, msecd-doc-authoring-1015
ms.topic: install-set-up-deploy
ms.subservice: onboard
ms.date: 2026-09-21T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 9ec0ea04-d85d-6d35-5057-d38a07400f09
document_version_independent_id: 9ec0ea04-d85d-6d35-5057-d38a07400f09
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/configure-endpoints-script.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-endpoints-script
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/configure-endpoints-script.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 95a73f90-d80c-9392-2b7c-aef51a9315b3
---

# Onboard Windows devices to Microsoft Defender for Endpoint with a local script - Microsoft Defender for Endpoint | Microsoft Learn

You can use a local script to onboard up to 10 supported Windows client or Windows Server devices to Microsoft Defender for Endpoint. This method is useful for evaluating the service before you select a deployment method for a larger environment. Before you begin, review the prerequisites, and then download and run the script, configure sample collection, verify onboarding, or offboard devices.

Important

Use the local script on 10 devices or fewer. For a production deployment, select a scalable method such as Group Policy, Microsoft Configuration Manager, Microsoft Intune, or the Defender deployment tool. To compare the available methods, see [Identify Defender for Endpoint architecture and deployment methods](deployment-strategy) and [other deployment options for Windows client devices](onboard-client).

Note

The Defender deployment tool can be used to deploy Defender endpoint security on Windows and Linux devices. The tool is a lightweight, self-updating application that streamlines the deployment process. For more information, see [Deploy Microsoft Defender endpoint security to Windows devices using the Defender deployment tool](/en-us/defender-endpoint/defender-deployment-tool-windows) and [Deploy Microsoft Defender endpoint security to Linux devices using the Defender deployment tool (preview)](/en-us/defender-endpoint/linux-install-with-defender-deployment-tool).

## Prerequisites

- Review the [minimum requirements for Microsoft Defender for Endpoint](minimum-requirements) and [configure device connectivity](configure-device-connectivity).
- To download onboarding and offboarding packages, you need full access to Defender for Endpoint. The Microsoft Entra [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator) role grants this access. For more information, see [Assign basic permissions](basic-permissions).
- Sign in to the device with an account that has local administrator permissions.

## Onboard devices with a local script

Download the onboarding package from the Microsoft Defender portal, and then run the included script on each device.

1. On the **Onboarding** page in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/endpoints/onboarding, configure the package:

    1. **Step 1: Select an operating system to start deployment**: Select the operating-system version group for the device. Don't select **Windows**, which starts the separate [Defender deployment tool workflow](defender-deployment-tool-windows).
    2. If **Connectivity type**is available, select the connectivity method for your environment:
        - **Standard**: Uses the full set of Defender for Endpoint service URLs.
        - **Streamlined**: Uses a smaller, consolidated set of service URLs. For more information, see [Onboard devices using streamlined connectivity](configure-device-connectivity).
    3. For **Deployment method**, select **Local script (for up to 10 devices)**.
    4. Select **Download onboarding package** to download `GatewayWindowsDefenderATPOnboardingPackage.zip`.
2. Extract the contents of the `.zip` file on the device to a location that's easy to find, such as the Desktop. The package contains `WindowsDefenderATPLocalOnboardingScript.cmd`.
3. Open Command Prompt as an administrator.
4. Go to the folder that contains `WindowsDefenderATPLocalOnboardingScript.cmd`. For example, the following command goes to the Desktop folder:

    ```dos
    if exist "%OneDrive%\Desktop" (cd /d "%OneDrive%\Desktop") else if exist "%USERPROFILE%\Desktop" cd /d "%USERPROFILE%\Desktop"
    ```
5. Run the onboarding script:

    ```dos
    WindowsDefenderATPLocalOnboardingScript.cmd
    ```
6. When the script displays **Press any key to continue...**, press any key to finish.

## Configure sample collection settings

Defender for Endpoint can collect files from an onboarded device when an analyst requests a file for deep analysis. The `AllowSampleCollection` registry value controls whether the device can respond to these requests:

- `0` (`00000000`): Don't allow sample sharing from the device.
- `1` (`00000001`): Allow sharing of all file types from the device. This setting is the default if the registry value doesn't exist.

To configure the setting manually, copy the following text into Notepad, set the `AllowSampleCollection` value, save the file with a `.reg` extension, and run the file on the device:

```text
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Advanced Threat Protection]
"AllowSampleCollection"=dword:00000000
```

## Verify device onboarding

After the script runs, verify that the device reports to Defender for Endpoint:

1. On the **Device inventory** page in the Microsoft Defender portal at https://security.microsoft.com/machines?category=all-devices, search for the device.
2. Open the device page, and verify that the device is onboarded and its sensor health state is active.

The device typically appears in the inventory within several minutes. Network connectivity and device state can delay reporting.

To generate a test alert and confirm end-to-end reporting, see [Run a detection test on a newly onboarded device](run-detection-test). If the device doesn't appear or report as expected, see [Troubleshoot Microsoft Defender for Endpoint onboarding issues](troubleshoot-onboarding).

## Offboard devices using a local script

The offboarding package expires seven days after you download it. Defender for Endpoint rejects expired packages, and the expiration date appears in the package file name.

Important

Don't run the onboarding and offboarding scripts on the same device at the same time. Complete onboarding or offboarding before you run the other script.

To offboard a device by using a local script, download and run the offboarding package:

1. On the **Offboarding** page in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/endpoints/offboarding, configure the package:

    1. Select the operating-system version group for the device. Don't select **Windows**, which starts the separate [Defender deployment tool workflow](defender-deployment-tool-windows).
    2. For **Deployment method**, select **Local script (for up to 10 devices)**.
    3. Select **Download package**, and then select **Download** in the confirmation dialog.
2. Extract `WindowsDefenderATPOffboardingPackage_valid_until_YYYY-MM-DD.zip` on the device to a location that's easy to find, such as the Desktop. The package contains `WindowsDefenderATPOffboardingScript_valid_until_YYYY-MM-DD.cmd`.
3. Open Command Prompt as an administrator.
4. Go to the folder that contains the offboarding script. For example, the following command goes to the Desktop folder:

    ```dos
    if exist "%OneDrive%\Desktop" (cd /d "%OneDrive%\Desktop") else if exist "%USERPROFILE%\Desktop" cd /d "%USERPROFILE%\Desktop"
    ```
5. Run the offboarding script:

    ```dos
    WindowsDefenderATPOffboardingScript_valid_until_YYYY-MM-DD.cmd
    ```

Important

Offboarding stops the device from sending new detection, vulnerability, and security data to Defender for Endpoint. Historical data remains in the Defender portal until the configured retention period expires. The device profile, without data, remains in the device inventory for up to 180 days. For more information, see [Offboard devices](offboard-machines).