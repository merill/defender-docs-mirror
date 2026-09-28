---
layout: Conceptual
title: The Advanced Security Information Model (ASIM) File Event normalization schema reference | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/normalization-schema-file-event
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
description: This article describes the Microsoft Sentinel File Event normalization schema.
ms.author: edbaynash
author: EdB-MSFT
ms.topic: reference
ms.date: 2026-09-16T00:00:00.0000000Z
locale: en-us
document_id: 8316811e-a1ac-ac3f-82a8-3e26056ba9f1
document_version_independent_id: cf74cac9-0262-8181-3e39-8d962bd6d2a7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/normalization-schema-file-event.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/normalization-schema-file-event
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/normalization-schema-file-event.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: dc6fa435-3276-f44a-669f-a5e3e40204a1
---

# The Advanced Security Information Model (ASIM) File Event normalization schema reference | Microsoft Learn

The File Event normalization schema is used to describe file activity such as creating, modifying, or deleting files or documents. Such events are reported by operating systems, file storage systems such as Azure Files, and document management systems such as Microsoft SharePoint.

For more information about normalization in Microsoft Sentinel, see [Normalization and the Advanced Security Information Model (ASIM)](normalization).

## Parsers

### Deploying and using file activity parsers

Deploy the ASIM File Activity parsers from the [Microsoft Sentinel GitHub repository](https://aka.ms/DeployASIM). To query across all File Activity sources, use the unifying parser `imFileEvent` as the table name in your query.

For more information about using ASIM parsers, see the [ASIM parsers overview](normalization-parsers-overview). For the list of the file activity parsers Microsoft Sentinel provides out-of-the-box refer to the [ASIM parsers list](normalization-parsers-list#file-activity-parsers)

### Add your own normalized parsers

When implementing custom parsers for the File Event information model, name your KQL functions using the following syntax: `imFileEvent<vendor><Product`.

Refer to the article [Managing ASIM parsers](normalization-manage-parsers) to learn how to add your custom parsers to the file activity unifying parser.

### Filtering parser parameters

The File Event parsers support [filtering parameters](normalization-about-parsers#optimizing-parsing-using-parameters). While these parameters are optional, they can improve your query performance.

The following filtering parameters are available:

| Name | Type | Description |
| --- | --- | --- |
| **starttime** | datetime | Filter only file events that occurred at or after this time. This parameter filters on the `TimeGenerated` field, which is the standard designator for the time of the event, regardless of the parser-specific mapping of the EventStartTime and EventEndTime fields. |
| **endtime** | datetime | Filter only file events that occurred at or before this time. This parameter filters on the `TimeGenerated` field, which is the standard designator for the time of the event, regardless of the parser-specific mapping of the EventStartTime and EventEndTime fields. |
| **eventtype\_in** | dynamic | Filter only file events where the event type is one of the values listed, such as `FileCreated`, `FileModified`, `FileDeleted`, `FileRenamed`, or `FileCopied`. |
| **srcipaddr\_has\_any\_prefix** | dynamic | Filter only file events where the source IP address prefix matches any of the listed values. Prefixes should end with a `.`, for example: `10.0.`. |
| **actorusername\_has\_any** | dynamic | Filter only file events where the actor username has any of the listed values. |
| **targetfilepath\_has\_any** | dynamic | Filter only file events where the target file path has any of the listed values. |
| **srcfilepath\_has\_any** | dynamic | Filter only file events where the source file path has any of the listed values. |
| **hashes\_has\_any** | dynamic | Filter only file events where the file hash matches any of the listed values. |
| **dvchostname\_has\_any** | dynamic | Filter only file events where the device hostname has any of the listed values. |

For example, to filter only file creation and modification events from the last day, use:

```kusto
_Im_FileEvent (eventtype_in=dynamic(['FileCreated','FileModified']), starttime = ago(1d), endtime=now())
```

## Normalized content

For a full list of analytics rules that use normalized File Activity events, see [File Activity security content](normalization-content#file-activity-security-content).

## Schema overview

The File Event information model is aligned to the [OSSEM Process entity schema](https://github.com/OTRF/OSSEM/blob/master/docs/cdm/entities/file.md).

The File Event schema references the following entities, which are central to file activities:

- **Actor**. The user that initiated the file activity
- **ActingProcess**. The process used by the Actor to initiate the file activity
- **TargetFile**. The file on which the operation was performed
- **Source File (SrcFile)**. Stores file information prior to the operation.

The relationship between these entities is best demonstrated as follows: An **Actor** performs a file operation using an **Acting Process**, which modifies the **Source File** to **Target File**.

For example: `JohnDoe` (**Actor**) uses `Windows File Explorer` (**Acting process**) to rename `new.doc` (**Source File**) to `old.doc` (**Target File**).

## Schema details

### Common fields

Important

Fields common to all schemas are described in detail in the [ASIM Common Fields](normalization-common-fields) article.

#### Fields with specific guidelines for the File Event schema

The following list mentions fields that have specific guidelines for File activity events:

| **Field** | **Class** | **Type** | **Description** |
| --- | --- | --- | --- |
| **EventType** | Mandatory | Enumerated | Describes the operation reported by the record. Supported values include: - `FileAccessed`- `FileCreated`- `FileModified`- `FileDeleted`- `FileRenamed`- `FileCopied`- `FileMoved`- `FolderCreated`- `FolderDeleted`- `FolderMoved`- `FolderModified`- `FileCreatedOrModified` |
| **EventSubType** | Optional | Enumerated | Describes details about the operation reported in EventType. Supported values per event type include:- `FileCreated` - `Upload`, `Checkin`- `FileModified` - `Checkin`- `FileCreatedOrModified` - `Checkin`- `FileAccessed` - `Download`, `Preview`, `Checkout`, `Extended`- `FileDeleted` - `Recycled`, `Versions`, `Site` |
| **EventSchema** | Mandatory | Enumerated | The name of the schema documented here is **FileEvent**. |
| **EventSchemaVersion** | Mandatory | SchemaVersion (String) | The version of the schema. The version of the schema documented here is `1.0.0` |
| **Dvc** fields | - | - | For File activity events, device fields refer to the system on which the file activity occurred. |

Important

The `EventSchema` field is currently optional but will become Mandatory on September 1st 2022.

#### All common fields

Fields that appear in the table are common to all ASIM schemas. Any of the schema specific guidelines in this document overrides the general guidelines for the field. For example, a field might be optional in general, but mandatory for a specific schema. For more information on each field, see to the [ASIM Common Fields](normalization-common-fields) article.

| **Class** | **Fields** |
| --- | --- |
| Mandatory | - [EventCount](normalization-common-fields#eventcount) - [EventStartTime](normalization-common-fields#eventstarttime) - [EventEndTime](normalization-common-fields#eventendtime) - [EventType](normalization-common-fields#eventtype)- [EventResult](normalization-common-fields#eventresult) - [EventProduct](normalization-common-fields#eventproduct) - [EventVendor](normalization-common-fields#eventvendor) - [EventSchema](normalization-common-fields#eventschema) - [EventSchemaVersion](normalization-common-fields#eventschemaversion) - [Dvc](normalization-common-fields#dvc) |
| Recommended | - [EventResultDetails](normalization-common-fields#eventresultdetails)- [EventSeverity](normalization-common-fields#eventseverity)- [EventUid](normalization-common-fields#eventuid) - [DvcIpAddr](normalization-common-fields#dvcipaddr) - [DvcHostname](normalization-common-fields#dvchostname) - [DvcDomain](normalization-common-fields#dvcdomain)- [DvcDomainType](normalization-common-fields#dvcdomaintype)- [DvcFQDN](normalization-common-fields#dvcfqdn)- [DvcId](normalization-common-fields#dvcid)- [DvcIdType](normalization-common-fields#dvcidtype)- [DvcAction](normalization-common-fields#dvcaction) |
| Optional | - [EventMessage](normalization-common-fields#eventmessage) - [EventSubType](normalization-common-fields#eventsubtype)- [EventOriginalUid](normalization-common-fields#eventoriginaluid)- [EventOriginalType](normalization-common-fields#eventoriginaltype)- [EventOriginalSubType](normalization-common-fields#eventoriginalsubtype)- [EventOriginalResultDetails](normalization-common-fields#eventoriginalresultdetails) - [EventOriginalSeverity](normalization-common-fields#eventoriginalseverity) - [EventProductVersion](normalization-common-fields#eventproductversion) - [EventReportUrl](normalization-common-fields#eventreporturl) - [EventOwner](normalization-common-fields#eventowner)- [DvcZone](normalization-common-fields#dvczone)- [DvcMacAddr](normalization-common-fields#dvcmacaddr)- [DvcOs](normalization-common-fields#dvcos)- [DvcOsVersion](normalization-common-fields#dvchostname)- [DvcOriginalAction](normalization-common-fields#dvcoriginalaction)- [DvcInterface](normalization-common-fields#dvcinterface)- [AdditionalFields](normalization-common-fields#additionalfields)- [DvcDescription](normalization-common-fields#dvcdescription)- [DvcScopeId](normalization-common-fields#dvcscopeid)- [DvcScope](normalization-common-fields#dvcscope) |

### Target file fields

The following fields represent information about the target file in a file operation. If the operation involves a single file, `FileCreate` for example, it is represented by the target file fields.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **TargetFileCreationTime** | Optional | Date/Time | The time at which the target file was created. |
| **TargetFileDirectory** | Optional | String | The target file folder or location. This field should be similar to the TargetFilePath field, without the final element. **Note**: A parser can provide this value if the value available in the log source and does not need to be extracted from the full path. |
| **TargetFileExtension** | Optional | String | The target file extension.**Note**: A parser can provide this value if the value available in the log source and does not need to be extracted from the full path. |
| **TargetFileMimeType** | Optional | String | The Mime, or Media, type of the target file. Allowed values are listed in the [IANA Media Types](https://www.iana.org/assignments/media-types/media-types.xhtml) repository. |
| **TargetFileName** | Recommended | String | The name of the target file, without a path or a location, but with an extension if relevant. This field should be similar to the final element in the TargetFilePath field. |
| **FileName** | Alias |  | Alias to the TargetFileName field. |
| **TargetFilePath** | Mandatory | String | The full, normalized path of the target file, including the folder or location, the file name, and the extension. For more information, see Path structure. **Note**: If the record does not include folder or location information, store the filename only here. Example: `C:\Windows\System32\notepad.exe` |
| **TargetFilePathType** | Mandatory | Enumerated | The type of TargetFilePath. For more information, see Path structure. |
| **FilePath** | Alias |  | Alias to the TargetFilePath field. |
| **TargetFileMD5** | Optional | MD5 | The MD5 hash of the target file. Example: `75a599802f1fa166cdadb360960b1dd0` |
| **TargetFileSHA1** | Optional | SHA1 | The SHA-1 hash of the target file. Example:`d55c5a4df19b46db8c54``c801c4665d3338acdab0` |
| **TargetFileSHA256** | Optional | SHA256 | The SHA-256 hash of the target file. Example:`e81bb824c4a09a811af17deae22f22dd``2e1ec8cbb00b22629d2899f7c68da274` |
| **TargetFileSHA512** | Optional | SHA512 | The SHA-512 hash of the source file. |
| **Hash** | Alias |  | Alias to the best available Target File hash. |
| **HashType** | Conditional | Enumerated | The type of hash stored in the HASH alias field, allowed values are `MD5`, `SHA`, `SHA256`, `SHA512` and `IMPHASH`. Mandatory if `Hash` is populated. |
| **TargetFileSize** | Optional | Long | The size of the target file in bytes. |

### Source file fields

The following fields represent information about the source file in a file operation that has both a source and a destination, such as copy. If the operation involves a single file, it is represented by the target file fields.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **SrcFileCreationTime** | Optional | Date/Time | The time at which the source file was created. |
| **SrcFileDirectory** | Optional | String | The source file folder or location. This field should be similar to the SrcFilePath field, without the final element. **Note**: A parser can provide this value if the value is available in the log source, and does not need to be extracted from the full path. |
| **SrcFileExtension** | Optional | String | The source file extension. **Note**: A parser can provide this value the value is available in the log source, and does not need to be extracted from the full path. |
| **SrcFileMimeType** | Optional | String | The Mime or Media type of the source file. Supported values are listed in the [IANA Media Types](https://www.iana.org/assignments/media-types/media-types.xhtml) repository. |
| **SrcFileName** | Recommended | String | The name of the source file, without a path or a location, but with an extension if relevant. This field should be similar to the last element in the SrcFilePath field. |
| **SrcFilePath** | Recommended | String | The full, normalized path of the source file, including the folder or location, the file name, and the extension. For more information, see Path structure.Example: `/etc/init.d/networking` |
| **SrcFilePathType** | Recommended | Enumerated | The type of SrcFilePath. For more information, see Path structure. |
| **SrcFileMD5** | Optional | MD5 | The MD5 hash of the source file. Example: `75a599802f1fa166cdadb360960b1dd0` |
| **SrcFileSHA1** | Optional | SHA1 | The SHA-1 hash of the source file.Example:`d55c5a4df19b46db8c54``c801c4665d3338acdab0` |
| **SrcFileSHA256** | Optional | SHA256 | The SHA-256 hash of the source file. Example:`e81bb824c4a09a811af17deae22f22dd``2e1ec8cbb00b22629d2899f7c68da274` |
| **SrcFileSHA512** | Optional | SHA512 | The SHA-512 hash of the source file. |
| **SrcFileSize** | Optional | Long | The size of the source file in bytes. |

### Actor fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **ActorUserId** | Recommended | String | A machine-readable, alphanumeric, unique representation of the Actor. For the supported format for different ID types, refer to [the User entity](normalization-entity-user). Example: `S-1-12` |
| **ActorScope** | Optional | String | The scope, such as Microsoft Entra tenant, in which ActorUserId and ActorUsername are defined. or more information and list of allowed values, see [UserScope](normalization-entity-user#userscope) in the [Schema Overview article](normalization-about-schemas). |
| **ActorScopeId** | Optional | String | The scope ID, such as Microsoft Entra Directory ID, in which ActorUserId and ActorUsername are defined. or more information and list of allowed values, see [UserScopeId](normalization-entity-user#userscopeid) in the [Schema Overview article](normalization-about-schemas). |
| **ActorUserIdType** | Conditional | Enumerated | The type of the ID stored in the ActorUserId field. For a list of allowed values and further information, refer to [UserIdType](normalization-entity-user#useridtype) in the [Schema Overview article](normalization-about-schemas). |
| **ActorUsername** | Mandatory | Username (String) | The Actor username, including domain information when available. For the supported format for different ID types, refer to [the User entity](normalization-entity-user). Use the simple form only if domain information isn't available.Store the Username type in the ActorUsernameType field. If other username formats are available, store them in the fields `ActorUsername<UsernameType>`.Example: `AlbertE` |
| **User** | Alias |  | Alias to the ActorUsername field. Example: `CONTOSO\dadmin` |
| **ActorUsernameType** | Conditional | Enumerated | Specifies the type of the user name stored in the ActorUsername field. For a list of allowed values and further information, refer to [UsernameType](normalization-entity-user#usernametype) in the [Schema Overview article](normalization-about-schemas).Example: `Windows` |
| **ActorSessionId** | Optional | String | The unique ID of the login session of the Actor. Example: `999`**Note**: The type is defined as *string* to support varying systems, but on Windows this value must be numeric. If you are using a Windows machine and used a different type, make sure to convert the values. For example, if you used a hexadecimal value, convert it to a decimal value. |
| **ActorUserType** | Optional | UserType | The type of Actor. For a list of allowed values and further information, refer to [UserType](normalization-entity-user#usertype) in the [Schema Overview article](normalization-about-schemas). **Note**: The value might be provided in the source record by using different terms, which should be normalized to these values. Store the original value in the ActorOriginalUserType field. |
| **ActorOriginalUserType** | Optional | String | The original destination user type, if provided by the reporting device. |

### Acting process fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **ActingProcessCommandLine** | Optional | String | The command line used to run the acting process. Example: `"choco.exe" -v` |
| **ActingProcessName** | Optional | string | The name of the acting process. This name is commonly derived from the image or executable file that's used to define the initial code and data that's mapped into the process' virtual address space.Example: `C:\Windows\explorer.exe` |
| **Process** | Alias |  | Alias to ActingProcessName |
| **ActingProcessId** | Optional | String | The process ID (PID) of the acting process.Example: `48610176`**Note**: The type is defined as *string* to support varying systems, but on Windows and Linux this value must be numeric. If you are using a Windows or Linux machine and used a different type, make sure to convert the values. For example, if you used a hexadecimal value, convert it to a decimal value. |
| **ActingProcessGuid** | Optional | GUID (string) | A generated unique identifier (GUID) of the acting process. Enables identifying the process across systems.  Example: `EF3BD0BD-2B74-60C5-AF5C-010000001E00` |

### Source system related fields

The following fields represent information about the system initiating the file activity, typically when carried over the network.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **SrcIpAddr** | Recommended | IP Address | When the operation is initiated by a remote system, the IP address of this system.Example: `185.175.35.214` |
| **IpAddr** | Alias |  | Alias to SrcIpAddr |
| **Src** | Alias |  | Alias to SrcIpAddr |
| **SrcPortNumber** | Optional | Integer | When the operation is initiated by a remote system, the port number from which the connection was initiated.Example: `2335` |
| **SrcHostname** | Optional | Hostname (String) | The source device hostname, excluding domain information. If no device name is available, store the relevant IP address in this field.Example: `DESKTOP-1282V4D` |
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
| **SrcGeoRegion** | Optional | Region | The region associated with the source IP address.Example: `Vermont` |
| **SrcGeoCity** | Optional | City | The city associated with the source IP address.Example: `Burlington` |
| **SrcGeoLatitude** | Optional | Latitude | The latitude of the geographical coordinate associated with the source IP address.Example: `44.475833` |
| **SrcGeoLongitude** | Optional | Longitude | The longitude of the geographical coordinate associated with the source IP address.Example: `73.211944` |

### Acting application fields

The following fields represent information about a local application that communicated over a network with a remote system to perform the file activity.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **ActingAppName** | Optional | String | The name of the acting application.Example: `Facebook` |
| **ActingAppId** | Optional | String | The ID of the acting application, as reported by the reporting device. |
| **ActingAppType** | Optional | AppType | The type of the destination application. For a list of allowed values and further information, refer to [AppType](normalization-about-schemas#apptype) in the [Schema Overview article](normalization-about-schemas).This field is mandatory if TargetAppName or TargetAppId are used. |
| **HttpUserAgent** | Optional | String | When the operation is initiated by a remote system using HTTP or HTTPS, the user agent used.For example:`Mozilla/5.0 (Windows NT 10.0; Win64; x64)``AppleWebKit/537.36 (KHTML, like Gecko)`` Chrome/42.0.2311.135``Safari/537.36 Edge/12.246` |
| **NetworkApplicationProtocol** | Optional | String | When the operation is initiated by a remote system, this value is the application layer protocol used in the OSI model. While this field is not enumerated, and any value is accepted, preferable values include: `HTTP`, `HTTPS`, `SMB`,`FTP`, and `SSH`Example: `SMB` |

### Target application fields

The following fields represent information about the destination application performing the file activity on behalf of the user. A destination application is usually related to over-the-network file activity, for example using SaaS (Software as a service) applications.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **TargetAppName** | Optional | String | The name of the destination application.Example: `Facebook` |
| **Application** | Alias |  | Alias to TargetAppName. |
| **TargetAppId** | Optional | String | The ID of the destination application, as reported by the reporting device. |
| **TargetAppType** | Conditional | AppType | The type of the destination application. For a list of allowed values and further information, refer to [AppType](normalization-about-schemas#apptype) in the [Schema Overview article](normalization-about-schemas).This field is mandatory if TargetAppName or TargetAppId are used. |
| **TargetOriginalAppType** | Optional | String | The type of the destination application as reported by the reporting device. |
| **TargetUrl** | Optional | URL (String) | When the operation is initiated using HTTP or HTTPS, the URL used. Example: `https://onedrive.live.com/?authkey=...` |
| **Url** | Alias |  | Alias to TargetUrl |

### Inspection fields

The following fields are used to represent that inspection performed by a security system such an anti-virus system. The thread identified is usually associated with the file on which the activity was performed rather than the activity itself.

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
| **ThreatFilePath** | Optional | String | A file path for which a threat was identified. The field ThreatField contains the name of the field **ThreatFilePath** represents. |
| **ThreatField** | Conditional | Enumerated | The field for which a threat was identified. The value is either `SrcFilePath` or `DstFilePath`. |
| **ThreatConfidence** | Optional | ConfidenceLevel (Integer) | The confidence level of the threat identified, normalized to a value between 0 and a 100. |
| **ThreatOriginalConfidence** | Optional | String | The original confidence level of the threat identified, as reported by the reporting device. |
| **ThreatIsActive** | Optional | Boolean | True if the threat identified is considered an active threat. |
| **ThreatFirstReportedTime** | Optional | datetime | The first time the IP address or domain were identified as a threat. |
| **ThreatLastReportedTime** | Optional | datetime | The last time the IP address or domain were identified as a threat. |

### Path structure

The path should be normalized to match one of the following formats. The format the value is normalized to will be reflected in the respective **FilePathType** field.

| Type | Example | Notes |
| --- | --- | --- |
| **Windows Local** | `C:\Windows\System32\notepad.exe` | Since Windows path names are case insensitive, this type implies that the value is case insensitive. |
| **Windows Share** | `\\Documents\My Shapes\Favorites.vssx` | Since Windows path names are case insensitive, this type implies that the value is case insensitive. |
| **Unix** | `/etc/init.d/networking` | Since Unix path names are case-sensitive, this type implies that the value is case-sensitive. - Use this type for AWS S3. Concatenate the bucket and key names to create the path. - Use this type for Azure Blob storage object keys. |
| **URL** | `https://1drv.ms/p/s!Av04S_*********we` | Use when the file path is available as a URL. URLs are not limited to *http* or *https*, and any value, including an FTP value, is valid. |

### Entity correlation fields

Note

Contributors don't need to populate these fields. Applicable parsers will populate them when internal Microsoft support is added.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **ActingApplicationEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the acting application within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **ActingProcessEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the acting process within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **ActorUserAdditionalIds** | Optional | Dynamic | For the field structure and usage, see [Fields suffixed with AdditionalIds](normalization-common-fields#fields-suffixed-with-additionalids). |
| **ActorUserEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the actor user within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **FileEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the file within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **SrcFileEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the source file within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **SrcSystemEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the source system within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **TargetApplicationEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the target application within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **TargetFileEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the target file within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |

## Schema updates

| Version | Changes |
| --- | --- |
| 0.1.1 | Added the field `EventSchema`. |
| 0.2 | - Added inspection fields.- Added the fields `ActorScope`, `TargetUserScope`, `HashType`, `TargetAppName`, `TargetAppId`, `TargetAppType`, `SrcGeoCountry`, `SrcGeoRegion`, `SrcGeoLongitude`, `SrcGeoLatitude`, `ActorSessionId`, `DvcScopeId`, and `DvcScope`.- Added the aliases `Url`, `IpAddr`, `FileName`, and `Src`. |
| 0.2.1 | - Added `Application` as an alias to `TargetAppName`.- Added the field `ActorScopeId`.- Added source device-related fields. |
| 0.2.2 | - Added the field `TargetOriginalAppType`.- Added the fields `ActingAppId`, `ActingAppName`, and `ActingAppType`, which aren't available in the `ASimFileEventLogs` table. |
| 1.0.0 | Added entity correlation fields. |