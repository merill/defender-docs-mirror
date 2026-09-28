---
layout: Conceptual
title: Manage KQL jobs - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/kql-manage-jobs
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
description: Managing KQL jobs in the Defender portal for Microsoft Sentinel data lake
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: zeinam
ms.topic: concept-article
ms.date: 2026-06-04T00:00:00.0000000Z
ms.collection: ms-security
locale: en-us
document_id: 05ee1d1d-aa20-83a8-937a-e2fd225f6d87
document_version_independent_id: d679f2cd-1006-9cbc-b8a2-884abe9d1f99
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/kql-manage-jobs.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/kql-manage-jobs
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/kql-manage-jobs.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: ae2cd443-0b4a-19cb-a857-6f64ba8e7517
---

# Manage KQL jobs - Microsoft Security | Microsoft Learn

A job is a one-time or scheduled task that runs against data in the Microsoft Sentinel data lake. The **Jobs** page, under **Microsoft Sentinel** &gt; **Data lake exploration** in the Microsoft Defender portal, lists every job in your tenant so you can monitor and manage them from one place.

The data lake supports three job types:

- **KQL jobs** run a Kusto Query Language (KQL) query against the data lake tier and promote the results to the analytics tier. You create them from the **KQL queries** editor or the **Jobs** page. For more information, see [KQL jobs](kql-jobs).
- **Notebook jobs** run a notebook on a schedule against data in the lake. You create them from the notebook authoring experience. For more information, see [Notebook jobs](notebook-jobs).
- **Graph jobs** run a custom graph built in the Microsoft Sentinel Visual Studio Code extension, either on demand or on a schedule. You create them when you publish or refresh a custom graph. For more information, see [Custom graphs overview](custom-graphs-overview) and Graph jobs in this article.

The Jobs management page provides the following functions:

- View all jobs in the Microsoft Sentinel data lake, including KQL, notebook, and graph jobs.
- View a summary of KQL, notebook, and graph jobs.
- View details of all jobs and apply filter to narrow down the list.
- View recent job health issues.
- Create a new job to run a KQL query. For more information on creating jobs, see [Create jobs in the Microsoft Sentinel data lake using KQL](kql-jobs). Notebook jobs and graph jobs can't be created from this page.
- Edit job details for KQL jobs.
- Disable a job, preventing it from running until you enable it again.
- Enable a job, allowing it to run again after being disabled.
- View job history, including the run times, and statuses of the job.
- Delete a job, removing it from the list of jobs. This action is permanent and can't be undone.

Note

Graph jobs and notebook jobs are **view-only** from the Jobs page. To change a graph or notebook job's query, schedule, or pool size, edit and republish the graph or notebook from the VS Code extension. The Jobs page doesn't support create, edit, or delete actions for graph or notebook jobs.

## KQL jobs

A KQL job runs a Kusto Query Language (KQL) query against the data lake tier and writes the results to the analytics tier, either once or on a schedule. You can create KQL jobs in the **KQL queries** editor or from the **Jobs** page. For more information about creating KQL jobs, see [Create jobs in the Microsoft Sentinel data lake using KQL](kql-jobs).

The Jobs page supports the full KQL job lifecycle: you can create, edit, enable or disable, view run history for, and delete a KQL job from this page. To find KQL jobs, open the Jobs page and look for rows where the **Job type** column shows **KQL**. For step-by-step procedures, see Manage jobs.

## Notebook jobs

A notebook job is a scheduled run of a notebook against data in the Microsoft Sentinel data lake. Notebook jobs are created from the VS Code extension when you schedule a notebook, not from the Jobs page. For more information about creating, editing, and scheduling notebook jobs, see [Notebook jobs](notebook-jobs).

To find notebook jobs, open the Jobs page and look for rows where the **Job type** column shows **Notebook**. Selecting a notebook job opens a details panel that shows:

- Job name and description.
- **Job type**: Notebook.
- Status (enabled or disabled) and most recent run status.
- Schedule configuration.
- Last run and next run times.

## Graph jobs

