---
layout: Conceptual
title: The Advanced Security Information Model (ASIM) Web Session normalization schema reference | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/normalization-schema-web
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
description: This article displays the Microsoft Sentinel Web Session normalization schema.
services: sentinel
cloud: na
ms.author: edbaynash
author: EdB-MSFT
ms.topic: reference
ms.date: 2026-09-18T00:00:00.0000000Z
locale: en-us
document_id: aa468ce0-4158-3ff1-69c6-6141134fe962
document_version_independent_id: de6421e3-cfbc-f4c6-e663-e34caaff4874
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/normalization-schema-web.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/normalization-schema-web
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/normalization-schema-web.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 4ec4df4f-3aa4-4b99-c110-8da4947ac60a
---

# The Advanced Security Information Model (ASIM) Web Session normalization schema reference | Microsoft Learn

The Web Session normalization schema is used to describe an IP network activity. For example, IP network activities are reported by web servers, web proxies, and web security gateways.

For more information about normalization in Microsoft Sentinel, see [Normalization and the Advanced Security Information Model (ASIM)](normalization).

## Schema overview

The Web Session normalization schema represents any HTTP network session, and is suitable to provide support for common source types, including:

- Web servers
- Web proxies
- Web security gateways

The ASIM Web Session schema represents HTTP and HTTPS protocol activity. Since the schema represents protocol activity, it is governed by RFCs and officially assigned parameter lists, which are referenced in this article when appropriate.

The Web Session schema doesn't represent audit events from source devices. For example, an event modifying a Web Security Gateway policy can't be represented by the Web Session schema.

Since HTTP sessions are application layer sessions that utilize TCP/IP as the underlying network layer session, the Web Session schema is a super set of the [ASIM Network Session schema](normalization-schema-network).

The most important fields in a Web Session schema are:

