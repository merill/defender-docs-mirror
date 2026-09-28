---
layout: Conceptual
title: The Advanced Security Information Model (ASIM) Audit Events normalization schema reference | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/normalization-schema-audit
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
description: This article displays the Microsoft Sentinel Audit Events normalization schema.
ms.author: edbaynash
author: EdB-MSFT
ms.topic: reference
ms.date: 2026-09-18T00:00:00.0000000Z
locale: en-us
document_id: f4daf8de-4e5d-6e08-966d-1facf1e29bf7
document_version_independent_id: bc302fbc-7061-ff41-e316-4ea73743ed5f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/normalization-schema-audit.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/normalization-schema-audit
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/normalization-schema-audit.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
platformId: 83121c18-16c2-72e4-4e88-fa772fb5affc
---

# The Advanced Security Information Model (ASIM) Audit Events normalization schema reference | Microsoft Learn

The Microsoft Sentinel Audit events normalization schema represents events associated with the audit trail of information systems. The audit trail logs system configuration activities and policy changes. Such changes are often performed by system administrators, but can also be performed by users when configuring the settings of their own applications.

Every system logs audit events alongside its core activity logs. For example, a Firewall will log events about the network sessions is processes, and audit events about configuration changes applied to the Firewall itself.

For more information about normalization in Microsoft Sentinel, see [Normalization and the Advanced Security Information Model (ASIM)](normalization).

## Schema overview

The main fields of an audit event are:

- The object, which may be, for example, a managed resource or policy rule, that the event focuses on, represented by the field Object. The field ObjectType specifies the type of the object.
- The application context of the object, represented by the field TargetAppName, which is aliased by Application.
- The operation performed on the object, represented by the fields EventType and Operation. While Operation is the value the source reported, EventType is a normalized version that is more consistent across sources.
- The old and new values for the object, if applicable, represented by OldValue and NewValue respectively.

Audit events also reference the following entities, which are involved in the configuration operation:

- **Actor** - The user performing the configuration operation.
- **TargetApp** - The application or system for which the configuration operation applies.
- **Target** - The system on which **TargetApp** is running.
- **ActingApp** - The application used by the **Actor** to perform the configuration operation.
- **Src** - The system used by the **Actor** to initiate the configuration operation, if different than **Target**.

The descriptor `Dvc` is used for the reporting device, which is the local system for sessions reported by an endpoint, and the intermediary or security device in other cases.

## Parsers

### Deploying and using audit events parsers

