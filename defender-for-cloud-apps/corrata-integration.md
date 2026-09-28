---
layout: Conceptual
title: Integrate with Corrata - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/corrata-integration
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
description: This article describes how to integrate Microsoft Defender for Cloud Apps with Corrata for seamless cloud discovery and automated block of unsanctioned apps.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: Mravela
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: f48b903a-5bb7-24cc-3493-42f53f1033c8
document_version_independent_id: f48b903a-5bb7-24cc-3493-42f53f1033c8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/corrata-integration.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: corrata-integration
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/corrata-integration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
platformId: 602464af-ac7b-6d17-5af2-d699e538d4e7
---

# Integrate with Corrata - Microsoft Defender for Cloud Apps | Microsoft Learn

If you work with both Defender for Cloud Apps and Corrata, you can integrate the two products to enhance your security cloud discovery experience for mobile app use. Corrata, as a local Mobile gateway, monitors your organization's traffic from mobile devices enabling administrators to set policies for blocking transactions. Together, Defender for Cloud Apps and Corrata provide the following capabilities:

- Seamless deployment of cloud discovery - Use Corrata to collect your mobile device traffic and send it to Defender for Cloud Apps. This approach eliminates the need for installation of log collectors on your network endpoints to enable cloud discovery.
- Corrata's block capabilities are automatically applied on apps you set as unsanctioned in Defender for Cloud Apps.
- Enhance your Corrata portal with the Defender for Cloud Apps risk assessment for leading cloud apps, which can be viewed directly in the Corrata portal.

## Prerequisites

Before you begin, make sure you have the following licenses:

- A valid license for Microsoft Defender for Cloud Apps
- A valid license for Corrata Cloud

## Deployment

Perform the following steps to deploy the Corrata integration with Defender for Cloud Apps:

1. In the Corrata portal, integrate Corrata into Defender for Cloud Apps. For instructions, see [Integrating Corrata with Microsoft Defender for Cloud Apps](https://corrata.com/microsoft-mcas-onboarding/).
2. In the [Microsoft Defender Portal](https://security.microsoft.com/), do the following integration steps:

    1. Select **Settings**. Then choose **Cloud Apps**.
    2. Under **Cloud Discovery**, select **Automatic log upload**. Then select **+Add data source**.
    3. In the **Add data source** page, enter the following settings:

        - Name = Corrata
        - Source = Corrata
        - Receiver type = FTP

        ![Screenshot of the Add data source page with Corrata selected as the source.](media/data-source-corrata.png)
    4. Select **View sample of expected log file**. Then select **Download sample log** to view a sample discovery log, and make sure it matches your logs.
3. Investigate cloud apps discovered on your network. For more information and investigation steps, see [Working with cloud discovery](working-with-cloud-discovery-data).
4. Any app that you set as unsanctioned in Defender for Cloud Apps will be pinged by Corrata, and then automatically blocked by Corrata. For more information about unsanctioning apps, see [Sanctioning/unsanctioning an app](governance-discovery#sanctioningunsanctioning-an-app).