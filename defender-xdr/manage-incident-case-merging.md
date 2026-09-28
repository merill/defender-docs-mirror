---
layout: Conceptual
title: Merge and split incident cases in the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/manage-incident-case-merging
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn when to merge incident cases or move alerts between incident cases in the Microsoft Defender portal.
ms.service: microsoft-defender
ms.subservice: unified-security-operations
author: guywi-ms
ms.author: guywild
ms.date: 2026-07-15T00:00:00.0000000Z
ms.collection:
- M365-security-compliance
- tier1
- usx-security
ms.topic: concept-article
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: a0406791-b922-086c-1717-4bbda5e1dbd2
document_version_independent_id: a0406791-b922-086c-1717-4bbda5e1dbd2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/manage-incident-case-merging.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: manage-incident-case-merging
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/manage-incident-case-merging.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 0a626894-1610-f5be-1532-02a25cd1c259
---

# Merge and split incident cases in the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn

Incident cases in the Microsoft Defender portal help security operations teams investigate and respond to related alerts in a single case management workflow. As an investigation develops, you might need to merge related incident cases or move alerts between incident cases to keep the investigation scope accurate.

Use merging and alert movement to reduce duplicate work, group related investigation context, and make sure analysts respond to the right set of alerts, assets, evidence, and activities.

Note

Incident cases are in preview and are the recommended experience for managing incidents in the Microsoft Defender portal. The legacy incident experience remains available during this preview.

For an overview of incident cases, see [Case management in the Microsoft Defender portal](siem-defender-case-management).

For general information about alert correlation and incident merging in the existing incident experience, see [Alert correlation and incident merging in the Microsoft Defender portal](alerts-incidents-correlation).

## Merge or split incident case scope

Use the following guidance to decide whether to merge incident cases or move alerts between incident cases.

| Action | Use when |
| --- | --- |
| Merge incident cases | Multiple incident cases represent the same attack, investigation, or related activity and should be handled together. |
| Move alerts between incident cases | One or more alerts don't belong in the current incident case and should be investigated as part of a different incident case. |

## Incident case correlation

Microsoft Defender automatically correlates related alerts and investigation context into incident cases. Correlation can be based on common entities, timing, attack behavior, service signals, detection sources, and other related activity.

Automatic correlation helps reduce duplicate investigation work and gives analysts a single incident case for related alerts, assets, evidence, and response activity.

The correlation logic is managed by Microsoft Defender.

## When to merge incident cases

Merge incident cases when multiple cases are part of the same investigation and should be handled together.

For example, merge incident cases when they include:

- Related alerts from the same attack or campaign
- Related users, devices, mailboxes, cloud resources, or other assets
- Shared indicators, such as files, IP addresses, senders, or processes
- Similar tactics, techniques, and procedures
- Activity that occurred in the same time frame
- Activity that represents a single multistage attack

Manual merging is useful when related incident cases weren't merged automatically, or when analysts determine during investigation that separate incident cases should be handled as one case.

When incident cases are merged, one case ID is retained, case data is consolidated into the retained case, and the other case IDs are removed.

Note

Incident cases with a resolved status can't be merged.

For step-by-step guidance, see [Merge incident cases manually in the Microsoft Defender portal](merge-incident-cases-manually).

## When to move alerts between incident cases

Move alerts between incident cases when an alert doesn't belong in the current case or should be investigated with a different case.

For example, move an alert when:

- The alert was correlated to the wrong incident case.
- The alert is unrelated to the rest of the current incident case.
- The alert belongs to another active investigation.
- Moving the alert improves investigation ownership, scope, or response accuracy.

Every alert must belong to an incident case. Moving an alert changes the incident case where the alert is investigated and managed.

For step-by-step guidance, see [Move alerts from one incident case to another in the Microsoft Defender portal](move-alert-to-another-incident-case).