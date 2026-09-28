---
layout: Conceptual
title: The Advanced Security Information Model (ASIM) Registry Event normalization schema reference | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/normalization-schema-registry-event
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
description: This article describes the Microsoft Sentinel Registry Event normalization schema.
ms.author: edbaynash
author: EdB-MSFT
ms.topic: reference
ms.date: 2026-09-16T00:00:00.0000000Z
locale: en-us
document_id: 9e87fae2-fad2-4181-13b7-a4c973294472
document_version_independent_id: 433ca128-0457-f997-e582-9c165dedf033
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/normalization-schema-registry-event.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/normalization-schema-registry-event
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/normalization-schema-registry-event.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
platformId: c42cc7c3-00ba-9aac-7a8a-34c4d30a2209
---

# The Advanced Security Information Model (ASIM) Registry Event normalization schema reference | Microsoft Learn

The Registry Event schema is used to describe the Windows activity of creating, modifying, or deleting Windows Registry entities.

Registry events are specific to Windows systems, but are reported by different systems that monitor Windows, such as EDR (End Point Detection and Response) systems, Sysmon, or Windows itself.

For more information about normalization in Microsoft Sentinel, see [Normalization and the Advanced Security Information Model (ASIM)](normalization).

## Parsers

To use the unifying parser that unifies all of the built-in parsers, and ensure that your analysis runs across all the configured sources, use **imRegistry** as the table name in your query.

