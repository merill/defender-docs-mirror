---
layout: Conceptual
title: Enable your ASR rules deployment - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/attack-surface-reduction-rules-deployment-implement
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to enable attack surface reduction (ASR) rules by transitioning from Audit to Block mode and expanding to other deployment rings.
ms.service: defender-endpoint
ms.subservice: asr
ms.localizationpriority: medium
author: chrisda
ms.author: chrisda
ms.reviewer: sugamar
ms.custom: asr, msecd-doc-authoring-1016
ms.topic: how-to
ms.collection:
- m365-security
- m365solution-asr-rules
- highpri
- tier1
- mde-asr
ms.date: 2026-07-02T00:00:00.0000000Z
search.appverid: met150
ai-usage: ai-assisted
locale: en-us
document_id: b344315a-485b-dbc1-a535-3e4cf9f83c58
document_version_independent_id: b344315a-485b-dbc1-a535-3e4cf9f83c58
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/attack-surface-reduction-rules-deployment-implement.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: attack-surface-reduction-rules-deployment-implement
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/attack-surface-reduction-rules-deployment-implement.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bba62c59-6b53-4be4-8b9d-6624f9184c22
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f3a81ffb-ee36-4ec7-b54a-01b6681aff65
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
platformId: ec73e10c-2b87-e432-5bdb-8a4cb5e86dd3
---

# Enable your ASR rules deployment - Microsoft Defender for Endpoint | Microsoft Learn

This article is part of the [Attack surface reduction (ASR) rules deployment guide](attack-surface-reduction-rules-deployment).

After testing ASR rules in Audit mode, transition them to **Block** or **Warn** mode, starting with your first deployment ring. This article covers how to move ASR rules from Audit to Block or Warn mode in your first deployment ring, and then safely broaden your deployment across additional rings.

> 
> [![Diagram of the steps to implement ASR rules: transition from Audit to Block mode, then expand to additional rings.](media/asr-rules-implementation-steps.png)](media/asr-rules-implementation-steps.png#lightbox)

## Step 1: Transition ASR from Audit to Block

Perform the following steps to transition ASR rules from Audit mode to Block or Warn mode for your first deployment ring.

1. After you determine all required exclusions for rules in **Audit** mode, start setting some rules to **Block** or **Warn** mode. Start with the rule with the fewest triggered events. For instructions, see [Configure attack surface reduction (ASR) rules and exclusions](attack-surface-reduction-rules-configure).
2. Review [ASR rule activity](attack-surface-reduction-rules-monitor). Also review feedback from your champions.
3. Refine exclusions or create new exclusions as necessary.

Tip

Rule exclusions are better than turning off rules or switching them back to **Audit** mode.

Take advantage of the **Warn** mode in available rules to limit disruptions. **Warn** mode enables you to capture triggered events and view potential disruptions without actually blocking user access (they can click through the warning notification). For more information, see [ASR rule modes](attack-surface-reduction-rules-overview#modes-for-asr-rules).

## Step 2: Expand deployment to ring n + 1

When you're confident you correctly configured ASR rules for ring 1, you can widen the scope of your deployment to the next ring (ring n + 1).

The deployment process for each subsequent ring is:

1. Enable ASR rules in **Audit** mode.
2. Review [ASR rule activity](attack-surface-reduction-rules-monitor).
3. [Create exclusions as necessary](attack-surface-reduction-rules-overview#file-and-folder-exclusions-for-asr-rules).
4. Review ASR rule activity and refine exclusions.
5. Set rules to **Block** mode.
6. Review [ASR rule activity](attack-surface-reduction-rules-monitor).
7. [Create exclusions as necessary](attack-surface-reduction-rules-overview#file-and-folder-exclusions-for-asr-rules).
8. Disable problematic rules or switch them back to **Audit** mode.