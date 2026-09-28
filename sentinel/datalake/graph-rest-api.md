---
layout: Conceptual
title: Graph REST APIs for custom graphs (preview) - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/graph-rest-api
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
ms.subservice: sentinel-platform
search.appverid: met150
description: Learn how to use the Graph REST APIs to list and query custom graphs in the Microsoft Sentinel data lake.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: sourinpaul
ms.topic: reference
ms.date: 2026-04-01T00:00:00.0000000Z
ms.collection: ms-security
locale: en-us
document_id: 8245050b-4006-4ad5-ea01-94e62bc5db86
document_version_independent_id: 58834f9b-f64a-b08b-2012-ffcfea470adf
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/graph-rest-api.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/graph-rest-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/graph-rest-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: ba9a176d-c37d-8a96-2e7c-2b6a313d4196
---

# Graph REST APIs for custom graphs (preview) - Microsoft Security | Microsoft Learn

The Graph REST APIs let you list and query custom graphs in your Microsoft Sentinel data lake. Use these APIs to programmatically interact with your custom graphs from any HTTP client, automation pipeline, or custom application.

For more information on creating custom graphs, see [Create custom graphs in the security data lake](create-custom-graphs).

## Authentication

The Graph REST APIs use OAuth 2.0 bearer token authentication. To call the APIs, obtain an access token from Microsoft Entra ID and include it in the `Authorization` header of each request.

### Get an access token

1. Register an application in Microsoft Entra ID, or use an existing app registration. For more information, see [Register an application](/en-us/entra/identity-platform/quickstart-register-app).
2. Grant the application the required permissions for Microsoft Defender XDR.
3. Request an access token using the OAuth 2.0 client credentials flow or on behalf of a signed-in user.

### Include the token in requests

Add the token to the `Authorization` header of every API request:

```http
Authorization: Bearer <access_token>
```

## Base URL

All Graph REST API endpoints use the following base URL:

```http
https://api.securityplatform.microsoft.com
```

## List graphs

List all custom graphs available in your tenant.

### Request

```http
GET https://api.securityplatform.microsoft.com/graphs/graph-instances?graphTypes=Custom
```

No request body is required.

### Response

```json
{
  "value": [
    {
      "name": "custom_graph_10",
      "mapFileName": "custom_graph_10",
      "mapFileVersion": "1.0.0",
      "graphDefinitionName": "custom_graph_10",
      "graphDefinitionVersion": "1.0.0",
      "refreshFrequency": "00:00:00",
      "createTime": "11/04/2025 22:32:43",
      "lastUpdateTime": "11/04/2025 22:32:43",
      "lastSnapshotTime": "2025-11-04T22:34:04.7105015+00:00",
      "lastSnapshotRequestTime": "2025-11-04T22:32:52.0187838+00:00",
      "instanceStatus": "Ready"
    },
    {
      "name": "notebook_graph_5",
      "mapFileName": null,
      "mapFileVersion": null,
      "graphDefinitionName": "notebook_graph_5",
      "graphDefinitionVersion": "1.0.0",
      "refreshFrequency": "00:00:00",
      "createTime": "11/04/2025 20:15:22",
      "lastUpdateTime": "11/04/2025 20:15:22",
      "lastSnapshotTime": null,
      "lastSnapshotRequestTime": null,
      "instanceStatus": "Creating"
    }
  ]
}
```

### Response properties

| Property | Type | Description |
| --- | --- | --- |
| `name` | String | The name of the graph instance. |
| `mapFileName` | String | The name of the map file associated with the graph. |
| `mapFileVersion` | String | The version of the map file. |
| `graphDefinitionName` | String | The name of the graph definition used to build this instance. |
| `graphDefinitionVersion` | String | The version of the graph definition. |
| `refreshFrequency` | String | How often the graph data is refreshed. |
| `createTime` | String | When the graph instance was created. |
| `lastUpdateTime` | String | When the graph instance was last updated. |
| `lastSnapshotTime` | String | The timestamp of the most recent data snapshot. |
| `lastSnapshotRequestTime` | String | When the last snapshot was requested. |
| `instanceStatus` | String | The current status of the graph instance. |

### Response status codes

| Status code | Description |
| --- | --- |
| 200 OK | List retrieved successfully. |

## Query a graph

Query a custom graph using Graph Query Language (GQL). For more information on GQL, see [GQL reference for Microsoft Sentinel graph](gql-reference-for-sentinel-custom-graph).

Note

`{graphName}` refers to the `name` of a graph returned from the list operation.

### Request

