---
layout: Conceptual
title: KQL and the Microsoft Sentinel data lake - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/kql-overview
breadcrumb_path: ../breadcrumb/toc.json
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
ms.subservice: sentinel-platform
search.appverid: met150
description: Exploring and interacting with the Microsoft Sentinel data lake using KQL
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: zeinam
ms.topic: concept-article
ms.date: 2025-08-27T00:00:00.0000000Z
ms.collection: ms-security
locale: en-us
document_id: 4370622a-fa28-8634-f0f2-8a8d5d38458f
document_version_independent_id: 8ca99fb5-90a7-15a2-e995-150aa8fa0a7d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/kql-overview.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/kql-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/kql-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 316137c4-d54f-404e-956e-6f75e0ec598d
---

# KQL and the Microsoft Sentinel data lake - Microsoft Security | Microsoft Learn

With Microsoft Sentinel data lake, you can store and analyze high-volume, low-fidelity logs like firewall or DNS data, asset inventories, and historical records for up to 12 years. Because storage and compute are decoupled, you can query the same copy of data using multiple tools, without moving or duplicating it.

You can explore data in the data lake using Kusto Query Language (KQL) and Jupyter Notebooks, to support a wide range of scenarios, from threat hunting and investigations to enrichment and machine learning.

This article introduces the core concepts and scenarios of data lake exploration, highlights common use cases, and shows how to interact with your data using familiar tools.

## KQL interactive queries

Use Kusto Query Language (KQL) to run interactive queries directly on the data lake over multiple workspaces.

Using KQL, analysts can:

- Investigate and respond using historical data: Use long-term data in the data lake to gather forensic evidence, investigate an incident, detect patterns, and respond incidents.
- Enrich investigations with high-volume logs: Leverage noisy or low-fidelity data stored in the data lake to add context and depth to security investigations.
- Correlate asset and logs data in the data lake: Query asset inventories and identity logs to connect user activity with resources and uncover broader attack.

Use **KQL queries** under **Microsoft Sentinel** &gt; **Data lake exploration** in the Defender portal to run ad-hoc interactive KQL queries directly on long-term data. **Data lake exploration** is available after the [onboarding](sentinel-lake-onboarding) process has been completed. KQL queries are ideal for SOC analysts investigating incidents where data may no longer reside in the analytics tier. Queries enable forensic analysis using familiar queries without rewriting code. To get started with KQL queries see [Data lake exploration - KQL queries](kql-queries).

## KQL jobs

KQL jobs are one-time or scheduled asynchronous KQL queries on data in the Microsoft Sentinel data lake. Jobs are useful for investigative and analytical scenarios for example;

- Long-running one-time queries for incident investigations and incident response (IR)
- Data aggregation tasks that support enrichment workflows using low-fidelity logs
- Historical threat intelligence (TI) matching scans for retrospective analysis
- Anomaly detection scans that identify unusual patterns across multiple tables
- Promote data from the data lake to the analytics tier to enable incident investigation or log correlation.

Run one-time KQL jobs on the data lake to promote specific historical data from the data lake tier to the analytics tier, or create custom summary tables in the data lake tier. Promoting data is useful for root cause analysis or zero-day detection when investigating incidents that span beyond the analytics tier window. Submit a scheduled job on data lake to automate recurring queries to detect anomalies or build baselines using historical data. Threat hunters can use this to monitor for unusual patterns over time and feed results into detections or dashboards. For more information, see [Create jobs in the Microsoft Sentinel data lake](kql-jobs) and [Manage jobs in the Microsoft Sentinel data lake](kql-manage-jobs).

## Visualize data in Microsoft Sentinel data lake using Workbooks

You can use Microsoft Sentinel workbooks to visualize and monitor data in the Microsoft Sentinel data lake. By selecting Sentinel data lake as the data source in a workbook, you can run KQL queries directly on the data lake and render the results as interactive charts and tables. This allows you to create dashboards and reports that leverage long-term, high-volume telemetry stored in the data lake, making it ideal for advanced threat hunting, trend analysis, and executive reporting. For more information on creating workbooks with Sentinel data lake, see [Visualize data in Microsoft Sentinel data lake using Workbooks](workbooks-for-data-lake).

## Exploration scenarios

The following scenarios illustrate how KQL queries in the Microsoft Sentinel data lake can be used to enhance security operations:

| Scenario | Details | Example |
| --- | --- | --- |
| **Investigate security incidents using long-term historical data** | Security teams often need to go beyond the default retention window to uncover the full scope of an incident. | A Tier 3 SOC analyst investigating a brute force attack uses KQL queries against the data lake to query data older than 90 days. After identifying suspicious activity from over a year ago, the analyst promotes the findings to the analytics tier for deeper analysis and incident correlation. |
| **Detect anomalies and build behavioral baselines over time** | Detection engineers rely on historical data to establish baselines and identify patterns that may indicate malicious behavior. | A detection engineer analyzes sign-in logs over several months to detect spikes in activity. By scheduling a KQL job in the data lake, they build a time-series baseline and uncover a pattern consistent with credential abuse. |
| **Enrich investigations using high-volume, low-fidelity logs** | Some logs are too noisy or voluminous for the analytics tier but are still valuable for contextual analysis. | SOC analysts use KQL to query network and firewall logs stored only in the data lake. These logs, while not in the analytics tier, help validate alerts and provide supporting evidence during investigations. |
| **Respond to emerging threats with flexible data tiering** | When new threat intelligence emerges, analysts need to quickly access and act on historical data. | A threat intelligence analyst reacts to a newly published threat analytics report by running the suggested KQL queries in the data lake. Upon discovering relevant activity from several months ago, the required log is promoted into the analytics tier. To enable real-time detection for future detections, tiering policies can be adjusted on the relevant tables to mirror most recent logs into analytics tier. |
| **Explore asset data from sources beyond traditional security logs** | Enrich investigation using asset inventory such as Microsoft Entra ID objects and Azure resources. | Analysts can use KQL to query identity and resource asset information, such as Microsoft Entra ID users, apps, groups, or Azure Resources inventories, to correlate logs for broader context that complements existing security data. |