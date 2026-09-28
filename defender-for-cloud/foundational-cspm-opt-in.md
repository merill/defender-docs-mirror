---
layout: Conceptual
title: Opt in to Foundational CSPM - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/foundational-cspm-opt-in
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
description: Learn about the opt-in model for Foundational CSPM for new Azure subscriptions and choose how to manage your Azure security posture.
ms.topic: concept-article
ms.date: 2026-07-30T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: b36f08e8-6006-88f2-cad1-8994f6b3e6ac
document_version_independent_id: 43eb57ad-74a8-5f32-6ab9-9ba472a23b49
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/foundational-cspm-opt-in.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/foundational-cspm-opt-in
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/foundational-cspm-opt-in.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: b7159c5a-d04d-7387-8cb2-7269c3e174cc
---

# Opt in to Foundational CSPM - Microsoft Defender for Cloud | Microsoft Learn

Starting October 27, 2026, Foundational CSPM will move to an opt-in model for new Azure subscriptions and will no longer be enabled by default.

This change gives you more control over how security posture management is configured for each new Azure subscription and is part of the transition of cloud security posture management to the Microsoft Defender portal.

Foundational CSPM will continue to be available at no cost and can be enabled at any time based on your organization's needs.

Important

This change applies only to new Azure subscriptions. Existing subscriptions that already have Foundational CSPM enabled will remain enabled unless you turn off the plan.

## What is Foundational CSPM?

Foundational CSPM is a free cloud security posture management plan in Microsoft Defender for Cloud. It helps you assess the security posture of your cloud resources by providing foundational capabilities, including security recommendations and Secure Score. These capabilities help you identify risks and prioritize remediation.

To learn more, see [What is Cloud Security Posture Management (CSPM)](concept-cloud-security-posture-management).

## What's changing?

Starting October 27, 2026, the default behavior for new Azure subscriptions will change:

- New Azure subscriptions will start with Foundational CSPM turned off.
- To use Foundational CSPM on a new Azure subscription, you must enable the plan for that subscription.

## What stays the same?

- Foundational CSPM remains available at no cost.
- Existing Azure subscriptions keep their current Foundational CSPM configuration.
- AWS and GCP environments aren't affected. Foundational CSPM remains enabled by default when those environments are onboarded.
- When enabled, Foundational CSPM continues to provide its existing posture-management capabilities, including security recommendations and Secure Score.

## Choose how to manage your Azure security posture

The move to an opt-in model for Foundational CSPM is part of Microsoft's broader transition of cloud security posture management to the Microsoft Defender portal. To learn more about the new management experience, see [Overview of Defender for Cloud in Defender portal](defender-portal/defender-for-cloud-defender-portal).

Starting October 27, 2026, the Microsoft Defender portal will become the recommended experience for managing Azure security posture. It provides a unified security experience alongside other Microsoft Security solutions and introduces advanced posture-management capabilities that help security teams manage posture across onboarded environments at scale.

In the Microsoft Defender portal, you can centrally manage Defender plans, Azure posture policies, and security recommendations.

Choose the management experience that best fits your organization:

| Option | What to do |
| --- | --- |
| **Recommended: Microsoft Defender portal** | Onboard your Azure environment to Microsoft Defender.[Overview of Defender for Cloud in Defender portal](defender-portal/defender-for-cloud-defender-portal).Manage your Azure posture policies and security recommendations in the Microsoft Defender portal. |
| **Continue managing plans in the Azure portal** | [Enable Foundational CSPM or another Defender plan in the Azure portal](connect-azure-subscription).Continue managing your Azure security posture in the Azure portal. |

More information about the transition to the Microsoft Defender portal will be published closer to the transition date.

## Learn more

- [What is Cloud Security Posture Management (CSPM)](concept-cloud-security-posture-management)
- [Overview of Defender for Cloud in Defender portal](defender-portal/defender-for-cloud-defender-portal)