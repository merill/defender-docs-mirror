---
layout: Conceptual
title: The Advanced Security Information Model (ASIM) DNS normalization schema reference | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/normalization-schema-dns
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
description: This article describes the Microsoft Sentinel DNS normalization schema.
ms.author: edbaynash
author: EdB-MSFT
ms.topic: reference
ms.date: 2026-09-16T00:00:00.0000000Z
locale: en-us
document_id: 3b4d1a8b-a4b3-cbd7-6496-89c5a51624bc
document_version_independent_id: ab96d02f-4b41-ce99-5898-ad865d8853db
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/normalization-schema-dns.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/normalization-schema-dns
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/normalization-schema-dns.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 2f1fea37-36d2-c74d-d454-012ef17175c4
---

# The Advanced Security Information Model (ASIM) DNS normalization schema reference | Microsoft Learn

The DNS information model is used to describe events reported by a DNS server or a DNS security system, and is used by Microsoft Sentinel to enable source-agnostic analytics.

For more information, see [Normalization and the Advanced Security Information Model (ASIM)](normalization).

## Schema overview

The ASIM DNS schema represents DNS protocol activity. Both DNS servers and devices sending DNS requests to a DNS server log DNS activity. The DNS protocol activity includes DNS queries, DNS server updates, and DNS bulk data transfers. Since the schema represents protocol activity, it's governed by RFCs and officially assigned parameter lists, which are referenced in this article when appropriate. The DNS schema doesn't represent DNS server audit events.

The most important activity reported by DNS servers is a DNS query, for which the `EventType` field is set to `Query`.

The most important fields in a DNS event are:

- DnsQuery, which reports the domain name for which the query was issued.
- The SrcIpAddr (aliased to IpAddr), which represents the IP address from which the request was generated. DNS servers typically provide the SrcIpAddr field, but DNS clients sometimes don't provide this field and only provide the SrcHostname field.
- EventResultDetails, which reports whether the request was successful and if not, why.
- When available, DnsResponseName, which holds the answer provided by the server to the query. ASIM doesn't require parsing the response, and its format varies between sources.

    To use this field in source-agnostic content, search the content with the `has` or `contains` operators.

DNS events collected on client device may also include User and Process information.

## Guidelines for collecting DNS events

DNS is a unique protocol in that it may cross a large number of computers. Also, since DNS uses UDP, requests and responses are de-coupled and aren't directly related to each other.

The following image shows a simplified DNS request flow, including four segments. A real-world request can be more complex, with more segments involved.

![Simplified DNS request flow.](media/normalization/dns-request-flow.png)

Since request and response segments aren't directly connected to each other in the DNS request flow, full logging can result in significant duplication.

The most valuable segment to log is the response to the client. The response provides the domain name queries, the lookup result, and the IP address of the client. While many DNS systems log only this segment, there is value in logging the other parts. For example, a DNS cache poisoning attack often takes advantage of fake responses from an upstream server.

If your data source supports full DNS logging and you've chosen to log multiple segments, adjust your queries to prevent data duplication in Microsoft Sentinel.

For example, you might modify your query with the following normalization:

```kusto
_Im_Dns | where SrcIpAddr != "127.0.0.1" and EventSubType == "response"
```

## Parsers

For more information about ASIM parsers, see the [ASIM parsers overview](normalization-parsers-overview).

### Out-of-the-box parsers

To use parsers that unify all ASIM out-of-the-box parsers, and ensure that your analysis runs across all the configured sources, use the unifying parser `_Im_Dns` as the table name in your query.

