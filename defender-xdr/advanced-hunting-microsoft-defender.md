---
layout: Conceptual
title: Advanced hunting with Microsoft Sentinel data in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-microsoft-defender
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to use advanced hunting in the portal unifying Defender XDR and Sentinel data
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- m365initiative-m365-defender
- tier1
- usx-security
ms.custom:
- cx-ti
- cx-ah
ms.topic: concept-article
ms.date: 2026-06-09T00:00:00.0000000Z
locale: en-us
document_id: 485b66a5-0967-f695-8102-d7278977a3af
document_version_independent_id: 485b66a5-0967-f695-8102-d7278977a3af
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-microsoft-defender.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-microsoft-defender
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-microsoft-defender.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: b7cd008b-8c9f-ae32-38b8-d6ce55fb23f1
---

# Advanced hunting with Microsoft Sentinel data in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn

Advanced hunting enables you to view and query all the data sources available within the [unified Microsoft Defender portal](/en-us/defender-xdr/microsoft-365-defender-portal). These data sources include Microsoft Defender XDR and various Microsoft security services. If you onboard Microsoft Sentinel to the Defender portal, you can also access and use all your existing Microsoft Sentinel workspace content, including queries and functions.

Querying from a single portal across different data sets makes hunting more efficient and removes the need for context-switching.

Important

Microsoft Sentinel is generally available in the Microsoft Defender portal, with or without Microsoft Defender XDR or an E5 license. For more information, see [Microsoft Sentinel in the Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2263690).

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal.

If you're currently using Microsoft Sentinel in the Azure portal, we recommend that you start planning your transition to the Defender portal now to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview). For more information, see [Transition your Microsoft Sentinel environment to the Defender portal](/en-us/azure/sentinel/move-to-defender) and [Planning your move to Microsoft Defender portal for all Microsoft Sentinel customers](https://techcommunity.microsoft.com/blog/microsoft-security-blog/planning-your-move-to-microsoft-defender-portal-for-all-microsoft-sentinel-custo/4428613) (blog).

## How to access

### Required roles and permissions

You can query data in any workload that you can currently access based on your roles and permissions.

