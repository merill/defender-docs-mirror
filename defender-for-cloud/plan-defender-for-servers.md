---
layout: Conceptual
title: Plan a Defender for Servers deployment - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/plan-defender-for-servers
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
description: Design a solution to protect on-premises and multicloud servers with Microsoft Defender for Servers.
ms.topic: concept-article
ms.date: 2026-08-07T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
locale: en-us
document_id: 7f4c46df-42d0-b015-eec8-b670bbeb2844
document_version_independent_id: 7559f935-99aa-0e34-db90-03f255c5513c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/plan-defender-for-servers.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/plan-defender-for-servers
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/plan-defender-for-servers.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://authoring-docs-microsoft.poolparty.biz/devrel/beac614b-f66d-40ed-a947-3996de709333
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://authoring-docs-microsoft.poolparty.biz/devrel/9da05372-4706-43ec-a899-f436adab380d
platformId: 3ad6b622-e048-e66d-eca5-5c6187662fdf
---

# Plan a Defender for Servers deployment - Microsoft Defender for Cloud | Microsoft Learn

The Defender for Servers plan in Microsoft Defender for Cloud reduces security risk by providing actionable recommendations to improve and remediate machine security posture. Defender for Servers also helps protect machines against real-time security threats and attacks.

This guide helps you design and plan an effective Defender for Servers deployment.

## About this guide

The intended audience of this guide includes cloud solution and infrastructure architects, security architects and analysts, and anyone involved in protecting cloud and hybrid servers and workloads.

The guide answers these questions:

- What does Defender for Servers do and how is it deployed?
- Where is my data stored and when do I need a Log Analytics workspace?
- How do I control access to Defender for Servers resources?
- Which Defender for Servers plan should I choose, and where should I deploy the plan?
- What agents and extensions are needed in my deployment?
- How do I scale a deployment?

## Before you begin

Before you begin deployment planning:

- Learn more about [Defender for Cloud](defender-for-cloud-introduction) capabilities, and [review pricing details](https://azure.microsoft.com/pricing/details/defender-for-cloud/).
- [Get an overview](defender-for-servers-overview) of Defender for Servers.
- If you're deploying for AWS machines or GCP projects, review the [multicloud planning guide](plan-multicloud-security-get-started).
- Onboarding AWS/GCP and on-premises machines as Azure Arc VMs ensures that you can use all features in Defender for Servers. Before you begin planning, learn more about [Azure Arc](/en-us/azure/azure-arc/overview).

## Deployment steps

The following table summarizes Defender for Servers deployment steps.

| **Step** | **Details** | **Outcome** |
| --- | --- | --- |
| **Connect AWS/GCP machines** | To protect AWS and GCP machines with Defender for Servers, [connect AWS accounts](quickstart-onboard-aws) and [GCP projects](quickstart-onboard-gcp) to Defender for Cloud. You can enable Defender for Cloud plans, including Defender for Servers, as part of the connection process. To take full advantage of Defender for Servers features, we recommend onboarding AWS and GCP machines as Azure Arc VMs. Installation of the Azure Arc agent is available as part of the connection process. | AWS and GCP machines are successfully onboarded to Defender for Cloud. |
| **Connect on-premises machines** | To protect on-premises machines, we recommend [onboarding on-premises machines as Azure Arc VMs](quickstart-onboard-machines). You can [directly onboard on-premises machines to Defender for Cloud](onboard-machines-with-defender-for-endpoint). However, with direct onboarding you won't have full access to Defender for Servers Plan 2 features. | On-premises machines are successfully onboarded to Defender for Cloud |
| **Enable Defender for Servers** | [Deploy a Defender for Servers plan](tutorial-enable-servers-plan). | Defender for Cloud starts protecting supported machines within the deployment scope. |
| **Take advantage of free data ingestion** | To take advantage of 500 MB of free daily ingestion per node for eligible security data, enable Defender for Servers Plan 2 on the Log Analytics workspace to which the machines report. Data must be collected through a supported method, such as Azure Monitor Agent (AMA). Creating a data collection rule alone doesn't enable the benefit. For more information, see [Defender for Servers data ingestion benefit](data-ingestion-benefit). | Free daily ingestion is configured for supported data types. |
| **Prepare for OS assessment** | For Defender for Servers Plan 2 to [assess operation system configuration settings](operating-system-misconfiguration) against compute security baselines in Microsoft Cloud Security Benchmark, machines must be running the Azure Policy machine configuration extension. [Learn more](security-baseline-guest-configuration) about setting up the extension. | Defender for Servers Plan 2 collects OS configuration information for assessment. |
| **Set up file integrity monitoring** | After enabling Defender for Servers Plan 2, you [set up file integrity monitoring after enabling the plan](file-integrity-monitoring-overview). You need a Log Analytics workspace for file integrity monitoring. You can use an existing workspace, or create a new workspace when you configure the feature. | Defender for Servers monitors critical file changes. |