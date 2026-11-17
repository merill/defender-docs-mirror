---
layout: Conceptual
title: Manage tables, tiers, and retention in Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/manage-table-tiers-retention
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
description: Configure retention and data tier settings for Microsoft Sentinel and Defender XDR tables in the Microsoft Defender portal.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 2aefff74-c751-476e-24bf-8c0ff3782d97
document_version_independent_id: 27054b03-c125-f508-b11f-cd31c69d9da7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/manage-table-tiers-retention.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/manage-table-tiers-retention
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/manage-table-tiers-retention.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
platformId: 4fa798b0-9a70-0a32-fd8e-1487bccf21f0
---

# Manage tables, tiers, and retention in Sentinel | Microsoft Learn

The Microsoft Defender portal provides a centralized experience for configuring table-level data retention and tier settings across Microsoft Sentinel and Microsoft Defender XDR. You can view and manage retention settings, switch between Analytics and Data Lake tiers, and optimize storage based on operational and cost requirements.

For an overview of the **Data & connectors** experience, see [Manage data in Microsoft Sentinel and Defender](manage-data-overview).

Note

If you use Integrated Security Operations Center (ISOC), see [Manage tables, tiers, and retention in ISOC](manage-table-tiers-retention-isoc). Review [Data ingestion and billing for ISOC in Microsoft Defender](/en-us/defender-xdr/integrated-security-operations-data-billing-retention) for eligibility and included retention before changing table settings. The general retention ranges in this article don't establish which settings are supported for an individual ISOC XDR table. The XDR retention thresholds and cost examples describe the existing Microsoft Sentinel XDR ingestion experience, not the ISOC retention benefit.

## Prerequisites

