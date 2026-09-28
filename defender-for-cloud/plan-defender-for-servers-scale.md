---
layout: Conceptual
title: Scale a Defender for Servers deployment - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/plan-defender-for-servers-scale
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
description: Scale protection of Azure, AWS, GCP, and on-premises servers by using Microsoft Defender for Servers.
ms.topic: concept-article
ms.date: 2026-04-19T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 7cf5e9f0-399f-4b52-ea71-d589b845e329
document_version_independent_id: fcca5950-0d2f-b6b1-a680-40364f29aa81
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/plan-defender-for-servers-scale.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/plan-defender-for-servers-scale
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/plan-defender-for-servers-scale.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 1b33ab40-31c5-954d-2cfc-c3ca7d59d46c
---

# Scale a Defender for Servers deployment - Microsoft Defender for Cloud | Microsoft Learn

This article helps you scale your Microsoft Defender for Servers deployment.

Defender for Servers is one of the paid plans provided by [Microsoft Defender for Cloud](defender-for-cloud-introduction).

## Before you begin

This article is the *sixth* and final article in the Defender for Servers planning guide series. Before you begin, review the earlier articles: Before you begin, review the earlier articles:

1. Start [planning your deployment](plan-defender-for-servers).
2. Review [Defender for Servers access roles](plan-defender-for-servers-roles).
3. Select a [Defender for Servers plan](plan-defender-for-servers-select-plan)
4. Understand how [Defender for Servers collects data for assessment and when you need a workspace](plan-defender-for-servers-agents).
5. Understand where [Defender for Servers stores data](plan-defender-for-servers-data-workspace).

## Enable overview

When you enable a Defender for Cloud subscription, this process occurs:

1. The *microsoft.security* resource provider is automatically registered on the subscription.
2. At the same time, the Cloud Security Benchmark initiative that's responsible for creating security recommendations and calculating the secure score is assigned to the subscription.
3. After you enable Defender for Cloud on the subscription, you turn on Defender for Servers Plan 1 or Defender for Servers Plan 2.

In the next sections, review considerations for specific steps as you scale your deployment:

- Scale a Microsoft Cloud Security Benchmark deployment
- Scale a Defender for Servers plan

## Scale a MCSB deployment

Defender for Cloud assesses and enforces best-practice security configurations using [built-in Azure policy initiatives](policy-reference). The [Microsoft Cloud Security Benchmark (MCSB)](/en-us/security/benchmark/azure/introduction) is Defender for Cloud's default initiative.

In a scaled deployment, you might want the MCSB to be automatically assigned.

The assignment is inherited for every existing and future subscription in the management group. To set up your deployment to automatically apply the benchmark, assign the policy initiative to your management group (root) instead of to each subscription.

You can get the *Microsoft Cloud Security Benchmark* policy definition on [GitHub](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policySetDefinitions/Security%20Center/AzureSecurityCenter.json).

[Learn more](onboard-management-group) about using a built-in policy definition to register a resource provider.

## Scale a Defender for Servers plan

You can use a policy definition to enable Defender for Servers at scale:

- To get the built-in *Configure Azure Defender for Servers to be enabled* policy definition, in the Azure portal for your deployment, go to **Azure Policy** &gt; **Policy Definitions**.

    [![Screenshot that shows the Configure Azure Defender for Servers to be enabled policy definition.](media/plan-defender-for-servers-scale/select-policy-definition.png)](media/plan-defender-for-servers-scale/select-policy-definition.png#lightbox)
- Alternatively, you can use a [custom policy](https://github.com/Azure/Microsoft-Defender-for-Cloud/tree/main/Policy/Enable%20Defender%20for%20Servers%20plans) to enable Defender for Servers and select the plan at the same time.
- You can enable only one Defender for Servers plan on each subscription. You can't enable both Defender for Servers Plan 1 and Plan 2 at the same subscription.
- If you want to use both plans in your environment, divide your subscriptions into two management groups. On each management group, assign a policy to enable the respective plan on each underlying subscription.