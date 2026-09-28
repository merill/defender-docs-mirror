---
layout: Conceptual
title: Manage generic cases in the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/manage-cases
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to create, assign, update, review, and manage generic cases in the Microsoft Defender portal.
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
document_id: 57274645-51ca-5687-7afa-90c2602fd9de
document_version_independent_id: 57274645-51ca-5687-7afa-90c2602fd9de
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/manage-cases.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: manage-cases
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/manage-cases.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 14c5d0c3-cb72-eb5e-fb12-d3869b19a215
---

# Manage generic cases in the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn

Generic cases help analysts track and manage security operations work that isn't tied to a single incident. Use generic cases to track ownership, priority, status, tasks, comments, activity history, attachments, linked objects, custom fields, due dates, and due times.

For an overview of Case Management, see [Case management in the Microsoft Defender portal](siem-defender-case-management).

## Prerequisites

Before you begin, make sure that you have one of the following Microsoft Defender unified RBAC permissions:

- To view generic cases: **Security data basics (read)** in the **Security operations** group.
- To create and manage generic cases: **Alerts (manage)** in the **Security operations** group.

For more information, see [Microsoft Defender unified role-based access control (RBAC)](/en-us/defender-xdr/manage-rbac).

## Create a generic case

Create a generic case to track security operations work that isn't managed as an incident case or exposure case.

To create a generic case:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Generic**.
4. Select **Create**.
5. Enter the required case details.

    ![Screenshot showing the Generic cases page and the Create case pane in the Microsoft Defender portal.](media/manage-cases/manage-cases-create-case.png)
6. Select **Save**.

Available fields can vary by tenant configuration and preview scope.

## Access the Manage case pane

Most generic case management tasks are available from the **Manage case** pane.

To access the **Manage case** pane:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Generic**.
4. Select a generic case.
5. Select **Manage case**.
6. Update the fields you need.

    ![Screenshot showing a generic case and the Manage case pane in the Microsoft Defender portal.](media/manage-cases/manage-cases-manage-case-pane.png)
7. Select **Save**.

Available fields can vary by tenant configuration and preview scope.

## Rename a generic case

Use the case name to help analysts understand the purpose of the case.

To rename a generic case:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Generic**.
4. Select the relevant generic case.
5. Select **Manage case**.
6. In **Case name**, enter the updated name.
7. Select **Save**.

## Assign a generic case to an owner

Assign a generic case to an owner to track responsibility and support handoff between analysts or teams.

To assign an owner:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Generic**.
4. Select the relevant generic case.
5. Select **Manage case**.
6. In **Assigned to** field, select the user or group you want to assign the generic case to.
7. To remove an existing assignment, clear the current value.
8. Select **Save**.

## Change generic case priority

Priority helps teams decide which generic cases require the most immediate attention.

To change priority:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Generic**.
4. Select the relevant generic case.
5. Select **Manage case**.
6. In **Priority**, select the priority value.
7. Select **Save**.

## Change generic case status

Use status to track where the generic case is in the response lifecycle.

To change status:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Generic**.
4. Select the relevant generic case.
5. Select **Manage case**.
6. In **Status**, select the status value.
7. Select **Save**.

## Add or update custom fields

Custom fields are configured by admins in case templates. Use custom fields to capture organization-specific information required by your security operations process.

To update custom fields:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Generic**.
4. Select the relevant generic case.
5. Select **Manage case**.
6. Update the custom fields that apply to your workflow.
7. Select **Save**.

For more information about configuring custom fields, see [Configure case templates in the Microsoft Defender portal](manage-case-templates).

## Set or update the due date and due time

Use the due date and due time to track response expectations for the generic case.

To update the due date and due time:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Generic**.
4. Select the relevant generic case.
5. Select **Manage case**.
6. In **Due date**, select the required date.
7. In **Due time**, select the required time.
8. Select **Save**.

If your organization uses SLA policies, the due date and due time might be affected by the SLA policy configured for generic cases.

For more information, see [Configure case templates in the Microsoft Defender portal](manage-case-templates).

## Add or update tags

Use tags to add context to a generic case and help analysts filter, group, or identify related work.

