---
layout: Conceptual
title: Integrate with iboss - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/iboss-integration
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
description: This article describes how to integrate Microsoft Defender for Cloud Apps with iboss secure cloud gateway for seamless cloud discovery and automated block of unsanctioned apps.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: Mravela
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 14eeaa0b-1699-068e-9928-b9e881044782
document_version_independent_id: 14eeaa0b-1699-068e-9928-b9e881044782
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/iboss-integration.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: iboss-integration
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/iboss-integration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
platformId: 5b6ad5bc-5d68-9f03-f89a-209f04969b50
---

# Integrate with iboss - Microsoft Defender for Cloud Apps | Microsoft Learn

If you work with both Defender for Cloud Apps and iboss, you can integrate the two products to enhance your security cloud discovery experience. iboss is a standalone secure cloud gateway that monitors your organization's traffic and enables you to set policies that block transactions. Together, Defender for Cloud Apps and iboss provide the following capabilities:

- Seamless deployment of cloud discovery - Use iboss to proxy your traffic and send it to Defender for Cloud Apps. Proxying traffic through iboss eliminates the need for installation of log collectors on your network endpoints to enable cloud discovery.
- iboss's block capabilities are automatically applied on apps you set as unsanctioned in Defender for Cloud Apps.
- Enhance your iboss admin portal with the Defender for Cloud Apps risk assessment of the top 100 cloud apps in your organization, which can be viewed directly in the iboss admin portal.

## Prerequisites

Before you begin, make sure you have the following licenses:

- A valid license for Microsoft Defender for Cloud Apps
- A valid license for iboss secure cloud gateway (release 9.1.100.0 or later)

## Deploy the iboss integration

To deploy the iboss integration with Defender for Cloud Apps, complete the following steps:

1. In the [Microsoft Defender Portal](https://security.microsoft.com/), do the following integration steps:

    1. Select **Settings**. Then choose **Cloud Apps**.
    2. Under **Cloud Discovery**, select **Automatic log upload**. Then select **+Add data source**.
    3. In the **Add data source** page, enter the following settings:

        - Name = iboss
        - Source = iboss Secure Cloud Gateway
        - Receiver type = Syslog - UDP

        ![Screenshot of the Add data source page with iboss Secure Cloud Gateway selected and Syslog UDP receiver type configured.](media/iboss-integration.png)
    4. Select **View sample of expected log file**. Then select **Download sample log** to view a sample discovery log, and make sure it matches your logs.
2. Investigate cloud apps discovered on your network. For more information and investigation steps, see [Working with cloud discovery](working-with-cloud-discovery-data).
3. Any app that you set as unsanctioned in Defender for Cloud Apps will be pinged by iboss once every ten minutes, and then automatically blocked by iboss. For more information about unsanctioning apps, see [Sanctioning/unsanctioning an app](governance-discovery#sanctioningunsanctioning-an-app).
4. To configure iboss to send traffic logs to Microsoft Defender for Cloud Apps, contact iboss support.