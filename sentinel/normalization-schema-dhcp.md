---
layout: Conceptual
title: The Advanced Security Information Model (ASIM) DHCP normalization schema reference | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/normalization-schema-dhcp
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
ms.reviewer: noak
description: This article describes the Microsoft Sentinel DHCP normalization schema.
ms.author: guywild
author: guywi-ms
ms.topic: reference
ms.date: 2026-09-16T00:00:00.0000000Z
locale: en-us
document_id: 656366d1-19dc-ab05-6a41-9457a26bda09
document_version_independent_id: 8b9ff391-ab96-a1c4-2002-dfab120e1139
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/normalization-schema-dhcp.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/normalization-schema-dhcp
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/normalization-schema-dhcp.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: dda21b78-5065-78fa-3618-57cc3506a00d
---

# The Advanced Security Information Model (ASIM) DHCP normalization schema reference | Microsoft Learn

The DHCP information model is used to describe events reported by a DHCP server, and is used by Microsoft Sentinel to enable source-agnostic analytics.

For more information, see [Normalization and the Advanced Security Information Model (ASIM)](normalization).

## Parsers

For more information about ASIM parsers, see the [ASIM parsers overview](normalization-parsers-overview).

### Filtering parser parameters

The DHCP parsers support [filtering parameters](normalization-about-parsers#optimizing-parsing-using-parameters). While these parameters are optional, they can improve your query performance.

The following filtering parameters are available:

| Name | Type | Description |
| --- | --- | --- |
| **starttime** | datetime | Filter only DHCP events that occurred at or after this time. This parameter filters on the `TimeGenerated` field, which is the standard designator for the time of the event, regardless of the parser-specific mapping of the EventStartTime and EventEndTime fields. |
| **endtime** | datetime | Filter only DHCP events that occurred at or before this time. This parameter filters on the `TimeGenerated` field, which is the standard designator for the time of the event, regardless of the parser-specific mapping of the EventStartTime and EventEndTime fields. |
| **srcipaddr\_has\_any\_prefix** | dynamic | Filter only DHCP events where the source IP address prefix matches any of the listed values. Prefixes should end with a `.`, for example: `10.0.`. |
| **srchostname\_has\_any** | dynamic | Filter only DHCP events where the source hostname has any of the listed values. |
| **srcusername\_has\_any** | dynamic | Filter only DHCP events where the source username has any of the listed values. |
| **eventresult** | string | Filter only DHCP events with a specific event result. Use `*` to include all results. |

For example, to filter only DHCP events from a specific IP address range in the last day, use:

```kusto
_Im_DhcpEvent (srcipaddr_has_any_prefix=dynamic(['10.0.']), starttime = ago(1d), endtime=now())
```

## Schema overview

The ASIM DHCP schema represents DHCP server activity, including serving requests for DHCP IP address leased from client systems and updating a DNS server with the leases granted.

The most important fields in a DHCP event are SrcIpAddr and SrcHostname, which the DHCP server binds by granting the lease, and are aliased by IpAddr and Hostname fields respectively. The SrcMacAddr field is also important as it represents the client machine used when an IP address isn't leased.

A DHCP server may reject a client, either due to the security concerns, or because of network saturation. It may also quarantine a client by leasing to it an IP address that would connect it to a limited network. The [EventResult](normalization-common-fields#eventresult), [EventResultDetails](normalization-common-fields#eventresultdetails) and [DvcAction](normalization-common-fields#dvcaction) fields provide information about the DHCP server response and action.

A lease's duration is stored in the DhcpLeaseDuration field.

## Schema details

ASIM is aligned with the [Open Source Security Events Metadata (OSSEM)](https://github.com/OTRF/OSSEM) project.

OSSEM doesn't have a DHCP schema comparable to the ASIM DHCP schema.

### Common ASIM fields

Important

Fields common to all schemas are described in detail in the [ASIM Common Fields](normalization-common-fields) article.

#### Common Fields with specific guidelines

The following list mentions fields that have specific guidelines for DHCP events:

| **Field** | **Class** | **Type** | **Description** |
| --- | --- | --- | --- |
| **EventType** | Mandatory | Enumerated | Indicate the operation reported by the record.  Possible values are `Assign`, `Renew`, `Release`, and `DNS Update`. Example: `Assign` |
| **EventSchemaVersion** | Mandatory | SchemaVersion (String) | The version of the schema documented here is **1.0.0**. |
| **EventSchema** | Mandatory | String | The name of the schema documented here's **DhcpEvent**. |
| **Dvc** fields | - | - | For DHCP events, device fields refer to the system that reports the DHCP event. |

#### All common fields

Fields that appear in the table are common to all ASIM schemas. Any guideline specified above overrides the general guidelines for the field. For example, a field might be optional in general, but mandatory for a specific schema. For more information on each field, see the [ASIM Common Fields](normalization-common-fields) article.

| **Class** | **Fields** |
| --- | --- |
| Mandatory | - [EventCount](normalization-common-fields#eventcount) - [EventStartTime](normalization-common-fields#eventstarttime) - [EventEndTime](normalization-common-fields#eventendtime) - [EventType](normalization-common-fields#eventtype)- [EventResult](normalization-common-fields#eventresult) - [EventProduct](normalization-common-fields#eventproduct) - [EventVendor](normalization-common-fields#eventvendor) - [EventSchema](normalization-common-fields#eventschema) - [EventSchemaVersion](normalization-common-fields#eventschemaversion) - [Dvc](normalization-common-fields#dvc) |
| Recommended | - [EventResultDetails](normalization-common-fields#eventresultdetails)- [EventSeverity](normalization-common-fields#eventseverity)- [EventUid](normalization-common-fields#eventuid) - [DvcIpAddr](normalization-common-fields#dvcipaddr) - [DvcHostname](normalization-common-fields#dvchostname) - [DvcDomain](normalization-common-fields#dvcdomain)- [DvcDomainType](normalization-common-fields#dvcdomaintype)- [DvcFQDN](normalization-common-fields#dvcfqdn)- [DvcId](normalization-common-fields#dvcid)- [DvcIdType](normalization-common-fields#dvcidtype)- [DvcAction](normalization-common-fields#dvcaction) |
| Optional | - [EventMessage](normalization-common-fields#eventmessage) - [EventSubType](normalization-common-fields#eventsubtype)- [EventOriginalUid](normalization-common-fields#eventoriginaluid)- [EventOriginalType](normalization-common-fields#eventoriginaltype)- [EventOriginalSubType](normalization-common-fields#eventoriginalsubtype)- [EventOriginalResultDetails](normalization-common-fields#eventoriginalresultdetails) - [EventOriginalSeverity](normalization-common-fields#eventoriginalseverity) - [EventProductVersion](normalization-common-fields#eventproductversion) - [EventReportUrl](normalization-common-fields#eventreporturl) - [EventOwner](normalization-common-fields#eventowner)- [DvcZone](normalization-common-fields#dvczone)- [DvcMacAddr](normalization-common-fields#dvcmacaddr)- [DvcOs](normalization-common-fields#dvcos)- [DvcOsVersion](normalization-common-fields#dvchostname)- [DvcOriginalAction](normalization-common-fields#dvcoriginalaction)- [DvcInterface](normalization-common-fields#dvcinterface)- [AdditionalFields](normalization-common-fields#additionalfields)- [DvcDescription](normalization-common-fields#dvcdescription)- [DvcScopeId](normalization-common-fields#dvcscopeid)- [DvcScope](normalization-common-fields#dvcscope) |

### DHCP-specific fields

| **Field** | **Class** | **Type** | **Notes** |
| --- | --- | --- | --- |
| **DhcpLeaseDuration** | Optional | Integer | The length of the lease granted to a client, in seconds. |
| **DhcpSessionId** | Optional | string | The session identifier as reported by the reporting device. For the Windows DHCP server, set this to the TransactionID field. Example: `2099570186` |
| **SessionId** | Alias | String | Alias to DhcpSessionId |
| **DhcpSessionDuration** | Optional | Integer | The amount of time, in milliseconds, for the completion of the DHCP session.Example: `1500` |
| **Duration** | Alias |  | Alias to DhcpSessionDuration |
| **DhcpSrcDHCId** | Optional | String | The DHCP client ID, as defined by [RFC4701](https://datatracker.ietf.org/doc/html/rfc4701) |
| **DhcpCircuitId** | Optional | String | The DHCP circuit ID, as defined by [RFC3046](https://datatracker.ietf.org/doc/html/rfc3046) |
| **DhcpSubscriberId** | Optional | String | The DHCP subscriber ID, as defined by [RFC3993](https://datatracker.ietf.org/doc/html/rfc3993) |
| **DhcpVendorClassId** | Optional | String | The DHCP Vendor Class Id, as defined by [RFC3925](https://datatracker.ietf.org/doc/html/rfc3925). |
| **DhcpVendorClass** | Optional | String | The DHCP Vendor Class, as defined by [RFC3925](https://datatracker.ietf.org/doc/html/rfc3925). |
| **DhcpUserClassId** | Optional | String | The DHCP User Class ID, as defined by [RFC3004](https://datatracker.ietf.org/doc/html/rfc3004). |
| **DhcpUserClass** | Optional | String | The DHCP User Class, as defined by [RFC3004](https://datatracker.ietf.org/doc/html/rfc3004). |
| **RequestedIpAddr** | Optional | IP Address | The IP address requested by the DHCP client, when available.Example: `192.168.12.3` |

### Source system fields

The source system is the system that requests a DHCP lease

| **Field** | **Class** | **Type** | **Notes** |
| --- | --- | --- | --- |
| **Src** | Alias | String | A unique identifier of the source device. This field might alias the SrcDvcId, SrcHostname, or SrcIpAddr fields. Example: `192.168.12.1` |
| **SrcIpAddr** | Mandatory | IP Address | The IP address assigned to the client by the DHCP server.Example: `192.168.12.1` |
| **IpAddr** | Alias |  | Alias for SrcIpAddr |
| **SrcHostname** | Mandatory | Hostname (String) | The hostname of the device requesting the DHCP lease. If no device name is available, store the relevant IP address in this field.Example: `DESKTOP-1282V4D` |
| **Hostname** | Alias |  | Alias for SrcHostname |
| **SrcDomain** | Recommended | Domain (String) | The domain of the source device.Example: `Contoso` |
| **SrcDomainType** | Conditional | Enumerated | The type of SrcDomain, if known. Possible values include:- `Windows` (such as: `contoso`)- `FQDN` (such as: `microsoft.com`)Required if SrcDomain is used. |
| **SrcFQDN** | Optional | FQDN (String) | The source device hostname, including domain information when available. **Note**: This field supports both traditional FQDN format and Windows domain\hostname format. The SrcDomainType field reflects the format used. Example: `Contoso\DESKTOP-1282V4D` |
| **SrcDvcId** | Optional | String | The ID of the source device as reported in the record.For example: `ac7e9755-8eae-4ffc-8a02-50ed7a2216c3` |
| **SrcDvcScopeId** | Optional | String | The cloud platform scope ID the device belongs to. **SrcDvcScopeId** map to a subscription ID on Azure and to an account ID on AWS. |
| **SrcDvcScope** | Optional | String | The cloud platform scope the device belongs to. **SrcDvcScope** map to a subscription ID on Azure and to an account ID on AWS. |
| **SrcDvcIdType** | Conditional | Enumerated | The type of SrcDvcId, if known. Possible values include: - `AzureResourceId`- `MDEid`If multiple IDs are available, use the first one from the list above, and store the others in the **SrcDvcAzureResourceId** and **SrcDvcMDEid**, respectively.**Note**: This field is required if SrcDvcId is used. |
| **SrcDeviceType** | Optional | Enumerated | The type of the source device. Possible values include:- `Computer`- `Mobile Device`- `IOT Device`- `Other` |
| **SrcDescription** | Optional | String | A descriptive text associated with the device. For example: `Primary Domain Controller`. |
| **SrcGeoCountry** | Optional | Country | The country/region associated with the source IP address.Example: `USA` |
| **SrcGeoRegion** | Optional | Region | The region associated with the source IP address.Example: `Vermont` |
| **SrcGeoCity** | Optional | City | The city associated with the source IP address.Example: `Burlington` |
| **SrcGeoLatitude** | Optional | Latitude | The latitude of the geographical coordinate associated with the source IP address.Example: `44.475833` |
| **SrcGeoLongitude** | Optional | Longitude | The longitude of the geographical coordinate associated with the source IP address.Example: `73.211944` |
| **SrcRiskLevel** | Optional | Integer | The risk level associated with the source. The value should be adjusted to a range of `0` to `100`, with `0` for benign and `100` for a high risk.Example: `90` |
| **SrcOriginalRiskLevel** | Optional | String | The risk level associated with the source, as reported by the reporting device. Example: `Suspicious` |
| **SrcPortNumber** | Optional | Integer | The IP port from which the connection originated. Might not be relevant for a session comprising multiple connections.Example: `2335` |

### Source user fields

| **Field** | **Class** | **Type** | **Notes** |
| --- | --- | --- | --- |
| **SrcUserId** | Optional | String | A machine-readable, alphanumeric, unique representation of the source user. For more information, and for alternative fields for additional IDs, see [The User entity](normalization-entity-user). Example: `S-1-12-1-4141952679-1282074057-627758481-2916039507` |
| **SrcUserIdType** | Conditional | UserIdType | The type of the ID stored in the SrcUserId field. For more information and list of allowed values, see [UserIdType](normalization-entity-user#useridtype) in the [Schema Overview article](normalization-about-schemas). |
| **SrcUsername** | Optional | Username (String) | The source username, including domain information when available. For more information, see [The User entity](normalization-entity-user).Example: `AlbertE` |
| **User** | Alias |  | Alias for SrcUsername |
| **SrcUsernameType** | Conditional | UsernameType | Specifies the type of the user name stored in the SrcUsername field. For more information, and list of allowed values, see [UsernameType](normalization-entity-user#usernametype) in the [Schema Overview article](normalization-about-schemas). Example: `Windows` |
| **SrcUserType** | Optional | UserType | The type of the source user. For more information, and list of allowed values, see [UserType](normalization-entity-user#usertype) in the [Schema Overview article](normalization-about-schemas).For example: `Guest` |
| **SrcOriginalUserType** | Optional | String | The original source user type, if provided by the source. |
| **SrcMacAddr** | Mandatory | Mac Address | The MAC address of the client requesting a DHCP lease. **Note**: The Windows DHCP server logs MAC address in a nonstandard way, omitting the colons, which should be inserted by the parser.Example: `06:10:9f:eb:8f:14` |
| **SrcUserScope** | Optional | String | The scope, such as Microsoft Entra tenant, in which SrcUserId and SrcUsername are defined. or more information and list of allowed values, see [UserScope](normalization-entity-user#userscope) in the [Schema Overview article](normalization-about-schemas). |
| **SrcUserScopeId** | Optional | String | The scope ID, such as Microsoft Entra Directory ID, in which SrcUserId and SrcUsername are defined. for more information and list of allowed values, see [UserScopeId](normalization-entity-user#userscopeid) in the [Schema Overview article](normalization-about-schemas). |
| **SrcUserSessionId** | Optional | String | The unique ID of the sign-in session of the Actor. Example: `102pTUgC3p8RIqHvzxLCHnFlg` |

### Inspection fields

| **Field** | **Class** | **Type** | **Notes** |
| --- | --- | --- | --- |
| **Rule** | Alias | string | Either the value of RuleName or the value of RuleNumber. If the value of RuleNumber is used, the type should be converted to string. |
| **RuleNumber** | Optional | int | The number of the rule associated with the alert.e.g. `123456` |
| **RuleName** | Optional | string | The name or ID of the rule associated with the alert.e.g. `Server PSEXEC Execution via Remote Access` |
| **ThreatId** | Optional | string | The ID of the threat or malware identified in the alert. e.g. `1234567891011121314` |
| **ThreatCategory** | Optional | String | The category of the threat or malware identified in the alert.Supported values are: `Malware`, `Ransomware`, `Trojan`, `Virus`, `Worm`, `Adware`, `Spyware`, `Rootkit`, `Cryptominor`, `Phishing`, `Spam`, `MaliciousUrl`, `Spoofing`, `Security Policy Violation`, `Unknown` |
| **ThreatName** | Optional | string | The name of the threat or malware identified in the alert. e.g. `Init.exe` |
| **ThreatConfidence** | Optional | ConfidenceLevel (Integer) | The confidence level of the threat identified, normalized to a value between 0 and a 100. |
| **ThreatOriginalConfidence** | Optional | string | The confidence level as reported by the originating system. |
| **ThreatRiskLevel** | Optional | RiskLevel (Integer) | The risk level associated with the threat. The level should be a number between 0 and 100.**Note**: The value might be provided in the source record by using a different scale, which should be normalized to this scale. The original value should be stored in ThreatRiskLevelOriginal. |
| **ThreatOriginalRiskLevel** | Optional | string | The risk level as reported by the originating system. |
| **ThreatIsActive** | Optional | bool | Indicates whether the threat is currently active.Supported values are: `True`, `False` |
| **ThreatFirstReportedTime** | Optional | Date/Time | Date and time when the threat was first reported. e.g. `2024-09-19T10:12:10.0000000Z` |
| **ThreatLastReportedTime** | Optional | Date/Time | Date and time when the threat was last reported. e.g. `2024-09-19T10:12:10.0000000Z` |

### Entity correlation fields

Note

Contributors don't need to populate these fields. Applicable parsers will populate them when internal Microsoft support is added.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **SrcSystemEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the source system within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **SrcUserAdditionalIds** | Optional | Dynamic | For the field structure and usage, see [Fields suffixed with AdditionalIds](normalization-common-fields#fields-suffixed-with-additionalids). |
| **SrcUserEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the source user within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |

## Schema updates

| Version | Changes |
| --- | --- |
| 0.1.1 | - Added inspection fields.- Added the source geolocation fields.- Added the source fields `SrcDescription`, `SrcOriginalRiskLevel`, `SrcOriginalUserType`, `SrcPortNumber`, `SrcRiskLevel`, `SrcUserScope`, `SrcUserScopeId`, `SrcUserSessionId`, and `SrcUserUid`.- Added the aliases `Src` and `User`.- The fields `SrcUserUid` and `ThreatField` are available in the `ASimDhcpEventLogs` table but aren't part of the schema. |
| 1.0.0 | Added entity correlation fields. |