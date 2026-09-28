---
layout: Conceptual
title: Determine Business Needs for Multicloud Security Planning - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/plan-multicloud-security-determine-business-needs
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
description: Learn about determining business needs to meet business goals in multicloud environment with Microsoft Defender for Cloud.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 0e249230-dcb9-05ea-cd52-31e83320abe6
document_version_independent_id: a27cf828-4b60-199e-08b7-df4cf34ad807
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/plan-multicloud-security-determine-business-needs.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/plan-multicloud-security-determine-business-needs
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/plan-multicloud-security-determine-business-needs.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 0240024e-6569-e4a0-4bfe-fda23323de38
---

# Determine Business Needs for Multicloud Security Planning - Microsoft Defender for Cloud | Microsoft Learn

## Identify business requirements for multicloud security

Use this guidance to design a cloud security posture management (CSPM) and cloud workload protection platform (CWPP) solution for multicloud resources with Microsoft Defender for Cloud. Identify your organization's business needs for multicloud security, assess key requirements, and map those needs to Defender for Cloud capabilities for protecting Amazon Web Services (AWS) and Google Cloud Platform (GCP) resources.

## Business planning goals

Identify how Defender for Cloud multicloud capabilities can help your organization meet business goals and protect Amazon Web Services (AWS) and Google Cloud Platform (GCP) resources.

## Start assessing business needs

The first step in designing a multicloud security solution is to determine your business needs. Every company, even in the same industry, has different requirements. Best practices provide general guidance, but your business needs define your requirements.

As you start defining requirements, answer these questions:

- Does your company need to assess and strengthen the security configuration of its cloud resources?
- Does your company want to manage the security posture of multicloud resources from a single point or *single pane of glass*?
- What boundaries do you want to put in place to ensure that your entire organization is covered, and no areas are missed?
- Does your company need to comply with industry and regulatory standards? If so, which standards?
- What are your goals for protecting critical workloads, including containers and servers, against malicious attacks?
- Do you need a solution only in a specific cloud environment, or a cross-cloud solution?
- How will the company respond to alerts and recommendations, and remediate non-compliant resources?
- Will workload owners be expected to remediate issues?

## Map Defender for Cloud to business requirements

Defender for Cloud provides a single management point for protecting Azure, on-premises, and multicloud resources. Defender for Cloud can meet your business requirements by:

- Securing and protecting your GCP, AWS, and Azure environments.
- Assessing and strengthening the security configuration of your cloud workloads.
- Managing compliance against critical industry and regulatory standards.
- Providing vulnerability management solutions for servers and containers.
- Protecting critical workloads, including containers, servers, and databases, against malicious attacks.

The following diagram shows the Defender for Cloud architecture. Defender for Cloud can:

- Provide unified visibility and recommendations across multicloud environments. There's no need to switch between different portals to see the status of your resources.
- Compare your resource configuration against industry standards, regulations, and benchmarks. For more information, see [Assign regulatory compliance standards](assign-regulatory-compliance-standards).
- Help security analysts to triage alerts based on threats and suspicious activities. Apply workload protection capabilities to critical workloads for threat detection and advanced defenses.

[![Diagram that shows multicloud architecture.](media/planning-multicloud-security/architecture.png)](media/planning-multicloud-security/architecture.png#lightbox)