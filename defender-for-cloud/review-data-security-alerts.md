---
layout: Conceptual
title: Review Data Security Alerts - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/review-data-security-alerts
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
description: Learn how to review data security alerts in the Data and AI security dashboard in Microsoft Defender for Cloud.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 1508d442-9e0f-3a86-0d22-5e7d997326b2
document_version_independent_id: 97bb3f4b-dde5-f045-9f6b-4c2384ceb512
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/review-data-security-alerts.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/review-data-security-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/review-data-security-alerts.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 2bc1085b-e046-55d9-f163-b3c9c6dc82dc
---

# Review Data Security Alerts - Microsoft Defender for Cloud | Microsoft Learn

You can review and triage data security alerts in Microsoft Defender for Cloud. Use these alerts to identify threats and take remediation actions faster.

## Prerequisites

Before you review data security alerts, make sure you enable these components:

- [Defender cloud security posture management (Defender CSPM)](tutorial-enable-cspm-plan)
- [Sensitive data discovery](tutorial-enable-cspm-plan#enable-the-components-of-the-defender-cspm-plan)
- [Defender for Storage](tutorial-enable-storage-plan)
- [Defender for Databases](tutorial-enable-databases-plan)

## View data security alerts

Data security alerts in Defender for Cloud help you identify threats and vulnerabilities in your data environments.

To view data security alerts:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Defender for Cloud** &gt; **Data and AI security dashboard**.
3. Locate the **Data closer look** section and select either **View all managed databases alerts** or **View all storage alerts**.

    [![Screenshot that shows where the view all managed databases alerts and view all storage alerts buttons are located.](media/review-data-security-alerts/databases-storage-alerts.png)](media/review-data-security-alerts/databases-storage-alerts.png#lightbox)

After you open the alerts page, you can [investigate each security alert](manage-respond-alerts#investigate-a-security-alert), and [respond to the alerts](manage-respond-alerts#respond-to-a-security-alert).