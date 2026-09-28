---
layout: Conceptual
title: Manage incidents in the Microsoft Defender portal (legacy) - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/manage-incidents
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
ms.reviewer: yotam segev
description: Discover how to assign, tag, and resolve incidents in Microsoft Defender. Improve your security operations with actionable insights and streamlined processes.
ms.service: defender-xdr
f1.keywords:
- NOCSH
ms.author: monaberdugo
author: mberdugo
ms.collection:
- m365-security
- usx-security
- tier1
ms.custom:
- msecd-doc-authoring-1014
- admindeeplinkDEFENDER
- sfi-image-nochange
ms.topic: how-to
search.appverid:
- MOE150
- MET150
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 5fd984c5-ea3f-a3e2-8122-695a2c95ede3
document_version_independent_id: 5fd984c5-ea3f-a3e2-8122-695a2c95ede3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/manage-incidents.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: manage-incidents
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/manage-incidents.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 4ea4b224-2d66-6f92-6d87-20274acf9f90
---

# Manage incidents in the Microsoft Defender portal (legacy) - Microsoft Defender XDR | Microsoft Learn

Incident management is critical to ensuring that incidents are named, assigned, and tagged to optimize time in your incident workflow and more quickly contain and address threats. To perform these tasks, you need access to the [Microsoft Defender portal](https://security.microsoft.com) with an appropriate role assigned through [Microsoft Defender XDR role-based access control (RBAC)](manage-rbac).

To manage your incidents in the [Microsoft Defender portal](https://security.microsoft.com), use the quick launch and go to **Investigation & response &gt; Incidents & alerts &gt; Incidents**.

[![Screenshot showing the incident queue and quick launch pane in the Microsoft Defender portal.](media/manage-incidents/incidents-queue.png)](media/manage-incidents/incidents-queue.png#lightbox)

This section explains how to perform incident management tasks in Microsoft Defender across the incident lifecycle.

Note

This article describes the legacy incident experience in the Microsoft Defender portal. Incident cases are in preview and are the recommended experience for managing incidents. The legacy incident experience remains available during this preview. For the recommended incident case experience, see [Manage incident cases in the Microsoft Defender portal](manage-incident-cases).

To open an incident or alert on demand for an investigation or operational workflow, see [Manually create an incident or alert in Microsoft Defender](manually-create-incident).

**Incident triage:**

- Assign the incident to an owner
- Assign or change severity
- Add incident tags
- Change the incident status

**Incident investigation and resolution:**

- Resolve an incident
- Specify an incident's classification
- Add comments to an incident

**Incident logging and reporting:**

- Edit the incident name.
- Assess the activity audit and add comments in the Activity log.
- Generate a summary of the incident investigation and analysis.
- Export incident data to PDF.

Tip

**Defender Boxed**, a series of cards showcasing your organization's security successes, improvements, and response actions in the past six months/year, appears for a limited time during January and July of each year. Learn how you can share your [Defender Boxed](incident-queue#defender-boxed) highlights.

## Access the *Manage incident* pane

Most of these tasks are accessible from the **Manage incident** pane for an incident. You can reach this pane from any of several locations.

Select **Incidents & alerts &gt; Incidents** on the quick launch of the Microsoft Defender portal.

# [From the incident queue](#tab/queue)
To access the **Manage incident** pane from the incident queue, select the check box of an incident, and select **Manage incidents** from the toolbar above the filters. Manage many incidents at once by selecting multiple check boxes.

Alternatively, you can select the row of an incident (without selecting the incident name), so that the incident details pane appears, and select **Manage incident** from the incident details pane.

[![Screenshot showing how to manage incidents from the incidents queue in the Microsoft Defender portal.](media/manage-incidents/manage-incidents-from-queue.png)](media/manage-incidents/select-manage-incident.png#lightbox)

# [From the incident page](#tab/incident-page)
To access the **Manage incident** pane from the incident page, follow these steps:

1. Select the name of an incident from the queue. Or, select the row of an incident in the queue and then select **Open incident page** from the incident details pane.
2. From the incident page, select **Manage incident** from the top panel.

    If **Manage incident** isn't visible, select the three dots in the upper right corner, and select it from the menu that appears.

    [![Screenshot showing how to manage an incident from the incident page in the Microsoft Defender portal.](media/manage-incidents/select-manage-incident.png)](media/manage-incidents/select-manage-incident.png#lightbox)

---

## Incident triage

The following management tasks are closely associated with incident triage, though they can be performed at any time.

- Assign the incident to an owner
- Assign or change severity
- Add incident tags
- Change the incident status

### Assign an incident to an owner

By default, new incidents are created with no owner. Ideally, your SecOps team should have mechanisms and procedures in place to automatically assign incidents to owners. You might need to reassign an incident in the case of escalation or mistaken original assignment.

#### Assign an owner from the incident pane

To manually assign a new owner to an incident, take the following steps:

1. Follow the instructions in the opening section to Access the *Manage incident* pane.
2. Select the **Assign to** box. A drop-down list of suggested assignees appears.
3. If you see the user or group account you want to assign the incident to, select it.

    Otherwise, begin typing the name or account ID of the desired user or group in the text box at the top of the list. The list is dynamically updated, filtered by what you type. When you see the user or group you want, select it.
4. To remove an existing assignment, including any you just added, select the **X** next to the account name. Then, select the **Assign to** box if you want to add another assignment.

    Only one user or group account can be assigned to an incident.
5. Select **Save**.

Assigning ownership of an incident assigns the same ownership to all the alerts associated with the incident.

![Screenshot showing how to assign an owner in the Manage incident pane in the Microsoft Defender portal.](media/manage-incidents/assign-incident.png)

#### View incidents assigned to a particular owner

To see the list of incidents assigned to a particular user or group, filter the incident queue:

1. From the incident queue, select the **Incident assignment** filter. A drop-down list of suggested assignees appears.

    If you don't see **Incident assignment** among the filters, select **Add filter**, select **Incident assignment** from the drop-down list, and select **Add**.
2. If you see the user account whose assigned incidents you want to display, select it.

    Otherwise, begin typing the name or account ID of the desired user or group in the text box at the top of the list. The list is dynamically updated, filtered by what you type. When you see the user or group you want, select it.

    Unlike assigning incidents, here you can select more than one assignee to filter the list by. To add another user or group account to the filter, select the text box (next to the existing account in the filter), and the list of suggested assignees appears again.
3. Select **Apply**.

    ![Screenshot showing how to view incidents assigned to an owner in the incident queue page in the Microsoft Defender portal.](media/manage-incidents/assignment-filter.png)

To save a link to the incident queue with the current filters applied, select **Copy list link** from the toolbar on the incident queue page. Create a shortcut in your favorites or on your desktop and paste the link into it.

### Assign or change incident severity

The severity of an incident is set to the highest severity of the alerts associated with the incident. The severity of an incident can be set to *high*, *medium*, *low*, or *informational*.

To manually assign or change the severity of an incident, take the following steps:

1. Follow the instructions in the opening section to Access the *Manage incident* pane.
2. Select the severity value you want to apply from the **Severity** drop-down on the **Manage incident** pane.
3. Select **Save**.

### Add incident tags

Custom tags add information to lend context to an incident. For example, a tag can label a group of incidents with a common characteristic. Tags are a criteria for filtering, so you can later filter the incident queue for all incidents that contain a specific tag. To apply a tag to an incident:

1. Follow the instructions in the opening section to Access the *Manage incident* pane.
2. In the **Incident tags** field, begin typing the name of the tag you want to apply. As you type, a list of previously used and selected tags appears. If you see the tag you want to apply in the list, select it.

    ![Screenshot showing how to create an incident tag in the Manage incidents pane.](media/manage-incidents/create-incident-tag.png)

    If you type a tag name that was never used before, select the last entry in the list, which is the text you typed followed by "(Create new)."

    ![Screenshot showing how to select a tag to apply to an incident in the Manage incidents pane.](media/manage-incidents/select-tag.png)

    The tag then appears as a label inside the Incident tags field. Repeat this step to add more tags as you like.

    ![Screenshot showing how a selected tag appears in the Incident tags field.](media/manage-incidents/selected-tag.png)
3. Select **Save**.

An incident can have system tags and/or custom tags with certain color backgrounds. Custom tags use the white background while system tags typically use red or black background colors. System tags identify the following information:

- A **type of attack**, like credential phishing or BEC fraud
- **Automatic actions**, like automatic investigation and response and automatic attack disruption
- **Defender Experts** handling an incident
- **Critical assets** involved in the incident

Tip

Microsoft's Security Exposure Management, based on predefined classifications, automatically tags devices, identities, and cloud resources as a **critical asset**. This out-of-the-box capability ensures the protection of an organization's valuable and most important assets. It also helps security operations teams to prioritize investigation and remediation. Know more about [critical asset management](/en-us/security-exposure-management/critical-asset-management).

### Change the incident status

Incidents begin life with a status of **Active**. When you're working on an incident, change the **Status** to **In progress**.

## Incident investigation and resolution

The following management tasks are closely associated with incident investigation and resolution, though they can be performed at any time.

- Resolve an incident
- Specify an incident's classification
- Add comments to an incident

### Resolve an incident

When an incident is remediated and resolved, take the following actions to record the resolution:

1. Follow the instructions in the opening section to Access the *Manage incident* pane.
2. Change the status. Select **Resolved** from the **Status** drop-down list. When you change an incident's status to **Resolved**, a new field is displayed immediately following the **Status** field.
3. Enter a note in this field that explains why you consider the incident resolved. This note is visible in the activity log of the incident, near the entry recording the incident's resolution.

    ![Screenshot of incident management panel with incident resolution note.](media/manage-incidents/resolve-incidents.png)

    The resolution note is also visible in the *Incident details* panel on both the incidents queue page and the incident page of a resolved incident.

    [![Screenshot of appearance of resolution note in the incident details panel.](media/manage-incidents/resolution-note-in-side-panel.png)](media/manage-incidents/resolution-note-in-side-panel.png#lightbox)
4. Select **Save**.

Resolving an incident also resolves all the linked and active alerts related to the incident. An incident that isn't resolved displays as **Active**.

### Specify the incident's classification

When you resolve an incident, or at any point in an incident's investigation, as soon as you become aware of how the incident should be classified, set the **Classification** field accordingly.

1. Follow the instructions in the opening section to Access the *Manage incident* pane.
2. Choose the appropriate value from the **Classification** drop-down list:

    - **Not set** (the default).
    - **True positive** with a type of threat. Use this classification for incidents that accurately indicate a real threat. Specifying the threat type helps your security team see threat patterns and act to defend your organization from them.
    - **Informational, expected activity** with a type of activity. Use the options in the **Informational, expected activity** category to classify incidents for security tests, red team activity, and expected unusual behavior from trusted apps and users.
    - **False positive** for types of incidents that you determine can be ignored because they're technically inaccurate or misleading.

    The **Classification** drop-down list shows the available activity and threat types for each classification.
3. Select **Save**.

    ![Screenshot showing the classification options for incidents.](media/manage-incidents/incident-classification.png)

Classifying incidents and specifying their status and type helps tune Microsoft Defender to provide better detection determination over time.

### Add comments to an incident

Over the course of investigating and incident, add comments to record your activities, insights, and conclusions.

1. Open the incident's activity log: from the incident page, or from the incident details panel on the incident queue page, select the three dots in the upper right corner, and from the resulting menu, select **Activities**.

    [![Screenshot showing how to access an incident's activity log.](media/manage-incidents/activity-log.png)](media/manage-incidents/activity-log.png#lightbox)
2. Select **Add comment** at the top of the Activities pane. Type your comment in the text field. The comment field supports text and formatting, links, and images. Each comment is limited to 30,000 characters.

    ![Screenshot showing how to add a comment to an incident.](media/manage-incidents/add-comments.png)
3. Select **Save**.

All comments are added to the historical events of the incident. You can see the comments and history of an incident from the **Comments and history** link on the **Summary** page.

## Incident logging and reporting

The following management tasks can be associated with auditing and reporting on incident investigations, though they can be performed at any time.

- Edit the incident name
- Assess the activity audit and add comments in the activity log
- Export incident data to PDF

### Edit the incident name

Microsoft Defender automatically assigns a name based on alert attributes such as the number of endpoints affected, users affected, detection sources, or categories. The incident name allows you to quickly understand the scope of the incident. For example: *Multi-stage incident on multiple endpoints reported by multiple sources.*

To edit the incident name, take the following steps:

1. Follow the instructions in the opening section to Access the *Manage incident* pane.
2. Type a new name in the **Incident name** field on the **Manage incident** pane.
3. Select **Save**.

Note

- Incidents that existed before the rollout of the automatic incident naming feature retain their names.
- If another incident is merged into a renamed incident, Defender gives the incident a new name, overwriting any custom name you gave it beforehand.

### View the activity log of an incident

When doing a postmortem of an incident, view the incident's **Activity log** to see the history of actions performed on the incident (called "Audits") and any comments recorded. All changes made to the incident, whether by a user or by the system, are recorded in the activity log. For a more detailed view of all activities, select the [Activities tab](investigate-incidents#activities) on the incident page.

#### Open an incident's activity log

To open an incident's activity log, follow these steps:

1. From the incident page, or from the incident details panel on the incident queue page, select the three dots in the upper right corner, and from the resulting menu, select **Activities**.

    [![Screenshot highlighting selecting the Activities option from the three-dot menu on the incidents page of the Microsoft Defender portal.](media/manage-incidents/activity-log.png)](media/manage-incidents/activity-log.png#lightbox)
2. You can filter the activities in the activity log by origin, category, provider, trigger, activity status, policy status, type, target name, target type, or performed by. Go to **Add filter**, select your desired filters, and select **Add**.

    [![Screenshot highlighting the filter options within the activity log pane from the incident page in the Microsoft Defender portal.](media/manage-incidents/activity-log-add-filters.png)](media/manage-incidents/activity-log-add-filters.png#lightbox)
3. Go to each filter's dropdown, select filter criteria, and select **Apply**.

    [![Example of selecting a filter's dropdown menu, selecting criteria, and applying.](media/manage-incidents/activity-log-filter-example.png)](media/manage-incidents/activity-log-filter-example.png#lightbox)

You can also add your own comments by selecting **Add comment** at the top of the Activities panel. The comment box accepts text and formatting, links, and images.

## AI-generated analyst notes

When you finish investigating an incident, you can generate an automatic summary and analysis of the investigation.

The analysis includes details such as:

- A high-level summary of the incident and investigation process including actions and activities done by the analyst.
- Detailed step-by-step log and Kusto Query Language (KQL) queries run during the investigation process.

Use the generated analyst notes to train new analysts, conduct audits, support investigations, hand off work to teammates, or feed AI models and tools.

### Prerequisites for generating analyst notes

To generate analyst notes, ensure the following prerequisites are met:

- *Analyst notes* is enabled for your tenant. Your security administrator can enable analyst notes by following these steps:

    1. From the Microsoft Defender portal, go to **System** &gt; **Settings**
    2. Select **Microsoft Defender XDR**
    3. Open **Advanced features**
    4. Find the *Opt-in to analyst notes* feature and toggle it to **On**

    [![Screenshot showing the Opt-in to analyst notes feature toggle in the Microsoft Defender portal.](media/manage-incidents/opt-in-analyst-notes.png)](media/manage-incidents/opt-in-analyst-notes.png#lightbox)
- Security Copilot license
- You have one of the following permissions ([RBAC](manage-rbac)).

    - Security Data Read
    - Security Data Manage

### Generate analyst notes

To generate analyst notes after investigation is finished, take the following steps:

1. From the incident page, go to the three dots on the top right and select **Generate analyst notes**.

    ![Screenshot highlighting the generate analyst notes option from the incident page in the Microsoft Defender portal.](media/manage-incidents/generate-analyst-notes.png)

    A banner appears with the date and time the analyst-notes generation started. The preparation process can take up to 20 minutes. You can leave the page and continue working elsewhere. You receive a notification when it finishes.

    ![Screenshot showing a notification that says the analyst notes are ready with a link to the activities tab.](media/manage-incidents/notes-ready-notification.png)
2. In the **Activities** tab, there's a new line in the activity log indicating that the generation is in progress. You might have to refresh the screen to see it. Select the line to open the side panel with the status of the generation. If needed, you can stop analyst-notes generation by selecting **Stop generating**.

    [![Screenshot showing the side panel while it is in the process of generating analyst notes. There's a Stop generating button visible.](media/manage-incidents/stop-generating.png)](media/manage-incidents/stop-generating.png#lightbox)
3. When the generation is complete, go to the **Activities** tab. The analyst notes appear as a new line in the activity log. The line includes the date and time the notes were generated and who generated them.

    [![Screenshot highlighting the analyst notes in the frontline of the activities tab from the incident page in the Microsoft Defender portal.](media/manage-incidents/activities-tab.png)](media/manage-incidents/activities-tab.png#lightbox)

    Select the line to open the side panel with the generated analyst notes.

    The generated log has a disclaimer saying that it was AI generated. Select **Edit Copilot generated content** to review and modify the notes as needed. When you save the edited notes, the disclaimer is removed.

    ![Screenshot of the generated analyst notes from the incident page in the Microsoft Defender portal.](media/manage-incidents/analyst-notes.png)

    You can also give feedback on the generated notes to help improve the feature.

    ![Screenshot showing the feedback option for the generated analyst notes in the Microsoft Defender portal.](media/manage-incidents/feedback.png)

- Only users with at least the same permissions and scopeas the analyst who generated the notes can view and edit them.

## Export incident data to PDF

You can export an incident's data to PDF through the **Export incident as PDF** function and save it into PDF format. This function allows security teams to review an incident's details offline at any given time.

The incident data exported includes the following information:

- An overview containing the incident details
- The [attack story](investigate-incidents#attack-story) graph and threat categories
- The impacted [assets](investigate-incidents#assets), covering up to 10 assets for each asset type
- The [evidence list](investigate-incidents#evidence-and-response) covering up to 100 items
- Supporting data, including all [related alerts](investigate-incidents#alerts) and activities recorded in the activity log

Here's an example of the exported PDF:

[![Screenshot of the exported PDF's first page.](media/manage-incidents/export-results-small.png)](media/manage-incidents/export-results.png#lightbox)

If you have the [Copilot for Security](/en-us/security-copilot/microsoft-security-copilot) license, the exported PDF also contains the following incident data:

- [Incident summary](security-copilot-m365d-incident-summary)
- [Incident report](security-copilot-m365d-create-incident-report)

The export to PDF function is also available in the Copilot side panel. When you select the **More actions** ellipsis (...) on the upper right corner of the **Incident report** results card in the Copilot side panel, you can choose **Export incident as PDF**.

![Screenshot of additional actions in the incident report results card.](media/manage-incidents/export-incident-more-actions1.png)

To generate the PDF, perform the following steps:

1. Open an incident page. Select the **More actions** ellipsis (...) on the upper right corner and choose **Export incident as PDF**.

    [![Screenshot highlighting the More actions ellipsis on the incident page.](media/manage-incidents/export-ellipsis-small.png)](media/manage-incidents/export-ellipsis.png#lightbox)
2. In the dialog box that appears next, confirm the incident information that you want to include or exclude in the PDF. All incident information is selected by default. Select **Export PDF** to proceed.

    ![Screenshot highlighting the export incident to PDF option.](media/manage-incidents/export-options.png)
3. A status message indicating the current state of the download appears below the incident title. The export process might take a few minutes depending on the incident's complexity and the amount of data to be exported.

    [![Screenshot highlighting export message and status before download.](media/manage-incidents/export-prepare-small.png)](media/manage-incidents/export-prepare.png#lightbox)
4. Another dialog box appears indicating that the PDF is ready. Select **Download** from the dialog box to save the PDF to your device. The status message below the incident title also updates to indicate that the download is available.

    [![Screenshot highlighting export message and status when download is available.](media/manage-incidents/export-download-small.png)](media/manage-incidents/export-download.png#lightbox)

The report is cached for a couple of minutes. The system provides the previously generated PDF if you try to export the same incident again within a short time frame. To generate a newer version of the PDF, wait for a few minutes for the cache to expire.

## Set up email notifications for incidents

You can set up the Microsoft Defender portal to notify your staff with an email about new incidents or updates to existing incidents. You can choose to get notifications based on:

- Alert severity
- Alert sources
- Device group

To set up email notifications for incidents, see [get email notifications on incidents](m365d-notifications-incidents).