---
layout: Conceptual
title: Monthly Operational Guide - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/ops-guide/ops-guide-monthly
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: Learn about the Microsoft Defender for Identity activities that we recommend for your team on a monthly basis.
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: martin77s
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: ff192fb8-62b7-07bd-1b53-5612d70ad16a
document_version_independent_id: ff192fb8-62b7-07bd-1b53-5612d70ad16a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/ops-guide/ops-guide-monthly.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: ops-guide/ops-guide-monthly
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/ops-guide/ops-guide-monthly.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 9b51cc4b-644f-a0e6-3bc1-860950b1ac9f
---

# Monthly Operational Guide - Microsoft Defender for Identity | Microsoft Learn

This article reviews the Microsoft Defender for Identity activities we recommend for your team on a monthly basis. These tasks include reviewing and adjusting alert tuning configurations and tracking new feature changes across Microsoft Defender XDR and Defender for Identity. This guide is intended for security administrators and SOC analysts responsible for maintaining an effective detection and response posture.

## Review tuned alerts and adjust tuning if needed

**Where**: In Microsoft Defender, select **Hunting &gt; Advanced hunting**

**Persona**: Security and compliance administrators, SOC analysts

Microsoft Defender allows you to *tune* alerts, helping you reduce the number of alerts you need to triage. Tuning alerts resolves alerts automatically based on your configurations and rule conditions.

We recommend reviewing your tuning configurations regularly to make sure that they're still relevant and effective. For example:

- Check to see if your existing rules have matches as expected
- If a rule has no matches, consider whether you still need it or if you can remove it

For more information, see [Investigate Defender for Identity security alerts in Microsoft Defender](../manage-security-alerts).

## Track new changes in Microsoft Defender and Defender for Identity

**Persona**: Security administrators, SOC analysts

Use the following resources to stay informed about recent changes and new features in Microsoft Defender XDR and Defender for Identity:

**Where**:

- In the Microsoft 365 admin center, select **Health &gt; Message center**. For more information, see [Track new and changed features in the Microsoft 365 Message center](/en-us/microsoft-365/admin/manage/message-center).
- The [Microsoft Defender XDR monthly news](https://techcommunity.microsoft.com/t5/microsoft-defender-xdr-blog/bg-p/MicrosoftThreatProtectionBlog/label-name/Defender%20News).
- For details about Defender for Identity updates, see [What's new in Microsoft Defender for Identity](../whats-new).