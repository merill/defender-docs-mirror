---
layout: Conceptual
title: Plan your ASR rules deployment - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/attack-surface-reduction-rules-deployment-plan
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to plan your attack surface reduction (ASR) rules deployment, including identifying business units, champions, apps, and deployment rings.
ms.service: defender-endpoint
ms.subservice: asr
ms.localizationpriority: medium
author: chrisda
ms.author: chrisda
ms.reviewer: sugamar, yongrhee
ms.custom: asr, msecd-doc-authoring-1012
ms.topic: article
ms.collection:
- m365-security
- m365solution-asr-rules
- highpri
- tier1
- mde-asr
ms.date: 2026-05-04T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: d77832b8-ddc2-98de-1c8d-7fa323de1234
document_version_independent_id: d77832b8-ddc2-98de-1c8d-7fa323de1234
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/attack-surface-reduction-rules-deployment-plan.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: attack-surface-reduction-rules-deployment-plan
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/attack-surface-reduction-rules-deployment-plan.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bba62c59-6b53-4be4-8b9d-6624f9184c22
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f3a81ffb-ee36-4ec7-b54a-01b6681aff65
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
platformId: 0fa17f82-f9c6-809d-4262-6caed64a4101
---

# Plan your ASR rules deployment - Microsoft Defender for Endpoint | Microsoft Learn

This article is part of the [Attack surface reduction rules deployment guide](attack-surface-reduction-rules-deployment).

Before you test or enable attack surface reduction (ASR) rules, plan your deployment. This article describes a planning methodology that you can adjust to meet your business needs.

> 
> [![Diagram of the ASR rules planning steps: determine deployment rings, identify champions, inventory apps, and define team roles.](media/asr-rules-planning-steps.png)](media/asr-rules-planning-steps.png#lightbox)

Tip

Typically, you can enable the [standard protection rules](attack-surface-reduction-rules-overview#asr-rules) in **Block** or **Warn** mode without testing. You should test other ASR rules in **Audit** mode before you switch them to **Block** or **Warn** mode. For more information, see the [ASR rules deployment guide](attack-surface-reduction-rules-deployment).

## Infrastructure requirements for the deployment guide

Although there are [multiple ways to enable ASR rules](attack-surface-reduction-rules-configure), this deployment guide is based on an infrastructure that uses:

- Microsoft Entra ID
- Microsoft Intune
- Windows 10 and Windows 11 devices
- Microsoft Defender for Endpoint E5 or Windows E5 licenses

To take full advantage of ASR rules and reporting, use a Microsoft 365 E5, Windows E5, or Microsoft 365 A5 license. For more information, see [Minimum requirements for Microsoft Defender for Endpoint](minimum-requirements).

Note

If you're transitioning from a non-Microsoft host intrusion prevention system (HIPS) to Microsoft Defender Antivirus and ASR rules, run the HIPS solution alongside ASR rules until you enable rules in **Block** mode during the [implementation phase](attack-surface-reduction-rules-deployment-implement). Contact the antivirus solution provider for exclusion recommendations.

## Step 1: Identify business units

How you select the first business unit to receive ASR rules in the [testing phase](attack-surface-reduction-rules-deployment-test) depends on the following factors:

- Size of the business unit (smaller is easier to manage)
- Availability of ASR rule champions
- Distribution and usage of affected software. For example:
    - Software
    - Shared folders
    - Scripts
    - Office macros

Your business needs might clearly dictate one of the following choices:

- Include multiple business units to get a broad sampling of software, shared folders, scripts, macros, and line of business apps that ASR rules might affect.
- Limit the initial scope to a single business unit, work through all the issues in that business unit, then repeat the rollout to other business units individually.

## Step 2: Identify ASR rule champions

ASR rule champions are people in the affected business units who can help you during the preliminary testing and implementation phases. Typically, a champion has more technical skills and doesn't mind intermittent workflow outages. Champion involvement continues throughout the broader expansion of ASR rules deployment to your organization. Your ASR rule champions are the first to experience each level of the ASR rules rollout.

It's important to provide a feedback and response channel for your ASR rule champions to alert you to work disruptions and to receive ASR rules rollout communications.

## Step 3: Inventory line-of-business apps and understand the business unit processes

A full understanding of the apps and business processes in your organization is critical to a successful ASR rules deployment. It's imperative that you understand how those apps are used within the various business units in your organization.

Take inventory of the approved apps in your organization. You can use tools like the Microsoft 365 Apps admin center to help. For more information, see [Overview of inventory in the Microsoft 365 Apps admin center](/en-us/microsoft-365-apps/admin-center/inventory).

Note

Some ASR rules don't work well if you frequently use unsigned, internally developed apps and scripts. It's more difficult to deploy ASR rules if you don't enforce code signing.

## Step 4: Define reporting and response ASR rules team roles and responsibilities

Clearly articulate the roles and responsibilities for monitoring and communicating ASR rule status and activity. Therefore, it's important to determine:

- Who's responsible for gathering reports.
- How and with whom reports are shared.
- How to escalate and address new threats or unwanted blocks by ASR rules.

Typical roles and responsibilities include:

- **IT admins**: Implement ASR rules and manage exclusions. Work with different business units on apps and processes. Create and share reports to stakeholders.
- **Certified security operations center (CSOC) analysts**: Investigate high-priority blocked processes.
- **Chief information security officer (CISO)**: Responsible for the overall security posture and health of the organization.

## Step 5: Define ASR rule deployment rings

For large enterprises, deploy ASR rules in *rings*. You define rings through the assessment of your business units, ASR rule champions, apps, and processes. After you successfully deploy ASR rules to the first ring, you can transition to the next ring into the testing phase, and so on. If you already defined rings for phased rollout of Windows updates, you can likely use those same rings to deploy ASR rules.

For more information about rings, see [Windows: Create a deployment plan](/en-us/windows/deployment/update/create-deployment-plan).