To add or update tags:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Generic**.
4. Select the relevant generic case.
5. Select **Manage case**.
6. In **Tags**, add or remove tags as needed.
7. Select **Save**.

## Send email notifications

Use email notifications to notify users or groups about updates to a generic case.

To send an email notification:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Generic**.
4. Select the relevant generic case.
5. Select **Manage case**.
6. In **Send email notification**, enter or select the users or groups you want to notify.
7. Update the fields you need.
8. Select **Save**.

## Add attachments

Use attachments to keep reports and other relevant files in one place.

To add an attachment:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Generic**.
4. Select the relevant generic case.
5. Select **Attachments**.
6. Select **Upload**.
7. Select the file you want to upload.

Uploaded files are added to the generic case attachments list. From the **Attachments** tab, you can also download or remove an attachment. For files added with a comment, you can use **Locate last comment** to find the associated comment.

## Link objects to a generic case

Use linked objects to connect related security information to a generic case.

Generic cases can include linked objects such as:

- Incidents
- Indicators
- Recommendations

To link an object:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Generic**.
4. Select the relevant generic case.
5. Select **Linked objects**.
6. Select **Incidents**.

    ![Screenshot showing the Linked objects tab with linked incidents for a generic case in the Microsoft Defender portal.](media/manage-cases/manage-cases-linked-incidents.png)
7. Select **Link incidents**.
8. Select the objects you want to link.
9. Select **Save**.

### Link indicators (preview)

Important

Projects in Microsoft Defender Threat Intelligence are deprecated. To organize and investigate threat indicators, link indicators to a case in the Microsoft Defender portal.

Link relevant indicators of compromise (IoCs) to a generic case to provide additional context for an investigation.

To link indicators from a generic case:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Generic**.
4. Select the relevant generic case.
5. Select **Linked objects**.
6. Select **Indicators**.

    ![Screenshot showing the Linked objects tab with linked indicators for a generic case in the Microsoft Defender portal.](media/manage-cases/manage-cases-linked-indicators.png)
7. Select **Add**.
8. Select the workspace that contains the indicator.
9. Select the indicator you want to link.
10. Select **Link**.

You can also link an indicator from its details page in Intel management. Select the indicator, and then select **Link cases**.

## Unlink objects from a generic case

Unlink objects when they no longer apply to the generic case.

To unlink an object:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Generic**.
4. Select the relevant generic case.
5. Select **Linked objects**.
6. Select the object type.
7. Select the object you want to unlink.
8. Select **Unlink**.

## Add comments

Use comments to document investigation progress, decisions, handoffs, and resolution details. You can also attach relevant files when you add a comment.

To add a comment:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Generic**.
4. Select the relevant generic case.
5. On the **Summary** tab, enter your comment in the comments area.
6. Use the formatting options as needed.
7. To attach a file to the comment, select the attachment icon, and then select the file.
8. Select **Send**.

The comment is added to the case activity. Files attached to a comment are also available from the **Attachments** tab.

## Review activity history

Activity history shows changes and actions performed on the generic case.

Use activity history to review:

- Case creation
- Assignment changes
- Status changes
- Priority changes
- Due date changes
- Task updates
- Comments
- Automation updates
- Other workflow changes

To review activity history:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Generic**.
4. Select the relevant generic case.
5. Go to **Summary**.

    ![Screenshot showing the Summary page for a generic case in the Microsoft Defender portal.](media/manage-cases/manage-cases-summary.png)
6. Review the activity feed.
7. Filter the feed as needed.
8. Select an activity item to review more details.

## Filter generic cases

Use filters to find generic cases by case details, ownership, dates, tags, or custom fields.

To filter generic cases:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Select **Cases**.
3. Select **Generic**.
4. Select **Add filter**.
5. Choose the filter you want to apply.
6. Select the filter value.

Generic case filters can vary based on tenant configuration, case templates, and custom fields.

## Manage generic case tasks

Use tasks to break generic case work into smaller action items, assign ownership, track progress, and document outcomes.

For step-by-step guidance, see [Manage generic case tasks in the Microsoft Defender portal](manage-generic-case-tasks).