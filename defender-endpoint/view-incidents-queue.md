---
layout: Conceptual
title: View and organize the Incidents queue - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/view-incidents-queue
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: 
description: See the list of incidents and learn how to apply filters to limit the list and get a more focused view.
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
ms.date: 2025-01-06T00:00:00.0000000Z
locale: en-us
document_id: fb4478c6-7abd-2719-eb3e-072911502371
document_version_independent_id: fb4478c6-7abd-2719-eb3e-072911502371
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/view-incidents-queue.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: view-incidents-queue
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/view-incidents-queue.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 01762c56-0fe2-1bdb-e763-c9da72bc70e4
---

# View and organize the Incidents queue - Microsoft Defender for Endpoint | Microsoft Learn

The **Incidents queue** shows a collection of incidents that were flagged from devices in your network. It helps you sort through incidents to prioritize and create an informed cybersecurity response decision.

By default, the queue displays incidents seen in the last week, with the most recent incident showing at the top of the list, helping you see the most recent incidents first.

There are several options you can choose from to customize the Incidents queue view.

On the top navigation you can:

- Customize columns to add or remove columns
- Modify the number of items to view per page
- Select the items to show per page
- Batch-select the incidents to assign
- Navigate between pages
- Apply filters
- Customize and apply date ranges

[![The Incidents queue](media/atp-incident-queue.png)](media/atp-incident-queue.png#lightbox)

Tip

**Defender Boxed**, a series of cards showcasing your organization's security successes, improvements, and response actions in the past six months/year, appears for a limited time during January and July of each year. Learn how you can share your [Defender Boxed](/en-us/defender-xdr/incident-queue#defender-boxed) highlights.

## Sort and filter the incidents queue

You can apply the following filters to limit the list of incidents and get a more focused view.

### Severity

| Incident severity | Description |
| --- | --- |
| High (Red) | Threats often associated with advanced persistent threats (APT). These incidents indicate a high risk due to the severity of damage they can inflict on devices. |
| Medium (Orange) | Threats rarely observed in the organization, such as anomalous registry change, execution of suspicious files, and observed behaviors typical of attack stages. |
| Low (Yellow) | Threats associated with prevalent malware and hack-tools that don't necessarily indicate an advanced threat targeting the organization. |
| Informational (Grey) | Informational incidents might not be considered harmful to the network but might be good to keep track of. |

## Assigned to

You can choose to filter the list by selecting assigned to anyone or ones that are assigned to you.

### Category

Incidents are categorized based on the description of the stage by which the cybersecurity kill chain is in. This view helps the threat analyst to determine priority, urgency, and corresponding response strategy to deploy based on context.

### Status

You can choose to limit the list of incidents shown based on their status to see which ones are active or resolved.

### Data sensitivity

Use this filter to show incidents that contain sensitivity labels.

## Incident naming

To understand the incident's scope at a glance, incident names are automatically generated based on alert attributes such as the number of endpoints affected, users affected, detection sources, or categories.

For example: *Multi-stage incident on multiple endpoints reported by multiple sources.*

Note

Incidents that existed prior to the rollout of automatic incident naming retains their original name.