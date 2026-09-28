---
layout: Conceptual
title: Manage hunting queries in Microsoft Sentinel using REST API | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/hunting-with-rest-api
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
description: This article describes how Microsoft Sentinel hunting features enable you to take advantage Log Analytics’ REST API to manage hunting queries.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: reference
ms.custom: mvc
ms.date: 2025-11-09T00:00:00.0000000Z
locale: en-us
document_id: 172c04b4-a843-1256-7eaf-16f9724ecabd
document_version_independent_id: 60a50710-3d61-9fe0-7efe-d82a5b1d5d35
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/hunting-with-rest-api.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/hunting-with-rest-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/hunting-with-rest-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: e9accdc9-7f37-88be-6127-ecb309c35501
---

# Manage hunting queries in Microsoft Sentinel using REST API | Microsoft Learn

Microsoft Sentinel, being built in part on Azure Monitor Log Analytics, lets you use Log Analytics’ REST API to manage hunting queries. This document shows you how to create and manage hunting queries using the REST API. Queries created in this way are displayed in the Microsoft Sentinel UI. For more information on the [saved searches API](/en-us/rest/api/loganalytics/savedsearches), see the definitive REST API reference.

## API examples

In the following examples, replace these placeholders with the replacement prescribed in the following table:

| Placeholder | Replace with |
| --- | --- |
| **{subscriptionId}** | the name of the subscription to which you're applying the hunting query. |
| **{resourceGroupName}** | the name of the resource group to which you're applying the hunting query. |
| **{savedSearchId}** | a unique ID (GUID) for each hunting query. |
| **{WorkspaceName}** | the name of the Log Analytics workspace that is the target of the query. |
| **{DisplayName}** | a display name of your choice for the query. |
| **{Description}** | a description of the hunting query. |
| **{Tactics}** | the relevant MITRE ATT&CK tactics that apply to the query. |
| **{Query}** | the query expression for your query. |

### Example 1

This example shows you how to create or update a hunting query for a given Microsoft Sentinel workspace.

#### Request header

```http
PUT https://management.azure.com/subscriptions/{subscriptionId} _
    /resourcegroups/{resourceGroupName} _
    /providers/Microsoft.OperationalInsights/workspaces/{workspaceName} _
    /savedSearches/{savedSearchId}?api-version=2020-03-01-preview
```

#### Request body

```json
{
"properties": {
    “Category”: “Hunting Queries”,
    "DisplayName": "HuntingRule02",
    "Query": "SecurityEvent | where EventID == \"4688\" | where CommandLine contains \"-noni -ep bypass $\"",
    “Tags”: [
        { 
        “Name”: “Description”,
        “Value”: “Test Hunting Query”
        },
        { 
        “Name”: “Tactics”,
        “Value”: “Execution, Discovery”
        }
        ]        
    }
}
```

### Example 2

This example shows you how to delete a hunting query for a given Microsoft Sentinel workspace:

```http
DELETE https://management.azure.com/subscriptions/{subscriptionId} _
       /resourcegroups/{resourceGroupName} _
       /providers/Microsoft.OperationalInsights/workspaces/{workspaceName} _
       /savedSearches/{savedSearchId}?api-version=2020-03-01-preview
```

### Example 3

This example shows you how to retrieve a hunting query for a given workspace:

```http
GET https://management.azure.com/subscriptions/{subscriptionId} _
    /resourcegroups/{resourceGroupName} _
    /providers/Microsoft.OperationalInsights/workspaces/{workspaceName} _
    /savedSearches/{savedSearchId}?api-version=2020-03-01-preview
```