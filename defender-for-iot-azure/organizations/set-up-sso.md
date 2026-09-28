---
layout: Conceptual
title: Set up Single Sign-on for Microsoft Defender for IoT Sensor Console - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/set-up-sso
breadcrumb_path: ../breadcrumb/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-iot-blog/bg-p/MicrosoftDefenderIoTBlog
feedback_help_link_type: ask-the-community
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
ms.service: defender-for-iot
author: limwainstein
manager: bagol
ms.author: lwainstein
description: Configure single sign-on (SSO) for the Microsoft Defender for IoT sensor console using Microsoft Entra ID in the Azure portal.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: e2e1ecdd-3c6b-ee2a-67e9-634b8ff2758f
document_version_independent_id: 3d3ce11c-2428-9146-d4cf-7af6d2b707b9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/set-up-sso.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/set-up-sso
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/set-up-sso.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 85a03701-acdb-fbe1-7748-ffb377e0e0e5
---

# Set up Single Sign-on for Microsoft Defender for IoT Sensor Console - Microsoft Defender for IoT | Microsoft Learn

This article shows how to set up single sign-on (SSO) for the Defender for IoT sensor console. SSO uses Microsoft Entra ID so your users can sign in once. They don't need separate credentials for each sensor or site.

Microsoft Entra ID makes it easier to add or remove users, reduces admin work, and keeps access controls consistent across your organization.

Note

Signing in via SSO is currently in PREVIEW. The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include other legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

## Prerequisites

Before you begin:

- [Synchronize on-premises active directory with Microsoft Entra ID](/en-us/azure/architecture/reference-architectures/identity/azure-ad).
- Add outbound allow rules to your firewall, proxy server, and so on. You can access the list of required endpoints from the [Sites and sensors page](how-to-manage-sensors-on-the-cloud#endpoint).
- If you don't have existing Microsoft Entra ID user groups to use for SSO authorization, work with your organization's identity manager to create relevant user groups.
- Verify that you have the following permissions:
    - A Member user on Microsoft Entra ID.
    - Admin, Contributor, or Security Admin permissions on the Defender for IoT subscription.
- Ensure that each user has a **First name**, **Last name**, and **User principal name**.
- If needed, set up [Multifactor authentication (MFA)](/en-us/entra/identity/authentication/tutorial-enable-azure-mfa).

## Create an application ID in Microsoft Entra ID

To create an application ID in Microsoft Entra ID, perform the following steps:

1. In the Azure portal, open Microsoft Entra ID.
2. Select **Add &gt; App registration**.

    [![Screenshot of adding a new app registration on the Microsoft Entra ID Overview page.](media/set-up-sso/create-application-id.png)](media/set-up-sso/create-application-id.png#lightbox)
3. In the **Register an application** page:

    - Under **Name**, type a name for your application.
    - Under **Supported account types**, select **Accounts in this organizational directory only (Microsoft only - single tenant)**.
    - Under **Redirect URI**, add an IP or hostname for the first sensor on which you want to enable SSO. You continue to add URIs for the other sensors in the next step, Add your sensor URIs.

    Note

    Adding the URI at this stage is required for SSO to work.

    [![Screenshot of registering an application on Microsoft Entra ID.](media/set-up-sso/register-application.png)](media/set-up-sso/register-application.png#lightbox)
4. Select **Register**. Microsoft Entra ID displays your newly registered application.

## Add your sensor URIs

Add the redirect URIs for each sensor to your registered application:

1. In your new application, select **Authentication​**.
2. Under **Redirect URIs**, the URI for the first sensor, added in Create application ID on Microsoft Entra ID, is displayed under **Redirect URIs**. To add the rest of the URIs:

    1. Select **Add URI** to add another row, and type an IP or hostname.
    2. Repeat this step for the rest of the connected sensors.

        When Microsoft Entra ID adds the URIs successfully, a "Your redirect URI is eligible for the Authorization Code Flow with PKCE" message is displayed.

        [![Screenshot of setting up URIs for your application on the Microsoft Entra ID Authentication page.](media/set-up-sso/authentication.png)](media/set-up-sso/authentication.png#lightbox)
3. Select **Save**.

## Grant API permissions

Your registered application needs the default Microsoft Graph `User.Read` permission to sign in users. An admin must grant tenant-wide consent so that all users can use SSO without individual approval prompts.

1. In your new application, select **API permissions​**.
2. Select **Grant admin consent for &lt;Directory name&gt;**.

    [![Screenshot of setting up API permissions in Microsoft Entra ID.](media/set-up-sso/api-permissions.png)](media/set-up-sso/api-permissions.png#lightbox)

## Configure single sign-on settings

Create the SSO configuration in Defender for IoT to enable single sign-on for your sensors:

1. In [Defender for IoT](https://portal.azure.com/#view/Microsoft_Azure_IoT_Defender/IoTDefenderDashboard/%7E/Getting_started) on the Azure portal, select **Sites and sensors** &gt; **Sensor settings**.
2. On the **Sensor settings** page, select **+ Add**. In the **Basics** tab:

    1. Select your subscription.
    2. Next to **Type**, select **Single sign-on**.
    3. Next to **Name**, type a name for the relevant site, and select **Next**.

        ![Screenshot of creating a new Single sign-on sensor setting in Defender for IoT.](media/set-up-sso/sensor-setting-sso.png)
3. In the **Settings** tab:

    1. Next to **Application name**, select the ID of the registered Microsoft Entra application.
    2. Under **Permissions management**, assign the **Admin**, **Security analyst**, and **Read only​** permissions to relevant user groups. You can select multiple user groups​.

        ![Screenshot of setting up permissions in the Defender for IoT sensor settings.](media/set-up-sso/permissions-management.png)
    3. Select **Next**.

    Note

    Make sure you've added allow rules on your firewall/proxy for the specified endpoints. You can access the list of required endpoints from the [Sites and sensors page](how-to-manage-sensors-on-the-cloud#endpoint).
4. In the **Apply** tab, select the relevant sites.

    [![Screenshot of the Apply tab in the Defender for IoT sensor settings.](media/set-up-sso/apply.png)](media/set-up-sso/apply.png#lightbox)

    You can optionally toggle on **Add selection by specific zone/sensor** to apply your setting to specific zones and sensors.​
5. Select **Next**, review your configuration, and select **Create**.

## Test sign-in with SSO

To test signing in with SSO:

1. Open [Defender for IoT](https://portal.azure.com/#view/Microsoft_Azure_IoT_Defender/IoTDefenderDashboard/%7E/Getting_started) on the Azure portal, and select **SSO Sign-in**.

    ![Screenshot of the sensor console login screen with SSO.](media/set-up-sso/sso-sign-in.png)
2. For the first sign in, in the **Sign in** page, type your personal credentials (your work email and password).

    ![Screenshot of the Sign in screen when signing in to Defender for IoT on the Azure portal via SSO.](media/set-up-sso/sso-first-sign-in-credentials.png)

The Defender for IoT **Overview** page is displayed.