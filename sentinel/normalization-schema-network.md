---
layout: Conceptual
title: The Advanced Security Information Model (ASIM) Network Session normalization schema reference | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/normalization-schema-network
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
description: This article displays the Microsoft Sentinel Network Session normalization schema.
ms.author: edbaynash
author: EdB-MSFT
ms.topic: reference
ms.date: 2026-09-16T00:00:00.0000000Z
locale: en-us
document_id: 6ef6b794-19a9-3df4-5ceb-67e032666185
document_version_independent_id: 0a8b25e3-85d5-679d-2be5-42f8327a818f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/normalization-schema-network.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/normalization-schema-network
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/normalization-schema-network.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 71163367-a2e8-36ec-1491-952b00467dd8
---

# The Advanced Security Information Model (ASIM) Network Session normalization schema reference | Microsoft Learn

The Microsoft Sentinel Network Session normalization schema represents an IP network activity, such as network connections and network sessions. Such events are reported, for example, by operating systems, routers, firewalls, and intrusion prevention systems.

The network normalization schema can represent any type of an IP network session but is designed to provide support for common source types, such as Netflow, firewalls, and intrusion prevention systems.

For more information about normalization in Microsoft Sentinel, see [Normalization and the Advanced Security Information Model (ASIM)](normalization).

## Parsers

For more information about ASIM parsers, see the [ASIM parsers overview](normalization-parsers-overview).

### Unifying parsers

To use parsers that unify all ASIM out-of-the-box parsers, and ensure that your analysis runs across all the configured sources, use the `_Im_NetworkSession` parser.

### Out-of-the-box, source-specific parsers

