---
layout: Conceptual
title: Configure Microsoft Defender for Endpoint on iOS using MAM - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/ios-install-unmanaged
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to connect Microsoft Defender for Endpoint to Intune and use iOS app protection policies to enforce device threat-level requirements.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.reviewer: sunasing
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-ios
ms.topic: how-to
ms.subservice: ios
ms.date: 2026-09-21T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: 68d9aa52-738e-6701-e6a9-a9e2e64954b9
document_version_independent_id: 68d9aa52-738e-6701-e6a9-a9e2e64954b9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/ios-install-unmanaged.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: ios-install-unmanaged
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/ios-install-unmanaged.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/a72e95ff-4b4f-4cc1-90c6-7dcba67ff05f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/24dc3ccd-591a-4415-a1fe-8759afafcb12
platformId: 710b19c1-4e8d-0478-6c6a-49e9f4891aa2
---

# Configure Microsoft Defender for Endpoint on iOS using MAM - Microsoft Defender for Endpoint | Microsoft Learn

Microsoft Defender for Endpoint on iOS supports Microsoft Intune mobile application management (MAM) on devices that are enrolled or aren't enrolled in Intune mobile device management (MDM). Organizations that use another enterprise mobility management solution can also use Intune MAM to protect organizational data in managed apps.

Intune app protection policies use Defender for Endpoint device risk signals to apply conditional launch actions to managed apps. This article explains how to connect Defender for Endpoint to Intune, configure an iOS app protection policy, and prepare users to onboard Defender for Endpoint.

Microsoft Intune is required for the procedures in this article. Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

Note

Defender for Endpoint on iOS uses a local loopback virtual private network (VPN) for web protection. The VPN doesn't route traffic outside the device.

Defender for Endpoint on iOS supports the following MAM configurations:

- **Intune MDM with MAM**: Intune manages the device and applies app protection policies to managed apps.
- **MAM without device enrollment**: Intune applies [app protection policies](/en-us/intune/app-management/protection/create-policy) to managed apps on devices that aren't enrolled in Intune. This configuration, also known as MAM-WE, can protect apps on devices enrolled with a third-party enterprise mobility management provider.

Use the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) to manage apps in both configurations.

## Prerequisites

Before users can onboard Defender for Endpoint in MAM mode, connect Defender for Endpoint to Intune, enable the connector for iOS app protection policies, and create an app protection policy.

To configure the integration and policy, you need the following permissions:

- In Intune, the **Endpoint Security Manager**role or equivalent custom-role permissions:
    - To configure the service connection and app protection policy evaluation, **Read** and **Modify** permissions for **Mobile Threat Defense**.
    - To create and assign app protection policies, **Assign**, **Create**, **Delete**, **Read**, **Update**, and **Wipe** permissions for **Managed apps**.
- In Microsoft Entra ID, the **Security Administrator** role, or the **Manage security settings in Windows Security Center** permission in Defender for Endpoint.

### Connect Defender for Endpoint to Intune

For the complete connection procedure, see [Configure Microsoft Defender for Endpoint with Intune and onboard devices](/en-us/intune/device-security/microsoft-defender/configure-integration#connect-defender-for-endpoint-to-intune).

Verify the following settings:

- On the **Other options** page in the Microsoft Defender portal at https://security.microsoft.com/securitysettings/endpoints/integration, **Microsoft Intune Connection** is ![](media/toggle-on.png)**On**.
- On the **Endpoint security | Microsoft Defender for Endpoint** page in the Microsoft Intune admin center at [https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/~/atp](https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/%7E/atp), verify the following settings:
    - At the top of the page, **Connection status** is **Enabled**.
    - In the **App protection policy evaluation** section, **Connect iOS/iPadOS devices to Defender for Endpoint** is **On**.

## Configure Defender risk signals in an app protection policy

App protection policies protect organizational data in managed apps. An app integrated with the [Intune App SDK](/en-us/intune/developer/app-sdk/) or wrapped by the [Intune App Wrapping Tool](/en-us/intune/developer/app-sdk/configure-wrapping-ios) can be managed by Intune. For supported public apps, see [Microsoft Intune protected apps](/en-us/intune/app-management/ref-protected-apps).

For the complete procedure to create and assign an iOS/iPadOS app protection policy, see [Create and assign app protection policies](/en-us/intune/app-management/protection/create-policy#app-protection-policies-for-ios-ipados-and-android-apps).

When you create the policy on the **Apps | Protection** page in the Microsoft Intune admin center at [https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/AppsMenu/~/protection](https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/AppsMenu/%7E/protection), configure these Defender-specific settings:

- **Policy type**: Select ![](media/defender-portal-icon-create.png)**Create** &gt; **iOS/iPadOS**.
- **Apps** tab: Add at least one managed app. Target the policy to apps on managed devices, unmanaged devices, or devices in any management state, as required by your organization.
- **Conditional launch** tab: In the **Device conditions** section, select **Max allowed device threat level**, and then configure the following settings:
    - **Value**: Select the maximum threat level your organization allows: **Secured**, **Low**, **Medium**, or **High**. **Secured** is the most restrictive value. **High** allows all threat levels and requires an active connection to the Mobile Threat Defense service.
    - **Action**: Select **Block access** or **Wipe data**.
- **Primary MTD service**: If your organization configured multiple Mobile Threat Defense connectors, select **Microsoft Defender for Endpoint**. This setting requires **Max allowed device threat level**.
- **Assignments** tab: Assign the policy to the applicable user groups.

Defender for Endpoint shares the device threat level with Intune. When users sign in to a targeted managed app, Intune evaluates the Defender device risk signal. If the risk exceeds the allowed threat level, Intune blocks access or wipes organizational data from the app, depending on the action you selected.

## Onboard users

For iOS devices, Microsoft Authenticator registers the device and verifies the user's identity with Microsoft Entra ID. The user must register the device in Authenticator with the same work or school account used to activate Defender for Endpoint.

When a targeted managed app detects that Defender for Endpoint isn't activated, Intune guides the user to install and sign in to Microsoft Authenticator and Defender for Endpoint. Users can also install the latest version of [Microsoft Defender from the Apple App Store](https://aka.ms/mdatpiosappstore).

For more information about preparing the required apps for unenrolled devices, see [Add Mobile Threat Defense apps to unenrolled devices](/en-us/intune/device-security/mobile-threat-defense/add-apps-unenrolled-devices).