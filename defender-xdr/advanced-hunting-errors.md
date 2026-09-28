---
layout: Conceptual
title: Handle errors in advanced hunting for Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-errors
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about common advanced hunting errors in Microsoft Defender XDR, including syntax, timeout, throttling, and query size issues, and how to resolve them.
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.custom:
- cx-ti
- cx-ah
- msecd-doc-authoring-1012
ms.topic: error-reference
ms.date: 2026-05-18T00:00:00.0000000Z
locale: en-us
document_id: aac1be13-53e4-9ccd-9690-4bc4d7a24711
document_version_independent_id: aac1be13-53e4-9ccd-9690-4bc4d7a24711
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-errors.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-errors
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-errors.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
- https://authoring-docs-microsoft.poolparty.biz/devrel/26e1a60c-4ce1-41de-b2d1-e5f3b7e68e6e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad3bd485-5ca9-4865-afde-baec02586899
platformId: e6efcfff-f6ff-cd81-172c-d92988602779
---

# Handle errors in advanced hunting for Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

Advanced hunting displays errors to notify you about syntax mistakes and whenever queries reach [predefined quotas and usage parameters](advanced-hunting-limits). Use the following table to resolve or avoid errors.

| Error type | Cause | Resolution | Error message examples |
| --- | --- | --- | --- |
| Syntax errors | The query contained unrecognized names, including references to nonexistent operators, columns, functions, or tables. | Ensure references to [Kusto operators and functions](/en-us/azure/data-explorer/kusto/query/) are correct. Check [the schema](advanced-hunting-schema-tables) for the correct advanced hunting columns, functions, and tables. Enclose variable strings in quotes so they're recognized. While writing your queries, use the autocomplete suggestions from IntelliSense. | `A recognition error occurred.` |
| Semantic errors | While the query uses valid operator, column, function, or table names, there were errors in its structure and resulting logic. In some cases, advanced hunting identifies the specific operator that caused the error. | Check for errors in the structure of query. Refer to [Kusto documentation](/en-us/azure/data-explorer/kusto/query/) for guidance. While writing your queries, use the autocomplete suggestions from IntelliSense. | `'project' operator: Failed to resolve scalar expression named 'x'` |
| Timeouts | A query can only run within a [limited period before timing out](advanced-hunting-limits). This error can happen more frequently when running complex queries. | [Optimize the query](advanced-hunting-best-practices) | `Query exceeded the timeout period.` |
| CPU throttling | Queries in the same tenant exceeded the [CPU resources](advanced-hunting-limits) that were allocated based on tenant size. | The service checks CPU resource usage every 15 minutes and daily and displays warnings after usage exceeds 10% of the allocated quota. If you reach 100% utilization, the service blocks queries until after the next daily or 15-minute cycle. [Optimize your queries to avoid hitting CPU quotas](advanced-hunting-best-practices) | `You have exceeded processing resources allocated to this tenant. You can run queries again in <duration>.` |
| Excessive resource consumption | The query consumed excessive amounts of resources and was stopped from completing. In some cases, advanced hunting identifies the specific operator that wasn't optimized. | [Optimize the query](advanced-hunting-best-practices) | -`Query stopped due to excessive resource consumption.`-`Query stopped. Adjust use of the <operator name> operator to avoid excessive resource consumption.` |
| Query size exceeded | An unscoped `search` or `union` query spans all tables in the schema (both Microsoft Defender and Microsoft Sentinel Log analytics), which could cause the internal request to exceed Kusto's size limits. This issue is more likely in environments with a large number of tables. | Scope the operator to specific tables using. For example, instead of `search "email"`, use `search in (EmailEvents, EmailAttachmentInfo, IdentityInfo) "email"`. [Optimize your advanced hunting queries](advanced-hunting-best-practices) | `The query cannot run because it exceeds the allowed size limit when processed. ` |
| Unknown errors | The query failed because of an unknown reason. | Try running the query again. Contact Microsoft through the portal if queries continue to return unknown errors. | `An unexpected error occurred during query execution. Please try again in a few minutes.` |