---
layout: Conceptual
title: Manage incident cases in the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/manage-incident-cases
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to assign, update, resolve, and review incident cases in the Microsoft Defender portal.
ms.service: microsoft-defender
ms.subservice: unified-security-operations
author: guywi-ms
ms.author: guywild
ms.date: 2026-08-19T00:00:00.0000000Z
ms.collection:
- M365-security-compliance
- tier1
- usx-security
ms.topic: how-to
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: 078cecfd-6e2e-350a-83de-8c0af96ef2e4
document_version_independent_id: 078cecfd-6e2e-350a-83de-8c0af96ef2e4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/manage-incident-cases.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: manage-incident-cases
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/manage-incident-cases.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 7d2adba6-3ae0-423e-3568-482c6a49ef69
---

# Manage incident cases in the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn

Use incident cases to track incident ownership, severity, status, classification, tasks, comments, activity history, custom fields, and resolution details.

![Screenshot showing the Manage case pane for an incident case in the Microsoft Defender portal.](media/manage-incident-cases/manage-incident-case-settings.png)

Note

Incident cases are in preview and are the recommended experience for managing incidents in the Microsoft Defender portal. The legacy incident experience remains available during this preview.

For an overview of Case Management, see [Case management in the Microsoft Defender portal](siem-defender-case-management).

## Prerequisites

Before you begin, make sure you have one of the following Microsoft Defender unified RBAC permissions:

- To view incident cases: **Security Data Read**.
- To view and manage incident cases: **Security Data Manage**.

Incident case permissions and scoping follow the same permissions model as the legacy incident experience.

For more information, see [Microsoft Defender unified role-based access control (RBAC)](/en-us/defender-xdr/manage-rbac).

## Access the Manage case pane

Most incident case management tasks are available from the **Manage case** pane.

To access the **Manage case** pane:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Incident**.
4. Select the relevant incident case.
5. Select the three-dot menu.
6. Select **Manage case**.

![Screenshot showing an incident case page in the Microsoft Defender portal with the Manage menu open.](media/manage-incident-cases/manage-incident-case-overview.png)

1. Update the fields you need.
2. Select **Save**.

Available fields can vary by tenant configuration and preview scope.

## Assign an incident case to an owner

Assign an incident case to an owner to track responsibility and support handoff between analysts or teams.

To assign an owner:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Incident**.
4. Select the relevant incident case.
5. Select **Manage case**.
6. In **Assigned to** field, select the user or group you want to assign the incident case to.
7. To remove an existing assignment, clear the current value.
8. Select **Save**.

Assigning ownership of an incident case also applies ownership to the related incident workflow.

## Change incident case severity

Severity helps analysts understand the impact of the incident case and prioritize response.

To change severity:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Incident**.
4. Select the relevant incident case.
5. Select **Manage case**.
6. In **Severity**, select the severity value.
7. Select **Save**.

## Change incident case status

Use status to track where the incident case is in the response lifecycle.

To change status:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Incident**.
4. Select the relevant incident case.
5. Select **Manage case**.
6. In **Status**, select the status value.
7. Select **Save**.

## Add or update custom fields

Custom fields are configured by admins in case templates. Use custom fields to capture organization-specific information required by your security operations process.

To update custom fields:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Incident**.
4. Select the relevant incident case.
5. Select **Manage case**.
6. Update the custom fields that apply to your workflow.
7. Select **Save**.

For more information about configuring custom fields, see [Configure case templates in the Microsoft Defender portal](manage-case-templates).

## Set or update the due date and time

Use the due date and time to track response expectations for the incident case.

To update the due date and time:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Incident**.
4. Select the relevant incident case.
5. Select **Manage case**.
6. In **Due date**, select the required date.
7. In **Due time**, select the required time.
8. Select **Save**.

If your organization uses SLA policies, the due date and time might be affected by the SLA policy configured for incident cases.

For more information, see [Configure case templates in the Microsoft Defender portal](manage-case-templates).

## Add or update tags

Use tags to add context to an incident case and help analysts filter, group, or identify related work.

Incident cases support both system tags and custom tags. Analysts can create custom tags from the incident case UI.

When tags are added, removed, or updated on an incident case, the tag changes are synced to the related incident.

To add or update tags:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Incident**.
4. Select the relevant incident case.
5. Select **Manage case**.
6. In **Tags**, add or remove tags as needed.
7. Select **Save**.

## Resolve or close an incident case

