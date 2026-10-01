---
layout: Conceptual
title: Review Remediation Actions in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-business/mdb-review-remediation-actions
breadcrumb_path: /defender-business/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: View remediations that were taken on detected threats or suspected attacks with Defender for Business.
author: chrisda
ms.author: chrisda
ms.topic: how-to
ms.service: defender-business
ms.localizationpriority: medium
ms.date: 2026-07-03T00:00:00.0000000Z
ms.reviewer: efratka
ms.collection:
- SMB
- m365-security
- m365-initiative-defender-business
- tier1
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: dcfc5c15-1969-7fdc-1b34-f5b254977e21
document_version_independent_id: dcfc5c15-1969-7fdc-1b34-f5b254977e21
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-business/mdb-review-remediation-actions.md
site_name: Docs
depot_name: Learn.defender-business
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdb-review-remediation-actions
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-business/mdb-review-remediation-actions.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b11ae577-8d18-47ab-998c-ea182a941e71
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/87b1d24d-826d-4337-90a0-b6c35e4561f2
platformId: 4b237734-b5c2-1ec5-b6c9-2bb3446ba484
---

# Review Remediation Actions in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn

As the system detects threats, remediation actions address them. Depending on the particular threat and your security settings, the system might take remediation actions automatically or wait for your approval. Examples of remediation actions include stopping a process from running or removing a scheduled task.

The Action Center tracks all remediation actions.

[![Screenshot of the location of the Action Center in the Microsoft Defender portal.](media/mdb-actioncenter.png)](media/mdb-actioncenter.png#lightbox)

Use the Action Center to review pending and completed remediation actions in Microsoft Defender for Business.

## How to use the Action Center

Use the following steps to open and review the Action Center.

1. In the [Defender portal](https://security.microsoft.com), go to **Actions & submissions** &gt; **Action Center**. Or, go directly to the **Action Center**[page](https://security.microsoft.com/action-center).
2. On the **Action Center** page, use the available tabs:

    - **Pending**: View and approve or reject any pending actions. Actions on the **Pending** tab can arise from virus protection, malware protection, automated investigations, manual response activities, or live response sessions.
    - **History**: View completed actions.

## Remediation actions

Defender for Business includes several remediation actions. These actions include manual response actions, actions following automated investigation, and live response actions.

The following table lists remediation actions that are available.

| Source | Actions |
| --- | --- |
| [Automatic attack disruption](mdb-attack-disruption) | - Contain a device<br>- Contain a user account on a device<br>- Disable a user account |
| [Automated investigations](/en-us/defender-endpoint/automated-investigations) | - Quarantine a file<br>- Remove a registry key<br>- Kill a process<br>- Stop a service<br>- Disable a driver<br>- Remove a scheduled task |
| [Manual response actions](/en-us/defender-endpoint/respond-machine-alerts) | - Run antivirus scan<br>- Isolate a device<br>- Add an indicator to block or allow a file |
| [Live response](/en-us/defender-endpoint/live-response) | - Collect forensic data<br>- Analyze a file<br>- Run a script<br>- Send a suspicious entity to Microsoft for analysis<br>- Remediate a file<br>- Proactively hunt for threats |

## Related concepts

- [Respond to and mitigate threats in Defender for Business](mdb-respond-mitigate-threats)
- [Manage devices in Defender for Business](mdb-manage-devices)