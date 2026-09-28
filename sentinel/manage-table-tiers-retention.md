---
layout: Conceptual
title: Configure Table Settings in Microsoft Sentinel | Microsoft Learn
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
description: Configure retention and data tier settings for Microsoft Sentinel and Defender XDR tables in the Microsoft Defender portal, and use Table insights to monitor ingestion health and optimize costs.
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
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 4fa798b0-9a70-0a32-fd8e-1487bccf21f0
---

# Configure Table Settings in Microsoft Sentinel | Microsoft Learn

The Microsoft Defender portal provides a centralized experience for configuring table-level data retention and tier settings across Microsoft Sentinel and Microsoft Defender XDR. You can view and manage retention settings, switch between Analytics and Data Lake tiers, and optimize storage based on operational and cost requirements.

This article explains how to configure retention and tier settings for Microsoft Sentinel and Defender XDR tables in the Microsoft Defender portal. It also explains how to use Table insights, a built-in monitoring feature that surfaces ingestion health data for each table in your workspace.

For more information about how data tiers and retention work, see [Manage data tiers and retention in Microsoft Sentinel](manage-data-overview).

## Prerequisites

- To manage Defender XDR hunting tables, you need to onboard to Microsoft Sentinel in the Defender portal. For more information, see [Connect Microsoft Sentinel to the Microsoft Defender portal](/en-us/azure/sentinel/microsoft-sentinel-onboard).
- To use Table insights, you need read access to the Tables page in your workspace. Table insights requires the same permissions as viewing table settings. For more information, see Permissions required.

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

### Table insights permissions

Use the following permissions when you want to investigate ingestion health in **Table insights** or take action from a flagged table.

| Task | Minimum role | Scope |
| --- | --- | --- |
| View **Table insights** cards and the table grid | [Microsoft Sentinel Reader built-in role](roles#built-in-azure-roles-for-microsoft-sentinel) | Resource group that contains the workspace |
| Configure fluctuation thresholds or customize table columns | [Microsoft Sentinel Contributor built-in role](roles#built-in-azure-roles-for-microsoft-sentinel) | Workspace |
| Change a table tier or retention setting | [Microsoft Sentinel Contributor built-in role](roles#built-in-azure-roles-for-microsoft-sentinel) and [Log Analytics Contributor built-in role](/en-us/azure/azure-monitor/logs/manage-access#log-analytics-contributor) | Workspace |
| Create a data collection rule (DCR) or ingestion-time transformation from a flagged table | [Monitoring Contributor built-in role](/en-us/azure/role-based-access-control/built-in-roles/monitor#monitoring-contributor) and [Microsoft Sentinel Contributor built-in role](roles#built-in-azure-roles-for-microsoft-sentinel) | Subscription or resource group that contains the DCR |
| Read the underlying health signals for custom alerting | [Log Analytics Reader built-in role](/en-us/azure/azure-monitor/logs/manage-access#log-analytics-reader) | Workspace |

Custom roles must include equivalent read and write permissions for table settings and health investigation, including `Microsoft.OperationalInsights/workspaces/tables/read` and `Microsoft.SecurityInsights/*/read` data actions.

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

    [![Screenshot that shows the Manage table screen for the CommonSecurityLog table in the Defender portal.](media/manage-data-overview/manage-table-settings-microsoft-defender-portal.png)](media/manage-data-overview/manage-table-settings-microsoft-defender-portal.png#lightbox)

    - **Analytics tier retention settings**:

        - **Analytics retention**: Set a value from 30 days to two years.
        - **Total retention**: Set a value up to 12 years of long-term storage in the Data Lake.
    - **Data Lake tier**: Set **Retention** to a value between 30 days and 12 years. Selecting **Data Lake tier** stores data exclusively in the Data Lake.
    - **Tier changes**: If necessary, you can change tiers at any time based on your cost management and data usage needs.

        Important

        Tier changes aren't available for all tables. For example, some XDR and Microsoft Sentinel solution tables must remain in the Analytics tier because Microsoft security services require the data in these tables for near-real-time analytics.

    For more information about retention and tier settings, see [Manage data tiers and retention in Microsoft Sentinel](manage-data-overview).
5. Review warnings and messages. These messages help you understand important implications of changing table settings.

    Examples include:

    - Increased retention is likely to increase data cost.
    - Changing from the Analytics tier to the Data Lake tier causes features that rely on Analytics data to stop functioning, such as:
        - Alerting
        - Advanced hunting
        - Analytics rules
        - Custom detection rules
6. Select **Save** to apply the new settings.

## Use Table insights to monitor table health

Table insights is a built-in monitoring view on the Tables page in the Microsoft Defender portal. It gives security and platform engineers a single table-level view of ingestion health across a Microsoft Sentinel workspace, including tables populated by third-party data connectors. Use it to spot silent connector failures, investigate cost spikes, validate a new connector onboarding, and identify tables that might need a different tier or retention setting.

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

### Table insights limitations

Keep the following limits in mind when you interpret the **Table insights** data:

| Area | Limitation |
| --- | --- |
| Lookback window | Ingestion volume cards show only the last 30 days. Fluctuations compare the last 24 hours with the same day of the previous week, so they don't account for longer seasonal patterns such as month-end batch jobs. |
| Fluctuation thresholds | By default, fluctuations require at least a 10 percent change and 1 megabyte of absolute change. Tables below 1 MB per day aren't evaluated and won't appear on the card even if they fully stop sending data. |
| Cost estimates | The **Est. daily ingestion cost** value is based on public list price for the table's current tier and region. It doesn't reflect commitment-tier discounts, reservations, or private pricing. |
| Tier coverage | Auxiliary, Basic Logs, and Data Lake tier tables are listed, but the **Volume anomaly** signal is currently optimized for Analytics tier tables. Results for Data Lake tier tables can be less precise. |
| Alerting | **Table insights** is a visualization surface only. To alert on table health, such as when a connector goes silent, create a scheduled analytics rule that uses the `SentinelHealth` table or a Kusto Query Language (KQL) query against `Usage` or a table-specific schema. |
| Multi-workspace view | **Table insights** shows data for the currently selected workspace only. If you manage multiple workspaces, switch workspaces to review each one separately. |