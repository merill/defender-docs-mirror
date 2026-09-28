---
layout: Conceptual
title: Audit and track changes to incident tasks in Microsoft Sentinel in the Azure portal | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/audit-track-tasks
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
description: This article explains how you, as a SOC manager, can audit the history of Microsoft Sentinel incident tasks, and track changes to them, in order to gauge your task assignments and their contribution to your SOC's efficiency and effectiveness.
ms.author: guywild
author: guywi-ms
ms.reviewer: idpelleg
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 91ea7c38-1dfa-e1c2-d156-1fb2aeeeebc9
document_version_independent_id: cab690bc-9918-9366-cde7-7fb37611b1d3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/audit-track-tasks.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/audit-track-tasks
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/audit-track-tasks.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
platformId: d37a9e8e-0524-827f-2abe-47466a85ae32
---

# Audit and track changes to incident tasks in Microsoft Sentinel in the Azure portal | Microsoft Learn

[Incident tasks](incident-tasks) ensure comprehensive and uniform treatment of incidents across all SOC personnel. Task lists are typically defined according to determinations made by senior analysts or SOC managers, and put into practice using automation rules or playbooks.

Your analysts can see the list of tasks they need to perform for a particular incident on the incident details page, and mark them complete as they go. Analysts can also create their own tasks on the spot, manually, right from within the incident.

This article explains how you, as a SOC manager, can audit the history of Microsoft Sentinel incident tasks, and track the changes made to them throughout their life cycle, in order to gauge the efficacy of your task assignments and their contribution to your SOC's efficiency and proper functioning.

## Structure of Tasks array in the SecurityIncident table

The *SecurityIncident* table is an audit table—it stores not the incidents themselves, but rather records of the life of an incident: its creation and any changes made to it. Any time an incident is created or a change is made to an incident, a record is generated in this table showing the now-current state of the incident.

The addition of task-detail fields to the schema of the *SecurityIncident* table allows you to audit tasks in greater depth.

The detailed information added to the **Tasks** field consists of key-value pairs taking the following structure:

| Key | Value description |
| --- | --- |
| **createdBy** | The identity that created the task:**- email**: email address of identity**- name**: name of the identity**- objectId**: GUID of the identity**- userPrincipalName**: UPN of the identity |
| **createdTimeUtc** | Time the task was created, in UTC. |
| **lastCompletedTimeUtc** | Time the task was marked complete, in UTC. |
| **lastModifiedBy** | The identity that last modified the task:**- email**: email address of identity**- name**: name of the identity**- objectId**: GUID of the identity**- userPrincipalName**: UPN of the identity |
| **lastModifiedTimeUtc** | Time the task was last modified, in UTC. |
| **status** | Current status of the task: New, Completed, Deleted. |
| **taskId** | Resource ID of the task. |
| **title** | Friendly name given to the task by its creator. |

## View incident tasks in the SecurityIncident table

Apart from the **Incident tasks workbook**, you can audit task activity by querying the *SecurityIncident* table in **Logs**. This section shows you how to query the table and read and understand the results to get task activity information.

1. In the **Logs** page, enter the following query in the query window and run it. This query will return all the incidents that have any tasks assigned.

    ```kusto
    SecurityIncident
    | where array_length( Tasks) > 0
    ```

    You can add any number of statements to the query to filter and narrow down the results. To demonstrate how to view and understand the results, we're going to add statements to filter the results so that we only see the tasks for a single incident, and we'll also add a `project` statement so that we see only those fields that will be useful for our purposes, without a lot of clutter.

    For more information, see [Kusto Query Language overview](/en-us/kusto/query/?toc=/azure/sentinel/TOC.json&amp;bc=/azure/sentinel/breadcrumb/toc.json).

    ```kusto
    SecurityIncident
    | where array_length( Tasks) > 0
    | where IncidentNumber == "405211"
    | sort by LastModifiedTime desc 
    | project IncidentName, Title, LastModifiedTime, Tasks
    ```