For the list of the Network Session parsers Microsoft Sentinel provides out-of-the-box refer to the [ASIM parsers list](normalization-parsers-list#network-session-parsers)

### Add your own normalized parsers

When [developing custom parsers](normalization-develop-parsers) for the Network Session information model, name your KQL functions using the following syntax:

- `vimNetworkSession<vendor><Product>` for parametrized parsers
- `ASimNetworkSession<vendor><Product>` for regular parsers

Refer to the article [Managing ASIM parsers](normalization-manage-parsers) to learn how to add your custom parsers to the network session unifying parsers.

### Filtering parser parameters

The Network Session parsers support [filtering parameters](normalization-about-parsers#optimizing-parsing-using-parameters). While these parameters are optional, they can improve your query performance.

The following filtering parameters are available:

| Name | Type | Description |
| --- | --- | --- |
| **starttime** | datetime | Filter only network sessions that *started* at or after this time. This parameter filters on the `TimeGenerated` field, which is the standard designator for the time of the event, regardless of the parser-specific mapping of the EventStartTime and EventEndTime fields. |
| **endtime** | datetime | Filter only network sessions that *started* running at or before this time. This parameter filters on the `TimeGenerated` field, which is the standard designator for the time of the event, regardless of the parser-specific mapping of the EventStartTime and EventEndTime fields. |
| **srcipaddr\_has\_any\_prefix** | dynamic | Filter only network sessions for which the source IP address field prefix is in one of the listed values. Prefixes should end with a `.`, for example: `10.0.`. The length of the list is limited to 10,000 items. |
| **dstipaddr\_has\_any\_prefix** | dynamic | Filter only network sessions for which the destination IP address field prefix is in one of the listed values. Prefixes should end with a `.`, for example: `10.0.`. The length of the list is limited to 10,000 items. |
| **ipaddr\_has\_any\_prefix** | dynamic | Filter only network sessions for which the destination IP address field or source IP address field prefix is in one of the listed values. Prefixes should end with a `.`, for example: `10.0.`. The length of the list is limited to 10,000 items.The field ASimMatchingIpAddr is set with the one of the values `SrcIpAddr`, `DstIpAddr`, or `Both` to reflect the matching fields or fields. |
| **dstportnumber** | Int | Filter only network sessions with the specified destination port number. |
| **hostname\_has\_any** | dynamic/string | Filter only network sessions for which the destination hostname field has any of the values listed. The length of the list is limited to 10,000 items. The field ASimMatchingHostname is set with the one of the values `SrcHostname`, `DstHostname`, or `Both` to reflect the matching fields or fields. |
| **dvcaction** | dynamic/string | Filter only network sessions for which the Device Action field is any of the values listed. |
| **eventresult** | String | Filter only network sessions with a specific **EventResult** value. |

Some parameter can accept both list of values of type `dynamic` or a single string value. To pass a literal list to parameters that expect a dynamic value, explicitly use a [dynamic literal](/en-us/kusto/query/scalar-data-types/dynamic?view=microsoft-sentinel&amp;preserve-view=true#dynamic-literals). For example: `dynamic(['192.168.','10.'])`

For example, to filter only network sessions for a specified list of domain names, use:

```kusto
let torProxies=dynamic(["tor2web.org", "tor2web.com", "torlink.co"]);
_Im_NetworkSession (hostname_has_any = torProxies)
```

Tip

To pass a literal list to parameters that expect a dynamic value, explicitly use a [dynamic literal](/en-us/kusto/query/scalar-data-types/dynamic?view=microsoft-sentinel&amp;preserve-view=true#dynamic-literals). For example: `dynamic(['192.168.','10.'])`.

## Normalized content

For a full list of analytics rules that use normalized DNS events, see [Network session security content](normalization-content#network-session-security-content).

## Schema overview

The Network Session information model is aligned with the [OSSEM Network entity schema](https://github.com/OTRF/OSSEM/blob/master/docs/cdm/entities/network.md).

The Network Session schema serves several types of similar but distinct scenarios, which share the same fields. Those scenarios are identified by the EventType field:

- `NetworkSession` - a network session reported by an intermediate device monitoring the network, such as a Firewall, a router, or a network tap.
- `L2NetworkSession` - a network session for which only layer 2 information is available. Such events will include MAC addresses but not IP addresses.
- `Flow` - an aggregated event that reports multiple similar network sessions, typically over a predefined time period, such as **Netflow** events.
- `EndpointNetworkSession` - a network session reported by one of the end points of the session, including clients and servers. For such events, the schema supports the `remote` and `local` alias fields.
- `IDS` - a network session reported as suspicious. Such an event will have some of the inspection fields populated, and may have just one IP address field populated, either the source or the destination.

Typically, a query should either select just a subset of those event types, and may need to address separately unique aspects of the use cases. For example, IDS events do not reflect the entire network volume and should not be taken into account in column based analytics.

Network session events use the descriptors `Src` and `Dst` to denote the roles of the devices and related users and applications involved in the session. So, for example, the source device hostname and IP address are named `SrcHostname` and `SrcIpAddr`. Other ASIM schemas typically use `Target` instead of `Dst`.

For events reported by an endpoint and for which the event type is `EndpointNetworkSession`, the descriptors `Local` and `Remote` denote the endpoint itself and the device at the other end of the network session respectively.

The descriptor `Dvc` is used for the reporting device, which is the local system for sessions reported by an endpoint, and the intermediary device or network tap for other network session events.

## Schema details

### Common ASIM fields

Important

Fields common to all schemas are described in detail in the [ASIM Common Fields](normalization-common-fields) article.

#### Common fields with specific guidelines

The following list mentions fields that have specific guidelines for Network Session events:

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **EventCount** | Mandatory | Integer | Netflow sources support aggregation, and the **EventCount** field should be set to the value of the Netflow **FLOWS** field. For other sources, the value is typically set to `1`. |
| **EventType** | Mandatory | Enumerated | Describes the scenario reported by the record. For Network Session records, the allowed values are: - `EndpointNetworkSession` - `NetworkSession` - `L2NetworkSession`- `IDS` - `Flow`For more information on event types, refer to the schema overview |
| **EventSubType** | Optional | Enumerated | Additional description of the event type, if applicable.  For Network Session records, supported values include:- `Start`- `End`This is field is not relevant for `Flow` events. |
| **EventResult** | Mandatory | Enumerated | If the source device does not provide an event result, **EventResult** should be based on the value of DvcAction. If DvcAction is `Deny`, `Drop`, `Drop ICMP`, `Reset`, `Reset Source`, or `Reset Destination`, **EventResult** should be `Failure`. Otherwise, **EventResult** should be `Success`. |
| **EventResultDetails** | Recommended | Enumerated | Reason or details for the result reported in the EventResult field. Supported values are: - Failover  - Invalid TCP  - Invalid Tunnel - Maximum Retry - Reset - Routing issue - Simulation - Terminated - Timeout - Transient error - Unknown - NA.The original, source specific, value is stored in the [EventOriginalResultDetails](normalization-common-fields#eventoriginalresultdetails) field. |
| **EventSchema** | Mandatory | Enumerated | The name of the schema documented here is `NetworkSession`. |
| **EventSchemaVersion** | Mandatory | SchemaVersion (String) | The version of the schema. The version of the schema documented here is `1.0.0`. |
| **DvcAction** | Recommended | Enumerated | The action taken on the network session. Supported values are:- `Allow`- `Deny`- `Drop`- `Drop ICMP`- `Reset`- `Reset Source`- `Reset Destination`- `Encrypt`- `Decrypt`- `VPNroute`**Note**: The value might be provided in the source record by using different terms, which should be normalized to these values. The original value should be stored in the [DvcOriginalAction](normalization-common-fields#dvcoriginalaction) field.Example: `drop` |
| **EventSeverity** | Optional | Enumerated | If the source device does not provide an event severity, **EventSeverity** should be based on the value of DvcAction. If DvcAction is `Deny`, `Drop`, `Drop ICMP`, `Reset`, `Reset Source`, or `Reset Destination`, **EventSeverity** should be `Low`. Otherwise, **EventSeverity** should be `Informational`. |
| **DvcInterface** |  |  | The DvcInterface field should alias either the DvcInboundInterface or the DvcOutboundInterface fields. |
| **Dvc** fields |  |  | For Network Session events, device fields refer to the system reporting the Network Session event. |

#### All common fields

Fields that appear in the table below are common to all ASIM schemas. Any guideline specified above overrides the general guidelines for the field. For example, a field might be optional in general, but mandatory for a specific schema. For more information on each field, refer to the [ASIM Common Fields](normalization-common-fields) article.

| **Class** | **Fields** |
| --- | --- |
| Mandatory | - [EventCount](normalization-common-fields#eventcount) - [EventStartTime](normalization-common-fields#eventstarttime) - [EventEndTime](normalization-common-fields#eventendtime) - [EventType](normalization-common-fields#eventtype)- [EventResult](normalization-common-fields#eventresult) - [EventProduct](normalization-common-fields#eventproduct) - [EventVendor](normalization-common-fields#eventvendor) - [EventSchema](normalization-common-fields#eventschema) - [EventSchemaVersion](normalization-common-fields#eventschemaversion) - [Dvc](normalization-common-fields#dvc) |
| Recommended | - [EventResultDetails](normalization-common-fields#eventresultdetails)- [EventSeverity](normalization-common-fields#eventseverity)- [EventUid](normalization-common-fields#eventuid) - [DvcIpAddr](normalization-common-fields#dvcipaddr) - [DvcHostname](normalization-common-fields#dvchostname) - [DvcDomain](normalization-common-fields#dvcdomain)- [DvcDomainType](normalization-common-fields#dvcdomaintype)- [DvcFQDN](normalization-common-fields#dvcfqdn)- [DvcId](normalization-common-fields#dvcid)- [DvcIdType](normalization-common-fields#dvcidtype)- [DvcAction](normalization-common-fields#dvcaction) |
| Optional | - [EventMessage](normalization-common-fields#eventmessage) - [EventSubType](normalization-common-fields#eventsubtype)- [EventOriginalUid](normalization-common-fields#eventoriginaluid)- [EventOriginalType](normalization-common-fields#eventoriginaltype)- [EventOriginalSubType](normalization-common-fields#eventoriginalsubtype)- [EventOriginalResultDetails](normalization-common-fields#eventoriginalresultdetails) - [EventOriginalSeverity](normalization-common-fields#eventoriginalseverity) - [EventProductVersion](normalization-common-fields#eventproductversion) - [EventReportUrl](normalization-common-fields#eventreporturl) - [EventOwner](normalization-common-fields#eventowner)- [DvcZone](normalization-common-fields#dvczone)- [DvcMacAddr](normalization-common-fields#dvcmacaddr)- [DvcOs](normalization-common-fields#dvcos)- [DvcOsVersion](normalization-common-fields#dvchostname)- [DvcOriginalAction](normalization-common-fields#dvcoriginalaction)- [DvcInterface](normalization-common-fields#dvcinterface)- [AdditionalFields](normalization-common-fields#additionalfields)- [DvcDescription](normalization-common-fields#dvcdescription)- [DvcScopeId](normalization-common-fields#dvcscopeid)- [DvcScope](normalization-common-fields#dvcscope) |

### Network session fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **NetworkApplicationProtocol** | Optional | String | The application layer protocol used by the connection or session. The value should be in all uppercase.Example: `FTP` |
| **NetworkProtocol** | Optional | Enumerated | The IP protocol used by the connection or session as listed in [IANA protocol assignment](https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml), which is typically `TCP`, `UDP`, or `ICMP`.Example: `TCP` |
| **NetworkProtocolVersion** | Optional | Enumerated | The version of NetworkProtocol. When using it to distinguish between IP version, use the values `IPv4` and `IPv6`. |
| **NetworkDirection** | Optional | Enumerated | The direction of the connection or session: - For the EventType`NetworkSession`, `Flow` or `L2NetworkSession`, **NetworkDirection** represents the direction relative to the organization or cloud environment boundary. Supported values are `Inbound`, `Outbound`, `Local` (to the organization), `External` (to the organization) or `NA` (Not Applicable). - For the EventType`EndpointNetworkSession`, **NetworkDirection** represents the direction relative to the endpoint. Supported values are `Inbound`, `Outbound`, `Local` (to the system), `Listen` or `NA` (Not Applicable). The `Listen` value indicates that a device has started accepting network connections but isn't actually, necessarily, connected. |
| **NetworkDuration** | Optional | Integer | The amount of time, in milliseconds, for the completion of the network session or connection.Example: `1500` |
| **Duration** | Alias |  | Alias to NetworkDuration. |
| **NetworkIcmpType** | Optional | String | For an ICMP message, ICMP type name associated with the numerical value, as described in [RFC 2780](https://datatracker.ietf.org/doc/html/rfc2780) for IPv4 network connections, or in [RFC 4443](https://datatracker.ietf.org/doc/html/rfc4443) for IPv6 network connections.Example: `Destination Unreachable` for NetworkIcmpCode `3` |
| **NetworkIcmpCode** | Optional | Integer | For an ICMP message, the ICMP code number as described in [RFC 2780](https://datatracker.ietf.org/doc/html/rfc2780) for IPv4 network connections, or in [RFC 4443](https://datatracker.ietf.org/doc/html/rfc4443) for IPv6 network connections. |
| **NetworkConnectionHistory** | Optional | String | TCP flags and other potential IP header information. |
| **DstBytes** | Recommended | Long | The number of bytes sent from the destination to the source for the connection or session. If the event is aggregated, **DstBytes** should be the sum over all aggregated sessions.Example: `32455` |
| **SrcBytes** | Recommended | Long | The number of bytes sent from the source to the destination for the connection or session. If the event is aggregated, **SrcBytes** should be the sum over all aggregated sessions.Example: `46536` |
| **NetworkBytes** | Optional | Long | Number of bytes sent in both directions. If both **BytesReceived** and **BytesSent** exist, **BytesTotal** should equal their sum. If the event is aggregated, **NetworkBytes** should be the sum over all aggregated sessions.Example: `78991` |
| **DstPackets** | Optional | Long | The number of packets sent from the destination to the source for the connection or session. The meaning of a packet is defined by the reporting device. If the event is aggregated, **DstPackets** should be the sum over all aggregated sessions.Example: `446` |
| **SrcPackets** | Optional | Long | The number of packets sent from the source to the destination for the connection or session. The meaning of a packet is defined by the reporting device. If the event is aggregated, **SrcPackets** should be the sum over all aggregated sessions.Example: `6478` |
| **NetworkPackets** | Optional | Long | The number of packets sent in both directions. If both **PacketsReceived** and **PacketsSent** exist, **PacketsTotal** should equal their sum. The meaning of a packet is defined by the reporting device. If the event is aggregated, **NetworkPackets** should be the sum over all aggregated sessions.Example: `6924` |
| **NetworkSessionId** | Optional | string | The session identifier as reported by the reporting device. Example: `172\_12\_53\_32\_4322\_\_123\_64\_207\_1\_80` |
| **SessionId** | Alias | String | Alias to NetworkSessionId. |
| **TcpFlagsAck** | Optional | Boolean | The TCP ACK Flag reported. The acknowledgment flag is used to acknowledge the successful receipt of a packet. As we can see from the diagram above, the receiver sends an ACK and a SYN in the second step of the three way handshake process to tell the sender that it received its initial packet. |
| **TcpFlagsFin** | Optional | Boolean | The TCP FIN Flag reported. The finished flag means there is no more data from the sender. Therefore, it is used in the last packet sent from the sender. |
| **TcpFlagsSyn** | Optional | Boolean | The TCP SYN Flag reported. The synchronization flag is used as a first step in establishing a three way handshake between two hosts. Only the first packet from both the sender and receiver should have this flag set. |
| **TcpFlagsUrg** | Optional | Boolean | The TCP URG Flag reported. The urgent flag is used to notify the receiver to process the urgent packets before processing all other packets. The receiver will be notified when all known urgent data has been received. See [RFC 6093](https://tools.ietf.org/html/rfc6093) for more details. |
| **TcpFlagsPsh** | Optional | Boolean | The TCP PSH Flag reported. The push flag is similar to the URG flag and tells the receiver to process these packets as they are received instead of buffering them. |
| **TcpFlagsRst** | Optional | Boolean | The TCP RST Flag reported. The reset flag gets sent from the receiver to the sender when a packet is sent to a particular host that was not expecting it. |
| **TcpFlagsEce** | Optional | Boolean | The TCP ECE Flag reported. This flag is responsible for indicating if the TCP peer is [ECN capable](https://en.wikipedia.org/wiki/Explicit_Congestion_Notification). See [RFC 3168](https://tools.ietf.org/html/rfc3168) for more details. |
| **TcpFlagsCwr** | Optional | Boolean | The TCP CWR Flag reported. The congestion window reduced flag is used by the sending host to indicate it received a packet with the ECE flag set. See [RFC 3168](https://tools.ietf.org/html/rfc3168) for more details. |
| **TcpFlagsNs** | Optional | Boolean | The TCP NS Flag reported. The nonce sum flag is still an experimental flag used to help protect against accidental malicious concealment of packets from the sender. See [RFC 3540](https://tools.ietf.org/html/rfc3540) for more details |

### Destination system fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **Dst** | Alias |  | A unique identifier of the server receiving the DNS request. This field might alias the DstDvcId, DstHostname, or DstIpAddr fields. Example: `192.168.12.1` |
| **DstIpAddr** | Recommended | IP address | The IP address of the connection or session destination. If the session uses network address translation, `DstIpAddr` is the publicly visible address, and not the original address of the source, which is stored in DstNatIpAddrExample: `2001:db8::ff00:42:8329`**Note**: This value is mandatory if DstHostname is specified. |
| **DstPortNumber** | Optional | Integer | The destination IP port.Example: `443` |
| **DstHostname** | Recommended | Hostname (String) | The destination device hostname, excluding domain information. If no device name is available, store the relevant IP address in this field.Example: `DESKTOP-1282V4D` |
| **DstDomain** | Recommended | Domain (String) | The domain of the destination device.Example: `Contoso` |
| **DstDomainType** | Conditional | Enumerated | The type of DstDomain. For a list of allowed values and further information, refer to [DomainType](normalization-entity-device#domaintype) in the [Schema Overview article](normalization-about-schemas).Required if DstDomain is used. |
| **DstFQDN** | Optional | FQDN (String) | The destination device hostname, including domain information when available. Example: `Contoso\DESKTOP-1282V4D`**Note**: This field supports both traditional FQDN format and Windows domain\hostname format. The DstDomainType reflects the format used. |
| **DstDvcId** | Optional | String | The ID of the destination device. If multiple IDs are available, use the most important one, and store the others in the fields `DstDvc<DvcIdType>`. Example: `ac7e9755-8eae-4ffc-8a02-50ed7a2216c3` |
| **DstDvcScopeId** | Optional | String | The cloud platform scope ID the device belongs to. **DstDvcScopeId** map to a subscription ID on Azure and to an account ID on AWS. |
| **DstDvcScope** | Optional | String | The cloud platform scope the device belongs to. **DstDvcScope** map to a subscription ID on Azure and to an account ID on AWS. |
| **DstDvcIdType** | Conditional | Enumerated | The type of DstDvcId. For a list of allowed values and further information, refer to [DvcIdType](normalization-entity-device#dvcidtype) in the [Schema Overview article](normalization-about-schemas). Required if **DstDeviceId** is used. |
| **DstDeviceType** | Optional | Enumerated | The type of the destination device. For a list of allowed values and further information, refer to [DeviceType](normalization-about-schemas#devicetype) in the [Schema Overview article](normalization-about-schemas). |
| **DstZone** | Optional | String | The network zone of the destination, as defined by the reporting device.Example: `Dmz` |
| **DstInterfaceName** | Optional | String | The network interface used for the connection or session by the destination device.Example: `Microsoft Hyper-V Network Adapter` |
| **DstInterfaceGuid** | Optional | GUID (String) | The GUID of the network interface used on the destination device.Example:`46ad544b-eaf0-47ef-``827c-266030f545a6` |
| **DstMacAddr** | Optional | MAC Address (String) | The MAC address of the network interface used for the connection or session by the destination device.Example: `06:10:9f:eb:8f:14` |
| **DstVlanId** | Optional | String | The VLAN ID related to the destination device.Example: `130` |
| **OuterVlanId** | Alias |  | Alias to DstVlanId. In many cases, the VLAN can't be determined as a source or a destination but is characterized as inner or outer. This alias to signifies that DstVlanId should be used when the VLAN is characterized as outer. |
| **DstGeoCountry** | Optional | Country | The country/region associated with the destination IP address. For more information, see [Logical types](normalization-about-schemas#logical-types).Example: `USA` |
| **DstGeoRegion** | Optional | Region | The region, or state, associated with the destination IP address. For more information, see [Logical types](normalization-about-schemas#logical-types).Example: `Vermont` |
| **DstGeoCity** | Optional | City | The city associated with the destination IP address. For more information, see [Logical types](normalization-about-schemas#logical-types).Example: `Burlington` |
| **DstGeoLatitude** | Optional | Latitude | The latitude of the geographical coordinate associated with the destination IP address. For more information, see [Logical types](normalization-about-schemas#logical-types).Example: `44.475833` |
| **DstGeoLongitude** | Optional | Longitude | The longitude of the geographical coordinate associated with the destination IP address. For more information, see [Logical types](normalization-about-schemas#logical-types).Example: `73.211944` |
| **DstDescription** | Optional | String | A descriptive text associated with the device. For example: `Primary Domain Controller`. |

### Destination user fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **DstUserId** | Optional | String | A machine-readable, alphanumeric, unique representation of the destination user. For the supported format for different ID types, refer to [the User entity](normalization-entity-user). Example: `S-1-12` |
| **DstUserScope** | Optional | String | The scope, such as Microsoft Entra tenant, in which DstUserId and DstUsername are defined. or more information and list of allowed values, see [UserScope](normalization-entity-user#userscope) in the [Schema Overview article](normalization-about-schemas). |
| **DstUserScopeId** | Optional | String | The scope ID, such as Microsoft Entra Directory ID, in which DstUserId and DstUsername are defined. for more information and list of allowed values, see [UserScopeId](normalization-entity-user#userscopeid) in the [Schema Overview article](normalization-about-schemas). |
| **DstUserIdType** | Conditional | UserIdType | The type of the ID stored in the DstUserId field. For a list of allowed values and further information, refer to [UserIdType](normalization-entity-user#useridtype) in the [Schema Overview article](normalization-about-schemas). |
| **DstUsername** | Optional | Username (String) | The destination username, including domain information when available. For the supported format for different ID types, refer to [the User entity](normalization-entity-user). Use the simple form only if domain information isn't available.Store the Username type in the DstUsernameType field. If other username formats are available, store them in the fields `DstUsername<UsernameType>`.Example: `AlbertE` |
| **User** | Alias |  | Alias to DstUsername. |
| **DstUsernameType** | Conditional | UsernameType | Specifies the type of the username stored in the DstUsername field. For a list of allowed values and further information, refer to [UsernameType](normalization-entity-user#usernametype) in the [Schema Overview article](normalization-about-schemas).Example: `Windows` |
| **DstUserType** | Optional | UserType | The type of destination user. For a list of allowed values and further information, refer to [UserType](normalization-entity-user#usertype) in the [Schema Overview article](normalization-about-schemas). **Note**: The value might be provided in the source record by using different terms, which should be normalized to these values. Store the original value in the DstOriginalUserType field. |
| **DstOriginalUserType** | Optional | String | The original destination user type, if provided by the source. |

### Destination application fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **DstAppName** | Optional | String | The name of the destination application.Example: `Facebook` |
| **DstAppId** | Optional | String | The ID of the destination application, as reported by the reporting device. If DstAppType is `Process`, `DstAppId` and `DstProcessId` should have the same value.Example: `124` |
| **DstAppType** | Optional | AppType | The type of the destination application. For a list of allowed values and further information, refer to [AppType](normalization-about-schemas#apptype) in the [Schema Overview article](normalization-about-schemas).This field is mandatory if DstAppName or DstAppId are used. |
| **DstProcessName** | Optional | String | The file name of the process that terminated the network session. This name is typically considered to be the process name. Example: `C:\Windows\explorer.exe` |
| **Process** | Alias |  | Alias to the DstProcessNameExample: `C:\Windows\System32\rundll32.exe` |
| **DstProcessId** | Optional | String | The process ID (PID) of the process that terminated the network session.Example: `48610176`**Note**: The type is defined as *string* to support varying systems, but on Windows and Linux this value must be numeric. If you are using a Windows or Linux machine and used a different type, make sure to convert the values. For example, if you used a hexadecimal value, convert it to a decimal value. |
| **DstProcessGuid** | Optional | String | A generated unique identifier (GUID) of the process that terminated the network session.  Example: `EF3BD0BD-2B74-60C5-AF5C-010000001E00` |

### Source system fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **Src** | Alias |  | A unique identifier of the source device. This field might alias the SrcDvcId, SrcHostname, or SrcIpAddr fields. Example: `192.168.12.1` |
| **SrcIpAddr** | Recommended | IP address | The IP address from which the connection or session originated. This value is mandatory if **SrcHostname** is specified. If the session uses network address translation, `SrcIpAddr` is the publicly visible address, and not the original address of the source, which is stored in SrcNatIpAddrExample: `77.138.103.108` |
| **SrcPortNumber** | Optional | Integer | The IP port from which the connection originated. Might not be relevant for a session comprising multiple connections.Example: `2335` |
| **SrcHostname** | Recommended | Hostname (String) | The source device hostname, excluding domain information. If no device name is available, store the relevant IP address in this field.Example: `DESKTOP-1282V4D` |
| **SrcDomain** | Recommended | Domain (String) | The domain of the source device.Example: `Contoso` |
| **SrcDomainType** | Conditional | DomainType | The type of SrcDomain. For a list of allowed values and further information, refer to [DomainType](normalization-entity-device#domaintype) in the [Schema Overview article](normalization-about-schemas).Required if SrcDomain is used. |
| **SrcFQDN** | Optional | FQDN (String) | The source device hostname, including domain information when available. **Note**: This field supports both traditional FQDN format and Windows domain\hostname format. The SrcDomainType field reflects the format used. Example: `Contoso\DESKTOP-1282V4D` |
| **SrcDvcId** | Optional | String | The ID of the source device. If multiple IDs are available, use the most important one, and store the others in the fields `SrcDvc<DvcIdType>`.Example: `ac7e9755-8eae-4ffc-8a02-50ed7a2216c3` |
| **SrcDvcScopeId** | Optional | String | The cloud platform scope ID the device belongs to. **SrcDvcScopeId** map to a subscription ID on Azure and to an account ID on AWS. |
| **SrcDvcScope** | Optional | String | The cloud platform scope the device belongs to. **SrcDvcScope** map to a subscription ID on Azure and to an account ID on AWS. |
| **SrcDvcIdType** | Conditional | DvcIdType | The type of SrcDvcId. For a list of allowed values and further information, refer to [DvcIdType](normalization-entity-device#dvcidtype) in the [Schema Overview article](normalization-about-schemas). **Note**: This field is required if SrcDvcId is used. |
| **SrcDeviceType** | Optional | DeviceType | The type of the source device. For a list of allowed values and further information, refer to [DeviceType](normalization-about-schemas#devicetype) in the [Schema Overview article](normalization-about-schemas). |
| **SrcZone** | Optional | String | The network zone of the source, as defined by the reporting device.Example: `Internet` |
| **SrcInterfaceName** | Optional | String | The network interface used for the connection or session by the source device. Example: `eth01` |
| **SrcInterfaceGuid** | Optional | GUID (String) | The GUID of the network interface used on the source device.Example:`46ad544b-eaf0-47ef-``827c-266030f545a6` |
| **SrcMacAddr** | Optional | MAC Address (String) | The MAC address of the network interface from which the connection or session originated.Example: `06:10:9f:eb:8f:14` |
| **SrcVlanId** | Optional | String | The VLAN ID related to the source device.Example: `130` |
| **InnerVlanId** | Alias |  | Alias to SrcVlanId. In many cases, the VLAN can't be determined as a source or a destination but is characterized as inner or outer. This alias to signifies that SrcVlanId should be used when the VLAN is characterized as inner. |
| **SrcGeoCountry** | Optional | Country | The country/region associated with the source IP address.Example: `USA` |
| **SrcGeoRegion** | Optional | Region | The region associated with the source IP address.Example: `Vermont` |
| **SrcGeoCity** | Optional | City | The city associated with the source IP address.Example: `Burlington` |
| **SrcGeoLatitude** | Optional | Latitude | The latitude of the geographical coordinate associated with the source IP address.Example: `44.475833` |
| **SrcGeoLongitude** | Optional | Longitude | The longitude of the geographical coordinate associated with the source IP address.Example: `73.211944` |
| **SrcDescription** | Optional | String | A descriptive text associated with the device. For example: `Primary Domain Controller`. |

### Source user fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **SrcUserId** | Optional | String | A machine-readable, alphanumeric, unique representation of the source user. For the supported format for different ID types, refer to [the User entity](normalization-entity-user). Example: `S-1-12` |
| **SrcUserScope** | Optional | String | The scope, such as Microsoft Entra tenant, in which SrcUserId and SrcUsername are defined. or more information and list of allowed values, see [UserScope](normalization-entity-user#userscope) in the [Schema Overview article](normalization-about-schemas). |
| **SrcUserScopeId** | Optional | String | The scope ID, such as Microsoft Entra Directory ID, in which SrcUserId and SrcUsername are defined. for more information and list of allowed values, see [UserScopeId](normalization-entity-user#userscopeid) in the [Schema Overview article](normalization-about-schemas). |
| **SrcUserIdType** | Conditional | UserIdType | The type of the ID stored in the SrcUserId field. For a list of allowed values and further information, refer to [UserIdType](normalization-entity-user#useridtype) in the [Schema Overview article](normalization-about-schemas). |
| **SrcUsername** | Optional | Username (String) | The source username, including domain information when available. For the supported format for different ID types, refer to [the User entity](normalization-entity-user). Use the simple form only if domain information isn't available.Store the Username type in the SrcUsernameType field. If other username formats are available, store them in the fields `SrcUsername<UsernameType>`.Example: `AlbertE` |
| **SrcUsernameType** | Conditional | UsernameType | Specifies the type of the username stored in the SrcUsername field. For a list of allowed values and further information, refer to [UsernameType](normalization-entity-user#usernametype) in the [Schema Overview article](normalization-about-schemas).Example: `Windows` |
| **SrcUserType** | Optional | UserType | The type of source user. For a list of allowed values and further information, refer to [UserType](normalization-entity-user#usertype) in the [Schema Overview article](normalization-about-schemas). **Note**: The value might be provided in the source record by using different terms, which should be normalized to these values. Store the original value in the SrcOriginalUserType field. |
| **SrcOriginalUserType** | Optional | String | The original destination user type, if provided by the reporting device. |

### Source application fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **SrcAppName** | Optional | String | The name of the source application. Example: `filezilla.exe` |
| **SrcAppId** | Optional | String | The ID of the source application, as reported by the reporting device. If SrcAppType is `Process`, `SrcAppId` and `SrcProcessId` should have the same value.Example: `124` |
| **SrcAppType** | Optional | AppType | The type of the source application. For a list of allowed values and further information, refer to [AppType](normalization-about-schemas#apptype) in the [Schema Overview article](normalization-about-schemas).This field is mandatory if SrcAppName or SrcAppId are used. |
| **SrcProcessName** | Optional | String | The file name of the process that initiated the network session. This name is typically considered to be the process name. Example: `C:\Windows\explorer.exe` |
| **SrcProcessId** | Optional | String | The process ID (PID) of the process that initiated the network session.Example: `48610176`**Note**: The type is defined as *string* to support varying systems, but on Windows and Linux this value must be numeric. If you are using a Windows or Linux machine and used a different type, make sure to convert the values. For example, if you used a hexadecimal value, convert it to a decimal value. |
| **SrcProcessGuid** | Optional | String | A generated unique identifier (GUID) of the process that initiated the network session.  Example: `EF3BD0BD-2B74-60C5-AF5C-010000001E00` |

### Local and remote aliases

All the source and destination fields listed above, can be optionally aliased by fields with the same name and the descriptors `Local` and `Remote`. This is typically helpful for events reported by an endpoint and for which the event type is `EndpointNetworkSession`.

For such events the descriptors `Local` and `Remote` denote the endpoint itself and the device at the other end of the network session respectively. For inbound connections, the local system is the destination, `Local` fields are aliases to the `Dst` fields, and 'Remote' fields are aliases to `Src` fields. Conversely, for outbound connections, the local system is the source, `Local` fields are aliases to the `Src` fields, and `Remote` fields are aliases to `Dst` fields.

For example, for an inbound event, the field `LocalIpAddr` is an alias to `DstIpAddr` and the field `RemoteIpAddr` is an alias to `SrcIpAddr`.

### Hostname and IP address aliases

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **Hostname** | Alias |  | - If the event type is `NetworkSession`, `Flow` or `L2NetworkSession`, Hostname is an alias to DstHostname. - If the event type is `EndpointNetworkSession`, Hostname is an alias to `RemoteHostname`, which can alias either DstHostname or SrcHostName, depending on NetworkDirection |
| **IpAddr** | Alias |  | - If the event type is `NetworkSession`, `Flow` or `L2NetworkSession`, IpAddr is an alias to SrcIpAddr. - If the event type is `EndpointNetworkSession`, IpAddr is an alias to `LocalIpAddr`, which can alias either SrcIpAddr or DstIpAddr, depending on NetworkDirection. |

### Intermediary device and Network Address Translation (NAT) fields

The following fields are useful if the record includes information about an intermediary device, such as a firewall or a proxy, which relays the network session.

Intermediary systems often use address translation and therefore the original address and the address observed externally are not the same. In such cases, the primary address fields such as SrcIPAddr and DstIpAddr represent the addresses observed externally, while the NAT address fields, SrcNatIpAddr and DstNatIpAddr represent the internal address of the original device before translation.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **DstNatIpAddr** | Optional | IP address | The **DstNatIpAddr** represents either of: - The original address of the destination device if network address translation was used. - The IP address used by the intermediary device for communication with the source.Example: `2::1` |
| **DstNatPortNumber** | Optional | Integer | If reported by an intermediary NAT device, the port used by the NAT device for communication with the source.Example: `443` |
| **SrcNatIpAddr** | Optional | IP address | The **SrcNatIpAddr** represents either of: - The original address of the source device if network address translation was used. - The IP address used by the intermediary device for communication with the destination.Example: `4.3.2.1` |
| **SrcNatPortNumber** | Optional | Integer | If reported by an intermediary NAT device, the port used by the NAT device for communication with the destination.Example: `345` |
| **DvcInboundInterface** | Optional | String | If reported by an intermediary device, the network interface used by the NAT device for the connection to the source device.Example: `eth0` |
| **DvcOutboundInterface** | Optional | String | If reported by an intermediary device, the network interface used by the NAT device for the connection to the destination device.Example: `Ethernet adapter Ethernet 4e` |

### Inspection fields

The following fields are used to represent that inspection which a security device such as a firewall, an IPS, or a web security gateway performed:

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **NetworkRuleName** | Optional | String | The name or ID of the rule by which DvcAction was decided upon. Example: `AnyAnyDrop` |
| **NetworkRuleNumber** | Optional | Integer | The number of the rule by which DvcAction was decided upon.Example: `23` |
| **Rule** | Alias | String | Either the value of NetworkRuleName or the value of NetworkRuleNumber. If the value of NetworkRuleNumber is used, the type should be converted to string. |
| **ThreatId** | Optional | String | The ID of the threat or malware identified in the network session.Example: `Tr.124` |
| **ThreatName** | Optional | String | The name of the threat or malware identified in the network session.Example: `EICAR Test File` |
| **ThreatCategory** | Optional | String | The category of the threat or malware identified in the network session.Example: `Trojan` |
| **ThreatRiskLevel** | Optional | RiskLevel (Integer) | The risk level associated with the session. The level should be a number between **0** and **100**.**Note**: The value might be provided in the source record by using a different scale, which should be normalized to this scale. The original value should be stored in ThreatRiskLevelOriginal. |
| **ThreatOriginalRiskLevel** | Optional | String | The risk level as reported by the reporting device. |
| **ThreatIpAddr** | Optional | IP Address | An IP address for which a threat was identified. The field ThreatField contains the name of the field **ThreatIpAddr** represents. |
| **ThreatField** | Conditional | Enumerated | The field for which a threat was identified. The value is either `SrcIpAddr` or `DstIpAddr`. |
| **ThreatConfidence** | Optional | ConfidenceLevel (Integer) | The confidence level of the threat identified, normalized to a value between 0 and a 100. |
| **ThreatOriginalConfidence** | Optional | String | The original confidence level of the threat identified, as reported by the reporting device. |
| **ThreatIsActive** | Optional | Boolean | True if the threat identified is considered an active threat. |
| **ThreatFirstReportedTime** | Optional | datetime | The first time the IP address or domain were identified as a threat. |
| **ThreatLastReportedTime** | Optional | datetime | The last time the IP address or domain were identified as a threat. |

### Other fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **ASimMatchingIpAddr** | Recommended | Enumerated | When a parser uses the `ipaddr_has_any_prefix` filtering parameters, this field is set with the one of the values `SrcIpAddr`, `DstIpAddr`, or `Both` to reflect the matching fields or fields. |
| **ASimMatchingHostname** | Recommended | Enumerated | When a parser uses the `hostname_has_any` filtering parameters, this field is set with the one of the values `SrcHostname`, `DstHostname`, or `Both` to reflect the matching fields or fields. |

If the event is reported by one of the endpoints of the network session, it might include information about the process that initiated or terminated the session. In such cases, the [ASIM Process Event schema](normalization-schema-process-event) is used to normalize this information.

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
| 0.2.1 | - Added `Src` and `Dst` as aliases to a leading identifier for the source and destination systems.- Added the fields `NetworkConnectionHistory`, `SrcVlanId`, `DstVlanId`, `InnerVlanId`, and `OuterVlanId`. |
| 0.2.2 | - Added the `Remote` and `Local` aliases.- Added the event type `EndpointNetworkSession`.- Defined `Hostname` and `IpAddr` as aliases for `RemoteHostname` and `LocalIpAddr`, respectively, when the event type is `EndpointNetworkSession`.- Defined `DvcInterface` as an alias to `DvcInboundInterface` or `DvcOutboundInterface`.- Changed the type of `SrcBytes`, `DstBytes`, `NetworkBytes`, `SrcPackets`, `DstPackets`, and `NetworkPackets` from Integer to Long.- Added the field `NetworkProtocolVersion`.- Deprecated `DstUserDomain` and `SrcUserDomain`. |
| 0.2.3 | - Added the `ipaddr_has_any_prefix` filtering parameter.- Updated the `hostname_has_any` filtering parameter to match either source or destination hostnames.- Added the fields `ASimMatchingHostname` and `ASimMatchingIpAddr`. |
| 0.2.4 | - Added the `TcpFlags` fields.- Updated `NetworkIcpmType` and `NetworkIcmpCode` to reflect their numeric values.- Added inspection fields.- Renamed `ThreatRiskLevelOriginal` to `ThreatOriginalRiskLevel` to align with ASIM conventions.- Marked `EventResultDetails` as recommended and specified the allowed values. |
| 0.2.5 | Added the fields `DstUserScope`, `SrcUserScope`, `SrcDvcScopeId`, `SrcDvcScope`, `DstDvcScopeId`, `DstDvcScope`, `DvcScopeId`, and `DvcScope`. |
| 0.2.6 | Added IDS as an event type. |
| 0.2.7 | Added the fields `DstDescription` and `SrcDescription`. |
| 1.0.0 | Added entity correlation fields. |