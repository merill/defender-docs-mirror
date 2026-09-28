---
layout: Conceptual
title: Microsoft Sentinel user management normalization schema reference | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/normalization-schema-user-management
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
description: This article describes the Microsoft Sentinel user management normalization schema.
ms.author: edbaynash
author: EdB-MSFT
ms.topic: reference
ms.date: 2026-09-16T00:00:00.0000000Z
locale: en-us
document_id: f69a95c9-7f47-605b-2a4b-2d0d1b7ea6a5
document_version_independent_id: 85118669-7e04-bdcd-55b0-f4495f877116
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/normalization-schema-user-management.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/normalization-schema-user-management
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/normalization-schema-user-management.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
platformId: 1ce01ba0-ca34-0ea6-1bc3-09ca3b558858
---

# Microsoft Sentinel user management normalization schema reference | Microsoft Learn

The Microsoft Sentinel user management normalization schema is used to describe user management activities, such as creating a user or a group, changing user attribute, or adding a user to a group. Such events are reported, for example, by operating systems, directory services, identity management systems, and any other system reporting on its local user management activity.

For more information about normalization in Microsoft Sentinel, see [Normalization and the Advanced Security Information Model (ASIM)](normalization).

## Schema overview

The ASIM user management schema describes user management activities. The activities typically include the following entities:

- **Actor** - the user performing the management activity.
- **Acting Process** - the process used by the actor to perform the management activity.
- **Src** - when the activity is performed over the network, the source device from which the activity was initiated.
- **Target User** - the user who's account is managed.
- **Group** the target user is added or removed from, or being modified.

Some activities, such as **UserCreated**, **GroupCreated**, **UserModified**, and **GroupModified**, set or update user properties. The property set or updated is documented in the following fields:

- EventSubType - the name of the value that was set or updated. UpdatedPropertyName is an alias to **EventSubType** when EventSubType refers to one of the relevant event types.
- PreviousPropertyValue - the previous value of the property.
- NewPropertyValue - the updated value of the property.

## Parsers

For more information about ASIM parsers, see the [ASIM parsers overview](normalization-parsers-overview).

### Filtering parser parameters

