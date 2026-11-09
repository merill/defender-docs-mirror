---
layout: Conceptual
title: Manage data tiers and retention in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/manage-data-overview
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
description: Manage log data in Microsoft Sentinel and with Microsoft Defender XDR services in the Microsoft Defender portal to optimize security operations and cost efficiency.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-08-24T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 4b97dc23-6530-6d86-149a-80e8d209fdde
document_version_independent_id: 5d097f39-b710-46be-aa1b-c4c1bd7f3aad
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/manage-data-overview.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/manage-data-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/manage-data-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
platformId: ad3cbb72-db10-6bde-479f-bf28fba0e2a0
---

# Manage data tiers and retention in Microsoft Sentinel | Microsoft Learn

The Microsoft Defender portal provides a centralized experience for managing Microsoft Sentinel and Microsoft Defender XDR data. The **Data & connectors** experience consolidates connector management, table management, transformations, and ingestion health monitoring into a single view, so you can understand and optimize your security data without navigating between separate pages.

This article introduces the **Data & connectors** experience and explains how to use it to manage data in Microsoft Sentinel and Microsoft Defender XDR. For related tasks, see:

- [Configure data connectors](configure-data-connector) to send data to Microsoft Sentinel or Microsoft Defender XDR.
- [Manage your existing tables and data](manage-table-tiers-retention).

## Data & connectors in the Microsoft Defender portal (preview)

Important

The **Data & connectors** experience is currently in PREVIEW. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

The **Data & connectors** experience brings connector management, table management, transformations, and ingestion health monitoring together into a single view in the Microsoft Defender portal. Use it to understand and manage your Microsoft Sentinel data without navigating between separate pages.

