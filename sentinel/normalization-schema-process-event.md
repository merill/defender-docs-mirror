---
layout: Conceptual
title: The Advanced Security Information Model (ASIM) Process Event normalization schema reference | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/normalization-schema-process-event
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
description: This article describes the Microsoft Sentinel Process Event normalization schema.
ms.author: edbaynash
author: EdB-MSFT
ms.topic: reference
ms.date: 2026-10-07T00:00:00.0000000Z
locale: en-us
document_id: e20742cf-3f2b-d516-662b-af1b8554b5de
document_version_independent_id: 0746209f-5a4b-98f5-c8ad-e122b378a681
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/normalization-schema-process-event.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/normalization-schema-process-event
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/normalization-schema-process-event.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: f58aeced-92b8-a5d4-b997-20710fab302f
---

# The Advanced Security Information Model (ASIM) Process Event normalization schema reference | Microsoft Learn

The Process Event normalization schema is used to describe the operating system activity of running and terminating a process. Such events are reported by operating systems and security systems, such as EDR (End Point Detection and Response) systems.

A process, as defined by OSSEM, is a containment and management object that represents a running instance of a program. While processes themselves do not run, they do manage threads that run and execute code.

For more information about normalization in Microsoft Sentinel, see [Normalization and the Advanced Security Information Model (ASIM)](normalization).

## Parsers

Use `imProcessEvent` to query all process event types from every configured source. You can also use the following specialized unifying parsers:

- `imProcessCreate` for queries that require process creation information.
- `imProcessTerminate` for queries that require process termination information.

