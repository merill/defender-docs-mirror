---
layout: Conceptual
title: Advanced Security Information Model (ASIM) helper functions | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/normalization-functions
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
description: This article outlines the Microsoft Sentinel Advanced Security Information Model (ASIM) helper functions.
ms.author: edbaynash
author: EdB-MSFT
ms.topic: reference
ms.date: 2021-06-07T00:00:00.0000000Z
locale: en-us
document_id: 22d723b3-1f6b-67ad-d982-0c9129e5e84c
document_version_independent_id: 7db04074-d724-ef1e-cb4c-11a4e1defb91
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/normalization-functions.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/normalization-functions
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/normalization-functions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
platformId: 8a63e29b-6221-f0ee-f68b-a7e3d6f49d96
---

# Advanced Security Information Model (ASIM) helper functions | Microsoft Learn

Advanced Security Information Model (ASIM) helper functions extend the KQL language providing functionality that helps interact with normalized data and in writing parsers.

## Enrichment lookup functions

Enrichment lookup functions provide an easy method of looking up known values, based on their numerical representation. Such functions are useful as events often use the short form numeric code, while users prefer the textual form. Most of the functions have two forms:

- The **lookup** version is a scalar function that accepts as input the numeric code and returns the textual form.

    Use the following KQL snippet with the **lookup** version:

    ```kusto
    | extend ProtocolName = _ASIM_LookupNetworkProtocol (ProtocolNumber)
    ```
- The **resolve** version is a tabular function that:

    - Is used as a KQL pipeline operator.
    - Accepts as input the name of the field holding the value to look up.
    - Sets the ASIM fields typically holding both the input value and the resulting lookup value.

    Use the following KQL snippet with the **resolve** version:

    ```kusto
    | invoke _ASIM_ResolveNetworkProtocol (`ProtocolNumber`)
    ```

    The function automatically populates the ASIM field with the result of the lookup.

The **resolve** version is preferable for use in ASIM parsers, while the **lookup** version is useful in general purpose queries. When an enrichment lookup function has to return more than one value, it will always use the **resolve** format.

For more information on scalar and tabular functions (represented by the lookup and resolve versions here, respectively), see [User-defined functions](/en-us/kusto/query/functions/user-defined-functions?view=microsoft-sentinel&amp;preserve-view=true) in the Kusto documentation.

### Lookup type functions

