---
layout: Conceptual
title: SaaS Security Initiative in Microsoft Defender XDR - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/saas-security-initiative
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: View and prioritize SaaS security posture management (SSPM) recommendations using the 12 metrics in the SaaS Security Initiative in Microsoft Defender XDR.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.reviewer: iidogGedanken
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: ca9b2b50-8047-5660-b8de-7b0aea430a26
document_version_independent_id: ca9b2b50-8047-5660-b8de-7b0aea430a26
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/saas-security-initiative.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: saas-security-initiative
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/saas-security-initiative.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
platformId: 146929a9-7381-d61e-f796-413c4960cd40
---

# SaaS Security Initiative in Microsoft Defender XDR - Microsoft Defender for Cloud Apps | Microsoft Learn

This article shows you how to view and prioritize SaaS security recommendations in Microsoft Defender XDR by using the SaaS Security Initiative. Before you start, make sure you meet the prerequisites.

## Overview of the SaaS Security Initiative

The SaaS Security Initiative is the main hub for SaaS security posture management (SSPM). It gives you a central place to manage software as a service (SaaS) security best practices.

The initiative groups best-practice tips into 12 metrics. You can use these metrics to rank and act on security tasks. Focus on the metrics with the most impact to improve your SaaS security posture.

## How to use the SaaS Security Initiative

Watch the following video for an overview of how to use the SaaS Security Initiative.

## Prerequisites

Before you view these recommendations, make sure you meet these requirements:

- Your organization must have Microsoft Defender for Cloud Apps licenses.
- The app you want to check must be connected to Defender for Cloud Apps. To learn how to connect apps and which connectors provide security tips, see [Connect apps to get visibility and control with Microsoft Defender for Cloud Apps](enable-instant-visibility-protection-and-governance-actions-for-your-apps).

## View SaaS Security Initiative recommendations

To view SaaS Security Initiative recommendations, perform the following steps:

1. In the Defender portal, go to **Exposure Management** and select **Initiatives**.
2. Select the **SaaS Security** initiative, and then select **Open Initiative Page**.

The page that appears lists the 12 metrics that categorize hundreds of best-practice recommendations.

[![Screenshot of the SaaS Security Initiative home page.](media/saas-securty-initiative/screenshot-of-the-saas-security-initiative-home-page.png)](media/saas-securty-initiative/screenshot-of-the-saas-security-initiative-home-page.png#lightbox)

Start with the metrics that have the highest **Impact on Initiative Score** level. This score combines the **Weight** of each item with the share of **Non-Compliant** items.

To track progress, set a **target score** for your security posture. Use this target as a benchmark to measure gains over time.

For example, to review tips for privileged access in SaaS apps, select **Missing Best Practices to Secure Privileged Access in SaaS Apps**. Then select any **Non-Compliant** item to see the fix steps.

## Related resources for SaaS Security Initiative

Use these resources to understand and build on the initiative results:

- Each metric lists its linked app connectors. Enable more connectors to get broader coverage. To see tips for a specific app, go to the **Security recommendations** tab and filter by that app.
- To learn more about Microsoft Security Exposure Management initiatives, see [Review security initiatives](/en-us/security-exposure-management/initiatives).