- Url, which reports the url that the client requested from the server.
- The [SrcIpAddr](normalization-schema-network#srcipaddr) (aliased to [IpAddr](normalization-schema-network#ipaddr)), which represents the IP address from which the request was generated.
- EventResultDetails field, which typically reports the HTTP Status Code.

Web Session events may also include [User](normalization-schema-network#user) and [Process](normalization-schema-process-event) information for the user and process initiating the request.

## Parsers

For more information about ASIM parsers, see the [ASIM parsers overview](normalization-parsers-overview).

### Unifying parsers

To use parsers that unify all ASIM out-of-the-box parsers, and ensure that your analysis runs across all the configured sources, use the `_Im_WebSession` parser.

### Out-of-the-box, source-specific parsers

For the list of the Web Session parsers Microsoft Sentinel provides out-of-the-box refer to the [ASIM parsers list](normalization-parsers-list#web-session-parsers)

### Add your own normalized parsers

When implementing custom parsers for the Web Session information model, name your KQL functions using the following syntax:

- `vimWebSession<vendor><Product>` for parametrized parsers
- `ASimWebSession<vendor><Product>` for regular parsers

### Filtering parser parameters

The `im` and `vim*` parsers support [filtering parameters](normalization-about-parsers#). While these parsers are optional, they can improve your query performance.

The following filtering parameters are available:

| Name | Type | Description |
| --- | --- | --- |
| **starttime** | datetime | Filter only Web sessions that **started** at or after this time. This parameter filters on the `TimeGenerated` field, which is the standard designator for the time of the event, regardless of the parser-specific mapping of the EventStartTime and EventEndTime fields. |
| **endtime** | datetime | Filter only Web sessions that **started** running at or before this time. This parameter filters on the `TimeGenerated` field, which is the standard designator for the time of the event, regardless of the parser-specific mapping of the EventStartTime and EventEndTime fields. |
| **srcipaddr\_has\_any\_prefix** | dynamic | Filter only Web sessions for which the [source IP address field](normalization-schema-network#srcipaddr) prefix is in one of the listed values. The list of values can include IP addresses and IP address prefixes. Prefixes should end with a `.`, for example: `10.0.`. The length of the list is limited to 10,000 items. |
| **ipaddr\_has\_any\_prefix** | dynamic | Filter only network sessions for which the [destination IP address field](normalization-schema-network#dstipaddr) or [source IP address field](normalization-schema-network#srcipaddr) prefix is in one of the listed values. Prefixes should end with a `.`, for example: `10.0.`. The length of the list is limited to 10,000 items.The field [ASimMatchingIpAddr](normalization-schema-network#asimmatchingipaddr) is set with the one of the values `SrcIpAddr`, `DstIpAddr`, or `Both` to reflect the matching fields or fields. |
| **url\_has\_any** | dynamic | Filter only Web sessions for which the URL field has any of the values listed. The parser may ignore the schema of the URL passed as a parameter, if the source does not report it. If specified, and the session is not a web session, no result will be returned. The length of the list is limited to 10,000 items. |
| **httpuseragent\_has\_any** | dynamic | Filter only web sessions for which the user agent field has any of the values listed. If specified, and the session is not a web session, no result will be returned. The length of the list is limited to 10,000 items. |
| **eventresultdetails\_in** | dynamic | Filter only web sessions for which the HTTP status code, stored in the EventResultDetails field, is any of the values listed. |
| **eventresult** | string | Filter only network sessions with a specific **EventResult** value. |
| **eventresultdetails\_has\_any** | dynamic | Declared in the canonical Web Session parser parameters, but not currently applied or forwarded by the workspace-deployed `imWebSession` query. Use `eventresultdetails_in` to filter by HTTP status code. |

Some parameter can accept both list of values of type `dynamic` or a single string value. To pass a literal list to parameters that expect a dynamic value, explicitly use a [dynamic literal](/en-us/kusto/query/scalar-data-types/dynamic?view=microsoft-sentinel&amp;preserve-view=true#dynamic-literals). For example: `dynamic(['192.168.','10.'])`

For example, to filter only Web sessions for a specified list of domain names, use:

```kusto
let torProxies=dynamic(["tor2web.org", "tor2web.com", "torlink.co"]);
_Im_WebSession (url_has_any = torProxies)
```

## Schema details

The Web Session information model is aligned with the [OSSEM Network entity schema](https://github.com/OTRF/OSSEM/blob/master/docs/cdm/entities/network.md) and the [OSSEM HTTP entity schema](https://github.com/OTRF/OSSEM/blob/master/docs/cdm/entities/http.md).

To conform with industry best practices, the Web Session schema uses the descriptors **Src** and **Dst** to identify the session source and destination devices, without including the token **Dvc** in the field name.

So, for example, the source device hostname and IP address are named **SrcHostname** and **SrcIpAddr** respectively, and not **Src*Dvc*Hostname** and **Src*Dvc*IpAddr**. The prefix **Dvc** is only used for the reporting or intermediary device, as applicable.

Fields that describe the user and application associated with the source and destination devices also use the **Src** and **Dst** descriptors.

Other ASIM schemas typically use **Target** instead of **Dst**.

### Common ASIM fields

Important

Fields common to all schemas are described in detail in the [ASIM Common Fields](normalization-common-fields) article.

#### Common fields with specific guidelines

The following list mentions fields that have specific guidelines for Web Session events:

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **EventType** | Mandatory | Enumerated | Describes the operation reported by the record. Allowed values are: - `HTTPsession`: Denotes a network session used for HTTP or HTTPS, typically reported by an intermediary device, such as a proxy or a Web security gateway. - `WebServerSession`: Denotes an HTTP request reported by a web server. Such an event typically has less network related information. The URL reported should not include a schema and a server name, but only the path and parameters part of the URL.  - `ApiRequest`: Denotes an HTTP request reported associated with an API call, typically reported by an application server. Such an event typically has less network related information. When reported by the application server, the URL reported should not include a schema and a server name, but only the path and parameters part of the URL. |
| **EventResult** | Mandatory | Enumerated | Describes the event result, normalized to one of the following values:  - `Success` - `Partial` - `Failure` - `NA` (not applicable) For an HTTP session, `Success` is defined as a status code lower than `400`, and `Failure` is defined as a status code higher than `400`. For a list of HTTP status codes, refer to [W3 Org](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html).The source may provide only a value for the EventResultDetails field, which must be analyzed to get the **EventResult** value. |
| **EventResultDetails** | Recommended | Enumerated | The HTTP status code as defined by [The World Wide Web Consortium](https://www.w3.org/Protocols/HTTP/HTRESP.html)**Note**: The value may be provided in the source record using different terms, which should be normalized to these values. The original value should be stored in the **EventOriginalResultDetails** field. |
| **EventSchema** | Mandatory | Enumerated | The name of the schema documented here is `WebSession`. |
| **EventSchemaVersion** | Mandatory | SchemaVersion (String) | The version of the schema. The version of the schema documented here is `1.0.0` |
| **Dvc** fields |  |  | For Web Session events, device fields refer to the system reporting the Web Session event. This is typically an intermediary device for `HTTPSession` events, and the destination web or application server for `WebServerSession` and `ApiRequest` events. |

#### All common fields

Fields that appear in the table below are common to all ASIM schemas. Any guideline specified above overrides the general guidelines for the field. For example, a field might be optional in general, but mandatory for a specific schema. For further details on each field, refer to the [ASIM Common Fields](normalization-common-fields) article.

| **Class** | **Fields** |
| --- | --- |
| Mandatory | - [EventCount](normalization-common-fields#eventcount) - [EventStartTime](normalization-common-fields#eventstarttime) - [EventEndTime](normalization-common-fields#eventendtime) - [EventType](normalization-common-fields#eventtype)- [EventResult](normalization-common-fields#eventresult) - [EventProduct](normalization-common-fields#eventproduct) - [EventVendor](normalization-common-fields#eventvendor) - [EventSchema](normalization-common-fields#eventschema) - [EventSchemaVersion](normalization-common-fields#eventschemaversion) - [Dvc](normalization-common-fields#dvc) |
| Recommended | - [EventResultDetails](normalization-common-fields#eventresultdetails)- [EventSeverity](normalization-common-fields#eventseverity)- [EventUid](normalization-common-fields#eventuid) - [DvcIpAddr](normalization-common-fields#dvcipaddr) - [DvcHostname](normalization-common-fields#dvchostname) - [DvcDomain](normalization-common-fields#dvcdomain)- [DvcDomainType](normalization-common-fields#dvcdomaintype)- [DvcFQDN](normalization-common-fields#dvcfqdn)- [DvcId](normalization-common-fields#dvcid)- [DvcIdType](normalization-common-fields#dvcidtype)- [DvcAction](normalization-common-fields#dvcaction) |
| Optional | - [EventMessage](normalization-common-fields#eventmessage) - [EventSubType](normalization-common-fields#eventsubtype)- [EventOriginalUid](normalization-common-fields#eventoriginaluid)- [EventOriginalType](normalization-common-fields#eventoriginaltype)- [EventOriginalSubType](normalization-common-fields#eventoriginalsubtype)- [EventOriginalResultDetails](normalization-common-fields#eventoriginalresultdetails) - [EventOriginalSeverity](normalization-common-fields#eventoriginalseverity) - [EventProductVersion](normalization-common-fields#eventproductversion) - [EventReportUrl](normalization-common-fields#eventreporturl) - [EventOwner](normalization-common-fields#eventowner)- [DvcZone](normalization-common-fields#dvczone)- [DvcMacAddr](normalization-common-fields#dvcmacaddr)- [DvcOs](normalization-common-fields#dvcos)- [DvcOsVersion](normalization-common-fields#dvchostname)- [DvcOriginalAction](normalization-common-fields#dvcoriginalaction)- [DvcInterface](normalization-common-fields#dvcinterface)- [AdditionalFields](normalization-common-fields#additionalfields)- [DvcDescription](normalization-common-fields#dvcdescription)- [DvcScopeId](normalization-common-fields#dvcscopeid)- [DvcScope](normalization-common-fields#dvcscope) |

### Network session fields

HTTP sessions are application layer sessions that utilize TCP/IP as the underlying network layer session. The Web Session schema is a super set of [ASIM Network Session schema](normalization-schema-network) and all the Network Schema Fields are also included in the Web Session schema.

The following ASIM Network Session schema fields have specific guidelines when used for a Web Session event:

- The alias User should refer to the [SrcUsername](normalization-schema-network#srcusername) and not to [DstUsername](normalization-schema-network#dstusername).
- The field [EventOriginalResultDetails](normalization-common-fields#eventoriginalresultdetails) can hold any result reported by the source in addition to the HTTP status code stored in EventResultDetails.
- For Web Sessions, the primary destination field is the Url Field. The [DstDomain](normalization-schema-network#dstdomain) is optional rather than recommended. Specifically, if not available, there is no need to extract it from the URL in the parser.
- The fields `NetworkRuleName` and `NetworkRuleNumber` are renamed `RuleName` and `RuleNumber` respectively.

Web Session events are commonly reported by intermediate devices that terminate the HTTP connection from the client and initiate a new connection, acting as a proxy, with the server. To represent the intermediate device, use the [ASIM Network Session schema](normalization-schema-network)[Intermediary device fields](normalization-schema-network#Intermediary)

### HTTP session fields

The following are additional fields that are specific to web sessions:

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **Url** | Mandatory | URL (String) | The HTTP request URL, including parameters. For `HTTPSession` events, the URL may include the schema and should include the server name. For `WebServerSession` and for `ApiRequest` the URL would typically not include the schema and server, which can be found in the `NetworkApplicationProtocol` and `DstFQDN` fields respectively. Example: `https://contoso.com/fo/?k=v&amp;q=u#f` |
| **UrlCategory** | Optional | String | The defined grouping of a URL or the domain part of the URL. The category is commonly provided by web security gateways and is based on the content of the site the URL points to.Example: search engines, adult, news, advertising, and parked domains. |
| **UrlOriginal** | Optional | URL (String) | The original value of the URL, when the URL was modified by the reporting device and both values are provided. |
| **HttpVersion** | Optional | String | The HTTP Request Version.Example: `2.0` |
| **HttpRequestMethod** | Recommended | Enumerated | The HTTP Method. The values are as defined in [RFC 7231](https://datatracker.ietf.org/doc/html/rfc7231#section-4) and [RFC 5789](https://datatracker.ietf.org/doc/html/rfc5789#section-2), and include `GET`, `HEAD`, `POST`, `PUT`, `DELETE`, `CONNECT`, `OPTIONS`, `TRACE`, and `PATCH`.Example: `GET` |
| **HttpStatusCode** | Alias |  | The HTTP Status Code. Alias to EventResultDetails. |
| **HttpContentType** | Optional | String | The HTTP Response content type header. **Note**: The **HttpContentType** field may include both the content format and extra parameters, such as the encoding used to get the actual format. Example: `text/html; charset=ISO-8859-4` |
| **HttpContentFormat** | Optional | String | The content format part of the HttpContentType Example: `text/html` |
| **HttpReferrer** | Optional | String | The HTTP referrer header.**Note**: ASIM, in sync with OSSEM, uses the correct spelling for *referrer*, and not the original HTTP header spelling.Example: `https://developer.mozilla.org/docs` |
| **HttpUserAgent** | Optional | String | The HTTP user agent header.Example:`Mozilla/5.0` (Windows NT 10.0; WOW64)`AppleWebKit/537.36` (KHTML, like Gecko)`Chrome/83.0.4103.97 Safari/537.36` |
| **UserAgent** | Alias |  | Alias to HttpUserAgent |
| **HttpRequestXff** | Optional | IP Address | The HTTP X-Forwarded-For header.Example: `120.12.41.1` |
| **HttpRequestTime** | Optional | Integer | The amount of time, in milliseconds, it took to send the request to the server, if applicable.Example: `700` |
| **HttpResponseTime** | Optional | Integer | The amount of time, in milliseconds, it took to receive a response in the server, if applicable.Example: `800` |
| **HttpHost** | Optional | String | The virtual web server the HTTP request has targeted. This value is typically based on the [HTTP Host header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Host). |
| **FileName** | Optional | String | For HTTP uploads, the name of the uploaded file. |
| **FileMD5** | Optional | MD5 | For HTTP uploads, the MD5 hash of the uploaded file.Example: `75a599802f1fa166cdadb360960b1dd0` |
| **FileSHA1** | Optional | SHA1 | For HTTP uploads, the SHA1 hash of the uploaded file.Example:`d55c5a4df19b46db8c54``c801c4665d3338acdab0` |
| **FileSHA256** | Optional | SHA256 | For HTTP uploads, the SHA256 hash of the uploaded file.Example:`e81bb824c4a09a811af17deae22f22dd``2e1ec8cbb00b22629d2899f7c68da274` |
| **FileSHA512** | Optional | SHA512 | For HTTP uploads, the SHA512 hash of the uploaded file. |
| **Hash** | Alias |  | Alias to the available Hash field. |
| **HashType** | Conditional | Enumerated | The type of the hash in the Hash field. Possible values include: `MD5`, `SHA1`, `SHA256`, and `SHA512`. |
| **FileSize** | Optional | Long | For HTTP uploads, the size in bytes of the uploaded file. |
| **FileContentType** | Optional | String | For HTTP uploads, the content type of the uploaded file. |
| **HttpCookie** | Optional | String | The content of the HTTP cookie header sent from the client to the server, containing name-value pairs of session data.Example: `session_id=abc123; user_pref=dark_mode` |
| **HttpIsProxied** | Optional | Boolean | Indicates whether the HTTP request was sent through a proxy server.Example: `true` |
| **HttpRequestBodyBytes** | Optional | Long | The size of the HTTP request body in bytes, not including headers.Example: `1024` |
| **HttpRequestCacheControl** | Optional | String | The content of the HTTP Cache-Control request header, specifying caching directives from the client.Example: `no-cache` |
| **HttpRequestHeaderCount** | Optional | Integer | The number of HTTP headers included in the request.Example: `12` |
| **HttpResponseBodyBytes** | Optional | Long | The size of the HTTP response body in bytes, not including headers.Example: `8192` |
| **HttpResponseCacheControl** | Optional | String | The content of the HTTP Cache-Control response header, specifying caching directives from the server.Example: `max-age=3600, public` |
| **HttpResponseExpires** | Optional | String | The content of the HTTP Expires response header, indicating when the response content expires.Example: `Thu, 01 Dec 2024 16:00:00 GMT` |
| **HttpResponseHeaderCount** | Optional | Integer | The number of HTTP headers included in the response.Example: `15` |

### Other fields

If the event is reported by one of the endpoints of the web session, it may include information about the process that initiated or terminated the session. In such cases, the [ASIM Process Event schema](normalization-schema-process-event) to normalize this information.

### Entity correlation fields

Note

Contributors don't need to populate these fields. Applicable parsers will populate them when internal Microsoft support is added.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **DstApplicationEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the destination application within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **DstSystemEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the destination system within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **DstUserAdditionalIds** | Optional | Dynamic | For the field structure and usage, see [Fields suffixed with AdditionalIds](normalization-common-fields#fields-suffixed-with-additionalids). |
| **DstUserEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the destination user within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **SrcApplicationEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the source application within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **SrcSystemEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the source system within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **SrcUserAdditionalIds** | Optional | Dynamic | For the field structure and usage, see [Fields suffixed with AdditionalIds](normalization-common-fields#fields-suffixed-with-additionalids). |
| **SrcUserEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the source user within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |

## Schema updates

| Version | Changes |
| --- | --- |
| 0.2.5 | Added the field `HttpHost`. |
| 0.2.6 | Changed the type of `FileSize` from Integer to Long. |
| 0.2.7 | Added the fields `HttpCookie`, `HttpIsProxied`, `HttpRequestBodyBytes`, `HttpRequestCacheControl`, `HttpRequestHeaderCount`, `HttpResponseBodyBytes`, `HttpResponseCacheControl`, `HttpResponseExpires`, and `HttpResponseHeaderCount`. |
| 1.0.0 | Added entity correlation fields. |

The Web Session schema relies on the Network Session schema. Therefore, [Network Session schema updates](normalization-schema-network#schema-updates) also apply to the Web Session schema.

### Related content

- [Advanced Security Information Model (ASIM) overview](normalization)
- [Advanced Security Information Model (ASIM) schemas](normalization-about-schemas)
- [Advanced Security Information Model (ASIM) parsers](normalization-parsers-overview)
- [Advanced Security Information Model (ASIM) content](normalization-content)
- [Azure Sentinel Webinar: The Information Model-Understanding Normalization in Azure Sentinel](https://www.youtube.com/watch?v=WoGD-JeC7ng)