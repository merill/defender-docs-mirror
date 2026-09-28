---
layout: Conceptual
title: View Defender for Identity workspace details on the About page in Microsoft Defender XDR - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/settings-about
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: Learn how to collect important details about your Defender for Identity workspace in Microsoft Defender XDR.
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: rlitinsky
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: aad2521e-bb62-662f-1139-a0c24646aba4
document_version_independent_id: aad2521e-bb62-662f-1139-a0c24646aba4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/settings-about.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: settings-about
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/settings-about.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
platformId: a0a5947c-dec2-395b-e911-ae6a45508fc8
---

# View Defender for Identity workspace details on the About page in Microsoft Defender XDR - Microsoft Defender for Identity | Microsoft Learn

This article explains how to use the About page to collect important details about your Defender for Identity workspace in Microsoft Defender. Before you begin, make sure you meet the [Defender for Identity prerequisites](prerequisites).

## Information shown on the Defender for Identity About page

To access the About page, in [Microsoft Defender XDR](https://security.microsoft.com), go to **Settings** and then **Identities**. Under **General**, select **About**.

![About page.](media/settings-about-page.png)

The About page provides the following details:

- Sensor version: The latest software version available for sensor updates.
- Geolocation: The geographic location of the workspace where your data is stored.
- Workspace ID: The identifier of your workspace.
- Workspace name: The name of your workspace.
- Total licenses: The total number of Microsoft Denfender for Identity licenses assigned to the tenant.
- Active identities during the past 28 days: The total number of on-premises identities that had activity detected by Defender for Identity.

This information can help you troubleshoot issues and open support tickets. You can also find your workspace name here. You need the workspace name to configure your [proxy or firewall](configure-proxy#enable-access-to-defender-for-identity-service-urls-in-the-proxy-server).