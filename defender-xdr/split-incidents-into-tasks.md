---
layout: Conceptual
title: Streamline incident response using tasks in the Microsoft Defender portal (Legacy) - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/split-incidents-into-tasks
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Create and manage tasks in the Microsoft Defender portal to investigate and resolve incidents collaboratively.
ms.service: microsoft-defender
ms.author: guywild
author: guywi-ms
ms.date: 2026-06-15T00:00:00.0000000Z
ms.collection:
- M365-security-compliance
- tier1
- usx-security
ms.topic: how-to
ai-usage: ai-assisted
ms.subservice: unified-security-operations
ms.custom: sfi-image-nochange, msecd-doc-authoring-1014
locale: en-us
document_id: d6c13054-8c1f-dce2-e1f8-899a9b3d426a
document_version_independent_id: d6c13054-8c1f-dce2-e1f8-899a9b3d426a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/split-incidents-into-tasks.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: split-incidents-into-tasks
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/split-incidents-into-tasks.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: efe2bdf0-6abc-432f-ed77-71edc67aeaa2
---

# Streamline incident response using tasks in the Microsoft Defender portal (Legacy) - Microsoft Defender XDR | Microsoft Learn

Note

This article describes the legacy incident experience in the Microsoft Defender portal. Incident cases are in preview and are the recommended experience for managing incidents. The legacy incident experience remains available during this preview. For the recommended incident case task experience, see [Manage incident case tasks in the Microsoft Defender portal](manage-incident-case-tasks).

Use tasks in the Microsoft Defender portal to investigate and resolve incidents collaboratively across your operations teams. Breaking incidents into actionable tasks boosts operational efficiency and reinforces accountability throughout the process.

This article explains how tasks work and how to use tasks to manage incidents in the Microsoft Defender portal.

## How tasks work

Break down investigations into clear, actionable steps and assign them across your team.

Using tasks is particularly useful for:

- Onboarding junior analysts
- Working with managed security service providers (MSSPs)
- Tracking work in compliance-oriented organizations

The task panel presents tasks alongside [Security Copilot summaries, guided responses, and reports](security-copilot-in-microsoft-365-defender) to provide a comprehensive view of progress and remaining actions required to close the incident.

Categorize, prioritize, assign, and track each task to ensure consistency, collaboration, and accountability. When you close a task, add Closing notes to document the outcome. These notes support thorough postmortems and help teams learn from each investigation.

## Permissions required

You need one of these roles in the Defender portal to work with tasks.

| Action | Permissions required |
| --- | --- |
| View tasks | **Read-only** or **Security data basics (read)** in the **Security operations** group. |
| Create tasks | **All read and manage permissions** or **Response (manage)** in the **Security operations** group. |

For more information about unified RBAC in the Defender portal, see [Microsoft Defender unified role-based access control (RBAC)](/en-us/defender-xdr/manage-rbac).

## View and manage tasks

To view and manage tasks:

1. From the Defender portal menu, select **Incidents & alerts** &gt; **Incidents** to open the Incident queue.
2. Select an incident from the queue.
3. Select **Tasks** to open the **Tasks** side panel, which lists all of the tasks and Security Copilot insights associated with the incident.

    [![Screenshot showing the Tasks side panel and incident details in Microsoft Defender portal.](media/split-incidents-into-tasks/task-pane-defender-portal.png)](media/split-incidents-into-tasks/task-pane-defender-portal.png#lightbox)
4. To create a new task, select **Add task**.

    [![Screenshot showing the Add task pane in Microsoft Defender portal.](media/split-incidents-into-tasks/add-task-page-defender-portal.png)](media/split-incidents-into-tasks/add-task-page-defender-portal.png#lightbox)

    Fill in the task details and select **Save**.
5. To update a task's status, select a status from the **Status** dropdown on task preview card.

    [![Screenshot showing the Update task status dropdown in Microsoft Defender portal.](media/split-incidents-into-tasks/update-task-status-defender-portal.png)](media/split-incidents-into-tasks/update-task-status-defender-portal.png#lightbox)
6. To edit or delete a task, select the ellipsis (**...**) &gt; **Edit** or **Delete**.

## Automate and synchronize tasks created in Microsoft Sentinel using the Azure portal

When you onboard Microsoft Sentinel to the Defender portal, the Defender portal automatically synchronizes tasks you create in Sentinel using the Azure portal.

Important

Synchronization is one-way - tasks you create in the Defender portal aren't synchronized back to Microsoft Sentinel.

The Defender portal doesn't yet support automatic task creation, but you can continue to use [task automation rules](/en-us/azure/sentinel/create-tasks-automation-rule), [Logic App playbooks](/en-us/azure/sentinel/automation/create-tasks-playbook), or the [Incident Tasks REST API](/en-us/rest/api/securityinsights/incident-tasks) in Azure to create tasks, which are synchronized to the Defender portal.