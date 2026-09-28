---
layout: Conceptual
title: Monitor the Health of your Microsoft Sentinel Automation Rules and Playbooks | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/monitor-automation-health
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
description: Use the SentinelHealth and AzureDiagnostics data tables to keep track of your automation rules' and playbooks' execution and performance.
ms.author: monaberdugo
author: mberdugo
ms.reviewer: sshuster
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: b4d2e687-5014-a7de-50a7-5f4d88bcc4bf
document_version_independent_id: 74f0f6be-5c04-1d2e-1bc9-d8020415755e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/monitor-automation-health.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/monitor-automation-health
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/monitor-automation-health.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 915192d5-134c-773e-8da9-4ee03a15e8a6
---

# Monitor the Health of your Microsoft Sentinel Automation Rules and Playbooks | Microsoft Learn

To ensure proper functioning and performance of your security orchestration, automation, and response operations in your Microsoft Sentinel service, keep track of the health of your automation rules and playbooks by monitoring their execution logs.

Set up notifications of health events for relevant stakeholders, who can then take action. For example, define and send email or Microsoft Teams messages, create new tickets in your ticketing system, and so on.

This article describes how to use Microsoft Sentinel's health monitoring features to keep track of your automation rules and playbooks's health from within Microsoft Sentinel. For more information, see [Auditing and health monitoring in Microsoft Sentinel](health-audit).

## Use the SentinelHealth data table

To get automation health data from the *SentinelHealth* data table, first turn on the Microsoft Sentinel health feature for your workspace. For more information, see [Turn on health monitoring for Microsoft Sentinel](enable-monitoring).

Once the health feature is turned on, the *SentinelHealth* data table is created at the first success or failure event generated for your automation rules and playbooks.

### Understanding SentinelHealth table events

The following types of automation health events are logged in the *SentinelHealth* table:

- **Automation rule run**: Logged whenever an automation rule's conditions are met, causing it to run. Besides the fields in the basic *SentinelHealth* table, these events include [extended properties unique to the running of automation rules](health-table-reference#automation-rules), including a list of the playbooks called by the rule. The following sample query displays these events:

    ```kusto
    SentinelHealth
    | where OperationName == "Automation rule run"
    ```
