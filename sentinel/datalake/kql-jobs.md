---
layout: Conceptual
title: Create jobs in the Microsoft Sentinel data lake - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/kql-jobs
breadcrumb_path: ../breadcrumb/toc.json
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
ms.subservice: sentinel-platform
search.appverid: met150
description: Use the Defender portal's Data lake exploration KQL queries to create and schedule jobs to promote data to the analytics tier.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: zeinam
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: ms-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 62ece617-03cc-5064-5db5-461729e10e7a
document_version_independent_id: f96bcd88-2b2f-42df-3541-6707ef298854
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/kql-jobs.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/kql-jobs
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/kql-jobs.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: d652b3c8-37b5-e3d5-cc2c-dedc77be9f2f
---

# Create jobs in the Microsoft Sentinel data lake - Microsoft Security | Microsoft Learn

Kusto Query Language (KQL) jobs are one-time or scheduled KQL queries on data in the Microsoft Sentinel data lake and federated tables. Federated tables are external data sources, such as Microsoft Entra ID, Microsoft 365, and Microsoft Resource Graph tables, that you can query alongside data lake tables without ingesting the data into your workspace. Use jobs for investigative and analytical scenarios, such as:

- Long-running one-time queries for incident investigations and incident response (IR)
- Data aggregation tasks that support enrichment workflows using low-fidelity logs
- Historical threat intelligence (TI) matching scans for retrospective analysis
- Anomaly detection scans that identify unusual patterns across multiple tables

KQL jobs are especially effective when queries use joins or unions across different datasets. Before you begin, make sure you meet the prerequisites, including data lake onboarding and required permissions.

Use jobs to promote data from the data lake tier to the analytics tier. Once in the analytics tier, use the advanced hunting KQL editor to query the data. Promoting data to the analytics tier has the following benefits:

- Combine current and historical data in the analytics tier or from federated tables to run advanced analytics and machine learning models on your data.
- Reduce query costs by running queries in the analytics tier.
- Combine data from multiple workspaces to a single workspace in the analytics tier.
- Combine Microsoft Entra ID, Microsoft 365, and Microsoft Resource Graph data in the analytics tier to run advanced analytics across data sources.

Note

Storage in the analytics tier incurs higher billing rates than in the data lake tier. To reduce costs, only promote data that you need to analyze further. Use the KQL in your query to project only the columns you need, and filter the data to reduce the amount of data promoted to the analytics tier.

You can promote data to a new table or append the results to an existing table in the analytics tier. When creating a new table, the table name is suffixed with *\_KQL\_CL* to indicate that the table was created by a KQL job.

Optionally, you can write output of a KQL job into another table in data lake tier to speed up investigation or use the enriched data for threat hunting. When creating a new table, the table name is suffixed with \_KQL if you write to System tables workspace.

## Prerequisites

To create and manage KQL jobs in the Microsoft Sentinel data lake, you need the following prerequisites.

### Onboard to the data lake

To create and manage KQL jobs in the Microsoft Sentinel data lake, you must first onboard to the data lake. For more information on onboarding to the data lake, see [Onboard to the Microsoft Sentinel data lake](sentinel-lake-onboarding).

### Permissions

