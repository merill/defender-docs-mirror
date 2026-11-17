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
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: ad3cbb72-db10-6bde-479f-bf28fba0e2a0
---

# Manage data tiers and retention in Microsoft Sentinel | Microsoft Learn

The Microsoft Defender portal provides a centralized experience for managing Microsoft Sentinel and Microsoft Defender XDR data. The **Data & connectors** experience consolidates connector management, table management, transformations, and ingestion health monitoring into a single view, so you can understand and optimize your security data without navigating between separate pages.

This article introduces the **Data & connectors** experience and explains how to use it to manage data in Microsoft Sentinel and Microsoft Defender XDR. For related tasks, see:

- [Configure data connectors](configure-data-connector) to send data to Microsoft Sentinel or Microsoft Defender XDR.
- [Manage tables, tiers, and retention in Sentinel](manage-table-tiers-retention).
- [Manage tables, tiers, and retention in ISOC](manage-table-tiers-retention-isoc).

Note

If you use Integrated Security Operations Center (ISOC), see [Data ingestion and billing for ISOC in Microsoft Defender](/en-us/defender-xdr/integrated-security-operations-data-billing-retention) for eligibility and included retention.

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

For supported table types, data tier comparisons, retention behavior, and XDR costs, see [Configure table settings in Microsoft Sentinel](manage-table-tiers-retention#which-tables-can-you-manage-in-the-microsoft-defender-portal).

### Use Table insights for table-level observability

Table insights on the **Tables** tab helps you understand ingestion health at the table level for the selected Microsoft Sentinel workspace. It gives you quick observability signals so you can identify ingestion and cost patterns before you change tier or retention settings.

Columns in the tables grid show per-table health signals for each table, including:

- Last data received.
- Average daily ingestion volume.
- Estimated daily ingestion cost.
- Volume anomaly (day-over-week ingestion fluctuation).

Use the grid columns to sort, filter, and compare tables side by side. Combine these signals to detect connector failures, investigate cost spikes, validate new connector onboarding, and identify candidates for right-sizing retention and tier.

[![Screenshot of the Tables grid showing filters and table insights columns for tier, last data received, average daily ingestion, estimated daily cost, volume anomaly, and retention.](media/manage-data-overview/table-insights-grid.png)](media/manage-data-overview/table-insights-grid.png#lightbox)

Important

Table insights is a visualization surface for investigation. It isn't a billing-grade or alerting surface.

For detailed signals, steps, and limitations, see Use Table insights to monitor table health.

#### Table insights permissions

Use the following permissions when you want to investigate ingestion health in **Table insights** or take action from a flagged table.

| Task | Minimum role | Scope |
| --- | --- | --- |
| View **Table insights** cards and the table grid | [Microsoft Sentinel Reader built-in role](roles#built-in-azure-roles-for-microsoft-sentinel) | Resource group that contains the workspace |
| Configure fluctuation thresholds or customize table columns | [Microsoft Sentinel Contributor built-in role](roles#built-in-azure-roles-for-microsoft-sentinel) | Workspace |
| Change a table tier or retention setting | [Microsoft Sentinel Contributor built-in role](roles#built-in-azure-roles-for-microsoft-sentinel) and [Log Analytics Contributor built-in role](/en-us/azure/azure-monitor/logs/manage-access#log-analytics-contributor) | Workspace |
| Create a data collection rule (DCR) or ingestion-time transformation from a flagged table | [Monitoring Contributor built-in role](/en-us/azure/role-based-access-control/built-in-roles/monitor#monitoring-contributor) and [Microsoft Sentinel Contributor built-in role](roles#built-in-azure-roles-for-microsoft-sentinel) | Subscription or resource group that contains the DCR |
| Read the underlying health signals for custom alerting | [Log Analytics Reader built-in role](/en-us/azure/azure-monitor/logs/manage-access#log-analytics-reader) | Workspace |

Custom roles must include equivalent read and write permissions for table settings and health investigation, including `Microsoft.OperationalInsights/workspaces/tables/read` and `Microsoft.SecurityInsights/*/read` data actions.

### Use Table insights to monitor table health

Table insights is a built-in monitoring view on the Tables page in the Microsoft Defender portal. It gives security and platform engineers a single table-level view of ingestion health in a Microsoft Sentinel workspace, including tables populated by third-party data connectors. Use it to spot silent connector failures, investigate cost spikes, validate a new connector onboarding, and identify tables that might need a different tier or retention setting.

Review the Table insights section and table grid together to understand whether a table is healthy, expensive, or misconfigured.

| Signal | What it shows | How to use it |
| --- | --- | --- |
| **Ingestion volume per tier** | The rolling 30-day total of gigabytes ingested into the Analytics and Data Lake tiers for the current workspace | Compare how much data each tier is receiving before you move tables between tiers or shorten retention. |
| **Table ingestion fluctuations** | Tables whose last 24-hour ingestion volume differs from the same day last week by at least the configured fluctuation threshold | Investigate large drops or spikes first. A negative value can indicate an upstream collection issue, while a positive value can signal unexpected cost growth. |
| **Top 5 tables by daily ingestion volume** | The tables that drove the most daily ingestion during the last 30 days | Use this view to identify the main cost drivers in the workspace and decide whether a transformation or tier change might help. |
| **Last data received** | How long it has been since the table last received a record | Use this value to detect a connector that has gone silent, especially after a deployment or credential change. |
| **Avg. daily ingestion** | The average number of gigabytes per day over the lookback window | Compare this value with retention settings to find tables that are storing more data than you need for active investigations. |
| **Est. daily ingestion cost** | The estimated daily ingestion cost for the table's current tier | Use this estimate to prioritize which tables to optimize first when costs increase. |
| **Volume anomaly** | The signed percentage change from the baseline ingestion pattern | Focus on large positive values for unexpected cost growth and large negative values for possible data collection failures. |

To view all table insights and investigate table behavior:

1. Sign in to the Microsoft Defender portal.
2. Go to **Microsoft Sentinel** &gt; **Configuration** &gt; **Tables**.
3. Select **View all**.

    [![Screenshot that shows where the View all button is located in the Table insights section of the page.](media/manage-table-tiers-retention/view-all-table-insights.png)](media/manage-table-tiers-retention/view-all-table-insights.png#lightbox)
4. Review all insights.
5. (Optional) Add additional filters such as:

    - Minimum fluctuation percentage.
    - Minimum fluctuation volume by kilobytes (KB), megabytes (MB), or gigabytes (GB).
6. (Optional) Sort the table by selecting one of the headers.

Table insights is useful in scenarios such as:

- If a third-party connector silently stops sending data, sort by **Last data received** and review the **Table ingestion fluctuations** card for tables that dropped to zero ingestion in the last 24 hours compared to the same period last week.
- If a noisy connector causes an unexpected cost spike, review **Top 5 tables by daily ingestion volume**, then inspect **Volume anomaly** and **Est. daily ingestion cost** to find the table that needs transformation or tier review.
- If you just onboarded a new third-party data connector, confirm that its destination table appears in the grid, is receiving data, and is on the expected tier.
- If you need to right-size table settings, compare **Avg. daily ingestion**, **Est. daily ingestion cost**, **Tier**, and **Retention** to identify candidates for the Data Lake tier or shorter retention.
- If detections suddenly drop, review the fluctuations card for tables that show a 100 percent decrease and correlate those tables with the detections that stopped firing.

#### Table insights limitations

Keep the following limits in mind when you interpret the **Table insights** data:

| Area | Limitation |
| --- | --- |
| Lookback window | Ingestion volume cards show only the last 30 days. Fluctuations compare the last 24 hours with the same day of the previous week, so they don't account for longer seasonal patterns such as month-end batch jobs. |
| Fluctuation thresholds | By default, fluctuations require at least a 10 percent change and 1 megabyte of absolute change. Tables below 1 MB per day aren't evaluated and won't appear on the card even if they fully stop sending data. |
| Cost estimates | The **Est. daily ingestion cost** value is based on public list price for the table's current tier and region. It doesn't reflect commitment-tier discounts, reservations, or private pricing. |
| Tier coverage | Auxiliary, Basic Logs, and Data Lake tier tables are listed, but the **Volume anomaly** signal is currently optimized for Analytics tier tables. Results for Data Lake tier tables can be less precise. |
| Alerting | **Table insights** is a visualization surface only. To alert on table health, such as when a connector goes silent, create a scheduled analytics rule that uses the `SentinelHealth` table or a Kusto Query Language (KQL) query against `Usage` or a table-specific schema. |
| Multi-workspace view | **Table insights** shows data for the currently selected workspace only. If you manage multiple workspaces, switch workspaces to review each one separately. |

### Table details panel

Select a table on the **Tables** tab to open the table details panel. The panel consolidates schema, transformations, and retention information for the selected table. It includes the following tabs:

| Tab | What it shows |
| --- | --- |
| **Overview** | Table type, tier, analytics retention, total retention, and other table metadata. |
| **Schema** | Column names, data types, and column descriptions for the selected table. Use this tab to inspect schema without running KQL queries. |
| **Transformations** | Filter, Split, and Scope Tag transformation rules that apply to the table. You can view, create, edit, and delete transformation rules from this tab. |
| **Retention** | Analytics retention and total retention settings for the table. |
| **Data Sources** | Connector information for the table. This tab appears only for federated table types. |