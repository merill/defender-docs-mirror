---
layout: Conceptual
title: Security alerts - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/alerts-overview
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
description: This article provides a list of the security alerts issued by Microsoft Defender for Identity.
ms.date: 2026-07-01T00:00:00.0000000Z
ms.topic: reference
ms.reviewer: rlitinsky
locale: en-us
document_id: ae0482a9-4ea2-c264-8513-2ecd1269ce7d
document_version_independent_id: ae0482a9-4ea2-c264-8513-2ecd1269ce7d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/alerts-overview.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: alerts-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/alerts-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 793c3823-d342-1bf3-0b44-2533e46e06f7
---

# Security alerts - Microsoft Defender for Identity | Microsoft Learn

## What are Microsoft Defender for Identity security alerts?

Microsoft Defender for Identity security alerts provide information about the suspicious activities detected by Defender for Identity, and the actors and computers involved in each threat. Alert evidence lists contain direct links to the involved users and computers, to help make your investigations easy and direct.

Note

Defender for Identity isn't designed to serve as an auditing or logging solution that captures every single operation or activity on the servers where the sensor is installed. It only captures the data required for its detection and recommendation mechanisms.

The Identity alerts page gives you cross-domain signal enrichment and automated identity response capabilities. The benefit of investigating alerts with [Microsoft Defender](/en-us/microsoft-365/security/defender/microsoft-365-defender) is that Microsoft Defender for Identity alerts are correlated with information obtained from each of the other products in the suite. These enhanced alerts are consistent with the other Microsoft Defender alert formats originating from [Microsoft Defender for Office 365](/en-us/microsoft-365/security/office-365-security) and [Microsoft Defender for Endpoint](/en-us/microsoft-365/security/defender-endpoint).

Alerts originating from Defender for Identity trigger [Microsoft Defender automated investigation and response (AIR)](/en-us/microsoft-365/security/defender/m365d-autoir) capabilities, including automatically remediating alerts and the mitigation of tools and processes that can contribute to the suspicious activity.

Microsoft Defender for Identity alerts currently appear in two different layouts in the Microsoft Defender portal. While the alert views may show different information, all alerts are based on detections from Defender for Identity sensors. The differences in layout and information shown are part of an ongoing transition to a unified alerting experience across Microsoft Defender products.

Note

Classic and Defender-format alerts aren't tied to sensor version. A v2.x or v3.x sensor can contribute data to alerts in either format, depending on the **Detection source** shown on the alert.

During the transition to the Defender-format alert experience, some detections might appear in both the classic alert list and the Defender-format alert list with different names. Use **Detection source** to confirm which format generated the alert.

Tuning is format-specific. Exclusions configured under **Settings** &gt; **Identities** &gt; **Excluded entities** apply to Defender for Identity detection exclusions. Defender-format alerts should be tuned with [Microsoft Defender alert tuning rules](/en-us/microsoft-365/security/defender/investigate-alerts#tune-an-alert).

To learn more about how to understand the structure, and common components of all Defender for Identity security alerts, see [View and manage alerts](understanding-security-alerts).

For information about **True positive (TP)**, **Benign true positive (B-TP)**, and **False positive (FP)**, see [security alert classifications](understanding-security-alerts#classify-security-alerts).

## Alerts categories

The alerts are divided into categories based on the phases seen in a typical cyber-attack kill chain. The categories differ slightly depending on whether the alert originates from using the classic Microsoft Defender for Identity alerting, or Microsoft Defender. The differences are part of an ongoing transition to a unified alerting experience across Microsoft Defender products.

For example, there are categories for:

- Reconnaissance and discovery alerts
- Persistence and privilege escalation alerts
- Credential access alerts
- Lateral movement alerts

For detailed information about each alert see:

- [Microsoft Defender for Identity classic alerts](alerts-mdi-classic)
- [Microsoft Defender for Identity Defender alerts](alerts-xdr)