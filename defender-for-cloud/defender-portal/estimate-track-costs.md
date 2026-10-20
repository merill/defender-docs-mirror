---
layout: Conceptual
title: Estimate and track cost with new Cloud security billing model in Defender portal - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-portal/estimate-track-costs
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
description: Estimate and track costs for Defender for Cloud in the Defender portal.
ms.topic: how-to
ms.date: 2026-07-28T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 8e29b514-bd40-c35e-4b23-721511ea3a0b
document_version_independent_id: 7eae2911-2972-2250-fa3b-47398ec7a07b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-portal/estimate-track-costs.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: ../toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-portal/estimate-track-costs
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-portal/estimate-track-costs.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: d58f0315-ed71-0ab7-fab8-59683fc12dd5
---

# Estimate and track cost with new Cloud security billing model in Defender portal - Microsoft Defender for Cloud | Microsoft Learn

Important

This feature is in preview. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Defender Workload Units (DWUs) provide a unified model for estimating Microsoft Defender for Cloud costs. Use the Cloud Security Cost Estimator before enabling protection, and use the Cloud security cost report to review actual costs over time.

## Defender Workload Units

A Defender Workload Unit represents cloud security usage across supported workload types. Each protected workload contributes to DWU usage according to its type and counting model.

The same underlying model is used for:

- Cost estimation
- Cost reporting
- Billing

The DWU model replaces separate billing signals with one unit that can be reviewed across workloads and environments. For current pricing and workload mappings, see [Microsoft Defender for Cloud pricing](https://azure.microsoft.com/pricing/details/defender-for-cloud/).

As part of the new model:

- Defender for Containers is measured by protected node instead of vCPU.
- Defender for Key Vault, Defender for Storage, and Defender for Resource Manager use per-resource measurement instead of transactional measurement.
- Defender for Azure SQL Databases, Defender for SQL Servers on Machines, and Defender for Open-Source Relational Databases are consolidated into one Defender for Databases plan.
- Defender for APIs uses a unified plan instead of multiple separate plans.
- Defender for DNS will no longer be offered as a standalone plan. Defender for Servers Plan 2 customers gain access to Defender for DNS value as part of Defender for Servers Plan 2 at no extra cost.

## Estimate cloud security costs

Use the Cloud Security Cost Estimator to estimate DWU usage and projected monthly costs before moving environments to the new model.

1. Open the [Cloud Security Cost Estimator](https://www.microsoft.com/security/business/cloud-security/cost-estimator).
2. Sign in if prompted.
3. Review the supported workload categories and their DWU mappings.
4. Enter the number of resources you want to protect for one or more workloads.
5. Review the calculated DWUs and estimated monthly cost for each workload.
6. Review the total DWUs and estimated monthly cost.
7. Adjust the resource quantities to compare different coverage scenarios.

The estimate updates automatically when you change a workload quantity.

## Track cloud security cost

After you move subscriptions to DWU-based billing, use the Cloud security cost report to review costs.

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. In the navigation pane, select **Cost & usage**.

The Cloud security cost page shows the total USD cost for the selected time period in the upper-right corner of the **Spending overview** chart.

## Analyze cloud security costs

Use **Group by** and **Add filter** at the top of the **Cost analysis** chart to review costs by:

- Meter name
- Billing subscription name
- Product name

Hover over the cost graph to review spending in USD. Use the toggle in the upper-right corner of the **Cost analysis** chart to switch between daily and cumulative spending.

Note

Cloud security costs can fluctuate from day to day even when there are no changes to the connected environments or their resources.