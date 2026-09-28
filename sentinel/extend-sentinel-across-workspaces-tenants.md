---
layout: Conceptual
title: Extend Microsoft Sentinel across workspaces and tenants | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/extend-sentinel-across-workspaces-tenants
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
description: How to use Microsoft Sentinel to query and analyze data across workspaces and tenants.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: krishsa
ms.topic: concept-article
ms.date: 2025-06-10T00:00:00.0000000Z
locale: en-us
document_id: 3739048c-b4d2-aa8f-f9d7-a16024f55251
document_version_independent_id: 3cddeae2-3d06-3b7c-ce9b-56a72732edc2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/extend-sentinel-across-workspaces-tenants.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/extend-sentinel-across-workspaces-tenants
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/extend-sentinel-across-workspaces-tenants.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 46f1b014-ed6f-d1d1-ec8e-39e42a98d294
---

# Extend Microsoft Sentinel across workspaces and tenants | Microsoft Learn

When you onboard Microsoft Sentinel, your first step is to select your Log Analytics workspace. While you can get the full benefit of the Microsoft Sentinel experience with a single workspace, in some cases, you might want to extend your workspace to query and analyze your data across workspaces and tenants. For more information, see [Design a Log Analytics workspace architecture](/en-us/azure/azure-monitor/logs/workspace-design) and [Prepare for multiple workspaces and tenants in Microsoft Sentinel](prepare-multiple-workspaces).

If you onboard Microsoft Sentinel to the Microsoft Defender portal, see:

- [Multiple Microsoft Sentinel workspaces in the Defender portal](/en-us/azure/sentinel/workspaces-defender-portal)
- [Microsoft Defender multitenant management](/en-us/defender-xdr/mto-overview)

## Manage incidents on multiple workspaces

In the Azure and Defender portals, the incidents view allows you to centrally manage and monitor incidents across multiple workspaces or filter the view by workspace. Manage incidents directly or drill down transparently to the incident details in the context of the originating workspace.

If you're working in the Azure portal, see [multiple workspace incident view](multiple-workspace-view). For the Defender portal, see [Multiple Microsoft Sentinel workspaces in the Defender portal](/en-us/azure/sentinel/workspaces-defender-portal).

## Query multiple workspaces

Query [multiple workspaces](/en-us/azure/azure-monitor/logs/cross-workspace-query) to search and correlate data from multiple workspaces in a single query.

