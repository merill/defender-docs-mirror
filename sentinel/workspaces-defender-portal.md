---
layout: Conceptual
title: Multiple workspaces - Microsoft Sentinel in Defender portal | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/workspaces-defender-portal
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
description: Learn about the support of multiple workspaces for Microsoft Sentinel in the Defender portal including primary and secondary workspaces.
author: EdB-MSFT
ms.author: edbaynash
ms.topic: concept-article
ms.date: 2026-06-08T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: bf3c67cc-fc60-57eb-9cc8-930051c8bc0f
document_version_independent_id: 90d86c74-2f0c-8682-55c4-980ab13c9af3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/workspaces-defender-portal.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/workspaces-defender-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/workspaces-defender-portal.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: b921c365-45bf-5ce9-c7b9-56d3f538b30f
---

# Multiple workspaces - Microsoft Sentinel in Defender portal | Microsoft Learn

The Defender portal allows you to connect to one primary workspace and multiple secondary workspaces for Microsoft Sentinel. In the context of this article, a workspace is a Log Analytics workspace with Microsoft Sentinel enabled.

This article primarily applies to the scenario where you onboard Microsoft Sentinel to the Defender portal together with Microsoft Defender XDR for [unified security operations](/en-us/defender-xdr/isoc-overview). If you plan to use Microsoft Sentinel in the Defender portal without Microsoft Defender XDR, you can still manage multiple workspaces. However, since you don't have Defender XDR, your primary workspace won't have Defender XDR data, and you won't have access to Defender XDR features.

## Primary and secondary workspaces

Select your primary workspace when you onboard Microsoft Sentinel to the Defender portal. Any other workspaces that you onboard to the Defender portal are considered as secondary workspaces. The Defender portal supports one primary workspace and an unlimited number of secondary workspaces per tenant for Microsoft Sentinel.

When you also have Microsoft Defender XDR, alerts from your primary workspace are correlated with Defender XDR data, and incidents include alerts from both your primary workspace and Defender XDR in a unified queue. When you select a primary workspace, the [Defender XDR data connector](connect-microsoft-365-defender) for incidents and alerts is connected to the primary workspace only.

In such cases:

