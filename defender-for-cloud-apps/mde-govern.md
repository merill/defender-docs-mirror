---
layout: Conceptual
title: Govern discovered apps using Microsoft Defender for Endpoint - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/mde-govern
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: Use the Microsoft Defender for Cloud Apps integration with Defender for Endpoint to govern discovered cloud apps by blocking or warning on unsanctioned apps.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: Mravela
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: e3ec30f4-dc4c-8a72-b672-27ef48133c29
document_version_independent_id: e3ec30f4-dc4c-8a72-b672-27ef48133c29
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/mde-govern.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mde-govern
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/mde-govern.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: bdc42d9c-dd24-931d-2b7e-0a7be7fe179a
---

# Govern discovered apps using Microsoft Defender for Endpoint - Microsoft Defender for Cloud Apps | Microsoft Learn

The Microsoft Defender for Cloud Apps [Integrate Defender for Cloud Apps with Microsoft Defender for Endpoint](mde-integration) provides a seamless Shadow IT visibility and control solution. Our integration enables Defender for Cloud Apps administrators to block access of end users to cloud apps, by natively integrating Defender for Cloud Apps app governance controls with Microsoft Defender for Endpoint's network protection. Alternatively, administrators can take a gentler approach of warning users when they access risky cloud apps.

Defender for Cloud Apps uses the built-in **Unsanctioned** app tag to mark cloud apps as prohibited for use, available in both the **Cloud Discovery** and **Cloud App Catalog** pages. For more information, see [Sanction or unsanction an app](governance-discovery#sanctioningunsanctioning-an-app). By enabling the integration with Defender for Endpoint, you can seamlessly block access to unsanctioned apps with a single click in Defender for Cloud Apps.

Apps marked as **Unsanctioned** in Defender for Cloud Apps are automatically synced to Defender for Endpoint. More specifically, the domains used by these unsanctioned apps are propagated to endpoint devices to be blocked by Microsoft Defender Antivirus within the Network Protection SLA.

Note

The time latency to block an app via Defender for Endpoint is up to three hours from the moment you mark the app as unsanctioned in Defender for Cloud Apps to the moment the app is blocked in the device. This latency is due to up to one hour of synchronization of Defender for Cloud Apps sanctioned/unsanctioned apps to Defender for Endpoint, and up to two hours to push the policy to the devices in order to block the app once the indicator was created in Defender for Endpoint.

## Prerequisites

Before you begin, make sure you meet the following requirements:

- One of the following licenses:

    - Defender for Cloud Apps + Endpoint
    - Microsoft 365 E5
- Microsoft Defender Antivirus. For more information, see:

    - [Real-time protection enabled](/en-us/microsoft-365/security/defender-endpoint/configure-real-time-protection-microsoft-defender-antivirus)
    - [Cloud-delivered protection enabled](/en-us/defender-endpoint/cloud-protection-configure)
    - [Network protection enabled and configured to block mode](/en-us/microsoft-365/security/defender-endpoint/enable-network-protection)
- One of the following supported operating systems:

    - Windows: Windows versions 10 18.09 (RS5) OS Build 1776.3, 11, and higher
    - Android: minimum version 8.0: For more information see: [Microsoft Defender for Endpoint on Android](/en-us/microsoft-365/security/defender-endpoint/microsoft-defender-endpoint-android#system-requirements)
    - iOS: minimum version 14.0: For more information see: [Microsoft Defender for Endpoint on iOS](/en-us/microsoft-365/security/defender-endpoint/microsoft-defender-endpoint-ios#prerequisites)
    - macOS: minimum version 11: For more information see: [Network protection for macOS](/en-us/microsoft-365/security/defender-endpoint/network-protection-macos)
    - [Linux system requirements](/en-us/microsoft-365/security/defender-endpoint/microsoft-defender-endpoint-linux): For more information see: [Network protection for Linux](/en-us/microsoft-365/security/defender-endpoint/network-protection-linux)
- Microsoft Defender for Endpoint onboarded. For more information, see [Onboard Defender for Cloud Apps with Defender for Endpoint](mde-integration#how-to-integrate-microsoft-defender-for-endpoint-with-defender-for-cloud-apps).
- Administrator access to make changes in Defender for Cloud Apps. For more information, see [Manage admin access](manage-admins).

## Enable cloud app blocking with Defender for Endpoint

Use the following steps to enable access control for cloud apps:

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Cloud Discovery**, select **Microsoft Defender for Endpoint**, and then select **Enforce app access**.

    ![Screenshot of Microsoft Defender for Endpoint settings showing the Enforce app access option under Cloud Discovery.](media/mde-integration.png)

    Note

    It can take up to 30 minutes for the **Enforce app access** setting to take effect.
2. In Microsoft Defender XDR, go to **Settings** &gt; **Endpoints** &gt; **Advanced features**, and then select **Custom network indicators**. For information about network indicators, see [Create indicators for IPs and URLs/domains](/en-us/microsoft-365/security/defender-endpoint/indicator-ip-domain).

    Enabling custom network indicators allows you to leverage Microsoft Defender Antivirus network protection capabilities to block access to a predefined set of URLs using Defender for Cloud Apps, either by manually [sanctioning or unsanctioning apps using app tags](governance-discovery#sanctioningunsanctioning-an-app) or automatically by [creating an app discovery policy](cloud-discovery-policies#creating-an-app-discovery-policy).

    ![Screenshot of the Advanced features settings page in Microsoft Defender XDR with the Custom network indicators toggle.](media/mde-custom-network-indicators.png)

## Educate users when accessing blocked apps & customize the block page

Admins can now configure and embed a support/help URL for block pages. With this configuration, admins can educate users when they access blocked apps. Users are prompted with a custom redirect link to a company page listing apps blocked for use and necessary steps to be followed to secure an exception on block pages. End users will be redirected to this URL that is configured by admin when they click on "Visit the Support page” on the block page.

Defender for Cloud Apps uses the built-in **Unsanctioned** app tag to mark cloud apps as blocked for use. The tag is available on both the **Cloud Discovery** and **Cloud App Catalog** pages. By enabling the integration with Defender for Endpoint, you can seamlessly educate users on apps blocked for use and steps to secure an exception with a single click in Defender for Cloud Apps.

Apps marked as **Unsanctioned** are automatically synced to Defender for Endpoint's custom URL indicators, usually within a few minutes. More specifically, the domains used by blocked apps are propagated to endpoint devices to provide a message by Microsoft Defender Antivirus within the Network Protection SLA.

### Setting up the custom redirect URL for the block page

Use the following steps to configure a custom help/support URL pointing to a company web page or a sharepoint link where you can educate employees on why they've been blocked from accessing the application and provide a list of steps to secure an exception or share the corporate access policy to adhere to your organization's risk acceptance.

1. In the Microsoft Defender portal, select **Settings** &gt; **Cloud Apps** &gt; **Cloud Discovery** &gt; **Microsoft Defender for Endpoint**.
2. In the **Alerts** dropdown, select **Informational**.
3. Under **User warnings** &gt; **Notification URL for blocked apps**, enter your URL. For example:

    [![Screenshot showing configuration of adding custom URL for blocked apps.](media/mde-govern/mda-custom-block-url-config.png)](media/mde-govern/mda-custom-block-url-config.png#lightbox)

## Disable informational alerts for unsanctioned app access (Preview)

By default, when users access an unsanctioned app, Defender for Cloud Apps generates an informational alert. To reduce alert noise and improve SOC focus in Microsoft Defender XDR, you can turn off these alerts using the **Generate alert for blocked app access** toggle.

When the toggle is off:

- Defender for Cloud Apps stops generating alerts for unsanctioned or blocked app access.
- Existing alerts aren't retroactively removed.
- Other Cloud Discovery or Defender alerts remain unaffected.
- Blocking enforcement continues to work as expected.

To turn off informational alerts:

1. In the Microsoft Defender portal, select **Setup & configuration** &gt; **Settings** &gt; **Cloud Apps** &gt; **Cloud Discovery** &gt; **Microsoft Defender for Endpoint**.
2. Locate the **Generate alert for blocked app access** toggle.
3. Turn off the toggle to disable informational alerts for blocked app access.

## Block apps for specific device groups

To block usage for specific device groups, do the following steps:

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Then under **Cloud discovery**, select **Apps tags** and go to the **Scoped profiles** tab.
2. Select **Add profile**. The scoped profile sets which entities are included or excluded for app blocking or unblocking.
3. Provide a descriptive profile name and description.
4. Choose whether the profile should be an **Include** or **Exclude** profile.

    - **Include**: only the included set of entities will be affected by the access enforcement. For example, the profile *myContoso* has **Include** for device groups A and B. Blocking app Y with the profile *myContoso* will block app access only for groups A and B.
    - **Exclude**: The excluded set of entities won't be affected by the access enforcement. For example, the profile *myContoso* has **Exclude** for device groups A and B. Blocking app Y with the profile *myContoso* will block app access for the entire organization except for groups A and B.
5. Select the relevant device groups for the profile. Device groups listed are pulled from Microsoft Defender for Endpoint. For more information, see [Create a device group](/en-us/microsoft-365/security/defender-endpoint/machine-groups#create-a-device-group).
6. Select **Save**.

    ![Screenshot of the scoped profiles tab for creating include or exclude device group profiles.](media/scoped-profiles.png)

To block an app, do the following steps:

1. In the Microsoft Defender Portal, under **Cloud Apps**, go to **Cloud Discovery** and go to the **Discovered apps** tab.
2. Select the app that should be blocked.
3. Tag the app as **Unsanctioned**.

    ![Screenshot of the Defender for Cloud Apps page for tagging a discovered app as unsanctioned.](media/unsanctioned-app.png)
4. To block all the devices in your organization, in the **Tag as unsanctioned?** dialog, select **Save**. To block specific device groups in your organizations, select **Select a profile to include or exclude groups from being blocked**. Then choose the profile for which the app will be blocked, and select **Save**.

    ![Screenshot of the profile selection dialog used to choose a scoped profile when tagging an app as unsanctioned.](media/choosing-unsanctioned-app-profile.png)

    The **Tag as unsanctioned?** dialog appears only when your tenant has cloud app blocking with Defender for Endpoint enabled and if you have admin access to make changes.

Note

- The enforcement ability is based on Defender for Endpoint’s custom URL indicators.
- Any organizational scoping that was set manually on indicators that were created by Defender for Cloud Apps before the release of this feature will be overridden by Defender for Cloud Apps. Any required organizational scoping for app blocking should be set from the Defender for Cloud Apps scoped profiles experience.
- To remove a selected scoping profile from an unsanctioned app, remove the unsanctioned tag and then tag the app again with the required scoped profile.
- It can take up to two hours for app domains to propagate and be updated in the endpoint devices once they're marked with the relevant tag or/and scoping.
- When an app is tagged as *Monitored*, the option to apply a scoped profile shows only if the built-in *Win10 Endpoint Users* data source has consistently received data during the past 30 days.
- Because device groups in Microsoft Defender for Business (MDB) are managed differently, no device groups appear in MDA device groups for customers with an MDB license.

## Educate users when accessing risky apps

Admins have the option to warn users when they access risky apps. Rather than blocking users, they're prompted with a message providing a custom redirect link to a company page listing apps approved for use. The warning prompt provides options for users to bypass the warning and continue to the app. Admins are also able to monitor the number of users that bypass the warning message.

Defender for Cloud Apps uses the built-in **Monitored** app tag to mark cloud apps as risky for use. The tag is available on both the **Cloud Discovery** and **Cloud App Catalog** pages. By enabling the integration with Defender for Endpoint, you can seamlessly warn users on access to monitored apps with a single click in Defender for Cloud Apps.

Apps marked as **Monitored** are automatically synced to Defender for Endpoint's custom URL indicators, usually within a few minutes. More specifically, the domains used by monitored apps are propagated to endpoint devices to provide a warning message by Microsoft Defender Antivirus within the Network Protection SLA.

### Setting up the custom redirect URL for the warn message

Use the following steps to configure a custom URL pointing to a company web page where you can educate employees on why they've been warned and provide a list of alternative approved apps that adhere to your organization's risk acceptance or are already managed by the organization.

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Cloud Discovery**, select **Microsoft Defender for Endpoint**.
2. In the **Notification URL** box, enter your URL.

    ![Screenshot of Microsoft Defender for Endpoint Cloud Discovery settings showing the Notification URL field for monitored app warnings.](media/mde-educate-config-notification-url.png)

### Setting up user bypass duration

Since users can bypass the warning message, you can use the following steps to configure how long the bypass remains in effect. Once the duration has elapsed, users are prompted with the warning message the next time they access the monitored app.

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Cloud Discovery**, select **Microsoft Defender for Endpoint**.
2. In the **Bypass duration** box, enter the duration (hours) of the user bypass.

    ![Screenshot of Microsoft Defender for Endpoint Cloud Discovery settings showing the Bypass duration field for monitored app warnings.](media/mde-educate-config-bypass-duration.png)

### Monitor applied app controls

Once access, block, or bypass controls are applied, you can monitor app usage patterns for those controls using the following steps.

1. In the Microsoft Defender Portal, under **Cloud Apps**, go to **Cloud Discovery** and then go to the **Discovered apps** tab. Use the [discovered app query filters](discovered-app-queries) to find the relevant monitored app.
2. Select the app's name to view applied app controls on the app's overview page.