---
layout: Conceptual
title: Deploy conditional access app control for any web app using AD FS - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/proxy-idp-adfs
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
description: This article provides information about how to deploy the Microsoft Defender for Cloud Apps conditional access app control for any web app using AD FS as the identity provider.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: aebd7575-11e3-1fcd-6172-b5ed65cd945a
document_version_independent_id: aebd7575-11e3-1fcd-6172-b5ed65cd945a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/proxy-idp-adfs.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: proxy-idp-adfs
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/proxy-idp-adfs.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: bccdc38b-bbd9-9f86-95c1-5cf000735c8a
---

# Deploy conditional access app control for any web app using AD FS - Microsoft Defender for Cloud Apps | Microsoft Learn

You can configure session controls in Microsoft Defender for Cloud Apps to work with any web app and any non-Microsoft IdP. This article describes how to route app sessions from AD FS to Defender for Cloud Apps for real-time session controls.

For this article, we'll use the Salesforce app as an example of a web app being configured to use Defender for Cloud Apps session controls.

## Prerequisites

- Your organization must have the following for conditional access app control:

    - A pre-configured Active Directory Federation Services (AD FS) environment
    - A Microsoft Defender for Cloud Apps license
- An existing AD FS single sign-on setup for the app that uses SAML 2.0

Note

The steps here apply to all versions of AD FS that run on supported version of Windows Server.

## Configure session controls for your app by using AD FS as the IdP

Use the following steps to route your web app sessions from AD FS to Defender for Cloud Apps.

Note

You can configure the app's SAML single sign-on information provided by AD FS using one of the following methods:

- **Option 1**: Uploading the app's SAML metadata file.
- **Option 2**: Manually providing the app's SAML data.

In the following steps, we'll use option 2.

**Step 1: Get your app's SAML single sign-on settings**

**Step 2: Configure Defender for Cloud Apps with your app's SAML information**

**Step 3: Create a new AD FS Relying Party Trust and app single sign-on configuration**.

**Step 4: Configure Defender for Cloud Apps with the AD FS app's information**

**Step 5: Complete the configuration of the AD FS Relying Party Trust**

**Step 6: Get the app changes in Defender for Cloud Apps**

**Step 7: Complete the app changes**

**Step 8: Complete the configuration in Defender for Cloud Apps**

## Step 1: Get your app's SAML single sign-on settings

Use the following steps to collect your app's current SAML single sign-on settings.

1. In Salesforce, browse to **Setup** &gt; **Settings** &gt; **Identity** &gt; **Single Sign-On Settings**.
2. Under **Single Sign-On Settings**, click on the name of your existing AD FS configuration.

    ![Screenshot of Salesforce Single Sign-On Settings page showing the existing AD FS configuration.](media/proxy-idp-adfs/idp-adfs-sf-select-sso-settings.png)
3. On the **SAML Single Sign-On Setting** page, make a note of the Salesforce **Login URL**. You'll need this later when configuring Defender for Cloud Apps.

    Note

    If your app provides a SAML certificate, download the certificate file.

    ![Screenshot of Salesforce SAML Single Sign-On settings page showing the Login URL to copy.](media/proxy-idp-adfs/idp-adfs-sf-copy-saml-sso-login-url.png)

## Step 2: Configure Defender for Cloud Apps with your app's SAML information

Use the following steps to add the app in Defender for Cloud Apps and enter its SAML details.

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**.
2. Under **Connected apps**, select **Conditional Access App Control apps**.
3. Select **+Add**, and in the pop-up, select the app you want to deploy, and then select **Start Wizard**.
4. On the **APP INFORMATION** page, select **Fill in data manually**, in the **Assertion consumer service URL** enter the Salesforce **Login URL** you noted earlier, and then click **Next**.

    Note

    If your app provides a SAML certificate, select **Use &lt;app\_name&gt; SAML certificate** and upload the certificate file.

    ![Screenshot of the Defender for Cloud Apps APP INFORMATION page with fields to manually enter Salesforce SAML details.](media/proxy-idp-adfs/idp-adfs-cas-sf-app-info.png)

## Step 3: Create a new AD FS Relying Party Trust and App Single Sign-On configuration

Note

To limit end-user downtime and preserve your existing known good configuration, we recommend creating a new **Relying Party Trust** and **Single Sign-On configuration**. Where this is not possible, skip the relevant steps. For example, if the app you are configuring does not support creating multiple **Single Sign-On configurations**, then skip the create new single sign-on step.

1. In the **AD FS Management** console, under **Relying Party Trusts**, view the properties of your existing relying party trust for your app, and make note of the settings.
2. Under **Actions**, click **Add Relying Party Trust**. Apart from the **Identifier** value that must be a unique name, configure the new trust using the settings you noted earlier. You'll need this trust later when configuring Defender for Cloud Apps.
3. Open the federation metadata file and make a note of the AD FS **SingleSignOnService Location**. You'll need this later.

    Note

    You can use the following endpoint to access your federation metadata file: `https://<Your_Domain>/federationmetadata/2007-06/federationmetadata.xml`

    ![Screenshot of the federation metadata file showing the AD FS SingleSignOnService location for the Salesforce app.](media/proxy-idp-adfs/idp-adfs-sf-app-copy-saml-sso-service-location.png)
4. Download the identity provider's Signing Certificate. You'll need this later.

    1. Under **Services** &gt; **Certificates**, right-click on the AD FS signing certificate, and then select **View Certificate**.

        ![Screenshot of the identity provider signing certificate properties window in AD FS.](media/proxy-idp-adfs/idp-adfs-view-signing-cert-props.png)
    2. On the certificate's details tab, click **Copy to File** and follow the steps in the **Certificate Export Wizard** to export your certificate as a *Base-64 encoded X.509 (.CER)* file.

        ![Screenshot of the Certificate Export Wizard showing the step to save the IdP signing certificate as a file.](media/proxy-idp-adfs/idp-adfs-save-signing-cert-file.png)
