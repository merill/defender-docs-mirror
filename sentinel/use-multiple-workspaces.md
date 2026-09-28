---
layout: Conceptual
title: Set up multiple workspaces and tenants in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/use-multiple-workspaces
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
description: If you've defined that your environment needs multiple workspaces, you now set up your multiple workspace architecture in Microsoft Sentinel.
author: EdB-MSFT
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.author: edbaynash
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 4405badd-7fa7-0497-2386-030bb5d81b46
document_version_independent_id: 945e4f98-ba46-4035-3bfc-f88f07e51576
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/use-multiple-workspaces.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/use-multiple-workspaces
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/use-multiple-workspaces.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: d26791b7-9a5e-360f-2b1b-90efac3bc1df
---

# Set up multiple workspaces and tenants in Microsoft Sentinel | Microsoft Learn

If your environment requires a multiple workspace architecture, you can set it up as part of your Microsoft Sentinel deployment. For more information on planning considerations, see [Prepare for multiple workspaces and tenants in Microsoft Sentinel](prepare-multiple-workspaces).

In this article, you learn how to set up Microsoft Sentinel to extend across multiple workspaces and tenants. This article is part of the [Deployment guide for Microsoft Sentinel](deploy-overview).

## Options for using multiple workspaces

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline). Starting in **July 2025**, many new customers are [automatically onboarded and redirected to the Defender portal](overview#changes-for-new-customers-starting-july-2025).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview). For more information, see [It’s Time to Move: Retiring Microsoft Sentinel’s Azure portal for greater security](https://techcommunity.microsoft.com/blog/microsoft-security-blog/planning-your-move-to-microsoft-defender-portal-for-all-microsoft-sentinel-custo/4428613).

After you set up your environment to extend across workspaces, you can:

- **Manage and monitor your cross-workspace architecture**: Query and analyze your data across workspaces and tenants.

    - If you're onboarding to the Microsoft Defender portal, see [Multiple Microsoft Sentinel workspaces in the Defender portal](workspaces-defender-portal) and [Microsoft Defender multitenant management](/en-us/defender-xdr/mto-overview).
    - To work in the Azure portal, see [Extend Microsoft Sentinel across workspaces and tenants](extend-sentinel-across-workspaces-tenants).
- **Manage multiple workspaces**: Centrally manage multiple workspaces within one or more tenants.

    - For the Defender portal, see [Multiple Microsoft Sentinel workspaces in the Defender portal](workspaces-defender-portal) and [Microsoft Defender multitenant management](/en-us/defender-xdr/mto-overview).
    - To work in the Azure portal, see [Centrally manage multiple Microsoft Sentinel workspaces with workspace manager](workspace-manager) within one or more Azure tenants.

For each tenant, the Defender portal allows you to connect to one primary workspace and multiple secondary workspaces for Microsoft Sentinel (preview). For more information, see [Microsoft Defender multitenant management](/en-us/defender-xdr/mto-overview).