Deploy the ASIM audit events parsers from the [Microsoft Sentinel GitHub repository](https://aka.ms/DeployASIM). To query across all audit event sources, use the unifying parser `imAuditEvent` as the table name in your query.

For more information about using ASIM parsers, see the [ASIM parsers overview](normalization-parsers-overview). For the list of the audit event parsers Microsoft Sentinel provides out-of-the-box refer to the [ASIM parsers list](normalization-parsers-list#audit-event-parsers)

### Add your own normalized parsers

When implementing custom parsers for the File Event information model, name your KQL functions using the following syntax: `imAuditEvent<vendor><Product>`. Refer to the article [Managing ASIM parsers](normalization-manage-parsers) to learn how to add your custom parsers to the audit event unifying parser.

### Filtering parser parameters

The audit events parsers support [filtering parameters](normalization-about-parsers#optimizing-parsing-using-parameters). While these parameters are optional, they can improve your query performance.

The following filtering parameters are available:

| Name | Type | Description |
| --- | --- | --- |
| **starttime** | datetime | Filter only events that ran at or after this time. This parameter uses the `TimeGenerated` field as the time designator of the event. |
| **endtime** | datetime | Filter only events queries that finished running at or before this time. This parameter uses the `TimeGenerated` field as the time designator of the event. |
| **srcipaddr\_has\_any\_prefix** | dynamic | Filter only events from this source IP address, as represented in the SrcIpAddr field. |
| **eventtype\_in** | dynamic | Filter only events in which the event type, as represented in the EventType field, is any of the listed values. For example: `dynamic(['Create', 'Delete'])`. |
| **eventresult** | string | Filter only events in which the event result, as represented in the [EventResult](normalization-common-fields#eventresult) field is equal to the parameter value. |
| **actorusername\_has\_any** | dynamic/string | Filter only events in which the ActorUsername includes any of the terms provided. |
| **operation\_has\_any** | dynamic/string | Filter only events in which Operation field includes any of the terms provided. |
| **object\_has\_any** | dynamic/string | Filter only events in which Object field includes any of the terms provided. |
| **newvalue\_has\_any** | dynamic/string | Filter only events in which NewValue field includes any of the terms provided. |

Some parameter can accept both list of values of type `dynamic` or a single string value. To pass a literal list to parameters that expect a dynamic value, explicitly use a [dynamic literal](/en-us/kusto/query/scalar-data-types/dynamic?view=microsoft-sentinel&amp;preserve-view=true#dynamic-literals). For example: `dynamic(['192.168.','10.'])`

For example, to filter only audit events with the terms `install` or `update` in their Operation field, from the last day, use:

```kusto
imAuditEvent (operation_has_any=dynamic(['install','update']), starttime = ago(1d), endtime=now())
```

## Schema details

### Common ASIM fields

Important

Fields common to all schemas are described in detail in the [ASIM Common Fields](normalization-common-fields) article.

#### Common fields with specific guidelines

The following list mentions fields that have specific guidelines for Audit Events:

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **EventType** | Mandatory | Enumerated | Describes the operation audited by the event using a normalized value. Use EventSubType to provide further details, which the normalized value does not convey, and Operation. to store the operation as reported by the reporting device. For Audit Event records, the allowed values are: - `Set`- `Read`- `Create`- `Delete`- `Execute`- `Install`- `Clear`- `Enable`- `Disable`- `Initialize`- `Start`- `Stop`- `Other`Audit events represent a large variety of operations, and the `Other` value enables mapping operations that have no corresponding `EventType`. However, the use of `Other` limits the usability of the event and should be avoided if possible. |
| **EventSubType** | Optional | String | Provides further details, which the normalized value in EventType does not convey. |
| **EventSchema** | Mandatory | Enumerated | The name of the schema documented here is `AuditEvent`. |
| **EventSchemaVersion** | Mandatory | SchemaVersion (String) | The version of the schema. The version of the schema documented here is `1.0.0`. |

#### All common fields

Fields that appear in the table are common to all ASIM schemas. Any of guidelines specified in this document overrides the general guidelines for the field. For example, a field might be optional in general, but mandatory for a specific schema. For more information on each field, see the [ASIM Common Fields](normalization-common-fields) article.

| **Class** | **Fields** |
| --- | --- |
| Mandatory | - [EventCount](normalization-common-fields#eventcount) - [EventStartTime](normalization-common-fields#eventstarttime) - [EventEndTime](normalization-common-fields#eventendtime) - [EventType](normalization-common-fields#eventtype)- [EventResult](normalization-common-fields#eventresult) - [EventProduct](normalization-common-fields#eventproduct) - [EventVendor](normalization-common-fields#eventvendor) - [EventSchema](normalization-common-fields#eventschema) - [EventSchemaVersion](normalization-common-fields#eventschemaversion) - [Dvc](normalization-common-fields#dvc) |
| Recommended | - [EventResultDetails](normalization-common-fields#eventresultdetails)- [EventSeverity](normalization-common-fields#eventseverity)- [EventUid](normalization-common-fields#eventuid) - [DvcIpAddr](normalization-common-fields#dvcipaddr) - [DvcHostname](normalization-common-fields#dvchostname) - [DvcDomain](normalization-common-fields#dvcdomain)- [DvcDomainType](normalization-common-fields#dvcdomaintype)- [DvcFQDN](normalization-common-fields#dvcfqdn)- [DvcId](normalization-common-fields#dvcid)- [DvcIdType](normalization-common-fields#dvcidtype)- [DvcAction](normalization-common-fields#dvcaction) |
| Optional | - [EventMessage](normalization-common-fields#eventmessage) - [EventSubType](normalization-common-fields#eventsubtype)- [EventOriginalUid](normalization-common-fields#eventoriginaluid)- [EventOriginalType](normalization-common-fields#eventoriginaltype)- [EventOriginalSubType](normalization-common-fields#eventoriginalsubtype)- [EventOriginalResultDetails](normalization-common-fields#eventoriginalresultdetails) - [EventOriginalSeverity](normalization-common-fields#eventoriginalseverity) - [EventProductVersion](normalization-common-fields#eventproductversion) - [EventReportUrl](normalization-common-fields#eventreporturl) - [EventOwner](normalization-common-fields#eventowner)- [DvcZone](normalization-common-fields#dvczone)- [DvcMacAddr](normalization-common-fields#dvcmacaddr)- [DvcOs](normalization-common-fields#dvcos)- [DvcOsVersion](normalization-common-fields#dvchostname)- [DvcOriginalAction](normalization-common-fields#dvcoriginalaction)- [DvcInterface](normalization-common-fields#dvcinterface)- [AdditionalFields](normalization-common-fields#additionalfields)- [DvcDescription](normalization-common-fields#dvcdescription)- [DvcScopeId](normalization-common-fields#dvcscopeid)- [DvcScope](normalization-common-fields#dvcscope) |

### Audit fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **Operation** | Mandatory | String | The operation audited as reported by the reporting device. |
| **Object** | Mandatory | String | The name of the object on which the operation identified by EventType is performed. |
| **ObjectId** | Optional | String | The ID of the object on which the operation identified by EventType is performed. |
| **ObjectType** | Conditional | Enumerated | The type of Object. Allowed values are:- `Cloud Resource`- `Configuration Atom`- `Policy Rule`- `Event Log`-`Scheduled Task`-`Service`-`Directory Service Object`-`Other` |
| **OriginalObjectType** | Optional | String | The type of Object as reported by the reporting system |
| **OldValue** | Optional | String | The old value of Object prior to the operation, if applicable. |
| **NewValue** | Recommended | String | The new value of Object after the operation was performed, if applicable. |
| **Value** | Alias |  | Alias to NewValue |
| **ValueType** | Conditional | Enumerated | The type of the old and new values. Allowed values are- Other |

### Actor fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **ActorUserId** | Optional | String | A machine-readable, alphanumeric, unique representation of the Actor. For more information, and for alternative fields for other IDs, see [The User entity](normalization-entity-user). Example: `S-1-12-1-4141952679-1282074057-627758481-2916039507` |
| **ActorScope** | Optional | String | The scope, such as Microsoft Entra Domain Name, in which ActorUserId and ActorUsername are defined. or more information and list of allowed values, see [UserScope](normalization-entity-user#userscope) in the [Schema Overview article](normalization-about-schemas). |
| **ActorScopeId** | Optional | String | The scope ID, such as Microsoft Entra Directory ID, in which ActorUserId and ActorUsername are defined. for more information and list of allowed values, see [UserScopeId](normalization-entity-user#userscopeid) in the [Schema Overview article](normalization-about-schemas). |
| **ActorUserIdType** | Conditional | Enumerated | The type of the ID stored in the ActorUserId field. For more information and list of allowed values, see [UserIdType](normalization-entity-user#useridtype) in the [Schema Overview article](normalization-about-schemas). |
| **ActorUsername** | Recommended | Username (String) | The Actor’s username, including domain information when available. For more information, see [The User entity](normalization-entity-user).Example: `AlbertE` |
| **User** | Alias |  | Alias to ActorUsername |
| **ActorUsernameType** | Conditional | UsernameType | Specifies the type of the user name stored in the ActorUsername field. For more information, and list of allowed values, see [UsernameType](normalization-entity-user#usernametype) in the [Schema Overview article](normalization-about-schemas). Example: `Windows` |
| **ActorUserType** | Optional | UserType | The type of the Actor. For more information, and list of allowed values, see [UserType](normalization-entity-user#usertype) in the [Schema Overview article](normalization-about-schemas).For example: `Guest` |
| **ActorOriginalUserType** | Optional | String | The user type as reported by the reporting device. |
| **ActorSessionId** | Optional | String | The unique ID of the sign-in session of the Actor. Example: `102pTUgC3p8RIqHvzxLCHnFlg` |

### Target application fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **TargetAppId** | Optional | String | The ID of the application to which the event applies, including a process, browser, or service. Example: `89162` |
| **TargetAppName** | Optional | String | The name of the application to which event applies, including a service, a URL, or a SaaS application. Example: `Exchange 365` |
| **Application** | Alias |  | Alias to TargetAppName |
| **TargetAppType** | Conditional | AppType | The type of the application authorizing on behalf of the Actor. For more information, and allowed list of values, see [AppType](normalization-about-schemas#apptype) in the [Schema Overview article](normalization-about-schemas). |
| **TargetOriginalAppType** | Optional | String | The type of the application to which event applies as reported by the reporting device. |
| **TargetUrl** | Optional | URL | The URL associated with the target application. Example: `https://console.aws.amazon.com/console/home?fromtb=true&hashArgs=%23&isauthcode=true&nc2=h_ct&src=header-signin&state=hashArgsFromTB_us-east-1_7596bc16c83d260b` |

### Target system fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **Dst** | Alias | String | A unique identifier of the authentication target. This field may alias the TargetDvcId, TargetHostname, TargetIpAddr, TargetAppId, or TargetAppName fields. Example: `192.168.12.1` |
| **TargetHostname** | Recommended | Hostname | The target device hostname, excluding domain information.Example: `DESKTOP-1282V4D` |
| **TargetDomain** | Optional | Domain(String) | The domain of the target device.Example: `Contoso` |
| **TargetDomainType** | Conditional | Enumerated | The type of TargetDomain. For a list of allowed values and further information, refer to [DomainType](normalization-entity-device#domaintype) in the [Schema Overview article](normalization-about-schemas).Required if TargetDomain is used. |
| **TargetFQDN** | Optional | FQDN (String) | The target device hostname, including domain information when available. Example: `Contoso\DESKTOP-1282V4D`**Note**: This field supports both traditional FQDN format and Windows domain\hostname format. The TargetDomainType reflects the format used. |
| **TargetDescription** | Optional | String | A descriptive text associated with the device. For example: `Primary Domain Controller`. |
| **TargetDvcId** | Optional | String | The ID of the target device. If multiple IDs are available, use the most important one, and store the others in the fields `TargetDvc<DvcIdType>`. Example: `ac7e9755-8eae-4ffc-8a02-50ed7a2216c3` |
| **TargetDvcScopeId** | Optional | String | The cloud platform scope ID the device belongs to. **TargetDvcScopeId** map to a subscription ID on Azure and to an account ID on AWS. |
| **TargetDvcScope** | Optional | String | The cloud platform scope the device belongs to. **TargetDvcScope** map to a subscription ID on Azure and to an account ID on AWS. |
| **TargetDvcIdType** | Conditional | Enumerated | The type of TargetDvcId. For a list of allowed values and further information, refer to [DvcIdType](normalization-entity-device#dvcidtype) in the [Schema Overview article](normalization-about-schemas). Required if **TargetDeviceId** is used. |
| **TargetDeviceType** | Optional | Enumerated | The type of the target device. For a list of allowed values and further information, refer to [DeviceType](normalization-about-schemas#devicetype) in the [Schema Overview article](normalization-about-schemas). |
| **TargetIpAddr** | Recommended | IP Address | The IP address of the target device. Example: `2.2.2.2` |
| **TargetDvcOs** | Optional | String | The OS of the target device. Example: `Windows 10` |
| **TargetPortNumber** | Optional | Integer | The port of the target device. |
| **TargetGeoCountry** | Optional | Country | The country/region associated with the Target IP address.Example: `USA` |
| **TargetGeoRegion** | Optional | Region | The region within a country/region associated with the Target IP address.Example: `Vermont` |
| **TargetGeoCity** | Optional | City | The city associated with the Target IP address.Example: `Burlington` |
| **TargetGeoLatitude** | Optional | Latitude | The latitude of the geographical coordinate associated with the Target IP address.Example: `44.475833` |
| **TargetGeoLongitude** | Optional | Longitude | The longitude of the geographical coordinate associated with the Target IP address.Example: `73.211944` |
| **TargetRiskLevel** | Optional | Integer | The risk level associated with the target. The value should be adjusted to a range of `0` to `100`, with `0` for benign and `100` for a high risk.Example: `90` |
| **TargetOriginalRiskLevel** | Optional | String | The risk level associated with the target, as reported by the reporting device. Example: `Suspicious` |

### Acting Application fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **ActingAppId** | Optional | String | The ID of the application that initiated the activity reported, including a process, browser, or service. For example: `0x12ae8` |
| **ActingAppName** | Optional | String | The name of the application that initiated the activity reported, including a service, a URL, or a SaaS application. For example: `C:\Windows\System32\svchost.exe` |
| **ActingAppType** | Optional | AppType | The type of acting application. For more information, and allowed list of values, see [AppType](normalization-about-schemas#apptype) in the [Schema Overview article](normalization-about-schemas). |
| **ActingOriginalAppType** | Optional | String | The type of the application that initiated the activity as reported by the reporting device. |
| **HttpUserAgent** | Optional | String | When authentication is performed over HTTP or HTTPS, this field's value is the user\_agent HTTP header provided by the acting application when performing the authentication.For example: `Mozilla/5.0 (iPhone; CPU iPhone OS 12_1 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0 Mobile/15E148 Safari/604.1` |

### Source system fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **Src** | Alias | String | A unique identifier of the source device. This field might alias the SrcDvcId, SrcHostname, or SrcIpAddr fields. Example: `192.168.12.1` |
| **SrcIpAddr** | Recommended | IP address | The IP address from which the connection or session originated. Example: `77.138.103.108` |
| **IpAddr** | Alias |  | Alias to SrcIpAddr, or to TargetIpAddr if SrcIpAddr is not provided. |
| **SrcPortNumber** | Optional | Integer | The IP port from which the connection originated. Might not be relevant for a session comprising multiple connections.Example: `2335` |
| **SrcHostname** | Optional | Hostname | The source device hostname, excluding domain information. If no device name is available, store the relevant IP address in this field.Example: `DESKTOP-1282V4D` |
| **SrcDomain** | Optional | Domain (String) | The domain of the source device.Example: `Contoso` |
| **SrcDomainType** | Conditional | DomainType | The type of SrcDomain. For a list of allowed values and further information, refer to [DomainType](normalization-entity-device#domaintype) in the [Schema Overview article](normalization-about-schemas).Required if SrcDomain is used. |
| **SrcFQDN** | Optional | FQDN (String) | The source device hostname, including domain information when available. **Note**: This field supports both traditional FQDN format and Windows domain\hostname format. The SrcDomainType field reflects the format used. Example: `Contoso\DESKTOP-1282V4D` |
| **SrcDescription** | Optional | String | A descriptive text associated with the device. For example: `Primary Domain Controller`. |
| **SrcDvcId** | Optional | String | The ID of the source device. If multiple IDs are available, use the most important one, and store the others in the fields `SrcDvc<DvcIdType>`.Example: `ac7e9755-8eae-4ffc-8a02-50ed7a2216c3` |
| **SrcDvcScopeId** | Optional | String | The cloud platform scope ID the device belongs to. **SrcDvcScopeId** map to a subscription ID on Azure and to an account ID on AWS. |
| **SrcDvcScope** | Optional | String | The cloud platform scope the device belongs to. **SrcDvcScope** map to a subscription ID on Azure and to an account ID on AWS. |
| **SrcDvcIdType** | Conditional | DvcIdType | The type of SrcDvcId. For a list of allowed values and further information, refer to [DvcIdType](normalization-entity-device#dvcidtype) in the [Schema Overview article](normalization-about-schemas). **Note**: This field is required if SrcDvcId is used. |
| **SrcDeviceType** | Optional | DeviceType | The type of the source device. For a list of allowed values and further information, refer to [DeviceType](normalization-about-schemas#devicetype) in the [Schema Overview article](normalization-about-schemas). |
| **SrcGeoCountry** | Optional | Country | The country/region associated with the source IP address.Example: `USA` |
| **SrcGeoRegion** | Optional | Region | The region within a country/region associated with the source IP address.Example: `Vermont` |
| **SrcGeoCity** | Optional | City | The city associated with the source IP address.Example: `Burlington` |
| **SrcGeoLatitude** | Optional | Latitude | The latitude of the geographical coordinate associated with the source IP address.Example: `44.475833` |
| **SrcGeoLongitude** | Optional | Longitude | The longitude of the geographical coordinate associated with the source IP address.Example: `73.211944` |
| **SrcRiskLevel** | Optional | Integer | The risk level associated with the source. The value should be adjusted to a range of `0` to `100`, with `0` for benign and `100` for a high risk.Example: `90` |
| **SrcOriginalRiskLevel** | Optional | String | The risk level associated with the source, as reported by the reporting device. Example: `Suspicious` |

### Inspection fields

The following fields are used to represent that inspection performed by a security system.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **RuleName** | Optional | String | The name or ID of the rule by associated with the inspection results. |
| **RuleNumber** | Optional | Integer | The number of the rule associated with the inspection results. |
| **Rule** | Alias | String | Either the value of RuleName or the value of RuleNumber. If the value of RuleNumber is used, the type should be converted to string. |
| **ThreatId** | Optional | String | The ID of the threat or malware identified in the audit activity. |
| **ThreatName** | Optional | String | The name of the threat or malware identified in the audit activity. |
| **ThreatCategory** | Optional | String | The category of the threat or malware identified in audit file activity. |
| **ThreatRiskLevel** | Optional | RiskLevel (Integer) | The risk level associated with the identified threat. The level should be a number between **0** and **100**.**Note**: The value might be provided in the source record by using a different scale, which should be normalized to this scale. The original value should be stored in ThreatRiskLevelOriginal. |
| **ThreatOriginalRiskLevel** | Optional | String | The risk level as reported by the reporting device. |
| **ThreatConfidence** | Optional | ConfidenceLevel (Integer) | The confidence level of the threat identified, normalized to a value between 0 and a 100. |
| **ThreatOriginalConfidence** | Optional | String | The original confidence level of the threat identified, as reported by the reporting device. |
| **ThreatIsActive** | Optional | Boolean | True if the threat identified is considered an active threat. |
| **ThreatFirstReportedTime** | Optional | datetime | The first time the IP address or domain were identified as a threat. |
| **ThreatLastReportedTime** | Optional | datetime | The last time the IP address or domain were identified as a threat. |
| **ThreatIpAddr** | Optional | IP Address | An IP address for which a threat was identified. The field ThreatField contains the name of the field **ThreatIpAddr** represents. |
| **ThreatField** | Conditional | Enumerated | The field for which a threat was identified. The value is either `SrcIpAddr` or `TargetIpAddr`. |

### Entity correlation fields

Note

Contributors don't need to populate these fields. Applicable parsers will populate them when internal Microsoft support is added.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **ActingApplicationEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the acting application within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **ActorUserAdditionalIds** | Optional | Dynamic | For the field structure and usage, see [Fields suffixed with AdditionalIds](normalization-common-fields#fields-suffixed-with-additionalids). |
| **ActorUserEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the actor user within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **SrcSystemEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the source system within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **TargetApplicationEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the target application within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **TargetSystemEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the target system within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |

## Schema updates

| Version | Changes |
| --- | --- |
| 0.1.1 | Added the fields `ObjectId` and `OriginalObjectType`. |
| 0.1.2 | Added the fields `ActingOriginalAppType`, `OriginalObjectType`, `SrcOriginalRiskLevel`, `SrcRiskLevel`, `TargetGeoCity`, `TargetGeoCountry`, `TargetGeoLatitude`, `TargetGeoLongitude`, `TargetGeoRegion`, `TargetOriginalAppType`, `TargetOriginalRiskLevel`, and `TargetRiskLevel`. |
| 1.0.0 | Added entity correlation fields. |