| Area | Description |
| --- | --- |
| **Other workspaces previously connected to Defender XDR** | Any other workspaces that were previously connected to the Defender XDR connector are disconnected, and function as secondary workspaces. Any analytics rules and automation that you had previously configured based on Defender XDR data no longer function until you configure table ingestion. |
| **Tenant-based alerts and standalone data connectors** | Alerts from other Microsoft services, including other Defender services, are tenant-based alerts and relate to the entire tenant instead of a specific workspace. To prevent duplication across workspaces, any direct, standalone data connectors for these services must be disconnected from Microsoft Sentinel in secondary workspaces. This results in tenant-based alerts surfacing only in the primary workspace. Upon onboarding, standalone data connectors for Microsoft Defender for Office 365, Microsoft Entra ID Protection, Microsoft Defender for Cloud Apps, Microsoft Defender for Endpoint, and Microsoft Defender for Identity are automatically disconnected. If you have other, standalone Microsoft data connectors with alerts in your workspaces, make sure to disconnect them before onboarding to the Defender portal. |
| **Defender XDR alerts and incidents** | All Defender XDR alerts and incidents are synced to your primary workspace only. However, secondary workspaces can ingest Defender table data if configured in the [Microsoft XDR connector in the Sentinel portal](connect-microsoft-365-defender#connect-to-microsoft-defender-xdr) in Azure, or under **Microsoft Sentinel** &gt; **Configuration** &gt; **Tables** in the Defender portal. |
| **Incident creation and alert correlation** | The Defender portal keeps incident creation and alert correlation separate between the Microsoft Sentinel workspaces. Incidents in secondary workspaces don't include data from any other workspace, or from Defender XDR. |
| **One primary workspace required** | One primary workspace must always be connected to the Defender portal. |

For example, you might be working on a global SOC team in a company that has multiple, autonomous workspaces. In such cases, you might not want to see incidents and alerts from each of these workspaces in your global SOC queue in the Defender portal. Since these workspaces are onboarded to the Defender portal as secondary workspaces, they show in the Defender portal as Microsoft Sentinel only, without Defender incidents and alerts, and continue to function autonomously. When looking at your global SOC workspace, you won't see data from these secondary workspaces.

Where you have multiple Microsoft Sentinel workspaces within a Microsoft Entra ID tenant, consider using the primary workspace for your global security operations center.

## Permissions to manage workspaces and view workspace data

Use one of the following roles or role combinations to manage primary and secondary workspaces:

| Task | Microsoft Entra or Azure built-in role required | Scope |
| --- | --- | --- |
| **Onboard a *primary* Microsoft Sentinel workspace to the Defender portal** | At least a [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator) in Microsoft Entra ID [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) (unconditional role assignment) OR [User Access Administrator](/en-us/azure/role-based-access-control/built-in-roles#user-access-administrator) and [Microsoft Sentinel Contributor](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-contributor) | Tenant- Subscription for Owner role |
| **Connect or disconnect a *secondary* workspace only** | [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) OR [User Access Administrator](/en-us/azure/role-based-access-control/built-in-roles#user-access-administrator) and [Microsoft Sentinel Contributor](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-contributor) | - Subscription for Owner or User Access Administrator roles - Subscription, resource group, or workspace resource for Microsoft Sentinel Contributor |
| **Change the primary workspace** | At least a [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator) in Microsoft Entra ID [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) OR [User Access Administrator](/en-us/azure/role-based-access-control/built-in-roles#user-access-administrator) and [Microsoft Sentinel Contributor](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-contributor) | Tenant- Subscription for Owner or User Access Administrator roles - Subscription, resource group, or workspace resource for Microsoft Sentinel Contributor |
| **Activate or deactivate a Sentinel workspace in Unified RBAC** | At least a [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator) in Microsoft Entra ID [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) OR [User Access Administrator](/en-us/azure/role-based-access-control/built-in-roles#user-access-administrator) and [Microsoft Sentinel Contributor](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-contributor) | Tenant- Subscription for Owner or User Access Administrator roles - Subscription, resource group, or workspace resource for Microsoft Sentinel Contributor |

For onboarding, the [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner) role assignment must be unconditional at the subscription scope.

![Screenshot of Azure Add role assignment conditions showing Owner set to Allow user to assign all roles (highly privileged).](media/workspaces-defender-portal/owner-unconditional-role-assignment.png)

Important

Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization.

After you connect Microsoft Sentinel to the Defender portal, your existing Azure role-based access control (RBAC) permissions allow you to view and work with the Microsoft Sentinel features and workspaces that you have access to.

| Workspace | Access |
| --- | --- |
| **Primary** | If you have access to the primary workspace, you're able to read and manage data from the workspace and Defender XDR. |
| **Secondary** | If you have access to a secondary workspace, you're able to read and manage data from the workspace only. Defender incidents and alerts aren't synchronized with secondary workspaces, but secondary workspaces can still ingest Defender table data. For more information, see Primary and secondary workspaces. |

**Exception:** If you've already onboarded one workspace to the Defender portal, any alerts created by using custom detections on `AlertInfo` and `AlertEvidence` tables before mid January 2025 are visible to all users.

For more information, see [Roles and permissions in Microsoft Sentinel](roles).

## Primary workspace changes

After you onboard Microsoft Sentinel to the Defender portal, you can change the primary workspace. When you switch the primary workspace for Microsoft Sentinel, the Defender XDR connector is connected to the new primary and disconnected from the former one automatically.

Change the primary workspace in the Defender portal by going to **System** &gt; **Settings** &gt; **Microsoft Sentinel** &gt; **Workspaces**.

## Scope of workspace data in different views

If you have the appropriate permissions to view data from primary and secondary workspaces for Microsoft Sentinel, the workspace scope in following table applies for each capability.

| Capability | Workspace scope |
| --- | --- |
| **Search** | The results from the global search at the top of the browser page in the Defender portal provide an aggregated view of all relevant workspace data that you have permissions to view. |
| Investigation & response &gt; Incidents & alerts &gt; **Incidents** | View incidents from different workspaces in a unified queue or filter the view by workspace. |
| Investigation & response &gt; Incidents & alerts &gt; **Alerts** | View alerts from different workspaces in a unified queue or filter the view by workspace. The Defender portal segments alert correlation by workspace. |
| **Entities**: From an incident or alert &gt; select a device, user, or other entity asset | View all relevant entity data from multiple workspaces in a single entity page. Entity pages aggregates alerts, incidents, and timeline events from all workspaces to provide deeper insights into entity behavior. Filter by workspace in **Incidents and alerts**, **Timeline**, and **Insights** tabs. The **Overview** tab displays entity metadata aggregated from all workspaces. |
| Investigation & response &gt; Hunting &gt; **Advanced hunting** | Select a workspace from the top right-hand side of the browser. Or, query across multiple workspaces by using the workspace operator in the query. See [Query multiple workspaces](extend-sentinel-across-workspaces-tenants#query-multiple-workspaces). The query results don't show a workspace name or ID.Access all log data of the workspace, including queries and functions, as read only. For more information, see [Advanced hunting with Microsoft Sentinel data in Microsoft Defender portal](/en-us/defender-xdr/advanced-hunting-microsoft-defender). Some capabilities are limited to the primary workspace:- Creating custom detections- Queries via API Cross-workspace queries for Log Analytics data remain subject to [Log Analytics limitations](/en-us/azure/azure-monitor/logs/cross-workspace-query#limitations). |
| **Microsoft Sentinel** experiences | View data from one workspace for each page in the Microsoft Sentinel section of the Defender portal. Switch between workspaces by selecting **Select a workspace** from the top-right hand side of the browser for most pages. - The **Workbooks** page only shows data associated with the primary workspace. Cross-workspace analytics rules remain subject to [cross-workspace analytics rules limitations and recommendations](extend-sentinel-across-workspaces-tenants#include-cross-workspace-queries-in-scheduled-analytics-rules). |
| **SOC optimization** | Data and recommendations are aggregated from multiple workspaces. |

## Bi-directional sync for workspaces

How incident changes sync between the Azure portal and the Defender portal depends on whether it's a primary or secondary workspace.

| Workspace | Sync behavior |
| --- | --- |
| Primary | For Microsoft Sentinel in the Azure portal, Defender XDR incidents appear in **Threat management** &gt; **Incidents** with the incident provider name **Microsoft XDR**. Any changes you make to the status, closing reason, or assignment of a Defender XDR incident in either the Azure or Defender portal, update in the other's incidents queue. For more information, see [Working with Microsoft Defender XDR incidents in Microsoft Sentinel and bi-directional sync](microsoft-365-defender-sentinel-integration#working-with-microsoft-defender-xdr-incidents-in-microsoft-sentinel-and-bi-directional-sync). |
| Secondary | All alerts and incidents that you create for a secondary workspace are synced between that workspace in the Azure and Defender portals. Data in a workspace is only synced to the workspace in the other portal. |

## Insider risk management (IRM) support

[Microsoft Purview Insider Risk Management (IRM)](/en-us/defender-xdr/irm-investigate-alerts-defender) alerts are correlated to the primary workspace only. If you have IRM alerts with [Microsoft Defender XDR](microsoft-365-defender-sentinel-integration), you must connect IRM to the Microsoft Defender XDR connector in your primary workspace before onboarding the workspace to the Defender portal. This is required to ensure that IRM alerts and incidents are available in the primary workspace. If you don't want to see IRM alerts in the primary workspace, you can instead opt out of the integration with Microsoft Defender XDR.

Also, if the direct [Microsoft 365 Insider Risk Management connector for Microsoft Sentinel](data-connectors-reference#microsoft-365-insider-risk-management) data connector is connected to any of the secondary workspaces, you must disconnect it before onboarding the workspace to the Defender portal.