---
layout: Conceptual
title: Use SOC optimizations programmatically | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/soc-optimization/soc-optimization-api
breadcrumb_path: ../breadcrumb/toc.json
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
ms.reviewer: yohasson
description: Learn how to use Microsoft Sentinel SOC optimization recommendations programmatically.
ms.pagetype: security
ms.author: monaberdugo
author: mberdugo
ms.collection:
- usx-security
ms.topic: concept-article
ms.date: 2024-06-09T00:00:00.0000000Z
locale: en-us
document_id: e6a043f8-9837-a708-c535-2d5e305fc710
document_version_independent_id: efb1b7ae-e848-3660-64d2-1145442c2cb8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/soc-optimization/soc-optimization-api.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/soc-optimization/soc-optimization-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/soc-optimization/soc-optimization-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 9867753b-efbc-84f0-fd91-252c99eb7953
---

# Use SOC optimizations programmatically | Microsoft Learn

Use the Microsoft Sentinel *[`recommendations`](/en-us/rest/api/securityinsights/get-recommendations/list)* API to programmatically interact with SOC optimization recommendations, helping you to close coverage gaps against specific threats and tighten ingestion rates. You can get details about all current recommendations across your workspaces or a specific SOC optimization recommendation, or you can reevaluate a recommendation if you've made changes in your environment.

For example, use the *[`recommendations`](/en-us/rest/api/securityinsights/get-recommendations/list)* API to:

- Build custom reports and dashboards. For example, see Visualize custom SOC optimization data.
- Integrate with third-party tools, such as for SOAR and ITSM services
- Get automated, real-time access to SOC optimization data, triggering evaluations and responding promptly to the suggestions

For customers or MSSPs managing multiple environments, the `recommendations` API provides a scalable way to handle recommendations across multiple workspaces. You can also export data from the API and store it externally for audit, archiving, or tracking trends.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](../overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline). Starting in **July 2025**, many new customers are [automatically onboarded and redirected to the Defender portal](../overview#changes-for-new-customers-starting-july-2025).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](../move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview). For more information, see [It’s Time to Move: Retiring Microsoft Sentinel’s Azure portal for greater security](https://techcommunity.microsoft.com/blog/microsoft-security-blog/planning-your-move-to-microsoft-defender-portal-for-all-microsoft-sentinel-custo/4428613).

The [`recommendations`](/en-us/rest/api/securityinsights/get-recommendations/list) API is in **PREVIEW** and uses version *2024-01-01-preview* or later. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

## Get, update, or reevaluate recommendations

Use the following examples of the [`recommendations`](/en-us/rest/api/securityinsights/get-recommendations/list)` API to interact with SOC optimization recommendations programmatically:

- **Get a list of all current SOC optimization recommendations in your workspace**:

    ```rest
    GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.OperationalInsights/workspaces/{workspaceName}/providers/Microsoft.SecurityInsights/recommendations?api-version=2024-01-01-preview 
    ```
- **Get a specific recommendation by recommendation ID**:

    ```rest
    GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.OperationalInsights/workspaces/{workspaceName}/providers/Microsoft.SecurityInsights/recommendations/{recommendationId} 
    ```

    Find a recommendation's ID value by first getting a list of all recommendations in your workspace.
- **Update a recommendation's status to *Active*, *In Progress*, *Completed*, *Dismissed*, or *Reactivate***:

    ```rest
    PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.OperationalInsights/workspaces/{workspaceName}/providers/Microsoft.SecurityInsights/recommendations/{recommendationId} 
    ```
- **Manually trigger an evaluation for a specific recommendation**:

    ```rest
    POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.OperationalInsights/workspaces/{workspaceName}/providers/Microsoft.SecurityInsights/recommendations/{recommendationId} /triggerEvaluation 
    ```

## Visualize custom SOC optimization data

The **Microsoft Sentinel Optimization Workbook** uses the [`recommendations`](/en-us/rest/api/securityinsights/get-recommendations/list) API to visualize SOC optimization data. Install and customize the workbook in your workspace to create your own custom SOC optimization dashboard.

In the **Microsoft Sentinel Optimization Workbooks**, select the **SOC Optimization** tab and expand the items under **Details** to drill down into to view SOC optimization data. Edit the workbook to modify the data shown as needed for your organization.

For example:

[![Screenshot of the Microsoft Sentinel Optimization Workbook.](media/soc-optimization-api/soc-optimization-workbook.png)](media/soc-optimization-api/soc-optimization-workbook.png#lightbox)

For more information, see:

- [Discover and manage Microsoft Sentinel out-of-the-box content](../sentinel-solutions-deploy)
- [Visualize and monitor your data by using workbooks in Microsoft Sentinel](../monitor-your-data).