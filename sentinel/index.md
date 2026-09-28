---
layout: Landing
title: Microsoft Sentinel documentation | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/
summary: Microsoft Sentinel provides attack detection, threat visibility, proactive hunting, and threat response to help you stop threats before they cause harm.
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
description: Microsoft Sentinel provides attack detection, threat visibility, proactive hunting, and threat response to help you stop threats before they cause harm.
ms.topic: landing-page
author: guywi-ms
ms.author: guywild
ms.date: 2025-01-03T00:00:00.0000000Z
locale: en-us
document_id: 3bfc9058-5207-8371-75e8-34bc992e897c
document_version_independent_id: bc538b94-01fd-56a3-3a58-b8fa6499990e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/index.yml
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: landing
toc_rel: toc.json
asset_id: sentinel/index
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/index.yml
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 4379f1c3-fc4c-ff50-9ab6-9c79239eb36b
---

# Microsoft Sentinel documentation

Microsoft Sentinel provides attack detection, threat visibility, proactive hunting, and threat response to help you stop threats before they cause harm.

## About Microsoft Sentinel

### Overview

- [What is Microsoft Sentinel?](overview)
- [Best practices](best-practices)

### What's new

- [What's new in Microsoft Sentinel?](whats-new)

## Get started

### Quickstart

- [Onboard Microsoft Sentinel](quickstart-onboard)

### Deploy

- [Deployment guide](deploy-overview)
- [Prerequisites](prerequisites)
- [Plan costs](billing)
- [Find solutions](sentinel-solutions-catalog)

### How-To Guide

- [Install solutions and content](sentinel-solutions-deploy)

## Microsoft Sentinel data lake

### Overview

- [What is Microsoft Sentinel data lake](datalake/sentinel-lake-overview)

### Deploy

- [Onboarding to Microsoft Sentinel data lake](datalake/sentinel-lake-onboarding)
- [Set up connectors for the Microsoft Sentinel data lake](datalake/sentinel-lake-connectors)

### Concept

- [KQL and Microsoft Sentinel data lake](datalake/kql-overview)
- [Notebooks and Microsoft Sentinel data lake](datalake/notebooks-overview)

### How-To Guide

- [Run KQL queries](datalake/kql-queries)
- [Running notebooks](datalake/notebooks)

## Unified security operations

### Overview

- [What are unified security operations?](/en-us/defender-xdr/isoc-overview)
- [Microsoft Defender portal overview](/en-us/defender-xdr/microsoft-365-defender-portal)
- [Microsoft Sentinel in the Microsoft Defender portal](microsoft-sentinel-defender-portal)

### Deploy

- [Plan for unified security operations](/en-us/defender-xdr/isoc-overview)
- [Deploy unified security operations](/en-us/defender-xdr/onboard-isoc-workspace)

### How-To Guide

- [Connect Microsoft Sentinel to the Microsoft Defender portal](/en-us/azure/sentinel/microsoft-sentinel-onboard)

## Collect data

### Concept

- [Microsoft Sentinel data connectors](connect-data-sources)
- [Data collection best practices](best-practices-data)
- [Normalizing and parsing data](normalization)

### Tutorial

- [Forward Syslog data to Log Analytics workspace](forward-syslog-monitor-agent)

### How-To Guide

- [Create a custom connector](create-custom-connector)
- [Monitor connector health](monitor-data-connector-health)

### Reference

- [Find data connectors](data-connectors-reference)

## Detect threats

### Concept

- [Understand threat intelligence](understand-threat-intelligence)
- [MITRE ATT&CK® framework](mitre-coverage)
- [User and entity behavior analytics (UEBA)](identify-threats-with-entity-behavior-analytics)
- [Customizable anomalies](soc-ml-anomalies)

### Tutorial

- [Detect threats by using analytics rules](tutorial-log4j-detection)

### How-To Guide

- [Detect threats by using built-in analytics](detect-threats-built-in)
- [Create custom detection rules](detect-threats-custom)

## Investigate and respond

### Concept

- [Incident investigation and case management](incident-investigation)
- [Threat hunting](hunting)
- [Kusto Query Language overview](/en-us/kusto/query/?toc=/azure/sentinel/TOC.json&amp;bc=/azure/sentinel/breadcrumb/toc.json)
- [Automation rules](automate-incident-handling-with-automation-rules)
- [Playbooks](automate-responses-with-playbooks)

### Tutorial

- [Investigate with UEBA](investigate-with-ueba)
- [Respond automatically to threats](tutorial-respond-threats-playbook)

### How-To Guide

- [Investigate incidents](investigate-incidents)
- [Manage incident workflow with tasks](work-with-tasks)
- [Monitor your data](monitor-your-data)
- [Conduct end-to-end threat hunting](hunts)