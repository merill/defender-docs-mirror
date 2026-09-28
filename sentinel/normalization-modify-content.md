---
layout: Conceptual
title: Modify content to use the Microsoft Sentinel Advanced Security Information Model (ASIM) | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/normalization-modify-content
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
ms.reviewer: ofshezaf
description: Learn how to convert existing Microsoft Sentinel analytics rules to use ASIM normalized data and understand how normalized content fits into the ASIM architecture.
ms.author: edbaynash
author: EdB-MSFT
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: af8983f4-77ee-95f8-ec31-78e86f4a40e7
document_version_independent_id: 132bb95b-7bc8-cac8-edd5-38a18eb8e3ad
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/normalization-modify-content.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/normalization-modify-content
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/normalization-modify-content.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: e800ae73-08f5-4dba-2d3b-5b86aef373ff
---

# Modify content to use the Microsoft Sentinel Advanced Security Information Model (ASIM) | Microsoft Learn

## Convert Microsoft Sentinel content to use ASIM normalized data

Normalized security content in Microsoft Sentinel includes analytics rules, hunting queries, and workbooks that work with unifying normalization parsers.

You can find normalized, out-of-the-box content in Microsoft Sentinel galleries and [Microsoft Sentinel solutions catalog](sentinel-solutions-catalog), create your own normalized content, or modify existing, custom content to use normalized data.

This article explains how to convert existing Microsoft Sentinel analytics rules to use [ASIM normalized data](normalization) with the Advanced Security Information Model (ASIM).

To understand how normalized content fits within the ASIM architecture, refer to the [ASIM architecture diagram](normalization#asim-components).

## Modify custom content to use normalization

To enable your custom Microsoft Sentinel content to use normalization:

- Modify your queries to use any [ASIM unifying parsers](normalization-about-parsers) relevant to the query.
- Modify field names in your query to use the [ASIM normalized schemas](normalization-about-schemas) field names.
- When applicable, change conditions to use the normalized values of the fields in your query.

## Sample normalization for analytics rules

For example, consider the **Rare client observed with high reverse DNS lookup count** DNS analytic rule, which works on DNS events send by Infoblox DNS servers:

```kusto
let threshold = 200;
InfobloxNIOS
| where ProcessName =~ "named" and Log_Type =~ "client"
| where isnotempty(ResponseCode)
| where ResponseCode =~ "NXDOMAIN"
| summarize count() by Client_IP, bin(TimeGenerated,15m)
| where count_ > threshold
| join kind=inner (InfobloxNIOS
    | where ProcessName =~ "named" and Log_Type =~ "client"
    | where isnotempty(ResponseCode)
    | where ResponseCode =~ "NXDOMAIN"
    ) on Client_IP
| extend timestamp = TimeGenerated, IPCustomEntity = Client_IP
```

The following code is the source-agnostic version, which uses normalization to provide the same detection for any source providing DNS query events. The following example uses built-in ASIM parsers:

```kusto
_Im_Dns(responsecodename='NXDOMAIN')
| summarize count() by SrcIpAddr, bin(TimeGenerated,15m)
| where count_ > threshold
| join kind=inner (imDns(responsecodename='NXDOMAIN')) on SrcIpAddr
| extend timestamp = TimeGenerated, IPCustomEntity = SrcIpAddr
```

The normalized, source-agnostic version has the following differences:

- The `_Im_Dns` or `imDns`normalized parsers are used instead of the Infoblox Parser.
- The normalized parsers fetch only DNS query events, so there is no need for checking the event type, as performed by the `where ProcessName =~ "named" and Log_Type =~ "client"` in the Infoblox version.
- The `SrcIpAddr` field is used instead of `Client_IP`.
- Parser parameter filtering is used for ResponseCodeName, eliminating the need for an explicit `where` clauses.

Note

Apart from supporting any normalized DNS source, the normalized version is shorter and easier to understand.

If the schema or parsers do not support filtering parameters, the query changes needed to normalize the rule are similar, except that the filtering conditions are kept from the original query. For example:

```kusto
let threshold = 200;
imDns
| where isnotempty(ResponseCodeName)
| where ResponseCodeName =~ "NXDOMAIN"
| summarize count() by SrcIpAddr, bin(TimeGenerated,15m)
| where count_ > threshold
| join kind=inner (imDns
    | where isnotempty(ResponseCodeName)
    | where ResponseCodeName =~ "NXDOMAIN"
    ) on SrcIpAddr
| extend timestamp = TimeGenerated, IPCustomEntity = SrcIpAddr
```

See more information on the following KQL elements used in the DNS query normalization examples, in the Kusto documentation:

- [***let*** statement](/en-us/kusto/query/let-statement?view=microsoft-sentinel&amp;preserve-view=true)
- [***where*** operator](/en-us/kusto/query/where-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***extend*** operator](/en-us/kusto/query/extend-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***join*** operator](/en-us/kusto/query/join-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***summarize*** operator](/en-us/kusto/query/summarize-operator?view=microsoft-sentinel&amp;preserve-view=true)
- [***isnotempty()*** function](/en-us/kusto/query/isnotempty-function?view=microsoft-sentinel&amp;preserve-view=true)
- [***count()*** aggregation function](/en-us/kusto/query/count-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true)

For more information on KQL, see [Kusto Query Language (KQL) overview](/en-us/kusto/query/?view=microsoft-sentinel&amp;preserve-view=true).

Other resources:

- [KQL quick reference](/en-us/kusto/query/kql-quick-reference?view=microsoft-sentinel&amp;preserve-view=true)
- [Kusto Query Language learning resources](/en-us/kusto/query/kql-learning-resources?view=microsoft-sentinel&amp;preserve-view=true)