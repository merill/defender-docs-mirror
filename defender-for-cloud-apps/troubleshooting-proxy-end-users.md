---
layout: Conceptual
title: Troubleshooting access and session controls for end-users - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/troubleshooting-proxy-end-users
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
description: This article describes how to troubleshoot common access and session control issues experienced by end-users with Microsoft Defender for Cloud Apps.
ms.date: 2024-05-15T00:00:00.0000000Z
ms.topic: troubleshooting
ms.custom: sfi-image-nochange
locale: en-us
document_id: d2bb8ce0-279a-d905-0599-2aa716f74db4
document_version_independent_id: d2bb8ce0-279a-d905-0599-2aa716f74db4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/troubleshooting-proxy-end-users.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: troubleshooting-proxy-end-users
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/troubleshooting-proxy-end-users.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 2653eb43-3b5d-7915-6a6e-ce679b016a50
---

# Troubleshooting access and session controls for end-users - Microsoft Defender for Cloud Apps | Microsoft Learn

This article provides Microsoft Defender for Cloud Apps admins with guidance on how to investigate and resolve common access and session control issues as experienced by end-users.

## Check minimum requirements

Before you start troubleshooting, make sure your environment meets the following minimum general requirements for access and session controls.

| Requirement | Description |
| --- | --- |
| **Licensing** | Make sure you have a valid [license](https://aka.ms/M365EnterprisePlans) for Microsoft Defender for Cloud Apps. |
| **Single Sign-On (SSO)** | Apps must be configured with one of the supported single sign-on (SSO) solutions:  - Microsoft Entra ID using SAML 2.0 or OpenID Connect 2.0 - Non-Microsoft IdP using SAML 2.0 |
| **Browser support** | Session controls are available for browser-based sessions on the latest versions of the following browsers: - Microsoft Edge- Google Chrome- Mozilla Firefox- Apple Safari In-browser protection for Microsoft Edge also has specific requirements, including the user signed in with their work profile. For more information, see [In-browser protection requirements](in-browser-protection#in-browser-protection-requirements). |
| **Downtime** | Defender for Cloud Apps allows you to define the default behavior to apply if there's a service disruption, such as a component not functioning correctly. For example, you might choose to harden (block) or bypass (allow) users from taking actions on potentially sensitive content when the normal policy controls can't be enforced. To configure the default behavior during system downtime, in Microsoft Defender XDR, go to **Settings** &gt; **Conditional Access App Control** &gt; **Default behavior** &gt; **Allow** or **Block** access. |

## User monitoring page isn't appearing

When routing a user through the Defender for Cloud Apps, you can notify the user that their session is monitored. By default, the user monitoring page is enabled.

This section describes the troubleshooting steps we recommend you taking if the user monitoring page is enabled but doesn't appear as expected.

**Recommended steps**

1. In the Microsoft Defender Portal, select **Settings** &gt; **Cloud Apps**.
2. Under **conditional access app control**, select **User monitoring**. This page shows the user monitoring options available in Defender for Cloud Apps. For example:

    ![Screenshot of the user monitoring options.](media/proxy-user-monitoring.png)
3. Verify that the **Notify users that their activity is being monitored** option is selected.
4. Select whether you want to use the default message or provide a custom message:

    | Message type | Details |
    | --- | --- |
    | **Default** | **Header**:Access to [App Name Will Appear Here] is monitored**Body**:For improved security, your organization allows access to [App Name Will Appear Here] in monitor mode. Access is only available from a web browser. |
    | **Custom** | **Header**:Use this box to provide a custom heading to inform users they're being monitored.**Body**:Use this box to add other custom information for the user, such as who to contact with questions, and supports the following inputs: plain text, rich text, hyperlinks. |
5. Select **Preview** to verify the user monitoring page that appears before accessing an app.
6. Select **Save**.

## Not able to access app from a non-Microsoft Identity Provider

If an end user receives a general failure after signing into an app from a non-Microsoft Identity Provider, validate the non-Microsoft IdP configuration.

**Recommended steps**

1. In the Microsoft Defender Portal, select **Settings** &gt; **Cloud Apps**.
2. Under **Connected apps**, select **Conditional Access App Control apps**.
3. In the list of apps, on the row in which the app you can't access appears, select the three dots at the end of the row, and then select **Edit app**.
4. Validate that the SAML certificate that was uploaded is correct.

    1. Verify that valid SSO URLs are provided in the app configuration.
    2. Validate that the attributes and values in the custom app are reflected in identity provider settings.

    For example:

    ![Screenshot of the SAML information page.](media/proxy-deploy-add-idp-ext-conf.png).
5. If you still can't access the app, open a [support ticket](/en-us/defender-xdr/contact-defender-support).

## Something Went Wrong page appears

Sometimes during a proxied session, the **Something Went Wrong** page might appear. This can happen when:

- A user logs in after being idle for a while
- Refreshing the browser and the page load takes longer than expected
- The non-Microsoft IdP app isn't configured correctly

**Recommended steps**

1. If the end user is trying to access an app that is configured using a non-Microsoft IdP, see Not able to access app from a non-Microsoft IdP and [App status: Continue Setup](troubleshooting-proxy#app-status-continue-setup).
2. If the end user unexpectedly reached this page, do the following:

    1. Restart your browser session.
    2. Clear history, cookies, and cache from the browser.

## Clipboard actions or file controls aren't being blocked

The ability to block clipboard actions such as cut, copy, paste, and file controls such as download, upload, and print is required to prevent data exfiltration and infiltration scenarios.

This ability enables companies to balance security and productivity for end users. If you're experiencing problems with these features, use the following steps to investigate the issue.

**Recommended steps**

If the session is being proxied, use the following steps to verify the policy:

1. In the Microsoft Defender Portal, under **Cloud Apps**, select **Activity log**.
2. Use the advanced filter, select **Applied action** and set its value equal to **Blocked**.
3. Verify that there are blocked file activities:

    1. If there's an activity, expand the activity drawer by clicking on the activity.
    2. On the activity drawer's **General** tab, select the matched policies link, to verify the policy you enforced is present.
    3. If you don't see your policy, see [Issues when creating access and session policies](troubleshooting-proxy#issues-when-creating-access-and-session-policies).
    4. If you see **Access blocked/allowed due to Default Behavior**, this indicates that the system was down, and the default behavior was applied.

        1. To change the default behavior, in the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Then under **Conditional Access App Control**, select **Default Behavior**, and set the default behavior to **Allow** or **Block** access.
        2. Go to the [Microsoft 365 admin portal](https://admin.microsoft.com/AdminPortal/Home?#/servicehealth) and monitor notifications about system downtime.
4. If you still not able to see blocked activity, open a [support ticket](/en-us/defender-xdr/contact-defender-support).

## Downloads aren't being protected

As an end user, downloading sensitive data on an unmanaged device might be necessary. In these scenarios, you can protect documents with Microsoft Purview Information Protection.

If the end user can't successfully encrypt the document, use the following steps to investigate the issue.

**Recommended steps**

1. In the Microsoft Defender Portal, under **Cloud Apps**, select **Activity log**.
2. Use the advanced filter, select **Applied action** and set its value equal to **Protected**.
3. Verify that there are blocked file activities:

    1. If there's an activity, expand the activity drawer by clicking on the activity
    2. On the activity drawer's **General** tab, select the matched policies link, to verify the policy you enforced is present.
    3. If you don't see your policy, see [Issues when creating access and session policies](troubleshooting-proxy#issues-when-creating-access-and-session-policies).
    4. If you see **Access blocked/allowed due to Default Behavior**, this indicates that the system was down, and the default behavior was applied.

        1. To change the default behavior, in the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Then under **Conditional Access App Control**, select **Default Behavior**, and set the default behavior to **Allow** or **Block** access.
        2. Go to the [Microsoft 365 Service Health Dashboard](/en-us/microsoft-365/admin/manage/health-dashboard-overview) and monitor notifications about system downtime.
    5. If you're protecting the file with a sensitivity label or custom permissions, in the **Activity description**, make sure the file extension is one of the following supported file types:

        - **Word**: docm, docx, dotm, dotx
        - **Excel**: xlam, xlsm, xlsx, xltx
        - **PowerPoint**: potm, potx, ppsx, ppsm, pptm, pptx
        - **PDF** if Unified Labeling is enabled

    If the file type isn't supported, in the session policy, you can select **Block download of any file that in unsupported by native protection or where native protection is unsuccessful**.
4. If you still not able to see blocked activity, open a [support ticket](/en-us/defender-xdr/contact-defender-support).

## Navigating to a particular URL of a suffixed app and landing on a generic page

In some scenarios, navigating to a link might result in the user landing on the app's home page rather than the full path of the link.

Tip

Defender for Cloud Apps maintains a list of apps that are known to suffer from context loss. For more information, see [Context loss limitations](caac-known-issues#context-loss-limitations).

**Recommended steps**

If you're using a browser other than Microsoft Edge and a user lands on the app's home page instead of the full path of the link, resolve the issue by appending `.mcas.ms` to the original URL.

For example, if the original URL is:

`https://www.github.com/organization/threads/threadnumber`, change it to `https://www.github.com.mcas.ms/organization/threads/threadnumber`

Microsoft Edge users benefit from in-browser protection, aren't redirected to a reverse proxy, and shouldn't need the `.mcas.ms` suffix added. For apps experiencing context loss, open a [support ticket](/en-us/defender-xdr/contact-defender-support).

## Blocking downloads cause PDF previews to be blocked

Occasionally, when you preview or print PDF files, apps initiate a download of the file. This causes Defender for Cloud Apps to intervene to ensure the download is blocked and that data isn't leaked from your environment.

For example, if you created a session policy to block downloads for Outlook Web Access (OWA), then previewing or printing PDF files might be blocked, with a message like this:

![Screenshot of a Download blocked message.](media/before-powershell.png)

To allow the preview, an Exchange administrator should perform the following steps:

1. Download the [Exchange Online PowerShell Module](https://www.powershellgallery.com/packages/ExchangeOnlineManagement/2.0.4).
2. Connect to the module. For more information, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell#connect-to-exchange-online-powershell-using-mfa-and-modern-authentication).
3. After you connected to the Exchange Online PowerShell, use the [Set-OwaMailboxPolicy](/en-us/powershell/module/exchangepowershell/set-owamailboxpolicy) cmdlet to update the parameters in the policy:

    ```powershell
    Set-OwaMailboxPolicy -Identity OwaMailboxPolicy-Default -DirectFileAccessOnPrivateComputersEnabled $false -DirectFileAccessOnPublicComputersEnabled $false
    ```

    Note

    The **OwaMailboxPolicy-Default** policy is the default OWA policy name in Exchange Online. Some customers may have deployed additional or created a custom OWA policy with a different name. If you have multiple OWA policies, they may be applied to specific users. Therefore, you'll need to also update them to have complete coverage.
4. After these parameters are set, run a test on OWA with a PDF file and a session policy configured to block downloads. The **Download** option should be removed from the dropdown and you can preview the file. For example:

    ![Screenshot of a PDF preview not blocked.](media/after-powershell.png)

## Similar site warning appears

Malicious actors can craft URLs that are similar to other sites' URLs in order to impersonate and trick users to believe they're browsing to another site. Some browsers try to detect this behavior and warn users before accessing the URL or block access.

In some rare cases, users under session control receive a message from the browser indicating suspicious site access. The reason for this is the browser treats the suffixed domain (for example: `.mcas.ms`) as suspicious.

This message only appears for Chrome users, as Microsoft Edge users benefit from in-browser protection, without the reverse proxy architecture. For example:

[![Screenshot of a similar site warning in Chrome.](media/chrome-similar-site-warning.png)](media/chrome-similar-site-warning.png#lightbox)

If you receive a message like this, contact Microsoft’s support to address it with the relevant browser vendor.

## Users encounter Entra ID Login after clicking mcas.ms links

Attackers can craft URLs that appear to lead to trusted domains but actually redirect users to malicious sites. For users protected by the session/suffix-based solution, an attacker might attempt to bypass controls by appending the mcas.ms suffix to a malicious URL, exploiting the assumption that such URLs are safe.

To mitigate this, Microsoft Defender for Cloud Apps redirects any mcas.ms URL lacking valid session context to Entra ID for authentication, effectively blocking such exploits.

However, legitimate mcas.ms URLs without context can exist, for example, if a user clicks on an old browser bookmark. In such cases, the user will first be redirected to Entra ID. If their identity provider (IdP) is not Entra ID, they will need to manually remove the mcas.ms suffix to proceed.

## More considerations for troubleshooting apps

When troubleshooting apps, there are some more things to consider:

- **Session controls support for modern browsers** Defender for Cloud Apps session controls now includes support for the new Microsoft Edge browser based on Chromium. While we continue supporting the most recent versions of Internet Explorer and the legacy version of Microsoft Edge, the support is limited and we recommend using the new Microsoft Edge browser.
- **Session controls protect limitation** Co-Auth labeling under **"protect"** action isn't supported by Defender for Cloud Apps session controls. For more information, see [Enable coauthoring for files encrypted with sensitivity labels](/en-us/purview/sensitivity-labels-coauthoring#if-you-need-to-disable-this-feature).