---
layout: Conceptual
title: Connect Citrix ShareFile - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/protect-citrix-sharefile
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
description: Connect Citrix ShareFile to Microsoft Defender for Cloud Apps using the API connector to gain visibility into user activity and improve threat detection and control.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: AmitMishaeli
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: cb6d12f5-cc5b-d056-3695-71a7e6ff2a82
document_version_independent_id: cb6d12f5-cc5b-d056-3695-71a7e6ff2a82
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/protect-citrix-sharefile.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: protect-citrix-sharefile
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/protect-citrix-sharefile.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/cd48b104-e308-4e08-a405-66f04a7df418
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/ac23bdb5-c078-4620-8ee2-60eba45e97f8
platformId: d0186d96-50f0-4359-4c62-ca02d03239fd
---

# Connect Citrix ShareFile - Microsoft Defender for Cloud Apps | Microsoft Learn

Citrix ShareFile is a secure content collaboration, file sharing and sync solution that supports all the document-centric tasks and workflow needs of small and large businesses. Citrix ShareFile holds critical data of your organization, and that critical role makes it a target for malicious actors.

Connecting Citrix ShareFile to Defender for Cloud Apps gives you improved insights into your users' activities and provides threat detection using machine learning based anomaly detections. Before you start, make sure you meet the prerequisites described later in this article.

Use this app connector to access SaaS Security Posture Management (SSPM) features, via security controls reflected in Microsoft Secure Score. [Learn more](/en-us/microsoft-365/security/defender/microsoft-secure-score).

## Main threats to your Citrix ShareFile environment

Connecting Citrix ShareFile to Defender for Cloud Apps helps you address the following threats:

- Compromised accounts and insider threats
- Data leakage
- Insufficient security awareness
- Unmanaged bring your own device (BYOD)

## How Defender for Cloud Apps helps to protect your environment

Defender for Cloud Apps can help protect your Citrix ShareFile environment in the following ways:

- [Detect cloud threats, compromised accounts, and malicious insiders](best-practices#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [Use the audit trail of activities for forensic investigations](best-practices#use-the-audit-trail-of-activities-for-forensic-investigations)

## SaaS security posture management for Citrix ShareFile

To see security posture recommendations for Citrix Share File in Microsoft Secure Score, create an API connector via the **Connectors** tab, with **Owner** and **Enterprise** permissions. In Secure Score, select **Recommended actions** and filter by **Product** = **CitrixSF**.

For example, recommendations for Citrix Share File include:

- *Enable multi-factor authentication (MFA)*
- *Enable single sign on (SSO)*
- *Enable session timeout for web users*

If a connector already exists and you don't see Citrix Share File recommendations yet, refresh the connection by disconnecting the API connector, and then reconnecting the API connector with the *Access Company account* permissions.

For more information, see:

- [Security posture management for SaaS apps](security-saas)
- [Microsoft Secure Score](/en-us/microsoft-365/security/defender/microsoft-secure-score)

## Connect Citrix ShareFile to Defender for Cloud Apps

Complete the following prerequisites and steps to connect Citrix ShareFile to Microsoft Defender for Cloud Apps.

### Prerequisites

The Citrix Share file user used for logging into Citrix Share file must have Access Company account permissions.

### Create API keys

Perform the following steps to create the API keys required for the connector:

1. Go to [ShareFile API Documentation](https://api.sharefile.com/), and sign in to your organization account.

    ![Screenshot of the Citrix ShareFile sign-in page for API access.](media/connect-citrix-sharefile-login.png)
2. Select **Get an API Key**.

    ![Screenshot of the Citrix ShareFile Get an API Key option.](media/connect-citrix-sharefile-api-key.png)
3. To generate API keys (*Client ID* and *Client Secret*), go to **Create New**.

    ![Screenshot of the Citrix ShareFile API portal Create New key option.](media/connect-citrix-sharefile-create-new.png)
4. Fill out the following fields:

    - **Application name**: Microsoft Defender for Cloud Apps (you can also choose another name).
    - **Redirect URL**: `https://portal.cloudappsecurity.com/api/oauth/saga`.

        For US Government GCC customers, enter `https://portal.cloudappsecuritygov.com/api/oauth/saga` as the redirect URL.

        For US Government GCC High customers, enter `https://portal.cloudappsecurity.us/api/oauth/saga` as the redirect URL.
5. Select **Generate API Key**.
6. Copy the *Client ID* and *Client Secret*.

### Configure Defender for Cloud Apps

Use the following steps to configure the Citrix ShareFile connector in Defender for Cloud Apps:

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**.
2. In the **App connectors** page, select **+Connect an app**, followed by **Citrix ShareFile**.

    ![Screenshot of the App connectors page with the Connect Citrix ShareFile option.](media/connect-citrix-sharefile-app-connectors.png)
3. In the pop-up, give the connector a descriptive name, and select **Connect Citrix ShareFile**.

    ![Screenshot of the Citrix ShareFile connector dialog with instance name field.](media/connect-citrix-sharefile-instance-name.png)
4. In the Citrix ShareFile connector details screen, enter the following fields:

    - The **Client ID** and **Client Secret** that you created in the Citrix ShareFile API portal.
    - **Client Subdomain**: Enter your account's subdomain. For example, if your account's URL is "mycompany.sharefile.com", you would enter "mycompany".
5. Select **Connect** in Citrix ShareFile.
6. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**. Make sure the status of the connected App Connector is **Connected**.

## Rate limits

The default rate limit is 420 requests per minute.