---
layout: Conceptual
title: Create access policies - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/access-policy-aad
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
description: Learn how to configure Microsoft Defender for Cloud Apps access policies with Conditional Access app control to control access to cloud apps.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: Adipkmic
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 47a94209-1960-43b7-54f6-24c167af1720
document_version_independent_id: 47a94209-1960-43b7-54f6-24c167af1720
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/access-policy-aad.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: access-policy-aad
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/access-policy-aad.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 070ea569-5b82-fdca-a3bb-89b0b0dcd129
---

# Create access policies - Microsoft Defender for Cloud Apps | Microsoft Learn

Microsoft Defender for Cloud Apps access policies use Conditional Access app control to provide real-time monitoring and control over access to cloud apps. Access policies control access based on user, location, device, and app, and are supported for any device. Before you create an access policy, make sure you meet the prerequisites, including the required licenses and Conditional Access app control configuration.

Policies created for a host app aren't connected to any related resource apps. For example, access policies that you create for Teams, Exchange, or Gmail aren't connected to SharePoint, OneDrive, or Google Drive. If you need a policy for the resource app in addition to the host app, create a separate policy.

Tip

If you'd prefer to generally allow access while monitoring sessions or limit specific session activities, create session policies instead. For more information, see [Create session policies for Conditional Access app control](session-policy-aad).

## Prerequisites

Before you start, make sure that you have the following prerequisites:

