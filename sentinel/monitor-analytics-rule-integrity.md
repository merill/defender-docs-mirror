---
layout: Conceptual
title: Monitor the health and audit the integrity of your Microsoft Sentinel analytics rules | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/monitor-analytics-rule-integrity
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
description: Monitor analytics rule health and audit integrity in Microsoft Sentinel by using health and audit logs, querying SentinelHealth data, and setting notifications for rule issues.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 80af35b1-3a90-22c7-57ba-cab9a7bb7c54
document_version_independent_id: 063682c9-9dc0-471f-ccee-1c48b89c210f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/monitor-analytics-rule-integrity.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/monitor-analytics-rule-integrity
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/monitor-analytics-rule-integrity.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
platformId: dce378dd-e84e-7d24-7cb8-ab297523060c
---

# Monitor the health and audit the integrity of your Microsoft Sentinel analytics rules | Microsoft Learn

To ensure comprehensive, uninterrupted, and tampering-free threat detection in your Microsoft Sentinel service, keep track of your analytics rules' health and integrity. Keep them functioning optimally by monitoring their [analytics rule execution insights](monitor-optimize-analytics-rule-execution#view-analytics-rule-insights), by querying the health and audit logs, and by [use manual rerun to test and optimize analytics rules](monitor-optimize-analytics-rule-execution#use-cases-and-benefits-of-rule-rerun).

Set up notifications of health and audit events for relevant stakeholders, who can then take action. For example, define and send email or Microsoft Teams messages, create new tickets in your ticketing system, and so on.

This article describes how to use Microsoft Sentinel's [auditing and health monitoring in Microsoft Sentinel](health-audit) to keep track of your analytics rules' health and integrity from within Microsoft Sentinel.

For information on rule insights and manual rerunning of rules, see [Monitor and optimize the execution of your scheduled analytics rules](monitor-optimize-analytics-rule-execution).

## Summary

Microsoft Sentinel provides two types of logs for monitoring analytics rules: health logs and audit logs. The following sections summarize what each log captures and where the data is stored.

- **Microsoft Sentinel analytics rule health logs:**

    - This log captures events that record the running of analytics rules, and the end result of these runnings—if they succeeded or failed, and if they failed, why.
    - The log also records, for each running of an analytics rule:
        - How many events the rule's query captured.
        - Whether the number of events passed the threshold defined in the rule, causing the rule to fire an alert.

    These logs are collected in the *SentinelHealth* table in Log Analytics.
- **Microsoft Sentinel analytics rule audit logs:**

    - This log captures events that record changes made to any analytics rule, including the following details:
        - The name of the rule that was changed.
        - Which properties of the rule were changed.
        - The state of the rule settings before and after the change.
        - The user or identity that made the change.
        - The source IP and date/time of the change.
        - ...and more.

    These logs are collected in the *SentinelAudit* table in Log Analytics.

## Use the SentinelHealth and SentinelAudit data tables

To get audit and health data from the *SentinelHealth* and *SentinelAudit* tables, you must first turn on the Microsoft Sentinel health feature for your workspace. For more information, see [Turn on auditing and health monitoring for Microsoft Sentinel](enable-monitoring).

Once the health feature is turned on, the *SentinelHealth* data table is created at the first success or failure event generated for your analytics rules.

### Understanding SentinelHealth and SentinelAudit table events

The *SentinelHealth* table logs the following types of analytics rule health events:

- **Scheduled analytics rule run**.
- **Near-real-time (NRT) analytics rule run**.

