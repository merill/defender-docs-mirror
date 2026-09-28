---
layout: Conceptual
title: Create deep links to Microsoft Sentinel graph queries | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/datalake/create-deep-links-graph-queries
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
description: Learn how to build a Microsoft Sentinel graph deep link that opens, and optionally runs, a query on a specific graph by using URL parameters.
author: EdB-MSFT
ms.author: edbaynash
ms.topic: how-to
ms.custom: msecd-doc-authoring-1012
ms.date: 2026-07-05T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 326f9639-dc3f-22d6-a558-216eef33663a
document_version_independent_id: 102d8af9-5d04-ccbf-c441-0ce2b7a513b1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/datalake/create-deep-links-graph-queries.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/datalake/create-deep-links-graph-queries
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/datalake/create-deep-links-graph-queries.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: d0d79a22-b76b-404d-dcaa-422b6c0b44e5
---

# Create deep links to Microsoft Sentinel graph queries | Microsoft Learn

You can create a deep link that opens the Microsoft Sentinel graph page with a specific query already in the editor and, optionally, runs the query automatically when the page loads. Embed these links in runbooks, incident reports, or other documentation so that a responder can select a link and jump straight to a preconfigured investigation query on the correct graph.

Deep link queries are embedded in the URL as Base64 (base64url) text so they can be passed reliably as a single URL parameter. The query isn't encrypted, signed, or compressed.

## Prerequisites

To create a deep link, you need the following prerequisites:

- A graph instance that exists in your tenant. You pass its name in the `graphInstance` parameter. To find valid names, see Find valid graphInstance values.
- The query text that you want to open in the editor.

To open a linked query, you need permission to view the graph and run queries. Deep links don't bypass access controls, so a user without those permissions can't access the linked query. For more information, see [Get started with custom graphs in Microsoft Sentinel](create-custom-graphs#permissions).

## Construct the deep link URL

A deep link URL consists of several components. The following breaks down the basic structure and each piece:

```http
https://security.microsoft.com/graphs?tid=<tenant-id>&graphInstance=<graph-name>&query=<encoded-query>&autoRun=<true|false>&addQuery=<true|false>
```

### URL components

| Component | Required | Description |
| --- | --- | --- |
| `https://security.microsoft.com/graphs` | — | Base URL for Microsoft Sentinel graphs. |
| `tid=<tenant-id>` | No | Your Azure tenant ID (GUID). If omitted, the current tenant is used. |
| `graphInstance=<graph-name>` | Yes | Name of the graph instance to open, for example `IdentityAttackScenarioGraph`. If the value is missing or unknown, nothing is prefilled. |
| `query=<encoded-query>` | No | Your base64url-encoded Graph Query Language (GQL) query. Prefills the editor with the decoded query. |
| `language=<language>` | No | Query language. The only supported value is `gql`. Case-insensitive; any unknown value falls back to `gql`. |
| `autoRun=<true\|false>` | No | Whether to run the query automatically when the tab opens. Defaults to `true`. Only the literal string `false` (case-insensitive) disables autorun; any other value runs the query. |
| `addQuery=<true\|false>` | No | Whether to prefill the editor with the query. Defaults to `true`. Set to `false` to leave the editor empty even when `query` is present. |

### Example breakdown

The following deep link opens the Microsoft Sentinel graph page with a specific query prefilled in the editor, but doesn't run it automatically:

```http
https://security.microsoft.com/graphs
  ?tid=12345678-1234-1234-1234-123456789012
  &graphInstance=IdentityAttackScenarioGraph
  &query=Ly8gVmlzdWFsaXplIGFueSBncmFwaApNQVRDSCAoeCktW3ldLT4oeikKUkVUVVJOICoKTElNSVQgMTAw
  &autoRun=false
```

The `query` parameter decodes to the following GQL query:

```gql
// Visualize any graph
MATCH (x)-[y]->(z)
RETURN *
LIMIT 100
```

Breakdown:

- **Base**: `https://security.microsoft.com/graphs`
- **Tenant**: `tid=12345678-1234-1234-1234-123456789012`
- **Graph**: `graphInstance=IdentityAttackScenarioGraph`
- **Query**: `query=Ly8gVmlzdWFsaXplIGFueSBncmFwaApNQVRDSCAoeCktW3ldLT4oeikKUkVUVVJOICoKTElNSVQgMTAw` (encodes to the GQL shown above)
- **Auto-run**: `autoRun=false` (query won't run automatically)

## Encode the query with base64url

Encode the `query` value with the following steps. These steps match the `encodeQueryBase64` function in `QueryUtils.ts`.

1. UTF-8 encode the raw query text into bytes.
2. Base64 encode those bytes.
3. Replace `+` with `-` and `/` with `_` to make the value URL-safe.
4. Strip any trailing `=` padding characters.
5. Place the result in the URL as the `query` parameter. Standard URL encoding is safe to apply on top.

Note

The maximum generated-link length is 7,168 characters. Very large queries may not produce a working deep link.

## Generate the link

The following JavaScript matches the application encoder exactly and assembles a complete deep link:

```javascript
function encodeQueryBase64(query) {
  const bytes = new TextEncoder().encode(query);
  const binary = String.fromCharCode(...bytes);
  return btoa(binary)
    .replace(/\+/g, '-')
    .replace(/\//g, '_')
    .replace(/=+$/g, '');
}

const base = 'https://security.microsoft.com/graphs';
const params = new URLSearchParams({
  graphInstance: 'IdentityAttackScenarioGraph',
  query: encodeQueryBase64('MATCH (x)-[y]->(z)\nRETURN *\nLIMIT 100'),
  autoRun: 'true',
});
const deeplink = `${base}?${params.toString()}`;
```

## Conditions for autorun

For the query to run automatically, all of the following conditions must be true:

- `autoRun` isn't set to the literal string `false`.
- The decoded query isn't empty.
- The `graphInstance` exists for the tenant.

## Find valid graphInstance values

You can use any graph instance that exists in your tenant by its instance name. To find the available names, either browse the Microsoft Sentinel graphs UI or call the Microsoft Sentinel Graph Service `GET /graph-instances` API. This API returns the graph instances available to your tenant. You can optionally filter the results with `?graphTypes=`. Use the name of any returned instance.

```http
GET https://api.securityplatform.microsoft.com/graphs/graph-instances?graphTypes=Custom
```

## Common use cases

- **Open the graph and prefill the query without running it**: Set `autoRun=false`, as shown in the example. Users can review and edit the query before it runs, which avoids unnecessary query costs.
- **Open the graph with no query**: Omit the `query` parameter, or set `addQuery=false`. Use this option to direct users to a graph for manual exploration without imposing a predefined query.
- **Target a specific tenant**: Include `tid=<tenant-id>`. The deep link then opens in the correct tenant without the user switching tenants manually.