Resolve or close an incident case when investigation and response work is complete.

To resolve or close an incident case:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Incident**.
4. Select the relevant incident case.
5. Select **Manage case**.
6. Change the status to the resolved or closed status used by your organization.
7. If needed, update the **Classification** field.
8. Add resolution notes or closing notes to document the outcome.
9. Select **Save**.

When you resolve or close an incident case, the status change is synced to the related incident. Related alerts keep their own status and aren't automatically resolved when the incident case is resolved or closed.

Classification, determination, and closing notes are stored on both the incident case and the related incident.

## Specify classification or determination

Use classification and determination to document the outcome of the investigation.

To specify classification or determination:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Incident**.
4. Select the relevant incident case.
5. Select **Manage case**.
6. In **Classification**, select the appropriate classification.
7. If a determination field is available, select the appropriate determination.
8. Select **Save**.

Classifying incident cases helps your team document investigation outcomes and improve future detection and response processes.

## Add comments and attachments

Use comments to document investigation progress, decisions, handoffs, and resolution details. You can also attach relevant files when you add a comment.

To add a comment:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Incident**.
4. Select the relevant incident case.
5. Select **Comments & Attachments**.
6. On the **Comments** tab, enter your comment.
7. Use the formatting options as needed.
8. To attach a file, select the attachment icon, and then select the file.
9. Select **Send**.

The comment is added to the incident case activity history. Any files you attach are also available from the **Attachments** tab.

If a file with the same name already exists in the case, select **Rename** to add it as a separate file, or **Link existing** to use the file that's already attached.

### Add an attachment without a comment

To add a file without adding a comment:

1. Select **Comments & Attachments**.
2. Select the **Attachments** tab.
3. Select **Upload**.
4. Select the file that you want to attach.

The file is added to the incident case attachments list. From the **Attachments** tab, you can also view attachment details, download files, or remove attachments.

## Manage incident case tasks

Use tasks to break incident response work into smaller action items, assign ownership, track progress, and document outcomes.

For step-by-step guidance, see [Manage incident case tasks in the Microsoft Defender portal](manage-incident-case-tasks).

## Work with agentic sessions in an incident case

You can run supported agentic playbooks from an incident case. Running an agentic playbook creates an agent session that's associated with the case, so you can track agent progress and review session outputs from the case experience.

Agentic sessions are supported only for customers with access to Project Perception. For more information, see [What is Project Perception?](/en-us/security/agentic-security/agentic-security-overview).

### Start an agentic session

To start an agentic session from an incident case:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Incident**.
4. Select the relevant incident case.
5. Select the three-dot menu.
6. Under **Actions**, select **Run agentic playbook**.
7. Select the agentic playbook you want to run.
8. Review the required inputs.
9. Select **Start session**.

The agent session is associated with the incident case and its status is available from the case experience.

### Track agent session status

To track agent sessions associated with incident cases:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Incident**.
4. Add the **Agent sessions status** column to the cases list, if it isn't already displayed.
5. Review **Agent sessions status** for the relevant incident case.

You can also use **Agent sessions status** as a filter to find incident cases based on their associated agent sessions.

To view the session status from an incident case:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Incident**.
4. Select the relevant incident case.
5. Review the agent session status in the case side pane.
6. Select **View session** to open the associated agent session.

### Review an agent session from an incident case

Agent sessions associated with an incident case are available from the case experience. You can select a session to review outputs generated by the agents, such as investigation notes, summaries, and reports.

To review an agent session:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Incident**.
4. Select the relevant incident case.
5. Select the relevant agent session.
6. Review the session outputs.
7. Select **Open session**.

The agent session opens as an overlay over the case experience. From the session, you can review the session summary, agent activity, inputs, outputs, session details, and conversation.

## Investigate an incident case

Incident cases include incident investigation context such as attack story, alerts, assets, investigations, evidence, activities, and response actions.

For detailed investigation guidance, see [Investigate incident cases in the Microsoft Defender portal](investigate-incident-cases).

## Merge incident cases

Incident cases can be merged when multiple incident cases represent the same attack, investigation, or related activity and should be handled together.

For more information, see [Merge and split incident cases in the Microsoft Defender portal](manage-incident-case-merging).

For step-by-step guidance, see [Merge incident cases manually in the Microsoft Defender portal](merge-incident-cases-manually).

## Incident case notifications

Existing incident email notification rules apply to incident cases. Notifications can be triggered by incident case updates such as assignment, status change, severity change, and resolution.