A graph job is a scheduled notebook-based custom graph job in your Microsoft Sentinel data lake tenant. Graph jobs are created when you publish a custom graph from Sentinel VS Code extension or when graphs are subsequently refreshed per your schedule configurations. For more information about creating custom graphs, see [Create custom graphs](create-custom-graphs) and [Custom graphs overview](custom-graphs-overview).

To find graph jobs, open the Jobs page and look for rows where the **Job type** column shows **Graph**. Selecting a graph job opens a details panel that shows:

- Job name and description.
- **Job type**: Graph.
- Status (enabled or disabled) and most recent run status.
- Schedule configuration.
- Pool size.
- Last run and next run times.

## Permissions

Microsoft Entra ID roles provide broad access across all workspaces in the data lake. To read tables across all workspaces, write to the analytics tier, and schedule jobs using KQL queries, you must have one of the supported Microsoft Entra ID roles. For more information on roles and permissions, see [Microsoft Sentinel data lake roles and permissions](../roles#roles-and-permissions-for-the-microsoft-sentinel-data-lake).

## Manage jobs

The Jobs page shows a list of jobs, including the job name, status, job type, last and next run dates, and the recent job health. You can filter the jobs by status, last run date, and creation date. The **Jobs status** column indicates whether the job is enabled or disabled. The **Job type** column indicates whether the job is a **KQL** job, a **Notebook** job, or a **Graph** job.

[![A screenshot showing the jobs page in the Defender portal.](media/kql-manage-jobs/jobs-page.png)](media/kql-manage-jobs/jobs-page.png#lightbox)

The **Recent health issues** column shows whether the job encountered any issues in its recent runs as per the filters. Select the link to view the job's health details.

[![A screenshot showing the recent health issues panel.](media/kql-manage-jobs/recent-health-issues.png)](media/kql-manage-jobs/recent-health-issues.png#lightbox)

To create a job from the jobs page, select **Create a new KQL job**. For more information on creating jobs, see [Create jobs in the Microsoft Sentinel data lake using KQL](kql-jobs).

### Job details

To see a job's details, select the job from the table. The job details panel opens, showing the job's details. You can enable and disable a job, view its history, edit, or delete it. Select the **Destination table** link to open the table in the KQL query editor in Advanced hunting. The query can be copied by selecting **Copy query**.

[![A screenshot showing the job details page.](media/kql-manage-jobs/manage-job-details.png)](media/kql-manage-jobs/manage-job-details.png#lightbox)

### View a job's run history

To view the history of a job, select **View history** in the job details panel. The job history panel opens, showing a list of job run times and statuses. The row count reflects the number of rows sent to the destination table in the analytics tier.

[![A screenshot showing the job history panel.](media/kql-manage-jobs/job-history.png)](media/kql-manage-jobs/job-history.png#lightbox)

## Manage KQL jobs

The jobs page supports the full lifecycle of KQL jobs, including creating, editing, enabling or disabling, and deleting a KQL job.

### Edit a KQL job

To edit a job, select **Edit** in the job details panel. The job details panel opens, allowing you to edit the following fields:

- Job description.
- KQL query. The query can be updated but must return the same output schema as the original query. For example, you can change the time range in the query, but you can't change the columns returned by the query.
- Job schedule. You can change the job to run once or on a schedule, or change the schedule.

Select **Next** to continue to the next screen.

After you edit the job, select **Submit** to save the changes. The job is updated and runs according to the new schedule or query.

Note

Editing a one-time job immediately triggers its execution.

### Enable or disable a KQL job

To enable or disable a job, select **Enable** or **Disable** in the job details panel. When a job is disabled, it won't run until you enable it again. The status of the job changes to reflect whether it's enabled or disabled.

Important

Disabling or deleting a KQL job doesn't stop any job runs that are already in progress or queued. Any runs that started before the job was disabled or deleted continue to completion. Any already queued jobs will run. Jobs scheduled to be run in the future and not queued will no longer be scheduled.

### Delete a KQL job

To delete a job, select **Delete** in the job details panel. A confirmation dialog appears, asking you to confirm the deletion. If you confirm, the job is permanently deleted and can't be recovered. You can't delete a running job.

## Considerations and limitations

For information on considerations and limitations when managing KQL jobs in the Microsoft Sentinel data lake, see [KQL jobs](kql-jobs#considerations-and-limitations).