---
layout: Conceptual
title: Deploy conditional access app control for any web app using PingOne - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/proxy-idp-pingone
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
description: This article provides information about how to deploy the Microsoft Defender for Cloud Apps conditional access app control for any web app using the PingOne identity provider.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: d141213a-05fe-455d-10b6-d3f4a775c32a
document_version_independent_id: d141213a-05fe-455d-10b6-d3f4a775c32a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/proxy-idp-pingone.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: proxy-idp-pingone
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/proxy-idp-pingone.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/7ebba99b-05c3-4387-8883-f7bbf6632cb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/006ab567-b18c-4cf1-9a25-c24daa46ede1
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
platformId: 940034df-3f2d-912b-ce60-42a53bfa0869
---

# Deploy conditional access app control for any web app using PingOne - Microsoft Defender for Cloud Apps | Microsoft Learn

You can configure session controls in Microsoft Defender for Cloud Apps to work with any web app and any non-Microsoft IdP. This article describes how to route app sessions from PingOne to Defender for Cloud Apps for real-time session controls.

For this article, we'll use the Salesforce app as an example of a web app being configured to use Defender for Cloud Apps session controls. To configure other apps, perform the same steps according to their requirements.

## Prerequisites

- Your organization must have the following licenses to use conditional access app control:

    - A relevant PingOne license (required for single sign-on)
    - Microsoft Defender for Cloud Apps
- An existing PingOne single sign-on configuration for the app using the SAML 2.0 authentication protocol

## Configure session controls for your app by using PingOne as the IdP

Use the following steps to route your web app sessions from PingOne to Defender for Cloud Apps.

Note

You can configure the app's SAML single sign-on information provided by PingOne using one of the following methods:

- **Option 1**: Uploading the app's SAML metadata file.
- **Option 2**: Manually providing the app's SAML data.

In the following steps, we'll use option 2.

**Step 1: Get your app's SAML single sign-on settings**

**Step 2: Configure Defender for Cloud Apps with your app's SAML information**

**Step 3: Create a custom app in PingOne**

**Step 4: Configure Defender for Cloud Apps with the PingOne app's information**

**Step 5: Complete the custom app in PingOne**

**Step 6: Get the app changes in Defender for Cloud Apps**

**Step 7: Complete the app changes**

**Step 8: Complete the configuration in Defender for Cloud Apps**

## Step 1: Get your app's SAML single sign-on settings

Use the following steps to locate your app's existing SAML single sign-on settings in Salesforce.

1. In Salesforce, browse to **Setup** &gt; **Settings** &gt; **Identity** &gt; **Single Sign-On Settings**.
2. Under **Single Sign-On Settings**, select the name of your existing SAML 2.0 configuration.

    ![Screenshot of the Salesforce Single Sign-On Settings page with the SAML 2.0 configuration selected.](media/proxy-idp-pingone/idp-pingone-sf-select-sso-settings.png)
3. On the **SAML Single Sign-On Setting** page, make a note of the Salesforce **Login URL**. You'll need this later.

    Note

    If your app provides a SAML certificate, download the certificate file.

    ![Screenshot of the Salesforce SAML Single Sign-On Setting page showing the Login URL.](media/proxy-idp-pingone/idp-pingone-sf-copy-saml-sso-login-url.png)

## Step 2: Configure Defender for Cloud Apps with your app's SAML information

Use the following steps to add your app's SAML information to Defender for Cloud Apps.

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**.
2. Under **Connected apps**, select **Conditional Access App Control apps**.
3. Select **+Add**, and in the pop-up, select the app you want to deploy, and then select **Start Wizard**.
4. On the **APP INFORMATION** page, select **Fill in data manually**, in the **Assertion consumer service URL** enter the Salesforce **Login URL** you noted earlier, and then select **Next**.

    Note

    If your app provides a SAML certificate, select **Use &lt;app\_name&gt; SAML certificate** and upload the certificate file.

    ![Screenshot of the APP INFORMATION page with manual SAML configuration for the Salesforce app.](media/proxy-idp-pingone/idp-pingone-cas-sf-app-info.png)

## Step 3: Create a custom app in PingOne

Before you proceed, use the following steps to get information from your existing Salesforce app.

1. In PingOne, edit your existing Salesforce app.
2. On the **SSO Attribute Mapping** page, make a note of the SAML\_SUBJECT attribute and value, and then download the **Signing Certificate** and **SAML Metadata** files.

    ![Screenshot of the existing Salesforce app SSO Attribute Mapping page showing attributes to copy.](media/proxy-idp-pingone/idp-pingone-sf-app-copy-saml-sso-attributes.png)
3. Open the SAML metadata file and make a note of the PingOne **SingleSignOnService Location**. You'll need this later.

    ![Screenshot of the existing Salesforce app SAML metadata showing the SingleSignOnService Location value.](media/proxy-idp-pingone/idp-pingone-sf-app-copy-saml-sso-service-location.png)
4. On the **Group Access** page, make a note of the assigned groups.

    ![Screenshot of the existing Salesforce app Group Access page showing the assigned groups.](media/proxy-idp-pingone/idp-pingone-sf-app-copy-saml-sso-user-groups.png)

Then use the instructions from the **Add a SAML application with your identity provider** page to configure a custom app in your IdP's portal.

![Screenshot of the identity provider setup page for adding a SAML application manually.](media/proxy-deploy-add-idp-get-conf.png)

Note

Configuring a custom app enables you to test the existing app with access and session controls without changing the current behavior for your organization.

1. Create a **New SAML Application**.

    ![Screenshot of the PingOne page for creating a new custom Salesforce SAML application.](media/proxy-idp-pingone/idp-pingone-sf-custom-app-new.png)
