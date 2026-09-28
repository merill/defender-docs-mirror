---
layout: Conceptual
title: KQL Jobs, Summary Rules, and Search Jobs - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/kql-jobs-summary-rules-search-jobs
breadcrumb_path: ../breadcrumb/toc.json
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
ms.subservice: sentinel-platform
search.appverid: met150
description: A comparison of KQL jobs, summary rules, and search jobs in Microsoft Sentinel to choose the best tool for querying and analyzing security data.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: zeinam
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: ms-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: e052abd7-c7b0-7217-2290-f2c6d1b43e93
document_version_independent_id: 87a2ad4e-ff67-6d5e-1ed7-7be0f426e8cd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/kql-jobs-summary-rules-search-jobs.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/kql-jobs-summary-rules-search-jobs
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/kql-jobs-summary-rules-search-jobs.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
platformId: 36f6cf5e-7cc2-032d-66e8-e3925796aaf5
---

# KQL Jobs, Summary Rules, and Search Jobs - Microsoft Security | Microsoft Learn

## Overview

KQL jobs, summary rules, and search jobs let you query and analyze data in Microsoft Sentinel. Each serves different purposes and use cases.

Note

KQL jobs require onboarding to the Microsoft Sentinel data lake. For more information, see [Onboard to the Microsoft Sentinel data lake](sentinel-lake-onboarding).

- **KQL jobs**: Run one-time or scheduled asynchronous queries on data stored in the Microsoft Sentinel data lake. KQL jobs are best for incident investigations using historical logs, enrichment using low-fidelity logs, and scenarios that need queries with joins or unions across multiple tables. For more information, see [KQL jobs](kql-jobs).
- **Summary rules**: Run frequent summarization jobs to aggregate high volume data such as network and firewall logs. Summary rules run in the background and store results in custom tables in the analytics tier. For more information, see [Summary rules](../summary-rules).
- **Search jobs**: Run one-time, long-running asynchronous queries across large datasets. Search jobs are useful when you need to hydrate large volumes of data from a single table into a new custom table within the analytics tier for further investigation or forensic analysis. For more information, see [Search jobs](../search-jobs).

## Usage scenarios and feature choice

Use the guidance below to decide which feature best fits your needs.

If you have any of the following requirements, use KQL jobs:

- You need to query up to 12 years of historical data.
- You need to run complex queries involving full KQL operators including joins or unions.
- You need scheduled or ad-hoc investigation capabilities.

Use summary rules if you have any of the following requirements:

- Data is in a workspace that isn't onboarded to Microsoft Sentinel data lake, for example, data in Auxiliary or Basic tiers.
- You need frequent summarization, for example, every 20 minutes.
- You want to use out-of-the-box summary rules templates.

If you have any of the following requirements, use search jobs:

- You have data in archive tier. If you're onboarded to Microsoft Sentinel data lake, to access data older than your onboarding date, use search jobs. For data from your onboarding date onward, use KQL jobs.
- You need to hydrate large volumes of data from a single table.

## Feature comparison

The following table compares KQL jobs, summary rules, and search jobs across scope, limits, and pricing.

| Feature | KQL Jobs | Summary Rules | Search jobs |
| --- | --- | --- | --- |
| **Source data tier** | Microsoft Sentinel data lake tier | Analytics, auxiliary, basic, data lake (except for tables in System tables) | Analytics, data lake (except for tables in System tables). For non-data-lake workspaces: Auxiliary, Basic, Archived tier |
| **Workspace scope** | Any Microsoft Sentinel workspace connected to Microsoft Defender | Any Microsoft Sentinel workspace connected to Microsoft Defender | Any Microsoft Sentinel workspace |
| **Table scope** | Multiple tables | Multiple tables | Single table |
| **Can query federated tables** | Yes | No | No |
| **Query language** | [KQL jobs supported operators](/en-us/azure/sentinel/datalake/kql-jobs#considerations-and-limitations) | Limited [KQL operators](/en-us/azure/azure-monitor/logs/summary-rules?tabs=api#create-or-update-a-summary-rule) | [Limited KQL operators](/en-us/azure/azure-monitor/logs/search-jobs#kql-query-considerations) |
| **Join support** | Supported | Analytics tier: supported; Basic: join up to five Analytics tables using [`lookup()`](/en-us/azure/data-explorer/kusto/query/lookup-operator) operator | Not supported |
| **Scheduling frequency** | On-demand; Daily, weekly, monthly | 20 minutes to 24 hours | On-demand (long-running searches support up to a 24‑hour timeout) |
| **Lookback period** | Up to 12 years | Up to 1 day | Up to 12 years |
| **Timespan** | - | - | Up to 1 year |
| **Timeout** | 1 hour | 10 minutes | 24 hours |
| **Maximum number of results** | Dependent on query timeout | 500,000 records | 100 million records |
| **Pricing model** | GB of data analyzed | Analytics tier: free; Basic and auxiliary tier: Data scan (Log Analytics pricing model) | GB of data analyzed |
| **Template support** / Health monitoring | Template Support: NoHealth Monitoring: No | Template Support: Yes (Content Hub, ARM)Health Monitoring: LASummaryLogs | Template Support: NoHealth Monitoring: No |