---
layout: Conceptual
title: Weekly Operational Guide - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/ops-guide/ops-guide-weekly
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
description: Learn about the Microsoft Defender for Identity activities that we recommend for your team on a weekly basis.
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: martin77s
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 4c42aa24-9101-06c6-9258-7bff8a59b644
document_version_independent_id: 4c42aa24-9101-06c6-9258-7bff8a59b644
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/ops-guide/ops-guide-weekly.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: ops-guide/ops-guide-weekly
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/ops-guide/ops-guide-weekly.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cd48b104-e308-4e08-a405-66f04a7df418
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ac23bdb5-c078-4620-8ee2-60eba45e97f8
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: 60f1d12d-32f2-2823-b1fe-4b76b3c46345
---

# Weekly Operational Guide - Microsoft Defender for Identity | Microsoft Learn

This article reviews the Microsoft Defender for Identity activities we recommend for your team on a weekly basis. These tasks include reviewing Secure Score recommendations, responding to emerging threats with custom detections, and proactively hunting for threats. Performing these checks each week helps security administrators and SOC analysts identify identity-related risks early and maintain a strong security posture.

## Review Secure score recommendations

**Where**: In Microsoft Defender, select **Secure score**.

**Persona**: Security and compliance administrators, SOC analysts

Microsoft Secure Score shows security recommendations that matter most to your organization. For Defender for Identity, these recommendations focus on monitoring on-premises identities and weak points in your identity infrastructure.

To view Secure Score recommendations per product, in Microsoft Defender, select **Secure score &gt; Recommended actions**, and group the list by **Product**.

For more information, see:

- [Microsoft Defender for Identity's security posture assessments](../security-assessment)
- [Microsoft Secure Score](/en-us/microsoft-365/security/defender/microsoft-secure-score)

## Review and respond to emerging threats

**Where**: In Microsoft Defender, select **Hunting &gt; Advanced hunting**

**Persona**: Security and compliance administrators, SOC analysts

Configure custom detections in Microsoft Defender to monitor and respond to events like suspected breach activity and misconfigured endpoints.

Custom detection rules use advanced hunting queries. They can trigger alerts and response actions on their own. Run these rules regularly to stay on top of new alerts and take action.

For more information, see:

- [Custom detections overview](/en-us/microsoft-365/security/defender/custom-detections-overview)
- [Create and manage custom detections rules](/en-us/microsoft-365/security/defender/custom-detection-rules)

## Proactively hunt

**Where**: In Microsoft Defender, select **Hunting &gt; Advanced hunting**.

**Persona**: SOC analysts

You might want to proactively hunt on a daily or weekly basis, depending on your level as a SOC analyst.

Use Microsoft Defender advanced hunting to proactively explore through the last 30 days of raw data, including Defender for Identity data correlated with data streaming from other Microsoft Defender services.

Inspect events in your network to locate threat indicators and entities, including both known and potential threats.

We recommend that beginners use guided advanced hunting, which provides a query builder. If you're comfortable using Kusto Query Language (KQL), build queries from scratch as needed for your investigations.

For more information, see [Proactively hunt for threats with advanced hunting in Microsoft Defender](/en-us/microsoft-365/security/defender/advanced-hunting-overview).