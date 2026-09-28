---
layout: Conceptual
title: Manual onboarding of apps using Microsoft Entra ID - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/apps-manual-onboarding-with-microsoft-entra-id
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: damalkaw
manager: bagol
ms.author: damalkaw
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: Learn how to onboard and deploy custom line-of-business apps, non-featured SaaS apps, and on-premises apps hosted via the Microsoft Entra ID Application Proxy with session controls.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: d06d511e-bb80-3000-8fc4-bec5945b9d1f
document_version_independent_id: d06d511e-bb80-3000-8fc4-bec5945b9d1f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/apps-manual-onboarding-with-microsoft-entra-id.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: apps-manual-onboarding-with-microsoft-entra-id
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/apps-manual-onboarding-with-microsoft-entra-id.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 2a16c6ac-b495-b14f-c8f3-7451b3bf89ca
---

# Manual onboarding of apps using Microsoft Entra ID - Microsoft Defender for Cloud Apps | Microsoft Learn

Note

Microsoft Defender for Cloud Apps is now part of [Microsoft Defender XDR](https://security.microsoft.com), which correlates signals from across the Microsoft Defender suite and provides incident-level detection, investigation, and powerful response capabilities. For more information, see [Microsoft Defender for Cloud Apps in Microsoft Defender XDR](/en-us/microsoft-365/security/defender/microsoft-365-security-center-defender-cloud-apps).

Session controls in Microsoft Defender for Cloud Apps can be configured to work with any web apps. This article describes how to onboard and deploy custom line-of-business apps, non-featured SaaS apps, and on-premises apps hosted via the Microsoft Entra ID Application Proxy with session controls. It provides steps to create a Microsoft Entra ID Conditional Access policy that routes app sessions to Defender for Cloud Apps. For other IdP solutions, see [Deploy conditional access app control for custom apps with non-Microsoft IdP](proxy-deployment-any-app-idp).

## Prerequisites

Before you begin, make sure you have the required licenses, administrative access, and app configuration in place.

### Add admins to the app onboarding/maintenance list

To add admins to the app onboarding/maintenance list, perform the following steps:

1. In the menu bar of Defender for Cloud Apps, select the settings cog and select **Settings**.
2. Under **Conditional Access App Control**, select **App onboarding/maintenance**.
3. Enter the user principal name or email for the users that will be onboarding the app, and then select **Save**.

    ![Screenshot of the App onboarding and maintenance settings page in Defender for Cloud Apps, showing the user principal name input field.](media/app-onboarding-settings.png)

### Check for necessary licenses

- Your organization must have the following licenses to use conditional access app control:

    - [Microsoft Entra ID Premium P1](/en-us/azure/active-directory/license-users-groups) or higher
    - Microsoft Defender for Cloud Apps
- Apps must be configured with single sign-on
- Apps must use one of the following authentication protocols:

    | IdP | Protocols |
    | --- | --- |
    | Microsoft Entra ID | SAML 2.0 or OpenID Connect |

### Check for pre-onboarded apps

Before you onboard your apps, make sure that each app isn't already included in the following list of pre-onboarded apps for both access and session controls:

- AWS
- Box
- Concur
- CornerStone on Demand
- DocuSign
- Dropbox
- Egnyte
- GitHub
- Google Workspace
- HighQ
- JIRA/Confluence
- LinkedIn Learning
- Microsoft Azure DevOps (Visual Studio Team Services)
- Microsoft Azure portal
- Microsoft Dynamics 365 CRM
- Microsoft Exchange Online
- Microsoft OneDrive
- Microsoft Power BI
- Microsoft SharePoint Online
- Microsoft Teams
- Microsoft Yammer
- Salesforce
- ServiceNow
- Slack
- Tableau
- Workday
- Workiva
- Workplace by Facebook

To use pre-onboarded apps with Defender for Cloud Apps, you must route the app to access and session controls and perform an initial sign-in.

## Deploy an app with conditional access app control

Follow these steps to configure any app to be controlled by Defender for Cloud Apps conditional access app control.

1. **Configure your Microsoft Entra ID to work with Defender for Cloud Apps**
2. **Configure the app that you are deploying**
3. **Verify that the app is working correctly**
4. **Enable the app for use in your organization**
5. **Update the Microsoft Entra ID policy**

Note

To deploy conditional access app control for Microsoft Entra ID apps, you need a valid [license for Microsoft Entra ID Premium P1 or higher](/en-us/azure/active-directory/fundamentals/license-users-groups) as well as a Defender for Cloud Apps license.

## Step 1: Configure Microsoft Entra ID to work with Defender for Cloud Apps

Note

When configuring an application with SSO in Microsoft Entra ID, or other identity providers, one field that may be listed as optional is the sign-on URL setting. Note that this field may be required for conditional access app control to work.

1. In Microsoft Entra ID, browse to **Security** &gt; **Conditional Access**.
2. On the **Conditional Access** pane, in the toolbar at the top, select **New policy**.
3. On the **New** pane, in the **Name** textbox, enter the policy name.
4. Under **Assignments**, select **Users and groups**, assign the users that will be onboarding (initial sign-on and verification) the app, and then select **Done**.
5. Under **Assignments**, select **Cloud apps**, assign the apps you want to control with conditional access app control, and then select **Done**.
6. Under **Access controls**, select **Session**, select **Use Conditional Access App Control**, and choose a built-in policy (**Monitor only** or **Block downloads**) or **Use custom policy** to set an advanced policy in Defender for Cloud Apps, and then click **Select**.

    ![Screenshot of the Microsoft Entra ID Conditional Access policy page with session controls configured for Conditional Access App Control.](media/azure-ad-caac-policy.png)
7. Optionally, add conditions and grant controls as required.
8. Set **Enable policy** to **On** and then select **Create**.

## Step 2: Add the app manually and install certificates, if necessary

Applications in the app catalog are automatically populated into the Connected Apps table on the Conditional Access App Control page. Check that the app you want to deploy is recognized in the Connected Apps table.

1. In the menu bar of Defender for Cloud Apps, select the settings cog, and select the **Conditional Access App Control** tab to access a table of applications that can be configured with access and session policies.

    ![Screenshot of the Conditional Access App Control apps page listing connected apps that can be configured with access and session policies.](media/conditional-access-app-control-apps.png)
2. Select the **App: Select apps…** dropdown menu to filter and search for the app you want to deploy.

    ![Screenshot of the Select an app dialog used to filter and search for an application to deploy.](media/select-apps.png)
3. If you don't see the app in the Conditional Access App Control apps table, you'll have to add the app manually.

### How to manually add an unidentified app

If your app doesn't appear in the Conditional Access App Control apps table, use the following steps to manually add it:

1. In the banner, select **View new apps**.

    ![Screenshot of the Conditional Access App Control page showing newly discovered apps available for onboarding.](media/caac-view-apps.png)
2. In the list of new apps, for each app that you're onboarding, select the **+** sign, and then select **Add**.

    Note

    If an app does not appear in the Defender for Cloud Apps app catalog, it will appear in the dialog under unidentified apps along with the login URL. When you click the + sign for these apps, you can onboard the application as a custom app.

    ![Screenshot of the Conditional Access App Control page listing discovered Microsoft Entra ID apps available for onboarding as custom apps.](media/caac-discovered-aad-apps.png)

### To add domains for an app

Associating the correct domains to an app allows Defender for Cloud Apps to enforce policies and audit activities.

For example, if you've configured a policy that blocks downloading files for an associated domain, file downloads by the app from the associated domain will be blocked. However, file downloads by the app from domains not associated with the app won't be blocked and the download won't be audited in the activity log.

Note

Defender for Cloud Apps still adds a suffix to domains not associated with the app to ensure a seamless user experience.

1. From within the app, on the Defender for Cloud Apps admin toolbar, select **Discovered domains**. 
    Note

    The admin toolbar is only visible to users with permissions to onboard or maintenance apps.
2. In the Discovered domains panel, make a note of domain names or export the list as a .csv file. 
    Note

    The panel displays a list of discovered domains that are not associated in the app. The domain names are fully qualified.
3. Go to Defender for Cloud Apps, in the menu bar, select the settings cog and select **Conditional Access App Control**.
4. In the list of apps, on the row in which the app you're deploying appears, choose the three dots at the end of the row, and then under **APP DETAILS**, choose **Edit**. 
    Tip

    To view the list of domains configured in the app, select **View app domains**.
5. In **User-defined domains**, enter all the domains you want to associate with this app, and then select **Save**. 
    Note

    You can use the \* wildcard character as a placeholder for any character. When adding domains, decide whether you want to add specific domains (`sub1.contoso.com`,`sub2.contoso.com`) or multiple domains (`*.contoso.com`).

### Install root certificates

Install the required root certificates by completing the following steps:

1. Repeat the following steps for each certificate to install the **Current CA** and **Next CA** self-signed root certificates from the Defender for Cloud Apps certificate page.

    1. Select the certificate.
    2. Select **Open**, and when prompted select **Open** again.
    3. Select **Install certificate**.
    4. Choose either **Current User** or **Local Machine**.
    5. Select **Place all certificates in the following store** and then select **Browse**.
    6. Select **Trusted Root Certificate Authorities** and then select **OK**.
    7. Select **Finish**.

    Note

    For the certificates to be recognized, once you have installed the certificate, you must restart the browser and go to the same page.
2. On the Defender for Cloud Apps certificate page, select **Continue**.
3. Check that the application is available in the Conditional Access App Control apps table.

## Step 3: Verify that the app is working correctly

To verify that the application is being proxied, first perform either a hard sign-out of browsers associated with the application or open a new browser with incognito mode.

Open the application and perform the following checks:

- Check that the URL contains the `.mcas` suffix
- Visit all pages within the app that are part of a user's work process and verify that the pages render correctly.
- Verify that the behavior and functionality of the app isn't adversely affected by performing common actions such as downloading and uploading files.
- Review the list of domains associated with the app. For more information, see Add the domains for the app.

If you encounter errors or issues, use the admin toolbar to gather resources such as `.har` files and recorded sessions for filing a support ticket.

## Step 4: Enable the app for use in your organization

Once you're ready to enable the app for use in your organization's production environment, do the following steps.

1. In Defender for Cloud Apps, select the settings cog, and then select **Conditional Access App Control**.
2. In the list of apps, on the row in which the app you're deploying appears, choose the three dots at the end of the row, and then choose **Edit app**.
3. Select **Use with Conditional Access App Control** and then select **Save**.

## Step 5: Update the Microsoft Entra ID policy

Update the Microsoft Entra ID Conditional Access policy to apply to your production environment:

1. In Microsoft Entra ID, under **Security**, select **Conditional Access**.
2. Update the Conditional Access policy you created in Step 1 to include the relevant users, groups, and controls you require.
3. Under **Session** &gt; **Use Conditional Access App Control**, if you selected **Use Custom Policy**, go to Defender for Cloud Apps and create a corresponding session policy. For more information, see [Session policies](session-policy-aad).