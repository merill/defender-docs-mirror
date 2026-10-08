---
layout: Conceptual
title: Manage Advanced Security Information Model (ASIM) parsers | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/normalization-manage-parsers
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
description: This article explains how to manage Advanced Security Information Model (ASIM) parsers, add a customer parser, and replace a built-in parser.
ms.author: edbaynash
author: EdB-MSFT
ms.topic: how-to
ms.date: 2026-10-08T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 51c10057-a777-a549-4a46-b50bdc860256
document_version_independent_id: fadaa816-bf27-4210-18d4-b87427a8d5f9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/normalization-manage-parsers.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/normalization-manage-parsers
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/normalization-manage-parsers.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
platformId: 017f459e-4c86-4ac3-7125-a42b7e7ada5d
---

# Manage Advanced Security Information Model (ASIM) parsers | Microsoft Learn

Advanced Security Information Model (ASIM) users use *unifying parsers* instead of table names in their queries, to view data in a normalized format and get all the data relevant to the schema in a single query. Each unifying parser uses multiple source-specific parsers that handle each source's specific details.

To understand how parsers fit within the ASIM architecture, refer to the [ASIM components section in the ASIM architecture diagram](normalization#asim-components).

You may need to manage the source-specific parsers used by each unifying parser to:

- **Add a custom, source-specific parser** to a unifying parser.
- **Replace a built-in, source-specific parser** that's used by a unifying parser with a custom, source-specific parser. Replace built-in parsers when you want to:

    - Use a version of the built-in parser other than the one used by default in the unifying parser.
    - Prevent automated updates by preserving the version of the source-specific parser used by the unifying parser.
    - Use a modified version of a built-in parser.
- **Configure a source-specific parser**, for example to define the sources that send information relevant to the parser.

This article guides you through managing the source-specific parsers used by unifying parsers.

## Prerequisites

The procedures in this article assume that all source-specific parsers have already been deployed to your Microsoft Sentinel workspace.

For deployment instructions, see the [Deploy parsers section in Develop ASIM parsers](normalization-develop-parsers#deploy-parsers).

## Manage built-in unifying parsers

Because built-in unifying parsers can't be edited directly, you manage them by deploying custom unifying parsers, adding or excluding source-specific parsers, and using watchlists to control parser behavior.

### Set up your workspace

Microsoft Sentinel users cannot edit built-in unifying parsers. Instead, use the following mechanisms to modify the behavior of built-in unifying parsers:

- **To support adding source-specific parsers**, ASIM uses unifying, custom parsers. These custom parsers are workspace-deployed, and therefore editable. Built-in, unifying parsers automatically pick up these custom parsers, if they exist.

    You can deploy initial, empty, unifying custom parsers to your Microsoft Sentinel workspace for all supported schemas, or individually for specific schemas. For more information, see [Deploy initial ASIM empty custom unifying parsers](https://aka.ms/ASimDeployEmptyCustomUnifyingParsers) in the Microsoft Sentinel GitHub repository.
- **To support excluding built-in source-specific parsers**, ASIM uses a watchlist. Deploy the watchlist to your Microsoft Sentinel workspace from the Microsoft Sentinel [ASIM watchlist deployment template](https://aka.ms/DeployASimWatchlists) on GitHub.
- **To define source type for built-in and custom parsers**, ASIM uses a watchlist. Deploy the watchlist to your Microsoft Sentinel workspace from the Microsoft Sentinel [ASIM watchlist deployment template](https://aka.ms/DeployASimWatchlists) on GitHub.

### Add a custom parser to a built-in unifying parser

To add a custom parser, insert a line to the custom unifying parser to reference the new, custom parser.

Make sure to add both a filtering custom parser (one that accepts filtering parameters to optimize performance) and a parameter-less custom parser (one that returns all results without filtering parameters). To learn more about how to edit parsers, refer to the document [Functions in Azure Monitor log queries](/en-us/azure/azure-monitor/logs/functions#edit-a-function).

The syntax of the line to add is different for each schema. The following table uses the parameters defined in `ParserParams` in the corresponding `Parsers/ASim<SchemaName>/Parsers/im<SchemaName>.yaml` file in the [Microsoft Sentinel repository](https://github.com/Azure/Azure-Sentinel/tree/master/Parsers). Replace `_parser_name_` with your filtering source-specific parser's function name. Use named arguments to avoid binding values to the wrong parameters when declaration order differs.

Before adding a line, verify that your custom unifying function declares the referenced parameters and that your source-specific parser accepts them. Forward `pack=pack` only if the source-specific parser supports it. The table sets `disabled=false` so that the custom parser is enabled. To disable or re-enable the parser, change the `disabled` argument to `true` or `false` in the source-specific parser call within the custom unifying function.

| Schema | Parser | Line to add |
| --- | --- | --- |
| AgentEvent | `Im_AgentEventCustom` | `_parser_name_ (starttime=starttime, endtime=endtime, agentid_has_any=agentid_has_any, agentname_has_any=agentname_has_any, username_has_any=username_has_any, disabled=false, pack=pack)` |
| AlertEvent | `Im_AlertEventCustom` | `_parser_name_ (starttime=starttime, endtime=endtime, ipaddr_has_any_prefix=ipaddr_has_any_prefix, hostname_has_any=hostname_has_any, username_has_any=username_has_any, attacktactics_has_any=attacktactics_has_any, attacktechniques_has_any=attacktechniques_has_any, threatcategory_has_any=threatcategory_has_any, alertverdict_has_any=alertverdict_has_any, eventseverity_has_any=eventseverity_has_any, disabled=false, pack=pack)` |
| AssetEntity | `Im_AssetEntityCustom` | `_parser_name_ (starttime=starttime, endtime=endtime, entityid_has_any=entityid_has_any, entityname_has_any=entityname_has_any, assettype_in=assettype_in, path_has_any=path_has_any, assetowner_has_any=assetowner_has_any, entitysource_has_any=entitysource_has_any, disabled=false, pack=pack)` |
| AuditEvent | `Im_AuditEventCustom` | `_parser_name_ (starttime=starttime, endtime=endtime, srcipaddr_has_any_prefix=srcipaddr_has_any_prefix, actorusername_has_any=actorusername_has_any, operation_has_any=operation_has_any, eventtype_in=eventtype_in, eventresult=eventresult, object_has_any=object_has_any, newvalue_has_any=newvalue_has_any, disabled=false, pack=pack)` |
| Authentication | `Im_AuthenticationCustom` | `_parser_name_ (starttime=starttime, endtime=endtime, username_has_any=username_has_any, targetappname_has_any=targetappname_has_any, srcipaddr_has_any_prefix=srcipaddr_has_any_prefix, srchostname_has_any=srchostname_has_any, eventtype_in=eventtype_in, eventresultdetails_in=eventresultdetails_in, eventresult=eventresult, disabled=false, pack=pack)` |
| DhcpEvent | `Im_DhcpEventCustom` | `_parser_name_ (starttime=starttime, endtime=endtime, srcipaddr_has_any_prefix=srcipaddr_has_any_prefix, srchostname_has_any=srchostname_has_any, srcusername_has_any=srcusername_has_any, eventresult=eventresult, disabled=false, pack=pack)` |
| Dns | `Im_DnsCustom` | `_parser_name_ (starttime=starttime, endtime=endtime, srcipaddr=srcipaddr, domain_has_any=domain_has_any, responsecodename=responsecodename, response_has_ipv4=response_has_ipv4, response_has_any_prefix=response_has_any_prefix, eventtype=eventtype, disabled=false, pack=pack)` |
| EmailEvent | `Im_EmailEventCustom` | `_parser_name_ (starttime=starttime, endtime=endtime, ipaddr_has_any_prefix=ipaddr_has_any_prefix, emailfromaddress_has_any=emailfromaddress_has_any, emailrecipient_has_any=emailrecipient_has_any, emailsubject_has_any=emailsubject_has_any, emaildirection_in=emaildirection_in, emaildeliverylocation_in=emaildeliverylocation_in, eventresult=eventresult, disabled=false, pack=pack)` |
| FileEvent | `Im_FileEventCustom` | `_parser_name_ (starttime=starttime, endtime=endtime, eventtype_in=eventtype_in, srcipaddr_has_any_prefix=srcipaddr_has_any_prefix, actorusername_has_any=actorusername_has_any, targetfilepath_has_any=targetfilepath_has_any, srcfilepath_has_any=srcfilepath_has_any, hashes_has_any=hashes_has_any, dvchostname_has_any=dvchostname_has_any, disabled=false, pack=pack)` |
| NetworkSession | `Im_NetworkSessionCustom` | `_parser_name_ (starttime=starttime, endtime=endtime, srcipaddr_has_any_prefix=srcipaddr_has_any_prefix, dstipaddr_has_any_prefix=dstipaddr_has_any_prefix, ipaddr_has_any_prefix=ipaddr_has_any_prefix, dstportnumber=dstportnumber, hostname_has_any=hostname_has_any, dvcaction=dvcaction, eventresult=eventresult, disabled=false, pack=pack)` |
| ProcessEvent | `Im_ProcessEventCustom` | `_parser_name_ (starttime=starttime, endtime=endtime, commandline_has_any=commandline_has_any, commandline_has_all=commandline_has_all, commandline_has_any_ip_prefix=commandline_has_any_ip_prefix, actingprocess_has_any=actingprocess_has_any, targetprocess_has_any=targetprocess_has_any, parentprocess_has_any=parentprocess_has_any, actorusername_has=actorusername_has, targetusername_has=targetusername_has, dvcipaddr_has_any_prefix=dvcipaddr_has_any_prefix, dvchostname_has_any=dvchostname_has_any, hashes_has_any=hashes_has_any, eventtype=eventtype, disabled=false)` |
| RegistryEvent | `Im_RegistryEventCustom` | `_parser_name_ (starttime=starttime, endtime=endtime, eventtype_in=eventtype_in, actorusername_has_any=actorusername_has_any, registrykey_has_any=registrykey_has_any, registryvalue_has_any=registryvalue_has_any, registrydata_has_any=registrydata_has_any, dvchostname_has_any=dvchostname_has_any, disabled=false, pack=pack)` |
| UserManagement | `Im_UserManagementCustom` | `_parser_name_ (starttime=starttime, endtime=endtime, srcipaddr_has_any_prefix=srcipaddr_has_any_prefix, targetusername_has_any=targetusername_has_any, actorusername_has_any=actorusername_has_any, eventtype_in=eventtype_in, disabled=false, pack=pack)` |
| WebSession | `Im_WebSessionCustom` | `_parser_name_ (starttime=starttime, endtime=endtime, srcipaddr_has_any_prefix=srcipaddr_has_any_prefix, ipaddr_has_any_prefix=ipaddr_has_any_prefix, url_has_any=url_has_any, httpuseragent_has_any=httpuseragent_has_any, eventresultdetails_in=eventresultdetails_in, eventresult=eventresult, eventresultdetails_has_any=eventresultdetails_has_any, disabled=false, pack=pack)` |

When adding an additional parser to a unifying custom parser that already references parsers, make sure you add a comma at the end of the previous line.

For example, the following code shows `Im_DnsCustom` after adding `added_parser`. Both source-specific parsers in this example accept `disabled` and `pack`, and the custom unifying function declares both parameters. The `union isfuzzy=true` statement combines results from the existing and new parsers. It can tolerate a missing union source when another source resolves, but it doesn't suppress all query errors or validate parameter forwarding:

```kusto
union isfuzzy=true
existing_parser(starttime=starttime, endtime=endtime, srcipaddr=srcipaddr, domain_has_any=domain_has_any, responsecodename=responsecodename, response_has_ipv4=response_has_ipv4, response_has_any_prefix=response_has_any_prefix, eventtype=eventtype, disabled=disabled, pack=pack),
added_parser(starttime=starttime, endtime=endtime, srcipaddr=srcipaddr, domain_has_any=domain_has_any, responsecodename=responsecodename, response_has_ipv4=response_has_ipv4, response_has_any_prefix=response_has_any_prefix, eventtype=eventtype, disabled=disabled, pack=pack)
```

### Use a modified version of a built-in parser

To modify an existing, built-in source-specific parser:

1. Create a custom parser based on the original parser and add the custom parser to the built-in unifying parser. You can use the [workspace-deployed ASIM parsers](normalization-about-workspace-parsers) version of the parser as a starting point.
2. Add a record to the `ASim Disabled Parsers` watchlist.
3. Define the `CallerContext` value as `Exclude<parser name>`, where `<parser name>` is the name of the unifying parsers you want to exclude the parser from.
4. Define the `SourceSpecificParser` value `Exclude<parser name>`, where `<parser name>`is the name of the parser you want to exclude, without a version specifier.

For example, to exclude the Azure Firewall DNS parser, add the following record to the watchlist:

| Parser deployment | CallerContext | SourceSpecificParser |
| --- | --- | --- |
| Read-only built-in `_ASim_Dns` | `Exclude_ASim_Dns` | `Exclude_ASim_Dns_AzureFirewall` |
| Read-only built-in `_Im_Dns` | `Exclude_Im_Dns` | `Exclude_Im_Dns_AzureFirewall` |
| Workspace-deployed `ASimDns` | `ExcludeASimDns` | `ExcludeASimASimDnsAzureFirewall` |

Title-case exclusion keys without underscores are specific to workspace-deployed parsers.

### Prevent an automated update of a built-in parser

To pin a built-in, source-specific parser to a specific version and prevent automatic updates, complete these steps:

1. Add the built-in parser version you want to use, such as `_Im_Dns_AzureFirewallV02`, to the custom unifying parser. For more information, see Add a custom parser to a built-in unifying parser.
2. Add an exception for the built-in parser. For example, when you want to entirely opt out from automatic updates, and therefore exclude a large number of built-in parsers, add:

- A record with `Any` as the `SourceSpecificParser` field, to exclude all parsers for the `CallerContext`.
- A record for `Any` in the CallerContext and the `SourceSpecificParser` fields to exclude all built-in parsers.

For details on excluding built-in parsers using the watchlist, see the Use a modified version of a built-in parser section.

## Configure the sources relevant to a source-specific parser

Some parsers require you to update the list of sources that are relevant to the parser. For example, a parser that uses Syslog data, may not be able to determine what Syslog events are relevant to the parser. Such a parser may use the `Sources_by_SourceType` watchlist to determine which sources send information relevant to the parser. For such parses add a record for each relevant source to the watchlist:

- Set the `SourceType` field to the parser specific value specified in the parser documentation.
- Set the `Source` field to the identifier of the source used in the events. You may need to query the original table, such as Syslog, to determine the correct value.

If your system does not have the `Sources_by_SourceType` watchlist deployed, deploy the watchlist to your Microsoft Sentinel workspace from the [ASIM watchlist deployment template](https://aka.ms/DeployASimWatchlists) on GitHub.