- **Playbook was triggered**: Logged whenever a playbook is triggered on an incident manually from the portal or through the API. Besides the fields in the basic *SentinelHealth* table, these events include [extended properties unique to the manual triggering of playbooks](health-table-reference#playbooks). The following sample query displays these events:

    ```kusto
    SentinelHealth
    | where OperationName == "Playbook was triggered"
    ```

For more information, see [SentinelHealth table columns schema](health-table-reference#sentinelhealth-table-columns-schema).

### Statuses, errors and suggested steps

For the **Automation rule run** status, you might see the following statuses:

- **Success**: Rule executed successfully, triggering all actions.
- **Partial success**: Rule executed and triggered at least one action, but some actions failed.
- **Failure**: Automation rule didn't run any action due to one of the following reasons:

    - Conditions evaluation failed.
    - Conditions met, but the first action failed.

For the **Playbook was triggered** status, you might see the following statuses:

- **Success**: Playbook was triggered successfully.
- **Failure**: Playbook couldn't be triggered.

    Note

    **Success** means only that the automation rule successfully triggered a playbook. It doesn't tell you when the playbook started or ended, the results of the actions in the playbook, or the final result of the playbook.

    To find this information, query the Logic Apps diagnostics logs. For more information, see Get the complete automation picture.

### Error descriptions and suggested actions

The following table describes common automation rule and playbook errors and recommended actions to resolve them.

| Error description | Suggested actions |
| --- | --- |
| **Could not add task: *&lt;TaskName&gt;*.**Incident/alert was not found. | Make sure the incident/alert exists and try again. |
| **Could not add task: *&lt;TaskName&gt;*.**Incident already contains the maximum allowed number of tasks. | If this task is required, see if there are any tasks that can be removed or consolidated, then try again. |
| **Could not modify property: *&lt;PropertyName&gt;*.**Incident/alert was not found. | Make sure the incident/alert exists and try again. |
| **Could not modify property: *&lt;PropertyName&gt;*.**Too many requests, exceeding throttling limits. |  |
| **Could not trigger playbook: *&lt;PlaybookName&gt;*.**Incident/alert was not found. | If the error occurred when trying to trigger a playbook on demand, make sure the incident/alert exists and try again. |
| **Could not trigger playbook: *&lt;PlaybookName&gt;*.**Either the playbook was not found, or Microsoft Sentinel was missing permissions on it. | Edit the automation rule, find and select the playbook in its new location, and save. Make sure Microsoft Sentinel has [permission to run this playbook](tutorial-respond-threats-playbook?tabs=LAC#respond-to-incidents). |
| **Could not trigger playbook: *&lt;PlaybookName&gt;*.**Contains an unsupported trigger type. | Make sure your playbook starts with the [correct Logic Apps trigger](playbook-triggers-actions#microsoft-sentinel-triggers-summary): Microsoft Sentinel Incident or Microsoft Sentinel Alert. |
| **Could not trigger playbook: *&lt;PlaybookName&gt;*.**The subscription is disabled and marked as read-only. Playbooks in this subscription cannot be run until the subscription is re-enabled. | Re-enable the Azure subscription in which the playbook is located. |
| **Could not trigger playbook: *&lt;PlaybookName&gt;*.**The playbook was disabled. | Enable your playbook, in Microsoft Sentinel in the Active Playbooks tab under Automation, or in the Logic Apps resource page. |
| **Could not trigger playbook: *&lt;PlaybookName&gt;*.**Invalid template definition. | There is an error in the playbook definition. Go to the Logic Apps designer to fix the issues and save the playbook. |
| **Could not trigger playbook: *&lt;PlaybookName&gt;*.**Access control configuration restricts Microsoft Sentinel. | Logic Apps configurations allow restricting access to trigger the playbook. This restriction is in effect for this playbook. Remove this restriction so Microsoft Sentinel is not blocked. [Restrict access by IP address range](/en-us/azure/logic-apps/logic-apps-securing-a-logic-app?tabs=azure-portal#restrict-access-by-ip-address-range) |
| **Could not trigger playbook: *&lt;PlaybookName&gt;*.**Microsoft Sentinel is missing permissions to run it. | Microsoft Sentinel requires [permissions to run playbooks](tutorial-respond-threats-playbook?tabs=LAC#respond-to-incidents). |
| **Could not trigger playbook: *&lt;PlaybookName&gt;*.**Playbook wasn’t migrated to new permissions model. Grant Microsoft Sentinel permissions to run this playbook and resave the rule. | Grant Microsoft Sentinel [permissions to run this playbook](tutorial-respond-threats-playbook?tabs=LAC#respond-to-incidents) and resave the rule. |
| **Could not trigger playbook: *&lt;PlaybookName&gt;*.**Too many requests, exceeding workflow throttling limits. | The number of waiting workflow runs has exceeded the maximum allowed limit. Try increasing the value of `'maximumWaitingRuns'` in [trigger concurrency configuration](/en-us/azure/logic-apps/logic-apps-workflow-actions-triggers#change-waiting-runs-limit). |
| **Could not trigger playbook: *&lt;PlaybookName&gt;*.**Too many requests, exceeding throttling limits. | Learn more about [throttling limits](/en-us/azure/azure-resource-manager/management/request-limits-and-throttling). |
| **Could not trigger playbook: *&lt;PlaybookName&gt;*.**Access was forbidden. Managed identity is missing configuration or Logic Apps network restriction has been set. | If the playbook uses managed identity, [make sure the managed identity was assigned with permissions](authenticate-playbooks-to-sentinel#authenticate-with-managed-identity). The playbook may have network restriction rules preventing it from being triggered as they block Microsoft Sentinel service. |
| **Could not trigger playbook: *&lt;PlaybookName&gt;*.**The subscription or resource group was locked. | Remove the lock to allow Microsoft Sentinel trigger playbooks in the locked scope. Learn more about [locked resources](/en-us/azure/azure-resource-manager/management/lock-resources?tabs=json). |
| **Could not trigger playbook: *&lt;PlaybookName&gt;*.**Caller is missing required playbook-triggering permissions on playbook, or Microsoft Sentinel is missing permissions on it. | The user trying to trigger the playbook on demand is missing Logic Apps Contributor role on the playbook or to trigger the playbook. [Restrict access to a logic app by IP address range](/en-us/azure/logic-apps/logic-apps-securing-a-logic-app?tabs=azure-portal#restrict-access-by-ip-address-range) |
| **Could not trigger playbook: *&lt;PlaybookName&gt;*.**Invalid credentials in connection. | [Check the credentials your connection is using](authenticate-playbooks-to-sentinel#manage-your-api-connections) in the **API connections** service in the Azure portal. |
| **Could not trigger playbook: *&lt;PlaybookName&gt;*.**Playbook ARM ID is not valid. |  |

## Get the complete automation picture

Microsoft Sentinel's health monitoring table allows you to track when playbooks are triggered, but to monitor what happens inside your playbooks and their results when they're run, you must also [turn on diagnostics in Azure Logic Apps](/en-us/azure/logic-apps/monitor-workflows-collect-diagnostic-data) to ingest the following events to the *AzureDiagnostics* table:

- {Action name} started
- {Action name} ended
- Workflow (playbook) started
- Workflow (playbook) ended

These added events provide additional insights into the actions being taken in your playbooks.

### Turn on Azure Logic Apps diagnostics

For each playbook you're interested in monitoring, [enable Log Analytics for your logic app](/en-us/azure/logic-apps/monitor-workflows-collect-diagnostic-data). Make sure to select **Send to Log Analytics workspace** as your log destination, and choose your Microsoft Sentinel workspace.

### Correlate Microsoft Sentinel and Azure Logic Apps logs

Now that you have logs for your automation rules and playbooks *and* logs for your individual Logic Apps workflows in your workspace, you can correlate them to get the complete picture. Consider the following sample query:

```kusto
SentinelHealth 
| where SentinelResourceType == "Automation rule"
| mv-expand TriggeredPlaybooks = ExtendedProperties.TriggeredPlaybooks
| extend runId = tostring(TriggeredPlaybooks.RunId)
| join (AzureDiagnostics 
    | where OperationName == "Microsoft.Logic/workflows/workflowRunCompleted"
    | project
        resource_runId_s,
        playbookName = resource_workflowName_s,
        playbookRunStatus = status_s)
    on $left.runId == $right.resource_runId_s
| project
    RecordId,
    TimeGenerated,
    AutomationRuleName= SentinelResourceName,
    AutomationRuleStatus = Status,
    Description,
    workflowRunId = runId,
    playbookName,
    playbookRunStatus
```

See more information on the following items used in the preceding examples in the Kusto documentation:

- [***where*** operator](/en-us/kusto/query/where-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***mv-expand*** operator](/en-us/kusto/query/mv-expand-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***extend*** operator](/en-us/kusto/query/extend-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***join*** operator](/en-us/kusto/query/join-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***project*** operator](/en-us/kusto/query/project-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***tostring()*** function](/en-us/kusto/query/tostring-function?view=microsoft-sentinel&amp;preserve-view=true)

For more information on KQL, see [Kusto Query Language (KQL) overview](/en-us/kusto/query/?view=microsoft-sentinel&amp;preserve-view=true).

Other resources:

- [KQL quick reference](/en-us/kusto/query/kql-quick-reference?view=microsoft-sentinel&amp;preserve-view=true)
- [Kusto Query Language learning resources](/en-us/kusto/query/kql-learning-resources?view=microsoft-sentinel&amp;preserve-view=true)

## Use the health monitoring workbook

The **Automation health** workbook helps you visualize your health data, as well as the correlation between Microsoft Sentinel *SentinelHealth* logs and Azure Logic Apps *AzureDiagnostics* logs. The **Automation health** workbook includes the following displays:

- Automation rule health and details
- Playbook trigger health and details
- Playbook runs health and details (requires Azure Diagnostic enabled on the Playbook level)
- Automation details per incident

For example:

![Screenshot shows the opening panel of the automation health workbook.](media/monitor-automation-health/automation-health-monitoring-workbook.png)

Select the **Playbooks run by Automation Rules** tab to see playbook activity.

![Screenshot shows a list of the playbooks called by automation rules.](media/monitor-automation-health/automation-health-monitoring-workbook-playbooks.png)

Select a playbook to see the list of its runs in the drill-down chart below.

![Screenshot shows a list of runs of the chosen playbook.](media/monitor-automation-health/automation-health-monitoring-workbook-playbook-run-list.png)

Select a particular run to see the results of the actions in that playbook run.

[![Screenshot shows the actions taken in a given run of the selected playbook.](media/monitor-automation-health/automation-health-monitoring-workbook-playbook-runs.png)](media/monitor-automation-health/automation-health-monitoring-workbook-playbook-runs.png#lightbox)