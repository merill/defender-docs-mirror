---
layout: Conceptual
title: Work with incident tasks in Microsoft Sentinel in the Azure portal | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/work-with-tasks
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
description: Learn how analysts can view, create, and complete incident tasks in the Azure portal to track and manage investigation workflow.
ms.author: guywild
author: guywi-ms
ms.reviewer: idpelleg
ms.topic: how-to
ms.date: 2026-06-15T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1014
ai-usage: ai-assisted
locale: en-us
document_id: 92f0aee9-fbd6-e3aa-6f47-4b118e20bf74
document_version_independent_id: e8ef334a-411e-b8f2-df83-d2093ac99b00
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/work-with-tasks.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/work-with-tasks
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/work-with-tasks.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: c282fa1d-1867-1d9e-c09d-bfa5937d8b59
---

# Work with incident tasks in Microsoft Sentinel in the Azure portal | Microsoft Learn

This article explains how SOC analysts can use incident tasks to manage their incident-handling workflow processes in Microsoft Sentinel in the Azure portal.

[Incident tasks](incident-tasks) are typically created automatically by either automation rules or playbooks set up by senior analysts or SOC managers, but lower-tier analysts can create their own tasks on the spot, manually, right from within the incident.

You can see the list of tasks you need to perform for a particular incident on the incident details page, and mark them complete as you go.

## Use cases for different roles

This article addresses the following scenarios, which apply to SOC analysts:

- View and follow incident tasks
- Manually add an ad-hoc task to an incident

Other articles at the following links address scenarios that apply more to SOC managers, senior analysts, and automation engineers:

- [View automation rules with incident task actions](create-tasks-automation-rule#view-automation-rules-with-incident-task-actions)
- [Add tasks to incidents with automation rules](create-tasks-automation-rule#add-tasks-to-incidents-with-automation-rules)
- [Add tasks to incidents with playbooks](create-tasks-playbook)

## Prerequisites

The **Microsoft Sentinel Responder** role is required to create automation rules and to view and edit incidents, both of which are necessary to add, view, and edit tasks.

## View and follow incident tasks

Perform the following steps to view and follow tasks for an incident:

1. In the **Incidents** page, select an incident from the list, and select **View full details** under **Tasks** in the details panel, or select **View full details** at the bottom of the details panel.

    ![Screenshot of link to enter the tasks panel from the incident info panel on the main incidents screen.](media/work-with-tasks/tasks-from-incident-info-panel.png)
2. If you opted to enter the full details page, select **Tasks** from the top banner.

    [![Screenshot shows incident details screen with tasks panel open.](media/work-with-tasks/incident-details-screen.png)](media/work-with-tasks/incident-details-screen.png#lightbox)
3. The **Incident tasks** panel will open on the right side of whichever screen you were in (the main incidents page or the incident details page). You'll see the list of tasks defined for this incident, along with how or by whom it was created - whether manually or by an automation rule or a playbook.

    ![Screenshot shows incident tasks panel as seen from incident details page.](media/work-with-tasks/incident-tasks-panel.png)
4. The tasks that have descriptions will be marked with an expansion arrow. Expand a task to see its full description.

    ![Screenshot shows incident tasks panel with expanded task descriptions.](media/work-with-tasks/incident-tasks-panel-with-descriptions.png)
5. Mark a task complete by marking the circle next to the task name. A check mark will appear in the circle, and the text of the task will be grayed out. See the "Reset user password" example in the screenshots above.

## Manually add an ad-hoc task to an incident

You can also add tasks for yourself, on the spot, to an incident's task list. This task will apply only to the open incident. This helps if your investigation leads you in new directions and you think of new things you need to check. Adding these as tasks ensures that you won't forget to do them, and that there will be a record of what you did, that other analysts and managers can benefit from.

1. Select **+ Add task** from the top of the **Incident tasks** panel.

    ![Screenshot shows how to manually add a task to your task list.](media/work-with-tasks/add-task-ad-hoc-1.png)
2. Enter a **Title** for your task, and a **Description** if you choose.

    ![Screenshot shows how to add a title and description to your task.](media/work-with-tasks/add-task-ad-hoc-2.png)
3. Select **Save** when you've finished.

    ![Screenshot shows how to finish defining and save your task.](media/work-with-tasks/add-task-ad-hoc-3.png)
4. See your new task at the bottom of the task list. Note that manually created tasks have a different color band on the left border, and that your name appears as *Created by:* under the task title and description.

    ![Screenshot showing your new task at the end of the task list.](media/work-with-tasks/view-ad-hoc-added-task.png)