[![Screenshot of the Data and connectors page showing the Overview, Connectors, and Tables tabs.](media/manage-data-overview/data-and-connectors-tabs.png)](media/manage-data-overview/data-and-connectors-tabs.png#lightbox)

To open the experience, in the Microsoft Defender portal, select **Setup & configuration** &gt; **Data & connectors**. The page includes three tabs:

- Overview tab — Workspace-level ingestion health dashboard.
- Connectors tab — Centralized inventory of data connectors, including classic Sentinel connectors and unified connectors.
- Tables tab — Table management, schema exploration, transformations, and retention.

### Prerequisites

To use the **Data & connectors** experience in preview, you need:

- Unified role-based access control (URBAC) enabled in the Microsoft Defender portal.
- **Data (manage)** permission in the **Data Operations** permission group.
- Workspace permissions equivalent to **Log Analytics Contributor**, including:
    - `Microsoft.OperationalInsights/workspaces/write`
    - `Microsoft.OperationalInsights/workspaces/tables/write`

### Known limitations

The following limitations apply to the preview:

- The **Data Sources** tab on the table details panel appears only for federated tables. Support for other table types is planned.
- The **Data & connectors** experience is available in the commercial cloud only. Sovereign clouds, including US Government and China, aren't supported.

## Overview tab

The **Overview** tab is a workspace-level dashboard that surfaces ingestion health signals so you can act on issues before they impact detections. Filter by time range and workspace to scope the dashboard.

The Overview tab includes:

- **Ingestion volume** — Daily ingestion split by Analytics tier and Data Lake tier for the selected time range.
- **Connectors that need attention** — Connectors with credential errors, ingestion failures, or outages, along with the error type, failure count in the last 24 hours, and last successful ingestion.
- **Table ingestion fluctuations** — Tables with unexpected volume changes compared to the same day the previous week, grouped as spikes and drops. You can adjust the fluctuation thresholds.
- **Data ingestion volume by table** — Top ingesting tables ranked by daily volume, so you can identify high-volume tables driving ingestion costs.
- **Ingestion latency by table** — The time between data generation and availability in your environment, so you can identify connector throttling or source-side delays.

[![Screenshot of Overview health insights showing ingestion volume, a connector that needs attention, and table ingestion fluctuations.](media/manage-data-overview/overview-data-health-insights.png)](media/manage-data-overview/overview-data-health-insights.png#lightbox)

[![Screenshot of the Data ingestion volume by table chart showing daily volume trends for the top 10 tables.](media/manage-data-overview/overview-ingestion-volume-by-table.png)](media/manage-data-overview/overview-ingestion-volume-by-table.png#lightbox)

[![Screenshot of the Ingestion latency by table chart showing P95 latency trends for all tables.](media/manage-data-overview/overview-ingestion-latency-by-table.png)](media/manage-data-overview/overview-ingestion-latency-by-table.png#lightbox)

## Connectors tab

The **Connectors** tab brings [unified data connectors](unified-connector) and [Sentinel classic data connectors](connect-data-sources) together in a single inventory. Use it to review connector health, add new connectors, or open a connector's details view.

The Connectors tab includes:

- **Unified connector inventory** — All onboarded connectors, with status, provider, content source, and available updates.
- **Toggle between unified and classic connectors** — Use the classic connectors selector to switch between the [unified connector](unified-connector) catalog and the [Sentinel classic data connectors](connect-data-sources) inventory, which includes connectors built with the [Codeless Connector Framework (CCF)](isv/create-codeless-connector).
- **Filter by provider, data type, and status** — Narrow the list to find specific connectors quickly.
- **Data onboarding assistant** — Guided flow to add new connectors.
- **Create custom connector** — Start a new custom connector from the Connectors tab.

[![Screenshot of the connector selector with Sentinel under Classic connectors and My connectors under Unified connectors.](media/manage-data-overview/connector-type-selector.png)](media/manage-data-overview/connector-type-selector.png#lightbox)

## Tables tab

Data you collect into Microsoft Sentinel and Microsoft Defender XDR is stored in tables. The **Tables** tab is where you view your tables, review their ingestion health, inspect their schema and transformations, and manage the retention period and storage costs associated with your data.

### Which tables can you manage in the Microsoft Defender portal?

This section describes the table types you can manage in the Microsoft Defender portal.

[![Screenshot that shows the Table Management screen in the Defender portal.](media/manage-data-overview/view-table-properties-microsoft-defender-portal.png)](media/manage-data-overview/view-table-properties-microsoft-defender-portal.png#lightbox)

| Table type | Description | Examples | Is in Microsoft Sentinel workspace? |
| --- | --- | --- | --- |
| **Microsoft Sentinel** | Built-in tables, including:- Azure tables, such as AzureDiagnostics and SigninLogs.- Microsoft Sentinel tables.- [Microsoft Defender XDR integration with Microsoft Sentinel](connect-microsoft-365-defender?tabs=MDE#connect-events), which are created in your Microsoft Sentinel workspace when you increase the analytics retention period beyond 30 days. See the **XDR** table type for Defender XDR tables that are currently unsupported. | - Azure tables: `AzureDiagnostics`, `SigninLogs`- Microsoft Sentinel tables: `AWSCloudTrail`, `SecurityAlert`- XDR tables: `DeviceEvents`,`AlertInfo` | Yes |
| **Custom** | Tables you create manually or through jobs in your Microsoft Sentinel workspace, including summary rule and search job results tables, and custom data source tables. | Tables with `_CL` or `_SRCH` suffixes. | Yes |
| **XDR** | Tables in the XDR default tier, which have 30 days of analytics retention by default. You can view these tables, but you can't manage them from the Defender portal. | `IdentityInfo` | No |

Note

You can view Basic Logs tables in your Microsoft Sentinel workspace from the Microsoft Defender portal, but you can currently manage them only from your Log Analytics workspace. To manage these tables from the Microsoft Defender portal, change the table plan from Basic Logs to Analytics in your Microsoft Sentinel workspace.

### How data tiers and retention work

You can retain data in Microsoft Sentinel in one of two tiers:

- **Analytics tier**: This tier makes data available for alerting, hunting, workbooks, and all Microsoft Sentinel features. It retains data in two states:

    - **Analytics retention**: In this "hot" state, data is fully available for real-time analytics, including high-performance queries, analytics rules, and threat hunting. By default, Microsoft Sentinel and Microsoft Defender XDR retain data in this tier for 30 days. You can extend the retention period of all tables to up to two years at a prorated monthly long-term retention charge. You can extend the retention period of Microsoft Sentinel solution tables to 90 days for free.
    - **Total retention**: By default, all data in the analytics tier is mirrored to the data lake for the same retention period. You can extend the retention of your data in the lake beyond the analytics retention, for up to 12 years of total retention at a low cost.
- **Data Lake tier**: In this low-cost "cold" tier, Microsoft Sentinel retains your data in the data lake only. Data in the Data Lake tier isn't available for real-time analytics features and threat hunting. However, you can access data in the lake whenever you need it through [KQL jobs](datalake/kql-jobs), analyze trends over time by running scheduled KQL or Spark jobs, and aggregate insights from incoming data at a regular cadence by using summary rules.
- **XDR data**: By default, Microsoft Defender XDR threat hunting data is always available in the Analytics tier for 30 days. You can extend retention of this data in the Analytics tier up to 90 days, which incurs ingestion costs, while storage remains free. Extending retention beyond 90 days in the Analytics tier also incurs storage costs. You can also ingest exclusively into the Data Lake tier, but the data remains available in the Analytics tier for 30 days. Ingesting XDR data directly into the Data Lake tier is more cost-effective, but it involves ingestion, storage, and processing costs. In this option, customers still get 30 days' worth of data in the Analytics tier at no additional cost.

For more information about the differences between the Analytics tier and the Data Lake tier, see Compare the analytics and data lake tiers.

The following diagram illustrates the retention components of the Analytics, Data Lake, and XDR default tiers, and the table types that apply to each tier:

[![Diagram that depicts the analytics and data lake tiers in the Microsoft Defender portal.](media/manage-data-overview/tiers-retention-defender-portal.png)](media/manage-data-overview/tiers-retention-defender-portal.png#lightbox)

For more information about the Microsoft Sentinel data lake, see [What is Microsoft Sentinel data lake](datalake/sentinel-lake-overview).

### Use Table insights for table-level observability

Table insights on the **Tables** tab helps you understand ingestion health at the table level for the selected Microsoft Sentinel workspace. It gives you quick observability signals so you can identify ingestion and cost patterns before you change tier or retention settings.

Table insights signals appear in two places on the **Tables** tab:

- **Summary tiles at the top of the page** show workspace-level counts, including the number of tables and how they're distributed across the Analytics tier, Data Lake tier, and XDR default tier.
- **Columns in the tables grid**show per-table health signals for each table, including:
    - Last data received
    - Average daily ingestion volume
    - Estimated daily ingestion cost
    - Volume anomaly (day-over-week ingestion fluctuation)

Use the grid columns to sort, filter, and compare tables side by side. Combine these signals to detect connector failures, investigate cost spikes, validate new connector onboarding, and identify candidates for right-sizing retention and tier.

[![Screenshot of the Tables grid showing filters and table insights columns for tier, last data received, average daily ingestion, estimated daily cost, volume anomaly, and retention.](media/manage-data-overview/table-insights-grid.png)](media/manage-data-overview/table-insights-grid.png#lightbox)

Important

Table insights is a visualization surface for investigation. It isn't a billing-grade or alerting surface.

For setup, access, and interpretation guidance, see [Configure table settings in Microsoft Sentinel](manage-table-tiers-retention#use-table-insights-to-monitor-table-health).

### Table details panel

Select a table on the **Tables** tab to open the table details panel. The panel consolidates schema, transformations, and retention information for the selected table. It includes the following tabs:

| Tab | What it shows |
| --- | --- |
| **Overview** | Table type, tier, analytics retention, total retention, and other table metadata. |
| **Schema** | Column names, data types, and column descriptions for the selected table. Use this tab to inspect schema without running KQL queries. |
| **Transformations** | Filter, Split, and Scope Tag transformation rules that apply to the table. You can view, create, edit, and delete transformation rules from this tab. |
| **Retention** | Analytics retention and total retention settings for the table. |
| **Data Sources** | Connector information for the table. This tab appears only for federated table types. |

### Compare the analytics and data lake tiers

This table compares the Analytics and Data Lake tiers and their key characteristics:

| Comparison | Analytics tier | Data Lake tier |
| --- | --- | --- |
| Key characteristics | High-performance querying and indexing for logs (also known as hot, or interactive retention). | Cost-effective long-term retention of large data volumes (also known as cold storage). |
| Best for | Real-time analytics rules, alerting, hunting, workbooks, and all Microsoft Sentinel features. | - Compliance and regulatory logging.- Historical trend analysis and forensics.- Low-touch data that's not needed for real-time alerts. |
| Ingestion cost | Standard | Minimal |
| Query price included | ✅ | ❌ |
| Optimized query performance | ✅ | ❌ Slower queries.Good for auditing. Not optimized for real-time analysis. |
| Query capabilities | [Full query capabilities](/en-us/azure/azure-monitor/logs/get-started-queries) in the Microsoft Defender portal, the Azure portal, and by using APIs. | - [Full query capabilities](/en-us/azure/azure-monitor/logs/get-started-queries), including unions and joins.- Run scheduled KQL or Spark jobs.- Use notebooks. |
| Full set of real-time analytics features | ✅ | ❌ Limitations on some features, including analytics rules, hunting queries, parsers, watchlists, workbooks, and playbooks. |
| [Search jobs](investigate-large-datasets) | ✅ | ✅ |
| [Summary rules](summary-rules) | ✅ | ✅ [Full KQL on a single table](/en-us/azure/azure-monitor/logs/basic-logs-query), which you can extend with data from an analytics table using [lookup](/en-us/azure/data-explorer/kusto/query/lookup-operator) |
| [Restore](restore) | ✅ | ❌ KQL and Notebook jobs can promote data to the analytics tier. |
| [Data export](/en-us/azure/azure-monitor/logs/logs-data-export) | ✅ | ❌ |
| Retention period | 90 days for Microsoft Sentinel, 30 days for Microsoft Defender XDR. Can be extended to up to two years at a prorated monthly long-term retention charge. | Same as analytics retention, by default. Can be extended to up to 12 years. |

### What happens when you modify table settings

You can switch a table's tier and retention settings at any time.

When you change a table's tier from Analytics to Data Lake, all real-time analytics and hunting queries stop working.

When you shorten a table's total retention, Microsoft waits 30 days before removing the data, so you can revert the change and avoid data loss if you made a configuration error.

When you increase total retention, the new retention period applies to all data that was already ingested into the table and wasn't yet removed.

When you change the analytics retention settings of a table with existing data, the change takes effect immediately.

***Example***:

- You have a table in the Analytics tier with 180 days of analytics retention. By default, total retention is also set to 180 days.
- You change analytics retention to 90 days without changing total retention, which remains 180 days.
- Microsoft Sentinel automatically removes the last 90 days of data from analytics retention, but continues to store data that's 90-180 days old in the Data Lake tier.

### Manage XDR data in Microsoft Sentinel

By default, Microsoft Defender XDR retains threat hunting data in the **XDR default tier** for 30 days. This data isn't ingested into the Analytics or Data Lake tiers by default. If you extend the retention period of supported XDR tables beyond 30 days and up to 90 days, Sentinel ingestion costs apply, but there are no additional storage costs. The tables are created in your Microsoft Sentinel workspace in the Analytics tier and mirrored to the Data Lake tier.

If you enable the Microsoft Sentinel XDR connector in the Azure portal, the tables you select during setup are automatically ingested into the Analytics tier and mirrored to the Data Lake tier. The default retention is 30 days, and you can extend it up to 12 years. For a list of tables, see [Microsoft Defender XDR integration with Microsoft Sentinel](connect-microsoft-365-defender?tabs=MDE#connect-events). You can ingest supported XDR tables that you didn't select during connector deployment into the Analytics tier and mirror them to the Data Lake tier by setting retention to more than 30 days.

If you don't enable the Microsoft Sentinel XDR connector, XDR tables aren't automatically ingested, but you can still ingest them by setting Analytics or Data Lake tier retention to more than 30 days in the Microsoft Defender portal.

You can choose to ingest supported XDR tables exclusively into the Data Lake tier by selecting the **Data Lake tier** option when configuring retention settings. For more information, see [Configure data retention and tiering](configure-data-connector?tabs=defender-portal#configure-data-retention-and-tiering).

Warning

Resetting analytics retention and total retention to the default 30 days disables the connector in the Azure portal.

To stop ingesting data into the Analytics tier, reset analytics retention and total retention to the default 30 days.

For more information about managing your tables and data, see [Manage your existing tables and data](manage-table-tiers-retention).

#### XDR data retention and costs

The following tables summarize the free retention periods and cost implications for the different tiers in Microsoft Sentinel:

| Tier | Retention | Notes |
| --- | --- | --- |
| Advanced hunting (default) | 30 days | Default, included in the XDR license. |
| Analytics tier | 31-90 days | Free storage for Sentinel-enabled workspaces. Data is mirrored to the data lake. Sentinel ingestion charges apply. |
| Data Lake tier | Configurable. By default, the same as the analytics tier. | Free storage when total retention is the same as analytics tier retention.Retaining data in the Data Lake tier beyond analytics tier retention incurs Data Lake tier storage costs.Ingesting data directly into the Data Lake tier incurs ingestion, storage, and processing costs. |

For more information about billing and costs, see [Understand the full billing model for Microsoft Sentinel](billing#understand-the-full-billing-model-for-microsoft-sentinel).

In the following examples, XDR data is available through advanced hunting for at least 30 days, regardless of the retention settings in the analytics or data lake tiers.

| Analytics tier retention | Total retention | Analytics tier ingestion costs | Analytics tier storage costs | Data Lake tier costs |
| --- | --- | --- | --- | --- |
| 30 days default | 30 days default | No additional costs | N/A | N/A |
| 90 days | 90 days | Costs apply for analytics tier ingestion. | No additional costs. 90 days included free. | No additional costs. Total retention matches analytics tier retention. |
| 90 days | 180 days | Costs apply for analytics tier ingestion. | No additional costs; 90 days included free. | Costs apply for 90 days of additional data lake retention (180 - 90 days). |
| 180 days | 1 year | Costs apply for analytics tier ingestion. | Costs apply for 90 days of additional analytics tier retention. | Costs apply for 185 days of additional data lake retention (365 - 180 days). |
| 0 days (data lake only) | 5 years | N/A | N/A | Costs apply for ingestion and for 5 years of data lake retention. |