---
layout: Conceptual
title: Configure Interactive and Long-term Data Retention in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/configure-data-retention-archive
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
description: Towards the end of your deployment procedure, you set up data retention to suit your organization's needs.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: krishsa
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: af963aeb-ae6a-816b-2018-166176127d85
document_version_independent_id: 4cbe36eb-3d93-79cb-a27b-e34a2393c653
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/configure-data-retention-archive.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/configure-data-retention-archive
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/configure-data-retention-archive.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: 6eadb128-de27-de79-f5f8-dfcd3cb00dab
---

# Configure Interactive and Long-term Data Retention in Microsoft Sentinel | Microsoft Learn

In the [Enable UEBA](enable-entity-behavior-analytics) step of the deployment guide, you enabled the User and Entity Behavior Analytics (UEBA) feature to streamline your analysis process. In this article, you learn how to set up interactive and long-term data retention, to make sure your organization retains the data that's important in the long term. This article is part of the [Deployment guide for Microsoft Sentinel](deploy-overview).

## Configure data retention

Retention policies define when to remove data, or mark it for long-term retention, in a Log Analytics workspace. Long-term retention lets you keep older, less used data in your workspace at a reduced cost. To set up data retention plans, consult [Log retention plans in Microsoft Sentinel](log-plans), and use one or both of these methods, depending on your use case:

- [Configure interactive and long-term data retention for one or more tables](/en-us/azure/azure-monitor/logs/data-retention-configure) (one table at a time)
- [Configure data retention for multiple tables](https://github.com/Azure/Azure-Sentinel/tree/master/Tools/Archive-Log-Tool) at once