---
layout: Conceptual
title: Approve Microsoft Defender for Endpoint extensions in Microsoft Intune - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/manage-profiles-approve-sys-extensions-intune
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use the Microsoft Intune settings catalog to approve the macOS system extensions required by Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.author: chrisda
author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.topic: how-to
ms.date: 2026-09-17T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
locale: en-us
document_id: b20adb2d-8442-c0e9-aa7c-620d2fe44457
document_version_independent_id: b20adb2d-8442-c0e9-aa7c-620d2fe44457
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/manage-profiles-approve-sys-extensions-intune.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: manage-profiles-approve-sys-extensions-intune
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/manage-profiles-approve-sys-extensions-intune.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/a72e95ff-4b4f-4cc1-90c6-7dcba67ff05f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/24dc3ccd-591a-4415-a1fe-8759afafcb12
platformId: 2a9ff894-9e16-0a24-d549-e658f4c2e336
---

# Approve Microsoft Defender for Endpoint extensions in Microsoft Intune - Microsoft Defender for Endpoint | Microsoft Learn

Use the Microsoft Intune settings catalog to approve the endpoint security and network extensions required by Microsoft Defender for Endpoint on managed macOS devices.

The procedure in this article requires Microsoft Intune. Intune is a separate product that isn't part of Microsoft Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have Intune, see [Configure Microsoft Defender for Endpoint system extension profiles with Jamf Pro](mac-sysext-policies#configure-profiles-with-jamf-pro). For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

Note

The macOS **Extensions** template in Intune was deprecated in the August 2024 service release (2408). Policies created with the template continue to work, but you can't create new policies with it.

Use the settings catalog to create policies that configure the macOS System Extensions payload.

## Prerequisites

Before you create the policy, verify the following requirements:

- The devices meet the [Microsoft Defender for Endpoint on macOS prerequisites](microsoft-defender-endpoint-mac-prerequisites).
- The devices are enrolled in Intune by using **Automated Device Enrollment** or **Device enrollment**. For more information, see [Enrollment guide: Enroll macOS devices in Microsoft Intune](/en-us/intune/device-enrollment/apple/guide-macos).
- Your account has the Intune **Policy and Profile Manager** role. For more information, see [Built-in roles for Microsoft Intune](/en-us/intune/fundamentals/role-based-access-control/ref-built-in-roles#policy-and-profile-manager).

## Configure the Intune system extensions policy

Create a policy by following the instructions in [Create a policy using the settings catalog in Microsoft Intune](/en-us/intune/device-configuration/settings-catalog/) (link opens in a new window).

When you create the policy on the **Policies** tab of the **Devices | Configuration** page in the Microsoft Intune admin center at [https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/DevicesMenu/~/configuration](https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/DevicesMenu/%7E/configuration), by selecting **Create** &gt; ![](media/defender-portal-icon-create.png)**New policy**, use these specific settings:

- **Platform**: Select **macOS**.
- **Profile type**: Select **Settings catalog**.

In the **Settings catalog** wizard, add and configure the Defender for Endpoint system extension settings on the **Configuration settings** tab:

1. Select **Add settings**.
2. In the **Settings picker**, enter `allowed system` in the search box, and then select **Search**.
3. Under **Browse by category**, select **System Configuration** &gt; **System Extensions**.
4. Select the following settings:

    - **Allowed System Extension Types**
    - **Allowed System Extensions**

    [![Screenshot of the Intune Settings picker with Allowed System Extension Types and Allowed System Extensions selected.](media/intune-macos-settings-catalog-select.png)](media/intune-macos-settings-catalog-select.png#lightbox)
5. Close the **Settings picker**.
6. Configure **Allowed System Extensions**:

    1. In the **Allowed System Extensions** section, select **+ Edit instance**.
    2. In the **Configure instance**flyout, enter the following bundle identifiers, one per box:
        - `com.microsoft.wdav.epsext`
        - `com.microsoft.wdav.netext`
    3. For **Team Identifier**, enter `UBF8T346G9`.
    4. Select **Save**.

    [![Screenshot of the Configure instance flyout with the Defender for Endpoint bundle identifiers and team identifier entered.](media/intune-macos-settings-catalog-allowed-system-extensions.png)](media/intune-macos-settings-catalog-allowed-system-extensions.png#lightbox)
7. Configure **Allowed System Extension Types**:

    1. In the **Allowed System Extension Types** section, select **+ Edit instance**.
    2. In the **Configure instance**flyout, enter the following values, one per box:
        - `Network`
        - `EndpointSecurity`
    3. For **Team Identifier**, enter `UBF8T346G9`.
    4. Select **Save**.

    [![Screenshot of the Configure instance flyout with Network, EndpointSecurity, and the Microsoft team identifier entered.](media/intune-macos-settings-catalog-allowed-system-extension-types.png)](media/intune-macos-settings-catalog-allowed-system-extension-types.png#lightbox)
8. Verify that both entries appear on the **Configuration settings** tab.

    [![Screenshot of the Configuration settings tab with Allowed System Extensions and Allowed System Extension Types configured.](media/intune-macos-settings-catalog-configured-settings.png)](media/intune-macos-settings-catalog-configured-settings.png#lightbox)

On the **Assignments** tab, assign the policy to the devices that should receive it. Complete the remaining tabs, and then create the policy.

The next time the targeted devices check in, they receive the system extension settings.