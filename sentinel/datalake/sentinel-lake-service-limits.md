---
layout: Conceptual
title: Microsoft Sentinel data lake service limits - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/sentinel-lake-service-limits
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
description: Service limits for the Microsoft Sentinel data lake service.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: abhiag
ms.topic: concept-article
ms.custom: sentinel-graph
ms.date: 2025-07-09T00:00:00.0000000Z
locale: en-us
document_id: 5669114d-8a94-58c0-4fa3-83b5f2c1adf3
document_version_independent_id: 2c70f9ce-22e6-0c50-b37e-e41fabf23bfa
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/sentinel-lake-service-limits.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/sentinel-lake-service-limits
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/sentinel-lake-service-limits.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
platformId: 4021a488-eed0-38ea-4b68-365e3226dc35
---

# Microsoft Sentinel data lake service limits - Microsoft Security | Microsoft Learn

The following service parameters and limits apply to the Microsoft Sentinel data lake service.

## Service parameters and limits for tables, data management, and ingestion

Important

If your organization uses Customer-Managed Keys (CMK) for data encryption, be aware that CMK isn't supported for data stored in the Microsoft Sentinel data lake. Sentinel workspaces applying CMK aren't accessible via data lake experiences.

Any data ingested into the data lake, such as custom tables or transformed data is encrypted using Microsoft-managed keys.

Onboarding to the Microsoft Sentinel data lake may not fully align with your organization's encryption policies or data protection standards.

The following table lists the service parameters and limits for the Microsoft Sentinel data lake service related to table management, data ingestion, and retention. These limits include, but aren't limited to, Azure Resource Graph data, Microsoft 365 data, and data mirroring.

| Category | Parameter/limit |
| --- | --- |
| Workspaces per tenant | 20 workspaces |
| Lake Retention (Asset data) | 12 years |
| Lake Retention (Aux) | 12 years |
| Maximum size for field values (Log Analytics) | 32 KB (truncated above the limit) |
| Table setup latency during onboarding | 90-120 minutes |
| New table setup latency | 90-120 minutes |
| Switching data between tiers latency | 90-120 minutes |

For information on Log Analytics workspace ingestion limits, see [Log Analytics workspaces, data collection volume and retention](/en-us/azure/azure-monitor/fundamentals/service-limits#logs-ingestion-api).

## Service parameters and limits for VS Code Notebooks

The following section lists the service parameters and limits for Microsoft Sentinel data lake when using VS Code Notebooks.

| Category | Parameter/limit |
| --- | --- |
| Custom table in the analytics tier | Custom tables in analytics tier can't be deleted from a notebook; Use Log Analytics to delete these tables. For more information, see [Add or delete tables and columns in Azure Monitor Logs](/en-us/azure/azure-monitor/logs/create-custom-table?tabs=azure-portal-1%2Cazure-portal-2%2Cazure-portal-3#delete-a-table) |
| Gateway web socket timeout | 2 hours |
| Interactive query timeout | 2 hours |
| Interactive session inactivity timeout | 20 minutes |
| Language | Python |
| Graph query timeout | 7.5 minutes |
| Notebook job timeout | 8 hours |
| Max concurrent notebook jobs | 3, subsequent jobs are queued |
| Max concurrent users on interactive querying | 8-10 on Large pool |
| Session start-up time | Spark compute session takes about 5-6 minutes to start. You can view the status of the session at the bottom of your VS Code Notebook. |
| Supported libraries | Only [Azure Synapse libraries 3.4](https://github.com/microsoft/synapse-spark-runtime/tree/main#readme) and the Microsoft Sentinel Provider library for abstracted functions are supported for querying the data lake. Pip installs or custom libraries aren't supported. |
| VS Code UX limit to display records | 100,000 rows |

## Service parameters and limits for KQL queries in the lake tier

The following service parameters and limits apply when writing queries in the Microsoft Sentinel data lake.

Note

All limits in this table apply **per tenant**. There's no per-user limit. Interactive KQL queries and asynchronous KQL queries share the same rate-limit and concurrency counters.

When either the rate limit or the concurrency limit is exceeded, the request is **rejected** and not queued. The concurrency counter decrements as soon as a running query finishes, and the rate-limit counter resets every minute.

| Category | Parameter/limit |
| --- | --- |
| Rate limit per tenant | 30 queries per minute (combined interactive and async) |
| Concurrency per tenant | 10 concurrent queries (combined interactive and async) |
| Query result data | 64 MB. To override the default for a specific query, see [Query limits](/en-us/azure/data-explorer/kusto/concepts/querylimits) in the Kusto Query Language reference. |
| Query result rows | 500,000 rows. To override the default for a specific query, see [Query limits](/en-us/azure/data-explorer/kusto/concepts/querylimits) in the Kusto Query Language reference. |
| Query scope | Multiple workspaces |
| Query timeout | 4 minutes |
| Queryable time range | Up to 12 years, depending on data retention. |

## Service parameters and limits for KQL jobs

The following table lists the service parameters and limits for KQL jobs in the Microsoft Sentinel data lake.

Note

All limits in this table apply **per tenant**. There's no per-user limit. KQL jobs have their own concurrency quota and don't share counters with KQL queries.

When the concurrent-job-execution limit is exceeded, the request is **rejected** and not queued. The counter decrements as soon as a running job finishes.

| Category | Parameter/limit |
| --- | --- |
| Concurrent job execution per tenant | 5 |
| Job query execution timeout | 1 hour |
| Jobs per tenant (enabled jobs) | 100 |
| Number of output tables per job | 1 |
| Query scope | Multiple workspaces |
| Query time range | Up to 12 years |

## Service parameters and limits for KQL async queries

The following table lists the service parameters and limits for KQL async queries in the Microsoft Sentinel data lake.

Note

All limits in this table apply **per tenant**. There's no per-user limit. Asynchronous KQL queries share the same rate-limit and concurrency counters as interactive KQL queries; KQL jobs have their own separate quota.

When either the rate limit or the concurrency limit is exceeded, the request is **rejected** and not queued. The concurrency counter decrements as soon as a running query finishes, and the rate-limit counter resets every minute.

| Category | Parameter/limit |
| --- | --- |
| Rate limit per tenant | 30 queries per minute (combined with interactive KQL queries) |
| Concurrency per tenant | 10 concurrent queries (combined with interactive KQL queries) |
| Async query execution timeout | 1 hour |
| Cache duration | 24 hours |
| Number of times users can fetch cached results | Unlimited |
| Query scope | Multiple workspaces |
| Query time range | Up to 12 years |