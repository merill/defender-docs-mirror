---
layout: Conceptual
title: Run KQL queries on Microsoft Sentinel data lake using APIs - Microsoft Security | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/kql-queries-api
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
description: Learn how to run KQL queries against the Microsoft Sentinel data lake programmatically using REST APIs. Enable automation, intelligent agents, and scalable analytics.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: zeinam
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: ms-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: b1145f2c-2ba1-07c1-9a8d-3625d7a43ca0
document_version_independent_id: c62f066d-e110-26b9-5b98-eb0dbee3022c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/kql-queries-api.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/kql-queries-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/kql-queries-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
platformId: 150fb620-12c5-8728-f72a-196dedafe4aa
---

# Run KQL queries on Microsoft Sentinel data lake using APIs - Microsoft Security | Microsoft Learn

Microsoft Sentinel data lake supports running Kusto Query Language (KQL) queries programmatically by using REST APIs. Using the REST APIs enables security teams and automation systems to retrieve analytical results without using the Azure portal or interactive query editors. This article explains when to use the API, required permissions, and how to submit a basic query request.

## When to use the KQL query API

The KQL query API is designed for system-to-system access scenarios, including:

- Automation and orchestration workflows
- Background services and scheduled jobs
- Agent and security tools that require query results as input
- Integration with external systems or agents

For interactive investigation and ad-hoc analysis, run KQL queries from the Defender portal instead.

## Authentication and permissions

You can authenticate to the Sentinel data lake API by using either:

- A service principal
- A user access token

Note

Using a service principal currently Entra ID roles and Microsoft Defender XDR unified RBAC roles aren't supported for querying the Sentinel data lake through the Sentinel data lake KQL query API.

## Calling the API

**API endpoint**

All KQL queries are submitted by using the following REST endpoint:

`POST https://api.securityplatform.microsoft.com/lake/kql/v2/rest/query`

**Request body format**

A query request consists of:

- The KQL query
- The target workspace, specified as workspaceName-workspaceId

**Payload parameters**

| Field | Description |
| --- | --- |
| csl | The KQL query to execute |
| db | The Sentinel workspace name and workspace ID |

Sample payload:

```json
{
"csl": "SigninLogs | take 10",
"db": "workspace1-12345678-abcd-abcd-1234-1234567890ab"
}
```

**Submitting the request**

The request must include an OAuth 2.0 bearer token in the Authorization header.

```http
Authorization: Bearer <access_token>
Content-Type: application/json
```

The API returns query results in a structured JSON format that can be processed by automation workflows or applications.

### Optional query settings

You can include additional execution options in the request payload, such as:

- Server timeout
- Query consistency
- Read-only enforcement

Server timeout, query consistency, and read-only enforcement options are useful when running queries in automated or high-scale environments.

sample payload:

```json
{
    "csl": "SigninLogs | take 10",
    "db": "workspace1-12345678-abcd-abcd-1234-1234567890ab",
    "properties": {
        "Options": {
            "servertimeout": "00:04:00",
            "queryconsistency": "strongconsistency",
            "query_language": "kql",
            "request_readonly": false,
            "request_readonly_hardline": false
        }
    }
}
```

## Service limits and considerations

Query execution is subject to time and result size limits. For current limits, see: [Microsoft Sentinel data lake service limits](sentinel-lake-service-limits)