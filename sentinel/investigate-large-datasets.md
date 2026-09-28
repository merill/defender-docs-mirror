---
layout: Conceptual
title: Start an Investigation by Searching Large Datasets | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/investigate-large-datasets
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
description: Learn about search jobs and restoring data from long-term retention in Microsoft Sentinel.
author: EdB-MSFT
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.author: edbaynash
ms.collection: usx-security
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 9f579d00-e58e-52f5-45e5-ade77da550cc
document_version_independent_id: edb0636c-e9af-f8ab-fa68-b5cbde3e24b8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/investigate-large-datasets.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/investigate-large-datasets
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/investigate-large-datasets.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 292cee78-c79f-c505-ebfa-85089af622de
---

# Start an Investigation by Searching Large Datasets | Microsoft Learn

One of the primary activities of a security team is to search logs for specific events. For example, you might search logs for the activities of a specific user within a given time-frame.

In Microsoft Sentinel, you can search across long time periods in extremely large datasets by using a search job. Although you can run a search job on any type of log, search jobs are ideally suited to search logs in a long-term retention (formerly known as archive) state. If you need to do a full investigation on such data, you can restore that data into an interactive retention state (like your regular Log Analytics tables) to run high performing queries and deeper analysis.

This article shows you how to run search jobs on large datasets, restore archived log data for deeper investigation, and bookmark search results.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Search large datasets

Use a search job to retrieve data stored in [long-term retention](/en-us/azure/azure-monitor/logs/data-retention-configure#interactive-long-term-and-total-retention), or to scan through large volumes of data, if the log query time-out of 10 minutes isn't sufficient. Search jobs are asynchronous queries that fetch records into a search table in your Log Analytics workspace. The search job uses parallel processing to search across long time spans in extremely large datasets, so search jobs don't impact the workspace's performance or availability.

Search results are stored in a table named with a `_SRCH` suffix.

The following screenshot shows example search criteria for a search job.

![Screenshot of search page with search criteria of administrator, time range last 1 year, and a table selected.](media/investigate-large-datasets/search-job-criteria.png)

## Restore log data from long-term retention

When you need to do a full investigation on log data in long-term retention, restore a table from the **Search** page in Microsoft Sentinel. Specify a target table and time range for the data you want to restore. Within a few minutes, the log data is restored and available within the Log Analytics workspace. Then you can use the data in high-performance queries that support full KQL.

A restored log table is available in a new table that has a `*_RST` suffix. The restored data is available as long as the underlying source data is available. But you can delete restored tables at any time without deleting the underlying source data. To save costs, we recommend you delete the restored table when you no longer need it.

The restore option appears on a saved search, as shown in the screenshot.

![Screenshot of the restore link on a saved search.](media/investigate-large-datasets/search-results-restore.png)

### Limitations of log restore

See [Restore limitations](/en-us/azure/azure-monitor/logs/restore#limitations) in the Azure Monitor documentation.

## Bookmark search results or restored data rows

Similar to the [threat hunting dashboard](hunting#use-the-hunting-dashboard), bookmark rows that contain information you find interesting so you can attach them to an incident or refer to them later. For more information, see [Create bookmarks](hunting#create-bookmarks).