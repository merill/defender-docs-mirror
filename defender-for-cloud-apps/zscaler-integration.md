---
layout: Conceptual
title: Integrate with Zscaler - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/zscaler-integration
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
description: This article describes how to integrate Microsoft Defender for Cloud Apps with Zscaler for seamless cloud discovery and automated block of unsanctioned apps.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: Mravela
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: b921d4e6-52d8-973b-474d-39ad7abde37f
document_version_independent_id: b921d4e6-52d8-973b-474d-39ad7abde37f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/zscaler-integration.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: zscaler-integration
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/zscaler-integration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 07aafdce-808f-b724-13e8-caf27f12f4ea
---

# Integrate with Zscaler - Microsoft Defender for Cloud Apps | Microsoft Learn

This article explains how to configure the integration between Microsoft Defender for Cloud Apps and Zscaler, including prerequisites and setup steps. If you work with both Microsoft Defender for Cloud Apps and [Zscaler](https://www.zscaler.com/), integrate the two to enhance your cloud discovery experience. Zscaler, as a standalone cloud proxy, monitors your organization's traffic and enables you set policies for blocking transactions. Together, Defender for Cloud Apps and Zscaler provide the following capabilities:

- **Seamless cloud discovery**: Use Zscaler to proxy your traffic and send it to Defender for Cloud Apps. Integrating the two services means that you don't need to install log collectors on your network endpoints to enable cloud discovery.
- **Automatic blocking**: After configuring the integration, Zscaler's block capabilities are automatically applied on any apps you set as *unsanctioned* in Defender for Cloud Apps.
- **Enhanced Zscalar data**: Enhance your Zscaler portal with the Defender for Cloud Apps risk assessment for leading cloud apps, which can be viewed directly in the Zscaler portal.

## Prerequisites

Before you deploy the Zscaler integration, make sure you have the following prerequisites:

- A valid license for Microsoft Defender for Cloud Apps, or a valid license for Microsoft Entra ID P1
- A valid license for Zscaler Cloud 5.6
- An active Zscaler NSS subscription

## Deploy the Zscaler integration

Perform the following steps to deploy and complete the Zscaler integration:

1. In the Zscalar portal, configure the Zscaler integration for Defender for Cloud Apps. For more information, see the [Zscaler documentation](https://help.zscaler.com/zia/configuring-mcas-integration).
2. In [Microsoft Defender XDR](https://security.microsoft.com/), complete the integration with the following steps:

    1. Select **Settings** &gt; **Cloud apps** &gt; **Cloud discovery** &gt; **Automatic log upload** &gt; **+Add data source**.
    2. In the **Add data source** page, enter the following settings:

        - **Name** = NSS
        - **Source** = Zscaler QRadar LEEF
        - **Receiver type** = Syslog - UDP

        For example:

        [![Screenshot of adding the Zscaler data source.](media/data-source-zscaler.png)](media/data-source-zscaler.png#lightbox)

        Note

        Make sure the name of the data source is **NSS.** For more information about setting up NSS feeds, see [Adding Defender for Cloud Apps NSS Feeds](https://help.zscaler.com/zia/adding-mcas-nss-feeds).
    3. To view a sample discovery log, select **View sample of expected log file** &gt; **Download sample log**. Make sure that the downloaded sample log matches your log files.

After completing the integration steps, any app that you set as *unsanctioned* in Defender for Cloud Apps is pinged by Zscaler every two hours, and then blocked according to the blocking settings configured in your Zscaler portal. For more information, see [Sanctioning/unsanctioning an app](governance-discovery#sanctioningunsanctioning-an-app).

Continue by investigating cloud apps discovered on your network. For more information and investigation steps, see [Working with cloud discovery](working-with-cloud-discovery-data).