```http
POST https://api.securityplatform.microsoft.com/graphs/graph-instances/{graphName}/query
Content-Type: application/json
```

### Request body

```json
{
  "query": "string",
  "queryLanguage": "GQL"
}
```

### Request body properties

| Property | Type | Required | Description |
| --- | --- | --- | --- |
| `query` | String | Yes | The GQL query to execute. |
| `queryLanguage` | String | Yes | The query language. Must be `GQL`. |
| `responseFormats` | String array | No | Controls the format of the query response. Accepts one or both of the following values: `Table`, `Graph`. Defaults to `Table` if not specified. |

### Response formats

The `responseFormats` property controls the structure of the response:

| Format | Description |
| --- | --- |
| `Table` | Returns raw tabular data (default if not specified). |
| `Graph` | Returns graph-structured data with nodes and edges. |

You can request one or both formats:

- `["Table"]` - Returns only table format.
- `["Graph"]` - Returns only graph format.
- `["Table", "Graph"]` - Returns both formats in the response.

### Example: Basic query

```http
POST https://api.securityplatform.microsoft.com/graphs/graph-instances/{graphName}/query
Content-Type: application/json

{
  "query": "MATCH (u)-[v]->(w) RETURN * LIMIT 2",
  "queryLanguage": "GQL"
}
```

### Example: Query with both response formats

```http
POST https://api.securityplatform.microsoft.com/graphs/graph-instances/{graphName}/query
Content-Type: application/json

{
  "query": "MATCH (n:User)-[r:HasAccess]->(m:Resource) RETURN n, r, m LIMIT 100",
  "responseFormats": ["Table", "Graph"],
  "queryLanguage": "GQL"
}
```

### Sample response (both formats)

```json
{
  "status": 200,
  "result": {
    "rawData": {
      "tables": [
        {
          "tableName": "PrimaryResult",
          "columns": [
            {
              "columnName": "u",
              "dataType": "dynamic"
            },
            {
              "columnName": "r",
              "dataType": "dynamic"
            },
            {
              "columnName": "g",
              "dataType": "dynamic"
            }
          ],
          "rows": [
            [
              {
                "oid": "node-user-001",
                "labels": ["User"],
                "properties": {
                  "name": "Aino Rebane",
                  "email": "aino.rebane@contoso.com",
                  "department": "Engineering"
                }
              },
              {
                "oid": "edge-001",
                "labels": ["HasRole"],
                "sourceOid": "node-user-001",
                "targetOid": "node-group-001",
                "properties": {
                  "assignedDate": "2024-01-15T10:30:00Z",
                  "assignedBy": "admin@contoso.com"
                }
              },
              {
                "oid": "node-group-001",
                "labels": ["Group"],
                "properties": {
                  "name": "Administrators",
                  "description": "System administrators group",
                  "memberCount": 25
                }
              }
            ]
          ]
        }
      ]
    },
    "graph": {
      "nodes": [
        {
          "id": "node-user-001",
          "labels": ["User"],
          "properties": {
            "name": "Aino Rebane",
            "email": "aino.rebane@contoso.com",
            "department": "Engineering"
          }
        },
        {
          "id": "node-group-001",
          "labels": ["Group"],
          "properties": {
            "name": "Administrators",
            "description": "System administrators group",
            "memberCount": 25
          }
        },
        {
          "id": "node-group-002",
          "labels": ["Group"],
          "properties": {
            "name": "Engineering Team",
            "description": "Software engineering team",
            "memberCount": 150
          }
        }
      ],
      "edges": [
        {
          "id": "edge-001",
          "sourceId": "node-user-001",
          "targetId": "node-group-001",
          "labels": ["HasRole"],
          "properties": {
            "assignedDate": "2024-01-15T10:30:00Z",
            "assignedBy": "admin@contoso.com"
          }
        },
        {
          "id": "edge-002",
          "sourceId": "node-user-001",
          "targetId": "node-group-002",
          "labels": ["HasRole"],
          "properties": {
            "assignedDate": "2024-02-01T14:20:00Z",
            "assignedBy": "hr@contoso.com"
          }
        }
      ]
    }
  },
  "correlationId": "aaaa0000-bb11-2222-33cc-444444dddddd"
}
```

### Response status codes

| Status code | Description |
| --- | --- |
| 200 OK | Query executed successfully. |
| 404 Not Found | The specified graph instance doesn't exist. |

### Error response example

```json
{
    "error": {
        "code": "GraphInstanceNotFound",
        "message": "Graph Instance CustomGraph1 does not exist.",
        "target": null,
        "details": []
    }
}
```