- To use data lake retention, your workspace must be in a [supported region](geographical-availability-data-residency#supported-regions).
- To manage Defender XDR hunting tables, you need to onboard to Microsoft Sentinel in the Defender portal. For more information, see [Connect Microsoft Sentinel to the Microsoft Defender portal](/en-us/azure/sentinel/microsoft-sentinel-onboard).
- To use Table insights, you need read access to the Tables page in your workspace. Table insights requires the same permissions as viewing table settings. For more information, see [Table insights permissions](manage-data-overview#table-insights-permissions).

## Permissions required

Microsoft Sentinel workspace permissions let you view or manage tables in specific Microsoft Sentinel workspaces, while unified role-based access control (RBAC) permissions apply to all Microsoft Sentinel workspaces in the Defender portal.

### Permissions to manage table settings

The following table lists the permissions required to view or configure table settings.

| Action | Unified RBAC in the Defender portal | Microsoft Sentinel workspace permissions |
| --- | --- | --- |
| View table settings | `Security data basics (read)` permissions under the `Security operations` permissions group | `Microsoft.OperationalInsights/workspaces/tables/read` permissions to the Log Analytics workspace, as provided by the [Log Analytics Reader built-in role](/en-us/azure/azure-monitor/logs/manage-access#log-analytics-reader), for example. |
| Configure table settings | `Data (manage)` permissions under the `Data operations` permissions group | `Microsoft.OperationalInsights/workspaces/write` and `Microsoft.OperationalInsights/workspaces/tables/write` permissions to the Log Analytics workspace, as provided by the [Log Analytics Contributor built-in role](/en-us/azure/azure-monitor/logs/manage-access#log-analytics-contributor), for example. |

For more information about unified RBAC in the Defender portal, see [Microsoft Defender XDR Unified role-based access control (RBAC)](/en-us/defender-xdr/manage-rbac).

For more information about Microsoft Sentinel workspace permissions, see [Roles and permissions in the Microsoft Sentinel platform](roles).

For permissions to investigate table health, see [Table insights permissions](manage-data-overview#table-insights-permissions).

## Which tables can you manage in the Microsoft Defender portal?

This section describes the table types you can manage in the Microsoft Defender portal.

[![Screenshot that shows the Table Management screen in the Defender portal.](media/manage-data-overview/view-table-properties-microsoft-defender-portal.png)](media/manage-data-overview/view-table-properties-microsoft-defender-portal.png#lightbox)

| Table type | Description | Examples | Is in Microsoft Sentinel workspace? |
| --- | --- | --- | --- |
| **Microsoft Sentinel** | Built-in tables, including:- Azure tables, such as AzureDiagnostics and SigninLogs.- Microsoft Sentinel tables.- [Microsoft Defender XDR integration with Microsoft Sentinel](connect-microsoft-365-defender?tabs=MDE#connect-events), which are created in your Microsoft Sentinel workspace when you increase the analytics retention period beyond 30 days. See the **XDR** table type for Defender XDR tables that are currently unsupported. | - Azure tables: `AzureDiagnostics`, `SigninLogs`- Microsoft Sentinel tables: `AWSCloudTrail`, `SecurityAlert`- XDR tables: `DeviceEvents`,`AlertInfo` | Yes |
| **Custom** | Tables you create manually or through jobs in your Microsoft Sentinel workspace, including summary rule and search job results tables, and custom data source tables. | Tables with `_CL` or `_SRCH` suffixes. | Yes |
| **XDR** | Tables in the XDR default tier, which have 30 days of analytics retention by default. You can view these tables, but you can't manage them from the Defender portal. | `IdentityInfo` | No |

Note

You can view Basic Logs tables in your Microsoft Sentinel workspace from the Microsoft Defender portal, but you can currently manage them only from your Log Analytics workspace. To manage these tables from the Microsoft Defender portal, change the table plan from Basic Logs to Analytics in your Microsoft Sentinel workspace.

## How data tiers and retention work

For regional support, see [Data lake retention availability](geographical-availability-data-residency#supported-regions).

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

## Compare the analytics and data lake tiers

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

## What happens when you modify table settings

You can switch a table's tier and retention settings at any time.

When you change a table's tier from Analytics to Data Lake, all real-time analytics and hunting queries stop working.

When you shorten a table's total retention, Microsoft waits 30 days before removing the data, so you can revert the change and avoid data loss if you made a configuration error.

When you increase total retention, the new retention period applies to all data that was already ingested into the table and wasn't yet removed.

When you change the analytics retention settings of a table with existing data, the change takes effect immediately.

***Example***:

- You have a table in the Analytics tier with 180 days of analytics retention. By default, total retention is also set to 180 days.
- You change analytics retention to 90 days without changing total retention, which remains 180 days.
- Microsoft Sentinel automatically removes the last 90 days of data from analytics retention, but continues to store data that's 90-180 days old in the Data Lake tier.

## Manage XDR data in Microsoft Sentinel

Before changing retention, review the table's current settings and the warnings in the Microsoft Defender portal. For ISOC-specific retention and billing, use the [ISOC guidance](/en-us/defender-xdr/integrated-security-operations-data-billing-retention) rather than the retention thresholds and cost examples in this section.

By default, Microsoft Defender XDR retains threat hunting data in the **XDR default tier** for 30 days. This data isn't ingested into the Analytics or Data Lake tiers by default. If you extend the retention period of supported XDR tables beyond 30 days and up to 90 days, Sentinel ingestion costs apply, but there are no additional storage costs. The tables are created in your Microsoft Sentinel workspace in the Analytics tier and mirrored to the Data Lake tier.

If you enable the Microsoft Sentinel XDR connector in the Azure portal, the tables you select during setup are automatically ingested into the Analytics tier and mirrored to the Data Lake tier. The default retention is 30 days, and you can extend it up to 12 years. For a list of tables, see [Microsoft Defender XDR integration with Microsoft Sentinel](connect-microsoft-365-defender?tabs=MDE#connect-events). You can ingest supported XDR tables that you didn't select during connector deployment into the Analytics tier and mirror them to the Data Lake tier by setting retention to more than 30 days.

If you don't enable the Microsoft Sentinel XDR connector, XDR tables aren't automatically ingested, but you can still ingest them by setting Analytics or Data Lake tier retention to more than 30 days in the Microsoft Defender portal.

You can choose to ingest supported XDR tables exclusively into the Data Lake tier by selecting the **Data Lake tier** option when configuring retention settings. For more information, see [Configure data retention and tiering](configure-data-connector?tabs=defender-portal#configure-data-retention-and-tiering).

Warning

Resetting analytics retention and total retention to the default 30 days disables the connector in the Azure portal.

To stop ingesting data into the Analytics tier, reset analytics retention and total retention to the default 30 days.

For more information about managing your tables and data, see Manage table settings.

### XDR data retention and costs

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

## Manage table settings

To configure table retention and tier settings in the Microsoft Defender portal, follow these steps:

1. Select **Microsoft Sentinel** &gt; **Configuration** &gt; **Tables** from the left navigation pane.

    The **Tables** page lists all the tables you can manage in the Microsoft Defender portal and each table's current settings.

    [![Screenshot that shows the Tables screen in the Defender portal.](media/manage-data-overview/view-table-properties-microsoft-defender-portal.png)](media/manage-data-overview/view-table-properties-microsoft-defender-portal.png#lightbox)

    The workspace column shows the Microsoft Sentinel workspace where a Microsoft Sentinel or custom table is stored.
2. To manage Microsoft Sentinel and custom tables in a different Microsoft Sentinel workspace, select the workspace name at the top left corner of the screen to switch between workspaces.
3. Select a table on the **Tables** screen.

    Selecting a table opens the table details side panel with more information about the table, including data sources, table description, tier, and retention details.

    [![Screenshot that shows the table details side panel for the CommonSecurityLog table, including data sources, on the Table Management screen in the Defender portal.](media/manage-data-overview/table-management-microsoft-defender-portal.png)](media/manage-data-overview/table-management-microsoft-defender-portal.png#lightbox)
4. Select **Manage table**.

    The **Manage table** screen lets you modify retention settings in the current tier and change the storage tier, if necessary.

    Available settings depend on the table. Review the options and warnings shown for the selected table rather than assuming that every table supports the full ranges listed here.

    [![Screenshot that shows the Manage table screen for the CommonSecurityLog table in the Defender portal.](media/manage-data-overview/manage-table-settings-microsoft-defender-portal.png)](media/manage-data-overview/manage-table-settings-microsoft-defender-portal.png#lightbox)

    - **Analytics tier retention settings**:

        - **Analytics retention**: Set a value from 30 days to two years.
        - **Total retention**: Set a value up to 12 years of long-term storage in the Data Lake.
    - **Data Lake tier**: Set **Retention** to a value between 30 days and 12 years. Selecting **Data Lake tier** stores data exclusively in the Data Lake.
    - **Tier changes**: If necessary, you can change tiers at any time based on your cost management and data usage needs.

        Important

        Tier changes aren't available for all tables. For example, some XDR and Microsoft Sentinel solution tables must remain in the Analytics tier because Microsoft security services require the data in these tables for near-real-time analytics.

    For more information about retention and tier settings, see How data tiers and retention work.
5. Review warnings and messages. These messages help you understand important implications of changing table settings.

    Examples include:

    - Increased retention is likely to increase data cost.
    - Changing from the Analytics tier to the Data Lake tier causes features that rely on Analytics data to stop functioning, such as:
        - Alerting
        - Advanced hunting
        - Analytics rules
        - Custom detection rules
6. Select **Save** to apply the new settings.