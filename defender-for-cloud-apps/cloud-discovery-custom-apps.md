---
layout: Conceptual
title: Add custom apps to cloud discovery - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/cloud-discovery-custom-apps
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
description: This topic provides information about how to add custom apps to cloud discovery in Defender for Cloud Apps to monitor Shadow IT.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: Mravela
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 79e8153e-9e16-28e4-3309-e00b6e1bcbe6
document_version_independent_id: 79e8153e-9e16-28e4-3309-e00b6e1bcbe6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/cloud-discovery-custom-apps.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: cloud-discovery-custom-apps
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/cloud-discovery-custom-apps.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: c172a82f-7f8a-5463-c1a7-2478b8b1e4d3
---

# Add custom apps to cloud discovery - Microsoft Defender for Cloud Apps | Microsoft Learn

Cloud discovery analyzes your traffic logs against the Defender for Cloud Apps catalog. Over 31,000 cloud apps are in the cloud app catalog. The catalog contains publicly available cloud apps only, for which Defender for Cloud Apps provides visibility and risk information.

To gain visibility into cloud apps that are excluded from the cloud app catalog, Defender for Cloud Apps enables you to discover use of custom cloud apps (LOB apps) that were developed or assigned specifically for your organization.

By adding a new custom cloud app, Defender for Cloud Apps can match uploaded firewall and proxy traffic log messages to the app and then provide you with visibility into the use of this app across your organization in the cloud discovery pages, such as how many users use the app, how many unique source IP addresses use it, and how much traffic is transmitted to and from the app.

## Add a new custom cloud app

To add a new custom cloud app, perform the following steps:

1. In the Microsoft Defender Portal, under **Cloud Apps**, select **Cloud Discovery**. You should see the cloud discovery dashboard.

    ![Screenshot of the Cloud Discovery dashboard menu in the Microsoft Defender Portal.](media/cloud-discovery-dashboard-menu.png)
2. In the top right corner, select the **Action** menu and then select **Add new custom app**.

    ![Screenshot of the Action menu with the Add new custom app option selected.](media/add-custom-app-menu.png)
3. Fill in the fields to define the new app record that will be listed in the cloud app catalog and in cloud discovery after it's discovered in your firewall logs.

    ![Screenshot of the Add custom app page showing fields for defining a new custom app record.](media/add-custom-app.png)
4. Under **Domains**, fill in the unique domains that are used when accessing the custom app. These domains are used to match traffic log messages to this app. If the data source you're using doesn't have app URL information, make sure you fill in the **IPv4** and **IPv6** address fields.
5. Add the **Hosting platform** and **Azure Subscription ID**. Optionally, specify the app's **Business unit**.
6. Assign a risk **Score** and add **App Notes** to help you track changes for this record.
7. Select **Create**.

After the app is created, the custom app is available for you in the cloud app catalog.

At any time, in the cloud app catalog, you can select the three dots at the end of a custom app's row to edit or delete the custom app.

Warning

Avoid adding custom apps when you are using the **Remove all tags** feature. Using **Remove all tags** also removes the **Custom app** tag from the app.

Note

Custom apps are automatically tagged with the **Custom app** tag after you add them. To view all your custom apps, set the **App tag** filter to *Custom app*.