The User Management parsers support [filtering parameters](normalization-about-parsers#optimizing-parsing-using-parameters). While these parameters are optional, they can improve your query performance.

The following filtering parameters are available:

| Name | Type | Description |
| --- | --- | --- |
| **starttime** | datetime | Filter only user management events that occurred at or after this time. This parameter filters on the `TimeGenerated` field, which is the standard designator for the time of the event, regardless of the parser-specific mapping of the EventStartTime and EventEndTime fields. |
| **endtime** | datetime | Filter only user management events that occurred at or before this time. This parameter filters on the `TimeGenerated` field, which is the standard designator for the time of the event, regardless of the parser-specific mapping of the EventStartTime and EventEndTime fields. |
| **srcipaddr\_has\_any\_prefix** | dynamic | Filter only user management events where the source IP address prefix matches any of the listed values. Prefixes should end with a `.`, for example: `10.0.`. |
| **targetusername\_has\_any** | dynamic | Filter only user management events where the target username has any of the listed values. |
| **actorusername\_has\_any** | dynamic | Filter only user management events where the actor username has any of the listed values. |
| **eventtype\_in** | dynamic | Filter only user management events where the event type is one of the listed values, such as `UserCreated`, `UserDeleted`, `UserModified`, `PasswordChanged`, or `GroupCreated`. |

For example, to filter only user creation events from the last day, use:

```kusto
_Im_UserManagement (eventtype_in=dynamic(['UserCreated']), starttime = ago(1d), endtime=now())
```

## Schema details

### Common ASIM fields

Important

Fields common to all schemas are described in detail in the [ASIM Common Fields](normalization-common-fields) article.

#### Common fields with specific guidelines

The following list mentions fields that have specific guidelines for process activity events:

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **EventType** | Mandatory | Enumerated | Describes the operation reported by the record. For User Management activity, the supported values are: - `UserCreated` - `UserDeleted` - `UserModified` - `UserLocked` - `UserUnlocked` - `UserDisabled` - `UserEnabled` - `PasswordChanged` - `PasswordReset` - `GroupCreated` - `GroupDeleted` - `GroupModified` - `UserAddedToGroup` - `UserRemovedFromGroup` - `GroupEnumerated` - `UserRead` - `GroupRead` |
| **EventSubType** | Optional | Enumerated | The following sub-types are supported: - `UserRead`: Password, Hash - `UserCreated`, `GroupCreated`, `UserModified`, `GroupModified`. For more information, see UpdatedPropertyName |
| **EventResult** | Mandatory | Enumerated | While failure is possible, most systems report only successful user management events. The expected value for successful events is `Success`. |
| **EventResultDetails** | Recommended | Enumerated | The valid values are `NotAuthorized` and `Other`. |
| **EventSeverity** | Mandatory | Enumerated | While any valid severity value is allowed, the severity of user management events is typically `Informational`. |
| **EventSchema** | Mandatory | Enumerated | The name of the schema documented here is `UserManagement`. |
| **EventSchemaVersion** | Mandatory | SchemaVersion (String) | The version of the schema. The version of the schema documented here is `1.0.0`. |
| **Dvc** fields |  |  | For user management events, device fields refer to the system reporting the event. This is usually the system on which the user is managed. |

#### All common fields

Fields that appear in the table below are common to all ASIM schemas. Any guideline specified above overrides the general guidelines for the field. For example, a field might be optional in general, but mandatory for a specific schema. For further details on each field, refer to the [ASIM Common Fields](normalization-common-fields) article.

| **Class** | **Fields** |
| --- | --- |
| Mandatory | - [EventCount](normalization-common-fields#eventcount) - [EventStartTime](normalization-common-fields#eventstarttime) - [EventEndTime](normalization-common-fields#eventendtime) - [EventType](normalization-common-fields#eventtype)- [EventResult](normalization-common-fields#eventresult) - [EventProduct](normalization-common-fields#eventproduct) - [EventVendor](normalization-common-fields#eventvendor) - [EventSchema](normalization-common-fields#eventschema) - [EventSchemaVersion](normalization-common-fields#eventschemaversion) - [Dvc](normalization-common-fields#dvc) |
| Recommended | - [EventResultDetails](normalization-common-fields#eventresultdetails)- [EventSeverity](normalization-common-fields#eventseverity)- [EventUid](normalization-common-fields#eventuid) - [DvcIpAddr](normalization-common-fields#dvcipaddr) - [DvcHostname](normalization-common-fields#dvchostname) - [DvcDomain](normalization-common-fields#dvcdomain)- [DvcDomainType](normalization-common-fields#dvcdomaintype)- [DvcFQDN](normalization-common-fields#dvcfqdn)- [DvcId](normalization-common-fields#dvcid)- [DvcIdType](normalization-common-fields#dvcidtype)- [DvcAction](normalization-common-fields#dvcaction) |
| Optional | - [EventMessage](normalization-common-fields#eventmessage) - [EventSubType](normalization-common-fields#eventsubtype)- [EventOriginalUid](normalization-common-fields#eventoriginaluid)- [EventOriginalType](normalization-common-fields#eventoriginaltype)- [EventOriginalSubType](normalization-common-fields#eventoriginalsubtype)- [EventOriginalResultDetails](normalization-common-fields#eventoriginalresultdetails) - [EventOriginalSeverity](normalization-common-fields#eventoriginalseverity) - [EventProductVersion](normalization-common-fields#eventproductversion) - [EventReportUrl](normalization-common-fields#eventreporturl) - [EventOwner](normalization-common-fields#eventowner)- [DvcZone](normalization-common-fields#dvczone)- [DvcMacAddr](normalization-common-fields#dvcmacaddr)- [DvcOs](normalization-common-fields#dvcos)- [DvcOsVersion](normalization-common-fields#dvchostname)- [DvcOriginalAction](normalization-common-fields#dvcoriginalaction)- [DvcInterface](normalization-common-fields#dvcinterface)- [AdditionalFields](normalization-common-fields#additionalfields)- [DvcDescription](normalization-common-fields#dvcdescription)- [DvcScopeId](normalization-common-fields#dvcscopeid)- [DvcScope](normalization-common-fields#dvcscope) |

### Updated property fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **UpdatedPropertyName** | Alias |  | Alias to EventSubType when the Event Type is `UserCreated`, `GroupCreated`, `UserModified`, or `GroupModified`.Supported values are:- `MultipleProperties`: Used when the activity updates multiple properties- `Previous<PropertyName>`, where `<PropertyName>` is one of the supported values for `UpdatedPropertyName`. - `New<PropertyName>`, where `<PropertyName>` is one of the supported values for `UpdatedPropertyName`. |
| **PreviousPropertyValue** | Optional | String | The previous value that was stored in the specified property. |
| **NewPropertyValue** | Optional | String | The new value stored in the specified property. |

### Target user fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **TargetUserId** | Optional | String | A machine-readable, alphanumeric, unique representation of the target user. Supported formats and types include:- **SID** (Windows): `S-1-5-21-1377283216-344919071-3415362939-500`- **UID** (Linux): `4578`- **AADID** (Microsoft Entra ID): `9267d02c-5f76-40a9-a9eb-b686f3ca47aa`- **OktaId**: `00urjk4znu3BcncfY0h7`- **AWSId**: `72643944673`Store the ID type in the TargetUserIdType field. If other IDs are available, we recommend that you normalize the field names to **TargetUserSid**, **TargetUserUid**, **TargetUserAADID**, **TargetUserOktaId**, and **TargetUserAwsId**, respectively. For more information, see [The User entity](normalization-entity-user).Example: `S-1-12` |
| **TargetUserIdType** | Conditional | Enumerated | The type of the ID stored in the TargetUserId field. Supported values are `SID`, `UID`, `AADID`, `OktaId`, and `AWSId`. |
| **TargetUsername** | Optional | Username (String) | The target username, including domain information when available. Use one of the following formats and in the following order of priority:- **Upn/Email**: `johndow@contoso.com`- **Windows**: `Contoso\johndow`- **DN**: `CN=Jeff Smith,OU=Sales,DC=Fabrikam,DC=COM`- **Simple**: `johndow`. Use the Simple form only if domain information isn't available.Store the Username type in the TargetUsernameType field. If other IDs are available, we recommend that you normalize the field names to **TargetUserUpn**, **TargetUserWindows**, and **TargetUserDn**. For more information, see [The User entity](normalization-entity-user).Example: `AlbertE` |
| **TargetUsernameType** | Conditional | Enumerated | Specifies the type of the username stored in the TargetUsername field. Supported values include `UPN`, `Windows`, `DN`, and `Simple`. For more information, see [The User entity](normalization-entity-user).Example: `Windows` |
| **TargetUserType** | Optional | Enumerated | The type of target user. Supported values include:- `Regular`- `Machine`- `Admin`- `System`- `Application`- `Service Principal`- `Other`**Note**: The value might be provided in the source record by using different terms, which should be normalized to these values. Store the original value in the TargetOriginalUserType field. |
| **TargetOriginalUserType** | Optional | String | The original destination user type, if provided by the source. |
| **TargetUserScope** | Optional | String | The scope, such as Microsoft Entra tenant, in which TargetUserId and TargetUsername are defined. or more information and list of allowed values, see [UserScope](normalization-entity-user#userscope) in the [Schema Overview article](normalization-about-schemas). |
| **TargetUserScopeId** | Optional | String | The scope ID, such as Microsoft Entra Directory ID, in which TargetUserId and TargetUsername are defined. for more information and list of allowed values, see [UserScopeId](normalization-entity-user#userscopeid) in the [Schema Overview article](normalization-about-schemas). |
| **TargetUserSessionId** | Optional | String | The unique ID of the target user's login session. Example: `999`**Note**: The type is defined as *string* to support varying systems, but on Windows this value must be numeric. If you are using a Windows or Linux machine and used a different type, make sure to convert the values. For example, if you used a hexadecimal value, convert it to a decimal value. |

### Actor fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **ActorUserId** | Optional | String | A machine-readable, alphanumeric, unique representation of the Actor. Supported formats and types include:- **SID** (Windows): `S-1-5-21-1377283216-344919071-3415362939-500`- **UID** (Linux): `4578`- **AADID** (Microsoft Entra ID): `9267d02c-5f76-40a9-a9eb-b686f3ca47aa`- **OktaId**: `00urjk4znu3BcncfY0h7`- **AWSId**: `72643944673`Store the ID type in the ActorUserIdType field. If other IDs are available, we recommend that you normalize the field names to **ActorUserSid**, **ActorUserUid**, **ActorUserAadId**, **ActorUserOktaId**, and **ActorAwsId**, respectively. For more information, see [The User entity](normalization-entity-user).Example: S-1-12 |
| **ActorUserIdType** | Conditional | Enumerated | The type of the ID stored in the ActorUserId field. Supported values include `SID`, `UID`, `AADID`, `OktaId`, and `AWSId`. |
| **ActorUsername** | Mandatory | Username (String) | The Actor username, including domain information when available. Use one of the following formats and in the following order of priority:- **Upn/Email**: `johndow@contoso.com`- **Windows**: `Contoso\johndow`- **DN**: `CN=Jeff Smith,OU=Sales,DC=Fabrikam,DC=COM`- **Simple**: `johndow`. Use the Simple form only if domain information isn't available.Store the Username type in the ActorUsernameType field. If other IDs are available, we recommend that you normalize the field names to **ActorUserUpn**, **ActorUserWindows**, and **ActorUserDn**.For more information, see [The User entity](normalization-entity-user).Example: `AlbertE` |
| **User** | Alias |  | Alias to ActorUsername. |
| **ActorUsernameType** | Conditional | Enumerated | Specifies the type of the username stored in the ActorUsername field. Supported values are `UPN`, `Windows`, `DN`, and `Simple`. For more information, see [The User entity](normalization-entity-user).Example: `Windows` |
| **ActorUserType** | Optional | Enumerated | The type of the Actor. Allowed values are:- `Regular`- `Machine`- `Admin`- `System`- `Application`- `Service Principal`- `Other`**Note**: The value might be provided in the source record by using different terms, which should be normalized to these values. Store the original value in the ActorOriginalUserType field. |
| **ActorOriginalUserType** | Optional | String | The original actor user type, if provided by the source. |
| **ActorSessionId** | Optional | String | The unique ID of the login session of the Actor. Example: `999`**Note**: The type is defined as *string* to support varying systems, but on Windows this value must be numeric. If you are using a Windows machine and used a different type, make sure to convert the values. For example, if you used a hexadecimal value, convert it to a decimal value. |
| **ActorScope** | Optional | String | The scope, such as Microsoft Entra tenant, in which ActorUserId and ActorUsername are defined. or more information and list of allowed values, see [UserScope](normalization-entity-user#userscope) in the [Schema Overview article](normalization-about-schemas). |
| **ActorScopeId** | Optional | String | The scope ID, such as Microsoft Entra Directory ID, in which ActorUserId and ActorUsername are defined. or more information and list of allowed values, see [UserScopeId](normalization-entity-user#userscopeid) in the [Schema Overview article](normalization-about-schemas). |

### Group fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **GroupId** | Optional | String | A machine-readable, alphanumeric, unique representation of the group, for activities involving a group. Supported formats and types include:- **SID** (Windows): `S-1-5-21-1377283216-344919071-3415362939-500`- **UID** (Linux): `4578`Store the ID type in the GroupIdType field. If other IDs are available, we recommend that you normalize the field names to **GroupSid** or **GroupUid**, respectively. For more information, see [The User entity](normalization-entity-user).Example: `S-1-12` |
| **GroupIdType** | Optional | Enumerated | The type of the ID stored in the GroupId field. Supported values are `SID`, and `UID`. |
| **GroupName** | Optional | String | The group name, including domain information when available, for activities involving a group. Use one of the following formats and in the following order of priority:- **Upn/Email**: `grp@contoso.com`- **Windows**: `Contoso\grp`- **DN**: `CN=grp,OU=Sales,DC=Fabrikam,DC=COM`- **Simple**: `grp`. Use the Simple form only if domain information isn't available.Store the group name type in the GroupNameType field. If other IDs are available, we recommend that you normalize the field names to **GroupUpn**, **GroupNameWindows**, and **GroupDn**.Example: `Contoso\Finance` |
| **GroupNameType** | Optional | Enumerated | Specifies the type of the group name stored in the GroupName field. Supported values include `UPN`, `Windows`, `DN`, and `Simple`.Example: `Windows` |
| **GroupType** | Optional | Enumerated | The type of the group, for activities involving a group. Supported values include:- `Local Distribution`- `Local Security Enabled`- `Global Distribution`- `Global Security Enabled`- `Universal Distribution`- `Universal Security Enabled`- `Other`**Note**: The value might be provided in the source record by using different terms, which should be normalized to these values. Store the original value in the GroupOriginalType field. |
| **GroupOriginalType** | Optional | String | The original group type, if provided by the source. |

### Source fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **Src** | Recommended | String | A unique identifier of the source device. This field might alias the SrcDvcId, SrcHostname, or SrcIpAddr fields. Example: `192.168.12.1` |
| **SrcIpAddr** | Recommended | IP address | The IP address of the source device. This value is mandatory if **SrcHostname** is specified.Example: `77.138.103.108` |
| **IpAddr** | Alias |  | Alias to SrcIpAddr. |
| **SrcPortNumber** | Optional | Integer | The IP port from which the connection originated. Might not be relevant for a session comprising multiple connections.Example: `2335` |
| **SrcMacAddr** | Optional | MAC Address (String) | The MAC address of the network interface from which the connection or session originated.Example: `06:10:9f:eb:8f:14` |
| **SrcDescription** | Optional | String | A descriptive text associated with the device. For example: `Primary Domain Controller`. |
| **SrcHostname** | Recommended | String | The source device hostname, excluding domain information.Example: `DESKTOP-1282V4D` |
| **SrcDomain** | Recommended | Domain (String) | The domain of the source device.Example: `Contoso` |
| **SrcDomainType** | Recommended | Enumerated | The type of SrcDomain, if known. Possible values include:- `Windows` (such as `contoso`)- `FQDN` (such as `microsoft.com`)Required if SrcDomain is used. |
| **SrcFQDN** | Optional | FQDN (String) | The source device hostname, including domain information when available. **Note**: This field supports both traditional FQDN format and Windows domain\hostname format. The SrcDomainType field reflects the format used. Example: `Contoso\DESKTOP-1282V4D` |
| **SrcDvcId** | Optional | String | The ID of the source device as reported in the record.Example: `ac7e9755-8eae-4ffc-8a02-50ed7a2216c3` |
| **SrcDvcScopeId** | Optional | String | The cloud platform scope ID the device belongs to. **SrcDvcScopeId** map to a subscription ID on Azure and to an account ID on AWS. |
| **SrcDvcScope** | Optional | String | The cloud platform scope the device belongs to. **SrcDvcScope** map to a subscription ID on Azure and to an account ID on AWS. |
| **SrcDvcIdType** | Conditional | Enumerated | The type of SrcDvcId, if known. Possible values include: - `AzureResourceId`- `MDEid`If multiple IDs are available, use the first one from the preceding list, and store the others in **SrcDvcAzureResourceId** and **SrcDvcMDEid**, respectively.**Note**: This field is required if SrcDvcId is used. |
| **SrcDeviceType** | Optional | Enumerated | The type of the source device. Possible values include:- `Computer`- `Mobile Device`- `IOT Device`- `Other` |
| **SrcGeoCountry** | Optional | Country | The country/region associated with the source IP address.Example: `USA` |
| **SrcGeoRegion** | Optional | Region | The region associated with the source IP address.Example: `Vermont` |
| **SrcGeoCity** | Optional | City | The city associated with the source IP address.Example: `Burlington` |
| **SrcGeoLatitude** | Optional | Latitude | The latitude of the geographical coordinate associated with the source IP address.Example: `44.475833` |
| **SrcGeoLongitude** | Optional | Longitude | The longitude of the geographical coordinate associated with the source IP address.Example: `73.211944` |
| **SrcRiskLevel** | Optional | Integer | The risk level associated with the source. The value should be adjusted to a range of `0` to `100`, with `0` for benign and `100` for a high risk.Example: `90` |
| **SrcOriginalRiskLevel** | Optional | String | The risk level associated with the source, as reported by the reporting device. Example: `Suspicious` |

### Acting Application

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **ActingAppId** | Optional | String | The ID of the application used by the actor to perform the activity, including a process, browser, or service. For example: `0x12ae8` |
| **ActingAppName** | Optional | String | The name of the application used by the actor to perform the activity, including a process, browser, or service. For example: `C:\Windows\System32\svchost.exe` |
| **ActingAppType** | Optional | Enumerated | The type of acting application. Supported values include: - `Process`- `Browser`- `Resource`- `Other` |
| **ActingOriginalAppType** | Optional | String | The type of the application that initiated the activity as reported by the reporting device. |
| **HttpUserAgent** | Optional | String | When authentication is performed over HTTP or HTTPS, this field's value is the user\_agent HTTP header provided by the acting application when performing the authentication.For example: `Mozilla/5.0 (iPhone; CPU iPhone OS 12_1 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0 Mobile/15E148 Safari/604.1` |

### Inspection fields

The following fields are used to represent that inspection performed by a security system such an EDR system.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **RuleName** | Optional | String | The name or ID of the rule by associated with the inspection results. |
| **RuleNumber** | Optional | Integer | The number of the rule associated with the inspection results. |
| **Rule** | Conditional | String | Either the value of RuleName or the value of RuleNumber. If the value of RuleNumber is used, the type should be converted to string. |
| **ThreatId** | Optional | String | The ID of the threat or malware identified in the file activity. |
| **ThreatName** | Optional | String | The name of the threat or malware identified in the file activity.Example: `EICAR Test File` |
| **ThreatCategory** | Optional | String | The category of the threat or malware identified in the file activity.Example: `Trojan` |
| **ThreatRiskLevel** | Optional | RiskLevel (Integer) | The risk level associated with the identified threat. The level should be a number between **0** and **100**.**Note**: The value might be provided in the source record by using a different scale, which should be normalized to this scale. The original value should be stored in ThreatOriginalRiskLevel. |
| **ThreatOriginalRiskLevel** | Optional | String | The risk level as reported by the reporting device. |
| **ThreatField** | Optional | String | The field for which a threat was identified. |
| **ThreatConfidence** | Optional | ConfidenceLevel (Integer) | The confidence level of the threat identified, normalized to a value between 0 and a 100. |
| **ThreatOriginalConfidence** | Optional | String | The original confidence level of the threat identified, as reported by the reporting device. |
| **ThreatIsActive** | Optional | Boolean | True if the threat identified is considered an active threat. |
| **ThreatFirstReportedTime** | Optional | datetime | The first time the IP address or domain were identified as a threat. |
| **ThreatLastReportedTime** | Optional | datetime | The last time the IP address or domain were identified as a threat. |

### Additional fields and aliases

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **Hostname** | Alias |  | Alias to [DvcHostname](normalization-common-fields#dvchostname). |

### Entity correlation fields

Note

Contributors don't need to populate these fields. Applicable parsers will populate them when internal Microsoft support is added.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **ActingApplicationEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the acting application within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **ActorUserAdditionalIds** | Optional | Dynamic | For the field structure and usage, see [Fields suffixed with AdditionalIds](normalization-common-fields#fields-suffixed-with-additionalids). |
| **ActorUserEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the actor user within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **SrcSystemEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the source system within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **TargetUserAdditionalIds** | Optional | Dynamic | For the field structure and usage, see [Fields suffixed with AdditionalIds](normalization-common-fields#fields-suffixed-with-additionalids). |
| **TargetUserEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the target user within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |

## Schema updates

| Version | Changes |
| --- | --- |
| 0.1.2 | - Added inspection fields.- Added the source fields `SrcDescription`, `SrcMacAddr`, `SrcOriginalRiskLevel`, `SrcPortNumber`, and `SrcRiskLevel`.- Added the target fields `TargetUserScope`, `TargetUserScopeId`, and `TargetUserSessionId`.- Added the actor fields `ActorOriginalUserType`, `ActorScope`, and `ActorScopeId`.- Added the acting application field `ActingOriginalAppType`. |
| 1.0.0 | Added entity correlation fields. |