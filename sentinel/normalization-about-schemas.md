---
layout: Conceptual
title: Advanced Security Information Model (ASIM) schemas | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/normalization-about-schemas
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
description: This article explains Advanced Security Information Model (ASIM) schemas, and how they help. ASIM normalizes data from many different sources to a uniform presentation.
ms.author: edbaynash
author: EdB-MSFT
ms.topic: article
ms.date: 2026-09-16T00:00:00.0000000Z
locale: en-us
document_id: b15321ad-82c4-dbeb-00b8-47ced715869a
document_version_independent_id: cf9361c1-1f5d-37d8-8dad-4dba77282a92
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/normalization-about-schemas.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/normalization-about-schemas
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/normalization-about-schemas.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/97159432-14a9-4307-a469-d2f2c75f0e33
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/50565c62-5f6b-4687-be38-323113c72c2e
platformId: acc04d2b-0519-d800-cfcc-e5eb3b24eab0
---

# Advanced Security Information Model (ASIM) schemas | Microsoft Learn

An Advanced Security Information Model ([ASIM](normalization)) schema is a set of fields that represent an activity or entity. Using the fields from a normalized schema in a query ensures that the query works with every normalized source.

To understand how schemas fit within the ASIM architecture, refer to the [ASIM architecture diagram](normalization#asim-components).

## Activity/Event Schemas

Schema references outline the fields that comprise each schema. ASIM currently defines the following schemas for events:

| Schema | Schema Name for Tests | Version | Status |
| --- | --- | --- | --- |
| [Agent Event](normalization-schema-agent) | `AgentEvent` | 1.0.0 | GA |
| [Alert Event](normalization-schema-alert) | `AlertEvent` | 1.0.0 | GA |
| [Audit Event](normalization-schema-audit) | `AuditEvent` | 1.0.0 | GA |
| [Authentication Event](normalization-schema-authentication) | `Authentication` | 1.0.0 | GA |
| [DHCP Activity](normalization-schema-dhcp) | `DhcpEvent` | 1.0.0 | GA |
| [DNS Activity](normalization-schema-dns) | `Dns` | 1.0.0 | GA |
| [Email Event](normalization-schema-email) | `EmailEvent` | 1.0.0 | GA |
| [File Activity](normalization-schema-file-event) | `FileEvent` | 1.0.0 | GA |
| [Network Session](normalization-schema) | `NetworkSession` | 1.0.0 | GA |
| [Process Event](normalization-schema-process-event) | `ProcessEvent` | 1.0.0 | GA |
| [Registry Event](normalization-schema-registry-event) | `RegistryEvent` | 1.0.0 | GA |
| [User Management](normalization-schema-user-management) | `UserManagement` | 1.0.0 | GA |
| [Web Session](normalization-schema-web) | `WebSession` | 1.0.0 | GA |

## Entity Schemas

ASIM currently defines the following schemas for entities:

| Schema | Schema Name for Tests | Version | Status |
| --- | --- | --- | --- |
| [Asset Entity](normalization-schema-asset) | `AssetEntity` | 1.0.0 | GA |

For entities which are part of other ASIM schemas, refer to Event Entities.

## Field naming

At the core of each schema are its field names. Field names belong to the following groups:

- Fields common to all schemas.
- Fields specific to a schema.
- Fields that represent entities, such as users, which take part in the schema. Fields that represent entities are similar across schemas.

When sources have fields that aren't presented in the documented schema, they're normalized to maintain consistency. If the extra fields represent an entity, they're normalized based on the entity field guidelines. Otherwise, the schemas strive to keep consistency across all schemas. For example, while DNS server activity logs don't provide user information, DNS activity logs from an endpoint might include user information, which can be normalized according to the user entity guidelines.

## Common fields

Some fields are common to all ASIM schemas. Each schema might add guidelines for using some of the common fields in the context of the specific schema. For example, permitted values for the **EventType** field might vary per schema, as might the value of the **EventSchemaVersion** field.

## Field classes

Fields might have several classes, which define when the fields should be implemented by a parser:

- **Mandatory** fields must appear in every parser. If your source doesn't provide information for this value, or the data can't be otherwise added, it does not support most content items that reference the normalized schema.
- **Recommended** fields should be normalized if available. However, they might not be available in every source. Any content item that references that normalized schema should take availability into account.
- **Optional** fields, if available, can be normalized or left in their original form. Typically, a minimal parser wouldn't normalize them for performance reasons.
- **Conditional** fields are mandatory if the field they follow is populated. Conditional fields are typically used to describe the value in another field. For example, the common field [DvcIdType](normalization-common-fields#dvcidtype) describes the value int the common field [DvcId](normalization-common-fields#dvcid) and is therefore mandatory if the latter is populated.
- **Alias** is a special type of a conditional field, and is mandatory if the aliased field is populated.

## Event Entities

Events evolve around entities, such as users, hosts, processes, or files. Each entity might require several fields to describe it. For example, a host might have a name and an IP address.

A single record might include multiple entities of the same type, such as both a source and destination host. ASIM defines how to describe entities consistently, and entities allow for extending the schemas. For example, while the Network Session schema doesn't include process information, some event sources do provide process information that can be added. For more information, see Entities.

To enable entity functionality, entity representation has the following guidelines:

| Guideline | Description |
| --- | --- |
| **Prefixes and aliasing** | Since a single event often includes more than one entity of the same type, such as source and destination hosts, *prefixes* are used to identify the entity a field is associated. To maintain normalization, ASIM uses a small set of standard prefixes, picking the most appropriate ones for the specific role of the entities. If a single entity of a type is relevant for an event, there's no need to use a prefix. Also, a set of fields without a prefix aliases the most used entity for each type. |
| **Identifiers and types** | A normalized schema allows for several identifiers for each entity, which we expect to coexist in events. If the source event has other entity identifiers that can't be mapped to the normalized schema, keep them in the source form or use the **AdditionalFields** dynamic field. To maintain the type information for the identifiers, store the type, when applicable, in a field with the same name and a suffix of **Type**. For example, **UserIdType**. |
| **Attributes** | Entities often have other attributes that don't serve as an identifier and can also be qualified with a descriptor. For example, if the source user has domain information, the normalized field is **SrcUserDomain**. |

For more information about specific entity types, refer to:

- [User Entity](normalization-entity-user)
- [Device Entity](normalization-entity-device)
- [Application Entity](normalization-entity-application)

For more information about full entity schemas, refer to:

- [Asset Entity Schema](normalization-schema-asset)

## Aliases

Aliases allow multiple names for a specified value. In some cases, different users expect a field to have different names. For example, in DNS terminology, you might expect a field named [DnsQuery](normalization-schema-dns#query), while more generally, it holds a domain name. The alias [Domain](normalization-schema-dns#domain) helps the user by allowing the use of both names.

Note

Aliases are intended to help an analyst with interactive queries. When using queries in reusable content such asn custom detections, analytic rules, or workbooks, use the aliased field rather than the alias. Using the aliased field ensures better performance, less errors and better query readability.

In some cases, an alias can have the value of one of several fields, depending on which values are available in the event. For example, the [Dvc](normalization-common-fields#dvc) alias, aliases either the [DvcFQDN](normalization-common-fields#dvcfqdn), [DvcId](normalization-common-fields#dvcid), [DvcHostname](normalization-common-fields#dvchostname), or [DvcIpAddr](normalization-common-fields#dvcipaddr) , or [Event Product](normalization-common-fields#eventproduct) fields. When an alias can have several values, its type has to be a string to accommodate all possible aliased values. As a result, when assigning a value to such an alias, make sure to convert the type to string using the KQL function [tostring](/en-us/kusto/query/tostring-function?view=microsoft-sentinel&amp;preserve-view=true).[Native normalized tables](normalization-ingest-time#ingest-time-parsing) don't include aliases, as those would imply duplicate data storage. Instead the [stub parsers](normalization-ingest-time#combining-ingest-time-and-query-time-normalization) add the aliases. To implement aliases in parsers, create a copy of the original value by using the `extend` operator.

## Logical types

Each schema field has a type. The Log Analytics workspace has a limited set of data types. For this reason, Microsoft Sentinel uses a logical type for many schema fields, which Log Analytics doesn't enforce but is required for schema compatibility. Logical field types ensure that both values and field names are consistent across sources.

| Data type | Physical type | Format and value |
| --- | --- | --- |
| **Boolean** | Bool | Use the built-in KQL `bool` data type rather than a numerical or string representation of Boolean values. |
| **Enumerated** | String | A list of values as explicitly defined for the field. The schema definition lists the accepted values. |
| **Date/Time** | Depending on the ingestion method capability, use any of the following physical representations in descending priority: - Log Analytics built-in datetime type - An integer field using Log Analytics datetime numerical representation. - A string field using Log Analytics datetime numerical representation - A string field storing a supported [Log Analytics date/time format](/en-us/kusto/query/scalar-data-types/datetime?view=microsoft-sentinel&amp;preserve-view=true). | [Log Analytics date and time representation](/en-us/kusto/query/scalar-data-types/datetime?view=microsoft-sentinel&amp;preserve-view=true) is similar but different than Unix time representation. For more information, see the [conversion guidelines](/en-us/kusto/query/datetime-timespan-arithmetic?view=microsoft-sentinel&amp;preserve-view=true). **Note**: When applicable, the time should be time zone adjusted. |
| **MAC address** | String | Colon-Hexadecimal notation. |
| **IP address** | String | Microsoft Sentinel schemas don't have separate IPv4 and IPv6 addresses. Any IP address field might include either an IPv4 address or an IPv6 address, as follows: - **IPv4** in a dot-decimal notation.- **IPv6** in 8-hextets notation, allowing for the short form.For example:- **IPv4**: `192.168.10.10`- **IPv6**: `FEDC:BA98:7654:3210:FEDC:BA98:7654:3210`- **IPv6 short form**: `1080::8:800:200C:417A` |
| **FQDN** | String | A fully qualified domain name using a dot notation, for example, `learn.microsoft.com`. For more information, see [The Device entity](normalization-entity-device). |
| **Hostname** | String | A hostname that isn't an FQDN, includes up to 63 characters including letters, numbers, and hyphens. For more information, see [The Device entity](normalization-entity-device). |
| **Domain** | String | the domain part of an FQDN, without the hostname, for example, `learn.microsoft.com`. For more information, see [The Device entity](normalization-entity-device). |
| **DomainType** | Enumerated | The type of domain stored in domain and FQDN fields. For a list of values and more information, see [The Device entity](normalization-entity-device). |
| **DvcIdType** | Enumerated | The type of the device ID stored in DvcId fields. For a list of allowed values and further information, refer to [DvcIdType](normalization-entity-device#dvcidtype). |
| **DeviceType** | Enumerated | The type of the device stored in DeviceType fields. Possible values include:- `Computer`- `Mobile Device`- `IOT Device`- `Other`. For more information, see [The Device entity](normalization-entity-device). |
| **Username** | String | A valid username in one of the supported types. For more information, see [The User entity](normalization-entity-user). |
| **UsernameType** | Enumerated | The type of username stored in username fields. For more information and list of supported values, see [The User entity](normalization-entity-user). |
| **UserIdType** | Enumerated | The type of the ID stored in user ID fields. Supported values are `SID`, `UIS`, `AADID`, `OktaId`, `AWSId`, and `PUID`. For more information, see [The User entity](normalization-entity-user). |
| **UserType** | Enumerated | The type of a user. For more information and list of allowed values, see [The User entity](normalization-entity-user). |
| **AppType** | Enumerated | The type of an application. For a list of supported values, see [The Application Entity](normalization-entity-application#apptype). |
| **Country** | String | A string using [ISO 3166-1](https://www.iso.org/iso-3166-country-codes.html), according to the following priority:  - Alpha-2 codes, such as `US` for the United States.  - Alpha-3 codes, such as `USA` for the United States. - Short name.The list of codes can be found on the [International Standards Organization (ISO) website](https://www.iso.org/obp/ui/#search). |
| **Region** | String | The country/region subdivision name, using ISO 3166-2.The list of codes can be found on the [International Standards Organization (ISO) website](https://www.iso.org/obp/ui/#search). |
| **City** | String |  |
| **Longitude** | Double | ISO 6709 coordinate representation (signed decimal). |
| **Latitude** | Double | ISO 6709 coordinate representation (signed decimal). |
| **MD5** | String | 32-hex characters. |
| **SHA1** | String | 40-hex characters. |
| **SHA256** | String | 64-hex characters. |
| **SHA512** | String | 128-hex characters. |
| **ConfidenceLevel** | Integer | A confidence level normalized to the range of 0 to a 100. |
| **RiskLevel** | Integer | A risk level normalized to the range of 0 to a 100. |
| **SchemaVersion** | String | An ASIM schema version in the format `<major>.<minor>.<sub-minor>` |
| **DnsQueryClassName** | String | The [DNS class name](https://www.iana.org/assignments/dns-parameters/dns-parameters.xhtml). |
| **Username** | String | A simple or domain qualified username |

## Sample entity mapping

This section uses [Windows event 4624](/en-us/windows/security/threat-protection/auditing/event-4624) as an example to describe how the event data is normalized for Microsoft Sentinel.

This event has the following entities:

| Microsoft terminology | Original event field prefix | ASIM field prefix | Description |
| --- | --- | --- | --- |
| **Subject** | `Subject` | `Actor` | The user that reported information about a successful sign-in. |
| **New Logon** | `Target` | `TargetUser` | The user for which the sign-in was performed. |
| **Process** | - | `ActingProcess` | The process that attempted the sign-in. |
| **Network information** | - | `Src` | The machine from which a sign-in attempt was performed. |

Based on these entities, [Windows event 4624](/en-us/windows/security/threat-protection/auditing/event-4624) is normalized as follows (some fields are optional):

| Normalized field | Original field | Value in example | Notes |
| --- | --- | --- | --- |
| **ActorUserId** | SubjectUserSid | S-1-5-18 |  |
| **ActorUserIdType** | - | SID |  |
| **ActorUserName** | SubjectDomainName\ SubjectUserName | WORKGROUP\WIN-GG82ULGC9GO$ | Built by concatenating the two fields |
| **ActorUserNameType** | - | Windows |  |
| **ActorSessionId** | SubjectLogonId | 0x3e7 |  |
| **TargetUserId** | TargetUserSid | S-1-5-21-1377283216-344919071-3415362939-500 |  |
| **UserId** | TargetUserSid | Alias |  |
| **TargetUserIdType** | - | SID |  |
| **TargetUserName** | TargetDomainName\ TargetUserName | Administrator\WIN-GG82ULGC9GO$ | Built by concatenating the two fields |
| **Username** | TargetDomainName\ TargetUserName | Alias |  |
| **TargetUserNameType** | - | Windows |  |
| **TargetSessionId** | TargetLogonId | 0x8dcdc |  |
| **ActingProcessName** | ProcessName | C:\Windows\System32\svchost.exe |  |
| **ActingProcessId** | ProcessId | 0x44c |  |
| **SrcHostname** | WorkstationName | Windows |  |
| **SrcIpAddr** | IpAddress | 127.0.0.1 |  |
| **SrcPortNumber** | IpPort | 0 |  |
| **TargetHostname** | Computer | WIN-GG82ULGC9GO |  |
| **Hostname** | Computer | Alias |  |