- A Defender for Cloud Apps license, either as a stand-alone license or as part of another license
- A license for Microsoft Entra ID P1, either as stand-alone license or as part of another license
- If you're using a non-Microsoft IdP, the license required by your identity provider (IdP) solution
- A Microsoft Entra ID Conditional Access policy configured for Microsoft Defender for Cloud Apps (Conditional Access app control). The Conditional Access policy creates the permissions required to control traffic. For more information, see: [Automatically onboard Microsoft Entra ID apps to conditional access app control (preview)](app-onboarding#supported-apps)
- The relevant apps onboarded to Conditional Access app control. Microsoft Entra ID apps are automatically onboarded, while non-Microsoft IdP apps must be onboarded manually.

    If you're working with a non-Microsoft IdP, make sure that you've also configured your IdP to work with Microsoft Defender for Cloud Apps. For more information, see:

    - [Onboard non-Microsoft IdP catalog apps for Conditional Access app control](proxy-deployment-featured-idp)
    - [Onboard non-Microsoft IdP custom apps for Conditional Access app control](proxy-deployment-any-app-idp)

### Sample: Create Microsoft Entra ID Conditional Access policies for use with Defender for Cloud Apps

This procedure provides a high-level example of how to create a Conditional Access policy for use with Defender for Cloud Apps.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com) as at least a [Conditional Access Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#conditional-access-administrator).
2. Browse to **Entra ID** &gt; **Conditional Access** &gt; **Policies**.
3. Select **New policy**.
4. Give your policy a name. We recommend that organizations create a meaningful standard for the names of their policies.
5. Under **Assignments**, select **Users or workload identities**.
    1. Under **Include**, select **All users**
    2. Under **Exclude**, select **Users and groups** and choose your organization's emergency access or break-glass accounts.
6. Under **Target resources** &gt; **Resources (formerly cloud apps)**, select the following options:
    1. Under **Include**, choose **Select resources**.
    2. Select the client apps that you want to include in your policy.
7. Under **Conditions**, select any conditions that you want to include in your policy.
8. Under **Access controls** &gt; **Session**, select **Use Conditional Access App Control**, then select **Select**.
9. Confirm your settings and set **Enable policy** to **Report-only**.
10. Select **Create** to create to enable your policy.

After confirming your settings using [policy impact or report-only mode](/en-us/entra/identity/conditional-access/concept-conditional-access-report-only#reviewing-results), move the **Enable policy** toggle from **Report-only** to **On**.

For more information, see [Conditional Access policies](/en-us/azure/active-directory/conditional-access/overview) and [Building a Conditional Access policy](/en-us/entra/identity/conditional-access/concept-conditional-access-policies).

Note

Microsoft Defender for Cloud Apps uses the **Microsoft Defender for Cloud Apps - Session Controls** enterprise application for user sign-in through Conditional Access App Control. To protect software as a service (SaaS) applications with session controls, allow access to this application.

A Microsoft Entra Conditional Access policy that selects **Block access** under **Grant** and targets this application prevents users from accessing protected applications through session controls. For policies that block all or selected applications, exclude the session controls application under **Target resources** unless blocking it is intentional.

```powershell
# Connect with the appropriate scopes to create service principal
Connect-MgGraph -Scopes "Application.ReadWrite.All"

# Create service principal for the service **Microsoft Defender for Cloud Apps - Session Controls**
New-MgServicePrincipal -AppId 8a0c2593-9cbc-4f86-a247-beb7aab00d83
```

Include the **Microsoft Defender for Cloud Apps - Session Controls** application in location-based Conditional Access policies to ensure the policies work correctly.

## Create a Defender for Cloud Apps access policy

This procedure describes how to create a new access policy in Defender for Cloud Apps.

1. In Microsoft Defender, select the **Cloud Apps &gt; Policies &gt; Policy management &gt; Conditional Access** tab.
2. Select **Create policy** &gt; **Access policy**. For example:

    ![Screenshot of the Defender for Cloud Apps Policy management page with the Create policy menu expanded and the Access policy option highlighted.](media/create-policy-from-conditional-access-tab.png)
3. On the **Create access policy** page, enter the following basic information:

    | Name | Description |
    | --- | --- |
    | **Policy name** | A meaningful name for your policy, such as *Block access from unmanaged devices* |
    | **Policy severity** | Select the severity you want to apply to your policy. |
    | **Category** | Keep the default value of **Access control** |
    | **Description** | Enter an optional, meaningful description for your policy to help your team understand its purpose. |
4. In the **Activities matching all of the following** area, select additional activity filters to apply to the policy. Filters include the following options:

    | Name | Description |
    | --- | --- |
    | **App** | Filters for a specific app to include in the policy. Select apps by first selecting whether they use **Automated Azure AD onboarding**, for Microsoft Entra ID apps, or **Manual onboarding**, for non-Microsoft IdP apps. Then, select the app you want to include in your filter from the list. If your non-Microsoft IdP app is missing from the list, make sure that you've onboarded it fully. For more information, see: - [Onboard non-Microsoft IdP catalog apps for Conditional Access app control](proxy-deployment-featured-idp)- [Onboard non-Microsoft IdP custom apps for Conditional Access app control](proxy-deployment-any-app-idp)If you choose not to use the **App** filter, the policy applies to all applications that are marked as **Enabled** on the **Settings &gt; Cloud Apps &gt; Connected apps &gt; Conditional Access App Control apps** page.**Note**: You might see some overlap between apps that are onboarded and apps that need manual onboarding. In case of a conflict in your filter between the apps, manually onboarded apps take precedence. |
    | **Client app** | Filter for browser or mobile/desktop apps. |
    | **Device** | Filter for device tags, such as for a specific device management method, or device types, such as PC, mobile, or tablet. |
    | **IP address** | Filter per IP address or use previously assigned IP address tags. |
    | **Location** | Filter by geographic location. The absence of a clearly defined location might identify risky activities. |
    | **Registered ISP** | Filter for activities coming from a specific ISP. |
    | **User** | Filter for a specific user or group of users. |
    | **User agent string** | Filter for a specific user agent string. |
    | **User agent tag** | Filter for user agent tags, such as for outdated browsers or operating systems. |

    For example:

    ![Screenshot of a sample filter when creating an access policy.](media/access-policy-aad/onboarded-apps-filter.png)

    Select **Edit and preview results** to get a preview of the types of activities that would be returned with your current selection.
5. In the **Actions** area, select one of the following options:

    - **Audit**: Set this action to allow access according to the policy filters you set explicitly.
    - **Block**: Set this action to block access according to the policy filters you set explicitly.
6. In the **Alerts** area, configure any of the following actions as needed:

    - **Create an alert for each matching event with the policy's severity**
    - **Send an alert as email**
    - **Daily alert limit per policy**
    - **Send alerts to Power Automate**
7. When you're done, select **Create**.

## Test your policy

After you've created your access policy, test it by re-authenticating to each app configured in the policy. Verify that your app experience is as expected, and then check your activity logs.

We recommend that you:

- Create a policy for a user you've created specifically for testing.
- Sign out of all existing sessions before re-authenticating to your apps.
- Sign into mobile and desktop apps from both managed and unmanaged devices to ensure that activities are fully captured in the activity log.

Make sure to sign in with a user that matches your policy.

**To test your policy in your app**:

- Visit all pages within the app that are part of a user's work process and verify that the pages render correctly.
- Verify that the behavior and functionality of the app isn't adversely affected by performing common actions such as downloading and uploading files.
- If you're working with custom, non-Microsoft IdP apps, check each of the domains that you've added for your app. For more information, see [Add domains for your app](troubleshooting-proxy#add-domains-for-your-app).

**To check activity logs**:

1. In Microsoft Defender XDR, select **Cloud apps &gt; Activity log**, and check for the sign-in activities captured for each step. You might want to filter by selecting **Advanced filters** and filtering for **Source equals Access control**.

    **Single sign-on log on** activities are Conditional Access app control events.
2. Select an activity to expand for more details. Check to see that the **User agent** tag properly reflects whether the device is a built-in client, either a mobile or desktop app, or the device is a managed device that's compliant and domain-joined.

If you encounter errors or issues, use the **Admin View toolbar** to gather resources such as `.Har` files and recorded sessions, and then file a support ticket.

## Create access policies for identity-managed devices

Use client certificates to control access for devices that aren't Microsoft Entra-hybrid joined and aren't managed by Microsoft Intune. Roll out new certificates to managed devices, or use existing certificates, such as third-party MDM certificates. For example, you might want to deploy client certificate to managed devices and then block access from devices without a certificate.

For more information, see [Identify managed devices with Conditional Access app control](conditional-access-app-control-identity).