---
layout: Conceptual
title: Merge incidents manually in the Microsoft Defender portal (Legacy) - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/merge-incidents-manually
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to merge two or more incidents into a single incident in the Microsoft Defender portal, to help you investigate incidents more efficiently and effectively and resolve them more quickly and accurately.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- usx-security
- sentinel-only
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 91de55aa-48ed-e995-97a0-7d02ad0e761b
document_version_independent_id: 91de55aa-48ed-e995-97a0-7d02ad0e761b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/merge-incidents-manually.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: merge-incidents-manually
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/merge-incidents-manually.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 28c326ac-3a07-0ff3-ee57-a38d13cefbc2
---

# Merge incidents manually in the Microsoft Defender portal (Legacy) - Microsoft Defender XDR | Microsoft Learn

Note

This article describes the legacy incident experience in the Microsoft Defender portal. Incident cases are in preview and are the recommended experience for managing incidents. The legacy incident experience remains available during this preview. For the recommended incident case experience, see [Merge incident cases manually in the Microsoft Defender portal](merge-incident-cases-manually).

Incidents are automatically created in the Microsoft Defender portal when suspicious activities are detected. When two incidents describe parts of the same attack story, Defender usually merges those incidents into a single incident automatically to help you investigate incidents more efficiently and effectively and resolve them more quickly and accurately.

Sometimes, however, automatic incident merging doesn't happen, due to certain conditions that prevent incidents from being merged. To learn more about when incidents are or aren't merged, see [Incident correlation and merging](alerts-incidents-correlation#incident-correlation-and-merging). When automatic incident merging doesn't occur, or if you decide independently that two (unmerged) incidents are related and should be investigated as a single unit, you can merge them manually. The following sections explain how to merge incidents manually.

## Prerequisites

- Users must have permissions to view the incidents queue.
- Users must have read and write permissions on all the incidents they wish to merge. Incidents from different sources have different RBAC roles defined.
- Incidents that are candidates for merging must have either the same values as each other, or null values, for the **Assigned to**, **Classification**, and **Determination** fields.

## Merge incidents from the incident queue page

To merge incidents from the incident queue page, perform the following steps:

1. Open the incident queue. Select **Investigation & response &gt; Incidents & alerts &gt; Incidents** from the quick launch menu in the Microsoft Defender portal.
2. Select the two incidents you want to merge by marking the checkboxes at the beginning of their rows in the queue. When two incidents are marked, the **Merge incidents** button appears on the toolbar.

    [![Screenshot of selecting incidents from queue to merge them.](media/merge-incidents-manually/merge-incidents-from-queue.png)](media/merge-incidents-manually/merge-incidents-from-queue.png#lightbox)
3. Select **Merge incidents** from the toolbar. The **Merge incidents** flyout opens.
4. In the **Reason for merging** text box, type a description of the reason why you want to merge the incidents.
5. Provide feedback explaining why you are merging the incidents by selecting one of the predefined options. Providing this feedback helps Microsoft improve alert correlation in the future.
6. Select **Merge incidents** at the bottom of the flyout to execute the merge.

    ![Screenshot of merging incidents from queue.](media/merge-incidents-manually/merge-incidents-panel-from-queue.png)
7. In the confirmation dialog that appears, select **Merge**. When the merge is complete, a "Success" notification appears, with a link to follow to go to the merged (target) incident.

    If the merge fails, a dialog box appears with a message that the incidents failed to merge. Verify that both incidents have the same values, or that at least one of the incidents has a null value, for **Assigned to**, **Classification**, and **Determination**.

## Merge incidents from within the incident page

To merge incidents from within an incident page, follow these steps:

1. Select the name of one of the two incidents you want to merge from the incident queue. This could be either the source or the target incident, as Microsoft Defender decides which is which. For more information, see [Details of the merge process](alerts-incidents-correlation#details-of-the-merge-process).
2. The incident page appears. On the incident page, from the **Actions** menu (the three dots in the upper right corner), select **Merge incidents**.

    [![Screenshot of merging incidents from incident page.](media/merge-incidents-manually/merge-incident-from-incident-page.png)](media/merge-incidents-manually/merge-incident-from-incident-page.png#lightbox)
3. The **Merge incidents** flyout appears. In the **Other incident name or ID** field, begin typing the name or ID of the incident you want to merge with the open one. The list of available incidents is dynamically displayed and filtered as you type. When you see the one you want in the list, select it.

    ![Screenshot of incident merge panel from incident page.](media/merge-incidents-manually/merge-incidents-panel-from-incident-page.png)
4. In the **Comment** text box, type a description of the reason why you want to merge the incidents.
5. Select **Merge incidents** at the bottom of the flyout to execute the merge.
6. In the confirmation dialog that appears, select **Merge**. When the merge is complete, a "Success" notification appears, the open incident is closed, and you are redirected to the merged (target) incident.

    If the merge fails, a dialog box appears with a message that the incidents failed to merge. For the merge to succeed, both incidents must have the same values—or at least one incident must have a null value—for **Assigned to**, **Classification**, and **Determination**.

## Notes

Keep the following behaviors in mind when merging incidents:

- When the incidents are in the process of merging, you can't display or make any changes to either incident.
- Incident merges are recorded in the target incident's activity log. The log messages show the names and IDs of the source incidents that were merged into the open (target) incident.
- Activity log entries from the source incident are copied into the target incident's activity log. The entries appear with an indication that they were merged from the source incident. You can filter the activity log to show entries from either the source or target incidents, or from both.