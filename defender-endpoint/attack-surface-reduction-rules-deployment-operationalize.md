---
layout: Conceptual
title: Manage and monitor your ASR rules deployment - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/attack-surface-reduction-rules-deployment-operationalize
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to manage and monitor your attack surface reduction (ASR) rules deployment, including reviewing reports and troubleshooting false positives.
ms.service: defender-endpoint
ms.subservice: asr
ms.localizationpriority: medium
author: chrisda
ms.author: chrisda
ms.reviewer: sugamar, yongrhee
ms.custom: asr, msecd-doc-authoring-1014
ms.topic: how-to
ms.collection:
- m365-security
- m365solution-asr-rules
- highpri
- tier1
- mde-asr
ms.date: 2026-06-16T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 468f0a03-efd9-0789-b733-ba4e6295cc43
document_version_independent_id: 468f0a03-efd9-0789-b733-ba4e6295cc43
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/attack-surface-reduction-rules-deployment-operationalize.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: attack-surface-reduction-rules-deployment-operationalize
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/attack-surface-reduction-rules-deployment-operationalize.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bba62c59-6b53-4be4-8b9d-6624f9184c22
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f3a81ffb-ee36-4ec7-b54a-01b6681aff65
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 55681e93-7d6a-a969-c35d-0c326973aa61
---

# Manage and monitor your ASR rules deployment - Microsoft Defender for Endpoint | Microsoft Learn

This article is part of the [Attack surface reduction rules deployment guide](attack-surface-reduction-rules-deployment).

After you deploy attack surface reduction (ASR) rules, monitor reports regularly and troubleshoot rule behavior to maintain protection and reduce false positives. This article describes how to review ASR rule reports and respond to ASR rules-related activity.

## Keep up with ASR rule reports and data

Any threat protection solution produces some false positives (legitimate files identified as threats) and false negatives (threats that aren't detected). For more information, see [Address false positives/negatives in Microsoft Defender for Endpoint](defender-endpoint-false-positives-negatives).

Consistent, regular review of ASR rule reports and data is important to maintain your deployment and keep up with emerging threats. Schedule reviews of ASR rule events at a frequency that keeps pace with reported events. Depending on the size of your organization, reviews might be hourly, daily, or continuously.

For more information, see [Monitor attack surface reduction (ASR) rule activity](attack-surface-reduction-rules-monitor).

## Troubleshoot ASR rules

To troubleshoot ASR rules, see [Troubleshoot attack surface reduction rules](troubleshoot-asr).