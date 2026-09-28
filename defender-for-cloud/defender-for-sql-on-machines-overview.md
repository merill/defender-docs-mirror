---
layout: Conceptual
title: Microsoft Defender for SQL Servers on Machines overview - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-sql-on-machines-overview
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
description: Protect infrastructure as a service (IaaS) SQL servers across Azure, multicloud, and on-premises environments with vulnerability assessment and threat protection.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 40c1b0ea-9304-664f-47f1-57132a5a688a
document_version_independent_id: 0f02024d-6fb0-9e51-2697-c9d88279971f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-sql-on-machines-overview.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-sql-on-machines-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-sql-on-machines-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: c8d2a2cf-ff2b-c868-7a64-6aba2e7d1fd4
---

# Microsoft Defender for SQL Servers on Machines overview - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for SQL Servers on Machines helps you secure SQL workloads that run across Azure, multicloud, and on-premises environments.

## Microsoft Defender for SQL Servers on Machines plan

The Defender for SQL on Machines plan in Microsoft Defender for Cloud protects your infrastructure as a service (IaaS) SQL Servers hosted on virtual machines (VMs) in Azure, multicloud, and on-premises environments.

- To use the plan, onboard on-premises SQL servers to Defender for Cloud as Azure Arc VMs. Learn more about [SQL Server enabled by Azure Arc](/en-us/sql/sql-server/azure-arc/overview) and [SQL Server on Virtual Machines](https://azure.microsoft.com/services/virtual-machines/sql-server/).
- For multicloud SQL Server machines, connect Defender for Cloud by using the [AWS onboarding quickstart](quickstart-onboard-aws) and [GCP onboarding quickstart](quickstart-onboard-gcp).

Defender for SQL Servers on Machines identifies and mitigates potential database vulnerabilities, and detects anomalous activities that could indicate threats to your databases.

- **Vulnerability assessment**: Defender for Cloud uses vulnerability assessment to discover, track, and assist you in the remediation of potential database vulnerabilities. Assessment scans provide an overview of your SQL machines' security state and provide details of any security findings.
- **Threat protection**: Defender for Cloud generates alerts when it detects suspicious database activities, potentially harmful attempts to access or exploit SQL machines, SQL injection attacks, anomalous database access, and unusual query patterns. [Review SQL alerts](alerts-sql-database-and-azure-synapse-analytics).