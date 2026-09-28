---
layout: Conceptual
title: Prioritize, manage, investigate, and respond to incidents in Microsoft Defender XDR - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/step-by-step-guides/how-to-prioritize-manage-investigate-and-respond-to-incidents-in-microsoft-365-defender
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to prioritize and manage incidents in Microsoft Defender XDR. See how Automated Investigation and Response (AIR) correlates related alerts, assesses threat scope, and combines findings into a single incident.
ms.service: defender-office-365
author: chrisda
ms.author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-guidance-templates
- m365-security
- tier3
ms.topic: how-to
ms.date: 2026-06-12T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: b09aadf3-8c2e-4334-8ada-a8230f0d7702
document_version_independent_id: b09aadf3-8c2e-4334-8ada-a8230f0d7702
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/step-by-step-guides/how-to-prioritize-manage-investigate-and-respond-to-incidents-in-microsoft-365-defender.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: step-by-step-guides/how-to-prioritize-manage-investigate-and-respond-to-incidents-in-microsoft-365-defender
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/step-by-step-guides/how-to-prioritize-manage-investigate-and-respond-to-incidents-in-microsoft-365-defender.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: 1b467263-ddb1-6276-a7b4-aa157bb4108a
---

# Prioritize, manage, investigate, and respond to incidents in Microsoft Defender XDR - Microsoft Defender for Office 365 | Microsoft Learn

When alerts are triggered in Microsoft Defender, automated investigation and response (AIR) begins and hunts throughout an organization's subscription, determine the impact and scope of the threat, and collate the information into a single Incident so that admins don't have to manage multiple incidents.

## Prerequisites

Before you begin, make sure you have the following licensing and permissions:

- Microsoft Defender for Office 365 Plan 2 or higher
- Sufficient permissions (Security reader, security operations, or security administrator, plus [Search and purge](../mdo-portal-permissions) role)

## Prioritize & manage Incidents

Navigate to the security portal Incidents page https://security.microsoft.com/incidents.

When the Incident page loads you can filter and prioritize by clicking columns to sort the actions or press Filters to apply a filter such as data source, tags or state.

Now you have a prioritized list of incidents, from which you can select to rename, assign, classify, tag, change the status or add comments via the **Manage incidents** button.

Use the filters to make sure Microsoft Defender for Office 365 items are included.

If you're looking for specific alerts, either use the incident search capability (*Search for name or ID*) or consider using the alert queue filtering by alert title, severity, or another alert attribute.

## Investigate & Respond to Incidents

After you have prioritized your incident queue, select the Incident you'd like to investigate to load the incidents Overview page. You see useful information, such as *MITRE ATT&CK techniques observed* and a *timeline of the attack*.

The tabs at the top of the incident page allow you to explore more details such as the affected users, mailboxes, endpoints, and et cetera.

The *Evidence and Response* tab shows items identified as related to the alert that triggered the investigation.

Any items showing as *Pending Action* on the *Evidence and Response* tab are awaiting approval from an administrator. Sorting by the remediation status column in the *All Evidence* view is recommended, followed by clicking the entity or cluster to load the flyout menu where you can then approve the actions if appropriate.

If you need to understand the evidence and entities involved further, you can use the incident graph to see the visual linkage of the evidence and entities involved. Alternatively, you can review the underlying investigations, which show more of the entities and items involved in the security event.