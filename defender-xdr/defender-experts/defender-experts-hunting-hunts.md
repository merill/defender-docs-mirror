---
layout: Conceptual
title: Hunts in Microsoft Defender Experts Hunting overview - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/defender-experts/defender-experts-hunting-hunts
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how Hunts in Microsoft Defender Experts Hunting gives security teams visibility into in-progress and completed expert-led threat investigations.
ms.service: defender-experts-for-hunting
ms.author: dpersaud
author: dpersaud-microsoft
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- essentials-overview
ms.topic: overview
ms.custom:
- msecd-doc-authoring-1028
- cx-ti
- cx-ean
ms.date: 2026-09-22T00:00:00.0000000Z
ai-usage: ai-generated
locale: en-us
document_id: 63564ab1-2149-4450-eced-2826b09f5042
document_version_independent_id: 63564ab1-2149-4450-eced-2826b09f5042
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/defender-experts/defender-experts-hunting-hunts.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-experts/defender-experts-hunting-hunts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/defender-experts/defender-experts-hunting-hunts.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 733b0483-3bea-d1fb-db69-365eaf8dcbfd
---

# Hunts in Microsoft Defender Experts Hunting overview - Microsoft Defender XDR | Microsoft Learn

**Hunts** is an experience in Microsoft Defender Experts Hunting that gives security teams a centralized view of threat hunts Microsoft experts conduct in their environment. Use Hunts to see expert threat hunting activities while they're both in progress to see what threats we're currently tracking, and after completion to review the outcome and supporting details.

Hunts provides a record of proactive hunting activity, including investigations that don't result in uncovering an undetected threat. This visibility helps you understand what Defender Experts hunted, what they found, and whether your team needs to take follow-up action.

Hunts is generally available to Defender Experts customers. Before you use Hunts, your organization must be enrolled in Defender Experts Hunting, Plan 1, or Plan 2, and your account must have at least the **Security Reader** role in Microsoft Defender role-based access control (RBAC).

**Applies to:**

- [Microsoft Defender](../microsoft-365-defender)

## Prerequisites

- Your organization must be enrolled in [Microsoft Defender Experts Hunting](defender-experts-hunting-prerequisites).
- Your account must have the **Security Reader** role in Microsoft Defender RBAC.

## View hunt activity in one place

In the Microsoft Defender portal, select **Defender Experts** &gt; **Hunts** to view hunts conducted in your environment.

The Hunts experience distinguishes investigations that are still in progress from completed investigations. You can monitor an active investigation and return after it concludes to review the final outcome.

[![Screenshot of the Hunts page showing in-progress and completed Defender Experts investigations.](media/defender-experts-hunting-hunts/hunts-list.png)](media/defender-experts-hunting-hunts/hunts-list.png#lightbox)

## Understand hunt types

Defender Experts conducts the following types of hunts:

- **Intelligence-based hunts:** Proactive investigations of emerging threats, attacker techniques, campaigns, and other intelligence-driven hypotheses.
- **Suspicious activity hunts:** Investigations that begin when Defender Experts identifies behavior in your environment that warrants deeper analysis.

## Follow a hunt from investigation to outcome

The hunt status helps you distinguish ongoing work from final conclusions.

| Status | What it means |
| --- | --- |
| **In progress** | Defender Experts is still investigating. The available information isn't a final conclusion. |
| **Completed** | The investigation has concluded. You can review the outcome and supporting details, including when the hunt didn't result in an incident. |

When a noteworthy threat is circulating, Hunts lets you see that Defender Experts is investigating it on your behalf. After the hunt is complete, review the findings to determine whether your organization needs to take action.

[![Screenshot of a completed Defender Experts hunt showing the investigation status, summary, and outcome.](media/defender-experts-hunting-hunts/completed-hunt-details.png)](media/defender-experts-hunting-hunts/completed-hunt-details.png#lightbox)

## How Hunts works

Defender Experts investigates intelligence-based hypotheses and suspicious activity in your environment. Hunts shows the investigation as it progresses:

1. Defender Experts starts a hunt based on threat intelligence or suspicious behavior.
2. The hunt appears as **In progress** while the investigation continues.
3. Defender Experts completes the investigation and records the outcome.
4. You review the completed hunt and its supporting details to determine whether follow-up action is needed.