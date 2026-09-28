---
layout: Conceptual
title: Microsoft Sentinel Advanced Security Information Model (ASIM) parsers overview | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/normalization-parsers-overview
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
description: This article provides an overview of Advanced Security Information Model (ASIM) parsers and a link to more detailed ASIM parsers documents.
ms.author: edbaynash
author: EdB-MSFT
ms.topic: concept-article
ms.date: 2021-11-09T00:00:00.0000000Z
locale: en-us
document_id: 6882c803-0a9f-8b3e-3002-9c98da1d395a
document_version_independent_id: d220fee0-22fb-00c8-44d3-bca878cc5603
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/normalization-parsers-overview.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/normalization-parsers-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/normalization-parsers-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: c6cfeeae-ab94-3e45-c9d2-81fa37acfe39
---

# Microsoft Sentinel Advanced Security Information Model (ASIM) parsers overview | Microsoft Learn

In Microsoft Sentinel, parsing and [normalizing](normalization) happen at query time. Parsers are built as [KQL user-defined functions](/en-us/kusto/query/functions/user-defined-functions?view=microsoft-sentinel&amp;preserve-view=true) that transform data in existing tables, such as **CommonSecurityLog**, custom logs tables, or Syslog, into the normalized schema.

Users [use Advanced Security Information Model (ASIM) parsers](normalization-about-parsers) instead of table names in their queries to view data in a normalized format, and to include all data relevant to the schema in your query.

To understand how parsers fit within the ASIM architecture, refer to the [ASIM architecture diagram](normalization#asim-components).

## Built-in ASIM parsers and workspace-deployed parsers

ASIM parsers are built in and available out-of-the-box in every Microsoft Sentinel workspace.

ASIM also supports deploying parsers to specific workspaces [from GitHub](https://aka.ms/DeployASIM), using an ARM template. Workspace deployed parsers are used for ASIM parser development and management. Workspace deployed parsers are functionally equivalent, but have slightly different naming conventions, allowing both parser sets to coexist with built-in parsers in the same Microsoft Sentinel workspace. Read more about [workspace deployed parsers](normalization-about-workspace-parsers) to deploy, use and manage them.

It is recommended to use built-in parsers when developing ASIM content. Workspace deployed parsers are typically used during the parser development process or to provide modified versions of built-in parsers as described in [managing parsers](normalization-manage-parsers)

## Parser hierarchy and naming

ASIM includes two levels of parsers: **unifying** parser and **source-specific** parsers. The user usually uses the **unifying** parser for the relevant schema, ensuring all data relevant to the schema is queried. The **unifying** parser in turn calls **source-specific** parsers to perform the actual parsing and normalization, which is specific for each source.

The unifying parser name is `_Im_<schema>` where `<schema>` stands for the specific schema it serves. Source-specific parsers can also be used independently. Their naming convention is `_Im_<schema>_<source>V<version>`. You can find a list of source-specific parsers in the [ASIM parsers list](normalization-parsers-list).

Note

A corresponding set of parsers that use `_ASim_<schema>`. These parsers do not support filtering parameters and are provided for backward compatibility.

Tip

The parser hierarchy adds a layer to support customization. For more information, see [Managing ASIM parsers](normalization-develop-parsers).