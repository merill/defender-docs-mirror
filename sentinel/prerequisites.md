---
layout: Conceptual
title: Prerequisites for deploying Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/prerequisites
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
description: Learn about prerequisites to deploy Microsoft Sentinel.
ms.author: guywild
author: guywi-ms
ms.topic: article
ms.date: 2026-03-06T00:00:00.0000000Z
locale: en-us
document_id: 740e2862-ea0e-ba86-6adc-40e6cd940155
document_version_independent_id: 876b84dc-66fd-ecaf-927e-668d2e7c0fa0
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/prerequisites.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/prerequisites
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/prerequisites.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 8e072db1-a157-fad6-8870-f81c6281bbc0
---

# Prerequisites for deploying Microsoft Sentinel | Microsoft Learn

Before deploying Microsoft Sentinel, make sure that your Azure tenant meets the requirements listed in this article. This article is part of the [Deployment guide for Microsoft Sentinel](deploy-overview).

## Licensing and subscription requirements

| Requirement | Description |
| --- | --- |
| **Licensing, tenant, or individual account** | A [Microsoft Entra ID license and tenant](/en-us/azure/active-directory/develop/quickstart-create-new-tenant), or an [individual account with a valid payment method](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn), are required to access Azure and deploy resources. |
| **Azure subscription** | An [Azure subscription](/en-us/azure/cost-management-billing/manage/create-subscription) is required to track resource creation and billing. |
| **Permissions** | Assign [relevant permissions](/en-us/azure/role-based-access-control/) to your subscription. For new subscriptions, designate an [owner/contributor](/en-us/azure/role-based-access-control/rbac-and-directory-admin-roles). - To maintain the least privileged access, assign roles at resource group level. - For more control over permissions and access, set up custom roles. For more information, see [Role-based access control](/en-us/azure/role-based-access-control/custom-roles) (RBAC).- For extra separation between users and security users, consider [resource-context](resource-context-rbac) or [table-level RBAC](https://techcommunity.microsoft.com/t5/azure-sentinel/table-level-rbac-in-azure-sentinel/ba-p/965043).  For more information about other roles and permissions supported for Microsoft Sentinel, see [Permissions in Microsoft Sentinel](roles). |

## Workspace requirements

A [Log Analytics workspace](/en-us/azure/azure-monitor/logs/quick-create-workspace) is required to house the data that Microsoft Sentinel ingests and analyzes for detections, analytics, and other features. For more information, see [Design a Log Analytics workspace architecture](/en-us/azure/azure-monitor/logs/workspace-design?toc=/azure/sentinel/TOC.json&amp;bc=/azure/sentinel/breadcrumb/toc.json).

The Log Analytics workspace must not have a resource lock applied, and the workspace pricing tier must be pay-as-you-go or a commitment tier. Log Analytics legacy pricing tiers and resource locks aren't supported when enabling Microsoft Sentinel. For more information about pricing tiers, see [Simplified pricing tiers for Microsoft Sentinel](enroll-simplified-pricing-tier#prerequisites).

[Network security perimeters](/en-us/azure/private-link/network-security-perimeter-concepts) aren't supported for Log Analytics workspaces enabled for Microsoft Sentinel. If a network security perimeter is enabled on the workspace, analytic rules are automatically disabled.

### Dedicated resource group (recommended)

To reduce complexity, we recommend a dedicated [resource group](/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal) for your Log Analytics workspace enabled for Microsoft Sentinel. This resource group should only contain the resources that Microsoft Sentinel uses, including the Log Analytics workspace, any playbooks, workbooks, and so on.

A dedicated resource group allows for permissions to be assigned once, at the resource group level, with permissions automatically applied to dependent resources. With a dedicated resource group, access management of Microsoft Sentinel is efficient and less prone to improper permissions. Reducing permission complexity ensures users and service principals have the permissions required to complete actions and makes it easier to keep less privileged roles from accessing inappropriate resources.

Implement extra resource groups to control access by tiers. Use the extra resource groups to house resources only accessible by groups with higher permissions. Use multiple tiers to separate access between resource groups even more granularly.