- Use the [`workspace( )` expression](/en-us/azure/azure-monitor/logs/cross-workspace-query#query-across-log-analytics-workspaces-using-workspace), with the workspace identifier as the argument, to refer to a table in a different workspace. Use explicit identifier formats to ensure best performance. For more information, see [Identifier formats for cross workspace queries](/en-us/azure/azure-monitor/logs/cross-workspace-query#arguments).
- Use the [union operator](/en-us/kusto/query/union-operator?view=microsoft-sentinel&amp;preserve-view=true) alongside the `workspace( )` expression to apply a query across tables in multiple workspaces.
- Use saved [functions](/en-us/azure/azure-monitor/logs/functions) to simplify cross-workspace queries. For example, you can shorten a long reference to the *SecurityEvent* table in Customer A's workspace by saving the expression:

    ```kusto
    workspace("/subscriptions/<customerA_subscriptionId>/resourcegroups/<resourceGroupName>/providers/microsoft.OperationalInsights/workspaces/<workspaceName>").SecurityEvent
    ```

    as a function called `SecurityEventCustomerA`. You can then query Customer A's *SecurityEvent* table with this function: `SecurityEventCustomerA | where ...` .
- A function can also simplify a commonly used union. For example, you can save the following expression as a function called `unionSecurityEvent`:

    ```kusto
    union 
    workspace("/subscriptions/<subscriptionId>/resourcegroups/<resourceGroupName>/providers/microsoft.OperationalInsights/workspaces/<workspaceName1>").SecurityEvent, 
    workspace("/subscriptions/<subscriptionId>/resourcegroups/<resourceGroupName>/providers/microsoft.OperationalInsights/workspaces/<workspaceName2>").SecurityEvent
    ```

    Then, write a query across both workspaces by beginning with `unionSecurityEvent | where ...` .

Cross-workspace queries for Log Analytics data remain subject to [Log Analytics considerations](/en-us/azure/azure-monitor/logs/cross-workspace-query#considerations).

### Include cross-workspace queries in scheduled analytics rules

You can include cross-workspace queries in scheduled analytics rules. You can use cross-workspace analytics rules in a central SOC, and across tenants (using Azure Lighthouse), suitable for MSSPs. This use is subject to the following limitations:

- You can include **up to 20 workspaces** in a single query. However, for good performance, we recommend including no more than 5.
- You must deploy Microsoft Sentinel **on every workspace** referenced in the query.
- Alerts generated by a cross-workspace analytics rule, and the incidents created from them, exist **only in the workspace where the rule was defined**. The alerts won't be displayed in any of the other workspaces referenced in the query.
- A cross-workspace analytics rule, like any analytics rule, will continue running even if the user who created the rule loses access to workspaces referenced in the rule's query. The only exception to this is in the [case of workspaces in different subscriptions and/or tenants](threat-detection#access-permissions-for-analytics-rules) than the analytics rule.

Alerts and incidents created by cross-workspace analytics rules contain all the related entities, including those from all the referenced workspaces and the "home" workspace (where the rule was defined). This way, analysts get a full picture of alerts and incidents.

Note

Querying multiple workspaces in the same query might affect performance, and therefore is recommended only when the logic requires this functionality.

### Use cross-workspace workbooks

Workbooks provide dashboards and apps to Microsoft Sentinel. When working with multiple workspaces, workbooks provide monitoring and actions across workspaces.

Workbooks can provide cross-workspace queries in one of three methods, suitable for different levels of end-user expertise:

| Method | Description | When should I use? |
| --- | --- | --- |
| Write cross-workspace queries | The workbook creator can write cross-workspace queries (described above) in the workbook. | I want the workbook creator to create a workspace structure that is transparent to the user. |
| Add a workspace selector to the workbook | The workbook creator can [implement a workspace selector as part of the workbook](https://techcommunity.microsoft.com/t5/azure-sentinel/making-your-azure-sentinel-workbooks-multi-tenant-or-multi/ba-p/1402357). | I want to allow the user to control the workspaces shown by the workbook, with an easy-to-use dropdown box. |
| Edit the workbook interactively | An advanced user modifying an existing workbook can edit the queries in it, selecting the target workspaces using the workspace selector in the editor. | I want to allow a power user to easily modify existing workbooks to work with multiple workspaces. |

### Hunt across multiple workspaces

Microsoft Sentinel provides preloaded query samples designed to get you started and get you familiar with the tables and the query language. Microsoft security researchers constantly add new built-in queries and fine-tune existing queries. You can use these queries to look for new detections and identify signs of intrusion that your security tools might have missed.

Cross-workspace hunting capabilities enable your threat hunters to create new hunting queries, or adapt existing ones, to cover multiple workspaces, by using the union operator and the workspace() expression as shown above.

## Manage multiple workspaces using automation

To configure and manage multiple Log Analytics workspaces enabled for Microsoft Sentinel, you need to automate the use of the Microsoft Sentinel management API.

- Learn how to [automate the deployment of Microsoft Sentinel resources](https://techcommunity.microsoft.com/t5/azure-sentinel/extending-azure-sentinel-apis-integration-and-management/ba-p/1116885), including alert rules, hunting queries, workbooks, and playbooks.
- Learn how to [deploy custom content from your repository](ci-cd). This resource provides a consolidated methodology for managing Microsoft Sentinel as code and for deploying and configuring resources from a private Azure DevOps or GitHub repository.

## Manage workspaces across tenants

In many scenarios, the different Log Analytics workspaces enabled for Microsoft Sentinels can be located in different Microsoft Entra tenants. You can use [Azure Lighthouse](/en-us/azure/lighthouse/overview) to extend all cross-workspace activities across tenant boundaries, allowing users in your managing tenant to work on workspaces across all tenants.

Once Azure Lighthouse is [onboarded](/en-us/azure/lighthouse/how-to/onboard-customer), use the [directory + subscription selector](multiple-tenants-service-providers#access-microsoft-sentinel-in-managed-tenants) on the Azure portal to select all the subscriptions containing workspaces you want to manage, in order to ensure that they'll all be available in the different workspace selectors in the portal.

When using Azure Lighthouse, it's recommended to create a group for each Microsoft Sentinel role and delegate permissions from each tenant to those groups.

If you're using the Defender portal, multitenant management for Microsoft Defender XDR and Microsoft Sentinel provides your security operation teams with a single, unified view of all the tenants you manage. For more information, see [Microsoft Defender multitenant management](/en-us/defender-xdr/mto-overview).