---
layout: Conceptual
title: Monitor the health of your Microsoft Sentinel data connectors | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/monitor-data-connector-health
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
description: Use the SentinelHealth data table and the Health Monitoring workbook to keep track of your data connectors' connectivity and performance.
ms.author: guywild
author: guywi-ms
ms.reviewer: ofshezaf
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 9f18e952-ab52-3236-9ac1-7a2dfa8cff4c
document_version_independent_id: 778f62c7-a78b-a732-2ced-9f1787ec298b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/monitor-data-connector-health.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/monitor-data-connector-health
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/monitor-data-connector-health.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 602cc80d-539b-b1f8-c766-a90d14495d99
---

# Monitor the health of your Microsoft Sentinel data connectors | Microsoft Learn

To ensure complete and uninterrupted data ingestion in your Microsoft Sentinel service, keep track of your data connectors' health, connectivity, and performance.

The following features allow you to perform this monitoring from within Microsoft Sentinel:

- **Data collection health monitoring workbook**: This workbook provides additional monitors, detects anomalies, and gives insight regarding the workspace’s data ingestion status. You can use the workbook’s logic to monitor the general health of the ingested data, and to build custom views and rule-based alerts.
- ***SentinelHealth* data table**: Querying this table provides insights on health drifts, such as latest failure events per connector, or connectors with changes from success to failure states, which you can use to create alerts and other automated actions. The *SentinelHealth* data table is currently supported only for selected data connectors, such as Amazon Web Services, Dynamics 365, Office 365, and others listed in the Supported data connectors section later in this article.
- [**View the health and status of your connected SAP systems**](monitor-sap-system-health): Review health information for your SAP systems under the SAP data connector, and use an alert rule template to get information about the health of the SAP agent's data collection.

This article explains how to use the data collection health monitoring workbook and the *SentinelHealth* data table to monitor data connector health, run diagnostic queries, and configure automated alerts for health drifts.

## Use the health monitoring workbook

To get started, install the **Data collection health monitoring** workbook from the **Content hub** and view or create a copy of the template from the **Workbooks** section of Microsoft Sentinel.