Microsoft Entra ID roles provide broad access across all workspaces in the data lake. To read tables across all workspaces, write to the analytics tier, and schedule jobs using KQL queries, you must have one of the supported Microsoft Entra ID roles. For more information on roles and permissions, see [Microsoft Sentinel data lake roles and permissions](../roles#roles-and-permissions-for-the-microsoft-sentinel-data-lake).

To create new custom tables in the analytics tier, assign the **Log Analytics Contributor** role in the Log Analytics workspace to the data lake managed identity.

To assign the role, follow these steps:

1. In the Azure portal, go to the Log Analytics workspace that you want to assign the role to.
2. Select **Access control (IAM)** in the left navigation pane.
3. Select **Add role assignment**.
4. In the **Role** table, select \***Log Analytics Contributor**, then select **Next**.
5. Select **Managed identity**, then select **Select members**.
6. Your data lake managed identity is a system assigned managed identity named `msg-resources-<guid>`. Select the managed identity, then select **Select**.
7. Select **Review and assign**.

For more information on assigning roles to managed identities, see [Assign Azure roles using the Azure portal](/en-us/azure/role-based-access-control/role-assignments-portal).

## Create a job

You can create jobs to run on a schedule or one-time. When you create a job, you specify the destination workspace and table for the results. You can write the results to a new table or append them to an existing table in the analytics or data lake tier. You can't write the results to federated tables. You can create a new KQL job or create a job from a template containing the query and job settings. For more information, see Create a KQL job from a template.

1. Start the job creation process from KQL query editor, or from the jobs management page.

    1. To create a job from the KQL query editor, select the **Create job** button in the upper right corner of the query editor. [![A screenshot showing the create job button in the KQL query editor.](media/kql-jobs/kql-queries-create-job.png)](media/kql-jobs/kql-queries-create-job.png#lightbox)
    2. To create a job from the jobs management page, select **Microsoft Sentinel** &gt; **Data lake exploration** &gt; **Jobs** then select the **Create job** button. [![A screenshot showing the create job button on the jobs management page.](media/kql-jobs/create-job.png)](media/kql-jobs/create-job.png#lightbox)
2. Enter a **Job name**. The job name must be unique for the tenant. Job names can contain up to 256 characters. You can't use a `#` or a `-` in a job name.
3. Enter a **Job Description** providing the context and purpose of the job.
4. From the **Select workspace** dropdown, select the destination workspace. This workspace can be either System tables or a Sentinel workspace where you want to write the query results.
5. Select the destination table:

    1. To append to an existing table, select **Add to an existing table** and select the table name form the drop-down list. When adding to an existing table, the query results must match the schema of the existing table.
6. Select **Next**. [![A screenshot showing the new job details page.](media/kql-jobs/enter-job-details.png)](media/kql-jobs/enter-job-details.png#lightbox)
7. Review or write your query in the **Prepare the query** panel. Check that the time picker is set to the required time range for the job if the date range isn't specified in the query.
8. Select the workspaces to run the query against from the **Selected workspaces** drop-down. These workspaces are the source workspaces whose tables you want to query. The workspaces you select determine the tables available for querying. The selected workspaces apply to all query tabs in the query editor. When using multiple workspaces, the `union()` operator is applied by default to tables with the same name and schema from different workspaces. Use the `workspace()` operator to query a table from a specific workspace, for example `workspace("MyWorkspace").AuditLogs`.

    Note

    If you're writing to an existing table, the query must return results with a schema that matches the destination table schema. If the query doesn't return results with the correct schema, the job fails when it runs.

    Writing KQL jobs into System tables is currently in preview.
9. Select **Next**.

    [![A screenshot showing the review query panel.](media/kql-jobs/review-query.png)](media/kql-jobs/review-query.png#lightbox)

    On the **Schedule the query job** page, select whether you want to run the job once or on a schedule. If you select **One time**, the job runs as soon as the job definition is complete. If you select **Schedule**, you can specify a date and time for the job to run, or run the job on a recurring schedule.
10. Select **One time** or **Scheduled job**.

    Note

    Editing a one-time job immediately triggers its execution.
11. If you selected **Schedule**, enter the following details:

    1. Select the **Repeat frequency** from the drop-down. You can select **By minute**, **Hourly**, **Daily**, **Weekly**, or **Monthly**.
    2. Set the **Repeat every** value for how often you want the job to run with respect to the selected frequency.
    3. Under **Set schedule**, select a **From** date and enter a time. The job start time in the **From** field must be at least 30 minutes after job creation. The job runs from this date and time according to the frequency select in the **Run every** dropdown.
    4. Select the **To** date, and enter a time to specify when the job schedule finishes. If you want the schedule to continue indefinitely, select **Set job to run indefinitely**.

    Job from and to times are set for the user's locale.

    Note

    If you schedule a job to run at a high frequency, for example every 30 minutes, you must take into account the time it takes for data to become available in the data lake. There's typically a latency of up to 15 minutes before newly ingested data is available for querying.
12. Select **Next** to review the job details.

    [![A screenshot showing the schedule job panel.](media/kql-jobs/schedule-query-job.png)](media/kql-jobs/schedule-query-job.png#lightbox)
13. Review the job details and select **Submit** to create the job. If the job is a one-time job, it runs after you select **Submit**. If the job is scheduled, it's added to the list of jobs in the **Jobs** page and runs according to the start data and time. [![A screenshot showing the review job details panel.](media/kql-jobs/review-job-details.png)](media/kql-jobs/review-job-details.png#lightbox)
14. The job is scheduled and the following page is displayed. You can view the job by selecting the link. [![A screenshot showing the job created page.](media/kql-jobs/job-successfully-scheduled.png)](media/kql-jobs/job-successfully-scheduled.png#lightbox)

## Create a job from a template

You can create a KQL job from a predefined job template. Job templates contain the KQL query and job settings, such as the destination workspace and table, schedule, and description. You can create your own job templates or use built-in templates provided by Microsoft.

To create a job from a template, follow these steps:

1. From the **Jobs** page or the KQL query editor, select **Create job**, then select **Create from template**.
2. On the **Job templates** page, select the template you want to use from the list of available templates.
3. Review the **Description** and **KQL query** from the template.
4. Select **Create job from template**.

    [![A screenshot showing the job templates page.](media/kql-jobs/create-job-from-template.png)](media/kql-jobs/create-job-from-template.png#lightbox)
5. The job creation wizard opens with the **Create a new KQL job** page. The job details prepopulated from the template except for the destination workspace.
6. Select the destination workspace from the **Select workspace** dropdown.
7. Review and modify the job details as required, then select **Next** to proceed through the job creation wizard.
8. The remaining steps are the same as those in Create a job. The fields are prepopulated from the template and can be modified as needed.

The following templates are available:

| Template name | Category |
| --- | --- |
| **Anomalous sign-in locations increase**<br>Analyze trend analysis of Entra ID sign-in logs to detect unusual location changes for users across applications by computing trend lines of location diversity. It highlights the top three accounts with the steepest increase in location variability and lists their associated locations within 21-day windows.**Destination table:** UserAppSigninLocationTrend**Query lookback:** 1 day**Schedule:** daily**Start date:** Current date + 1 hr | Hunting |
| **Anomalous sign-in behavior based on location changes**<br>Identify anomalous sign-in behavior based on location changes for Entra ID users and apps to detect sudden changes in behavior.**Destination table:** UserAppSigninLocationAnomalies**Query lookback:** 1 day**Schedule:** daily**Start date:** Current date + 1 hr | Anomaly detection |
| **Audit rare activity by app**<br>Find apps performing rare actions (for example, consent, grants) that can quietly create privilege. Compare the current day to last 14 days of audits to identify new audit activities. Useful for tracking malicious activity related to user/group additions or removals by Azure Apps and automated approvals.**Destination table:** AppAuditRareActivity**Query lookback:** 14 days**Schedule:** daily**Start date:** Current date + 1 hr | Hunting |
| **Azure rare subscription level operations**<br>Identify sensitive Azure subscription-level events based on Azure Activity Logs. For example, monitoring based on operation name "Create or Update Snapshot", which is used for creating backups but could be misused by attackers to dump hashes or extract sensitive information from the disk.**Destination table:** AzureSubscriptionSensitiveOps**Query lookback:** 14 days**Schedule:** daily**Start date:** Current date + 1 hr | Hunting |
| **Daily activity trend by app in AuditLogs**<br>From the last 14 days, identify any "Consent to application" operation occurs by a user or app. This could indicate that permissions to access the listed AzureApp was provided to a malicious actor. Consent to application, add service principal and add Auth2PermissionGrant events should be rare. If available, extra context is added from the AuditLogs based on CorrleationId from the same account that performed "Consent to application".**Destination table:** AppAuditActivityBaseline**Query lookback:** 14 days**Schedule:** daily**Start date:** Current date + 1 hr | Baseline |
| **Daily location trend per user or app in SignInLogs**<br>Build daily trends for all user sign-ins, locations count, and their app usage.**Destination table:** UserAppSigninLocationBaseline**Query lookback:** 1 day**Schedule:** daily**Start date:** Current date + 1 hr | Baseline |
| **Daily network traffic trend per destination IP**<br>Create a baseline including bytes and distinct peers to detect beaconing and exfiltration.**Destination table:** NetworkTrafficDestinationIPDailyBaseline**Query lookback:** 1 day**Schedule:** daily**Start date:** Current date + 1 hr | Baseline |
| **Daily network traffic trend per destination IP with data transfer stats**<br>Identify internal host that reached out outbound destination, including volume trends, estimating blast radius.**Destination table:** NetworkTrafficDestinationIPTrend**Query lookback**: 1 day**Schedule:** daily**Start date:** Current date + 1 hr | Hunting |
| **Daily network traffic trend per source IP**<br>Create a baseline including bytes and distinct peers to detect beaconing and exfiltration.**Destination table:** NetworkTrafficSourceIPDailyBaseline**Query lookback:** 1 day**Schedule:** daily**Start date:** Current date + 1 hr | Baseline |
| **Daily network traffic trend per source IP with data transfer stats**<br>Today's connections and bytes are evaluated against the host's day-over-day baseline to determine whether the observed behaviors deviate significantly from established pattern.**Destination table:** NetworkTrafficSourceIPTrend**Query lookback:** 1 day**Schedule:** daily**Start date:** Current date + 1 hr | Hunting |
| **Daily sign-in location trend per user and app**<br>Create a sign-in baseline for each user or application with typical geographic and IP, enabling efficient and cost-effective anomaly detection at scale.**Destination table:** UserAppSigninLocationDailyBaseline**Query lookback:** 1 day**Schedule:** daily**Start date:** Current date + 1 hr | Baseline |
| **Daily process execution trend**<br>Identify new processes and prevalence, making "new rare process" detections easier.**Destination table:** EndpointProcessExecutionBaseline**Query lookback:** 1 day**Schedule:** daily**Start date:** Current date + 1 hr | Baseline |
| **Entra ID rare user agent per app**<br>Establish a baseline of the type of UserAgent (that is, browser, office application, etc.) that is typically used for a particular application by looking back for a number of days. It then searches the current day for any deviations from this pattern, that is, types of UserAgents not seen before in combination with this application.**Destination table:** UserAppRareUserAgentAnomalies**Query lookback:** 7 days**Schedule:** daily**Start date:** Current date + 1 hr | Anomaly detection |
| **Network log IOC matching**<br>Identify any IP indicators of compromise (IOCs) from threat intelligence (TI), by searching for matches in CommonSecurityLog.**Destination table:** NetworkLogIOCMatches**Query lookback:** 1 hour**Schedule:** hourly**Start date:** Current date + 1 hr | Hunting |
| **New processes observed in last 24 hours**<br>New processes in stable environments may indicate malicious activity. Analyzing sign-in sessions where these binaries ran can help identify attacks.**Destination table:** EndpointNewProcessExecutions**Query lookback:** 14 days**Schedule:** daily**Start date:** Current date + 1 hr | Hunting |
| **SharePoint file operation via previously unseen IPs**<br>Identify anomalies using user behavior by setting a threshold for significant changes in file upload/download activities from new IP addresses. It establishes a baseline of typical behavior, compares it to recent activity, and flags deviations exceeding a default threshold of 25.**Destination table:** SharePointFileOpsNewIPs**Query lookback:** 14 days**Schedule:** daily**Start date:** Current date + 1 hr | Hunting |
| **Palo Alto potential network beaconing**<br>Identify beaconing patterns from Palo Alto Network traffic logs based on recurrent time delta patterns. The query uses various KQL functions to calculate time deltas and then compares it with total events observed in a day to find percentage of beaconing.**Destination table:** PaloAltoNetworkBeaconingTrend**Query lookback:** 1 day**Schedule:** daily**Start date:** Current date + 1 hr | Hunting |
| **Windows suspicious login outside normal hours**<br>Identify unusual Windows sign-in events outside a user's normal hours by comparing with the last 14 days' sign-in activity, flagging anomalies based on historical patterns.**Destination table:** WindowsLoginOffHoursAnomalies**Query lookback:** 14 days**Schedule:** daily**Start date:** Current date + 1 hr | Anomaly detection |

## Considerations and limitations

When you create jobs in the Microsoft Sentinel data lake, consider the following limitations and best practices:

## Choose a data tier for KQL job output

KQL jobs can write data to either the Analytics tier or the Data lake tier, depending on the tier of the destination table. When creating a new table through the job creation wizard, you can select system tables as the destination workspace to write data directly to the data lake. Tables created in this way are created and stored directly in the data lake tier and are automatically suffixed with \_KQL.

## KQL considerations for data lake jobs

The following KQL limitations apply to data lake jobs:

- All KQL operators and functions are supported except for the following:

    - `adx()`
    - `arg()`
    - `externaldata()`
    - `ingestion_time()`
- When you use the `stored_query_results` command, provide the time range in the KQL query. The time selector above the query editor doesn't work with this command.
- User-defined functions aren't supported.

## Job naming and scheduling limits

The following naming and scheduling limitations apply to KQL jobs:

- Job names must be unique for the tenant.
- Job names can be up to 256 characters.
- Job names can't contain a `#` or a `-`.
- Job start time must be at least 30 minutes after job creation or editing.

## Source workspaces deletion

If a source workspace referenced by a scheduled KQL job is deleted, the job might continue to run and fail on each scheduled execution until the schedule expires or the job is modified. To prevent repeated failures and unnecessary resource consumption, jobs that reference deleted source workspaces are automatically placed in a **Disabled** state and require user action before they can resume.

## Data lake ingestion latency

The data lake tier stores data in cold storage. Unlike hot or near real-time analytics tiers, cold storage is optimized for long-term retention and cost efficiency and doesn't provide immediate access to newly ingested data. When new rows are added to existing tables in the data lake or in federated tables, there's a typical latency of up to 15 minutes before the data is available for querying. Account for the ingestion latency when you run queries and schedule KQL jobs by ensuring that lookback windows and job schedules are configured to avoid data that isn't available yet.

To avoid querying data that might not yet be available, include a delay parameter in your KQL queries or jobs. For example, when you schedule automated jobs, set the query's end time to `now() - delay`, where `delay` matches the typical data readiness latency of 15 minutes. This approach ensures that queries only target data that's fully ingested and ready for analysis.

The following KQL query detects events within a 15-minute lookback window while accounting for ingestion delay. The `lookback` variable controls the query time range, and the `delay` variable offsets the window to ensure only fully ingested data is queried.

```kql
let lookback = 15m;
let delay = 15m;
let endTime = now() - delay;
let startTime = endTime - lookback;
CommonSecurityLog
| where TimeGenerated between (startTime .. endTime)
```

This approach is effective for jobs with short lookback windows or frequent execution intervals.

Consider overlapping the lookback period with job frequency to reduce the risk of missing late-arriving data.

For more information, see [Handle ingestion delay in scheduled analytics rules](/en-us/azure/sentinel/ingestion-delay).

### Column names

Column names must start with a letter.

The following standard columns aren't supported for export. The ingestion process overwrites these columns in the destination tier:

- TenantId
- \_TimeReceived
- Type
- SourceSystem
- \_ResourceId
- \_SubscriptionId
- \_ItemId
- \_BilledSize
- \_IsBillable
- \_WorkspaceId
- `TimeGenerated` is overwritten if it's older than two days. To preserve the original event time, write the source timestamp to a separate column.

For service limits, see [Microsoft Sentinel data lake service limits](sentinel-lake-service-limits#service-parameters-and-limits-for-kql-jobs).

Note

Partial results might be promoted if the job's query exceeds the one hour limit.

## Service parameters and limits for KQL jobs

The following table lists the service parameters and limits for KQL jobs in the Microsoft Sentinel data lake.

Note

All limits in this table apply **per tenant**. There's no per-user limit. KQL jobs have their own concurrency quota and don't share counters with KQL queries.

When the concurrent-job-execution limit is exceeded, the request is **rejected** and not queued. The counter decrements as soon as a running job finishes.

| Category | Parameter/limit |
| --- | --- |
| Concurrent job execution per tenant | 5 |
| Job query execution timeout | 1 hour |
| Jobs per tenant (enabled jobs) | 100 |
| Number of output tables per job | 1 |
| Query scope | Multiple workspaces |
| Query time range | Up to 12 years |

For troubleshooting tips and error messages, see [Troubleshooting KQL queries for the Microsoft Sentinel data lake](kql-troubleshoot).