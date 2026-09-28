---
layout: Conceptual
title: Understand Defender for Servers data collection in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/plan-defender-for-servers-agents
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
description: Understand how the Defender for Servers plan collects data.
ms.topic: concept-article
ms.date: 2025-02-19T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 9ca98031-cedc-b483-8d3f-f7fbeafbbc89
document_version_independent_id: 1ef67f2c-30ac-c000-dc70-582f0fe4d4e7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/plan-defender-for-servers-agents.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/plan-defender-for-servers-agents
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/plan-defender-for-servers-agents.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: e105aa3f-2c25-f39e-977e-89d723049869
---

# Understand Defender for Servers data collection in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

This article helps you to understand how [Defender for Servers](defender-for-servers-overview) in Microsoft Defender for Cloud collects data for assessment.

## Before you begin

This article is the *fourth* article in the Defender for Servers planning guide. Before you begin, review the earlier articles:

1. Start [planning your deployment](plan-defender-for-servers).
2. Review [Defender for Servers access roles](plan-defender-for-servers-roles).
3. Select a [Defender for Servers plan](plan-defender-for-servers-select-plan)

## Data collection

Defender for Servers uses a number of methods to collect machine information, including [agentless machine scanning](concept-agentless-data-collection) and the [Defender for Endpoint agent](integration-defender-for-endpoint).

| **Feature** | **Data collection method** |
| --- | --- |
| [Assess machines for an EDR solution](detect-endpoint-detection-response-solutions) | Agentless scanning |
| [Assess Defender for Endpoint as an EDR solution](endpoint-detection-response) | Agentless scanning. |
| [Scan software inventory](/en-us/defender-vulnerability-management/tvm-software-inventory) | Agentless scanning. Software inventory is provided by the integration with Defender Vulnerability Management. |
| [Scan for vulnerabilities](auto-deploy-vulnerability-assessment) | Agentless scanningAgent-based scanning with the Defender for Endpoint agent.Bring your own license (BYOL) scanning with a [supported third-party solution](deploy-vulnerability-assessment-byol-vm).[Learn about](auto-deploy-vulnerability-assessment#hybrid-scanning-behavior) hybrid scanning using both agentless and agent-based scanning. |
| [Scan machines for secrets](secrets-scanning-servers) | Agentless scanning. |
| [Scan machines for malware](agentless-malware-scanning) | Agentless scanning.[Next-generation antimalware protection](/en-us/defender-endpoint/next-generation-protection) is also provided by Defender for Endpoint integration, using the Defender for Endpoint agent. |
| [Scan for OS misconfigurations](operating-system-misconfiguration) | Assess OS configuration against compute security baselines in the Microsoft Cloud Security Benchmark using the [Azure Machine Configuration extension](security-baseline-guest-configuration). |
| [Scan for file and registry changes with file integrity monitoring](file-integrity-monitoring-overview) | Defender for Endpoint agent. |
| [Scan for system and patch updates](enable-periodic-system-updates) | Relies on [Azure Update Manager VM extension](/en-us/azure/update-manager/workflow-update-manager). |
| [Use free data ingestion benefit](data-ingestion-benefit) | Azure Monitor agent (AMA). |