---
layout: Conceptual
title: Enable Microsoft Sentinel SIEM and Initial Features and Content | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/enable-sentinel-features-content
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
description: As the first step of your deployment, you enable Microsoft Sentinel, and then enable the health and audit feature, solutions, and content.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: abhiag
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 132dc8f1-7d15-517a-c94d-8b377f75a04e
document_version_independent_id: f5f2ef3d-d3e1-e880-ae9a-4b41a872b9c8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/enable-sentinel-features-content.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/enable-sentinel-features-content
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/enable-sentinel-features-content.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 1d59874e-ff5c-b253-fbf2-918b8892b784
---

# Enable Microsoft Sentinel SIEM and Initial Features and Content | Microsoft Learn

As part of the [Deployment guide for Microsoft Sentinel](deploy-overview), this procedure walks you through enabling Microsoft Sentinel, enabling the health and audit feature, and enabling the solutions and content you've identified according to your organization's needs. This article is intended for security architects and operations teams who have already completed workspace planning and are ready to activate the service. By the end of these steps, you'll have a functioning Microsoft Sentinel instance with health monitoring turned on and the solutions needed for your selected data sources deployed. This procedure covers initial enablement only; configuring data connectors, analytics rules, and other content is handled in subsequent steps of the deployment guide.

## Enable features and content

Use the following steps to enable Microsoft Sentinel features and content for your deployment.

| Step | Description |
| --- | --- |
| 1. [Enable the Microsoft Sentinel service](quickstart-onboard#enable) | In the Azure portal, enable Microsoft Sentinel to run on the Log Analytics workspace your organization planned as part of your workspace design. To onboard to Microsoft Sentinel by using the API, see the latest supported version of [Sentinel Onboarding States](/en-us/rest/api/securityinsights/sentinel-onboarding-states). |
| 2. [Enable health and audit](enable-monitoring) | Enable health and audit at this stage of your deployment to make sure that the service's many moving parts are always functioning as intended and that the service isn't being manipulated by unauthorized actions. Learn more about the [health and audit](health-audit) feature. |
| 3. [Enable solutions and content](sentinel-solutions-deploy) | When you planned your deployment, you identified which data sources you need to ingest into Microsoft Sentinel. Now, you want to enable the relevant solutions and content so that the data you need can start flowing into Microsoft Sentinel. |