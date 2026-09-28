---
layout: Conceptual
title: Advanced Security Information Model (ASIM) known issues | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/normalization-known-issues
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
ms.reviewer: ofshezaf
description: This article outlines the Microsoft Sentinel Advanced Security Information Model (ASIM) known issues.
ms.author: edbaynash
author: EdB-MSFT
ms.topic: reference
ms.date: 2021-08-02T00:00:00.0000000Z
locale: en-us
document_id: 32d6b203-d700-ae2c-924f-4dd7ecdd0bea
document_version_independent_id: 5a0d3062-d19b-fc9e-50c7-bf1b4a83b783
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/normalization-known-issues.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/normalization-known-issues
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/normalization-known-issues.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
platformId: 6fa3b6be-2654-e2dd-d512-c8b34eeb7259
---

# Advanced Security Information Model (ASIM) known issues | Microsoft Learn

The following are the Advanced Security Information Model (ASIM) known issues and limitations:

## Sentinel data lake

ASIM query time parsers are not supported for lake explorer and KQL jobs.

## Performance challenges

ASIM based queries over a long time range, and which don't use filtering parameters, may be slow. Parsing is a resource-intensive operation, and when applied to a large, unfiltered, dataset, it's expected to be slow.

If you encounter performance issues:

- When using an interactive query, make sure to set the time picker to time range needed.
- Use parser filters. Most importantly use the `starttime` and the `endtime` filter parameters.

## The ingest\_time() function isn't supported

The `ingest_time()` function reports the time at which a record was ingested into Microsoft Sentinel, which may be different from `TimeGenerated`. This information is commonly used in queries that take into account ingestion delays. The `ingest_time()` has to be used in the context of a specific table and doesn't work with ASIM functions, which unify many different tables.

## Misleading informational message

In some cases when using ASIM parser functions, usually when there are no results to the query, the following information message is displayed.

![Screenshot of ASIM-related misleading informational message.](media/normalization/asim-error-message.png)

While the message is alarming, it's informational only, and the system behaved as expected. ASIM functions combine data from many sources, regardless of whether they're available in your environment or not. The message suggests that some of the sources aren't available in your environment.