For more information, see [SentinelHealth table columns schema](health-table-reference#sentinelhealth-table-columns-schema).

The *SentinelAudit* table logs the following types of analytics rule audit events:

- **Create or update analytics rule**.
- **Analytics rule deleted**.

For more information, see [SentinelAudit table columns schema](audit-table-reference#sentinelaudit-table-columns-schema).

### Run queries to detect health and integrity issues

For best results, build your queries on the **prebuilt functions** for these tables, ***\_SentinelHealth()*** and ***\_SentinelAudit()***, instead of querying the tables directly. These functions maintain your queries' backward compatibility if changes are made to the schema of the tables.

As a first step, filter the tables for data related to analytics rules. Use the `SentinelResourceType` parameter.

```kusto
_SentinelHealth()
| where SentinelResourceType == "Analytics Rule"
```

If you want, you can further filter the list for a particular kind of analytics rule. Use the `SentinelResourceKind` parameter for this.

```kusto
| where SentinelResourceKind == "Scheduled"

# OR

| where SentinelResourceKind == "NRT"
```

Here are some sample queries to help you get started:

- Find rules that are "[auto-disabled scheduled analytics rules](troubleshoot-analytics-rules#issue-a-scheduled-rule-failed-to-execute-or-appears-with-auto-disabled-added-to-the-name)":

    ```kusto
    _SentinelHealth()
    | where SentinelResourceType == "Analytics Rule"
    | where Reason == "The analytics rule is disabled and was not executed."
    ```
- Count the rules and runnings that succeeded or failed, by reason:

    ```kusto
    _SentinelHealth()
    | where SentinelResourceType == "Analytics Rule"
    | summarize Occurrence=count(), Unique_rule=dcount(SentinelResourceId) by Status, Reason
    ```
- Find rule deletion activity in the *SentinelAudit* table. This query returns audit records where an analytics rule was deleted, so you can track who removed a rule and when:

    ```kusto
    _SentinelAudit()
    | where SentinelResourceType =="Analytic Rule"
    | where Description =="Analytics rule deleted"
    ```
- Find activity on rules, by rule name and activity name:

    ```kusto
    _SentinelAudit()
    | where SentinelResourceType =="Analytic Rule"
    | summarize Count= count() by RuleName=SentinelResourceName, Activity=Description
    ```
- Find activity on rules, by caller name (the identity that performed the activity):

    ```kusto
    _SentinelAudit()
    | where SentinelResourceType =="Analytic Rule"
    | extend Caller= tostring(ExtendedProperties.CallerName)
    | summarize Count = count() by Caller, Activity=Description
    ```

For more information on the Kusto operators and functions used in the sample queries, see the Kusto documentation:

- [***where*** operator](/en-us/kusto/query/where-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***summarize*** operator](/en-us/kusto/query/summarize-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***tostring()*** function](/en-us/kusto/query/tostring-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***count()*** aggregation function](/en-us/kusto/query/count-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***dcount()*** aggregation function](/en-us/kusto/query/dcount-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true)

For more information on KQL, see [Kusto Query Language (KQL) overview](/en-us/kusto/query/?view=microsoft-sentinel&amp;preserve-view=true).

Other resources:

- [KQL quick reference](/en-us/kusto/query/kql-quick-reference?view=microsoft-sentinel&amp;preserve-view=true)
- [Kusto Query Language learning resources](/en-us/kusto/query/kql-learning-resources?view=microsoft-sentinel&amp;preserve-view=true)

#### Query health and integrity issues for scheduled rules

When a schedule rule fails, it's retried five more times on the exact same window. The rule doesn't skip the window and miss an alert as long as one of the six attempts is successful.

Failure in one of the six attempts indicates a delay in the alert triggering. The following query calculates the exact delay:

```kusto
_SentinelHealth()
| where SentinelResourceType == @"Analytics Rule" 
| where SentinelResourceKind == "Scheduled"
| extend startTime = todatetime(ExtendedProperties["QueryStartTimeUTC"]), executionStart = todatetime(ExtendedProperties["executionStart"])
| extend delay = datetime_diff('minute', startTime, executionStart)
```

To look for complete failures (that is, a window that was skipped), use the following query:

```kusto
_SentinelHealth()| where SentinelResourceType == @"Analytics Rule" 
| where SentinelResourceKind == "Scheduled"
| where Status != "Success"
| extend startTime = tostring(ExtendedProperties["QueryStartTimeUTC"])
| summarize failuresByStartTime = count() by startTime, SentinelResourceId
| where failuresByStartTime == 6
| summarize count() by SentinelResourceId
```

This query looks for scheduled analytics rule runs where none of the six retries were successful. You can identify a retry by looking at the start time of the rule’s window since the retries always look at the original start time. This query gives you the amount of skipped windows for each analytic rule. We expect skipped windows to be rare. If you see that you have analytics rules with skipped windows, use the queries to understand the failure reason of these specific rules and the table of failures reasons and mitigations to fix them.

#### Query health and integrity issues for NRT rules

The retry mechanism for NRT rules behaves differently from scheduled rules. If a rule fails to run, the system also considers the failed window in the next run (one minute later). This behavior continues for up to 60 failures (one hour).

Since one failure of a specific run reflects only one-minute delay, don't look at single failures. Instead, use the following query to monitor the delay of each analytic rule:

```kusto
_SentinelHealth()
| where SentinelResourceKind == "NRT"
| extend startTime = todatetime(ExtendedProperties["QueryStartTimeUTC"]), endTime = todatetime(ExtendedProperties["QueryEndTimeUTC"]), alertsCreated = toint(ExtendedProperties["AlertsGeneratedAmount"])
| where alertsCreated == 0 
| extend ruleDelay = datetime_diff('minute', endTime, startTime)
| project TimeGenerated, ruleDelay, SentinelResourceId
| render timechart
```

You can also define an analytics rule to trigger alerts on significant delays (for example, if an NRT rule has a delay of more than 10 minutes).

### Statuses, errors, and suggested steps

For either **Scheduled analytics rule run** or **NRT analytics rule run**, you might see any of the following statuses and descriptions:

- **Success**: Rule executed successfully, generating `<n>` alerts.
- **Success**: Rule executed successfully, but didn't reach the threshold (`<n>`) required to generate an alert.
- **Failure**: These descriptions explain rule failure and what you can do about them.

    | Description | Remediation |
    | --- | --- |
    | An internal server error occurred while running the query. |  |
    | The query execution timed out. |  |
    | A table referenced in the query wasn't found. | Verify that the relevant data source is connected. |
    | A semantic error occurred while running the query. | Try resetting the analytics rule by editing and saving it (without changing any settings). |
    | A function called by the query is named with a reserved word. | Remove or rename the function. |
    | A syntax error occurred while running the query. | Try resetting the analytics rule by editing and saving it (without changing any settings). |
    | The workspace doesn't exist. |  |
    | This query uses too many system resources and was prevented from running. | Review and tune the analytics rule. Consult our Kusto Query Language [Kusto Query Language overview](/en-us/kusto/query/?toc=/azure/sentinel/TOC.json&amp;bc=/azure/sentinel/breadcrumb/toc.json) and [Kusto Query Language best practices](/en-us/kusto/query/best-practices?view=microsoft-sentinel&amp;preserve-view=true&amp;toc=/azure/sentinel/TOC.json&amp;bc=/azure/sentinel/breadcrumb/toc.json) documentation. |
    | A function called by the query wasn't found. | Verify the existence in your workspace of all functions called by the query. |
    | The workspace used in the query wasn't found. | Verify that all workspaces in the query exist. |
    | You don't have permissions to run this query. | Try resetting the analytics rule by editing and saving it (without changing any settings). |
    | You don't have access permissions to one or more of the resources in the query. |  |
    | The query referred to a storage path that wasn't found. |  |
    | The query was denied access to a storage path. |  |
    | Multiple functions with the same name are defined in this workspace. | Remove or rename the redundant function and reset the rule by editing and saving it. |
    | This query didn't return any result. |  |
    | Multiple result sets in this query aren't allowed. |  |
    | Query results contain inconsistent number of fields per row. |  |
    | The rule's running was delayed due to long data ingestion times. |  |
    | The rule's running was delayed due to temporary issues. |  |
    | The alert wasn't enriched due to temporary issues. |  |
    | The alert wasn't enriched due to entity mapping issues. |  |
    | &lt;*number*&gt; entities were dropped in alert &lt;*name*&gt; due to the 32 KB alert size limit. |  |
    | &lt;*number*&gt; entities were dropped in alert &lt;*name*&gt; due to entity mapping issues. |  |
    | The query resulted in &lt;*number*&gt; events, which exceeds the maximum of &lt;*limit*&gt; results allowed for &lt;*rule type*&gt; rules with alert-per-row event-grouping configuration. Alert-per-row was generated for first &lt;*limit*-1&gt; events and an additional aggregated alert was generated to account for all events.- &lt;*number*&gt; = number of events returned by the query- &lt;*limit*&gt; = currently 150 alerts for scheduled rules, 30 for NRT rules- &lt;*rule type*&gt; = Scheduled or NRT |  |

## Use the auditing and health monitoring workbook

To visualize analytics rule health and audit data, install and configure the Analytics Health & Audit workbook from the Microsoft Sentinel content hub.

1. To make the workbook available in your workspace, install the workbook solution from the Microsoft Sentinel content hub:

    1. From the Microsoft Sentinel portal, select **Content hub (Preview)** from the **Content management** menu.
    2. In the **Content hub**, enter *health* in the search bar, and select **Analytics Health & Audit** from among the **Workbook** solutions under **Standalone** in the results.

        ![Screenshot of selection of analytics health workbook from content hub.](media/monitor-analytics-rule-integrity/select-workbook-from-content-hub.png)
    3. Select **Install** from the details pane, then select **Save** that appears in its place.
2. When the solution indicates it's installed, select **Workbooks** from the **Threat management** menu.

    ![Screenshot of indication that analytics health workbook solution is installed from content hub.](media/monitor-analytics-rule-integrity/installed.png)
3. In the **Workbooks** gallery, select the **Templates** tab, enter *health* in the search bar, and select **Analytics Health & Audit** from among the results.

    ![Screenshot of selecting analytics health workbook from template gallery.](media/monitor-analytics-rule-integrity/select-workbook-template.png)
4. Select **Save** in the details pane to create an editable and usable copy of the workbook. When the copy is created, select **View saved workbook**.
5. Once in the workbook, first select the **subscription** and **workspace** you want to view (they might already be selected), then define the **TimeRange** to filter the data according to your needs. Use the **Show help** toggle to display in-place explanation of the workbook.

    ![Screenshot of analytics rule health workbook overview tab.](media/monitor-analytics-rule-integrity/analytics-health-workbook-overview.png)

This workbook has three tabbed sections:

### Review health and audit summaries on the Overview tab

The **Overview** tab shows health and audit summaries:

- Health summaries of the status of analytics rule runs in the selected workspace: number of runs, successes and failures, and failure event details.
- Audit summaries of activities on analytics rules in the selected workspace: number of activities over time, number of activities by type, and number of activities of different types by rule.

### Use the Health tab to identify analytics rule issues

The **Health** tab lets you explore specific health events.

![Screenshot of selection of health tab in analytics health workbook.](media/monitor-analytics-rule-integrity/analytics-health-workbook-health-tab.png)

- Filter the whole page data by **status** (success or failure) and **rule type** (scheduled or NRT).
- See the trends of successful and failed rule runs (depending on the status filter) over the selected time period. You can "time brush" the trend graph to see a subset of the original time range. ![Screenshot of analytics rule runs over time in analytics health workbook.](media/monitor-analytics-rule-integrity/analytics-rule-runs-over-time.png)
- Filter the rest of the page by **reason**.
- See the total number of runs for all the analytics rules, displayed proportionally by status in a pie chart.
- Following that is a table showing the number of unique analytics rules that ran, broken down by rule type and status.
    - Select a status to filter the remaining charts for that status.
    - Clear the filter by selecting the "Clear selection" icon (it looks like an "Undo" icon) in the upper right corner of the chart. ![Screenshot of number of rules run by status and type in the analytics health workbook.](media/monitor-analytics-rule-integrity/number-rule-runs-by-status-and-type.png)
- See each status, with the number of possible reasons for that status. (Only reasons represented in the runs in the selected time frame are shown.)
    - Select a status to filter the remaining charts for that status.
    - Clear the filter by selecting the "Clear selection" icon (it looks like an "Undo" icon) in the upper right corner of the chart. ![Screenshot of number of unique reasons by status in analytics health workbook.](media/monitor-analytics-rule-integrity/unique-reasons-by-status.png)
- Next, see a list of those reasons, with the number of total rule runs combined and the number of unique rules that were run.
    - Select a reason to filter the following charts for that reason.
    - Clear the filter by selecting the "Clear selection" icon (it looks like an "Undo" icon) in the upper right corner of the chart. ![Screenshot of rule runs by unique reason in analytics health workbook.](media/monitor-analytics-rule-integrity/rule-runs-by-reason.png)
- After that is a list of the unique analytics rules that ran, with the latest results and trendlines of their success and failure (depending on the status selected to filter the list).
    - Select a rule to drill down and show a new table with all the runnings of that rule (in the selected time frame).
    - Clear that table by selecting the "Clear selection" icon (it looks like an "Undo" icon) in the upper right corner of the chart. ![Screenshot of list of unique rules run, with status and trendlines, in analytics health workbook.](media/monitor-analytics-rule-integrity/unique-rules-by-status-and-trend.png)
- If you select a rule in the list, a new table appears with the health details for the selected rule. ![Screenshot of list of runs of selected analytics rule, in analytics health workbook.](media/monitor-analytics-rule-integrity/health-events-for-rule.png)

### Use the Audit tab to review analytics rule changes

The **Audit** tab lets you drill down to particular audit events.

![Screenshot of selection of audit tab in analytics health workbook.](media/monitor-analytics-rule-integrity/analytics-health-workbook-audit-tab.png)

- Filter the whole page data by **audit rule type** (scheduled or Fusion, which are correlation-based rules that detect multistage attacks).
- See the trends of audited activity on analytics rules over the selected time period. You can "time brush" the trend graph to see a subset of the original time range. ![Screenshot of trending audit activity in analytics health workbook.](media/monitor-analytics-rule-integrity/audit-trending-by-activity.png)
- See the numbers of audited events, broken down by **activity** and **rule type**.
    - Select an activity to filter the following charts for that activity.
    - Clear the filter by selecting the "Clear selection" icon (it looks like an "Undo" icon) in the upper right corner of the chart. ![Screenshot of counts of audit events by activity and type in analytics health workbook.](media/monitor-analytics-rule-integrity/number-audit-events-by-activity-and-type.png)
- See the number of audited events by **rule name**.
    - Select a rule name to filter the following table for that rule, and to drill down and show a new table with all the activity on that rule (in the selected time frame). (See after the following screenshot.)
    - Clear the filter by selecting the "Clear selection" icon (it looks like an "Undo" icon) in the upper right corner of the chart. ![Screenshot of audited events by rule name and caller in analytics health workbook.](media/monitor-analytics-rule-integrity/activity-by-rule-name-and-caller.png)
- See the number of audited events by **caller** (the identity that performed the activity).
- If you selected a rule name in the preceding chart, another table appears showing the audited **activities** on that rule. Select the value that appears as a link in the ExtendedProperties column to open a side panel displaying the changes made to the rule. ![Screenshot of audit activity for selected rule in analytics health workbook.](media/monitor-analytics-rule-integrity/audit-activity-for-rule.png)