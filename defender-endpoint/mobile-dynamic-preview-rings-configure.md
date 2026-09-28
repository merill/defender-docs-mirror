---
layout: Conceptual
title: Configure Dynamic Preview Rings for Microsoft Defender on mobile - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/mobile-dynamic-preview-rings-configure
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use Dynamic Preview Rings to enable preview features on the production Microsoft Defender mobile app for a selected group of users on Android and iOS.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.reviewer: smwasson
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-android
- mde-ios
ms.topic: how-to
ms.subservice: ngp
ms.date: 2026-09-09T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
locale: en-us
document_id: 3f1d9584-4f03-333c-a3a3-c0b2d36d5ec5
document_version_independent_id: 3f1d9584-4f03-333c-a3a3-c0b2d36d5ec5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/mobile-dynamic-preview-rings-configure.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mobile-dynamic-preview-rings-configure
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/mobile-dynamic-preview-rings-configure.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/80beb97b-18aa-44f8-9420-8f2a4cd448eb
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/8c09e0ef-0fde-4b6d-bf1b-b517e4db7f80
platformId: 4362a5ca-e64b-ec3e-095f-b17235c0e946
---

# Configure Dynamic Preview Rings for Microsoft Defender on mobile - Microsoft Defender for Endpoint | Microsoft Learn

Organizations often need to validate new experiences and capabilities before they deploy them broadly. Traditionally, this validation requires distributing separate preview builds of the app and managing more enrollment or distribution processes.

Dynamic Preview Rings let you evaluate upcoming Microsoft Defender mobile experiences on Android and iOS devices without distributing separate preview builds of the app. Use a Microsoft Intune [app configuration policy](/en-us/intune/app-management/configuration/overview) for managed devices or managed apps to enable preview features for a pilot group in the production version of the Microsoft Defender app. Users outside the pilot group continue to receive only generally available features. A yellow banner at the top of the Microsoft Defender app indicates that preview features are active, which matches the behavior in the nonproduction build.

Intune delivers the `DefenderPreview` setting from the app configuration policy to the Microsoft Defender app. A value of `1` enables Dynamic Preview. A value of `0`, or removing the key from the policy, returns the app to production features.

The benefits of Dynamic Preview Rings are:

- Eliminates the need to distribute nonproduction builds of the Microsoft Defender mobile app for preview testing.
- Removes the requirement to collect personal Gmail IDs for Android testing in non-MDM scenarios, which addresses privacy concerns.
- Accelerates testing by using your existing configuration policy workflows.

The limitations of Dynamic Preview Rings are:

- Currently, Dynamic Preview Rings don't support enabling or disabling individual preview features independently. Preview participation is assigned at the preview audience level.
- On Android, Dynamic Preview Rings don't work if you use [Microsoft Tunnel](/en-us/intune/device-security/microsoft-tunnel/overview) features (exclusively or with Microsoft Defender).

Important

Dynamic Preview provides early access to preview features before they're generally available. Preview features are provided for evaluation purposes and might contain known or unknown issues, limitations, or incomplete functionality. As with other preview programs, preview features aren't intended for production use and might change before general availability.

Support and response processes for issues that occur only in preview features might differ from the processes for generally available features. Standard incident management (ICM) service-level agreement (SLA) commitments might not apply unless the issue is reproducible in a generally available (production) feature.

The set of preview features changes over time.

## Requirements

- Microsoft Defender for Endpoint must be deployed to your managed mobile devices.

    Intune is a separate product that isn't part of Microsoft Defender for Endpoint, and it isn't included in all subscriptions. You need a subscription that includes Intune, or you can buy Intune separately as a standalone subscription or add-on. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).
