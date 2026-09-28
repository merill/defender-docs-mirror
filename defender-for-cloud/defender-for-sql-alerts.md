---
layout: Conceptual
title: Explore and investigate Defender for SQL security alerts - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-sql-alerts
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
description: View and investigate SQL security alerts through the Alerts page, affected machine security pages, workload protections dashboard, or alert email links.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 02b7abf6-8ca4-dfdf-0427-f8a5b523e27b
document_version_independent_id: aced2b5a-805d-b855-83db-a67c5bda60ba
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-sql-alerts.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-sql-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-sql-alerts.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 374addc7-b316-5119-a30f-bfb634dcb485
---

# Explore and investigate Defender for SQL security alerts - Microsoft Defender for Cloud | Microsoft Learn

This article shows how to review Microsoft Defender for SQL alerts. Learn how to spot suspicious activity and take action on affected resources. You can open alerts quickly and follow up with a deeper look when needed.

## View and investigate SQL alerts

You can access and review security alerts from Microsoft Defender for SQL. Defender for SQL creates alerts when it detects suspicious database activity or possible weak points. Each alert needs your review.

There are several ways to view Microsoft Defender for SQL alerts in Microsoft Defender for Cloud:

- The **Alerts** page.
- The affected machine's security page.
- The [workload protections dashboard](workload-protections-dashboard), which shows security coverage across resources.
- Through the direct link provided in the alert's email.

## Open SQL security alerts in Defender for Cloud

To view security alerts in Microsoft Defender for Cloud, follow these steps:

1. Go to the [Azure portal](https://portal.azure.com) and sign in.
2. Search for and select **Microsoft Defender for Cloud**.
3. Select **Security alerts**.
4. Select an alert.

Alerts are self-contained and include detailed remediation steps and investigation guidance. For broader investigation, use related Microsoft Defender for Cloud and Microsoft Sentinel capabilities:

- Enable SQL Server auditing for deeper investigations. If you use Microsoft Sentinel, you can upload SQL auditing logs from Windows Security Log events to Sentinel for richer investigation. For details, see [SQL Server auditing](/en-us/sql/relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification?preserve-view=true&amp;view=sql-server-ver15).
- To improve your security posture, use Defender for Cloud's recommendations for the host machine indicated in each alert to reduce the risks of future attacks.

For details, see [Manage and respond to security alerts](manage-respond-alerts).