---
layout: Conceptual
title: The Advanced Security Information Model (ASIM) Authentication normalization schema reference | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/normalization-schema-authentication
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
description: This article describes the Microsoft Sentinel Authentication normalization schema.
ms.author: edbaynash
author: EdB-MSFT
ms.topic: reference
ms.date: 2026-09-16T00:00:00.0000000Z
locale: en-us
document_id: 90e005e7-dc5e-f69b-1bb1-1017e639fd63
document_version_independent_id: c168465a-a5f1-c5ee-0c19-202ba72c1e31
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/normalization-schema-authentication.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/normalization-schema-authentication
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/normalization-schema-authentication.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 25ec49ab-02dc-13ce-c6ad-bb4474ad0d76
---

# The Advanced Security Information Model (ASIM) Authentication normalization schema reference | Microsoft Learn

The Microsoft Sentinel Authentication schema is used to describe events related to user authentication, sign-in, and sign-out. Authentication events are sent by many reporting devices, usually as part of the event stream alongside other events. For example, Windows sends several authentication events alongside other OS activity events.

Authentication events include both events from systems that focus on authentication such as VPN gateways or domain controllers, and direct authentication to an end system, such as a computer or firewall.

For more information about normalization in Microsoft Sentinel, see [Normalization and the Advanced Security Information Model (ASIM)](normalization).

## Parsers

