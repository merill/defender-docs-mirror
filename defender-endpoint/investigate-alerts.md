---
layout: Conceptual
title: Investigate Microsoft Defender for Endpoint alerts - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/investigate-alerts
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use the investigation options to get details on alerts are affecting your network, what they mean, and how to resolve them.
ms.service: defender-endpoint
ms.author: chrisda
author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- mde-edr
ms.topic: concept-article
ms.date: 2025-03-26T00:00:00.0000000Z
ms.subservice: edr
locale: en-us
document_id: a7b4024e-36ae-1768-dfe1-88c782b67ff5
document_version_independent_id: a7b4024e-36ae-1768-dfe1-88c782b67ff5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/investigate-alerts.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: investigate-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/investigate-alerts.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: a727e780-d741-2185-c7d3-214d8983ec29
---

# Investigate Microsoft Defender for Endpoint alerts - Microsoft Defender for Endpoint | Microsoft Learn

Investigate alerts that are affecting your network, understand what they mean, and how to resolve them.

Select an alert from the alerts queue to go to alert page. This view contains the alert title, the affected assets, the details side pane, and the alert story.

From the alert page, begin your investigation by selecting the affected assets or any of the entities under the alert story tree view. The details pane automatically populates with further information about what you selected. To see what kind of information you can view here, read [Review alerts in Microsoft Defender for Endpoint](review-alerts).

## Investigate using the alert story

The alert story details why the alert was triggered, related events that happened before and after, as well as other related entities.

Entities are clickable and every entity that isn't an alert is expandable using the expand icon on the right side of that entity's card. The entity in focus will be indicated by a blue stripe to the left side of that entity's card, with the alert in the title being in focus at first.

Expand entities to view details at a glance. Selecting an entity will switch the context of the details pane to this entity, and will allow you to review further information, as well as manage that entity. Selecting *...* to the right of the entity card will reveal all actions available for that entity. These same actions appear in the details pane when that entity is in focus.

Note

The alert story section may contain more than one alert, with additional alerts related to the same execution tree appearing before or after the alert you've selected.

[![an alert story with an alert in focus and some expanded cards](media/alert-story-tree.png)](media/alert-story-tree.png#lightbox)

## Investigate using the alert timeline

The alert timeline complements the existing 'process tree' view by offering users a comprehensive perspective on each alert. While the process tree provides a detailed breakdown of the alert's associated processes and activities, the alert timeline presents a condensed chronological view that facilitates rapid triage and decision-making.

## Take action from the details pane

Once you've selected an entity of interest, the details pane will change to display information about the selected entity type, historic information when it's available, and offer controls to **take action** on this entity directly from the alert page.

Once you're done investigating, go back to the alert you started with, mark the alert's status as **Resolved** and classify it as either **False alert** or **True alert**. Classifying alerts helps tune this capability to provide more true alerts and less false alerts.

If you classify it as a true alert, you can also select a determination, as shown in the image below.

[![The details pane with a resolved alert and the determination drop-down expanded](media/alert-details-resolved-true.png)](media/alert-details-resolved-true.png#lightbox)

If you are experiencing a false alert with a line-of-business application, create a suppression rule to avoid this type of alert in the future.

[![The actions and classification in the details pane with the suppression rule highlighted](media/alert-false-suppression-rule.png)](media/alert-false-suppression-rule.png#lightbox)

Tip

If you're experiencing any issues not described above, use the 🙂 button to provide feedback or open a support ticket.