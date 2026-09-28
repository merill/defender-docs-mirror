---
layout: Conceptual
title: Connect your threat intelligence platform - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/connect-threat-intelligence-tip
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
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
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
description: Learn how to connect your threat intelligence platform (TIP) or custom feed to Microsoft Sentinel and send threat indicators.
ms.author: pauloliveria
author: poliveria
ms.reviewer: yoninave
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: f0e6daec-a15c-635c-270b-7041ccad51d2
document_version_independent_id: 7400bcc3-36d2-d90d-a659-375242571f09
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/connect-threat-intelligence-tip.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/connect-threat-intelligence-tip
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/connect-threat-intelligence-tip.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 0ed0125d-a846-01b0-10fc-7979a4d89817
---

# Connect your threat intelligence platform - Microsoft Sentinel | Microsoft Learn

Note

This data connector will be deprecated and will stop collecting data in **June 2026**. We recommend transitioning to the new Threat Intelligence Upload Indicators API data connector as soon as possible to ensure uninterrupted data collection. For more information, see [Connect your threat intelligence platform to Microsoft Sentinel with the upload API](connect-threat-intelligence-upload-api).

Many organizations use threat intelligence platform (TIP) solutions to aggregate threat indicator feeds from various sources. From the aggregated feed, the data is curated to apply to security solutions such as network devices, EDR/XDR solutions, or security information and event management (SIEM) solutions such as Microsoft Sentinel. By using the TIP data connector, you can use your TIP solution to import threat indicators into Microsoft Sentinel.

Because the TIP data connector works with the [Microsoft Graph Security tiIndicators API](/en-us/graph/api/resources/tiindicator) to import threat indicators, you can use the connector to send indicators to Microsoft Sentinel (and to other Microsoft security solutions like Defender XDR) from any other custom TIP that can communicate with that API.

![Screenshot that shows the threat intelligence import path.](media/connect-threat-intelligence-tip/threat-intel-import-path.png)

Note

For information about feature availability in US Government clouds, see the Microsoft Sentinel tables in [Cloud feature availability for US Government customers](/en-us/azure/security/fundamentals/feature-availability).

