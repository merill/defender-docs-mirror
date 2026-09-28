---
layout: Conceptual
title: ASR rules deployment guide - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/attack-surface-reduction-rules-deployment
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Plan, test, and deploy attack surface reduction (ASR) rules in Microsoft Defender for Endpoint to block risky software behavior and protect against advanced threats.
ms.service: defender-endpoint
ms.subservice: asr
ms.localizationpriority: medium
author: chrisda
ms.author: chrisda
ms.reviewer: sugamar
ms.custom: asr, msecd-doc-authoring-1012
ms.topic: concept-article
ms.collection:
- m365-security
- m365solution-asr-rules
- highpri
- tier1
- mde-asr
ms.date: 2026-05-04T00:00:00.0000000Z
ai-usage: ai-assisted
search.appverid: met150
locale: en-us
document_id: a33aae19-da91-5379-255d-3a839c672d03
document_version_independent_id: a33aae19-da91-5379-255d-3a839c672d03
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/attack-surface-reduction-rules-deployment.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: attack-surface-reduction-rules-deployment
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/attack-surface-reduction-rules-deployment.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bba62c59-6b53-4be4-8b9d-6624f9184c22
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f3a81ffb-ee36-4ec7-b54a-01b6681aff65
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
platformId: afb05ee3-88b8-a336-66a2-3c2efcb7e470
---

# ASR rules deployment guide - Microsoft Defender for Endpoint | Microsoft Learn

Attack surface reduction (ASR) rules target risky software behavior on Windows devices that attackers commonly exploit through malware (for example, launching scripts that download files, running obfuscated scripts, and injecting code into other processes). For an introduction to ASR rules and their requirements, see [Attack surface reduction (ASR) rules overview](attack-surface-reduction-rules-overview).

This guide helps you plan, test, implement, and manage your ASR rules deployment to effectively stop advanced threats like human-operated ransomware.

Important

This guide provides images and examples to help you decide how to configure ASR rules. These images and examples might not reflect the best configuration options for your environment.

[![Diagram of the ASR rules deployment phases: plan, test, enable, and maintain.](media/asr-rules-deployment-phases.png)](media/asr-rules-deployment-phases.png#lightbox)

## Important predeployment caveat

Typically, you can enable the [standard protection rules](attack-surface-reduction-rules-overview#asr-rules) in **Block** or **Warn** mode without testing. You should test other ASR rules in **Audit** mode before you switch them to **Block** or **Warn** mode.

## Before you begin

Before you start the deployment process, review the following documentation:

- [Overview of attack surface reduction](attack-surface-reduction-overview)
- [Attack surface reduction (ASR) rules reference](attack-surface-reduction-rules-reference)

## Deployment steps

Use the following articles to plan, test, implement, and manage your ASR rules deployment:

1. [Plan ASR rules deployment](attack-surface-reduction-rules-deployment-plan): Determine infrastructure requirements, select business units and champions, and define team roles.
2. [Test ASR rules](attack-surface-reduction-rules-deployment-test): Configure rules in **Audit** mode, review reports, and add exclusions.
3. [Enable ASR rules](attack-surface-reduction-rules-deployment-implement): Transition rules from **Audit** to **Block** mode, and expand to other deployment rings.
4. [Manage and monitor ASR rules](attack-surface-reduction-rules-deployment-operationalize): Monitor ongoing activity, manage false positives, and use advanced hunting.