2. Let's look at the most recent record for this incident, and find the list of tasks associated with it.

    1. Select the expander next to the top row in the query results (which have been sorted in descending order of recency).

        [![Screenshot of query results showing an incident with its tasks.](media/audit-track-tasks/incident-with-tasks-query-1.png)](media/audit-track-tasks/incident-with-tasks-query-1.png#lightbox)
    2. The *Tasks* field is an array of the current state of all the tasks in this incident. Select the expander to view each item in the array in its own row.

        [![Screenshot of query results showing an incident with its tasks expanded.](media/audit-track-tasks/incident-with-tasks-query-2.png)](media/audit-track-tasks/incident-with-tasks-query-2.png#lightbox)
    3. Now you see that there are two tasks in this incident. Each one is represented in turn by an expandable array. Select a single task's expander to view its information.

        [![Screenshot of query results showing an incident with a single task expanded.](media/audit-track-tasks/incident-with-tasks-query-3.png)](media/audit-track-tasks/incident-with-tasks-query-3.png#lightbox)
    4. Here you see the details for the first task in the array ("0" being the index position of the task in the array). The *title* field shows the name of the task as displayed in the incident.

### View tasks added to the list

Perform the following steps to add a task to an incident and observe how the *SecurityIncident* record changes.

1. Let's add a task to the incident, and then we'll come back here, run the query again, and see the changes in the results.

    1. On the **Incidents** page, enter the incident ID number in the Search bar.
    2. Open the incident details page and select **Tasks** from the toolbar.
    3. Add a new task, give it the name "This task is a test task!", then select **Save**. The last task shown below is what you should end up with:

        ![Screenshot shows incident tasks panel.](media/audit-track-tasks/incident-task-list-task-added.png)
2. Now let's return to the **Logs** page and run the *SecurityIncident* query again.

    In the results you'll see that there's a **new record in the table** for this same incident (note the timestamps). Expand the record and you'll see that while the record we saw before had two tasks in its *Tasks* array, the new one has three. The newest task is the one we just added, as you can see by its title.

    [![Screenshot of query results showing an incident with its newly created task.](media/audit-track-tasks/incident-with-tasks-query-5.png)](media/audit-track-tasks/incident-with-tasks-query-5.png#lightbox)

### View status changes to tasks

Now, if we go back to the task titled "This task is a test task!" in the incident details page and mark it as complete, and then come back to **Logs** and rerun the query again, we'll see yet another new record for the same incident, this time showing our task's new status as **Completed**.

[![Screenshot of query results showing an incident task with its new status.](media/audit-track-tasks/incident-with-tasks-query-6.png)](media/audit-track-tasks/incident-with-tasks-query-5.png#lightbox)

### View deletion of tasks

Let's go back to the task list in the incident details page and delete the task titled "This task is a test task!".

When we come back to **Logs** and rerun the incident-task query, we'll see another new record, only this time the status for our task—the one titled "This task is a test task!"—will be **Deleted**.

**However**— once the task has appeared one such time in the array (with a **Deleted** status), it will no longer appear in the **Tasks** array in new records for that incident in the **SecurityIncident** table. Existing earlier records for the incident will continue to preserve the evidence that this task once existed.

## View active tasks belonging to a closed incident

The following query allows you to see if an incident was closed but not all its assigned tasks were completed. This knowledge can help you verify that any remaining loose ends in your investigation were brought to a conclusion—all relevant parties were notified, all comments were entered, all responses were verified, and so on. The query uses the `arg_max` aggregation function to return only the most recent record for each incident and for each task, so the results reflect the latest state.

Run the following query to retrieve the most recent record for each incident, filter for closed incidents, and return any tasks that are not yet completed or deleted:

```kusto
SecurityIncident
| summarize arg_max(TimeGenerated, *) by IncidentNumber
| where Status == 'Closed'
| mv-expand Tasks
| evaluate bag_unpack(Tasks)
| summarize arg_max(lastModifiedTimeUtc, *) by taskId
| where status !in ('Completed', 'Deleted')
| project TaskTitle = ['title'], TaskStatus = ['status'], createdTimeUtc, lastModifiedTimeUtc = column_ifexists("lastModifiedTimeUtc", datetime(null)), TaskCreator = ['createdBy'].name, lastModifiedBy, IncidentNumber, IncidentOwner = Owner.userPrincipalName
| sort by lastModifiedTimeUtc desc
```

For more information about the Kusto operators and functions used in the example queries in this article, see:

- [***where*** operator](/en-us/kusto/query/where-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***project*** operator](/en-us/kusto/query/project-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***sort*** operator](/en-us/kusto/query/sort-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***summarize*** operator](/en-us/kusto/query/summarize-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***arg\_max()*** aggregation function](/en-us/kusto/query/arg-max-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true)

For more information on KQL, see [Kusto Query Language (KQL) overview](/en-us/kusto/query/?view=microsoft-sentinel&amp;preserve-view=true).

Other resources:

- [KQL quick reference](/en-us/kusto/query/kql-quick-reference?view=microsoft-sentinel&amp;preserve-view=true)
- [Kusto Query Language learning resources](/en-us/kusto/query/kql-learning-resources?view=microsoft-sentinel&amp;preserve-view=true)