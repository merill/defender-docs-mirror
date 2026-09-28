---
layout: Conceptual
title: Advanced Security Information Model (ASIM) workspace deployed parsers - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/normalization-about-workspace-parsers
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
description: This article explains how to manage and use workspace deployed Advanced Security Information Model (ASIM) parsers
ms.author: edbaynash
author: EdB-MSFT
ms.topic: concept-article
ms.date: 2024-11-11T00:00:00.0000000Z
locale: en-us
document_id: f21b0388-f96a-6e57-9aa1-a0e4db6d5a46
document_version_independent_id: a87cb520-6d3a-c625-e806-4e1fa552c300
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/normalization-about-workspace-parsers.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/normalization-about-workspace-parsers
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/normalization-about-workspace-parsers.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/9bdc1705-9b40-49d6-8377-caa0b71fda66
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/686ed158-d915-41e9-9760-efa46ba88f6d
platformId: 84d759c6-9204-e861-6af0-47e6459aa2f6
---

# Advanced Security Information Model (ASIM) workspace deployed parsers - Microsoft Sentinel | Microsoft Learn

Workspace deployed Advanced Security Information Model (ASIM) parsers are used to support developing and modifying ASIM parsers.

## Deploy workspace parsers

ASIM also supports deploying parsers to specific workspaces [from GitHub](https://aka.ms/DeployASIM), using an ARM template. Workspace deployed parsers are used for ASIM parser development and management. Workspace deployed parsers are functionally equivalent, but have slightly different naming conventions, allowing both parser sets to coexist with built-in parsers in the same Microsoft Sentinel workspace.

It is recommended to use built-in parsers when developing ASIM content. Workspace deployed parsers are typically used during the parser development process or to provide modified versions of built-in parsers as described in [managing parsers](normalization-manage-parsers)

## Use workspace parsers

When using workspace parsers in your queries, the unifying parser name is `im<schema>`, where `<schema>` stands for the specific schema it serves.

The following table lists the available unifying parsers:

| Schema | Unifying parser |
| --- | --- |
| Alert Event | imAlertEvent |
| Audit Event | imAuditEvent |
| Authentication | imAuthentication |
| DHCP Event | imDhcpEvent |
| Dns | imDns |
| File Event | imFileEvent |
| Network Session | imNetworkSession |
| Process Event | imProcessCreate imProcessTerminate |
| Registry Event | imRegistry |
| User Management | imUserManagement |
| Web Session | imWebSession |

## Manage workspace-deployed unifying parsers

### Add a custom parser to a workspace-deployed unifying parser

To add a custom parser, insert a line to the `union` statement in the workspace-deployed unifying parser that references the new custom parser.

Make sure to add both a filtering custom parser and a parameter-less custom parser. The syntax of the line to add is different for each schema:

| Schema | Parser | Line to add |
| --- | --- | --- |
| AlertEvent | `imAlertEvent` | `_parser_name_ (starttime, endtime, ipaddr_has_any_prefix, hostname_has_any, username_has_any, attacktactics_has_any, attacktechniques_has_any, threatcategory_has_any, alertverdict_has_any, eventseverity_has_any)` |
| AuditEvent | `imAuditEvent` | `_parser_name_ (starttime, endtime, srcipaddr_has_any_prefix, eventtype_in, eventresult, actorusername_has_any, operation_has_any, object_has_any, newvalue_has_any)` |
| Authentication | `imAuthentication` | `_parser_name_ (starttime, endtime, targetusername_has_any, actorusername_has_any, srcipaddr_has_any_prefix, srchostname_has_any, targetipaddr_has_any_prefix, dvcipaddr_has_any_prefix, dvchostname_has_any, eventtype_in, eventresultdetails_in, eventresult)` |
| DhcpEvent | `imDhcpEvent` | `_parser_name_ (starttime, endtime, srcipaddr_has_any_prefix, srchostname_has_any, srcusername_has_any, eventresult)` |
| Dns | `imDns` | `_parser_name_ (starttime, endtime, srcipaddr, domain_has_any, responsecodename, response_has_ipv4, response_has_any_prefix, eventtype)` |
| FileEvent | `imFileEvent` | `_parser_name_ (starttime, endtime, eventtype_in, srcipaddr_has_any_prefix, actorusername_has_any, targetfilepath_has_any, srcfilepath_has_any, hashes_has_any, dvchostname_has_any)` |
| NetworkSession | `imNetworkSession` | `_parser_name_ (starttime, endtime, srcipaddr_has_any_prefix, dstipaddr_has_any_prefix, ipaddr_has_any_prefix, dstportnumber, hostname_has_any, dvcaction, eventresult)` |
| ProcessEvent | `imProcessCreate`, `imProcessTerminate` | `_parser_name_ (starttime, endtime, commandline_has_any, commandline_has_all, commandline_has_any_ip_prefix, actingprocess_has_any, targetprocess_has_any, parentprocess_has_any, targetusername_has, actorusername_has, dvcipaddr_has_any_prefix, dvchostname_has_any, eventtype)` |
| RegistryEvent | `imRegistry` | `_parser_name_ (starttime, endtime, eventtype_in, actorusername_has_any, registrykey_has_any, registryvalue_has_any, registryvaluedata_has_any, dvchostname_has_any)` |
| UserManagement | `imUserManagement` | `_parser_name_ (starttime, endtime, srcipaddr_has_any_prefix, targetusername_has_any, actorusername_has_any, eventtype_in)` |
| WebSession | `imWebSession` | `_parser_name_ (starttime, endtime, srcipaddr_has_any_prefix, ipaddr_has_any_prefix, url_has_any, httpuseragent_has_any, eventresultdetails_in, eventresult)` |

When adding an additional parser to a unifying parser, make sure you add a comma at the end of the previous line.

For example, the following example shows the DNS filtering unifying parser, after having added the custom `added_parser`:

```kusto
  let Generic=(starttime:datetime=datetime(null), endtime:datetime=datetime(null) , srcipaddr:string='*' , domain_has_any:dynamic=dynamic([]) , responsecodename:string='*', response_has_ipv4:string='*' , response_has_any_prefix:dynamic=dynamic([]) , eventtype:string='lookup' ){
  let DisabledParsers=materialize(_GetWatchlist('ASimDisabledParsers') | where SearchKey in ('Any', 'imDns') | extend SourceSpecificParser=column_ifexists('SourceSpecificParser','') | distinct SourceSpecificParser);
  let imDnsBuiltInDisabled=toscalar('imDnsBuiltIn' in (DisabledParsers) or 'Any' in (DisabledParsers)); 
  union isfuzzy=true
      vimDnsEmpty
    , vimDnsCiscoUmbrella  ( starttime, endtime, srcipaddr, domain_has_any, responsecodename, response_has_ipv4, response_has_any_prefix, eventtype, (imDnsBuiltInDisabled or('vimDnsCiscoUmbrella'   in (DisabledParsers) )))
    , vimDnsInfobloxNIOS   ( starttime, endtime, srcipaddr, domain_has_any, responsecodename, response_has_ipv4, response_has_any_prefix, eventtype, (imDnsBuiltInDisabled or('vimDnsInfobloxNIOS'    in (DisabledParsers) )))
    ...
    , vimDnsAzureFirewall  ( starttime, endtime, srcipaddr, domain_has_any, responsecodename, response_has_ipv4, response_has_any_prefix, eventtype, (imDnsBuiltInDisabled or('vimDnsAzureFirewall'   in (DisabledParsers) )))
    , vimDnsMicrosoftNXlog ( starttime, endtime, srcipaddr, domain_has_any, responsecodename, response_has_ipv4, response_has_any_prefix, eventtype, (imDnsBuiltInDisabled or('vimDnsMicrosoftNXlog'  in (DisabledParsers) ))),
    added_parser ( starttime, endtime, srcipaddr, domain_has_any, responsecodename, response_has_ipv4, response_has_any_prefix, eventtype)
     };
  Generic( starttime, endtime, srcipaddr, domain_has_any, responsecodename, response_has_ipv4, response_has_any_prefix, eventtype)
```

### Use a modified version of a workspace-deployed parser

Microsoft Sentinel users can directly modify workspace-deployed parsers. Create a parser based on the original, comment out the original, and then add your modified version to the workspace-deployed unifying parser.

For example, the following code shows a DNS filtering unifying parser, having replaced the `vimDnsAzureFirewall` parser with a modified version:

```kusto
  let Generic=(starttime:datetime=datetime(null), endtime:datetime=datetime(null) , srcipaddr:string='*' , domain_has_any:dynamic=dynamic([]) , responsecodename:string='*', response_has_ipv4:string='*' , response_has_any_prefix:dynamic=dynamic([]) , eventtype:string='lookup' ){
  let DisabledParsers=materialize(_GetWatchlist('ASimDisabledParsers') | where SearchKey in ('Any', 'imDns') | extend SourceSpecificParser=column_ifexists('SourceSpecificParser','') | distinct SourceSpecificParser);
  let imDnsBuiltInDisabled=toscalar('imDnsBuiltIn' in (DisabledParsers) or 'Any' in (DisabledParsers)); 
  union isfuzzy=true
      vimDnsEmpty
    , vimDnsCiscoUmbrella  ( starttime, endtime, srcipaddr, domain_has_any, responsecodename, response_has_ipv4, response_has_any_prefix, eventtype, (imDnsBuiltInDisabled or('vimDnsCiscoUmbrella'   in (DisabledParsers) )))
    , vimDnsInfobloxNIOS   ( starttime, endtime, srcipaddr, domain_has_any, responsecodename, response_has_ipv4, response_has_any_prefix, eventtype, (imDnsBuiltInDisabled or('vimDnsInfobloxNIOS'    in (DisabledParsers) )))
    ...
    // , vimDnsAzureFirewall  ( starttime, endtime, srcipaddr, domain_has_any, responsecodename, response_has_ipv4, response_has_any_prefix, eventtype, (imDnsBuiltInDisabled or('vimDnsAzureFirewall'   in (DisabledParsers) )))
    , vimDnsMicrosoftNXlog ( starttime, endtime, srcipaddr, domain_has_any, responsecodename, response_has_ipv4, response_has_any_prefix, eventtype, (imDnsBuiltInDisabled or('vimDnsMicrosoftNXlog'  in (DisabledParsers) ))),
    modified_vimDnsAzureFirewall ( starttime, endtime, srcipaddr, domain_has_any, responsecodename, response_has_ipv4, response_has_any_prefix, eventtype)
     };
  Generic( starttime, endtime, srcipaddr, domain_has_any, responsecodename, response_has_ipv4, response_has_any_prefix, eventtype)
```