---
layout: Conceptual
title: Onboard Windows devices to Microsoft Defender for Endpoint by using Microsoft Intune - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/configure-endpoints-mdm
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use Microsoft Intune to onboard and offboard Windows 10 and Windows 11 devices in Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.custom: admindeeplinkDEFENDER, msecd-doc-authoring-1015
ms.topic: install-set-up-deploy
ms.subservice: onboard
ms.date: 2026-08-24T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 176ce618-048e-0db6-3573-6dd50751a037
document_version_independent_id: 176ce618-048e-0db6-3573-6dd50751a037
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/configure-endpoints-mdm.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-endpoints-mdm
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/configure-endpoints-mdm.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/a72e95ff-4b4f-4cc1-90c6-7dcba67ff05f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/24dc3ccd-591a-4415-a1fe-8759afafcb12
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: fc591fef-70d6-4b45-6033-98f868793922
---

# Onboard Windows devices to Microsoft Defender for Endpoint by using Microsoft Intune - Microsoft Defender for Endpoint | Microsoft Learn

Note

The Defender deployment tool can be used to deploy Defender endpoint security on Windows and Linux devices. The tool is a lightweight, self-updating application that streamlines the deployment process. For more information, see [Deploy Microsoft Defender endpoint security to Windows devices using the Defender deployment tool](/en-us/defender-endpoint/defender-deployment-tool-windows) and [Deploy Microsoft Defender endpoint security to Linux devices using the Defender deployment tool (preview)](/en-us/defender-endpoint/linux-install-with-defender-deployment-tool).

Use Microsoft Intune to onboard Windows 10 and Windows 11 devices to Microsoft Defender for Endpoint. Onboarding configures devices to communicate with Defender for Endpoint for threat detection and device risk assessment. You can also use Intune to offboard devices that no longer need monitoring.

Defender for Endpoint supports mobile device management (MDM) configuration through Open Mobile Alliance Uniform Resource Identifier (OMA-URI) settings. For more information, see [WindowsAdvancedThreatProtection CSP](/en-us/windows/client-management/mdm/windowsadvancedthreatprotection-csp) and [WindowsAdvancedThreatProtection DDF file](/en-us/windows/client-management/mdm/windowsadvancedthreatprotection-ddf).

## Before you begin

- Enroll the devices in Microsoft Intune as your MDM solution. For more information, see [Device enrollment in Microsoft Intune](/en-us/intune/intune-service/fundamentals/deployment-guide-enrollment).
- To create endpoint detection and response (EDR) policies, use an account with the **Endpoint Security Manager** role or equivalent permissions.

Intune is a separate product that's not included with every Defender for Endpoint subscription. You need a subscription that includes Intune, or you can buy Intune separately as a standalone subscription or add-on. For details, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses). If you don't have Intune, review the other methods in [Identify Defender for Endpoint architecture and deployment method](deployment-strategy).

## Onboard devices using Microsoft Intune

Review [Defender for Endpoint architecture and deployment methods](deployment-strategy) to select the appropriate onboarding method for your environment.

To connect Intune to Defender for Endpoint and onboard devices, follow the instructions in [Configure Microsoft Defender for Endpoint with Intune and onboard devices](/en-us/intune/device-security/microsoft-defender/configure-integration).

Note

- The **Health Status for onboarded devices** policy uses read-only properties and can't be remediated.
- The diagnostic data reporting frequency setting was added in Windows 10, version 1703. In Intune EDR policies, the setting is deprecated and doesn't affect new devices.
- Onboarding a device to Defender for Endpoint also onboards it to [Endpoint data loss prevention (DLP)](/en-us/purview/endpoint-dlp-learn-about).

## Run a detection test to verify onboarding

After onboarding the device, you can choose to run a detection test to verify that a device is properly onboarded to the service. For more information, see [Run a detection test on a newly onboarded Microsoft Defender for Endpoint device](run-detection-test).

## Offboard devices using Mobile Device Management tools

For security reasons, the package used to offboard devices expires seven days after you download it. Expired offboarding packages sent to a device are rejected. When you download an offboarding package, the portal displays its expiration date, which is also included in the package name.

Note

To avoid unpredictable policy collisions, don't deploy onboarding and offboarding policies on a device at the same time.

1. Get the offboarding package from the Defender portal.

    On the **Offboarding** page in the Defender portal at https://security.microsoft.com/securitysettings/endpoints/offboarding, configure the following settings:

    1. At the top of the page, select **Windows 10 and Windows 11**.
    2. In the **Offboard a device** section that appears, select **Mobile Device Management / Microsoft Intune** as the **Deployment method**.
    3. At the bottom of the page, select **Download package**, select **Download** in the confirmation dialog, and then save the `WindowsDefenderATPOffboardingPackage_valid_until_YYYY-MM-DD.offboarding.zip` file in a location that's easy to find.
2. Extract the contents of the `.zip` file (a file named `WindowsDefenderATP_valid_until_YYYY-MM-DD.offboarding`) to a shared, read-only location that's accessible to the admins who are responsible for deploying the package.
3. In the Microsoft Intune admin center, use one of the following deployment methods:

    - **Custom configuration policy**: To create a **Windows** device configuration policy, see [Create a device configuration profile in Microsoft Intune](/en-us/intune/device-configuration/create-device-profile) (opens in a new tab in the Intune documentation). When you create the policy, use these specific settings:

        - **Platform**: Select **Windows 10 and later**.
        - **Profile type**: Select **Templates**.
        - **Template name**: Select **Custom**.
        - **Configuration settings**tab: Add the following settings:
            - **OMA-URI**: Enter `./Device/Vendor/MSFT/WindowsAdvancedThreatProtection/Offboarding`.
            - **Data type**: Select **String**.
            - **Value**: Paste the value from the content of the `WindowsDefenderATP_valid_until_YYYY-MM-DD` offboarding file.
    - **EDR policy**: To create an **Endpoint detection and response** policy, see [Deploy endpoint detection and response policy with Intune](/en-us/intune/device-configuration/endpoint-security/deploy-edr) (opens in a new tab in the Intune documentation). When you create the policy, use these specific settings:

        - **Platform**: Select **Windows**.
        - **Profile**: Select **Endpoint detection and response**.
        - **Configuration settings**tab:
            - **Microsoft Defender for Endpoint client configuration package type**: Select **Offboard**.
            - In the **Offboarding (Device)** setting that appears, paste the value from the content of the `WindowsDefenderATP_valid_until_YYYY-MM-DD` offboarding file.

Important

The **Health Status for offboarded devices** policy uses read-only properties and can't be remediated.

Offboarding stops the device from sending new detection, vulnerability, and security data to Defender for Endpoint. Historical data remains in the Defender portal until the configured retention period expires. The device profile, without data, remains in the device inventory for up to 180 days. For more information, see [Offboard devices](offboard-machines).