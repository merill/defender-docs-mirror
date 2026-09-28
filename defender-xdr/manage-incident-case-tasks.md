---
layout: Conceptual
title: Manage incident case tasks in the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/manage-incident-case-tasks
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to create and manage tasks for incident cases in the Microsoft Defender portal.
ms.service: microsoft-defender
ms.subservice: unified-security-operations
author: guywi-ms
ms.author: guywild
ms.date: 2026-07-15T00:00:00.0000000Z
ms.collection:
- M365-security-compliance
- tier1
- usx-security
ms.topic: how-to
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: 0171450e-19f7-9def-642e-5dd64c241009
document_version_independent_id: 0171450e-19f7-9def-642e-5dd64c241009
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/manage-incident-case-tasks.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: manage-incident-case-tasks
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/manage-incident-case-tasks.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: d6f29a13-391e-8984-e123-49cbdb3a70b3
---

# Manage incident case tasks in the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn

Use tasks in the Microsoft Defender portal to break incident response work into actionable items, assign ownership, track progress, and document outcomes.

Incident case tasks help security operations teams coordinate investigation, response, remediation, handoff, and review work for incident cases.

Note

Incident cases are in preview and are the recommended experience for managing incidents in the Microsoft Defender portal. The legacy incident experience remains available during this preview.

For an overview of case management, see [Case management in the Microsoft Defender portal](siem-defender-case-management).

## How incident case tasks work

Tasks help analysts organize incident response work into smaller steps. Each task can include details such as status, priority, assigned user, due date, description, and closing notes.

Using tasks is useful for:

- Assigning investigation or response actions to specific analysts
- Tracking work across shifts or teams
- Coordinating handoff between analysts
- Onboarding junior analysts
- Working with managed security service providers
- Documenting investigation outcomes
- Supporting post-incident review and audit requirements

When you close a task, add closing notes to document what was done and what the outcome was.

## Prerequisites

Before you begin, make sure you have one of the following Microsoft Defender unified RBAC permissions:

- To view incident case tasks: **Read-only** or **Security data basics (read)** in the **Security operations** group.
- To create and manage incident case tasks: **All read and manage permissions** or **Response (manage)** in the **Security operations** group.

For more information, see [Microsoft Defender unified role-based access control (RBAC)](/en-us/defender-xdr/manage-rbac).

## View incident case tasks

To view tasks for an incident case:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Incident**.
4. Select the relevant incident case.
5. Go to **Tasks**.

From **Tasks**, you can view task status, add tasks, edit existing tasks, or delete tasks.

## Create an incident case task

To create a task for an incident case:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Incident**.
4. Select the relevant incident case.
5. Go to **Tasks**.
6. Select **Add task**.
7. Enter a name for your task.

    ![Screenshot showing the Add task pane for an incident case in the Microsoft Defender portal.](media/manage-incident-case-tasks/create-incident-case-task.png)
8. Select a task status.
9. Select a task priority.
10. Assign the task to a user, if needed.
11. Select a due date and due time, if needed.
12. Add a description for the task.
13. If you're closing the task, add closing notes to document the outcome.
14. Select **Save**.

## Update an incident case task

To update an incident case task:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Incident**.
4. Select the relevant incident case.
5. Go to **Tasks**.
6. Select the edit icon for the task you want to update.
7. Update the task details.
8. Select **Save**.

## Change task status

To change the status of an incident case task:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Incident**.
4. Select the relevant incident case.
5. Go to **Tasks**.
6. Select the task status.
7. Select the new status.

The task status is updated in **Tasks**.

## Close an incident case task

To close an incident case task:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Incident**.
4. Select the relevant incident case.
5. Go to **Tasks**.
6. Select the edit icon for the task you want to close.
7. Change the task status to **Closed**.
8. Add closing notes to document the outcome.
9. Select **Save**.

## Delete an incident case task

Delete a task only when you're sure it isn't needed.

To delete an incident case task:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Incident**.
4. Select the relevant incident case.
5. Go to **Tasks**.
6. Select the delete icon for the task you want to delete.
7. Select **Yes** to confirm.