For the list of the Process Event parsers Microsoft Sentinel provides out-of-the-box refer to the [ASIM parsers list](normalization-parsers-list#registry-event-parsers)

Deploy the [unifying and source-specific parsers](normalization-about-parsers) from the [Microsoft Sentinel GitHub repository](https://aka.ms/AzSentinelRegistry).

For more information, see [ASIM parsers](normalization-parsers-overview) and [Use ASIM parsers](normalization-about-parsers).

### Add your own normalized parsers

When implementing custom parsers for the Registry Event information model, name your KQL functions using the following syntax: `imRegistry<vendor><Product>`.

Add your KQL functions to the `imRegistry` unifying parsers to ensure that any content using the Registry Event model also uses your new parser.

### Filtering parser parameters

The Registry Event parsers support [filtering parameters](normalization-about-parsers#optimizing-parsing-using-parameters). While these parameters are optional, they can improve your query performance.

The following filtering parameters are available:

| Name | Type | Description |
| --- | --- | --- |
| **starttime** | datetime | Filter only registry events that occurred at or after this time. This parameter filters on the `TimeGenerated` field, which is the standard designator for the time of the event, regardless of the parser-specific mapping of the EventStartTime and EventEndTime fields. |
| **endtime** | datetime | Filter only registry events that occurred at or before this time. This parameter filters on the `TimeGenerated` field, which is the standard designator for the time of the event, regardless of the parser-specific mapping of the EventStartTime and EventEndTime fields. |
| **eventtype\_in** | dynamic | Filter only registry events where the event type is one of the values listed, including: `RegistryKeyCreated`, `RegistryKeyDeleted`, `RegistryKeyRenamed`, `RegistryValueDeleted`, or `RegistryValueSet`. |
| **actorusername\_has\_any** | dynamic | Filter only registry events where the actor username has any of the listed values. |
| **registrykey\_has\_any** | dynamic | Filter only registry events where the registry key has any of the listed values. |
| **registryvalue\_has\_any** | dynamic | Filter only registry events where the registry value has any of the listed values. |
| **registrydata\_has\_any** | dynamic | Filter only registry events where the registry data has any of the listed values. |
| **dvchostname\_has\_any** | dynamic | Filter only registry events where the device hostname has any of the listed values. |

For example, to filter only registry key creation events from the last day, use:

```kusto
_Im_RegistryEvent (eventtype_in=dynamic(['RegistryKeyCreated']), starttime = ago(1d), endtime=now())
```

## Normalized content

Microsoft Sentinel provides the [Persisting Via IFEO Registry Key](https://github.com/Azure/Azure-Sentinel/blob/master/Hunting%20Queries/MultipleDataSources/PersistViaIFEORegistryKey.yaml) hunting query. This query works on any registry activity data normalized using the Advanced Security Information Model.

For more information, see [Hunt for threats with Microsoft Sentinel](hunting).

## Schema details

The Registry Event information model is aligned with the [OSSEM Registry entity schema](https://github.com/OTRF/OSSEM/blob/master/docs/cdm/entities/registry.md).

### Common ASIM fields

Important

Fields common to all schemas are described in detail in the [ASIM Common Fields](normalization-common-fields) article.

#### Common fields with specific guidelines

The following list mentions fields that have specific guidelines for process activity events:

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **EventType** | Mandatory | Enumerated | Describes the operation reported by the record. For Registry records, supported values include: - `RegistryKeyCreated`- `RegistryKeyDeleted`- `RegistryKeyRenamed`- `RegistryValueDeleted`- `RegistryValueSet` |
| **EventSchemaVersion** | Mandatory | SchemaVersion (String) | The version of the schema. The version of the schema documented here is `1.0.0` |
| **EventSchema** | Mandatory | String | The name of the schema documented here is `RegistryEvent`. |
| **Dvc** fields |  |  | For registry activity events, device fields refer to the system on which the registry activity occurred. |

#### All common fields

Fields that appear in the table below are common to all ASIM schemas. Any guideline specified above overrides the general guidelines for the field. For example, a field might be optional in general, but mandatory for a specific schema. For further details on each field, refer to the [ASIM Common Fields](normalization-common-fields) article.

| **Class** | **Fields** |
| --- | --- |
| Mandatory | - [EventCount](normalization-common-fields#eventcount) - [EventStartTime](normalization-common-fields#eventstarttime) - [EventEndTime](normalization-common-fields#eventendtime) - [EventType](normalization-common-fields#eventtype)- [EventResult](normalization-common-fields#eventresult) - [EventProduct](normalization-common-fields#eventproduct) - [EventVendor](normalization-common-fields#eventvendor) - [EventSchema](normalization-common-fields#eventschema) - [EventSchemaVersion](normalization-common-fields#eventschemaversion) - [Dvc](normalization-common-fields#dvc) |
| Recommended | - [EventResultDetails](normalization-common-fields#eventresultdetails)- [EventSeverity](normalization-common-fields#eventseverity)- [EventUid](normalization-common-fields#eventuid) - [DvcIpAddr](normalization-common-fields#dvcipaddr) - [DvcHostname](normalization-common-fields#dvchostname) - [DvcDomain](normalization-common-fields#dvcdomain)- [DvcDomainType](normalization-common-fields#dvcdomaintype)- [DvcFQDN](normalization-common-fields#dvcfqdn)- [DvcId](normalization-common-fields#dvcid)- [DvcIdType](normalization-common-fields#dvcidtype)- [DvcAction](normalization-common-fields#dvcaction) |
| Optional | - [EventMessage](normalization-common-fields#eventmessage) - [EventSubType](normalization-common-fields#eventsubtype)- [EventOriginalUid](normalization-common-fields#eventoriginaluid)- [EventOriginalType](normalization-common-fields#eventoriginaltype)- [EventOriginalSubType](normalization-common-fields#eventoriginalsubtype)- [EventOriginalResultDetails](normalization-common-fields#eventoriginalresultdetails) - [EventOriginalSeverity](normalization-common-fields#eventoriginalseverity) - [EventProductVersion](normalization-common-fields#eventproductversion) - [EventReportUrl](normalization-common-fields#eventreporturl) - [EventOwner](normalization-common-fields#eventowner)- [DvcZone](normalization-common-fields#dvczone)- [DvcMacAddr](normalization-common-fields#dvcmacaddr)- [DvcOs](normalization-common-fields#dvcos)- [DvcOsVersion](normalization-common-fields#dvchostname)- [DvcOriginalAction](normalization-common-fields#dvcoriginalaction)- [DvcInterface](normalization-common-fields#dvcinterface)- [AdditionalFields](normalization-common-fields#additionalfields)- [DvcDescription](normalization-common-fields#dvcdescription)- [DvcScopeId](normalization-common-fields#dvcscopeid)- [DvcScope](normalization-common-fields#dvcscope) |

### Registry Event specific fields

The fields listed in the table below are specific to Registry events, but are similar to fields in other schemas and follow similar naming conventions.

For more information, see [Structure of the Registry](/en-us/windows/win32/sysinfo/structure-of-the-registry) in Windows documentation.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **RegistryKey** | Mandatory | String | The registry key associated with the operation, normalized to standard root key naming conventions. For more information, see Root Keys.Registry keys are similar to folders in file systems. For example: `HKEY_LOCAL_MACHINE\SOFTWARE\MTG` |
| **RegistryValue** | Recommended | String | The registry value associated with the operation. Registry values are similar to files in file systems. For example: `Path` |
| **RegistryValueType** | Recommended | String | The type of registry value, normalized to standard form. For more information, see Value Types.For example: `Reg_Expand_Sz` |
| **RegistryValueData** | Recommended | String | The data stored in the registry value. Example: `C:\Windows\system32;C:\Windows;` |
| **RegistryPreviousKey** | Recommended | String | For operations that modify the registry, the original registry key, normalized to standard root key naming. For more information, see Root Keys. **Note**: If the operation changed other fields, such as the value, but the key remains the same, the RegistryPreviousKey will have the same value as RegistryKey.Example: `HKEY_LOCAL_MACHINE\SOFTWARE\MTG` |
| **RegistryPreviousValue** | Recommended | String | For operations that modify the registry, the original value type, normalized to the standard form. For more information, see Value Types. If the type was not changed, this field has the same value as the RegistryValueType field. Example: `Path` |
| **RegistryPreviousValueType** | Recommended | String | For operations that modify the registry, the original value type. If the type was not changed, this field will have the same value as the RegistryValueType field, normalized to the standard form. For more information, see Value types.Example: `Reg_Expand_Sz` |
| **RegistryPreviousValueData** | Recommended | String | The original registry data, for operations that modify the registry. Example: `C:\Windows\system32;C:\Windows;` |
| **User** | Alias |  | Alias to the ActorUsername field. Example: `CONTOSO\ dadmin` |
| **Process** | Alias |  | Alias to the ActingProcessName field.Example: `C:\Windows\System32\rundll32.exe` |
| **ActorUsername** | Mandatory | Username (String) | The user name of the user who initiated the event. Example: `CONTOSO\WIN-GG82ULGC9GO$` |
| **ActorUsernameType** | Conditional | Enumerated | Specifies the type of the user name stored in the ActorUsername field. For more information, see [The User entity](normalization-entity-user). Example: `Windows` |
| **ActorUserId** | Recommended | String | A unique ID of the Actor. The specific ID depends on the system generating the event. For more information, see [The User entity](normalization-entity-user). Example: `S-1-5-18` |
| **ActorScope** | Optional | String | The scope, such as Microsoft Entra tenant, in which ActorUserId and ActorUsername are defined. or more information and list of allowed values, see [UserScope](normalization-entity-user#userscope) in the [Schema Overview article](normalization-about-schemas). |
| **ActorUserIdType** | Conditional | Enumerated | The type of the ID stored in the ActorUserId field. For more information, see [The User entity](normalization-entity-user). Example: `SID` |
| **ActorSessionId** | Optional | String | The unique ID of the login session of the Actor. Example: `999`**Note**: The type is defined as *string* to support varying systems, but on Windows this value must be numeric. If you are using a Windows machine and the source sends a different type, make sure to convert the value. For example, if source sends a hexadecimal value, convert it to a decimal value. |
| **ActingProcessName** | Optional | String | The file name of the acting process image file. This name is typically considered to be the process name. Example: `C:\Windows\explorer.exe` |
| **ActingProcessId** | Mandatory | String | The process ID (PID) of the acting process.Example: `48610176`**Note**: The type is defined as *string* to support varying systems, but on Windows and Linux this value must be numeric. If you are using a Windows or Linux machine and used a different type, make sure to convert the values. For example, if you used a hexadecimal value, convert it to a decimal value. |
| **ActingProcessGuid** | Optional | GUID (String) | A generated unique identifier (GUID) of the acting process.  Example: `EF3BD0BD-2B74-60C5-AF5C-010000001E00` |
| **ParentProcessName** | Optional | String | The file name of the parent process image file. This value is typically considered to be the process name. Example: `C:\Windows\explorer.exe` |
| **ParentProcessId** | Mandatory | String | The process ID (PID) of the parent process.  Example: `48610176` |
| **ParentProcessGuid** | Optional | String | A generated unique identifier (GUID) of the parent process.  Example: `EF3BD0BD-2B74-60C5-AF5C-010000001E00` |

### Inspection fields

The following fields are used to represent that inspection performed by a security system such an EDR system.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **RuleName** | Optional | String | The name or ID of the rule by associated with the inspection results. |
| **RuleNumber** | Optional | Integer | The number of the rule associated with the inspection results. |
| **Rule** | Conditional | String | Either the value of kRuleName or the value of RuleNumber. If the value of RuleNumber is used, the type should be converted to string. |
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

### Root keys

Different sources represent registry key prefixes using different representations. For the RegistryKey and RegistryPreviousKey fields, use the following normalized prefixes:

| Normalized key prefix | Other common representations |
| --- | --- |
| **HKEY\_LOCAL\_MACHINE** | `HKLM`, `\REGISTRY\MACHINE` |
| **HKEY\_USERS** | `HKU`, `\REGISTRY\USER` |

### Value types

Different sources represent registry value types using different representations. For the RegistryValueType and RegistryPreviousValueType fields, use the following normalized types:

| Normalized key prefix | Other common representations |
| --- | --- |
| **Reg\_None** | `None`, `%%1872` |
| **Reg\_Sz** | `String`, `%%1873` |
| **Reg\_Expand\_Sz** | `ExpandString`, `%%1874` |
| **Reg\_Binary** | `Binary`, `%%1875` |
| **Reg\_DWord** | `Dword`, `%%1876` |
| **Reg\_Multi\_Sz** | `MultiString`, `%%1879` |
| **Reg\_QWord** | `Qword`, `%%1883` |

### Entity correlation fields

Note

Contributors don't need to populate these fields. Applicable parsers will populate them when internal Microsoft support is added.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **ActingProcessEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the acting process within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **ActorUserAdditionalIds** | Optional | Dynamic | For the field structure and usage, see [Fields suffixed with AdditionalIds](normalization-common-fields#fields-suffixed-with-additionalids). |
| **ActorUserEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the actor user within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **ParentProcessEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the parent process within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |

## Schema updates

| Version | Changes |
| --- | --- |
| 0.1.1 | Added the field `EventSchema`. |
| 0.1.2 | Added the fields `ActorScope`, `DvcScopeId`, and `DvcScope`. |
| 0.1.3 | Added inspection fields. |
| 1.0.0 | Added entity correlation fields. |