Learn more about [threat intelligence](understand-threat-intelligence) in Microsoft Sentinel, and specifically about the [TIP products](threat-intelligence-integration#integrated-threat-intelligence-platform-products) that you can integrate with Microsoft Sentinel.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Prerequisites

Before you begin, make sure you have the following roles and permissions:

- To install, update, and delete standalone content or solutions in the **Content hub**, you need the Microsoft Sentinel Contributor role at the resource group level.
- To grant permissions to your TIP product or any other custom application that uses direct integration with the Microsoft Graph TI Indicators API, you must have the Security Administrator Microsoft Entra role or the equivalent permissions.
- To store your threat indicators, you must have read and write permissions to the Microsoft Sentinel workspace.

## Register an application and enable the TIP connector

To import threat indicators to Microsoft Sentinel from your integrated TIP or custom threat intelligence solution, follow these steps:

1. Obtain an application ID and client secret from Microsoft Entra ID.
2. Input this information into your TIP solution or custom application.
3. Enable the TIP data connector in Microsoft Sentinel.

## Sign up for an application ID and client secret from Microsoft Entra ID

Whether you're working with a TIP or a custom solution, the tiIndicators API requires some basic information to allow you to connect your feed to the API and send threat indicators. The three pieces of information you need are:

- Application (client) ID
- Directory (tenant) ID
- Client secret

You can get the application ID, tenant ID, and client secret from Microsoft Entra ID through app registration, which includes the following three steps:

- Register an app with Microsoft Entra ID.
- Specify the permissions required by the app to connect to the Microsoft Graph tiIndicators API and send threat indicators.
- Get consent from your organization to grant the Microsoft Graph tiIndicators API permissions to this application.

### Register an application with Microsoft Entra ID

Register an app in Microsoft Entra ID to obtain the application ID and tenant ID needed for TIP integration.

1. In the Azure portal, go to **Microsoft Entra ID**.
2. On the menu, select **App Registrations**, and then select **New registration**.
3. Choose a name for your application registration, select **Single tenant**, and then select **Register**.

    ![Screenshot that shows registering an application.](media/connect-threat-intelligence-tip/threat-intel-register-application.png)
4. On the screen that opens, copy the **Application (client) ID** and **Directory (tenant) ID** values. You need the application ID and tenant ID later to configure your TIP or custom solution to send threat indicators to Microsoft Sentinel. The third piece of information you need, the client secret, comes later.

### Specify the permissions required by the application

Grant the application the API permission it needs to send threat indicators.

1. Go back to the main page of **Microsoft Entra ID**.
2. On the menu, select **App Registrations**, and then select your newly registered app.
3. On the menu, select **API Permissions** &gt; **Add a permission**.
4. On the **Select an API** page, select the **Microsoft Graph** API. Then choose from a list of Microsoft Graph permissions.
5. At the prompt **What type of permissions does your application require?**, select **Application permissions**. Application permissions are used by applications that authenticate with app ID and app secrets (API keys).
6. Select **ThreatIndicators.ReadWrite.OwnedBy**, and then select **Add permissions** to add the **ThreatIndicators.ReadWrite.OwnedBy** permission to your app's list of permissions.

    ![Screenshot that shows specifying permissions.](media/connect-threat-intelligence-tip/threat-intel-api-permissions-1.png)

### Get consent from your organization to grant these permissions

1. To grant consent, a privileged role is required. For more information, see [Grant tenant-wide admin consent to an application](/en-us/entra/identity/enterprise-apps/grant-admin-consent?pivots=portal).

    ![Screenshot that shows granting consent.](media/connect-threat-intelligence-tip/threat-intel-api-permissions-2.png)
2. After consent is granted to your app, you should see a green check mark under **Status**.

After your app is registered and permissions are granted, you need to get a client secret for your app.

1. Go back to the main page of **Microsoft Entra ID**.
2. On the menu, select **App Registrations**, and then select your newly registered app.
3. On the menu, select **Certificates & secrets**. Then select **New client secret** to receive a secret (API key) for your app.

    ![Screenshot that shows getting a client secret.](media/connect-threat-intelligence-tip/threat-intel-client-secret.png)
4. Select **Add**, and then copy the client secret.

    Important

    You must copy the client secret before you leave this screen. You can't retrieve this secret again if you go away from this page. You need the client secret when you configure your TIP or custom solution.

## Enter the application ID, tenant ID, and client secret into your TIP solution or custom application

You now have all three pieces of information you need to configure your TIP or custom solution to send threat indicators to Microsoft Sentinel:

- Application (client) ID
- Directory (tenant) ID
- Client secret

Enter these values in the configuration of your integrated TIP or custom solution where required.

1. For the target product, specify **Azure Sentinel**. (Specifying **Microsoft Sentinel** results in an error.)
2. For the action, specify **alert**.

After you finish configuring your TIP or custom solution with the application ID, tenant ID, and client secret, threat indicators are sent from your TIP or custom solution, through the Microsoft Graph tiIndicators API, targeted at Microsoft Sentinel.

## Enable the TIP data connector in Microsoft Sentinel

The last step in the integration process is to enable the TIP data connector in Microsoft Sentinel. Enabling the TIP data connector allows Microsoft Sentinel to receive the threat indicators sent from your TIP or custom solution. These indicators are available to all Microsoft Sentinel workspaces for your organization. To enable the TIP data connector for each workspace, follow these steps:

1. For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), under **Content management**, select **Content hub**. For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), select **Microsoft Sentinel** &gt; **Content management** &gt; **Content hub**.
2. Find and select the **Threat Intelligence** solution.
3. Select the ![](media/connect-mdti-data-connector/install-update-button.png)**Install/Update** button.

    For more information about how to manage the solution components, see [Discover and deploy out-of-the-box content](sentinel-solutions-deploy).
4. To configure the TIP data connector, select **Configuration** &gt; **Data connectors**.
5. Find and select the **Threat Intelligence Platforms - BEING DEPRECATED** data connector, and then select **Open connector page**.
6. Because you already finished the app registration and configured your TIP or custom solution to send threat indicators, select **Connect** to finish enabling the TIP data connector.

Within a few minutes, threat indicators should begin flowing into this Microsoft Sentinel workspace. You can find the new indicators on the **Threat intelligence** pane, which you can access from the Microsoft Sentinel menu.