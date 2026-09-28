---
layout: Conceptual
title: Threat hunting features in the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/hunting-overview
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about threat hunting features in the Microsoft Defender portal.
author: mberdugo
ms.author: monaberdugo
ms.service: defender-xdr
ms.date: 2026-08-19T00:00:00.0000000Z
ms.collection:
- M365-security-compliance
- tier1
- usx-security
ms.topic: concept-article
ai-usage: ai-assisted
locale: en-us
document_id: cb25da81-6aba-c8e5-ff0c-f0f3a7792438
document_version_independent_id: cb25da81-6aba-c8e5-ff0c-f0f3a7792438
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/hunting-overview.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: hunting-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/hunting-overview.md
platformId: 16406501-9f01-af30-98f1-558bbdebb69c
---

# Threat hunting features in the Microsoft Defender portal - Microsoft Defender XDR | Microsoft Learn

Hunting for security threats is a highly customizable activity that's most effective throughout all stages of threat hunting: proactive, reactive, and post incident. The Defender portal provides hunting tools from Microsoft Defender XDR and Microsoft Sentinel for every stage. These tools are well suited for analysts who are just starting their careers and experienced threat hunters who use advanced hunting methods. Threat hunters of all levels benefit from features that let them share techniques, queries, and findings with their teams.

## Hunting tools

The foundation of hunting queries in the Defender portal rests on Kusto Query Language (KQL). KQL is a powerful and flexible language that's optimized for searching through big-data stores in cloud environments. However, crafting complex queries isn't the only way to hunt for threats. Here are some more hunting tools and resources within the Defender portal designed to bring hunting into your reach:

- [**Microsoft Security Copilot in advanced hunting**](/en-us/defender-xdr/advanced-hunting-security-copilot) provides prerelease capabilities that include the Threat Hunting Assistant for conversational hunting and the Query assistant for generating KQL from natural language.
- [**Guided mode**](/en-us/defender-xdr/advanced-hunting-query-builder) uses a query builder for crafting meaningful hunting queries without knowing KQL or the data schema.
- [**Get help as you write queries**](/en-us/defender-xdr/advanced-hunting-query-language#get-help-as-you-write-queries) with features like autosuggest, schema tree, and sample queries.
- [**Content hub**](/en-us/azure/sentinel/sentinel-solutions-deploy?tabs=defender-portal#hunting-query) provides expert queries to match out-of-the-box solutions in Microsoft Sentinel.
- [**Microsoft Defender Experts Hunting**](/en-us/defender-xdr/defender-experts/defender-experts-hunting-overview) is a separately sold managed threat hunting service that complements security operations teams that want assistance.

Maximize the full extent of your team's hunting prowess with the following hunting tools in the Defender portal:

| Hunting tool | Description |
| --- | --- |
| [**Advanced hunting**](/en-us/defender-xdr/advanced-hunting-overview) | View and query data sources available from Defender portal services and share queries with your team. After you onboard a Microsoft Sentinel workspace, use its content, including queries and functions. |
| [**Microsoft Sentinel hunting**](/en-us/azure/sentinel/hunting) | Hunt for security threats in your data sources. Use specialized search and query tools such as **hunts** and **bookmarks**. |
| [**Go hunt**](/en-us/defender-xdr/advanced-hunting-go-hunt) | Quickly pivot an investigation to entities found within an incident. |
| [**Hunts (preview)**](/en-us/azure/sentinel/hunts) | An end-to-end, proactive threat hunting process with collaboration features. |
| [**Bookmarks**](/en-us/azure/sentinel/bookmarks) | Preserve queries and their results, and add notes and contextual observations. In the Defender portal, you can view existing Microsoft Sentinel bookmarks but can't create them. Bookmarks aren't available in Advanced hunting. |
| [**Hunting with summary rules**](/en-us/azure/sentinel/summary-rules#quickly-find-a-malicious-ip-address-in-your-network-traffic) | Use summary rules to save costs hunting for threats in verbose logs. |
| [**MITRE ATT&CK map (preview)**](/en-us/azure/sentinel/mitre-coverage#use-the-mitre-attck-framework-in-analytics-rules-and-incidents) | When creating a new hunting query, select specific tactics and techniques to apply. |
| [**Restore historical data**](/en-us/azure/sentinel/restore) | Restore data from archived logs to use in high-performance queries. |
| [**Search large data sets**](/en-us/azure/sentinel/search-jobs?tabs=defender-portal) | Search for specific events in up to one year of data in a table using KQL. |
| [**Threat analytics**](/en-us/defender-xdr/threat-analytics) | Track emerging threats and review Microsoft threat research and insights. |
| [**Threat explorer**](/en-us/defender-office-365/threat-explorer-threat-hunting) | Hunt for specialized threats related to email. |

## Hunting stages

The following table describes how you can make the most of the Defender portal's hunting tools throughout all stages of threat hunting:

| Hunting stage | Hunting tools |
| --- | --- |
| **Proactive** - Find the weak areas in your environment before threat actors do. Detect suspicious activity extra early. | - Regularly conduct end-to-end [hunts (preview)](/en-us/azure/sentinel/hunts) to proactively seek out undetected threats and malicious behaviors, validate hypotheses, and act on findings by creating new detections, incidents, or threat intelligence. - Use the [MITRE ATT&CK map (preview)](/en-us/azure/sentinel/mitre-coverage#use-the-mitre-attck-framework-in-analytics-rules-and-incidents) to identify detection gaps, and then run predefined hunting queries for highlighted techniques. - Insert new threat intelligence into proven queries to tune detections and confirm if a compromise is in process. - Take proactive steps to build and test queries against data from new or updated sources. - Use [advanced hunting](/en-us/defender-xdr/advanced-hunting-overview) to find early-stage attacks or threats that don't have alerts. |
| **Reactive** - Use hunting tools during an active investigation. | - Quickly pivot on incidents with the [**Go hunt**](/en-us/defender-xdr/advanced-hunting-go-hunt) button to search broadly for suspicious entities found during an investigation. - Use [threat analytics](/en-us/defender-xdr/threat-analytics) to investigate emerging threats and assess their potential impact. - Use the prerelease [Microsoft Security Copilot capabilities in advanced hunting](/en-us/defender-xdr/advanced-hunting-security-copilot) to investigate threats or generate queries. |
| **Post incident** - Improve coverage and insights to prevent similar incidents from recurring. | - Turn successful hunting queries into new [analytics and detection rules](/en-us/azure/sentinel/threat-detection), or refine existing ones. - [Restore historical data](/en-us/azure/sentinel/restore) and [search large datasets](/en-us/azure/sentinel/search-jobs?tabs=defender-portal) for specialized hunting as part of full incident investigations. |