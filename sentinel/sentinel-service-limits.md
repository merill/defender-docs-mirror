---
layout: Conceptual
title: Microsoft Sentinel service limits | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sentinel-service-limits
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
description: This article provides a list of service limits for Microsoft Sentinel, divided into the different service areas.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: reference
ms.date: 2025-03-19T00:00:00.0000000Z
locale: en-us
document_id: 0597602e-b5e1-b081-7c22-15c810cca7fe
document_version_independent_id: 34dfa7b4-6fdb-e356-3814-f5dfc54b7ed4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sentinel-service-limits.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/sentinel-service-limits
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sentinel-service-limits.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 93626a02-4e4c-9dfd-8392-46ee83cdf995
---

# Microsoft Sentinel service limits | Microsoft Learn

This article lists the most common service limits you might encounter as you use Microsoft Sentinel. For other limits that might impact services or features you use, like Azure Monitor, see [Azure subscription and service limits, quotas, and constraints](/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits).

## Analytics rule limits

The following limit applies to analytics rules in Microsoft Sentinel.

| Description | Limit | Dependency |
| --- | --- | --- |
| Number of [scheduled rules](scheduled-rules-overview) | 512 *enabled* rules, 1024 in total, including disabled rules.With a [dedicated cluster](/en-us/azure/azure-monitor/logs/logs-dedicated-clusters) - 1024 *enabled* rules, 2048 in total, including disabled rules. Requires a request to increase the default limit through a [support ticket](/en-us/azure/azure-portal/supportability/how-to-create-azure-support-request). | Counted separately from NRT rules |
| Number of [near-real-time (NRT) rules](near-real-time-rules) | 50 *enabled* rules, 100 in total, including disabled rules | Counted separately from scheduled rules |
| [Entity mappings](map-data-fields-to-entities) | 10 mappings per rule | None |
| [Entities](map-data-fields-to-entities) identified per alert(Divided equally among the mapped entities) | 500 entities per alert | None |
| [Entities](map-data-fields-to-entities) cumulative size limit | 64 KB | None |
| [Custom details](surface-custom-details-in-alerts) | 20 details per rule50 values per detail2 KB cumulative size | None |
| [Alert details](customize-alert-details) | 50 values per overridden field5 KB per field for `Description` and collections256 bytes per field for `AlertName` and non-collections | None |
| Alerts per ruleApplicable when *Event grouping* is set to *Trigger an alert for each event* | 150 alerts | None |
| Alerts per rule for NRT rules | 30 alerts | None |

## Hunts limits

The following limits apply to Hunts in Microsoft Sentinel.

| Description | Limit | Dependency |
| --- | --- | --- |
| Number of Hunts | 100 | None |

## Incident limits

The following limits apply to incidents in Microsoft Sentinel.

| Description | Limit | Dependency |
| --- | --- | --- |
| Investigation experience availability | 90 days from the incident last update time | None |
| Retention period for incident entities | 180 days | Entities database retention |
| Number of alerts | 150 alerts | None |
| Number of automation rules | 512 rules | None |
| Number of automation rule actions | 20 actions | None |
| Number of automation rule conditions | 50 conditions | None |
| Number of bookmarks | 20 bookmarks | None |
| Number of characters for automation rule name | 500 characters | None |
| Number of characters for description | 5,000 characters | None |
| Number of characters per comment | 30,000 characters | None |
| Number of comments per incident | 100 comments | None |
| Number of tasks | 40 tasks | None |
| Number of incidents returned by API to *list* request | 1,000 incidents maximum | None |
| Number of incidents per day (per workspace) | See explanation after table | Database capacity |

**Number of incidents per day:** There isn't a formal, hard limit on the number of incidents that can be created per day. A workspace's actual capacity for incidents depends on the storage capacity of the incident database, so the size of the incidents is as much a factor as their number.

However, a SOC that experiences the creation of more than *around* 3,000 new incidents per day will most likely find itself unable to keep up, and the database capacity will quickly be reached. In this situation, the SOC needs to find and fix any rules that create large numbers of incidents, to get the count of daily new incidents to manageable levels.

## Case management limits

The following limits apply to case management in Microsoft Sentinel.

| Description | Limit | Dependency |
| --- | --- | --- |
| Cases per tenant | 100,000 cases | None |
| Attachments per tenant | 500 GB | None |
| Linked incidents per case | 100 incidents | None |

## Machine learning-based limits

The following limits apply to machine learning-based features in Microsoft Sentinel like customizable anomalies and Fusion.

| Description | Limit | Dependency |
| --- | --- | --- |
| Number of anomalies published per anomaly type | Top 3000 ranked by anomaly score | None |
| Number of alerts and/or anomalies in a single Fusion incident | 100 alerts and/or anomalies | None |