1. For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), under **Content management**, select **Content hub**. For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), select **Microsoft Sentinel** &gt; **Content management** &gt; **Content hub**.
2. In the **Content hub**, enter *health* in the search bar, and select **Data collection health monitoring** from among the results.
3. Select **Install** from the details pane. When you see a notification message that the workbook is installed, or if instead of *Install*, you see *Configuration*, proceed to the next step.
4. In Microsoft Sentinel, under **Threat management**, select **Workbooks**.
5. In the **Workbooks** page, select the **Templates** tab, enter *health* in the search bar, and select **Data collection health monitoring** from among the results.
6. Select **View template** to use the workbook as is, or select **Save** to create an editable copy of the workbook. When the copy is created, select **View saved workbook**.
7. Once in the workbook, first select the **subscription** and **workspace** you wish to view, then define the **TimeRange** to filter the data according to your needs. Use the **Show help** toggle to display in-place explanation of the workbook.

    [![data connector health monitoring workbook landing page](media/monitor-data-connector-health/data-health-workbook-1.png)](media/monitor-data-connector-health/data-health-workbook-1.png#lightbox)

There are three tabbed sections in this workbook:

- The **Overview** tab shows the general status of data ingestion in the selected workspace: volume measures, EPS rates, and time last log received.
- The **Data collection anomalies** tab will help you to detect anomalies in the data collection process, by table and data source. Each tab presents anomalies for a particular table (the **General** tab includes a collection of tables). The anomalies are calculated using the **series\_decompose\_anomalies()** function that returns an **anomaly score**. [Learn more about the series_decompose_anomalies() function](/en-us/kusto/query/series-decompose-anomalies-function?view=microsoft-sentinel&amp;preserve-view=true&amp;WT.mc_id=Portal-fx). Set the following parameters for the function to evaluate:

    - **AnomaliesTimeRange**: This time picker applies only to the data collection anomalies view.
    - **SampleInterval**: The time interval in which data is sampled in the given time range. The anomaly score is calculated only on the last interval's data.
    - **PositiveAlertThreshold**: This value defines the positive anomaly score threshold. It accepts decimal values.
    - **NegativeAlertThreshold**: This value defines the negative anomaly score threshold. It accepts decimal values.

        [![data connector health monitoring workbook anomalies page](media/monitor-data-connector-health/data-health-workbook-2.png)](media/monitor-data-connector-health/data-health-workbook-2.png#lightbox)
- The **Agent info** tab shows you information about the health of the agents installed on your various machines, whether Azure VM, other cloud VM, on-premises VM, or physical. Monitor system location, heartbeat status and latency, available memory and disk space, and agent operations.

    In this section you must select the tab that describes your machines’ environment: choose the **Azure-managed machines** tab if you want to view only the Azure Arc-managed machines; choose the **All machines** tab to view both managed and non-Azure machines with the Azure Monitor Agent installed.

    [![data connector health monitoring workbook agent info page](media/monitor-data-connector-health/data-health-workbook-3.png)](media/monitor-data-connector-health/data-health-workbook-3.png#lightbox)

## Use the SentinelHealth data table

To get data connector health data from the *SentinelHealth* data table, you must first turn on the Microsoft Sentinel health feature for your workspace. For more information, see [Turn on health monitoring for Microsoft Sentinel](enable-monitoring).

Once the health feature is turned on, the *SentinelHealth* data table is created at the first success or failure event generated for your data connectors.

### Supported data connectors

The *SentinelHealth* data table is currently supported only for the following data connectors:

- [Amazon Web Services (CloudTrail and S3)](connect-aws)
- [Dynamics 365](connect-dynamics-365)
- [Office 365](connect-office-365)
- [Microsoft Defender for Endpoint](connect-microsoft-defender-advanced-threat-protection)
- [Threat Intelligence - TAXII](connect-threat-intelligence-taxii)
- [Threat Intelligence Platforms](connect-threat-intelligence-tip)
- Any connector based on [Codeless Connector Framework](isv/create-codeless-connector)

### Understanding SentinelHealth table events

The *SentinelHealth* table is a Microsoft Sentinel log table that stores health events for supported data connectors. The following types of health events are logged in this table:

- **Data fetch status change**. To prevent redundant auditing and reduce table size, Microsoft Sentinel logs this event once an hour while a data connector's status remains stable with either continuous success or failure events. If the data connector's status has continuous failures, additional details about the failures are included in the *ExtendedProperties* column.

    If the data connector's status changes, either from a success to failure, from failure to success, or has changes in failure reasons, the event is logged immediately to allow your team to take proactive and immediate action.

    Potentially transient errors, such as source service throttling, are logged only after they've continued for more than 60 minutes. These 60 minutes allow Microsoft Sentinel to overcome a transient issue in the backend and catch up with the data, without requiring any user action. Errors that are definitely not transient are logged immediately.
- **Failure summary**. Logged once an hour, per connector, per workspace, with an aggregated failure summary. Failure summary events are created only when the connector has experienced polling errors during the given hour. They contain any extra details provided in the *ExtendedProperties* column, such as the time period for which the connector's source platform was queried, and a distinct list of failures encountered during the time period.

For more information, see [SentinelHealth table columns schema](health-table-reference#sentinelhealth-table-columns-schema).

### Run queries to detect health drifts

Create queries on the *SentinelHealth* table to help you detect health drifts in your data connectors. For example:

**Detect latest failure events per connector**:

```kusto
SentinelHealth
| where TimeGenerated > ago(3d)
| where OperationName == 'Data fetch status change'
| where Status in ('Success', 'Failure')
| summarize TimeGenerated = arg_max(TimeGenerated,*) by SentinelResourceName, SentinelResourceId
| where Status == 'Failure'
```

**Detect connectors with changes from fail to success state**:

```kusto
let latestStatus = SentinelHealth
| where TimeGenerated > ago(12h)
| where OperationName == 'Data fetch status change'
| where Status in ('Success', 'Failure')
| project TimeGenerated, SentinelResourceName, SentinelResourceId, LastStatus = Status
| summarize TimeGenerated = arg_max(TimeGenerated,*) by SentinelResourceName, SentinelResourceId;
let nextTolatestStatus = SentinelHealth
| where TimeGenerated > ago(12h)
| where OperationName == 'Data fetch status change'
| where Status in ('Success', 'Failure')
| join kind = leftanti (latestStatus) on SentinelResourceName, SentinelResourceId, TimeGenerated
| project TimeGenerated, SentinelResourceName, SentinelResourceId, NextToLastStatus = Status
| summarize TimeGenerated = arg_max(TimeGenerated,*) by SentinelResourceName, SentinelResourceId;
latestStatus
| join kind=inner (nextTolatestStatus) on SentinelResourceName, SentinelResourceId
| where NextToLastStatus == 'Failure' and LastStatus == 'Success'
```

**Detect connectors with changes from success to fail state**:

```kusto
let latestStatus = SentinelHealth
| where TimeGenerated > ago(12h)
| where OperationName == 'Data fetch status change'
| where Status in ('Success', 'Failure')
| project TimeGenerated, SentinelResourceName, SentinelResourceId, LastStatus = Status
| summarize TimeGenerated = arg_max(TimeGenerated,*) by SentinelResourceName, SentinelResourceId;
let nextTolatestStatus = SentinelHealth
| where TimeGenerated > ago(12h)
| where OperationName == 'Data fetch status change'
| where Status in ('Success', 'Failure')
| join kind = leftanti (latestStatus) on SentinelResourceName, SentinelResourceId, TimeGenerated
| project TimeGenerated, SentinelResourceName, SentinelResourceId, NextToLastStatus = Status
| summarize TimeGenerated = arg_max(TimeGenerated,*) by SentinelResourceName, SentinelResourceId;
latestStatus
| join kind=inner (nextTolatestStatus) on SentinelResourceName, SentinelResourceId
| where NextToLastStatus == 'Success' and LastStatus == 'Failure'
```

See more information on the following Kusto operators and functions used in the SentinelHealth health-drift queries, in the Kusto documentation:

- [***let*** statement](/en-us/kusto/query/let-statement?view=microsoft-sentinel&amp;preserve-view=true)
- [***where*** operator](/en-us/kusto/query/where-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***project*** operator](/en-us/kusto/query/project-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***summarize*** operator](/en-us/kusto/query/summarize-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***join*** operator](/en-us/kusto/query/join-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***ago()*** function](/en-us/kusto/query/ago-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***arg\_max()*** aggregation function](/en-us/kusto/query/arg-max-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true)

For more information on KQL, see [Kusto Query Language (KQL) overview](/en-us/kusto/query/?view=microsoft-sentinel&amp;preserve-view=true).

Other resources:

- [KQL quick reference](/en-us/kusto/query/kql-quick-reference?view=microsoft-sentinel&amp;preserve-view=true)
- [Kusto Query Language learning resources](/en-us/kusto/query/kql-learning-resources?view=microsoft-sentinel&amp;preserve-view=true)

### Configure alerts and automated actions for health issues

While you can use the Microsoft Sentinel [analytics rules](automate-incident-handling-with-automation-rules) to configure automation in Microsoft Sentinel logs, if you want to be notified and take immediate action for health drifts in your data connectors, we recommend that you use [Azure Monitor alert rules](/en-us/azure/azure-monitor/alerts/alerts-overview).

The following steps show how to create an Azure Monitor alert rule that uses a SentinelHealth query to detect data connector health drifts:

1. In an Azure Monitor alert rule, select your Microsoft Sentinel workspace as the rule scope, and **Custom log search** as the first condition.
2. Customize the alert logic as needed, such as frequency or lookback duration, and then use the health drift detection queries from the Run queries to detect health drifts section to search for health drifts.
3. For the rule actions, select an existing action group or create a new one as needed to configure push notifications or other automated actions such as triggering a Logic App, Webhook, or Azure Function in your system.

For more information, see [Azure Monitor alerts overview](/en-us/azure/azure-monitor/alerts/alerts-overview) and [Azure Monitor alerts log](/en-us/azure/azure-monitor/alerts/alerts-log).