2. On the **Application Details** page, fill out the form, and then select **Continue to Next Step**.

    Tip

    Use an app name that will help you to differentiate between the custom app and the existing Salesforce app.

    ![Screenshot of the custom Salesforce app Application Details form in PingOne.](media/proxy-idp-pingone/idp-pingone-sf-custom-app-details.png)
3. On the **Application Configuration** page, do the following, and then select **Continue to Next Step**.

    - In the **Assertion Consumer Service (ACS)** field, enter the Salesforce **Login URL** you noted earlier.
    - In the **Entity ID** field, enter a unique ID starting with `https://`. Make sure this is different from the exiting Salesforce PingOne app's configuration.
    - Make a note of the **Entity ID**. You'll need this later.

    ![Screenshot of the custom Salesforce app Application Configuration page with SAML details entered.](media/proxy-idp-pingone/idp-pingone-sf-custom-app-set-saml-sso-properties.png)
4. On the **SSO Attribute Mapping** page, add the existing Salesforce app's **SAML\_SUBJECT** attribute and value you noted earlier, and then select **Continue to Next Step**.

    ![Screenshot of the custom Salesforce app SSO Attribute Mapping page with attributes being added.](media/proxy-idp-pingone/idp-pingone-sf-custom-app-set-saml-sso-attributes.png)
5. On the **Group Access** page, add the existing Salesforce app's groups you noted earlier, and complete the configuration.

    ![Screenshot of the custom Salesforce app Group Access page with groups assigned in PingOne.](media/proxy-idp-pingone/idp-pingone-sf-custom-app-set-saml-sso-user-groups.png)

## Step 4: Configure Defender for Cloud Apps with the PingOne app's information

Use the following steps to enter the PingOne app details in Defender for Cloud Apps.

1. Back in the Defender for Cloud Apps **IDENTITY PROVIDER** page, select **Next** to proceed.
2. On the next page, select **Fill in data manually**, do the following, and then select **Next**.

    - For the **Assertion consumer service URL**, enter the Salesforce **Login URL** you noted earlier.
    - Select **Upload identity provider's SAML certificate** and upload the certificate file you downloaded earlier.

    ![Screenshot of the Defender for Cloud Apps identity provider page showing the SSO service URL and SAML certificate fields.](media/proxy-idp-pingone/idp-pingone-cas-sf-app-idp-info.png)
3. On the next page, make a note of the following information, and then select **Next**. You'll need the information later.

    - Defender for Cloud Apps single sign-on URL
    - Defender for Cloud Apps attributes and values

    ![Screenshot of the Defender for Cloud Apps page showing the SSO URL and SAML attributes to copy.](media/proxy-idp-pingone/idp-pingone-cas-get-sf-app-external-config.png)

## Step 5: Complete the custom app in PingOne

Use the following steps to finalize the custom app configuration in PingOne.

1. In PingOne, locate and edit the custom Salesforce app.

    ![Screenshot of the PingOne app list with the custom Salesforce app selected for editing.](media/proxy-idp-pingone/idp-pingone-sf-custom-app-edit.png)
2. In the **Assertion Consumer Service (ACS)** field, replace the URL with the Defender for Cloud Apps single sign-on URL you noted earlier, and then select **Next**.

    ![Screenshot of the custom Salesforce app SAML settings with the ACS URL replaced.](media/proxy-idp-pingone/idp-pingone-sf-custom-app-replace-saml-sso-properties.png)
3. Add the Defender for Cloud Apps attributes and values you noted earlier to the app's properties.

    ![Screenshot of the custom Salesforce app attribute mapping with Defender for Cloud Apps attributes added.](media/proxy-idp-pingone/idp-pingone-sf-custom-app-replace-saml-sso-attributes.png)
4. Save your settings.

## Step 6: Get the app changes in Defender for Cloud Apps

In the Defender for Cloud Apps wizard, on the **APP CHANGES** page, do the following, but **don't select Finish**. You'll need the information later.

- Copy the Defender for Cloud Apps SAML Single sign-on URL
- Download the Defender for Cloud Apps SAML certificate

![Screenshot of the Defender for Cloud Apps APP CHANGES page showing the SAML SSO URL and certificate download option.](media/proxy-idp-pingone/idp-pingone-cas-sf-app-changes.png)

## Step 7: Complete the app changes

In Salesforce, browse to **Setup** &gt; **Settings** &gt; **Identity** &gt; **Single Sign-On Settings**, and do the following:

1. Recommended: Create a backup of your current settings.
2. Replace the **Identity Provider Login URL** field value with the Defender for Cloud Apps SAML single sign-on URL you noted earlier.

    Note

    The Defender for Cloud Apps SAML certificate is valid for one year. After it expires, a new certificate will need to be generated.
3. Upload the Defender for Cloud Apps SAML certificate you downloaded earlier.
4. Replace the **Entity ID** field value with the PingOne custom app Entity ID you noted earlier.
5. Select **Save**.

    Note

    The Defender for Cloud Apps SAML certificate is valid for one year. After it expires, a new certificate will need to be generated.

    ![Screenshot of the Salesforce SSO settings updated with Defender for Cloud Apps SAML details.](media/proxy-idp-pingone/idp-pingone-sf-custom-app-changes.png)

## Step 8: Complete the configuration in Defender for Cloud Apps

Complete the final step in the Defender for Cloud Apps wizard to finish the configuration.

- In Defender for Cloud Apps, return to the **APP CHANGES** page, and then select **Finish**. After completing the wizard, all associated login requests to this app will be routed through conditional access app control.