| Function | Input\* | Output | Description |
| --- | --- | --- | --- |
| **\_ASIM\_LookupDnsQueryType** | Numeric DNS query type code | Query type name | Translate a numeric DNS resource record (RR) type to its name, as defined by [IANA](https://www.iana.org/assignments/dns-parameters/dns-parameters.xhtml#dns-parameters-4) |
| **\_ASIM\_LookupDnsResponseCode** | Numeric DNS response code | Response code name | Translate a numeric DNS response code (RCODE) to its name, as defined by [IANA](https://www.iana.org/assignments/dns-parameters/dns-parameters.xhtml#dns-parameters-6) |
| **\_ASIM\_LookupICMPType** | Numeric ICMP type | ICMP type name | Translate a numeric ICMP type to its name, as defined by [IANA](https://www.iana.org/assignments/icmp-parameters/icmp-parameters.xhtml#icmp-parameters-types) |
| **\_ASIM\_LookupNetworkProtocol** | IP protocol number | IP protocol name | Translate a numeric IP protocol code to its name, as defined by [IANA](https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml) |
| **\_ASIM\_LookupHTTPStatusCode** | HTTP status code | HTTP status code name | Translate a numeric HTTP status code to its name, as defined by [IANA](https://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml). Also supports extended status codes used by IIS and other web servers. |
| **\_ASIM\_LookupAADcodes** | Microsoft Entra ID STS error code | Error category | Translate a Microsoft Entra ID STS error code to its error category, such as `Logon violates policy` or `No such user or password`. |

### Resolve type functions

The resolve format functions perform the same action as their lookup counterpart, but accept a field name, provided as a string constant, as input and set up predefined fields as output. The input value is also assigned to a predefined field.

| Function | Extended fields |
| --- | --- |
| **\_ASIM\_ResolveDnsQueryType** | - `DnsQueryType` for the input value - `DnsQueryTypeName` for the output value |
| **\_ASIM\_ResolveDnsResponseCode** | - `DnsResponseCode` for the input value - `DnsResponseCodeName` for the output value |
| **\_ASIM\_ResolveICMPType** | - `NetworkIcmpCode` for the input value - `NetworkIcmpType` for the lookup value |
| **\_ASIM\_ResolveNetworkProtocol** | - `NetworkProtocolNumber` for the input value- `NetworkProtocol` for the lookup value |

## Parser helper functions

The following functions perform tasks which are common in parsers and useful to accelerate parser development.

### Device resolution functions

The device resolution functions analyze a hostname and determine whether it has domain information and the type of domain notation. The functions then populate the relevant ASIM fields representing a device. All the functions are resolve type functions and accept the name of the field containing the hostname, represented as a string, as input.

| Function | Extended fields | Description |
| --- | --- | --- |
| **\_ASIM\_ResolveFQDN** | - `ExtractedHostname` - `Domain` - `DomainType` - `FQDN` | Analyzes the value in the field specified and set the output fields accordingly. For more information, see [example](normalization-develop-parsers#resolvefqnd) in the article about developing parsers. |
| **\_ASIM\_ResolveSrcFQDN** | - `SrcHostname` - `SrcDomain` - `SrcDomainType` - `SrcFQDN` | Similar to `_ASIM_ResolveFQDN`, but sets the `Src` fields |
| **\_ASIM\_ResolveDstFQDN** | - `DstHostname` - `DstDomain` - `DstDomainType` - `DstFQDN` | Similar to `_ASIM_ResolveFQDN`, but sets the `Dst` fields |
| **\_ASIM\_ResolveDvcFQDN** | - `DvcHostname` - `DvcDomain` - `DvcDomainType` - `DvcFQDN` | Similar to `_ASIM_ResolveFQDN`, but sets the `Dvc` fields |

### User type functions

The user type functions help determine the type of user based on username patterns or security identifiers (SIDs).

| Function | Input | Output | Description |
| --- | --- | --- | --- |
| **\_ASIM\_GetUsernameType** | Username string | Username type | Returns the username type based on the format of the username. Possible values include `UPN` (for email-like usernames), `Windows` (for domain\user format), `DN` (for distinguished names), `Simple`, or empty if the username is empty. |
| **\_ASIM\_GetWindowsUserType** | Username string, SID string | User type | Returns the user type for Windows systems based on the username and security identifier (SID). Possible values include `Admin`, `Guest`, `Service`, `Machine`, `System`, `Anonymous`, `Regular`, or `Other`. |
| **\_ASIM\_GetUserType** | Username string, SID string | User type | **Deprecated.** Use `_ASIM_GetWindowsUserType` instead. Sets the UserType in Windows systems based on the username and SID. |

### Source identification functions

The **\_ASIM\_GetSourceBySourceType** function retrieves the list of sources associated with a source type provided as input from the `SourceBySourceType` Watchlist. The function is intended for use by parsers writers. For more information, see [Filtering by source type using a Watchlist](normalization-develop-parsers#filtering-by-source-type-using-a-watchlist).

The **\_ASIM\_GetDisabledParsers** function reads the `ASimDisabledParsers` watchlist and determines based on it whether the parser provided as a parameter is disabled. This function is used internally by ASIM parsers to support disabling specific parsers.

### Watchlist functions

The watchlist functions provide optimized methods for reading watchlists in ASIM parsers.

| Function | Input | Output | Description |
| --- | --- | --- | --- |
| **\_ASIM\_GetWatchlistRaw** | Watchlist alias (string), optional keys (dynamic array) | Watchlist items | Reads a single watchlist in raw format. More performant than the general `_GetWatchlist` function. |
| **\_ASIM\_GetWatchlistsRaw** | Watchlist aliases (dynamic array), optional keys (dynamic array) | Watchlist items | Reads multiple watchlists in raw format. The primary use case is providing an option for using multiple watchlist names for the same watchlist. |

## Identity enrichment functions

Identity enrichment functions help enrich your data with user information from the UEBA IdentityInfo table.

| Function | Input | Output | Description |
| --- | --- | --- | --- |
| **\_ASIM\_IdentityInfo** | None | Normalized IdentityInfo table | Deduplicates and normalizes the [IdentityInfo table](ueba-reference#identityinfo-table) to improve its usability in queries. Returns a deduplicated table with ASIM-normalized field names. |
| **\_ASIM\_Enrich\_IdentityInfo** | Input table, field name parameters | Enriched table | Enriches your result set with user information from the [IdentityInfo table](ueba-reference#identityinfo-table). Use the parameters to specify which field to use for matching: `AadIdField`, `TenantIdField`, `SidField`, `UpnField`, or `EmailField`. |