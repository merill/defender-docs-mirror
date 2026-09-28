---
layout: Conceptual
title: Threat analytics for Microsoft Sentinel users (preview) | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/threat-analytics-sentinel
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
description: Learn about threat analytics and how Microsoft Sentinel users can access it in the Microsoft Defender portal.
ms.author: pauloliveria
author: poliveria
ms.reviewer: prtanej
ms.topic: concept-article
ms.date: 2025-11-18T00:00:00.0000000Z
ms.collection: usx-security
locale: en-us
document_id: 79320ba9-0940-87bc-3e23-ac51d21dff9a
document_version_independent_id: 2b0473d4-9c17-de87-0ef2-5ba1b774b666
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/threat-analytics-sentinel.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/threat-analytics-sentinel
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/threat-analytics-sentinel.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: a3104924-1b97-f1e3-7666-9e436677377c
---

# Threat analytics for Microsoft Sentinel users (preview) | Microsoft Learn

Important

Threat analytics access for customers who use only Microsoft Sentinel is currently in preview. This information relates to a prerelease product that may be substantially modified before it's released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

**Threat analytics** is an in-product threat intelligence solution from expert Microsoft security researchers. It helps security teams stay efficient while facing emerging threats, such as:

- Active threat actors and their campaigns
- Popular and new attack techniques
- Critical vulnerabilities
- Common attack surfaces
- Prevalent malware

For more information, see the following articles:

- [Threat analytics in Microsoft Defender](/en-us/defender-xdr/threat-analytics)
- [Understand the analyst report in threat analytics in Microsoft Defender](/en-us/defender-xdr/threat-analytics-analyst-reports)
- [Get access to IOCs in threat analytics in Microsoft Defender](/en-us/defender-xdr/threat-analytics-indicators)

## Available threat analytics sections for Microsoft Sentinel customers

You can access threat analytics from the Microsoft Defender portal. By default, Microsoft Sentinel customers can access the following tabs or sections in threat analytics:

- Overview
- Analyst report
- Indicators

If you only have a Microsoft Sentinel license, you can't access the following sections in threat analytics because they're integrated with Microsoft Defender capabilities and data:

- Related incidents
- Impacted assets
- Endpoints exposure
- Recommended actions

## Unlock restricted sections in threat analytics

To access these other threat analytics sections, you need to have a license for at least one Microsoft Defender product and appropriate role-based access control (RBAC) permissions. For more information about Microsoft Defender license requirements, see [Microsoft Defender XDR prerequisites](/en-us/defender-xdr/prerequisites).