---
layout: Conceptual
title: Detection lifecycle management recommendations for Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/detection-lifecycle-management-recommendations
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
description: Learn how to choose the right capability for managing detections and other content types in Microsoft Sentinel.
author: mberdugo
ms.author: monaberdugo
ms.topic: concept-article
ms.date: 2026-08-07T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
ms.collection: usx-security
locale: en-us
document_id: 9a788f63-9b23-1915-603a-a5226b67fc15
document_version_independent_id: 4d941c27-99d1-09e3-728c-4b419719e865
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/detection-lifecycle-management-recommendations.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/detection-lifecycle-management-recommendations
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/detection-lifecycle-management-recommendations.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 6f878bd0-b28e-60a7-e8ba-3734b33054fb
---

# Detection lifecycle management recommendations for Microsoft Sentinel | Microsoft Learn

Choose a Microsoft Sentinel capability for managing detections and other content based on your organization's scale, complexity, and tooling preferences.

## Choose your capability

The following table summarizes the recommended capability based on your customer type and needs. There are three possible setups, see the table and explanations to choose the right fit.

| Customer type | Scalable, structured change management | Simple UI, low complexity | Custom/external tooling or high automation |
| --- | --- | --- | --- |
| Single tenant | Content as code (repositories) | Portal | APIs / [Terraform](https://techcommunity.microsoft.com/blog/azureinfrastructureblog/cicd-implementation-for-azure-sentinel-using-terraform/4413220) |
| Multitenant | Content as code (repositories; best for scalability) | Content distribution (via portal) | APIs / [Terraform](https://techcommunity.microsoft.com/blog/azureinfrastructureblog/cicd-implementation-for-azure-sentinel-using-terraform/4413220) |

### Content as code with repositories

For most Microsoft Sentinel customers, we recommend leveraging content as code with repositories. Repositories come with all the right versioning, approvals, workflows, and rollbacks for managing detections.

For multitenant customers, repositories provide a scalable way to manage your setup across multiple tenants.

Repositories are available only to Microsoft Sentinel customers.

For more information, see [Deploy content as code from your repository](ci-cd).

### Portal and content distribution

If content as code is too complex, the portal and content distribution are helpful alternatives.

- The portal lets you create and manage detections directly. You can also deploy out-of-the-box detections from the [content hub](/en-us/azure/sentinel/sentinel-solutions-deploy).
- For multitenant customers, content distribution can help manage content across multiple workspaces or tenants.

This is a good option for XDR-only customers who don't have access to repositories.

For more information, see [Content distribution in multitenant management](/en-us/defender-xdr/mto-distribution-profiles?toc=/azure/sentinel/TOC.json&amp;bc=/azure/sentinel/breadcrumb/toc.json).

### APIs

If you use external tools, custom pipelines, or other forms of managing content, APIs are the right solution — especially if you don't use the portal and need more flexibility.

For more information, see [Microsoft Sentinel REST API](/en-us/rest/api/securityinsights/).

## Capabilities feature coverage

The following table shows the feature coverage for each capability.

| Capabilities (for content) | Portal | Content distribution | Repositories | Content Hub | APIs | Terraform |
| --- | --- | --- | --- | --- | --- | --- |
| Create/edit | Yes | Yes | Yes | Yes | Yes | Yes |
| Delete | Yes | Yes | Yes | Yes | Yes | Yes |
| List/inventory | Yes | Yes | No | Yes | Yes | No |
| Change history | Yes | No | Yes | Yes | No | Yes |
| Rollbacks | No | No | Yes | No | No | Yes |
| Approvals | No | No | Yes | No | No | Yes |
| Automatic sync | No | No | Yes | No | No | Yes |
| Drift prevention | No | No | No | No | No | No |
| Drift visibility | No | No | No | Yes | No | No |

## Capabilities content coverage

The following table shows the content types supported by each capability.

| Content type | Portal | Content distribution | Repositories | Content Hub | APIs | Terraform |
| --- | --- | --- | --- | --- | --- | --- |
| Custom detection rules | Yes | Yes | Yes (Preview) | No | Yes | No |
| Analytics rules | Yes | Yes | Yes | Yes | Yes | Yes |
| Playbooks | Yes | Yes | Yes | Yes | Yes | Yes |
| Workbooks | Yes | Yes | Yes | Yes | Yes | Yes |
| Automation rules | Yes | Yes | Yes | Yes | Yes | Yes |
| Parsers | Yes | No | Yes | Yes | Yes | Yes |
| Connectors | Yes | No | No | Yes | Yes | Yes |
| Hunting queries | Yes | No | Yes | Yes | Yes | Yes |
| Watchlists | Yes | No | No | Yes | Yes | Yes |
| Summary rules | Yes | No | No | Yes | Yes | Yes |
| Notebooks | Yes | No | No | No | Yes | No |
| Endpoint security policies | Yes | Yes | No | No | No | No |
| Defender settings | Yes | No | No | No | No | No |
| URBAC roles | Yes | No | No | No | Yes | No |
| Agents | Yes | No | No | No | No | No |
| Unified connectors | Yes | No | No | No | No | No |