---
layout: Conceptual
title: Responsible AI FAQ for the Microsoft Sentinel UEBA behaviors layer | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/entity-behaviors-layer-rai-faqs
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
description: This FAQ provides information about the AI technology used in the Microsoft Sentinel UEBA behaviors layer, along with key considerations and details about how AI is used, how it was tested and evaluated, and any specific limitations.
ms.date: 2026-01-11T00:00:00.0000000Z
ms.custom:
- responsible-ai-faqs
ms.topic: contributor-guide
ms.author: guywild
author: guywi-ms
ms.reviewer: mshechter
locale: en-us
document_id: ce1c8336-fa72-30dd-7c1d-20a32d928549
document_version_independent_id: b942e690-720c-3147-5c0e-265cb9d7e54d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/entity-behaviors-layer-rai-faqs.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/entity-behaviors-layer-rai-faqs
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/entity-behaviors-layer-rai-faqs.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c6f99e62-1cf6-4b71-af9b-649b05f80cce
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3f56b378-07a9-4fa1-afe8-9889fdc77628
platformId: 8c07e442-0d65-4b96-a0a7-33d298572cc9
---

# Responsible AI FAQ for the Microsoft Sentinel UEBA behaviors layer | Microsoft Learn

These frequently asked questions (FAQ) describe the AI impact of the [UEBA behaviors layer](entity-behaviors-layer) feature in Microsoft Sentinel.

## What is the UEBA behaviors layer?

The UEBA behaviors layer is an AI-powered capability in Microsoft Sentinel that transforms fragmented raw logs into contextualized behavioral insights that explain "who did what to whom".

- **Inputs:** Raw security logs from sources, such as the AWS CloudTrail and CommonSecurityLog tables.
- **Outputs:** Structured behavior objects enriched with MITRE ATT&CK mappings, entity roles, and natural language explanations.

## What are the capabilities of the UEBA behaviors layer?

The UEBA behaviors layer provides these key capabilities:

- **Behavior aggregation:** Automatically groups and sequences related security events across multiple data sources. Instead of analysts manually correlating raw logs, the behaviors layer creates unified behavior objects that present "what happened" in a structured way.
- **Contextualization:** Each behavior is enriched with security context, including mapping to MITRE ATT&CK tactics and techniques. This helps analysts understand the intent behind an activity - for example, lateral movement, privilege escalation - without needing deep familiarity with every log format.
- **Explainability:** Generates natural language summaries of behaviors, making investigations faster and more accessible. Analysts can quickly see what happened and why it matters.

## What is the intended use of the UEBA behaviors layer?

The intended use is to accelerate threat detection and investigation by providing SOC analysts with a unified, AI-driven view of behaviors. It supports:

- Threat hunting
- Detection rule authoring at using large language models (LLMs)
- Incident investigation and triage

## How was the UEBA behaviors layer evaluated? What metrics are used to measure performance?

Our AI mechanisms generate behavior rules based on samples logs. The behavior rules use aggregation and sequencing of raw logs to reflect the intent and action behind those logs. The rules also provide the security context by mapping the behaviors to MITRE ATT&CK tactics and techniques, so that if the behavior was ill intended, you can understand the security context of that potential attack.

The AI-generated rules are then validated in various ways to ensure that:

- The intent, action, and entities are accurately captured and explained.
- The volume of the behaviors this rule generates is above a defined threshold to provide the most value.
- Sensitive data is protected.

## What are the limitations of the UEBA behaviors layer? How can users minimize the impact?

- **Limited data source coverage:** Currently supports CommonSecurityLogs and AWSCloudTrail.
- **Dependence on log quality:** Incomplete or noisy logs can reduce accuracy.
- **Preview feature:** Behavior schema and AI models might evolve.**Mitigation:** Ensure high-quality log ingestion, validate AI-generated queries, and use human review for critical detections.

## What operational factors and settings allow for effective and responsible use of the feature?

- **Enable supported connectors** for AWS and CommonSecurityLog sources.
- **Review AI-generated outputs** before deploying detection rules.
- **Monitor updates** as the feature expands to new sources and schemas.