- An account assigned the Microsoft Intune [Application Manager role](/en-us/intune/fundamentals/role-based-access-control/ref-built-in-roles#application-manager), or a custom Intune role with equivalent **Managed apps** and **Mobile apps** permissions.
- Identify the users or groups that participate in preview validation. No Microsoft Entra role is required to assign the policy to an existing group. To create the group or manage its membership, you need the appropriate Microsoft Entra permissions, such as the **Groups Administrator** role, or you must be an owner of the group.

### Supported platforms

- Android
- iOS/iPadOS

On both platforms, use a Microsoft Intune app configuration policy for managed devices or managed apps to deliver the `DefenderPreview` setting.

## Configure Dynamic Preview Rings on Android

You configure the `DefenderPreview` key for Android by using either a managed devices policy or a managed apps policy.

### Configure on Android using MDM

Note

Before you create the policy, add and approve **Defender: Antivirus** from Managed Google Play, and then sync it to Intune. After the sync, the app appears in Intune as **Microsoft Defender: Antivirus**. If no Android apps are synced from Managed Google Play, the target app list is empty and you see the message "You have not added any Android apps from the managed Google Play store." For deployment steps, see [Deploy Microsoft Defender for Endpoint on Android with Microsoft Intune](/en-us/intune/device-security/microsoft-defender/deploy-android).

You can enable Dynamic Preview on enrolled Android devices using a **Managed devices** app configuration policy. For detailed instructions, see [Create an app configuration policy](/en-us/intune/app-management/configuration/configure-managed-android#create-an-app-configuration-policy) or [Update an app configuration policy](/en-us/intune/app-management/configuration/overview) (links open new tabs in the Intune documentation).

When you create the policy, use these specific settings:

- **Policy type**: On the **Apps | Configuration** page in the Microsoft Intune admin center at [https://intune.microsoft.com/#view/Microsoft_Intune_Apps/ConfigPoliciesMenu/~/appConfigurationPolicies](https://intune.microsoft.com/#view/Microsoft_Intune_Apps/ConfigPoliciesMenu/%7E/appConfigurationPolicies), select **Create** &gt; **Managed devices**.
- **Platform**: Select **Android Enterprise**.
- **Profile type**: Select one of the following values:
    - **All Profile Types**: Applies the policy to all supported enrollment types.
    - **Fully Managed, Dedicated, and Corporate-Owned Work Profile Only**: For corporate-owned, personally enabled (COPE) and corporate-owned, business only (COBO) devices.
    - **Personally-Owned Work Profile Only**: For bring-your-own-device (BYOD) devices.
- **Target app**: Select **Select app**, find and select **Microsoft Defender: Antivirus**, and then select **OK**.

When you create or modify the policy, use these specific settings in the **Configuration settings** section:

1. **Configuration settings format**: Select **Use configuration designer**, and then select **Add**.
2. In the flyout that opens, use the search box to find **Defender Preview**, select **[Preview] Defender Preview** from the results, and then select **OK**.
3. In the **[Preview] Defender Preview** entry, set **Configuration value** to `1` (the default value is `0`).

To confirm the policy is applied, verify that **DefenderPreview** is present and set to `1` on the target device.

### Configure on Android using MAM

You can enable Dynamic Preview on enrolled or unenrolled Android devices using a **Managed apps** app configuration policy. For detailed instructions, see [Add an app configuration policy for managed apps](/en-us/intune/app-management/configuration/configure-managed-apps#add-an-app-configuration-policy-for-managed-apps-on-iosipados-and-android-devices) or [Update an app configuration policy](/en-us/intune/app-management/configuration/overview) (links open new tabs in the Intune documentation).

When you create the policy, use these specific settings:

- **Policy type**: On the **Apps | Configuration** page in the Microsoft Intune admin center at [https://intune.microsoft.com/#view/Microsoft_Intune_Apps/ConfigPoliciesMenu/~/appConfigurationPolicies](https://intune.microsoft.com/#view/Microsoft_Intune_Apps/ConfigPoliciesMenu/%7E/appConfigurationPolicies), select **Create** &gt; **Managed apps**.
- **Target policy to**: Verify **Selected apps** is selected.
- **Public apps**: Select **Select public apps**, find and select **Microsoft Defender Endpoint Android**, and then select **Select**.

When you create or modify the policy, use these specific settings in the **General configuration settings** section:

- **Name**: Enter `DefenderPreview`.
- **Value**: Enter `1`.

## Configure Dynamic Preview Rings on iOS

You configure the `DefenderPreview` key for iOS by using either a managed devices policy or a managed apps policy.

### Configure on iOS using MDM

Note

Before you create the policy, add the Microsoft Defender app from the Apple App Store to Intune so it appears in the target app list. If no iOS store apps are added to Intune, the target app list is empty and you can't select the app. For deployment steps, see [Deploy Microsoft Defender for Endpoint on iOS with Microsoft Intune](ios-install).

You can enable Dynamic Preview on enrolled iOS devices using a **Managed devices** app configuration policy. For detailed instructions, see [Create an app configuration policy](/en-us/intune/app-management/configuration/configure-managed-ios#create-an-app-configuration-policy) or [Update an app configuration policy](/en-us/intune/app-management/configuration/overview) (links open new tabs in the Intune documentation).

When you create the policy, use these specific settings:

- **Policy type**: On the **Apps | Configuration** page in the Microsoft Intune admin center at [https://intune.microsoft.com/#view/Microsoft_Intune_Apps/ConfigPoliciesMenu/~/appConfigurationPolicies](https://intune.microsoft.com/#view/Microsoft_Intune_Apps/ConfigPoliciesMenu/%7E/appConfigurationPolicies), select **Create** &gt; **Managed devices**.
- **Platform**: Select **iOS/iPadOS**.
- **Target app**: Select **Select app**, find and select **Microsoft Defender: Security**, and then select **OK**.

When you create or modify the policy, use these specific settings:

- **Configuration settings format**: Select **Use configuration designer**.
- **Configuration key**: Enter `DefenderPreview`.
- **Value type**: Select **Integer**.
- **Configuration value**: Enter `1`.

To confirm the policy is applied, verify that **DefenderPreview** is present and set to `1` on the target device.

### Configure on iOS using MAM

You can enable Dynamic Preview on enrolled or unenrolled iOS devices using a **Managed apps** app configuration policy. For detailed instructions, see [Add an app configuration policy for managed apps](/en-us/intune/app-management/configuration/configure-managed-apps#add-an-app-configuration-policy-for-managed-apps-on-iosipados-and-android-devices) or [Update an app configuration policy](/en-us/intune/app-management/configuration/overview) (links open new tabs in the Intune documentation).

When you create the policy, use these specific settings:

- **Policy type**: On the **Apps | Configuration** page in the Microsoft Intune admin center at [https://intune.microsoft.com/#view/Microsoft_Intune_Apps/ConfigPoliciesMenu/~/appConfigurationPolicies](https://intune.microsoft.com/#view/Microsoft_Intune_Apps/ConfigPoliciesMenu/%7E/appConfigurationPolicies), select **Create** &gt; **Managed apps**.
- **Target policy to**: Verify **Selected apps** is selected.
- **Public apps**: Select **Select public apps**, find and select **Microsoft Defender Endpoint iOS/iPadOS**, and then select **Select**.

When you create or modify the policy, use these specific settings in the **General configuration settings** section:

- **Name**: Enter `DefenderPreview`.
- **Value**: Enter `1`.