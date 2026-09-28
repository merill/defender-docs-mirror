---
layout: Conceptual
title: Risk prioritization - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/risk-prioritization
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Learn how Defender for Cloud prioritizes security recommendations and mitigates risks to protect your environment.
ms.topic: concept-article
ms.date: 2026-02-17T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 0158e036-9808-af14-c4ae-40851d7bb68f
document_version_independent_id: 4e6a6211-551c-828c-2d0e-83445b3adab5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/risk-prioritization.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/risk-prioritization
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/risk-prioritization.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 77b4bc6f-b6f4-5f88-1b48-de32a0077f98
---

# Risk prioritization - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud proactively utilizes a dynamic engine that assesses the risks in your environment while taking into account the potential for exploitation and the potential business impact to your organization. The engine prioritizes security recommendations based on the risk factors of each resource, which are determined by the context of the environment, including the resource's configuration, network connections, and security posture.

When Defender for Cloud performs a risk assessment of your security issues, the engine identifies the most significant security risks while distinguishing them from less risky issues. The recommendations are then sorted based on their risk level, allowing you to address the security issues that pose immediate threats with the greatest potential of being exploited in your environment.

## Prerequisites

Risk prioritization and governance are supported only with the [Defender CSPM plan](concept-cloud-security-posture-management#plan-availability). While recommendations are included with the [Foundational CSPM plan](concept-cloud-security-posture-management#plan-availability), risk prioritization features require the enhanced capabilities of Defender CSPM.

If your environment isn't protected by the Defender CSPM plan, the columns with the risk prioritization features appear blurred out in the recommendations interface.

## How to use risk prioritization

To learn how to use risk prioritization effectively in your security operations, including detailed explanations of risk factors, risk calculation methodology, and risk levels, see [Security recommendations](security-recommendations).

These comprehensive guides include:

- Risk factors and how they influence prioritization
- Risk calculation methodology
- Risk level classifications (Critical, High, Medium, Low, Not evaluated)
- Recommendations dashboard details and filtering options
- Integration with attack path analysis

For portal-specific guidance:

- **For Azure portal users**: [Review security recommendations - Azure portal](security-recommendations?pivots=azure-portal)
- **For Defender portal users**: [Review security recommendations - Defender portal](review-security-recommendations?pivots=defender-portal)