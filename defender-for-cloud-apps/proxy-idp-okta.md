---
layout: Conceptual
title: Deploy conditional access app control for any web app using Okta - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/proxy-idp-okta
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
description: This article provides information about how to deploy the Microsoft Defender for Cloud Apps conditional access app control for any web app using Okta as the identity provider.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: d895e194-9cf1-ea5f-851a-5cf196f4b362
document_version_independent_id: d895e194-9cf1-ea5f-851a-5cf196f4b362
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/proxy-idp-okta.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: proxy-idp-okta
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/proxy-idp-okta.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
platformId: 21a7da00-ed77-d99e-e776-9062c6e65f98
---

# Deploy conditional access app control for any web app using Okta - Microsoft Defender for Cloud Apps | Microsoft Learn

You can configure session controls in Microsoft Defender for Cloud Apps to work with any web app and any non-Microsoft IdP. This article describes how to route app sessions from Okta to Defender for Cloud Apps for real-time session controls.

For this article, we'll use the Salesforce app as an example of a web app being configured to use Defender for Cloud Apps session controls.

## Prerequisites

- Your organization must have the following licenses to use conditional access app control:

    - A pre-configured Okta tenant.
    - Microsoft Defender for Cloud Apps
- An existing Okta single sign-on configuration for the app using the SAML 2.0 authentication protocol

## Configure session controls for your app by using Okta as the IdP

Use the following steps to route your web app sessions from Okta to Defender for Cloud Apps.

Note

You can configure the app's SAML single sign-on information provided by Okta using one of the following methods:

- **Option 1**: Uploading the app's SAML metadata file.
- **Option 2**: Manually providing the app's SAML data.

In the following steps, we'll use option 2.

**Step 1: Get your app's SAML single sign-on settings**

**Step 2: Configure Defender for Cloud Apps with your app's SAML information**

**Step 3: Create a new Okta Custom Application and app single sign-on configuration**

**Step 4: Configure Defender for Cloud Apps with the Okta app's information**

**Step 5: Complete the configuration of the Okta Custom Application**

**Step 6: Get the app changes in Defender for Cloud Apps**

**Step 7: Complete the app changes**

**Step 8: Complete the configuration in Defender for Cloud Apps**

## Step 1: Get your app's SAML single sign-on settings

Collect your app's current SAML single sign-on settings from Salesforce.

1. In Salesforce, browse to **Setup** &gt; **Settings** &gt; **Identity** &gt; **Single Sign-On Settings**.
2. Under **Single Sign-On Settings**, click on the name of your existing Okta configuration.

    ![Screenshot of Salesforce Single Sign-On Settings page showing the existing Okta configuration to select.](media/proxy-idp-okta/idp-okta-sf-select-sso-settings.png)
3. On the **SAML Single Sign-On Setting** page, make a note of the Salesforce **Login URL**. You'll need this later when configuring Defender for Cloud Apps.

    Note

    If your app provides a SAML certificate, download the certificate file.

    ![Screenshot of the Salesforce SAML Single Sign-On Setting page showing the Login URL field.](media/proxy-idp-okta/idp-okta-sf-copy-saml-sso-login-url.png)

## Step 2: Configure Defender for Cloud Apps with your app's SAML information

Enter your app's SAML single sign-on details into Defender for Cloud Apps.

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**.
2. Under **Connected apps**, select **conditional access app control apps**.
3. Select **+Add**, and in the pop-up, select the app you want to deploy, and then select **Start Wizard**.
4. On the **APP INFORMATION** page, select **Fill in data manually**, in the **Assertion consumer service URL** enter the Salesforce **Login URL** from Step 1, and then click **Next**.

    Note

    If your app provides a SAML certificate, select **Use &lt;app\_name&gt; SAML certificate** and upload the certificate file.

    ![Screenshot of the Defender for Cloud Apps APP INFORMATION page with manual SAML configuration fields for Salesforce.](media/proxy-idp-okta/idp-okta-cas-sf-app-info.png)

## Step 3: Create a new Okta Custom Application and App Single Sign-On configuration

Note

To limit end-user downtime and preserve your existing known good configuration, we recommend creating a new **Custom Application** and **Single Sign-On configuration**. If creating a new Custom Application and Single Sign-On configuration is not possible, skip the relevant steps. For example, if the app you are configuring does not support creating multiple **Single Sign-On configurations**, then skip the create new single sign-on step.

1. In the **Okta Admin** console, under **Applications**, view the properties of your existing configuration for your app, and make note of the settings.
2. Click **Add Application**, and then click **Create New App**. Apart from the **Audience URI (SP Entity ID)** value that must be a unique name, configure the new application using the settings from your existing Okta application recorded in the previous step. You'll need this application later when configuring Defender for Cloud Apps.
3. Navigate to **Applications**, view your existing Okta configuration, and on the **Sign On** tab, select **View Setup Instructions**.

    ![Screenshot of the Okta application Sign On tab showing the View Setup Instructions option and SSO service location.](media/proxy-idp-okta/idp-okta-sf-view-setup-instructions.png)
