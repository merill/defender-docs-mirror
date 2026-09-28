---
layout: Conceptual
title: Prioritize data connectors for Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/prioritize-data-connectors
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
description: Learn how to plan and prioritize which data sources to use for your Microsoft Sentinel deployment.
author: EdB-MSFT
ms.topic: concept-article
ms.date: 2023-06-29T00:00:00.0000000Z
ms.author: edbaynash
locale: en-us
document_id: d315badf-fbaa-b130-2ea0-93aa7d77e6d0
document_version_independent_id: 11f80fe5-d2e6-02ab-2af5-68b6f5599e0b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/prioritize-data-connectors.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/prioritize-data-connectors
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/prioritize-data-connectors.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 70a555ff-37c7-751d-3fb3-b0fc3574d9c2
---

# Prioritize data connectors for Microsoft Sentinel | Microsoft Learn

In this article, you learn how to plan and prioritize which data sources to use for your Microsoft Sentinel deployment. This article is part of the [Deployment guide for Microsoft Sentinel](deploy-overview).

## Determine which connectors you need

Check which data connectors are relevant to your environment, in the following order:

1. Review this list of [free data connectors](billing#free-data-sources). The free data connectors will start showing value from Microsoft Sentinel as soon as possible, while you continue to plan other data connectors and budgets.
2. Review the [custom](create-custom-connector) data connectors.
3. Review the [partner](data-connectors-reference) data connectors.

For the custom and partner connectors, we recommend that you start by setting up [CEF/Syslog](connect-cef-syslog-options) connectors, with the highest priority first, as well as any Linux-based devices.

If your data ingestion becomes too expensive, too quickly, stop or filter the logs forwarded using the [Azure Monitor Agent](/en-us/azure/azure-monitor/agents/azure-monitor-agent-overview).

Tip

Custom data connectors enable you to ingest data into Microsoft Sentinel from data sources not currently supported by built-in functionality, such as via agent, Logstash, or API. For more information, see [Resources for creating Microsoft Sentinel custom connectors](create-custom-connector).

## Alternative data ingestion requirements

If the standard configuration for data collection doesn't work well for your organization, review these and possible [alternative solutions and considerations](best-practices-data#alternative-data-ingestion-requirements).

## Filter your logs

If you choose to filter your collected logs or log content before the data is ingested into Microsoft Sentinel, [review these best practices](best-practices-data#filter-your-logs-before-ingestion).