For the list of the DNS parsers Microsoft Sentinel provides out-of-the-box refer to the [ASIM parsers list](normalization-parsers-list#dns-parsers).

### Add your own normalized parsers

When implementing custom parsers for the Dns information model, name your KQL functions using the format `vimDns<vendor><Product>`. Refer to the article [Managing ASIM parsers](normalization-manage-parsers) to learn how to add your custom parsers to the DNS unifying parser.

### Filtering parser parameters

The DNS parsers support [filtering parameters](normalization-about-parsers#optimizing-parsing-using-parameters). While these parameters are optional, they can improve your query performance.

The following filtering parameters are available:

| Name | Type | Description |
| --- | --- | --- |
| **starttime** | datetime | Filter only DNS queries that ran at or after this time. This parameter filters on the `TimeGenerated` field, which is the standard designator for the time of the event, regardless of the parser-specific mapping of the EventStartTime and EventEndTime fields. |
| **endtime** | datetime | Filter only DNS queries that finished running at or before this time. This parameter filters on the `TimeGenerated` field, which is the standard designator for the time of the event, regardless of the parser-specific mapping of the EventStartTime and EventEndTime fields. |
| **srcipaddr** | string | Filter only DNS queries from this source IP address. |
| **domain\_has\_any** | dynamic/string | Filter only DNS queries where the `domain` (or `query`) has any of the listed domain names, including as part of the event domain. The length of the list is limited to 10,000 items. |
| **responsecodename** | string | Filter only DNS queries for which the response code name matches the provided value. For example: `NXDOMAIN` |
| **response\_has\_ipv4** | string | Filter only DNS queries in which the response field includes the provided IP address or IP address prefix. Use this parameter when you want to filter on a single IP address or prefix. Results aren't returned for sources that don't provide a response. |
| **response\_has\_any\_prefix** | dynamic | Filter only DNS queries in which the response field includes any of the listed IP addresses or IP address prefixes. Prefixes should end with a `.`, for example: `10.0.`. Use this parameter when you want to filter on a list of IP addresses or prefixes. Results aren't returned for sources that don't provide a response. The length of the list is limited to 10,000 items. |
| **eventtype** | string | Filter only DNS queries of the specified type. If no value is specified, only lookup queries are returned. |

For example, to filter only DNS queries from the last day that failed to resolve the domain name, use:

```kusto
_Im_Dns (responsecodename = 'NXDOMAIN', starttime = ago(1d), endtime=now())
```

To filter only DNS queries for a specified list of domain names, use:

```kusto
let torProxies=dynamic(["tor2web.org", "tor2web.com", "torlink.co"]);
_Im_Dns (domain_has_any = torProxies)
```

Some parameter can accept both list of values of type `dynamic` or a single string value. To pass a literal list to parameters that expect a dynamic value, explicitly use a [dynamic literal](/en-us/kusto/query/scalar-data-types/dynamic?view=microsoft-sentinel&amp;preserve-view=true#dynamic-literals). For example: `dynamic(['192.168.','10.'])`

## Normalized content

For a full list of analytics rules that use normalized DNS events, see [DNS query security content](normalization-content#dns-query-security-content).

## Schema details

The DNS information model is aligned with the [OSSEM DNS entity schema](https://github.com/OTRF/OSSEM/blob/master/docs/cdm/entities/dns.md).

For more information, see the [Internet Assigned Numbers Authority (IANA) DNS parameter reference](https://www.iana.org/assignments/dns-parameters/dns-parameters.xhtml).

### Common ASIM fields

Important

Fields common to all schemas are described in detail in the [ASIM Common Fields](normalization-common-fields) article.

#### Common fields with specific guidelines

The following list mentions fields that have specific guidelines for DNS events:

| **Field** | **Class** | **Type** | **Description** |
| --- | --- | --- | --- |
| **EventType** | Mandatory | Enumerated | Indicates the operation reported by the record.  For DNS records, this value would be the [DNS op code](https://www.iana.org/assignments/dns-parameters/dns-parameters.xhtml). Example: `Query` |
| **EventSubType** | Optional | Enumerated | Either `request` or `response`. For most sources, only the responses are logged, and therefore the value is often **response**. |
| **EventResultDetails** | Mandatory | Enumerated | For DNS events, this field provides the [DNS response code](https://www.iana.org/assignments/dns-parameters/dns-parameters.xhtml). **Notes**:- IANA doesn't define the case for the values, so analytics must normalize the case. - If the source provides only a numerical response code and not a response code name, the parser must include a lookup table to enrich with this value. - If this record represents a request and not a response, set to **NA**. Example: `NXDOMAIN` |
| **EventSchemaVersion** | Mandatory | SchemaVersion (String) | The version of the schema documented here is **1.0.0**. |
| **EventSchema** | Mandatory | Enumerated | The name of the schema documented here is **Dns**. |
| **Dvc** fields | - | - | For DNS events, device fields refer to the system that reports the DNS event. |

#### All common fields

Fields that appear in the table below are common to all ASIM schemas. Any guideline specified above overrides the general guidelines for the field. For example, a field might be optional in general, but mandatory for a specific schema. For further details on each field, see the [ASIM Common Fields](normalization-common-fields) article.

| **Class** | **Fields** |
| --- | --- |
| Mandatory | - [EventCount](normalization-common-fields#eventcount) - [EventStartTime](normalization-common-fields#eventstarttime) - [EventEndTime](normalization-common-fields#eventendtime) - [EventType](normalization-common-fields#eventtype)- [EventResult](normalization-common-fields#eventresult) - [EventProduct](normalization-common-fields#eventproduct) - [EventVendor](normalization-common-fields#eventvendor) - [EventSchema](normalization-common-fields#eventschema) - [EventSchemaVersion](normalization-common-fields#eventschemaversion) - [Dvc](normalization-common-fields#dvc) |
| Recommended | - [EventResultDetails](normalization-common-fields#eventresultdetails)- [EventSeverity](normalization-common-fields#eventseverity)- [EventUid](normalization-common-fields#eventuid) - [DvcIpAddr](normalization-common-fields#dvcipaddr) - [DvcHostname](normalization-common-fields#dvchostname) - [DvcDomain](normalization-common-fields#dvcdomain)- [DvcDomainType](normalization-common-fields#dvcdomaintype)- [DvcFQDN](normalization-common-fields#dvcfqdn)- [DvcId](normalization-common-fields#dvcid)- [DvcIdType](normalization-common-fields#dvcidtype)- [DvcAction](normalization-common-fields#dvcaction) |
| Optional | - [EventMessage](normalization-common-fields#eventmessage) - [EventSubType](normalization-common-fields#eventsubtype)- [EventOriginalUid](normalization-common-fields#eventoriginaluid)- [EventOriginalType](normalization-common-fields#eventoriginaltype)- [EventOriginalSubType](normalization-common-fields#eventoriginalsubtype)- [EventOriginalResultDetails](normalization-common-fields#eventoriginalresultdetails) - [EventOriginalSeverity](normalization-common-fields#eventoriginalseverity) - [EventProductVersion](normalization-common-fields#eventproductversion) - [EventReportUrl](normalization-common-fields#eventreporturl) - [EventOwner](normalization-common-fields#eventowner)- [DvcZone](normalization-common-fields#dvczone)- [DvcMacAddr](normalization-common-fields#dvcmacaddr)- [DvcOs](normalization-common-fields#dvcos)- [DvcOsVersion](normalization-common-fields#dvchostname)- [DvcOriginalAction](normalization-common-fields#dvcoriginalaction)- [DvcInterface](normalization-common-fields#dvcinterface)- [AdditionalFields](normalization-common-fields#additionalfields)- [DvcDescription](normalization-common-fields#dvcdescription)- [DvcScopeId](normalization-common-fields#dvcscopeid)- [DvcScope](normalization-common-fields#dvcscope) |

### Source system fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **Src** | Alias | String | A unique identifier of the source device. This field can alias the SrcDvcId, SrcHostname, or SrcIpAddr fields. Example: `192.168.12.1` |
| **SrcIpAddr** | Recommended | IP Address | The IP address of the client that sent the DNS request. For a recursive DNS request, this value would typically be the reporting device, and in most cases set to `127.0.0.1`. Example: `192.168.12.1` |
| **SrcPortNumber** | Optional | Integer | Source port of the DNS query.Example: `54312` |
| **IpAddr** | Alias |  | Alias to SrcIpAddr |
| **SrcGeoCountry** | Optional | Country | The country/region associated with the source IP address.Example: `USA` |
| **SrcGeoRegion** | Optional | Region | The region associated with the source IP address.Example: `Vermont` |
| **SrcGeoCity** | Optional | City | The city associated with the source IP address.Example: `Burlington` |
| **SrcGeoLatitude** | Optional | Latitude | The latitude of the geographical coordinate associated with the source IP address.Example: `44.475833` |
| **SrcGeoLongitude** | Optional | Longitude | The longitude of the geographical coordinate associated with the source IP address.Example: `73.211944` |
| **SrcRiskLevel** | Optional | Integer | The risk level associated with the source. The value should be adjusted to a range of `0` to `100`, with `0` for benign and `100` for a high risk.Example: `90` |
| **SrcOriginalRiskLevel** | Optional | String | The risk level associated with the source, as reported by the reporting device. Example: `Suspicious` |
| **SrcHostname** | Recommended | Hostname (String) | The source device hostname, excluding domain information.Example: `DESKTOP-1282V4D` |
| **Hostname** | Alias |  | Alias to SrcHostname |
| **SrcDomain** | Recommended | Domain (String) | The domain of the source device.Example: `Contoso` |
| **SrcDomainType** | Conditional | Enumerated | The type of SrcDomain, if known. Possible values include:- `Windows` (such as: `contoso`)- `FQDN` (such as: `microsoft.com`)Required if SrcDomain is used. |
| **SrcFQDN** | Optional | FQDN (String) | The source device hostname, including domain information when available. **Note**: This field supports both traditional FQDN format and Windows domain\hostname format. The SrcDomainType field reflects the format used. Example: `Contoso\DESKTOP-1282V4D` |
| **SrcDvcId** | Optional | String | The ID of the source device as reported in the record.For example: `ac7e9755-8eae-4ffc-8a02-50ed7a2216c3` |
| **SrcDvcScopeId** | Optional | String | The cloud platform scope ID the device belongs to. **SrcDvcScopeId** map to a subscription ID on Azure and to an account ID on AWS. |
| **SrcDvcScope** | Optional | String | The cloud platform scope the device belongs to. **SrcDvcScope** map to a subscription ID on Azure and to an account ID on AWS. |
| **SrcDvcIdType** | Conditional | Enumerated | The type of SrcDvcId, if known. Possible values include: - `AzureResourceId`- `MDEid`If multiple IDs are available, use the first one from the list, and store the others in the **SrcDvcAzureResourceId** and **SrcDvcMDEid**, respectively.**Note**: This field is required if SrcDvcId is used. |
| **SrcDeviceType** | Optional | Enumerated | The type of the source device. Possible values include:- `Computer`- `Mobile Device`- `IOT Device`- `Other` |
| **SrcDescription** | Optional | String | A descriptive text associated with the device. For example: `Primary Domain Controller`. |

### Source user fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **SrcUserId** | Optional | String | A machine-readable, alphanumeric, unique representation of the source user. For more information, and for alternative fields for additional IDs, see [The User entity](normalization-entity-user). Example: `S-1-12-1-4141952679-1282074057-627758481-2916039507` |
| **SrcUserScope** | Optional | String | The scope, such as Microsoft Entra tenant, in which SrcUserId and SrcUsername are defined. or more information and list of allowed values, see [UserScope](normalization-entity-user#userscope) in the [Schema Overview article](normalization-about-schemas). |
| **SrcUserScopeId** | Optional | String | The scope ID, such as Microsoft Entra Directory ID, in which SrcUserId and SrcUsername are defined. for more information and list of allowed values, see [UserScopeId](normalization-entity-user#userscopeid) in the [Schema Overview article](normalization-about-schemas). |
| **SrcUserIdType** | Conditional | UserIdType | The type of the ID stored in the SrcUserId field. For more information and list of allowed values, see [UserIdType](normalization-entity-user#useridtype) in the [Schema Overview article](normalization-about-schemas). |
| **SrcUsername** | Optional | Username (String) | The source username, including domain information when available. For more information, see [The User entity](normalization-entity-user).Example: `AlbertE` |
| **SrcUsernameType** | Conditional | UsernameType | Specifies the type of the user name stored in the SrcUsername field. For more information, and list of allowed values, see [UsernameType](normalization-entity-user#usernametype) in the [Schema Overview article](normalization-about-schemas). Example: `Windows` |
| **User** | Alias |  | Alias to SrcUsername |
| **SrcUserType** | Optional | UserType | The type of the source user. For more information, and list of allowed values, see [UserType](normalization-entity-user#usertype) in the [Schema Overview article](normalization-about-schemas).For example: `Guest` |
| **SrcUserSessionId** | Optional | String | The unique ID of the sign-in session of the Actor. Example: `102pTUgC3p8RIqHvzxLCHnFlg` |
| **SrcOriginalUserType** | Optional | String | The original source user type, if provided by the source. |

### Source process fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **SrcProcessName** | Optional | String | The file name of the process that initiated the DNS request. This name is typically considered to be the process name. Example: `C:\Windows\explorer.exe` |
| **Process** | Alias |  | Alias to the SrcProcessNameExample: `C:\Windows\System32\rundll32.exe` |
| **SrcProcessId** | Optional | String | The process ID (PID) of the process that initiated the DNS request.Example: `48610176`**Note**: The type is defined as *string* to support varying systems, but on Windows and Linux this value must be numeric. If you are using a Windows or Linux machine and used a different type, make sure to convert the values. For example, if you used a hexadecimal value, convert it to a decimal value. |
| **SrcProcessGuid** | Optional | GUID (String) | A generated unique identifier (GUID) of the process that initiated the DNS request.  Example: `EF3BD0BD-2B74-60C5-AF5C-010000001E00` |

### Destination system fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **Dst** | Alias | String | A unique identifier of the server that received the DNS request. This field may alias the DstDvcId, DstHostname, or DstIpAddr fields. Example: `192.168.12.1` |
| **DstIpAddr** | Optional | IP Address | The IP address of the server that received the DNS request. For a regular DNS request, this value would typically be the reporting device, and in most cases set to `127.0.0.1`.Example: `127.0.0.1` |
| **DstGeoCountry** | Optional | Country | The country/region associated with the destination IP address. For more information, see [Logical types](normalization-about-schemas#logical-types).Example: `USA` |
| **DstGeoRegion** | Optional | Region | The region, or state, associated with the destination IP address. For more information, see [Logical types](normalization-about-schemas#logical-types).Example: `Vermont` |
| **DstGeoCity** | Optional | City | The city associated with the destination IP address. For more information, see [Logical types](normalization-about-schemas#logical-types).Example: `Burlington` |
| **DstGeoLatitude** | Optional | Latitude | The latitude of the geographical coordinate associated with the destination IP address. For more information, see [Logical types](normalization-about-schemas#logical-types).Example: `44.475833` |
| **DstGeoLongitude** | Optional | Longitude | The longitude of the geographical coordinate associated with the destination IP address. For more information, see [Logical types](normalization-about-schemas#logical-types).Example: `73.211944` |
| **DstRiskLevel** | Optional | Integer | The risk level associated with the destination. The value should be adjusted to a range of 0 to 100, which 0 being benign and 100 being a high risk.Example: `90` |
| **DstOriginalRiskLevel** | Optional | String | The risk level associated with the destination, as reported by the reporting device. Example: `Malicious` |
| **DstPortNumber** | Optional | Integer | Destination Port number.Example: `53` |
| **DstHostname** | Optional | Hostname (String) | The destination device hostname, excluding domain information. If no device name is available, store the relevant IP address in this field.Example: `DESKTOP-1282V4D`**Note**: This value is mandatory if DstIpAddr is specified. |
| **DstDomain** | Optional | Domain (String) | The domain of the destination device.Example: `Contoso` |
| **DstDomainType** | Conditional | Enumerated | The type of DstDomain, if known. Possible values include:- `Windows (contoso\mypc)`- `FQDN (learn.microsoft.com)`Required if DstDomain is used. |
| **DstFQDN** | Optional | FQDN (String) | The destination device hostname, including domain information when available. Example: `Contoso\DESKTOP-1282V4D`**Note**: This field supports both traditional FQDN format and Windows domain\hostname format. The DstDomainType reflects the format used. |
| **DstDvcId** | Optional | String | The ID of the destination device as reported in the record.Example: `ac7e9755-8eae-4ffc-8a02-50ed7a2216c3` |
| **DstDvcScopeId** | Optional | String | The cloud platform scope ID the device belongs to. **DstDvcScopeId** map to a subscription ID on Azure and to an account ID on AWS. |
| **DstDvcScope** | Optional | String | The cloud platform scope the device belongs to. **DstDvcScope** map to a subscription ID on Azure and to an account ID on AWS. |
| **DstDvcIdType** | Conditional | Enumerated | The type of DstDvcId, if known. Possible values include: - `AzureResourceId`- `MDEidIf`If multiple IDs are available, use the first one from the list above, and store the others in the **DstDvcAzureResourceId** or **DstDvcMDEid** fields, respectively.Required if **DstDeviceId** is used. |
| **DstDeviceType** | Optional | Enumerated | The type of the destination device. Possible values include:- `Computer`- `Mobile Device`- `IOT Device`- `Other` |
| **DstDescription** | Optional | String | A descriptive text associated with the device. For example: `Primary Domain Controller`. |

### DNS specific fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **DnsQuery** | Mandatory | String | The domain that the request tries to resolve. **Notes**: - Some sources send valid FQDN queries in a different format. For example, in the DNS protocol itself, the query includes a dot (**.**) at the end, which must be removed.- While the DNS protocol limits the type of value in this field to an FQDN, most DNS servers allow any value, and this field is therefore not limited to FQDN values only. Most notably, DNS tunneling attacks may use invalid FQDN values in the query field.- While the DNS protocol allows for multiple queries in a single request, this scenario is rare, if it's found at all. If the request has multiple queries, store the first one in this field, and then and optionally keep the rest in the [AdditionalFields](normalization-common-fields#additionalfields) field.Example: `www.malicious.com` |
| **Domain** | Alias |  | Alias to DnsQuery. |
| **DnsQueryType** | Optional | Integer | The [DNS Resource Record Type codes](https://www.iana.org/assignments/dns-parameters/dns-parameters.xhtml). Example: `28` |
| **DnsQueryTypeName** | Recommended | Enumerated | The [DNS Resource Record Type](https://www.iana.org/assignments/dns-parameters/dns-parameters.xhtml) names. **Notes**: - IANA doesn't define the case for the values, so analytics must normalize the case as needed.- The value `ANY` is supported for the response code 255. - The value `TYPExxxx` is supported for unmapped response codes, where `xxxx` is the numerical value of the response code, as reported by the BIND DNS server. -If the source provides only a numerical query type code and not a query type name, the parser must include a lookup table to enrich with this value.Example: `AAAA` |
| **DnsResponseName** | Optional | String | The content of the response, as included in the record. The DNS response data is inconsistent across reporting devices, is complex to parse, and has less value for source-agnostic analytics. Therefore the information model doesn't require parsing and normalization, and Microsoft Sentinel uses an auxiliary function to provide response information. For more information, see Handling DNS response. |
| **DnsResponseCodeName** | Alias |  | Alias to EventResultDetails |
| **DnsResponseCode** | Optional | Integer | The [DNS numerical response code](https://www.iana.org/assignments/dns-parameters/dns-parameters.xhtml). Example: `3` |
| **TransactionIdHex** | Recommended | Hexadecimal (String) | The DNS query unique ID as assigned by the DNS client, in hexadecimal format. Note that this value is part of the DNS protocol and different from DnsSessionId, the network layer session ID, typically assigned by the reporting device. |
| **NetworkProtocol** | Optional | Enumerated | The transport protocol used by the network resolution event. The value can be **UDP** or **TCP**, and is most commonly set to **UDP** for DNS. Example: `UDP` |
| **NetworkProtocolVersion** | Optional | Enumerated | The version of NetworkProtocol. When using it to distinguish between IP version, use the values `IPv4` and `IPv6`. |
| **DnsQueryClass** | Optional | Integer | The [DNS class ID](https://www.iana.org/assignments/dns-parameters/dns-parameters.xhtml).In practice, only the **IN** class (ID 1) is used, and therefore this field is less valuable. |
| **DnsQueryClassName** | Recommended | DnsQueryClassName (String) | The [DNS class name](https://www.iana.org/assignments/dns-parameters/dns-parameters.xhtml).In practice, only the **IN** class (ID 1) is used, and therefore this field is less valuable.Example: `IN` |
| **DnsFlags** | Optional | String | The flags field, as provided by the reporting device. If flag information is provided in multiple fields, concatenate them with comma as a separator. Since DNS flags are complex to parse and are less often used by analytics, parsing, and normalization aren't required. Microsoft Sentinel can use an auxiliary function to provide flags information. For more information, see Handling DNS response. Example: `["DR"]` |
| **DnsNetworkDuration** | Optional | Integer | The amount of time, in milliseconds, for the completion of DNS request.Example: `1500` |
| **Duration** | Alias |  | Alias to DnsNetworkDuration |
| **DnsFlagsAuthenticated** | Optional | Boolean | The DNS `AD` flag, which is related to DNSSEC, indicates in a response that all data included in the answer and authority sections of the response have been verified by the server according to the policies of that server. For more information, see [RFC 3655 Section 6.1](https://tools.ietf.org/html/rfc3655#section-6.1) for more information. |
| **DnsFlagsAuthoritative** | Optional | Boolean | The DNS `AA` flag indicates whether the response from the server was authoritative |
| **DnsFlagsCheckingDisabled** | Optional | Boolean | The DNS `CD` flag, which is related to DNSSEC, indicates in a query that non-verified data is acceptable to the system sending the query. For more information, see [RFC 3655 Section 6.1](https://tools.ietf.org/html/rfc3655#section-6.1) for more information. |
| **DnsFlagsRecursionAvailable** | Optional | Boolean | The DNS `RA` flag indicates in a response that that server supports recursive queries. |
| **DnsFlagsRecursionDesired** | Optional | Boolean | The DNS `RD` flag indicates in a request that that client would like the server to use recursive queries. |
| **DnsFlagsTruncated** | Optional | Boolean | The DNS `TC` flag indicates that a response was truncated as it exceeded the maximum response size. |
| **DnsFlagsZ** | Optional | Boolean | The DNS `Z` flag is a deprecated DNS flag, which might be reported by older DNS systems. |
| **DnsSessionId** | Optional | string | The DNS session identifier as reported by the reporting device. This value is different from TransactionIdHex, the DNS query unique ID as assigned by the DNS client.Example: `EB4BFA28-2EAD-4EF7-BC8A-51DF4FDF5B55` |
| **SessionId** | Alias |  | Alias to DnsSessionId |
| **DnsResponseIpCountry** | Optional | Country | The country/region associated with one of the IP addresses in the DNS response. For more information, see [Logical types](normalization-about-schemas#logical-types).Example: `USA` |
| **DnsResponseIpRegion** | Optional | Region | The region, or state, associated with one of the IP addresses in the DNS response. For more information, see [Logical types](normalization-about-schemas#logical-types).Example: `Vermont` |
| **DnsResponseIpCity** | Optional | City | The city associated with one of the IP addresses in the DNS response. For more information, see [Logical types](normalization-about-schemas#logical-types).Example: `Burlington` |
| **DnsResponseIpLatitude** | Optional | Latitude | The latitude of the geographical coordinate associated with one of the IP addresses in the DNS response. For more information, see [Logical types](normalization-about-schemas#logical-types).Example: `44.475833` |
| **DnsResponseIpLongitude** | Optional | Longitude | The longitude of the geographical coordinate associated with one of the IP addresses in the DNS response. For more information, see [Logical types](normalization-about-schemas#logical-types).Example: `73.211944` |

### Inspection fields

The following fields are used to represent an inspection, which a DNS security device performed. The threat related fields represent a single threat that is associated with either the source address, the destination address, one of the IP addresses in the response or the DNS query domain. If more than one threat was identified as a threat, information about other IP addresses can be stored in the field `AdditionalFields`.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **UrlCategory** | Optional | String | A DNS event source may also look up the category of the requested Domains. The field is called **UrlCategory** to align with the Microsoft Sentinel network schema. **DomainCategory** is added as an alias that's fitting to DNS. Example: `Educational \\ Phishing` |
| **DomainCategory** | Alias |  | Alias to UrlCategory. |
| **RuleName** | Optional | String | The name or ID of the rule which identified the threat. Example: `AnyAnyDrop` |
| **RuleNumber** | Optional | Integer | The number of the rule which identified the threat.Example: `23` |
| **Rule** | Alias | String | Either the value of RuleName or the value of RuleNumber. If the value of RuleNumber is used, the type should be converted to string. |
| **RuleNumber** | Optional | int | The number of the rule associated with the alert.e.g. `123456` |
| **RuleName** | Optional | string | The name or ID of the rule associated with the alert.e.g. `Server PSEXEC Execution via Remote Access` |
| **ThreatId** | Optional | String | The ID of the threat or malware identified in the network session.Example: `Tr.124` |
| **ThreatCategory** | Optional | String | If a DNS event source also provides DNS security, it may also evaluate the DNS event. For example, it can search for the IP address or domain in a threat intelligence database, and assign the domain or IP address with a Threat Category. |
| **ThreatIpAddr** | Optional | IP Address | An IP address for which a threat was identified. The field ThreatField contains the name of the field **ThreatIpAddr** represents. If a threat is identified in the Domain field, this field should be empty. |
| **ThreatField** | Conditional | Enumerated | The field for which a threat was identified. The value is either `SrcIpAddr`, `DstIpAddr`, `Domain`, or `DnsResponseName`. |
| **ThreatName** | Optional | String | The name of the threat identified, as reported by the reporting device. |
| **ThreatConfidence** | Optional | ConfidenceLevel (Integer) | The confidence level of the threat identified, normalized to a value between 0 and a 100. |
| **ThreatOriginalConfidence** | Optional | String | The original confidence level of the threat identified, as reported by the reporting device. |
| **ThreatRiskLevel** | Optional | RiskLevel (Integer) | The risk level associated with the threat identified, normalized to a value between 0 and a 100. |
| **ThreatOriginalRiskLevel** | Optional | String | The original risk level associated with the threat identified, as reported by the reporting device. |
| **ThreatIsActive** | Optional | Boolean | True if the threat identified is considered an active threat. |
| **ThreatFirstReportedTime** | Optional | datetime | The first time the IP address or domain were identified as a threat. |
| **ThreatLastReportedTime** | Optional | datetime | The last time the IP address or domain were identified as a threat. |

### Deprecated aliases and fields

The following fields are aliases that are maintained for backwards compatibility. They were removed from the schema on December 31, 2021.

- `Query` (alias to `DnsQuery`)
- `QueryType` (alias to `DnsQueryType`)
- `QueryTypeName` (alias to `DnsQueryTypeName`)
- `ResponseName` (alias to `DnsResponseName`)
- `ResponseCodeName` (alias to `DnsResponseCodeName`)
- `ResponseCode` (alias to `DnsResponseCode`)
- `QueryClass` (alias to `DnsQueryClass`)
- `QueryClassName` (alias to `DnsQueryClassName`)
- `Flags` (alias to `DnsFlags`)
- `SrcUserDomain`

### Entity correlation fields

Note

Contributors don't need to populate these fields. Applicable parsers will populate them when internal Microsoft support is added.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **DstSystemEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the destination system within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **SrcProcessEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the source process within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **SrcSystemEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the source system within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **SrcUserAdditionalIds** | Optional | Dynamic | For the field structure and usage, see [Fields suffixed with AdditionalIds](normalization-common-fields#fields-suffixed-with-additionalids). |
| **SrcUserEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the source user within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |

## Schema updates

| Version | Changes |
| --- | --- |
| 0.1.2 | - Added the field `EventSchema`.- Added dedicated flag fields, which augment the combined **Flags** field: `DnsFlagsAuthoritative`, `DnsFlagsCheckingDisabled`, `DnsFlagsRecursionAvailable`, `DnsFlagsRecursionDesired`, `DnsFlagsTruncated`, and `DnsFlagsZ`. |
| 0.1.3 | - Explicitly documented the `Src*`, `Dst*`, `Process*`, and `User*` fields.- Added more `Dvc*` fields to match the latest common fields definition.- Added `Src` and `Dst` as aliases to a leading identifier for the source and destination systems.- Added the optional `DnsNetworkDuration` field and `Duration` as an alias to it.- Added optional geolocation and risk-level fields. |
| 0.1.4 | Added the optional fields `ThreatIpAddr`, `ThreatField`, `ThreatName`, `ThreatConfidence`, `ThreatOriginalConfidence`, `ThreatOriginalRiskLevel`, `ThreatIsActive`, `ThreatFirstReportedTime`, and `ThreatLastReportedTime`. |
| 0.1.5 | Added the fields `SrcUserScope`, `SrcUserSessionId`, `SrcDvcScopeId`, `SrcDvcScope`, `DstDvcScopeId`, `DstDvcScope`, `DvcScopeId`, and `DvcScope`. |
| 0.1.6 | Added the fields `DnsResponseIpCountry`, `DnsResponseIpRegion`, `DnsResponseIpCity`, `DnsResponseIpLatitude`, and `DnsResponseIpLongitude`. |
| 0.1.7 | Added the fields `SrcDescription`, `SrcOriginalRiskLevel`, `DstDescription`, `DstOriginalRiskLevel`, `SrcUserScopeId`, `NetworkProtocolVersion`, `Rule`, `RuleName`, `RuleNumber`, and `ThreatId`. |
| 1.0.0 | Added entity correlation fields. |

## Source-specific discrepancies

The goal of normalizing is to ensure that all sources provide consistent telemetry. A source that doesn't provide the required telemetry, such as mandatory schema fields, cannot be normalized. However, sources that typically provide all required telemetry, even if there are some discrepancies, can be normalized. Discrepancies may affect the completeness of query results.

The following table lists known discrepancies:

| Source | Discrepancies |
| --- | --- |
| Microsoft DNS Server Collected using the DNS connector and the Log Analytics Agent | The connector doesn't provide the mandatory DnsQuery field for original event ID 264 (Response to a dynamic update). The data is available at the source, but not forwarded by the connector. |
| Corelight Zeek | Corelight Zeek may not provide the mandatory DnsQuery field. We have observed such behavior in certain cases in which the DNS response code name is `NXDOMAIN`. |

## Handling DNS response

In most cases, logged DNS events don't include response information, which may be large and detailed. If your record includes more response information, store it in the ResponseName field as it appears in the record.

You can also provide an extra KQL function called `_imDNS<vendor>Response_`, which takes the unparsed response as input and returns dynamic value with the following structure:

```kusto
[
    {
        "part": "answer"
        "query": "yahoo.com."
        "TTL": 1782
        "Class": "IN"
        "Type": "A"
        "Response": "74.6.231.21"
    }
    {
        "part": "authority"
        "query": "yahoo.com."
        "TTL": 113066
        "Class": "IN"
        "Type": "NS"
        "Response": "ns5.yahoo.com"
    }
    ...
]
```

The fields in each dictionary in the dynamic value correspond to the fields in each DNS response. The `part` entry should include either `answer`, `authority`, or `additional` to reflect the part in the response that the dictionary belongs to.

Tip

To ensure optimal performance, call the `imDNS<vendor>Response` function only when needed, and only after an initial filtering to ensure better performance.

## Handling DNS flags

Parsing and normalization aren't required for flag data. Instead, store the flag data provided by the reporting device in the Flags field. If determining the value of individual flags is straight forward, you can also use the dedicated flags fields.

You can also provide an extra KQL function called `_imDNS<vendor>Flags_`, which takes the unparsed response, or dedicated flag fields, as input and returns a dynamic list, with Boolean values that represent each flag in the following order:

- Authenticated (AD)
- Authoritative (AA)
- Checking Disabled (CD)
- Recursion Available (RA)
- Recursion Desired (RD)
- Truncated (TC)
- Z