To query across Microsoft Sentinel and Microsoft Defender data in the unified advanced hunting page, you need at least the Microsoft Sentinel Reader role. For more information, see [Microsoft Sentinel-specific roles](/en-us/azure/sentinel/roles#microsoft-sentinel-specific-roles).

### Connect a workspace

In Microsoft Defender, you can connect workspaces by selecting **Connect a workspace** in the top banner. This button appears if you're eligible to onboard a Microsoft Sentinel workspace onto the unified Microsoft Defender portal. Follow the steps in: **[Onboarding a workspace](https://aka.ms/onboard-microsoft-sentinel)**.

After connecting your Microsoft Sentinel workspace and Microsoft Defender XDR advanced hunting data, you can start querying Microsoft Sentinel data from the advanced hunting page. For an overview of advanced hunting features, read [Proactively hunt for threats with advanced hunting](advanced-hunting-overview).

## What to expect for Defender XDR tables streamed to Microsoft Sentinel

- **Use tables with longer data retention periods in queries** – Advanced hunting follows the maximum data retention period you set for the Defender tables (see [Understand quotas](advanced-hunting-limits#understand-advanced-hunting-quotas-and-usage-parameters)). If you [stream Defender tables](/en-us/defender-xdr/streaming-api) to Microsoft Sentinel and set a data retention period longer than 30 days for those tables, you can query for the longer period in advanced hunting.
- **Use Kusto operators you use in Microsoft Sentinel** – In general, queries from Microsoft Sentinel work in advanced hunting, including queries that use the `adx()` operator. IntelliSense might warn you that the operators in your query don't match the schema. However, you can still run the query and it should execute successfully.
- **Use the time filter dropdown instead of setting the time span in the query** – If you're filtering ingestion of Defender tables to Sentinel instead of streaming the tables as is, don't filter the time in the query as this action might generate incomplete results. If you set the time in the query, the streamed, filtered data from Sentinel is used because it usually has the longer data retention period. If you want to make sure you're querying all Defender data for up to 30 days, use the time filter dropdown provided in the query editor instead.
- **View `SourceSystem` and `MachineGroup` columns for Defender data that you stream from Microsoft Sentinel** – Since the columns `SourceSystem` and `MachineGroup` are added to Defender tables once you stream them to Microsoft Sentinel, they also appear in results in advanced hunting in Defender. However, they remain blank for Defender tables that you don't stream (tables that follow the default 30-day data retention period).

Note

Using the unified portal, where you can query Microsoft Sentinel data after connecting a Microsoft Sentinel workspace, doesn't automatically mean you can also query Defender data while in Microsoft Sentinel. You still need to configure raw data ingestion of Defender in Microsoft Sentinel for this to happen.

Important

Microsoft Government Community Cloud Moderate (GCC-M) customers should be aware of the following limitation in advanced hunting:

- Queries that reference both Microsoft Sentinel and Defender tables aren't supported. If you use *Search* or *Union \** in your queries, consider replacing the *\** with an explicit list of tables that are limited to Microsoft Sentinel only or Defender only.

## Where to find your Microsoft Sentinel data

You can use advanced hunting KQL (Kusto Query Language) queries to hunt through Microsoft Defender XDR and Microsoft Sentinel data.

When you open the advanced hunting page for the first time after connecting a workspace, you can find many of that workspace's tables organized by solution after the Microsoft Defender tables under the **Schema** tab.

[![Screenshot of advanced hunting schema tab in the Microsoft Defender portal highlighting location of Sentinel tables](media/advanced-hunting-microsoft-defender/advanced-hunting-unified-sentinel-data.png)](media/advanced-hunting-microsoft-defender/advanced-hunting-unified-sentinel-data.png#lightbox)

Likewise, you can find the functions from Microsoft Sentinel in the **Functions** tab, and your shared and sample queries from Microsoft Sentinel can be found in the **Queries** tab inside folders marked **Sentinel**.

## View schema information

To learn more about a schema table, select the vertical ellipses ( ![kebab icon](/en-us/defender/media/ah-kebab.png) ) to the right of any schema table name under the **Schema** tab, and then select **View schema**.

In the unified portal, you can view the schema column names and descriptions, as well as the following information:

- Sample data – select **See preview data**, which loads a simple query like `TableName | take 5`
- **Schema type** – whether the table supports full query capabilities (advanced table) or not (basic logs table)
- **Data retention period** – how long the data is set to be kept
- **Tags** – available for Sentinel data tables

[![Screenshot of the schema information pane in the Microsoft Defender portal](media/advanced-hunting-microsoft-defender/advanced-hunting-unified-view-schema.png)](media/advanced-hunting-microsoft-defender/advanced-hunting-unified-view-schema.png#lightbox)

## Known issues

- Guided hunting mode and take actions capabilities support Defender XDR data only.
- Custom detections have the following limitations:
    - Near real-time detection frequency isn't available for detections that include Microsoft Sentinel data.
    - Custom functions that you create and save in Microsoft Sentinel aren't supported.
- Bookmarks aren't supported in the advanced hunting experience. They're supported in the **Microsoft Sentinel &gt; Threat management &gt; Hunting** feature. Alternatively, you can use the [Link to incident](advanced-hunting-defender-results#link-query-results-to-an-incident) feature to link query results to new or existing incidents.
- If you're streaming Defender XDR tables to Log Analytics, there might be a difference between the `Timestamp` and `TimeGenerated` columns. If the data arrives to Log Analytics after 48 hours, the ingestion process overrides it to `now()`. Therefore, to get the actual time the event happened, rely on the `Timestamp` column.
- When prompting [Security Copilot](advanced-hunting-security-copilot) for advanced hunting queries, you might find that not all Microsoft Sentinel tables are currently supported. However, support for these tables can be expected in the future.
- When a query contains a function with a time range defined within the function, the time range applied through the advanced hunting or custom detections UI overrides the function's intended time scope instead of using the **Set in query** option.
- New Microsoft Sentinel customers can use advanced hunting in Microsoft Defender to query Analytics and Lake tier tables. However, when an Analytics table is configured with extended retention in the Lake tier, advanced hunting interactive queries can access only data within the Analytics retention period. For example, if the `SigninLogs` table is configured with 90 days of retention in the Analytics tier and two years of total retention, advanced hunting can query only the most recent 90 days. Data retained beyond the Analytics retention period in the Lake tier should be accessed using [search jobs](/en-us/azure/azure-monitor/logs/search-jobs).
- Advanced hunting might display an incorrect schema type for tables in the Lake tier. Lake tier tables use a gold table icon and should display **Lake / Auxiliary logs table** as their schema type, but might instead display **Advanced table**.