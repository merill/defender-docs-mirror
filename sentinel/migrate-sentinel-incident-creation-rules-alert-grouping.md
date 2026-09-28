---
layout: Conceptual
title: Migrate Microsoft Sentinel incident creation rules to alert grouping in Microsoft Defender | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/migrate-sentinel-incident-creation-rules-alert-grouping
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
description: Learn how to migrate Microsoft Sentinel incident creation behavior to Microsoft Defender alert grouping rules during onboarding.
ms.author: monaberdugo
author: mberdugo
ms.localizationpriority: medium
ms.collection:
- m365-security
- sentinel-only
ms.topic: how-to
ms.date: 2026-06-11T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 3ea78c55-2084-4a1d-6539-a0d121087458
document_version_independent_id: 5b4eb370-8677-13df-273a-a525abf1051d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/migrate-sentinel-incident-creation-rules-alert-grouping.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/migrate-sentinel-incident-creation-rules-alert-grouping
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/migrate-sentinel-incident-creation-rules-alert-grouping.md
platformId: 4f704602-97c3-06fc-8036-89eac910816b
---

# Migrate Microsoft Sentinel incident creation rules to alert grouping in Microsoft Defender | Microsoft Learn

Use this guide when you onboard a Microsoft Sentinel workspace to the Defender portal and want to preserve Sentinel-like incident creation behavior for Defender alerts.

## What alert grouping rules do

Alert grouping rules in Microsoft Defender control how related alerts are grouped into incidents. They provide the Defender-side behavior controls that align with incident creation behavior used in Microsoft Sentinel Incident creation rules.

When you choose **Retain Sentinel incident creation behavior for XDR alerts** during onboarding, Defender applies equivalent grouping behavior as part of onboarding.

## Prerequisites

- A Microsoft Sentinel workspace with incident creation settings rules configured.
- Permission to onboard the workspace in the Defender portal.
- Permission to view and manage detection rules in Microsoft Defender.

## Migrate incident creation behavior during onboarding

To migrate incident creation behavior when you onboard a Microsoft Sentinel workspace to the Defender portal, follow the directions in [Connect Microsoft Sentinel to the Microsoft Defender portal](microsoft-sentinel-onboard#onboard-microsoft-sentinel). During the onboarding flow, make sure you do the following:

1. Set the workspace you want to use as the primary workspace.
2. In the onboarding dialog, select **Retain Sentinel incident creation behavior for XDR alerts**.

This option applies migration behavior during onboarding. Later changes to Sentinel rule grouping aren't continuously synced to Defender.

## Validate migrated alert grouping rules

After onboarding finishes:

1. Go to **Settings** &gt; **Microsoft Defender XDR** &gt; **Alert grouping**.
2. Verify that expected rules are present and enabled.
3. Open a migrated rule and confirm key behavior settings match your expected incident grouping outcomes.

[![Screenshot of the alert grouping rules page showing migrated rules in Microsoft Defender.](media/migrate-sentinel-incident-creation-rules-alert-grouping/alert-grouping-rules-list.png)](media/migrate-sentinel-incident-creation-rules-alert-grouping/alert-grouping-rules-list.png#lightbox)

## Validate incident and automation outcomes

1. Trigger representative detections.
2. Verify incident grouping still matches expected automation patterns.
3. Validate playbooks, routing, and ticketing integrations that depend on incident behavior.
4. Confirm incident title behavior matches your operational expectations. Incident titles might differ from Sentinel depending on correlation context.
5. If manual incident merges are used in your process, validate those workflows. Manual merges can combine incidents that were originally kept separate.

To review correlation behavior and incident merges during investigation, see [Alert correlation and incident merging in the Microsoft Defender portal](/en-us/defender-xdr/alerts-incidents-correlation).

The associated incidents view improves analyst context, but it doesn't change grouping rules by itself.

[![Screenshot of the incident graph filter showing associated incidents options.](media/migrate-sentinel-incident-creation-rules-alert-grouping/associated-incidents-filter.png)](media/migrate-sentinel-incident-creation-rules-alert-grouping/associated-incidents-filter.png#lightbox)