For the list of the Process Event parsers Microsoft Sentinel provides out-of-the-box refer to the [ASIM parsers list](normalization-parsers-list#process-event-parsers).

Deploy the Authentication parsers from the [Microsoft Sentinel GitHub repository](https://aka.ms/AzSentinelProcessEvents).

For more information, see [ASIM parsers overview](normalization-parsers-overview).

## Add your own normalized parsers

When you implement custom process event parsers, use `vimProcessEvent<vendor><Product>` for filtering parsers and `ASimProcessEvent<vendor><Product>` for parameter-less parsers.

Add your KQL function to the unifying parsers as described in [Managing ASIM parsers](normalization-manage-parsers).

### Filtering parser parameters

The `im` and `vim*` parsers support [filtering parameters](normalization-about-parsers#optimizing-parsing-using-parameters). While these parsers are optional, they can improve your query performance.

The following filtering parameters are available:

| Name | Type | Description |
| --- | --- | --- |
| **starttime** | datetime | Filter only process events occurred at or after this time. This parameter filters on the `TimeGenerated` field, which is the standard designator for the time of the event, regardless of the parser-specific mapping of the EventStartTime and EventEndTime fields. |
| **endtime** | datetime | Filter only process events queries that occurred at or before this time. This parameter filters on the `TimeGenerated` field, which is the standard designator for the time of the event, regardless of the parser-specific mapping of the EventStartTime and EventEndTime fields. |
| **commandline\_has\_any** | dynamic | Filter only process events for which the command line executed has **any** of the listed values. The length of the list is limited to 10,000 items. |
| **commandline\_has\_all** | dynamic | Filter only process events for which the command line executed has **all** of the listed values. The length of the list is limited to 10,000 items. |
| **commandline\_has\_any\_ip\_prefix** | dynamic | Filter only process events for which the command line executed has **any** of the listed IP addresses or IP address prefixes. Prefixes should end with a `.`, for example: `10.0.`. The length of the list is limited to 10,000 items. |
| **actingprocess\_has\_any** | dynamic | Filter only process events for which the acting process name, which includes the entire process path, has any of the listed values. The length of the list is limited to 10,000 items. |
| **targetprocess\_has\_any** | dynamic | Filter only process events for which the target process name, which includes the entire process path, has any of the listed values. The length of the list is limited to 10,000 items. |
| **parentprocess\_has\_any** | dynamic | Filter only process events for which the parent process name, which includes the entire process path, has any of the listed values. The length of the list is limited to 10,000 items. |
| **targetusername\_has** | string | Filter process creation events by a term in the target username. Pass a single string value, not a list. Use `*` to disable this filter. |
| **actorusername\_has** | string | Filter process termination events by a term in the actor username. Pass a single string value, not a list. Use `*` to disable this filter. |
| **dvcipaddr\_has\_any\_prefix** | dynamic | Filter only process events for which the device IP address matches any of the listed IP addresses or IP address prefixes. Prefixes should end with a `.`, for example: `10.0.`. The length of the list is limited to 10,000 items. |
| **dvchostname\_has\_any** | dynamic | Filter only process events for which the device hostname, or device FQDN is available, has any of the listed values. The length of the list is limited to 10,000 items. |
| **hashes\_has\_any** | dynamic | Filter only process events for which any of the target process hashes matches any of the listed values. |
| **eventtype** | string | Filter only process events of the specified type. |

For example, to filter process creation events from the last day for a specific target username, use:

```kusto
imProcessEvent(targetusername_has='johndoe', eventtype='ProcessCreated', starttime=ago(1d), endtime=now())
```

Tip

To pass a literal list to parameters that expect a dynamic value, explicitly use a [dynamic literal](/en-us/kusto/query/scalar-data-types/dynamic?view=microsoft-sentinel&amp;preserve-view=true#dynamic-literals). For example: `dynamic(['192.168.','10.'])`.

## Normalized content

For a full list of analytics rules that use normalized process events, see [Process Event security content](normalization-content#process-activity-security-content).

## Schema details

The Process Event information model is aligned to the [OSSEM Process entity schema](https://github.com/OTRF/OSSEM/blob/master/docs/cdm/entities/process.md).

### Common ASIM fields

Important

Fields common to all schemas are described in detail in the [ASIM Common Fields](normalization-common-fields) article.

#### Common fields with specific guidelines

The following list mentions fields that have specific guidelines for process activity events:

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **EventType** | Mandatory | Enumerated | Describes the operation reported by the record. For Process records, supported values include: - `ProcessCreated`- `ProcessTerminated` |
| **EventSchemaVersion** | Mandatory | SchemaVersion (String) | The version of the schema. The version of the schema documented here is `1.0.0` |
| **EventSchema** | Mandatory | String | The name of the schema documented here is `ProcessEvent`. |
| **Dvc** fields |  |  | For process activity events, device fields refer to the system on which the process was executed. |

Important

The `EventSchema` field is currently optional but will become Mandatory on September 1st 2022.

#### All common fields

Fields that appear in the table below are common to all ASIM schemas. Any guideline specified above overrides the general guidelines for the field. For example, a field might be optional in general, but mandatory for a specific schema. For further details on each field, refer to the [ASIM Common Fields](normalization-common-fields) article.

| **Class** | **Fields** |
| --- | --- |
| Mandatory | - [EventCount](normalization-common-fields#eventcount) - [EventStartTime](normalization-common-fields#eventstarttime) - [EventEndTime](normalization-common-fields#eventendtime) - [EventType](normalization-common-fields#eventtype)- [EventResult](normalization-common-fields#eventresult) - [EventProduct](normalization-common-fields#eventproduct) - [EventVendor](normalization-common-fields#eventvendor) - [EventSchema](normalization-common-fields#eventschema) - [EventSchemaVersion](normalization-common-fields#eventschemaversion) - [Dvc](normalization-common-fields#dvc) |
| Recommended | - [EventResultDetails](normalization-common-fields#eventresultdetails)- [EventSeverity](normalization-common-fields#eventseverity)- [EventUid](normalization-common-fields#eventuid) - [DvcIpAddr](normalization-common-fields#dvcipaddr) - [DvcHostname](normalization-common-fields#dvchostname) - [DvcDomain](normalization-common-fields#dvcdomain)- [DvcDomainType](normalization-common-fields#dvcdomaintype)- [DvcFQDN](normalization-common-fields#dvcfqdn)- [DvcId](normalization-common-fields#dvcid)- [DvcIdType](normalization-common-fields#dvcidtype)- [DvcAction](normalization-common-fields#dvcaction) |
| Optional | - [EventMessage](normalization-common-fields#eventmessage) - [EventSubType](normalization-common-fields#eventsubtype)- [EventOriginalUid](normalization-common-fields#eventoriginaluid)- [EventOriginalType](normalization-common-fields#eventoriginaltype)- [EventOriginalSubType](normalization-common-fields#eventoriginalsubtype)- [EventOriginalResultDetails](normalization-common-fields#eventoriginalresultdetails) - [EventOriginalSeverity](normalization-common-fields#eventoriginalseverity) - [EventProductVersion](normalization-common-fields#eventproductversion) - [EventReportUrl](normalization-common-fields#eventreporturl) - [EventOwner](normalization-common-fields#eventowner)- [DvcZone](normalization-common-fields#dvczone)- [DvcMacAddr](normalization-common-fields#dvcmacaddr)- [DvcOs](normalization-common-fields#dvcos)- [DvcOsVersion](normalization-common-fields#dvchostname)- [DvcOriginalAction](normalization-common-fields#dvcoriginalaction)- [DvcInterface](normalization-common-fields#dvcinterface)- [AdditionalFields](normalization-common-fields#additionalfields)- [DvcDescription](normalization-common-fields#dvcdescription)- [DvcScopeId](normalization-common-fields#dvcscopeid)- [DvcScope](normalization-common-fields#dvcscope) |

### Process Event-specific fields

The fields listed in the table below are specific to Process events, but are similar to fields in other schemas and follow similar naming conventions.

The process event schema references the following entities, which are central to process creation and termination activity:

- **Actor** - The user that initiated the process creation or termination.
- **ActingProcess** - The process used by the Actor to initiate the process creation or termination.
- **TargetProcess** - The new process.
- **TargetUser** - The user whose credentials are used to create the new process.
- **ParentProcess** - The process that initiated the Actor Process.

### Aliases

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **User** | Alias |  | Alias to the TargetUsername. Example: `CONTOSO\dadmin` |
| **Process** | Alias |  | Alias to the TargetProcessNameExample: `C:\Windows\System32\rundll32.exe` |
| **CommandLine** | Alias |  | Alias to TargetProcessCommandLine |
| **Hash** | Alias |  | Alias to the best available hash for the target process. |

### Actor fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **ActorUserId** | Recommended | String | A machine-readable, alphanumeric, unique representation of the Actor. For the supported format for different ID types, refer to [the User entity](normalization-entity-user). Example: `S-1-12` |
| **ActorUserIdType** | Conditional | Enumerated | The type of the ID stored in the ActorUserId field. For a list of allowed values and further information refer to [UserIdType](normalization-entity-user#useridtype) in the [Schema Overview article](normalization-about-schemas). |
| **ActorScope** | Optional | String | The scope, such as Microsoft Entra tenant, in which ActorUserId and ActorUsername are defined. or more information and list of allowed values, see [UserScope](normalization-entity-user#userscope) in the [Schema Overview article](normalization-about-schemas). |
| **ActorScopeId** | Optional | String | The scope ID, such as Microsoft Entra Directory ID, in which ActorUserId and ActorUsername are defined. or more information and list of allowed values, see [UserScopeId](normalization-entity-user#userscopeid) in the [Schema Overview article](normalization-about-schemas). |
| **ActorUsername** | Mandatory | Username (String) | The Actor username, including domain information when available. For the supported format for different ID types, refer to [the User entity](normalization-entity-user). Use the simple form only if domain information isn't available.Store the Username type in the ActorUsernameType field. If other username formats are available, store them in the fields `ActorUsername<UsernameType>`.Example: `AlbertE` |
| **ActorUsernameType** | Conditional | Enumerated | Specifies the type of the user name stored in the ActorUsername field. For a list of allowed values and further information refer to [UsernameType](normalization-entity-user#usernametype) in the [Schema Overview article](normalization-about-schemas).Example: `Windows` |
| **ActorSessionId** | Optional | String | The unique ID of the login session of the Actor. Example: `999`**Note**: The type is defined as *string* to support varying systems, but on Windows this value must be numeric. If you are using a Windows machine and used a different type, make sure to convert the values. For example, if you used a hexadecimal value, convert it to a decimal value. |
| **ActorUserType** | Optional | UserType | The type of Actor. For a list of allowed values and further information refer to [UserType](normalization-entity-user#usertype) in the [Schema Overview article](normalization-about-schemas). **Note**: The value might be provided in the source record by using different terms, which should be normalized to these values. Store the original value in the ActorOriginalUserType field. |
| **ActorOriginalUserType** | Optional | String | The original destination user type, if provided by the reporting device. |

### Acting process fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **ActingProcessCommandLine** | Optional | String | The command line used to run the acting process. Example: `"choco.exe" -v` |
| **ActingProcessName** | Optional | string | The name of the acting process. This name is commonly derived from the image or executable file that's used to define the initial code and data that's mapped into the process' virtual address space.Example: `C:\Windows\explorer.exe` |
| **ActingProcessFilename** | Optional | String | The file name part of the `ActingProcessName`, without folder information. Example: `explorer.exe` |
| **ActingProcessFileCompany** | Optional | String | The company that created the acting process image file.  Example: `Microsoft` |
| **ActingProcessFileDescription** | Optional | String | The description embedded in the version information of the acting process image file. Example: `Notepad++ : a free (GPL) source code editor` |
| **ActingProcessFileProduct** | Optional | String | The product name from the version information in the acting process image file.  Example: `Notepad++` |
| **ActingProcessFileVersion** | Optional | String | The product version from the version information of the acting process image file. Example: `7.9.5.0` |
| **ActingProcessFileInternalName** | Optional | String | The product internal file name from the version information of the acting process image file. |
| **ActingProcessFileOriginalName** | Optional | String | The product original file name from the version information of the acting process image file.  Example: `Notepad++.exe` |
| **ActingProcessIsHidden** | Optional | Boolean | An indication of whether the acting process is in hidden mode. |
| **ActingProcessInjectedAddress** | Optional | String | The memory address in which the responsible acting process is stored. |
| **ActingProcessId** | Mandatory | String | The process ID (PID) of the acting process.Example: `48610176`**Note**: The type is defined as *string* to support varying systems, but on Windows and Linux this value must be numeric. If you are using a Windows or Linux machine and used a different type, make sure to convert the values. For example, if you used a hexadecimal value, convert it to a decimal value. |
| **ActingProcessGuid** | Optional | GUID (string) | A generated unique identifier (GUID) of the acting process. Enables identifying the process across systems.  Example: `EF3BD0BD-2B74-60C5-AF5C-010000001E00` |
| **ActingProcessIntegrityLevel** | Optional | String | Every process has an integrity level that is represented in its token. Integrity levels determine the process level of protection or access.  Windows defines the following integrity levels: **low**, **medium**, **high**, and **system**. Standard users receive a **medium** integrity level and elevated users receive a **high** integrity level.  For more information, see [Mandatory Integrity Control - Win32 apps](/en-us/windows/win32/secauthz/mandatory-integrity-control). |
| **ActingProcessMD5** | Optional | String | The MD5 hash of the acting process image file. Example: `75a599802f1fa166cdadb360960b1dd0` |
| **ActingProcessSHA1** | Optional | SHA1 | The SHA-1 hash of the acting process image file.  Example: `d55c5a4df19b46db8c54c801c4665d3338acdab0` |
| **ActingProcessSHA256** | Optional | SHA256 | The SHA-256 hash of the acting process image file.  Example: `e81bb824c4a09a811af17deae22f22dd``2e1ec8cbb00b22629d2899f7c68da274` |
| **ActingProcessSHA512** | Optional | SHA512 | The SHA-512 hash of the acting process image file. |
| **ActingProcessIMPHASH** | Optional | String | The Import Hash of all the library DLLs that are used by the acting process. |
| **ActingProcessCreationTime** | Optional | DateTime | The date and time when the acting process was started. |
| **ActingProcessTokenElevation** | Optional | String | A token indicating the presence or absence of User Access Control (UAC) privilege elevation applied to the acting process. Example: `None` |
| **ActingProcessFileSize** | Optional | Long | The size of the file that ran the acting process. |

### Parent process fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **ParentProcessName** | Optional | string | The name of the parent process. This name is commonly derived from the image or executable file that's used to define the initial code and data that's mapped into the process' virtual address space.Example: `C:\Windows\explorer.exe` |
| **ParentProcessFileCompany** | Optional | String | The name of the company that created the parent process image file.  Example: `Microsoft` |
| **ParentProcessFileDescription** | Optional | String | The description from the version information in the parent process image file. Example: `Notepad++ : a free (GPL) source code editor` |
| **ParentProcessFileProduct** | Optional | String | The product name from the version information in parent process image file.  Example: `Notepad++` |
| **ParentProcessFileVersion** | Optional | String | The product version from the version information in parent process image file.  Example: `7.9.5.0` |
| **ParentProcessIsHidden** | Optional | Boolean | An indication of whether the parent process is in hidden mode. |
| **ParentProcessInjectedAddress** | Optional | String | The memory address in which the responsible parent process is stored. |
| **ParentProcessId** | Recommended | String | The process ID (PID) of the parent process.  Example: `48610176` |
| **ParentProcessGuid** | Optional | String | A generated unique identifier (GUID) of the parent process. Enables identifying the process across systems.  Example: `EF3BD0BD-2B74-60C5-AF5C-010000001E00` |
| **ParentProcessIntegrityLevel** | Optional | String | Every process has an integrity level that is represented in its token. Integrity levels determine the process level of protection or access.  Windows defines the following integrity levels: **low**, **medium**, **high**, and **system**. Standard users receive a **medium** integrity level and elevated users receive a **high** integrity level.  For more information, see [Mandatory Integrity Control - Win32 apps](/en-us/windows/win32/secauthz/mandatory-integrity-control). |
| **ParentProcessMD5** | Optional | MD5 | The MD5 hash of the parent process image file. Example: `75a599802f1fa166cdadb360960b1dd0` |
| **ParentProcessSHA1** | Optional | SHA1 | The SHA-1 hash of the parent process image file.  Example: `d55c5a4df19b46db8c54c801c4665d3338acdab0` |
| **ParentProcessSHA256** | Optional | SHA256 | The SHA-256 hash of the parent process image file.  Example: `e81bb824c4a09a811af17deae22f22dd``2e1ec8cbb00b22629d2899f7c68da274` |
| **ParentProcessSHA512** | Optional | SHA512 | The SHA-512 hash of the parent process image file. |
| **ParentProcessIMPHASH** | Optional | String | The Import Hash of all the library DLLs that are used by the parent process. |
| **ParentProcessTokenElevation** | Optional | String | A token indicating the presence or absence of User Access Control (UAC) privilege elevation applied to the parent process.  Example: `None` |
| **ParentProcessCreationTime** | Optional | DateTime | The date and time when the parent process was started. |

### Target user fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **TargetUsername** | Mandatory for process create events. | Username (String) | The target username, including domain information when available. For the supported format for different ID types, refer to [the User entity](normalization-entity-user). Use the simple form only if domain information isn't available.Store the Username type in the TargetUsernameType field. If other username formats are available, store them in the fields `TargetUsername<UsernameType>`.Example: `AlbertE` |
| **TargetUsernameType** | Conditional | Enumerated | Specifies the type of the user name stored in the TargetUsername field. For a list of allowed values and further information refer to [UsernameType](normalization-entity-user#usernametype) in the [Schema Overview article](normalization-about-schemas).Example: `Windows` |
| **TargetUserId** | Recommended | String | A machine-readable, alphanumeric, unique representation of the target user. For the supported format for different ID types, refer to [the User entity](normalization-entity-user). Example: `S-1-12` |
| **TargetUserIdType** | Conditional | UserIdType | The type of the ID stored in the TargetUserId field. For a list of allowed values and further information refer to [UserIdType](normalization-entity-user#useridtype) in the [Schema Overview article](normalization-about-schemas). |
| **TargetUserSessionId** | Optional | String | The unique ID of the target user's login session. Example: `999`**Note**: The type is defined as *string* to support varying systems, but on Windows this value must be numeric. If you are using a Windows or Linux machine and used a different type, make sure to convert the values. For example, if you used a hexadecimal value, convert it to a decimal value. |
| **TargetUserSessionGuid** | Optional | String | The unique GUID of the target user's login session, as reported by the reporting device. Example: `{12345678-1234-1234-1234-123456789012}` |
| **TargetUserType** | Optional | UserType | The type of Actor. For a list of allowed values and further information refer to [UserType](normalization-entity-user#usertype) in the [Schema Overview article](normalization-about-schemas). **Note**: The value might be provided in the source record by using different terms, which should be normalized to these values. Store the original value in the TargetOriginalUserType field. |
| **TargetOriginalUserType** | Optional | String | The original destination user type, if provided by the reporting device. |
| **TargetUserScope** | Optional | String | The scope, such as Microsoft Entra tenant, in which TargetUserId and TargetUsername are defined. or more information and list of allowed values, see [UserScope](normalization-entity-user#userscope) in the [Schema Overview article](normalization-about-schemas). |
| **TargetUserScopeId** | Optional | String | The scope ID, such as Microsoft Entra Directory ID, in which TargetUserId and TargetUsername are defined. for more information and list of allowed values, see [UserScopeId](normalization-entity-user#userscopeid) in the [Schema Overview article](normalization-about-schemas). |

### Target process fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **TargetProcessName** | Mandatory | string | The name of the target process. This name is commonly derived from the image or executable file that's used to define the initial code and data that's mapped into the process' virtual address space.  Example: `C:\Windows\explorer.exe` |
| **TargetProcessFilename** | Optional | String | The file name part of the `TargetProcessName`, without folder information. Example: `explorer.exe` |
| **TargetProcessFileCompany** | Optional | String | The name of the company that created the target process image file.  Example: `Microsoft` |
| **TargetProcessFileDescription** | Optional | String | The description from the version information in the target process image file. Example: `Notepad++ : a free (GPL) source code editor` |
| **TargetProcessFileProduct** | Optional | String | The product name from the version information in target process image file.  Example: `Notepad++` |
| **TargetProcessFileSize** | Optional | Long | Size of the file that ran the process responsible for the event. |
| **TargetProcessFileVersion** | Optional | String | The product version from the version information in the target process image file.  Example: `7.9.5.0` |
| **TargetProcessFileInternalName** | Optional | String | The product internal file name from the version information of the image file of the target process. |
| **TargetProcessFileOriginalName** | Optional | String | The product original file name from the version information of the image file of the target process. |
| **TargetProcessIsHidden** | Optional | Boolean | An indication of whether the target process is in hidden mode. |
| **TargetProcessInjectedAddress** | Optional | String | The memory address in which the responsible target process is stored. |
| **TargetProcessMD5** | Optional | MD5 | The MD5 hash of the target process image file.  Example: `75a599802f1fa166cdadb360960b1dd0` |
| **TargetProcessSHA1** | Optional | SHA1 | The SHA-1 hash of the target process image file.  Example: `d55c5a4df19b46db8c54c801c4665d3338acdab0` |
| **TargetProcessSHA256** | Optional | SHA256 | The SHA-256 hash of the target process image file.  Example: `e81bb824c4a09a811af17deae22f22dd``2e1ec8cbb00b22629d2899f7c68da274` |
| **TargetProcessSHA512** | Optional | SHA512 | The SHA-512 hash of the target process image file. |
| **TargetProcessIMPHASH** | Optional | String | The Import Hash of all the library DLLs that are used by the target process. |
| **HashType** | Conditional | Enumerated | The type of hash stored in the HASH alias field, allowed values are `MD5`, `SHA`, `SHA256`, `SHA512` and `IMPHASH`. |
| **TargetProcessCommandLine** | Mandatory | String | The command line used to run the target process.  Example: `"choco.exe" -v` |
| **TargetProcessCurrentDirectory** | Optional | String | The current directory in which the target process is executed.  Example: `c:\windows\system32` |
| **TargetProcessCreationTime** | Recommended | DateTime | The product version from the version information of the target process image file. |
| **TargetProcessId** | Mandatory | String | The process ID (PID) of the target process. Example: `48610176`**Note**: The type is defined as *string* to support varying systems, but on Windows and Linux this value must be numeric. If you are using a Windows or Linux machine and used a different type, make sure to convert the values. For example, if you used a hexadecimal value, convert it to a decimal value. |
| **TargetProcessGuid** | Optional | GUID (String) | A generated unique identifier (GUID) of the target process. Enables identifying the process across systems.  Example: `EF3BD0BD-2B74-60C5-AF5C-010000001E00` |
| **TargetProcessIntegrityLevel** | Optional | String | Every process has an integrity level that is represented in its token. Integrity levels determine the process level of protection or access.  Windows defines the following integrity levels: **low**, **medium**, **high**, and **system**. Standard users receive a **medium** integrity level and elevated users receive a **high** integrity level.  For more information, see [Mandatory Integrity Control - Win32 apps](/en-us/windows/win32/secauthz/mandatory-integrity-control). |
| **TargetProcessTokenElevation** | Optional | String | Token type indicating the presence or absence of User Access Control (UAC) privilege elevation applied to the process that was created or terminated.  Example: `None` |
| **TargetProcessStatusCode** | Optional | String | The exit code returned by the target process when terminated. This field is valid only for process termination events. For consistency, the field type is string, even if value provided by the operating system is numeric. |

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
| **ThreatField** | Optional | String | The field for which a threat was identified. |
| **ThreatConfidence** | Optional | ConfidenceLevel (Integer) | The confidence level of the threat identified, normalized to a value between 0 and a 100. |
| **ThreatOriginalConfidence** | Optional | String | The original confidence level of the threat identified, as reported by the reporting device. |
| **ThreatIsActive** | Optional | Boolean | True if the threat identified is considered an active threat. |
| **ThreatFirstReportedTime** | Optional | datetime | The first time the IP address or domain were identified as a threat. |
| **ThreatLastReportedTime** | Optional | datetime | The last time the IP address or domain were identified as a threat. |

### Entity correlation fields

Note

Contributors don't need to populate these fields. Applicable parsers will populate them when internal Microsoft support is added.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **ActingProcessEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the acting process within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **ActorUserAdditionalIds** | Optional | Dynamic | For the field structure and usage, see [Fields suffixed with AdditionalIds](normalization-common-fields#fields-suffixed-with-additionalids). |
| **ActorUserEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the actor user within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **ParentProcessEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the parent process within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **TargetProcessEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the target process within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **TargetUserAdditionalIds** | Optional | Dynamic | For the field structure and usage, see [Fields suffixed with AdditionalIds](normalization-common-fields#fields-suffixed-with-additionalids). |
| **TargetUserEntityKey** | Optional | String | A stable, deterministic string identifier that uniquely identifies the target user within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |

## Schema updates

| Version | Changes |
| --- | --- |
| 0.1.1 | Added the field `EventSchema`. |
| 0.1.2 | Added the fields `ActorUserType`, `ActorOriginalUserType`, `TargetUserType`, `TargetOriginalUserType`, and `HashType`. |
| 0.1.3 | Changed the fields `ParentProcessId` and `TargetProcessCreationTime` from mandatory to recommended. |
| 0.1.4 | Added the fields `ActorScope`, `DvcScopeId`, and `DvcScope`. |
| 1.0.0 | Added entity correlation fields. |