5. Back in Salesforce, on the existing AD FS single sign-on settings page, make a note of all the settings.
6. Create a new SAML single sign-on configuration. Apart from the **Entity ID** value that must match the relying party trust **Identifier**, configure the single sign-on using the settings you noted earlier. You'll need this later when configuring Defender for Cloud Apps.

## Step 4: Configure Defender for Cloud Apps with the AD FS app's information

Use the AD FS values you collected to complete the identity provider configuration in Defender for Cloud Apps.

1. Back in the Defender for Cloud Apps **IDENTITY PROVIDER** page, click **Next** to proceed.
2. On the **IDENTITY PROVIDER** details page, select **Fill in data manually**, do the following, and then click **Next**.

    - For the **Single sign-on service URL**, enter the AD FS **SingleSignOnService Location** you noted from the federation metadata file in Step 3.
    - Select **Upload identity provider's SAML certificate** and upload the certificate file you downloaded earlier.

    ![Screenshot of the Defender for Cloud Apps identity provider page with fields for the SSO service URL and SAML certificate.](media/proxy-idp-adfs/idp-adfs-cas-sf-app-idp-info.png)
3. On the **EXTERNAL CONFIGURATION** page, make a note of the following information, and then click **Next**. You'll need the single sign-on URL and the attributes and values when configuring the AD FS relying party trust and updating the app.

    - Defender for Cloud Apps single sign-on URL
    - Defender for Cloud Apps attributes and values

    Note

    If you see an option to upload the **Defender for Cloud Apps SAML certificate for the identity provider**, click on the link to download the certificate file. You'll need this later.

    ![Screenshot of Defender for Cloud Apps showing the single sign-on URL, attributes, and SAML certificate download link.](media/proxy-idp-adfs/idp-adfs-cas-get-sf-app-external-config.png)

## Step 5: Complete the configuration of the AD FS Relying Party Trust

Complete the following steps to update the AD FS relying party trust with the required claim rules and certificate settings.

1. Back in the **AD FS Management** console, right-click on the relying party trust you created earlier, and then select **Edit Claim Issuance Policy**.

    ![Screenshot of AD FS Management console with the relying party trust context menu showing the Edit Claim Issuance Policy option.](media/proxy-idp-adfs/idp-adfs-sf-relying-trust-edit.png)
2. In the **Edit Claim Issuance Policy** dialog box, under **Issuance Transform Rules**, use the provided information in the following table to complete the steps to create custom rules.

    | Claim rule name | Custom rule |
    | --- | --- |
    | McasSigningCert | `=> issue(type="McasSigningCert", value="<value>");` where `<value>` is the **McasSigningCert** value from the Defender for Cloud Apps wizard you noted earlier |
    | McasAppId | `=> issue(type="McasAppId", value="<value>");` is the **McasAppId** value from the Defender for Cloud Apps wizard you noted earlier |

    1. Click **Add Rule**, under **Claim rule template** select **Send Claims Using a Custom Rule**, and then click **Next**.
    2. On the **Configure Rule** page, enter the respective **Claim rule name** and **Custom rule** provided.

    Note

    These rules are in addition to any claim rules or attributes required by the app you are configuring.
3. Back on the **Relying Party Trust** page, right-click on the relying party trust you created earlier, and then select **Properties**.
4. On the **Endpoints** tab, select **SAML Assertion Consumer Endpoint**, click **Edit** and replace the **Trusted URL** with the Defender for Cloud Apps single sign-on URL you noted earlier, and then click **OK**.

    ![Screenshot of the relying party trust endpoint properties dialog showing the Trusted URL field for the SAML Assertion Consumer Endpoint.](media/proxy-idp-adfs/idp-adfs-sf-relying-trust-endpoint-properties.png)
5. If you downloaded a **Defender for Cloud Apps SAML certificate for the identity provider**, On the **Signature** tab, click **Add** and upload the certificate file, and then click **OK**.

    ![Screenshot of the relying party trust signature properties dialog showing the SAML certificate configuration.](media/proxy-idp-adfs/idp-adfs-sf-relying-trust-signature-properties.png)
6. Save your settings.

## Step 6: Get the app changes in Defender for Cloud Apps

Back in the Defender for Cloud Apps **APP CHANGES** page, do the following, but **don't click Finish**. You'll need the information later.

- Copy the Defender for Cloud Apps SAML Single sign-on URL
- Download the Defender for Cloud Apps SAML certificate

![Screenshot of the Defender for Cloud Apps APP CHANGES page showing the SAML single sign-on URL and certificate download option.](media/proxy-idp-adfs/idp-adfs-cas-sf-app-changes.png)

## Step 7: Complete the app changes

In Salesforce, browse to **Setup** &gt; **Settings** &gt; **Identity** &gt; **Single Sign-On Settings**, and do the following:

1. Recommended: Create a backup of your current settings.
2. Replace the **Identity Provider Login URL** field value with the Defender for Cloud Apps SAML single sign-on URL you noted earlier.
3. Upload the Defender for Cloud Apps SAML certificate you downloaded earlier.
4. Click **Save**.

    Note

    The Defender for Cloud Apps SAML certificate is valid for one year. After it expires, a new certificate will need to be generated.

## Step 8: Complete the configuration in Defender for Cloud Apps

Complete the wizard to enable routing through conditional access app control.

- Back in the Defender for Cloud Apps **APP CHANGES** page, click **Finish**. After completing the wizard, all associated login requests to the configured app will be routed through conditional access app control.