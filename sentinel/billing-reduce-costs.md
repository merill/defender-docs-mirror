---
layout: Conceptual
title: Reduce costs for Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/billing-reduce-costs
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
description: Learn how to reduce costs for Microsoft Sentinel by using different methods in the Azure portal.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: daniha
ms.custom: subject-cost-optimization
ms.topic: article
ms.date: 2025-06-14T00:00:00.0000000Z
ms.collection: usx-security
locale: en-us
document_id: 07f96d40-a294-8e56-11f5-189e9319d797
document_version_independent_id: 08f7b331-b999-19d7-4568-100a3456407b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/billing-reduce-costs.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/billing-reduce-costs
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/billing-reduce-costs.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 155571a6-451d-1e00-611d-c5ffc42148bc
---

# Reduce costs for Microsoft Sentinel | Microsoft Learn

Costs for Microsoft Sentinel are only a portion of the monthly costs in your Azure bill. Although this article explains how to reduce costs for Microsoft Sentinel, you're billed for all Azure services and resources your Azure subscription uses, including Partner services.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Set or change pricing tier

To optimize for highest savings, monitor your ingestion volume to ensure you have the commitment tier that aligns most closely with your ingestion volume patterns. Consider increasing or decreasing your commitment tier to align with changing data volumes.

You can increase your commitment tier anytime, which restarts the 31-day commitment period. However, to move back to pay-as-you-go or to a lower commitment tier, you must wait until after the 31-day commitment period finishes. Billing for commitment tiers is on a daily basis.

To see your current Microsoft Sentinel pricing tier, select **Settings** in the Microsoft Sentinel left navigation, and then select the **Pricing** tab. Your current pricing tier is marked **Current tier**.

To change your pricing tier commitment, select one of the other tiers on the pricing page, and then select **Apply**. You must have **Contributor** or **Owner** for the Microsoft Sentinel workspace to change the pricing tier.

[![Screenshot of pricing page in Microsoft Sentinel settings, with pay-as-you-go selected as current pricing tier.](media/billing-reduce-costs/simplified-pricing-tier.png)](media/billing-reduce-costs/simplified-pricing-tier.png#lightbox)

To learn more about how to monitor your costs, see [Manage and monitor costs for Microsoft Sentinel](billing-monitor-costs).

For workspaces still using classic pricing tiers, the Microsoft Sentinel pricing tiers don't include Log Analytics charges. For more information, see [Understand the full billing model for Microsoft Sentinel](billing#understand-the-full-billing-model-for-microsoft-sentinel).

## Buy a pre-purchase plan

Save on your Microsoft Sentinel analytics tier costs when you pre-purchase Microsoft Sentinel commit units (CUs). Use the pre-purchased CUs at any time during the one year purchase term.

Any eligible Microsoft Sentinel costs deduct first from the pre-purchased CUs automatically. You don't need to redeploy or assign a pre-purchased plan to your Microsoft Sentinel workspaces for the CU usage to get the pre-purchase discounts.

For more information, see [Optimize Microsoft Sentinel costs with a pre-purchase plan](billing-pre-purchase-plan).

## Separate non-security data in a different workspace

Microsoft Sentinel analyzes all the data ingested into Microsoft Sentinel-enabled Log Analytics workspaces. It's best to have a separate workspace for non-security operations data, to ensure it doesn't incur Microsoft Sentinel costs.

## Use the Microsoft Sentinel data lake for lower fidelity or secondary security data

While the analytics tier is most appropriate for continuous, real-time threat detection, the Microsoft Sentinel data lake is well-suited for query and analytics of secondary security data that is not needed for real time threat detection. Microsoft Sentinel data lake offers ingestion and storage at a significantly reduced cost. For more information, see [Microsoft Sentinel Pricing](https://azure.microsoft.com/pricing/details/microsoft-sentinel/).

## Optimize Log Analytics costs with dedicated clusters

If you ingest at least 100 GB into your Microsoft Sentinel workspace or workspaces in the same region, consider moving to a Log Analytics dedicated cluster to decrease costs. A Log Analytics dedicated cluster commitment tier aggregates data volume across workspaces that collectively ingest a total of 100 GB or more. For more information, see [Simplified pricing tier for dedicated cluster](enroll-simplified-pricing-tier#simplified-pricing-tiers-for-dedicated-clusters).

You can add multiple Microsoft Sentinel workspaces to a Log Analytics dedicated cluster. There are a couple of advantages to using a Log Analytics dedicated cluster for Microsoft Sentinel:

- Cross-workspace queries run faster if all the workspaces involved in the query are in the dedicated cluster. It's still best to have as few workspaces as possible in your environment, and a dedicated cluster still retains the [100 workspace limit](/en-us/azure/azure-monitor/logs/cross-workspace-query) for inclusion in a single cross-workspace query.
- All workspaces in the dedicated cluster can share the Log Analytics commitment tier set on the cluster. Not having to commit to separate Log Analytics commitment tiers for each workspace can allow for cost savings and efficiencies. By enabling a dedicated cluster, you commit to a minimum Log Analytics commitment tier of 100-GB ingestion per day.

Here are some other considerations for moving to a dedicated cluster for cost optimization:

- The maximum number of clusters per region and subscription is two.
- All workspaces linked to a cluster must be in the same region.
- The maximum of workspaces linked to a cluster is 1000.
- You can unlink a linked workspace from your cluster. The number of link operations on a particular workspace is limited to two in a period of 30 days.
- You can't move an existing workspace to a customer managed key (CMK) cluster. You must create the workspace in the cluster.
- Moving a cluster to another resource group or subscription isn't currently supported.
- A workspace link to a cluster fails if the workspace is linked to another cluster.

For more information about dedicated clusters, see [Log Analytics dedicated clusters](/en-us/azure/azure-monitor/logs/cost-logs#dedicated-clusters).

## Reduce data retention costs with total retention

Microsoft Sentinel retains analytics tier data by default for the first 90 days in analytics retention. As data ages, it loses its value for real-time analytics and investigation. Security operations center (SOC) users might not access older data as frequently but still want to access the data for wider historical investigations or audit purposes. To help you reduce Microsoft Sentinel data retention costs, total retention is available. Data that ages out of its analytics retention state can still be retained, at a much-reduced cost, and accessed using data lake exploration capabilities. For more information, see [Lake exploration, KQL queries](datalake/kql-overview).

Use **Data management &gt; Tables** to adjust the Analytics and Total retention period.

## Use data collection rules for your Windows Security Events

The [Windows Security Events connector](connect-windows-security-events?tabs=LAA) enables you to stream security events from any computer running Windows Server that's connected to your Microsoft Sentinel workspace, including physical, virtual, or on-premises servers, or in any cloud. This connector includes support for the Azure Monitor Agent, which uses data collection rules to define the data to collect from each agent.

Data collection rules enable you to manage collection settings at scale, while still allowing unique, scoped configurations for subsets of machines. For more information, see [Configure data collection for the Azure Monitor Agent](/en-us/azure/azure-monitor/agents/azure-monitor-agent-data-collection).

Besides for the predefined sets of events that you can select to ingest, such as All events, Minimal, or Common, data collection rules enable you to build custom filters and select specific events to ingest. The Azure Monitor Agent uses these rules to filter the data at the source, and then ingest only the events you selected, while leaving everything else behind. Selecting specific events to ingest can help you optimize your costs and save more.