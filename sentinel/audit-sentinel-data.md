---
layout: Conceptual
title: Audit Microsoft Sentinel queries and activities | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/audit-sentinel-data
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
description: Learn how to audit Microsoft Sentinel workspace activity using AzureActivity and LAQueryLogs tables for compliance and SOC monitoring.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: b78f8ccc-0c4d-874e-8555-fdcd125bef34
document_version_independent_id: ce02fefa-6097-2941-943e-3be103f6f213
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/audit-sentinel-data.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/audit-sentinel-data
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/audit-sentinel-data.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: da31c241-a240-5c88-7ae9-131f7827a241
---

# Audit Microsoft Sentinel queries and activities | Microsoft Learn

This article describes how you can view audit data for queries run and activities performed in your Microsoft Sentinel workspace, such as for internal and external compliance requirements in your Security Operations (SOC) workspace.

Microsoft Sentinel provides access to:

- The **AzureActivity** table, which provides details about all actions taken in Microsoft Sentinel, such as editing alert rules. The **AzureActivity** table doesn't log specific query data. For more information, see Auditing with Azure Activity logs.
- The **LAQueryLogs** table, which provides details about the queries run in Log Analytics, including queries run from Microsoft Sentinel. For more information, see Auditing with LAQueryLogs.

Tip

In addition to the manual queries described in this article, we recommend that you use the built-in **Workspace audit** workbook help you audit the activities in your SOC environment. For more information, see [Visualize and monitor your data by using workbooks in Microsoft Sentinel](monitor-your-data).

## Prerequisites

- Before you can successfully run the sample queries in this article, you need to have relevant data in your Microsoft Sentinel workspace to query on and access to Microsoft Sentinel.

    For more information, see [Configure Microsoft Sentinel content](configure-content) and [Roles and permissions in Microsoft Sentinel](roles).

## Auditing with Azure Activity logs

Microsoft Sentinel's audit logs are maintained in the [Azure Activity Logs](/en-us/azure/azure-monitor/essentials/platform-logs-overview), where the **AzureActivity** table includes all actions taken in your Microsoft Sentinel workspace.

Use the **AzureActivity** table when auditing activity in your SOC environment with Microsoft Sentinel.

**To query the AzureActivity table**:

1. Install the **Azure Activity solution for Sentinel** solution and connect the [Azure Activity](data-connectors-reference#azure-activity) data connector to start streaming audit events into a new table called `AzureActivity`.
2. Query the data using Kusto Query Language (KQL), like you would any other table:

    - In the Azure portal, query this table in the **[Logs](hunts-custom-queries)** page.
    - In the Defender portal, query this table in the **Investigation & response &gt; Hunting &gt; [Advanced hunting](/en-us/defender-xdr/advanced-hunting-overview)** page.

    The **AzureActivity** table includes data from many services, including Microsoft Sentinel. Use the following query to filter the **AzureActivity** table to show only Microsoft Sentinel operations:

    ```kusto
     AzureActivity
    | where OperationNameValue startswith "MICROSOFT.SECURITYINSIGHTS"
    ```

    For example, to find out who was the last user to edit a particular analytics rule, use the following query (replacing `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx` with the rule ID of the rule you want to check):

    ```kusto
    AzureActivity
    | where OperationNameValue startswith "MICROSOFT.SECURITYINSIGHTS/ALERTRULES/WRITE"
    | where Properties contains "alertRules/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
    | project Caller , TimeGenerated , Properties
    ```

Add more parameters to your query to explore the **AzureActivities** table further, depending on what you need to report. The following sections provide other sample queries to use when auditing with **AzureActivity** table data.

For more information, see Microsoft Sentinel data included in Azure Activity logs.

### Find all actions taken by a specific user in the last 24 hours

The following **AzureActivity** table query lists all actions taken by a specific Microsoft Entra user in the last 24 hours.

```kusto
AzureActivity
| where OperationNameValue contains "SecurityInsights"
| where Caller == "[AzureAD username]"
| where TimeGenerated > ago(1d)
```

### Find all delete operations

To identify Microsoft Sentinel resources that were deleted, run the following query to filter Azure Activity logs for successful delete operations in your workspace.

```kusto
AzureActivity
| where OperationNameValue contains "SecurityInsights"
| where OperationName contains "Delete"
| where ActivityStatusValue contains "Succeeded"
| project TimeGenerated, Caller, OperationName
```

### Microsoft Sentinel data included in Azure Activity logs

Microsoft Sentinel's audit logs are maintained in the [Azure Activity Logs](/en-us/azure/azure-monitor/essentials/platform-logs-overview), and include the following types of information:

| Operation | Information types |
| --- | --- |
| **Created** | Alert rules  Case comments Incident comments Saved searchesWatchlists Workbooks |
| **Deleted** | Alert rules Bookmarks Data connectors Incidents Saved searches Settings Threat intelligence reports Watchlists Workbooks Workflow |
| **Updated** | Alert rulesBookmarks  Cases  Data connectors Incidents Incident comments Threat intelligence reports  Workbooks Workflow |

You can also use the Azure Activity logs to check for user authorizations and licenses. For example, the following table lists selected operations found in Azure Activity logs with the specific resource the log data is pulled from.

| Operation name | Resource type |
| --- | --- |
| Create or update workbook | Microsoft.Insights/workbooks |
| Delete workbook | Microsoft.Insights/workbooks |
| Set workflow | Microsoft.Logic/workflows |
| Delete workflow | Microsoft.Logic/workflows |
| Create saved search | Microsoft.OperationalInsights/workspaces/savedSearches |
| Delete saved search | Microsoft.OperationalInsights/workspaces/savedSearches |
| Update alert rules | Microsoft.SecurityInsights/alertRules |
| Delete alert rules | Microsoft.SecurityInsights/alertRules |
| Update alert rule response actions | Microsoft.SecurityInsights/alertRules/actions |
| Delete alert rule response actions | Microsoft.SecurityInsights/alertRules/actions |
| Update bookmarks | Microsoft.SecurityInsights/bookmarks |
| Delete bookmarks | Microsoft.SecurityInsights/bookmarks |
| Update cases | Microsoft.SecurityInsights/Cases |
| Update case investigation | Microsoft.SecurityInsights/Cases/investigations |
| Create case comments | Microsoft.SecurityInsights/Cases/comments |
| Update data connectors | Microsoft.SecurityInsights/dataConnectors |
| Delete data connectors | Microsoft.SecurityInsights/dataConnectors |
| Update settings | Microsoft.SecurityInsights/settings |

For more information, see [Azure Activity Log event schema](/en-us/azure/azure-monitor/essentials/activity-log-schema).

## Auditing with LAQueryLogs

The **LAQueryLogs** table provides details about log queries run in Log Analytics. Since Log Analytics is used as Microsoft Sentinel's underlying data store, you can configure your system to collect LAQueryLogs data in your Microsoft Sentinel workspace.

LAQueryLogs data includes information such as:

- When queries were run
- Who ran queries in Log Analytics
- What tool was used to run queries in Log Analytics, such as Microsoft Sentinel
- The query texts themselves
- Performance data on each query run

Note

- The **LAQueryLogs** table only includes queries that have been run in the Logs blade of Microsoft Sentinel. It does not include the queries run by scheduled analytics rules, using the **Investigation Graph**, in the Microsoft Sentinel **Hunting** page, or in the Defender portal's **Advanced hunting** page.
- There may be a short delay between the time a query is run and the data is populated in the **LAQueryLogs** table. We recommend waiting about 5 minutes to query the **LAQueryLogs** table for audit data.

**To query the LAQueryLogs table**:

1. The **LAQueryLogs** table isn't enabled by default in your Log Analytics workspace. To use **LAQueryLogs** data when auditing in Microsoft Sentinel, first enable the **LAQueryLogs** in your Log Analytics workspace's **Diagnostics settings** area.

    For more information, see [Audit queries in Azure Monitor logs](/en-us/azure/azure-monitor/logs/query-audit).
2. Then, query the data using KQL, like you would any other table.

    For example, the following query shows how many queries were run in the last week, on a per-day basis:

    ```kusto
    LAQueryLogs
    | where TimeGenerated > ago(7d)
    | summarize events_count=count() by bin(TimeGenerated, 1d)
    ```

The following sections show more sample queries to run on the **LAQueryLogs** table when auditing activities in your SOC environment using Microsoft Sentinel.

### The number of queries run where the response wasn't "OK"

Use the following query to count Log Analytics queries that returned a non-success response code. This count includes queries that failed to run or returned anything other than an HTTP **200 OK** response.

```kusto
LAQueryLogs
| where ResponseCode != 200 
| count 
```

### Show users for CPU-intensive queries

To find the users or clients running the most resource-intensive queries, use the following query to surface the highest CPU-time query per Microsoft Entra client ID, sorted by CPU time consumed.

```kusto
LAQueryLogs
|summarize arg_max(StatsCPUTimeMs, *) by AADClientId
| extend User = AADEmail, QueryRunTime = StatsCPUTimeMs
| project User, QueryRunTime, QueryText
| sort by QueryRunTime desc
```

### Show users who ran the most queries in the past week

Use the following query to summarize how many queries each user ran in the last seven days, which helps identify the most active users in your workspace for auditing or usage analysis.

```kusto
LAQueryLogs
| where TimeGenerated > ago(7d)
| summarize events_count=count() by AADEmail
| extend UserPrincipalName = AADEmail, Queries = events_count
| join kind= leftouter (
    SigninLogs)
    on UserPrincipalName
| project UserDisplayName, UserPrincipalName, Queries
| summarize arg_max(Queries, *) by UserPrincipalName
| sort by Queries desc
```

## Configure alerts for Microsoft Sentinel activities

You might want to use Microsoft Sentinel auditing resources to create proactive alerts.

For example, if you have sensitive tables in your Microsoft Sentinel workspace, you can detect when those tables are accessed. The following query audits access to a specific sensitive table by listing queries that referenced it during the last 24 hours. Replace `[Name of sensitive table]` with the name of the table you want to monitor:

```kusto
LAQueryLogs
| where QueryText contains "[Name of sensitive table]"
| where TimeGenerated > ago(1d)
| extend User = AADEmail, Query = QueryText
| project User, Query
```

## Monitor Microsoft Sentinel with workbooks, rules, and playbooks

Use Microsoft Sentinel's own features to monitor events and actions that occur within Microsoft Sentinel.

- **Monitor with workbooks**. Several built-in Microsoft Sentinel workbooks can help you monitor workspace activity, including information about the users working in your workspace, the analytics rules being used, the MITRE tactics most covered, stalled or stopped ingestions, and SOC team performance.

    For more information, see [Visualize and monitor your data by using workbooks in Microsoft Sentinel](monitor-your-data) and [Commonly used Microsoft Sentinel workbooks](top-workbooks)
- **Watch for ingestion delay**. If you have concerns about ingestion delay, [set a variable in an analytics rule](ingestion-delay) to represent the delay.

    For example, the following analytics rule can help to ensure that results don't include duplicates, and that logs aren't missed when running the rules:

    ```kusto
    let ingestion_delay= 2min;let rule_look_back = 5min;CommonSecurityLog| where TimeGenerated >= ago(ingestion_delay + rule_look_back)| where ingestion_time() > (rule_look_back)
    - Calculating ingestion delay
      CommonSecurityLog| extend delay = ingestion_time() - TimeGenerated| summarize percentiles(delay,95,99) by DeviceVendor, DeviceProduct
    ```

    For more information, see [Automate incident handling in Microsoft Sentinel with automation rules](automate-incident-handling-with-automation-rules).
- **Monitor data connector health** using the [Connector Health Push Notification Solution](https://github.com/Azure/Azure-Sentinel/tree/master/Playbooks/Send-ConnectorHealthStatus) playbook to watch for stalled or stopped ingestion, and send notifications when a connector has stopped collecting data or machines have stopped reporting.

See the Kusto documentation for the operators and functions used in the KQL examples in this article:

- [***let*** statement](/en-us/kusto/query/let-statement?view=microsoft-sentinel&amp;preserve-view=true)
- [***where*** operator](/en-us/kusto/query/where-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***project*** operator](/en-us/kusto/query/project-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***count*** operator](/en-us/kusto/query/count-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***sort*** operator](/en-us/kusto/query/sort-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***extend*** operator](/en-us/kusto/query/extend-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***join*** operator](/en-us/kusto/query/join-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***summarize*** operator](/en-us/kusto/query/summarize-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***ago()*** function](/en-us/kusto/query/ago-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***ingestion\_time()*** function](/en-us/kusto/query/ingestion-time-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***count()*** aggregation function](/en-us/kusto/query/count-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***arg\_max()*** aggregation function](/en-us/kusto/query/arg-max-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true)

For more information on KQL, see [Kusto Query Language (KQL) overview](/en-us/kusto/query/?view=microsoft-sentinel&amp;preserve-view=true).

Other resources:

- [KQL quick reference](/en-us/kusto/query/kql-quick-reference?view=microsoft-sentinel&amp;preserve-view=true)
- [Kusto Query Language learning resources](/en-us/kusto/query/kql-learning-resources?view=microsoft-sentinel&amp;preserve-view=true)