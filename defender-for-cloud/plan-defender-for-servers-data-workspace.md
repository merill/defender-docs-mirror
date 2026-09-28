---
layout: Conceptual
title: Plan Defender for Servers data residency - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/plan-defender-for-servers-data-workspace
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
description: Review data residency and workspace design for Microsoft Defender for Servers.
ms.topic: concept-article
ms.date: 2025-02-19T00:00:00.0000000Z
ms.custom: references_regions
ai-usage: ai-assisted
locale: en-us
document_id: 5cfcd31e-c154-c8b9-adfc-e94be9abe83d
document_version_independent_id: 214128a6-30e7-3276-97ef-a5f6fd1018b5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/plan-defender-for-servers-data-workspace.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/plan-defender-for-servers-data-workspace
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/plan-defender-for-servers-data-workspace.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: d89f029b-3917-7a8b-38f5-dc18ba0529ec
---

# Plan Defender for Servers data residency - Microsoft Defender for Cloud | Microsoft Learn

This article helps you understand how data is stored in Microsoft Defender for Cloud, and when you need a Log Analytics workspace.

Defender for Servers is one of the paid plans provided by [Microsoft Defender for Cloud](defender-for-cloud-introduction).

## Before you begin

This article is the *fifth* article in the Defender for Servers planning guide. Before you begin, review the earlier articles:

1. Start [planning your deployment](plan-defender-for-servers).
2. Review [Defender for Servers access roles](plan-defender-for-servers-roles).
3. Select a [Defender for Servers plan](plan-defender-for-servers-select-plan)
4. Understand how [Defender for Servers collects data for assessment and when you need a workspace](plan-defender-for-servers-agents).

## Understand data residency

Before you deploy Defender for Servers, learn how Defender for Cloud stores data.

- Review [general Azure data residency considerations](https://azure.microsoft.com/blog/making-your-data-residency-choices-easier-with-azure/).
- Posture data collected by Defender for Cloud is stored in the Defender for Cloud backend. Data is routed based on the tenant location. European tenants are stored in a Europe location.
- Defender for Cloud's threat protection data including security alerts might be processed in the same region as the cloud resource, and later routed to the MDC backend.
- Data collected by the Defender for Endpoint agent for [file integrity monitoring](file-integrity-monitoring-overview) is stored for access and analysis in a Log Analytics workspace.
- You can export data to a Log Analytics workspace using [continuous export](continuous-export).