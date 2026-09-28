---
layout: Conceptual
title: Use Tasks to Manage Incidents in Microsoft Sentinel in the Azure Portal | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/incident-tasks
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
description: This article describes incident tasks and how to work with them to ensure all required steps are taken in triaging, investigating, and responding to incidents in Microsoft Sentinel.
ms.author: guywild
author: guywi-ms
ms.reviewer: idpelleg
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 8691cf39-cc0a-71f6-04ca-2cfbf707957a
document_version_independent_id: f65412d4-8f87-772f-2f67-faa0a2d1bee5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/incident-tasks.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/incident-tasks
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/incident-tasks.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 57ebe29a-08a1-a88d-32ff-df67c0d964ef
---

# Use Tasks to Manage Incidents in Microsoft Sentinel in the Azure Portal | Microsoft Learn

This article explains how to use incident tasks in Microsoft Sentinel to standardize and track the steps your team follows when triaging, investigating, and responding to incidents. You can add tasks manually, or automate task creation by using automation rules and playbooks.

One of the most important factors in running your security operations (SecOps) effectively and efficiently is the **standardization of processes**. SecOps analysts are expected to perform a list of steps, or tasks, in the process of triaging, investigating, or remediating an incident. Standardizing and formalizing the list of tasks can help keep your SOC running smoothly, ensuring the same requirements apply to all analysts. With this standardized process, regardless of who is on-shift, an incident will always get the same treatment and SLAs. Analysts won't need to spend time thinking about what to do, or worry about missing a critical step. Those steps are defined by the SOC manager or senior analysts (tier 2/3) based on common security knowledge (such as NIST), their experience with past incidents, or recommendations provided by the security vendor that detected the incident.

## When to use incident tasks

Incident tasks are useful in the following scenarios:

- Your SOC analysts can use a single central checklist to handle the processes of incident triage, investigation, and response, all without worrying about missing a critical step.
- Your SOC engineers or senior analysts can document, update, and align the standards of incident response across the analysts' teams and shifts. They can also create checklists of tasks to train new analysts or analysts encountering new types of incidents.
- As a SOC manager or as an MSSP, you can make sure incidents are handled in accordance with the relevant SLAs/SOPs.

## Prerequisites

The **Microsoft Sentinel Responder** role is required to create automation rules and to view and edit incidents, both of which are necessary to add, view, and edit tasks.

The **Logic Apps Contributor** role is required to create and edit playbooks.

## Incident task management scenarios

Incident task management scenarios vary depending on whether you are an analyst or a workflow creator.

### Analyst scenarios

The following scenarios show how analysts can use incident tasks during investigations.

#### Follow tasks when handling an incident

When you select an incident and **View full details**, on the incident details page you'll see on the right-hand panel all the tasks that have been added to that incident, whether manually or by automation rules.

Expand a task to see its full description, including the user, automation rule, or playbook that created it.

Mark a task complete by selecting its "checkbox" circle.

[![Screenshot of incident tasks panel for analysts on incident details screen.](media/incident-tasks/incident-details-screen.png)](media/incident-tasks/incident-details-screen.png#lightbox)

#### Add tasks to an incident on the spot

You can add tasks to an open incident that you're working on, either to give yourself reminders of actions you've discovered a need to take, or to record actions that you've taken of your own initiative that don't appear in the task list. Tasks added manually to an incident apply only to that incident.

### Workflow creator scenarios

The following scenarios describe how workflow creators can add and manage tasks automatically.

#### Add tasks to incidents with automation rules

Use the **Add task** action in automation rules to automatically furnish all incidents with a checklist of tasks for your analysts. Set the **Analytics rule name** condition in your automation rule to determine the scope:

- Apply the automation rule to *all analytics rules* in order to define a standard set of tasks to be applied to all incidents.
- By applying your automation rule to *a limited set of analytics rules*, you can assign specific tasks to particular incidents, according to the threats detected by the analytics rule or rules that generated those incidents.

Consider that the order in which tasks appear in your incident is determined by the tasks' creation time. You can set the order of automation rules so that rules that add tasks required for all incidents will run first, and only afterwards any rules that add tasks required for incidents generated by specific analytics rules. Within a single rule, the order in which the actions are defined governs the order in which they appear in an incident.

See which incidents are covered by existing automation rules and tasks, before you create a new automation rule. Use the **Action** filter on the **Automation rules** list to see only those rules that add tasks to incidents, and see which analytics rules those automation rules apply to, to understand which incidents those tasks will be added to.

#### Add tasks to incidents with playbooks

Use the **Add task** action in a playbook (in the Microsoft Sentinel connector) to automatically add a task to the incident that triggered the playbook.

Then, use other playbook actions—in their respective Logic Apps connectors—to complete the contents of the task.

Finally, use the **Mark task as completed** action (again in the Microsoft Sentinel connector) to automatically mark the task complete.

Consider the following scenarios as examples:

- **Let playbooks add and complete tasks:** When an incident is created, it triggers a playbook that does the following:

    1. Adds a task to the incident to reset a user's password.
    2. Performs the task by issuing an API call to the user provisioning system to reset the user's password.
    3. Awaits a response from the system as to the success or failure of the reset.
        - If the password reset succeeded, the playbook then marks the task it just created in the incident as completed.
        - If the password reset failed, the playbook will not mark the task as completed, leaving it to an analyst to perform.
- **Let playbook evaluate if conditional tasks should be added:** When an incident is created, it triggers a playbook that requests an IP address report from an external threat intelligence source.

    - If the IP address is malicious, the playbook adds a certain task (say, "Block this IP address").
    - Otherwise, the playbook takes no further action.

#### Use automation rules or playbooks to add tasks?

What considerations should dictate whether automation rules or playbooks should be used to create incident tasks?

- **Automation rules**: Use whenever possible. Use for plain, static tasks that don't require interactivity.
- **Playbooks**: Use for advanced use cases like creating tasks based on conditions or creating tasks with integrated automated actions.