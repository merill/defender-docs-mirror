---
layout: Conceptual
title: Transition to the new Threat intelligence experience in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/threat-intelligence-transition
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn what changed in the Threat intelligence experience in Microsoft Defender, including navigation, search, filters, threat intelligence types, and relationships.
ms.service: defender-xdr
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.custom:
- cx-ti
ms.topic: concept-article
ms.date: 2026-08-31T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 95a05e03-750e-315a-0c61-3d8789e6f843
document_version_independent_id: 95a05e03-750e-315a-0c61-3d8789e6f843
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/threat-intelligence-transition.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: threat-intelligence-transition
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/threat-intelligence-transition.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 29131e21-d840-32fe-74b3-928fdf029c05
---

# Transition to the new Threat intelligence experience in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn

The new Threat intelligence experience in the Microsoft Defender portal brings threat intelligence capabilities into two primary pages: **Overview** and **Intel explorer**.

If you previously used Threat Analytics, Intel management, or other Microsoft threat intelligence experiences in the Defender portal, use this article to understand the changes introduced with the new experience.

Unless otherwise described in this article, existing threat intelligence capabilities remain unchanged.

## Changes to navigation

Use **Threat intelligence** in the Microsoft Defender portal to access:

- **Overview** - Review the threats most relevant to your organization, including latest threats, high-impact threats, highest exposure threats, threat articles, and an executive summary from the Threat Intelligence Briefing Agent.
- **Intel explorer** - Search, filter, and investigate threat intelligence across supported threat intelligence types.

## Changes to search and filtering

Intel explorer provides keyword-based search across supported threat intelligence types.

Use filters such as targeted industry, targeted geography, and source to narrow the results. You can also use table-specific filters to filter supported attributes for the selected threat intelligence type.

## Changes to threat intelligence types

Some Threat Analytics profile types use different names in the new Threat intelligence experience.

| Previous Threat Analytics type | Threat intelligence type |
| --- | --- |
| Technique | Attack patterns |
| Actor | Threat actor |
| Activity | Campaign |
| Tool | Tool |
| Vulnerability | Vulnerability |
| OSINT | Report |
| Core threat | Report |

Indicators and identities continue to appear as **Indicators** and **Identities**.

## Changes to relationships

Relationship information has moved from the separate **Relationships** tab into the entity details experience. Relationships are now available directly within entity details instead of on a separate tab.