Deploy ASIM authentication parsers from the [Microsoft Sentinel GitHub repository](https://aka.ms/DeployASIM). For more information about ASIM parsers, see the articles [ASIM parsers overview](normalization-parsers-overview).

### Unifying parsers

To use parsers that unify all ASIM out-of-the-box parsers, and ensure that your analysis runs across all the configured sources, use the `imAuthentication` filtering parser or the `ASimAuthentication` parameter-less parser.

### Source-specific parsers

For the list of authentication parsers Microsoft Sentinel provides refer to the [ASIM parsers list](normalization-parsers-list#authentication-parsers):

### Add your own normalized parsers

When implementing custom parsers for the Authentication information model, name your KQL functions using the following syntax:

- `vimAuthentication<vendor><Product>` for filtering parsers
- `ASimAuthentication<vendor><Product>` for parameter-less parsers

For information on adding your custom parsers to the unifying parser, refer to [Managing ASIM parsers](normalization-manage-parsers).

### Filtering parser parameters

The `im` and `vim*` parsers support [filtering parameters](normalization-about-parsers#optimizing-parsing-using-parameters). While these parsers are optional, they can improve your query performance.

The following filtering parameters are available:

| Name | Type | Description |
| --- | --- | --- |
| **starttime** | datetime | Filter only authentication events that ran at or after this time. This parameter filters on the `TimeGenerated` field, which is the standard designator for the time of the event, regardless of the parser-specific mapping of the EventStartTime and EventEndTime fields. |
| **endtime** | datetime | Filter only authentication events that finished running at or before this time. This parameter filters on the `TimeGenerated` field, which is the standard designator for the time of the event, regardless of the parser-specific mapping of the EventStartTime and EventEndTime fields. |
| **srcipaddr\_has\_any\_prefix** | dynamic | Filter only authentication events for which the source IP address prefix is in one of the listed values. Prefixes should end with a `.`, for example: `10.0.`. |
| **srchostname\_has\_any** | dynamic | Filter only authentication events for which the source hostname is any of the listed values. |
| **username\_has\_any** | dynamic | Filter only authentication events for which the user name is any of the listed values. |
| **targetappname\_has\_any** | dynamic | Filter only authentication events for which the target application name is any of the listed values. |
| **eventtype\_in** | dynamic | Filter only authentication events for which the event type is any of the listed values. |
| **eventresult** | string | Filter only authentication events with a specific **EventResult** value. |
| **eventresultdetails\_in** | dynamic | Filter only authentication events for which the event result details is any of the listed values. |

For example, to filter only authentication events from the last day to a specific user, use:

```kusto
imAuthentication (username_has_any = dynamic(['johndoe']), starttime = ago(1d), endtime=now())
```

Tip

To pass a literal list to parameters that expect a dynamic value, explicitly use a [dynamic literal](/en-us/kusto/query/scalar-data-types/dynamic?view=microsoft-sentinel&amp;preserve-view=true#dynamic-literals). For example: `dynamic(['192.168.','10.'])`.

## Normalized content

Normalized authentication analytic rules are unique as they detect attacks across sources. So, for example, if a user logged in to different, unrelated systems, from different countries/regions, Microsoft Sentinel will now detect this threat.

For a full list of analytics rules that use normalized Authentication events, see [Authentication schema security content](normalization-content#authentication-security-content).

## Schema overview

The Authentication information model is aligned with the [OSSEM logon entity schema](https://github.com/OTRF/OSSEM/blob/master/docs/cdm/entities/logon.md).

The fields listed in the table below are specific to Authentication events, but are similar to fields in other schemas and follow similar naming conventions.

Authentication events reference the following entities:

- **TargetUser** - The user information used to authenticate to the system. The **TargetSystem** is the primary subject of the authentication event, and the alias User aliases a **TargetUser** identified.
- **TargetApp** - The application authenticated to.
- **Target** - The system on which **TargetApp** is running.
- **Actor** - The user initiating the authentication, if different than **TargetUser**.
- **ActingApp** - The application used by the **Actor** to perform the authentication.
- **Src** - The system used by the **Actor** to initiate the authentication.

The relationship between these entities is best demonstrated as follows:

An **Actor**, running an acting Application, **ActingApp**, on a source system, **Src**, attempts to authenticate as a **TargetUser** to a target application, **TargetApp**, on a target system, **TargetDvc**.

## Schema details

In the following tables, *Type* refers to a logical type. For more information, see [Logical types](normalization-about-schemas#logical-types).

### Common ASIM fields

Important

Fields common to all schemas are described in detail in the [ASIM Common Fields](normalization-common-fields) article.

#### Common fields with specific guidelines

The following list mentions fields that have specific guidelines for authentication events:

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **EventType** | Mandatory | Enumerated | Describes the operation reported by the record. For Authentication records, supported values include: - `Logon`- `Logoff`- `Elevate` |
| **EventResultDetails** | Recommended | Enumerated | The details associated with the event result. This field is typically populated when the result is a failure.Allowed values include:  - `No such user or password`. This value should be used also when the original event reports that there is no such user, without reference to a password. - `No such user` - `Incorrect password` - `Incorrect key`- `Account expired`- `Password expired`- `User locked`- `User disabled` - `Logon violates policy`. This value should be used when the original event reports, for example: MFA required, log on outside of working hours, conditional access restrictions, or too frequent attempts.- `Session expired`- `Other`The value may be provided in the source record using different terms, which should be normalized to these values. The original value should be stored in the field [EventOriginalResultDetails](normalization-common-fields#eventoriginalresultdetails) |
| **EventSubType** | Optional | Enumerated | The sign-in type. Allowed values include: - `System` - `Interactive` - `RemoteInteractive` - `Service` - `RemoteService` - `Remote` - Use when the type of remote sign-in is unknown. - `AssumeRole` - Typically used when the event type is `Elevate`. The value may be provided in the source record using different terms, which should be normalized to these values. The original value should be stored in the field [EventOriginalSubType](normalization-common-fields#eventoriginalsubtype). |
| **EventSchemaVersion** | Mandatory | SchemaVersion (String) | The version of the schema. The version of the schema documented here is `1.0.0` |
| **EventSchema** | Mandatory | Enumerated | The name of the schema documented here is **Authentication**. |
| **Dvc** fields | - | - | For authentication events, device fields refer to the system reporting the event. |

#### All common fields

Fields that appear in the table below are common to all ASIM schemas. Any guideline specified above overrides the general guidelines for the field. For example, a field might be optional in general, but mandatory for a specific schema. For further details on each field, refer to the [ASIM Common Fields](normalization-common-fields) article.

| **Class** | **Fields** |
| --- | --- |
| Mandatory | - [EventCount](normalization-common-fields#eventcount) - [EventStartTime](normalization-common-fields#eventstarttime) - [EventEndTime](normalization-common-fields#eventendtime) - [EventType](normalization-common-fields#eventtype)- [EventResult](normalization-common-fields#eventresult) - [EventProduct](normalization-common-fields#eventproduct) - [EventVendor](normalization-common-fields#eventvendor) - [EventSchema](normalization-common-fields#eventschema) - [EventSchemaVersion](normalization-common-fields#eventschemaversion) - [Dvc](normalization-common-fields#dvc) |
| Recommended | - [EventResultDetails](normalization-common-fields#eventresultdetails)- [EventSeverity](normalization-common-fields#eventseverity)- [EventUid](normalization-common-fields#eventuid) - [DvcIpAddr](normalization-common-fields#dvcipaddr) - [DvcHostname](normalization-common-fields#dvchostname) - [DvcDomain](normalization-common-fields#dvcdomain)- [DvcDomainType](normalization-common-fields#dvcdomaintype)- [DvcFQDN](normalization-common-fields#dvcfqdn)- [DvcId](normalization-common-fields#dvcid)- [DvcIdType](normalization-common-fields#dvcidtype)- [DvcAction](normalization-common-fields#dvcaction) |
| Optional | - [EventMessage](normalization-common-fields#eventmessage) - [EventSubType](normalization-common-fields#eventsubtype)- [EventOriginalUid](normalization-common-fields#eventoriginaluid)- [EventOriginalType](normalization-common-fields#eventoriginaltype)- [EventOriginalSubType](normalization-common-fields#eventoriginalsubtype)- [EventOriginalResultDetails](normalization-common-fields#eventoriginalresultdetails) - [EventOriginalSeverity](normalization-common-fields#eventoriginalseverity) - [EventProductVersion](normalization-common-fields#eventproductversion) - [EventReportUrl](normalization-common-fields#eventreporturl) - [EventOwner](normalization-common-fields#eventowner)- [DvcZone](normalization-common-fields#dvczone)- [DvcMacAddr](normalization-common-fields#dvcmacaddr)- [DvcOs](normalization-common-fields#dvcos)- [DvcOsVersion](normalization-common-fields#dvchostname)- [DvcOriginalAction](normalization-common-fields#dvcoriginalaction)- [DvcInterface](normalization-common-fields#dvcinterface)- [AdditionalFields](normalization-common-fields#additionalfields)- [DvcDescription](normalization-common-fields#dvcdescription)- [DvcScopeId](normalization-common-fields#dvcscopeid)- [DvcScope](normalization-common-fields#dvcscope) |

### Authentication-specific fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **LogonMethod** | Optional | String | The method used to perform authentication. Allowed values include: `Managed Identity`, `Service Principal`, `Username & Password`, `Multi factor authentication`, `Passwordless`, `PKI`, `PAM`, and `Other`. Examples: `Managed Identity` |
| **LogonProtocol** | Optional | String | The protocol used to perform authentication. Example: `NTLM` |

### Actor fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **ActorUserId** | Optional | String | A machine-readable, alphanumeric, unique representation of the Actor. For more information, and for alternative fields for additional IDs, see [The User entity](normalization-entity-user). Example: `S-1-12-1-4141952679-1282074057-627758481-2916039507` |
| **ActorScope** | Optional | String | The scope, such as Microsoft Entra tenant, in which ActorUserId and ActorUsername are defined. or more information and list of allowed values, see [UserScope](normalization-entity-user#userscope) in the [Schema Overview article](normalization-about-schemas). |
| **ActorScopeId** | Optional | String | The scope ID, such as Microsoft Entra Directory ID, in which ActorUserId and ActorUsername are defined. for more information and list of allowed values, see [UserScopeId](normalization-entity-user#userscopeid) in the [Schema Overview article](normalization-about-schemas). |
| **ActorUserIdType** | Conditional | UserIdType | The type of the ID stored in the ActorUserId field. For more information and list of allowed values, see [UserIdType](normalization-entity-user#useridtype) in the [Schema Overview article](normalization-about-schemas). |
| **ActorUsername** | Optional | Username (String) | The Actor’s username, including domain information when available. For more information, see [The User entity](normalization-entity-user).Example: `AlbertE` |
| **ActorUsernameType** | Conditional | UsernameType | Specifies the type of the user name stored in the ActorUsername field. For more information, and list of allowed values, see [UsernameType](normalization-entity-user#usernametype) in the [Schema Overview article](normalization-about-schemas). Example: `Windows` |
| **ActorUserType** | Optional | UserType | The type of the Actor. For more information, and list of allowed values, see [UserType](normalization-entity-user#usertype) in the [Schema Overview article](normalization-about-schemas).For example: `Guest` |
| **ActorOriginalUserType** | Optional | String | The user type as reported by the reporting device. |
| **ActorSessionId** | Optional | String | The unique ID of the sign-in session of the Actor. Example: `102pTUgC3p8RIqHvzxLCHnFlg` |

### Acting Application fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **ActingAppId** | Optional | String | The ID of the application authorizing on behalf of the actor, including a process, browser, or service. For example: `0x12ae8` |
| **ActingAppName** | Optional | String | The name of the application authorizing on behalf of the actor, including a process, browser, or service. For example: `C:\Windows\System32\svchost.exe` |
| **ActingAppType** | Optional | AppType | The type of acting application. For more information, and allowed list of values, see [AppType](normalization-about-schemas#apptype) in the [Schema Overview article](normalization-about-schemas). |
| **ActingOriginalAppType** | Optional | String | The type of the acting application as reported by the reporting device. |
| **HttpUserAgent** | Optional | String | When authentication is performed over HTTP or HTTPS, this field's value is the user\_agent HTTP header provided by the acting application when performing the authentication.For example: `Mozilla/5.0 (iPhone; CPU iPhone OS 12_1 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0 Mobile/15E148 Safari/604.1` |

### Target user fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **TargetUserId** | Optional | String | A machine-readable, alphanumeric, unique representation of the target user. For more information, and for alternative fields for additional IDs, see [The User entity](normalization-entity-user).  Example: `00urjk4znu3BcncfY0h7` |
| **TargetUserScope** | Optional | String | The scope, such as Microsoft Entra tenant, in which TargetUserId and TargetUsername are defined. or more information and list of allowed values, see [UserScope](normalization-entity-user#userscope) in the [Schema Overview article](normalization-about-schemas). |
| **TargetUserScopeId** | Optional | String | The scope ID, such as Microsoft Entra Directory ID, in which TargetUserId and TargetUsername are defined. for more information and list of allowed values, see [UserScopeId](normalization-entity-user#userscopeid) in the [Schema Overview article](normalization-about-schemas). |
| **TargetUserIdType** | Conditional | UserIdType | The type of the user ID stored in the TargetUserId field. For more information and list of allowed values, see [UserIdType](normalization-entity-user#useridtype) in the [Schema Overview article](normalization-about-schemas).  Example: `SID` |
| **TargetUsername** | Optional | Username (String) | The target user username, including domain information when available. For more information, see [The User entity](normalization-entity-user). Example: `MarieC` |
| **TargetUsernameType** | Conditional | UsernameType | Specifies the type of the username stored in the TargetUsername field. For more information and list of allowed values, see [UsernameType](normalization-entity-user#usernametype) in the [Schema Overview article](normalization-about-schemas). |
| **TargetUserType** | Optional | UserType | The type of the Target user. For more information, and list of allowed values, see [UserType](normalization-entity-user#usertype) in the [Schema Overview article](normalization-about-schemas). For example: `Member` |
| **TargetSessionId** | Optional | String | The sign-in session identifier of the TargetUser on the source device. |
| **TargetOriginalUserType** | Optional | String | The user type as reported by the reporting device. |
| **User** | Alias | Username (String) | Alias to the TargetUsername or to the TargetUserId if TargetUsername is not defined. Example: `CONTOSO\dadmin` |

### Source system fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **Src** | Recommended | String | A unique identifier of the source device. This field may alias the SrcDvcId, SrcHostname, or SrcIpAddr fields. Example: `192.168.12.1` |
| **SrcDvcId** | Optional | String | The ID of the source device. If multiple IDs are available, use the most important one, and store the others in the fields `SrcDvc<DvcIdType>`.Example: `ac7e9755-8eae-4ffc-8a02-50ed7a2216c3` |
| **SrcDvcScopeId** | Optional | String | The cloud platform scope ID the device belongs to. **SrcDvcScopeId** map to a subscription ID on Azure and to an account ID on AWS. |
| **SrcDvcScope** | Optional | String | The cloud platform scope the device belongs to. **SrcDvcScope** map to a subscription ID on Azure and to an account ID on AWS. |
| **SrcDvcIdType** | Conditional | DvcIdType | The type of SrcDvcId. For a list of allowed values and further information refer to [DvcIdType](normalization-entity-device#dvcidtype) in the [Schema Overview article](normalization-about-schemas). **Note**: This field is required if SrcDvcId is used. |
| **SrcDeviceType** | Optional | DeviceType | The type of the source device. For a list of allowed values and further information refer to [DeviceType](normalization-about-schemas#devicetype) in the [Schema Overview article](normalization-about-schemas). |
| **SrcHostname** | Optional | Hostname | The source device hostname, excluding domain information. If no device name is available, store the relevant IP address in this field. Example: `DESKTOP-1282V4D` |
| **SrcDomain** | Optional | Domain (String) | The domain of the source device.Example: `Contoso` |
| **SrcDomainType** | Conditional | DomainType | The type of SrcDomain. For a list of allowed values and further information refer to [DomainType](normalization-entity-device#domaintype) in the [Schema Overview article](normalization-about-schemas).Required if SrcDomain is used. |
| **SrcFQDN** | Optional | FQDN (String) | The source device hostname, including domain information when available. **Note**: This field supports both traditional FQDN format and Windows domain\hostname format. The SrcDomainType field reflects the format used. Example: `Contoso\DESKTOP-1282V4D` |
| **SrcDescription** | Optional | String | A descriptive text associated with the device. For example: `Primary Domain Controller`. |
| **SrcIpAddr** | Recommended | IP Address | The IP address of the source device. Example: `2.2.2.2` |
| **SrcPortNumber** | Optional | Integer | The IP port from which the connection originated.Example: `2335` |
| **SrcDvcOs** | Optional | String | The OS of the source device. Example: `Windows 10` |
| **IpAddr** | Alias |  | Alias to SrcIpAddr |
| **SrcIsp** | Optional | String | The Internet Service Provider (ISP) used by the source device to connect to the internet. Example: `corpconnect` |
| **SrcGeoCountry** | Optional | Country | Example: `Canada`For more information, see [Logical types](normalization-about-schemas#logical-types). |
| **SrcGeoCity** | Optional | City | Example: `Montreal`For more information, see [Logical types](normalization-about-schemas#logical-types). |
| **SrcGeoRegion** | Optional | Region | Example: `Quebec`For more information, see [Logical types](normalization-about-schemas#logical-types). |
| **SrcGeoLongitude** | Optional | Longitude | Example: `-73.614830`For more information, see [Logical types](normalization-about-schemas#logical-types). |
| **SrcGeoLatitude** | Optional | Latitude | Example: `45.505918`For more information, see [Logical types](normalization-about-schemas#logical-types). |
| **SrcRiskLevel** | Optional | Integer | The risk level associated with the source. The value should be adjusted to a range of `0` to `100`, with `0` for benign and `100` for a high risk.Example: `90` |
| **SrcOriginalRiskLevel** | Optional | String | The risk level associated with the source, as reported by the reporting device. Example: `Suspicious` |

### Target application fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **TargetAppId** | Optional | String | The ID of the application to which the authorization is required, often assigned by the reporting device. Example: `89162` |
| **TargetAppName** | Optional | String | The name of the application to which the authorization is required, including a service, a URL, or a SaaS application. Example: `Saleforce` |
| **Application** | Alias |  | Alias to TargetAppName. |
| **TargetAppType** | Conditional | AppType | The type of the application authorizing on behalf of the Actor. For more information, and allowed list of values, see [AppType](normalization-about-schemas#apptype) in the [Schema Overview article](normalization-about-schemas). |
| **TargetOriginalAppType** | Optional | String | The type of the application authorizing on behalf of the Actor as reported by the reporting device. |
| **TargetUrl** | Optional | URL | The URL associated with the target application. Example: `https://console.aws.amazon.com/console/home?fromtb=true&hashArgs=%23&isauthcode=true&nc2=h_ct&src=header-signin&state=hashArgsFromTB_us-east-1_7596bc16c83d260b` |
| **LogonTarget** | Alias |  | Alias to either TargetAppName, TargetUrl, or TargetHostname, whichever field best describes the authentication target. |

### Target system fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **Dst** | Alias | String | A unique identifier of the authentication target. This field may alias the TargetDvcId, TargetHostname, TargetIpAddr, TargetAppId, or TargetAppName fields. Example: `192.168.12.1` |
| **TargetHostname** | Recommended | Hostname | The target device hostname, excluding domain information.Example: `DESKTOP-1282V4D` |
| **TargetDomain** | Recommended | Domain (String) | The domain of the target device.Example: `Contoso` |
| **TargetDomainType** | Conditional | Enumerated | The type of TargetDomain. For a list of allowed values and further information refer to [DomainType](normalization-entity-device#domaintype) in the [Schema Overview article](normalization-about-schemas).Required if TargetDomain is used. |
| **TargetFQDN** | Optional | FQDN (String) | The target device hostname, including domain information when available. Example: `Contoso\DESKTOP-1282V4D`**Note**: This field supports both traditional FQDN format and Windows domain\hostname format. The TargetDomainType reflects the format used. |
| **TargetDescription** | Optional | String | A descriptive text associated with the device. For example: `Primary Domain Controller`. |
| **TargetDvcId** | Optional | String | The ID of the target device. If multiple IDs are available, use the most important one, and store the others in the fields `TargetDvc<DvcIdType>`. Example: `ac7e9755-8eae-4ffc-8a02-50ed7a2216c3` |
| **TargetDvcScopeId** | Optional | String | The cloud platform scope ID the device belongs to. **TargetDvcScopeId** map to a subscription ID on Azure and to an account ID on AWS. |
| **TargetDvcScope** | Optional | String | The cloud platform scope the device belongs to. **TargetDvcScope** map to a subscription ID on Azure and to an account ID on AWS. |
| **TargetDvcIdType** | Conditional | Enumerated | The type of TargetDvcId. For a list of allowed values and further information refer to [DvcIdType](normalization-entity-device#dvcidtype) in the [Schema Overview article](normalization-about-schemas). Required if **TargetDeviceId** is used. |
| **TargetDeviceType** | Optional | Enumerated | The type of the target device. For a list of allowed values and further information refer to [DeviceType](normalization-about-schemas#devicetype) in the [Schema Overview article](normalization-about-schemas). |
| **TargetIpAddr** | Optional | IP Address | The IP address of the target device. Example: `2.2.2.2` |
| **TargetDvcOs** | Optional | String | The OS of the target device. Example: `Windows 10` |
| **TargetPortNumber** | Optional | Integer | The port of the target device. |
| **TargetGeoCountry** | Optional | Country | The country/region associated with the target IP address.Example: `USA` |
| **TargetGeoRegion** | Optional | Region | The region associated with the target IP address.Example: `Vermont` |
| **TargetGeoCity** | Optional | City | The city associated with the target IP address.Example: `Burlington` |
| **TargetGeoLatitude** | Optional | Latitude | The latitude of the geographical coordinate associated with the target IP address.Example: `44.475833` |
| **TargetGeoLongitude** | Optional | Longitude | The longitude of the geographical coordinate associated with the target IP address.Example: `73.211944` |
| **TargetRiskLevel** | Optional | Integer | The risk level associated with the target. The value should be adjusted to a range of `0` to `100`, with `0` for benign and `100` for a high risk.Example: `90` |
| **TargetOriginalRiskLevel** | Optional | String | The risk level associated with the target, as reported by the reporting device. Example: `Suspicious` |

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
| **TargetUserAdditionalIds** | Optional | Dynamic | For the field structure and usage, see [Fields suffixed with AdditionalIds](normalization-common-fields#fields-suffixed-with-additionalids). |
| **TargetUserEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the target user within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |

## Schema updates

| Version | Changes |
| --- | --- |
| 0.1.1 | - Updated user and device entity fields to align with other schemas.- Renamed `TargetDvc` and `SrcDvc` to `Target` and `Src`, respectively, to align with current ASIM guidelines. The renamed fields are implemented as aliases. These fields include `SrcDvcHostname`, `SrcDvcHostnameType`, `SrcDvcType`, `SrcDvcIpAddr`, `TargetDvcHostname`, `TargetDvcHostnameType`, `TargetDvcType`, `TargetDvcIpAddr`, and `TargetDvc`.- Added the aliases `Src` and `Dst`.- Added the fields `SrcDvcIdType`, `SrcDeviceType`, `TargetDvcIdType`, `TargetDeviceType`, and `EventSchema`. |
| 0.1.2 | Added the fields `ActorScope`, `TargetUserScope`, `SrcDvcScopeId`, `SrcDvcScope`, `TargetDvcScopeId`, `TargetDvcScope`, `DvcScopeId`, and `DvcScope`. |
| 0.1.3 | - Added the fields `SrcPortNumber`, `ActorOriginalUserType`, `ActorScopeId`, `TargetOriginalUserType`, `TargetUserScopeId`, `SrcDescription`, `SrcRiskLevel`, `SrcOriginalRiskLevel`, and `TargetDescription`.- Added inspection fields.- Added target system geolocation fields. |
| 0.1.4 | - Added the fields `ActingOriginalAppType` and `TargetOriginalAppType`.- Added the alias `Application`. |
| 1.0.0 | Added entity correlation fields. |