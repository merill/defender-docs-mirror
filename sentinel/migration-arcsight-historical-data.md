---
layout: Conceptual
title: 'Microsoft Sentinel migration: Export ArcSight data to target platform | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/migration-arcsight-historical-data
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
description: Export historical data from ArcSight for migration to a target platform, and choose the appropriate export method based on your data volume and environment.
author: EdB-MSFT
ms.author: edbaynash
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 5e946aaa-59c1-f756-6881-58f528329038
document_version_independent_id: 3536b4cb-4700-cdd7-8679-85fc24b32669
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/migration-arcsight-historical-data.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/migration-arcsight-historical-data
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/migration-arcsight-historical-data.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: dfa2b290-7f43-0f5a-a9ae-30025d1d6d6f
---

# Microsoft Sentinel migration: Export ArcSight data to target platform | Microsoft Learn

This article describes how to export your historical data from ArcSight. After you complete the steps in this article, you can [select a target platform](migration-ingestion-target-platform) to host the exported data, and then [select an ingestion tool](migration-ingestion-tool) to migrate the data.

![Diagram illustrating steps involved in export and ingestion.](media/migration-export-ingest/export-data.png)

You can export data from ArcSight in several ways. Your selection of an export method depends on the data volumes and the deployed ArcSight environment. You can export the logs to a local folder on the ArcSight server or to another server accessible by ArcSight.

To export the data, use one of the following methods:

- ArcSight Event Data Transfer Tool: Use this option for large volumes of data, namely terabytes (TB).
- lacat tool: Use for volumes of data smaller than a TB.

## ArcSight Event Data Transfer tool

Use the Event Data Transfer tool to export data from ArcSight Enterprise Security Manager (ESM) version 7.x. To export data from ArcSight Logger, use the lacat utility.

The Event Data Transfer tool retrieves event data from ESM. This event data can be combined with unstructured data in addition to the CEF data. The Event Data Transfer tool exports ESM events in three formats: CEF, CSV, and key-value pairs.

To export data using the Event Data Transfer tool:

1. [Install and configure the Event Transfer Tool](https://www.microfocus.com/documentation/arcsight/arcsight-esm-7.6/ESM_AdminGuide/#ESM_AdminGuide/EventDataTransfer/EventDataTransfer.htm).
2. Configure the logs export to use a CSV format. For example, this command exports data recorded between 15:45 and 16:45 on May 4, 2016 to a CSV file:

    ```
        arcsight event_transfer -dtype File -dpath <***path***> -format csv -start "05/04/2016 15:45:00" -end "05/04/2016 16:45:00" 
    ```

## lacat utility

Use the lacat utility to export data from ArcSight Logger. lacat exports CEF records from a Logger archive file, and prints the records to `stdout`. You can redirect the records to a file, or pipe the file for further manipulation with options such as `grep` or `awk`.

To export data with the lacat utility:

1. [Download the lacat utility](https://github.com/hpsec/lacat). For large volumes of data, we suggest that you modify the script for better performance. [Download the Microsoft-modified lacat utility](https://aka.ms/lacatmicrosoft).
2. Follow the examples in the lacat repository on how to run the script.