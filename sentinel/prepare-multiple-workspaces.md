---
layout: Conceptual
title: Prepare for multiple workspaces and tenants in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/prepare-multiple-workspaces
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
description: To prepare for your deployment, learn how Microsoft Sentinel can extend across multiple workspaces and tenants.
author: EdB-MSFT
ms.topic: concept-article
ms.date: 2025-07-16T00:00:00.0000000Z
ms.author: edbaynash
locale: en-us
document_id: be7e059c-bb0f-d4b6-baf2-7c36d933a285
document_version_independent_id: 06376a94-f2b9-8970-514c-2a2b1cfcb804
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/prepare-multiple-workspaces.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/prepare-multiple-workspaces
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/prepare-multiple-workspaces.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 6fac0412-6a91-4c2e-8d7a-6b420729e1df
---

# Prepare for multiple workspaces and tenants in Microsoft Sentinel | Microsoft Learn

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

To prepare for your deployment, you need to determine whether a multiple workspace architecture is relevant for your environment. In this article, you learn how Microsoft Sentinel can extend across multiple workspaces and tenants so you can determine whether this capability suits your organization's needs. This article is part of the [Deployment guide for Microsoft Sentinel](deploy-overview).

Use one of the following sets of setup instructions, depending on which portal you're using to extend Microsoft Sentinel across workspaces:

| Portal | References |
| --- | --- |
| Microsoft Defender portal | - [Multiple Microsoft Sentinel workspaces in the Defender portal](/en-us/azure/sentinel/workspaces-defender-portal)- [Microsoft Defender multitenant management](/en-us/defender-xdr/mto-overview) |
| Azure portal | - [Extend Microsoft Sentinel across workspaces and tenants](extend-sentinel-across-workspaces-tenants)- [Centrally manage multiple Log Analytics workspaces enabled for Microsoft Sentinel with workspace manager](workspace-manager) |

## The need to use multiple workspaces

When you onboard Microsoft Sentinel, your first step is to select your Log Analytics workspace. While you can get the full benefit of the Microsoft Sentinel experience with a single workspace, in some cases, you might want to extend your workspace to query and analyze your data across workspaces and tenants.

This table lists some of these scenarios and, when possible, suggests how you might use a single workspace for the scenario.

| Requirement | Description | Ways to reduce workspace count |
| --- | --- | --- |
| **Sovereignty and regulatory compliance** | A workspace is tied to a specific region. To keep data in different [Azure geographies](https://azure.microsoft.com/global-infrastructure/geographies/) to satisfy regulatory requirements, split up the data into separate workspaces. In Microsoft Sentinel, data is mostly stored and processed in the same geography or region, with some exceptions, such as when using detection rules that leverage Microsoft's Machine learning. In such cases, data might be copied outside your workspace geography for processing. |  |
| **Data ownership** | The boundaries of data ownership, for example by subsidiaries or affiliated companies, are better delineated using separate workspaces. |  |
| **Multiple Azure tenants** | Microsoft Sentinel supports data collection from Microsoft and Azure SaaS resources only within its own Microsoft Entra tenant boundary. Therefore, each Microsoft Entra tenant requires a separate workspace. |  |
| **Granular data access control** | An organization might need to allow different groups, within or outside the organization, to access some of the data collected by Microsoft Sentinel. For example:<br>- Resource owners' access to data pertaining to their resources<br>- Regional or subsidiary SOCs' access to data relevant to their parts of the organization | Use [resource Azure RBAC](resource-context-rbac) or [table level Azure RBAC](https://techcommunity.microsoft.com/t5/azure-sentinel/table-level-rbac-in-azure-sentinel/ba-p/965043) |
| **Granular retention settings** | Historically, multiple workspaces were the only way to set different retention periods for different data types. This is no longer needed in many cases, thanks to the introduction of table level retention settings. | Use [table level retention settings](https://techcommunity.microsoft.com/t5/azure-sentinel/new-per-data-type-retention-is-now-available-for-azure-sentinel/ba-p/917316) or automate [data deletion](/en-us/azure/azure-monitor/logs/personal-data-mgmt#exporting-and-deleting-personal-data) |
| **Split billing** | By placing workspaces in separate subscriptions, they can be billed to different parties. | Usage reporting and cross-charging |
| **Legacy architecture** | The use of multiple workspaces might stem from a historical design that took into consideration limitations or best practices which don't hold true anymore. It might also be an arbitrary design choice that can be modified to better accommodate Microsoft Sentinel.Examples include:<br>- Using a per-subscription default workspace when deploying Microsoft Defender for Cloud<br>- The need for granular access control or retention settings, the solutions for which are relatively new | Re-architect workspaces |

When determining how many tenants and workspaces to use, consider that most Microsoft Sentinel features operate by using a single workspace or Microsoft Sentinel instance, and Microsoft Sentinel ingests all logs housed within the workspace.

### Managed Security Service Provider (MSSP)

In case of an MSSP, many if not all of the above requirements apply, making multiple workspaces, across tenants, the best practice. Specifically, we recommend that you create at least one workspace for each Microsoft Entra tenant to support built-in, [service to service data connectors](connect-data-sources#service-to-service-integration-for-data-connectors) that work only within their own Microsoft Entra tenant.

- Connectors that are based on diagnostics settings can't be connected to a workspace that isn't located in the same tenant where the resource resides. This applies to connectors such as [Azure Firewall](data-connectors-reference#azure-firewall), [Azure Storage](data-connectors-reference#azure-storage-account), [Azure Activity](data-connectors-reference#azure-activity) or [Microsoft Entra ID](connect-azure-active-directory).
- [Partner data connectors](data-connectors-reference) are often based on API or agent collections, and therefore are not attached to a specific Microsoft Entra tenant.

Use [Azure Lighthouse](/en-us/azure/lighthouse/how-to/onboard-customer) to help manage multiple Microsoft Sentinel instances in different tenants.

## Microsoft Sentinel multiple workspace architecture

As implied by the requirements above, there are cases where a single SOC needs to centrally manage and monitor multiple Log Analytics workspaces enabled for Microsoft Sentinel, potentially across Microsoft Entra tenants.

- An MSSP Microsoft Sentinel Service.
- A global SOC serving multiple subsidiaries, each having its own local SOC.
- A SOC monitoring multiple Microsoft Entra tenants within an organization.

To address these cases, Microsoft Sentinel offers multiple-workspace capabilities that enable central monitoring, configuration, and management, providing a single pane of glass across everything covered by the SOC. This diagram shows an example architecture for such use cases.

![Diagram showing extend workspace across multiple tenants: architecture.](media/extend-sentinel-across-workspaces-tenants/cross-workspace-architecture.png)

This model offers significant advantages over a fully centralized model in which all data is copied to a single workspace:

- Flexible role assignment to the global and local SOCs, or to the MSSP its customers.
- Fewer challenges regarding data ownerships, data privacy and regulatory compliance.
- Minimal network latency and charges.
- Easy onboarding and offboarding of new subsidiaries or customers.