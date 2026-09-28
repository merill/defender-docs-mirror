---
layout: Conceptual
title: Troubleshoot issues on Microsoft Defender for Endpoint on Android - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/android-support-signin
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Troubleshoot issues for Microsoft Defender for Endpoint on Android
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-android
ms.topic: troubleshooting-general
ms.subservice: android
ms.date: 2026-04-12T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 387efabe-fa90-d50f-f7d6-5edde8e835f2
document_version_independent_id: 387efabe-fa90-d50f-f7d6-5edde8e835f2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/android-support-signin.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: android-support-signin
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/android-support-signin.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/5686b492-7c45-4088-8291-ecc0458747d3
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/838f4f15-80c1-4d49-b873-501fe4ed2d28
platformId: 1f6fcda2-e0f8-0c77-de72-a1f820dd54b3
---

# Troubleshoot issues on Microsoft Defender for Endpoint on Android - Microsoft Defender for Endpoint | Microsoft Learn

When onboarding a device, you might see sign in issues after the app is installed.

During onboarding, you might encounter sign in issues after the app is installed on your device.

This article provides solutions to help address the sign-on issues.

## Sign in failed - unexpected error

**Sign in failed:***Unexpected error, try later*

[![A screenshot showing a sign-in failed error Unexpected error in the sign-in page of the Microsoft Defender 365 portal.](media/f9c3bad127d636c1f150d79814f35d4c.png)](media/f9c3bad127d636c1f150d79814f35d4c.png#lightbox)

**Message:**

Unexpected error, try later

**Cause:**

You have an older version of "Microsoft Authenticator" app installed on your device.

**Solution:**

Install latest version and of [Microsoft Authenticator](https://play.google.com/store/apps/details?id=com.azure.authenticator) from Google Play Store and try again.

## Sign in failed - invalid license

**Sign in failed:***Invalid license, contact administrator*

[![The directive contact details in the sign-in page of the Microsoft Defender 365 portal](media/920e433f440fa1d3d298e6a2a43d4811.png)](media/920e433f440fa1d3d298e6a2a43d4811.png#lightbox)

**Message:***Invalid license, contact administrator*

**Cause:**

You don't have Microsoft 365 license assigned, or your organization doesn't have a license for Microsoft 365 Enterprise subscription.

**Solution:**

Contact your administrator for help.

## Report unsafe site

Phishing websites impersonate trustworthy websites for obtaining your personal or financial information. Visit the [Provide feedback about network protection](https://www.microsoft.com/wdsi/filesubmission/exploitguard/networkprotection) page if you want to report a website that could be a phishing site.

## Phishing pages aren't blocked on some OEM devices

**Applies to:** Specific OEMs only

- **Xiaomi**

Phishing and harmful web threats detected by Defender for Endpoint for Android aren't blocked on some Xiaomi devices. The following functionality doesn't work on these devices.

[![A site-unsafe notification message](media/0c04975c74746a5cdb085e1d9386e713.png)](media/0c04975c74746a5cdb085e1d9386e713.png#lightbox)

**Cause:**

Xiaomi devices include a new permission model. This permission model prevents Defender for Endpoint for Android from displaying pop-up windows while it runs in the background.

Xiaomi devices permission: "Display pop-up windows while running in the background."

[![The pop-up setting pane in the Microsoft Defender 365 portal](media/6e48e7b29daf50afddcc6c8c7d59fd64.png)](media/6e48e7b29daf50afddcc6c8c7d59fd64.png#lightbox)

**Solution:**

Enable the required permission on Xiaomi devices.

- Display pop-up windows while running in the background.

## Unable to allow permission for 'Permanent protection' during onboarding on some OEM devices

**Applies to:** Specific OEM devices only.

- **Xiaomi**

Defender App asks for Battery Optimization/Permanent Protection permission on devices as part of app onboarding, and selecting **Allow** returns an error that the permission couldn't be set. It only affects the last permission called "Permanent Protection."

**Cause:**

Xiaomi changed the battery optimization permissions from Android 11 onwards. Defender for Endpoint isn't allowed to configure this setting to ignore battery optimizations.

**Solution 1:**

The Android devices Battery Optimization screen opens automatically as part of the onboarding flow where the user needs to give the permissions. The user must then follow these steps to get on-boarded:

1. Select Work Profile to see all of the work profile apps

    ![Image of Battery Optimization screen](media/android-support-signin/image.png)
2. Tap on **Not optimized** and select **All Apps**

    ![Image of Optimization dropdown menu](media/android-support-signin/image1.png)

    ![Image of All Apps option in the dropdown](media/android-support-signin/image2.png)
3. Scroll down to find **Microsoft Defender** and tap on it

    ![Image of All Apps including Microsoft Defender](media/android-support-signin/image3.png)
4. Select **Don't Optimize** option and tap on **Done**![Image of the Microsoft Defender Optimize drop down](media/android-support-signin/image4.png)
5. Navigate back to Defender

**Solution 2** (needed in case the Solution 1 doesn't work):

1. Install the Microsoft Defender for Endpoint app in personal profile. (Sign-in isn't required.)
2. Open the Company Portal and tap on Settings.
3. Go to the Battery Optimization section, tap on the **Turn Off** button, and then select on **Allow** to turn off Battery Optimization for the Company Portal.
4. Again, go to the Battery Optimization section and tap on the **Turn On** button. The battery saver section opens.
5. Find the Defender app and tap on it.
6. Select **No Restriction**. Go back to the Defender app in work profile and tap on **Allow** button.
7. The application shouldn't be uninstalled from personal profile for this to work.

## Unable to use certain third party applications along with the Microsoft Defender for Endpoint app (VPN)

**Applies to:** (Not limited) Apps handling banking, government services, or handling sensitive personal information

**Cause:** Some applications, such as those used for banking, government services, or handling sensitive personal information, may restrict access if a VPN is detected on your device. These restrictions are determined by the app developer as part of their implementation and even applies all VPNs \*including third party on the device. Microsoft Defender doesn't control or enforce this behavior through its settings or policies.

**Workaround:** If an app doesn't function while a VPN is enabled or present in the work profile, you might need to disable the VPN or work profile when you use the app. Users should enable VPN when they're no longer using the app to ensure that their devices are protected.

## Send in-app feedback

If a user faces an issue, which isn't already addressed in the above sections or is unable to resolve using the listed steps, the user can provide **in-app feedback** along with **diagnostic data**. Our team can then investigate the logs to provide the right solution. Users can follow these steps to do the same:

1. Open the **Microsoft Defender for Endpoint application** on your device and select the **profile icon** in the top-left corner.
2. Select **Help & feedback** &gt; **Send feedback**.

    [![Screenshots showing how to send feedback and logs from the Microsoft Defender mobile app options menu.](media/android-new-ux/bottom-experience-android.png)](media/android-new-ux/bottom-experience-android.png#lightbox)
3. Provide details of the issue that you're facing and check **Include diagnostic data**. We recommend selecting **Include your email address** so that the team can reach back to you with a solution or a follow-up.
4. Select on **Submit** to successfully send the feedback.