## Multi workspace limits

The following limit applies to multiple workspaces in Microsoft Sentinel. Limits here are applied when working with Sentinel features across more than workspace at a time.

| Description | Limit | Dependency |
| --- | --- | --- |
| Incident view | 100 concurrently displayed workspaces |  |
| Log query | 100 Sentinel workspaces | [Log Analytics](/en-us/azure/azure-monitor/logs/cross-workspace-query#limitations) |
| Analytics rules | 20 Sentinel workspaces per query |  |

## Notebook limits

The following limits apply to notebooks in Microsoft Sentinel. The limits are related to the dependencies on other services used by notebooks.

| Description | Limit | Dependency |
| --- | --- | --- |
| Total count of these assets per machine learning workspace: datasets, runs, models, and artifacts | 10 million assets | Azure Machine Learning |
| Default limit for total compute clusters per region. Limit is shared between a training cluster and a compute instance. A compute instance is considered a single-node cluster for quota purposes. | 200 compute clusters per region | Azure Machine Learning |
| Storage accounts per region per subscription | 250 storage accounts | Azure Storage |
| Maximum size of a file share by default | 5 TB | Azure Storage |
| Maximum size of a file share with large file share feature enabled | 100 TB | Azure Storage |
| Maximum throughput (ingress + egress) for a single file share by default | 60 MB/sec | Azure Storage |
| Maximum throughput (ingress + egress) for a single file share with large file share feature enabled | 300 MB/sec | Azure Storage |

## Repositories limits

The following limits apply to repositories in Microsoft Sentinel.

| Description | Limit | Dependency |
| --- | --- | --- |
| Number of repositories | 5 | Sentinel Workspace |
| Deployment history | 800 | Azure Resource Group |

## Threat intelligence limits

The following limit applies to threat intelligence in Microsoft Sentinel. The limit is related to the dependency on an API used by threat intelligence.

| Description | Limit | Dependency |
| --- | --- | --- |
| Indicators per call that use Graph security API | 100 indicators | Microsoft Graph security API |
| CSV TI object file import size | 50MB | none |
| JSON TI object file import size | 250MB | none |

## TI upload API limits

The following limit applies to the threat intelligence upload API in Microsoft Sentinel.

| Description | Limit | Dependency |
| --- | --- | --- |
| STIX objects per request | 100 objects |  |
| Requests per minute | 100 |  |

## User and Entity Behavior Analytics (UEBA) limits

The following limit applies to UEBA in Microsoft Sentinel. The limit for UEBA in Microsoft Sentinel is related to dependencies on another service.

| Description | Limit | Dependency |
| --- | --- | --- |
| Lowest retention configuration in days for the [IdentityInfo](/en-us/azure/azure-monitor/reference/tables/identityinfo) table. All data stored on the IdentityInfo table in Log Analytics is refreshed every 14 days. | 14 days | Log Analytics |
| Groups listed in the *GroupMembership* field in the [IdentityInfo](ueba-reference#identityinfo-table) table (including subgroups) | 500 |  |

## Watchlist limits

The following limits apply to watchlists in Microsoft Sentinel. The limits are related to the dependencies on other services used by watchlists.

| Description | Limit | Dependency |
| --- | --- | --- |
| Upload size limit for local filefiles over this limit are considered `large` | 3.8 MB per file | Azure Resource Manager |
| Line entry in the CSV file | 10,240 characters per line | Azure Resource Manager |
| Total size of a single row | 10 Kb | Log Analytics |
| Upload size for large watchlist files in Azure Storage | 500 MB per file | Azure Storage |
| Total number of active watchlist items per workspaceWhen the max count is reached, delete some existing items to add a new watchlist. | 10 million active watchlist items | Log Analytics |
| Total rate of change of all watchlist items per workspace(create, update, and delete operations) | 100,000 changes per month(1% of max active watchlist items) | Log Analytics |
| Number of `large` watchlist uploads per workspace at a timeSee upload size limit for what makes a watchlist `large` | One `large` watchlist | Azure Cosmos DB |
| Number of large watchlist deletions per workspace at a timeSee upload size limit for what makes a watchlist `large` | One `large` watchlist | Azure Cosmos DB |

## Workbook limits

Workbook limits for Sentinel are the same result limits found in Azure Monitor. For more information, see [Workbooks result limits](/en-us/azure/azure-monitor/visualize/workbooks-limits).

## Workspace manager limits

The following limits apply to workspace manager in Microsoft Sentinel.

| Description | Limit | Dependency |
| --- | --- | --- |
| Number of published operations in a group*Published operations* = (*member workspaces*) \* (*content items*) | 2000 published operations | None |