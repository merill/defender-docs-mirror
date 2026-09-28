---
layout: Conceptual
title: Manage Microsoft Defender for Endpoint incidents - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/manage-incidents
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Manage incidents by assigning it, updating its status, or setting its classification.
ms.service: defender-endpoint
ms.author: chrisda
author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- mde-edr
ms.topic: article
ms.subservice: edr
ms.date: 2024-06-05T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 6c65acc0-38d6-8ebd-dcc1-d4e4edddad30
document_version_independent_id: 6c65acc0-38d6-8ebd-dcc1-d4e4edddad30
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/manage-incidents.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: manage-incidents
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/manage-incidents.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 452a21a4-5117-e27d-6365-35ce48e5dd92
---

# Manage Microsoft Defender for Endpoint incidents - Microsoft Defender for Endpoint | Microsoft Learn

Managing incidents is an important part of every cybersecurity operation. You can manage incidents by selecting an incident from the **Incidents queue** or the **Incidents management pane**.

Selecting an incident from the **Incidents queue** brings up the **Incident management pane** where you can open the incident page for details.

[![The incidents management pane](media/atp-incidents-mgt-pane-updated.png)](media/atp-incidents-mgt-pane-updated.png#lightbox)

You can assign incidents to yourself, change the status and classification, rename, or comment on them to keep track of their progress.

Tip

For additional visibility at a glance, incident names are automatically generated based on alert attributes such as the number of endpoints affected, users affected, detection sources, or categories. This allows you to quickly understand the scope of the incident.

For example: *Multi-stage incident on multiple endpoints reported by multiple sources.*

Incidents that existed prior to the rollout of automatic incident naming retain their names.

[![The incident detail page](media/atp-incident-details-updated.png)](media/atp-incident-details-updated.png#lightbox)

## Assign incidents

If an incident hasn't been assigned yet, you can select **Assign to me** to assign the incident to yourself. Doing so assumes ownership of not just the incident, but also all the alerts associated with it.

## Set status and classification

### Incident status

You can categorize incidents (as **Active**, or **Resolved**) by changing their status as your investigation progresses. This helps you organize and manage how your team can respond to incidents.

For example, your SOC analyst can review the urgent **Active** incidents for the day, and decide to assign them to their self for investigation.

Alternatively, your SOC analyst might set the incident as **Resolved** if the incident was remediated.

### Classification

You can choose not to set a classification, or decide to specify whether an incident is true or false. Doing so helps the team see patterns and learn from them.

### Add comments

You can add comments and view historical events about an incident to see previous changes made to it.

Whenever a change or comment is made to an alert, it's recorded in the Comments and history section.

Added comments instantly appear on the pane.