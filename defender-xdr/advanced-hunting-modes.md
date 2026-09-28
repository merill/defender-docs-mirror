---
layout: Conceptual
title: Choose between guided and advanced modes for hunting in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-modes
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Guided hunting in Microsoft Defender XDR does not require KQL knowledge while advanced hunting allows you to write a query from scratch.
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- m365initiative-m365-defender
- tier2
ms.custom:
- msecd-doc-authoring-1014
- cx-ti
- cx-ah
- seo-marvel-apr2020
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: a781e6c8-b9bb-87e9-df6d-1161c75b744b
document_version_independent_id: a781e6c8-b9bb-87e9-df6d-1161c75b744b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-modes.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-modes
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-modes.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 12f4ce54-96b6-4a96-25ab-32c2a48d1e15
---

# Choose between guided and advanced modes for hunting in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

## Use guided and advanced modes in advanced hunting

You can find the **advanced hunting** page by going to the left navigation bar in the Microsoft Defender portal and selecting **Hunting** &gt; **Advanced hunting**. If the navigation bar is collapsed, select the hunting icon ![Screenshot of the Advanced hunting icon in the Microsoft Defender portal navigation bar](media/advanced-hunting-modes/hunting-icon.png).

In the **advanced hunting** page, two modes are supported:

- **Guided mode** – to query using the query builder
- **Advanced mode** – to query using the query editor using Kusto Query Language (KQL)

The main difference between the two modes is that the guided mode *does not* require the hunter to know KQL to query the database, while advanced mode requires KQL knowledge.

Guided mode features a query builder that has an easy-to-use, visual, building-block style of constructing queries through dropdown menus containing available filters and conditions. To use guided mode, see [Get started with guided hunting mode](advanced-hunting-modes#get-started-with-guided-hunting-mode).

Advanced mode features a query editor area where users can create queries from scratch. To use advanced mode, see [Get started with advanced hunting mode](advanced-hunting-modes#get-started-with-advanced-hunting-mode).

## Get started with guided hunting mode

Important

Some information relates to prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

When you open the advanced hunting page for the first time after guided mode (guided hunting) is made available to you, you are invited to take the tour to learn more about the different parts of the page like the tabs and query areas.

To take the tour, select **Take tour** when the guided hunting invitation banner appears:

[![Screenshot of the guided hunting prompt with an option to take the tour](media/advanced-hunting-modes/1-guided-hunting-banner-tb.png)](media/advanced-hunting-modes/1-guided-hunting-banner.png#lightbox)

Follow the blue teaching bubbles that appear throughout the page and select **Next** to continue through the tour.

You can take the tour again at any time by going to **Help resources** &gt; **Learn more** and selecting **Take the tour**.

![Screenshot of Help resources menu with Learn more and Take the tour options](media/advanced-hunting-modes/help-resources.png)

You can then start building your query to hunt for threats. The following articles can help you get the most out of hunting in guided mode:

| Learning goal | Description | Resource |
| --- | --- | --- |
| **Craft your first query** | Learn the basics of the query builder like specifying the data domain and adding conditions and filters to help you create a meaningful query. Learn further by running sample queries. | [Build hunting queries using guided mode](advanced-hunting-query-builder) |
| **Learn the different query builder capabilities** | Get to know the different supported data types and guided mode capabilities to help you fine-tune your query according to your needs. | [Refine your query in guided mode](advanced-hunting-query-builder-details) |
| **Learn what you can do with query results** | Get familiar with the Results view and what you can do with generated results like how to take action on them or link them to an incident. | - [Work with query results in guided mode](advanced-hunting-query-builder-results) - [Take action on query results](advanced-hunting-take-action) - [Link query results to an incident](advanced-hunting-link-to-incident) |
| **Create custom detection rules** | Understand how you can use advanced hunting queries to trigger alerts and take response actions automatically. | - [Custom detections overview](custom-detections-overview)- [Custom detection rules](custom-detection-rules) |

## Get started with advanced hunting mode

We recommend using the following learning resources to quickly get started with advanced hunting:

| Learning goal | Description | Resource |
| --- | --- | --- |
| **Learn the language** | Advanced hunting is based on [Kusto query language](/en-us/azure/kusto/query/), supporting the same syntax and operators. Start learning the query language by running your first query. | [Query language overview](advanced-hunting-query-language) |
| **Learn how to use the query results** | Learn about charts and various ways you can view or export your results. Explore how you can quickly tweak queries, drill down to get richer information, and take response actions. | - [Work with query results in advanced mode](advanced-hunting-query-results) - [Take action on query results](advanced-hunting-take-action) - [Link query results to an incident](advanced-hunting-link-to-incident) |
| **Understand the schema** | Get a good, high-level understanding of the tables in the schema and their columns. Learn where to look for data when constructing your queries. | - [Schema reference](advanced-hunting-schema-tables)- [Transition from Microsoft Defender for Endpoint](advanced-hunting-migrate-from-mde) |
| **Get expert tips and examples** | Train for free with guides from Microsoft experts. Explore collections of predefined queries covering different threat hunting scenarios. | - [Get expert training](advanced-hunting-expert-training)- [Use shared queries](advanced-hunting-shared-queries)- [Quickly investigate entities with Go hunt](advanced-hunting-go-hunt)- [Hunt for threats across devices, emails, apps, and identities](advanced-hunting-query-emails-devices) |
| **Optimize queries and handle errors** | Understand how to create efficient and error-free queries. | - [Query best practices](advanced-hunting-best-practices)- [Handle errors](advanced-hunting-errors) |
| **Create custom detection rules** | Understand how you can use advanced hunting queries to trigger alerts and take response actions automatically. | - [Custom detections overview](custom-detections-overview)- [Custom detection rules](custom-detection-rules) |