4. Make a note of the **Identity Provider Single Sign-On URL** and download the identity provider's Signing Certificate (X.509). You'll need both the URL and the signing certificate in Step 4 to configure Defender for Cloud Apps.
5. Back in Salesforce, on the existing Okta single sign-on settings page, make a note of all the settings.
6. Create a new SAML single sign-on configuration. Apart from the **Entity ID** value that must match the custom application's **Audience URI (SP Entity ID)**, configure the single sign-on using the settings from the existing Okta single sign-on settings page noted in the previous step. You'll need this new configuration later when configuring Defender for Cloud Apps.
7. After saving your new application, navigate to **Assignments** page and assign the **People** or **Groups** that require access to the application.

ׂ

## Step 4: Configure Defender for Cloud Apps with the Okta app's information

Provide Defender for Cloud Apps with your Okta identity provider details.

1. In Defender for Cloud Apps, on the **IDENTITY PROVIDER** page, click **Next** to proceed.
2. On the next page of the **IDENTITY PROVIDER** wizard, select **Fill in data manually**, do the following, and then click **Next**.

    - For the **Single sign-on service URL**, enter the Salesforce **Login URL** you noted earlier.
    - Select **Upload identity provider's SAML certificate** and upload the certificate file you downloaded earlier.

    ![Screenshot of Defender for Cloud Apps identity provider settings showing the SSO service URL and SAML certificate upload fields.](media/proxy-idp-okta/idp-okta-cas-sf-app-idp-info.png)
3. On the **External Configuration** page, make a note of the following information, and then click **Next**. You'll need the Defender for Cloud Apps single sign-on URL and attribute values when configuring the Okta custom application in Step 5.

    - Defender for Cloud Apps single sign-on URL
    - Defender for Cloud Apps attributes and values

    Note

    If you see an option to upload the **Defender for Cloud Apps SAML certificate for the identity provider**, click the download link to download the certificate file. You'll need this certificate file in Step 5 to configure the Okta custom application.

    ![Screenshot of the Defender for Cloud Apps configuration page showing the SSO URL and attribute values.](media/proxy-idp-okta/idp-okta-cas-get-sf-app-external-config.png)

## Step 5: Complete the configuration of the Okta Custom Application

Update the custom Okta application's SAML settings with the values from Defender for Cloud Apps.

1. Back in the **Okta Admin** console, under **Applications**, select the custom application you created earlier, and then under **General** &gt; **SAML Settings**, click **Edit**.

    ![Screenshot of the Okta Admin console showing the custom application General tab with SAML Settings and the Edit option.](media/proxy-idp-okta/idp-okta-sf-saml-settings-edit.png)
2. In the **Single Sign On URL** field, replace the URL with the Defender for Cloud Apps single sign-on URL from Step 4, and then save your settings.
3. Under **Directory**, select **Profile Editor**, select the custom application you created earlier, and then click **Profile**. Add attributes using the following information.

    | Display name | Variable name | Data type | Attribute type |
    | --- | --- | --- | --- |
    | McasSigningCert | McasSigningCert | string | Custom |
    | McasAppId | McasAppId | string | Custom |

    ![Screenshot of the Okta Profile Editor showing fields for adding custom profile attributes.](media/proxy-idp-okta/idp-okta-sf-add-profile-attributes-edit.png)
4. Back on the **Profile Editor** page, select the custom application you created earlier, click **Mappings**, and then select **Okta User to {custom\_app\_name}**. Map the **McasSigningCert** and **McasAppId** attributes to the Defender for Cloud Apps attribute values recorded in Step 4.

    Note

    - Make sure you enclose the values in double quotes (")
    - Okta limits attributes to 1024 characters. To mitigate this limitation, add the attributes using the **Profile Editor** as described.

    ![Screenshot of the Okta attribute mappings page showing mappings for McasSigningCert and McasAppId.](media/proxy-idp-okta/idp-okta-sf-map-profile-attributes-edit.png)
5. Save your settings.

## Step 6: Get the app changes in Defender for Cloud Apps

Back in the Defender for Cloud Apps **APP CHANGES** page, do the following, but **don't click Finish**. You'll need the SAML single sign-on URL and certificate in Step 7.

- Copy the Defender for Cloud Apps SAML Single sign-on URL
- Download the Defender for Cloud Apps SAML certificate

![Screenshot of the Defender for Cloud Apps APP CHANGES page showing the SAML SSO URL and certificate download option.](media/proxy-idp-okta/idp-okta-cas-sf-app-changes.png)

## Step 7: Complete the app changes

In Salesforce, browse to **Setup** &gt; **Settings** &gt; **Identity** &gt; **Single Sign-On Settings**, and do the following:

1. [Recommended] Create a backup of your current settings.
2. Replace the **Identity Provider Login URL** field value with the Defender for Cloud Apps SAML single sign-on URL copied in Step 6.
3. Upload the Defender for Cloud Apps SAML certificate downloaded in Step 6.
4. Click **Save**.

    Note

    - After saving your settings, all associated login requests to this app will be routed through conditional access app control.
    - The Defender for Cloud Apps SAML certificate is valid for one year. After it expires, a new certificate will need to be generated.

    ![Screenshot of the Salesforce Single Sign-On Settings page showing the updated SSO configuration fields.](media/proxy-idp-okta/idp-okta-sf-update-sso-settings.png)

## Step 8: Complete the configuration in Defender for Cloud Apps

Finalize the wizard in Defender for Cloud Apps to activate session routing through conditional access app control.

- Back in the Defender for Cloud Apps **APP CHANGES** page, click **Finish**. After completing the wizard, all associated login requests to this app will be routed through conditional access app control.