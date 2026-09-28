---
layout: Conceptual
title: Enrich cloud discovery data with Microsoft Entra usernames - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/cloud-discovery-aad-enrichment
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
description: This article provides information about how to enrich Defender for Cloud Apps Discovery data with Microsoft Entra usernames.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: Mravela
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: aa0e8f65-b8e4-1349-3f67-339a38e09110
document_version_independent_id: aa0e8f65-b8e4-1349-3f67-339a38e09110
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/cloud-discovery-aad-enrichment.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: cloud-discovery-aad-enrichment
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/cloud-discovery-aad-enrichment.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: d6c5469f-8d36-e0e5-544c-bd89c5290cfe
---

# Enrich cloud discovery data with Microsoft Entra usernames - Microsoft Defender for Cloud Apps | Microsoft Learn

Cloud discovery data can now be enriched with Microsoft Entra username data. When you enable cloud discovery user enrichment, the username received in discovery traffic logs is matched and replaced by the Microsoft Entra username. Cloud discovery enrichment enables the following features:

- You can investigate Shadow IT usage by Microsoft Entra user. The user will be shown with its UPN.
- You can correlate the Discovered cloud app use with the API collected activities.
- You can then create custom reports based on Microsoft Entra user groups. For example, a Shadow IT report for a specific Marketing department.

Note

As Microsoft Defender moves toward a fully unified identity platform, some Defender for Cloud Apps data pipelines remain separate. Cloud discovery user enrichment uses a separate data pipeline that isn't yet integrated with the [Identity inventory](/en-us/defender-for-identity/identity-inventory). Correlations defined in the Identity inventory don't affect cloud discovery user enrichment. For a full list of affected features, see [Enable Identity inventory integration](/en-us/defender-cloud-apps/general-setup#enable-identity-inventory-integration).

## Prerequisites

Before you enable user data enrichment, make sure the following prerequisites are met:

- Data source must provide username information
- [Microsoft 365 app connector](connect-office-365) connected

## Enable user data enrichment

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**.
2. Under **Cloud Discovery**, select **User enrichment**.
3. In the **User enrichment** tab, select **Enrich discovered user identifiers with Microsoft Entra ID usernames**. This option enables Defender for Cloud Apps to use Microsoft Entra ID data to enrich usernames by default.

    Tip

    The **Enrich discovered user identifiers with Microsoft Entra ID usernames** option enriches discovery traffic log usernames with Microsoft Entra ID data.

    ![Screenshot of the User enrichment tab with the option to enrich discovered user identifiers with Microsoft Entra ID usernames.](media/discovery-enrichment.png)