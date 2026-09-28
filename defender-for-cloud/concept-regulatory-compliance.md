---
layout: Conceptual
title: The Microsoft cloud security benchmark in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/concept-regulatory-compliance
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
description: Learn about the Microsoft cloud security benchmark in Microsoft Defender for Cloud.
ms.topic: concept-article
ms.date: 2025-10-29T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 96561f96-fb39-d8a6-0a54-2d7964458502
document_version_independent_id: 31da62fb-e1a5-904e-c7d6-fb2f4cf420a3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/concept-regulatory-compliance.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/concept-regulatory-compliance
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/concept-regulatory-compliance.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 98123404-afa5-6c6c-d745-5735a95fae5b
---

# The Microsoft cloud security benchmark in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud presents industry standards, regulatory standards, and benchmarks as [security standards](security-policy-concept). These standards are assigned to scopes such as Azure subscriptions, AWS accounts, and GCP projects, and are assessed continuously in the [Regulatory compliance dashboard](concept-regulatory-compliance-standards#view-compliance-standards).

When Defender for Cloud is enabled, the [Microsoft Cloud Security Benchmark (MCSB)](/en-us/security/benchmark/azure/introduction) automatically starts assessing resources in scope. This benchmark builds on the cloud security principles defined by the Azure Security Benchmark and applies these principles with detailed technical implementation guidance for Azure, for other cloud providers (such as AWS and GCP), and for other Microsoft clouds.

**MCSB v2 (preview)** is also available and can be enabled from the Regulatory compliance dashboard. This version introduces expanded guidance with additional risk-based controls, expanded Azure Policy mappings, and coverage for emerging workloads such as artificial intelligence (AI).

In addition to MCSB, Defender for Cloud applies additional default benchmarks for AWS and GCP. Learn more about [Default security benchmarks](concept-regulatory-compliance-standards#default-compliance-standards).

[![Image that shows the components that make up the Microsoft cloud security benchmark.](media/concept-regulatory-compliance/microsoft-security-benchmark.png)](media/concept-regulatory-compliance/microsoft-security-benchmark.png#lightbox)

The compliance dashboard provides a dedicated benchmark view to help you monitor resource compliance against benchmark controls. Non-Azure platforms follow the same cloud-neutral security principles as Azure. Each control provides a consistent level of technical implementation guidance across Azure and other cloud resources.

[![Screenshot of a sample regulatory compliance page in Defender for Cloud.](media/concept-regulatory-compliance/compliance-dashboard.png)](media/concept-regulatory-compliance/compliance-dashboard.png#lightbox)

From the compliance dashboard, you're able to manage all of your compliance requirements for your cloud deployments, including automatic, manual, and shared responsibilities.

Note

Shared responsibilities is only compatible with Azure.