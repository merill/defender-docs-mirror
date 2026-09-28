---
layout: Conceptual
title: The Advanced Security Information Model (ASIM) Alert Events normalization schema reference | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/normalization-schema-alert
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
description: This article displays the Microsoft Sentinel Alert Events normalization schema.
ms.author: edbaynash
author: EdB-MSFT
ms.topic: reference
ms.date: 2026-09-16T00:00:00.0000000Z
locale: en-us
document_id: c0e82d9e-e7bd-71ce-10a5-af4d0fc80d60
document_version_independent_id: c23ccc93-1269-92d1-8232-54dd46f2bc19
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/normalization-schema-alert.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/normalization-schema-alert
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/normalization-schema-alert.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: ea52595a-3cbb-b0e4-80d4-019837ad0476
---

# The Advanced Security Information Model (ASIM) Alert Events normalization schema reference | Microsoft Learn

The Microsoft Sentinel Alert Schema is designed to normalize security-related alerts from various products into a standardized format within Microsoft Advanced Security Information Model (ASIM). This schema focuses exclusively on security events, ensuring consistent and efficient analysis across different data sources.

The Alert Schema represents various types of security alerts, such as threats, suspicious activities, user behavior anomalies and compliance violations. These alerts are reported by different security products and systems, including but not limited to EDRs, antivirus software, intrusion detection systems, data loss prevention tools etc.

For more information about normalization in Microsoft Sentinel, see [Normalization and the Advanced Security Information Model (ASIM)](normalization).

## Parsers

For more information about ASIM parsers, see the [ASIM parsers overview](normalization-parsers-overview).

### Unifying Parsers

To use parsers that unify all ASIM out-of-the-box parsers and ensure that your analysis runs across all the configured sources, use the `_Im_AlertEvent` parser.

### Out-of-the-box, Source-specific Parsers

For the list of the Alert parsers Microsoft Sentinel provides out-of-the-box, refer to the [ASIM parsers list](normalization-parsers-list#alert-event-parsers).

### Add Your Own Normalized Parsers

When [developing custom parsers](normalization-develop-parsers) for the Alert information model, name your KQL functions using the following syntax:

- `vimAlertEvent<vendor><Product>` for parameterized parsers
- `ASimAlertEvent<vendor><Product>` for regular parsers

Refer to the article [Managing ASIM parsers](normalization-manage-parsers) to learn how to add your custom parsers to the alert unifying parsers.

### Filtering Parser Parameters

The Alert parsers support various [filtering parameters](normalization-about-parsers#optimizing-parsing-using-parameters) to improve query performance. These parameters are optional but can enhance your query performance. The following filtering parameters are available:

| Name | Type | Description |
| --- | --- | --- |
| **starttime** | datetime | Filter only alerts that started at or after this time. This parameter filters on the `TimeGenerated` field, which is the standard designator for the time of the event, regardless of the parser-specific mapping of the EventStartTime and EventEndTime fields. |
| **endtime** | datetime | Filter only alerts that started at or before this time. This parameter filters on the `TimeGenerated` field, which is the standard designator for the time of the event, regardless of the parser-specific mapping of the EventStartTime and EventEndTime fields. |
| **ipaddr\_has\_any\_prefix** | dynamic | Filter only alerts for which the **'DvcIpAddr'** field is in one of the listed values. |
| **hostname\_has\_any** | dynamic | Filter only alerts for which the **'DvcHostname'** field is in one of the listed values. |
| **username\_has\_any** | dynamic | Filter only alerts for which the **'Username'** field is in one of the listed values. |
| **attacktactics\_has\_any** | dynamic | Filter only alerts for which the **'AttackTactics'** field is in one of the listed values. |
| **attacktechniques\_has\_any** | dynamic | Filter only alerts for which the **'AttackTechniques'** field is in one of the listed values. |
| **threatcategory\_has\_any** | dynamic | Filter only alerts for which the **'ThreatCategory'** field is in one of the listed values. |
| **alertverdict\_has\_any** | dynamic | Filter only alerts for which the **'AlertVerdict'** field is in one of the listed values. |
| **eventseverity\_has\_any** | dynamic | Filter only alerts for which the **'EventSeverity'** field is in one of the listed values. |

## Schema Overview

The Alert Schema serves several types of security events, which share the same fields. These events are identified by the EventType field:

- **Threat Info**: Alerts related to various types of malicious activities such as malware, phishing, ransomware, and other cyber threats.
- **Suspicious Activities**: Alerts for activities that are not necessarily confirmed threats but are suspicious and warrant further investigation, such as multiple failed login attempts or access to restricted files.
- **User Behavior Anomalies**: Alerts indicating unusual or unexpected user behavior that might suggest a security issue, such as abnormal login times or unusual data access patterns.
- **Compliance Violations**: Alerts related to non-compliance with regulatory or internal policies. For example, a VM exposed with open public ports vulnerable to attacks (Cloud Security Alert).

Important

To preserve the relevance and effectiveness of the Alert Schema, only security-related alerts should be mapped.

Alert schema refers the following entities to capture details about the alert:

- **Dvc** fields are used to capture details about the host or Ip associated with the alert
- **User** fields are used to capture details about the user associated with the alert.
- Similarly **Process**, **File**, **Url**, **Registry** and **Email** fields are used to capture only key details about the process, file, Url, registry and email associated with the alert respectively.

Important

- When building a product-specific parser, use the ASIM Alert schema when the alert contains information about a security incident or potential threat, and the primary details can be mapped directly to available Alert schema fields. The Alert schema is ideal for capturing summary information without extensive entity-specific fields.
- However, if you find yourself placing essential fields in 'AdditionalFields' due to a lack of direct field matches, consider a more specialized schema. For example, if an alert includes network-related details such as multiple IP addresses e.g. SrcIpAdr, DstIpAddr, PortNumber etc. then you may opt for the NetworkSession schema over the Alert schema. Specialized schemas also provide dedicated fields for capturing threat-related information, enhancing data quality and facilitating efficient analysis.

## Schema Details

### Common ASIM Fields

The following list mentions fields that have specific guidelines for Alert events:

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **EventType** | Mandatory | Enumerated | Type of the event.Supported values are:-`Alert` |
| **EventSubType** | Recommended | Enumerated | Specifies the subtype or category of the alert event, providing more granular detail within the broader event classification. This field helps distinguish the nature of the detected issue, improving incident prioritization and response strategies.Supported values include:- `Threat` (Represents a confirmed or highly likely malicious activity that could compromise the system or network)- `Suspicious Activity` (Flags behavior or events that appear unusual or suspicious, though not yet confirmed as malicious)- `Anomaly` (Identifies deviations from normal patterns that could indicate a potential security risk or operational issue)- `Compliance Violation` (Highlights activities that breach regulatory, policy, or compliance standards) |
| **EventUid** | Mandatory | string | A machine-readable, alphanumeric string that uniquely identifies an alert within a system.  e.g. `A1bC2dE3fH4iJ5kL6mN7oP8qR9s` |
| **EventMessage** | Optional | string | Detailed information about the alert, including its context, cause, and potential impact.  e.g. `Potential use of the Rubeus tool for kerberoasting, a technique used to extract service account credentials from Kerberos tickets.` |
| **IpAddr** | Alias |  | Alias or friendly name for `DvcIpAddr` field. |
| **Hostname** | Alias |  | Alias or friendly name for `DvcHostname` field. |
| **EventSchema** | Mandatory | Enumerated | The schema used for the event. The schema documented here is `AlertEvent`. |
| **EventSchemaVersion** | Mandatory | SchemaVersion (String) | The version of the schema. The version of the schema documented here is `1.0.0`. |

### All Common Fields

Fields that appear in the table below are common to all ASIM schemas. Any guideline specified above overrides the general guidelines for the field. For example, a field might be optional in general, but mandatory for a specific schema. For more information on each field, refer to the [ASIM Common Fields](normalization-common-fields) article.

| Class | Fields |
| --- | --- |
| Mandatory | - [EventCount](normalization-common-fields#eventcount)- [EventStartTime](normalization-common-fields#eventstarttime)- [EventEndTime](normalization-common-fields#eventendtime)- [EventType](normalization-common-fields#eventtype)- [EventUid](normalization-common-fields#eventuid)- [EventProduct](normalization-common-fields#eventproduct)- [EventVendor](normalization-common-fields#eventvendor)- [EventSchema](normalization-common-fields#eventschema)- [EventSchemaVersion](normalization-common-fields#eventschemaversion) |
| Recommended | - [EventSubType](normalization-common-fields#eventsubtype)- [EventSeverity](normalization-common-fields#eventseverity)- [DvcIpAddr](normalization-common-fields#dvcipaddr)- [DvcHostname](normalization-common-fields#dvchostname)- [DvcDomain](normalization-common-fields#dvcdomain)- [DvcDomainType](normalization-common-fields#dvcdomaintype)- [DvcFQDN](normalization-common-fields#dvcfqdn)- [DvcId](normalization-common-fields#dvcid)- [DvcIdType](normalization-common-fields#dvcidtype) |
| Optional | - [EventMessage](normalization-common-fields#eventmessage)- [EventOriginalType](normalization-common-fields#eventoriginaltype)- [EventOriginalSubType](normalization-common-fields#eventoriginalsubtype)- [EventOriginalSeverity](normalization-common-fields#eventoriginalseverity)- [EventProductVersion](normalization-common-fields#eventproductversion) - [EventOriginalUid](normalization-common-fields#eventoriginaluid)- [EventReportUrl](normalization-common-fields#eventreporturl)- [EventResult](normalization-common-fields#eventresult)- [EventOwner](normalization-common-fields#eventowner)- [DvcZone](normalization-common-fields#dvczone)- [DvcMacAddr](normalization-common-fields#dvcmacaddr)- [DvcOs](normalization-common-fields#dvcos)- [DvcOsVersion](normalization-common-fields#dvchostname)- [DvcAction](normalization-common-fields#dvcaction)- [DvcOriginalAction](normalization-common-fields#dvcoriginalaction)- [DvcInterface](normalization-common-fields#dvcinterface)- [AdditionalFields](normalization-common-fields#additionalfields)- [DvcDescription](normalization-common-fields#dvcdescription)- [DvcScopeId](normalization-common-fields#dvcscopeid)- [DvcScope](normalization-common-fields#dvcscope) |

### Inspection Fields

The following table covers fields that provide critical insights into the rules and threats associated with alerts. Together, they help enrich the context of the alert, making it easier for security analysts to understand its origin and significance.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **AlertId** | Alias | string | Alias or friendly name for `EventUid` field. |
| **AlertName** | Recommended | string | Title or name of the alert.e.g. `Possible use of the Rubeus kerberoasting tool` |
| **AlertDescription** | Alias | string | Alias or friendly name for `EventMessage` field. |
| **AlertVerdict** | Optional | Enumerated | The final determination or outcome of the alert, indicating whether the alert was confirmed as a threat, deemed suspicious, or resolved as a false positive.Supported values are:- `True Positive` (Confirmed as a legitimate threat)- `False Positive` (Incorrectly identified as a threat)- `Benign Positive` (when event is determined to be harmless)- `Unknown` (Uncertain or undetermined status) |
| **AlertStatus** | Optional | Enumerated | Indicates the current state or progress of the alert.Supported values are:- `Active`- `Closed` |
| **AlertOriginalStatus** | Optional | string | The status of the alert as reported by the originating system. |
| **DetectionMethod** | Optional | Enumerated | Provides detailed information about the specific detection method, technology, or data source that contributed to the generation of the alert. This field offers greater insight into how the alert was detected or triggered, aiding in the understanding of the detection context and reliability.Supported values include:- `EDR`: Endpoint Detection and Response systems that monitor and analyze endpoint activities to identify threats.- `Behavioral Analytics`: Techniques that detect abnormal patterns in user, device, or system behavior.- `Reputation`: Threat detection based on the reputation of IP addresses, domains, or files.- `Threat Intelligence`: External or internal intelligence feeds providing data on known threats or adversary tactics.- `Intrusion Detection`: Systems that monitor network traffic or activities for signs of intrusions or attacks.- `Automated Investigation`: Automated systems that analyze and investigate alerts, reducing manual workload.- `Antivirus`: Traditional antivirus engines that detect malware based on signatures and heuristics.- `Data Loss Prevention`: Solutions focused on preventing unauthorized data transfers or leaks.- `User Defined Blocked List`: Custom lists defined by users to block specific IPs, domains, or files.- `Cloud Security Posture Management`: Tools that assess and manage security risks in cloud environments.- `Cloud Application Security`: Solutions that secure cloud applications and data.-`Scheduled Alerts`: Alerts generated based on predefined schedules or thresholds.- `Other`: Any other detection method not covered by the above categories. |
| **Rule** | Alias | string | Either the value of RuleName or the value of RuleNumber. If the value of RuleNumber is used, the type should be converted to string. |
| **RuleNumber** | Optional | int | The number of the rule associated with the alert.e.g. `123456` |
| **RuleName** | Optional | string | The name or ID of the rule associated with the alert.e.g. `Server PSEXEC Execution via Remote Access` |
| **RuleDescription** | Optional | string | Description of the rule associated with the alert.e.g. `This rule detects remote execution on a server using PSEXEC, which may indicate unauthorized administrative activity or lateral movement within the network` |
| **ThreatId** | Optional | string | The ID of the threat or malware identified in the alert. e.g. `1234567891011121314` |
| **ThreatName** | Optional | string | The name of the threat or malware identified in the alert. e.g. `Init.exe` |
| **ThreatFirstReportedTime** | Optional | datetime | Date and time when the threat was first reported. e.g. `2024-09-19T10:12:10.0000000Z` |
| **ThreatLastReportedTime** | Optional | datetime | Date and time when the threat was last reported. e.g. `2024-09-19T10:12:10.0000000Z` |
| **ThreatCategory** | Recommended | Enumerated | The category of the threat or malware identified in the alert.Supported values are: `Malware`, `Ransomware`, `Trojan`, `Virus`, `Worm`, `Adware`, `Spyware`, `Rootkit`, `Cryptominer`, `Phishing`, `Spam`, `MaliciousUrl`, `Spoofing`, `Security Policy Violation`, `Unknown` |
| **ThreatOriginalCategory** | Optional | string | The category of the threat as reported by the originating system. |
| **ThreatIsActive** | Optional | bool | Indicates whether the threat is currently active.Supported values are: `True`, `False` |
| **ThreatRiskLevel** | Optional | RiskLevel (Integer) | The risk level associated with the threat. The level should be a number between 0 and 100.**Note**: The value might be provided in the source record by using a different scale, which should be normalized to this scale. The original value should be stored in ThreatRiskLevelOriginal. |
| **ThreatOriginalRiskLevel** | Optional | string | The risk level as reported by the originating system. |
| **ThreatConfidence** | Optional | ConfidenceLevel (Integer) | The confidence level of the threat identified, normalized to a value between 0 and a 100. |
| **ThreatOriginalConfidence** | Optional | string | The confidence level as reported by the originating system. |
| **IndicatorType** | Recommended | Enumerated | The type or category of the indicatorSupported values are:-`Ip`-`User`-`Process`-`Registry`-`Url`-`Host`-`Cloud Resource`-`Application`-`File`-`Email`-`Mailbox`-`Logon Session` |
| **IndicatorAssociation** | Optional | Enumerated | Specifies whether the indicator is linked to or directly impacted by the threat.Supported values are:-`Associated`-`Targeted` |
| **AttackTactics** | Recommended | string | The attack tactics (name, ID, or both) associated with the alert. Preferred format:e.g: `Persistence, Privilege Escalation` |
| **AttackTechniques** | Recommended | string | The attack techniques (name, ID, or both) associated with the alert.  Preferred format:e.g: `Local Groups (T1069.001), Domain Groups (T1069.002)` |
| **AttackRemediationSteps** | Recommended | string | Recommended actions or steps to mitigate or remediate the identified attack or threat.  e.g.`1. Make sure the machine is completely updated and all your software has the latest patch.``2. Contact your incident response team.` |

### User Fields

This section defines fields related to the identification and classification of users associated with an alert, providing clarity on the impacted user and the format of their identity. If the alert contains additional, multiple user-related fields that exceed what is mapped here, you may consider whether a specialized schema, such as the Authentication Event schema, may be more appropriate to fully represent the data.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **UserId** | Optional | string | A machine-readable, alphanumeric, unique representation of the user associated with the alert.e.g. `A1bC2dE3fH4iJ5kL6mN7o` |
| **UserIdType** | Conditional | Enumerated | The type of the user ID, such as `GUID`, `SID`, or `Email`.Supported values are:- `GUID`- `SID`- `Email`- `Username`- `Phone`- `Other` |
| **Username** | Recommended | Username (string) | Name of the user associated with the alert, including domain information when available.e.g. `Contoso\JSmith` or `john.smith@contoso.com` |
| **User** | Alias | string | Alias or friendly name for `Username` field. |
| **UsernameType** | Conditional | UsernameType | Specifies the type of the user name stored in the `Username` field. For more information, and list of allowed values, see [UsernameType](normalization-entity-user#usernametype) in the [Schema Overview article](normalization-about-schemas).e.g. `Windows` |
| **UserType** | Optional | UserType | The type of the Actor. For more information, and list of allowed values, see [UserType](normalization-entity-user#usertype) in the [Schema Overview article](normalization-about-schemas). e.g. `Guest` |
| **OriginalUserType** | Optional | string | The user type as reported by the reporting device. |
| **UserSessionId** | Optional | string | The unique ID of the user's session associated with the alert.e.g. `a1bc2de3-fh4i-j5kl-6mn7-op8qr9st0u` |
| **UserScopeId** | Optional | string | The scope ID, such as Microsoft Entra Directory ID, in which UserId and Username are defined.e.g. `a1bc2de3-fh4i-j5kl-6mn7-op8qrs` |
| **UserScope** | Optional | string | The scope, such as Microsoft Entra tenant, in which UserId and Username are defined. For more information and list of allowed values, see [UserScope](normalization-entity-user#userscope) in the [Schema Overview article](normalization-about-schemas).e.g. `Contoso Directory` |

### Process Fields

This section allows you to capture details related to a process entity involved in an alert using the specified fields. If the alert contains additional, detailed process-related fields that exceed what is mapped here, you may consider whether a specialized schema, such as the Process Event schema, may be more appropriate to fully represent the data.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **ProcessId** | Optional | string | The process ID (PID) associated with the alert.e.g. `12345678` |
| **ProcessCommandLine** | Optional | string | Command line used to start the process.e.g. `"choco.exe" -v` |
| **ProcessName** | Optional | string | Name of the process.e.g. `C:\Windows\explorer.exe` |
| **ProcessFileCompany** | Optional | string | Company that created the process image file.e.g. `Microsoft` |

### File Fields

This section enables you to capture details related to a file entity involved in an alert. If the alert contains additional, detailed file-related fields that exceed what is mapped here, you may consider whether a specialized schema, such as the File Event schema, may be more appropriate to fully represent the data.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **FileName** | Optional | string | Name of the file associated with the alert, without path or a location.e.g. `Notepad.exe` |
| **FilePath** | Optional | string | The full, normalized path of the target file, including the folder or location, the file name, and the extension.e.g. `C:\Windows\System32\notepad.exe` |
| **FileSHA1** | Optional | string | SHA1 hash of the file.e.g. `j5kl6mn7op8qr9st0uv1` |
| **FileSHA256** | Optional | string | SHA256 hash of the file.e.g. `a1bc2de3fh4ij5kl6mn7op8qrs2de3` |
| **FileMD5** | Optional | string | MD5 hash of the file.e.g. `j5kl6mn7op8qr9st0uv1wx2yz3ab4c` |
| **FileSize** | Optional | long | Size of the file in bytes.e.g. `123456` |

### Url Field

If your alert includes information about Url entity, the following fields can capture URL-related data.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **Url** | Optional | string | The URL string captured in the alert.e.g. `https://contoso.com/fo/?k=v&amp;q=u#f` |

### Registry Fields

If your alert includes details about registry entity, use the following fields to capture specific registry-related information.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **RegistryKey** | Optional | string | The registry key associated with the alert, normalized to standard root key naming conventions.e.g. `HKEY_LOCAL_MACHINE\SOFTWARE\MTG` |
| **RegistryValue** | Optional | string | Registry value.e.g. `ImagePath` |
| **RegistryValueData** | Optional | string | Data of the registry value.e.g. `C:\Windows\system32;C:\Windows;` |
| **RegistryValueType** | Optional | Enumerated | Type of the registry value.e.g. `Reg_Expand_Sz` |

### Email Fields

If your alert includes information about email entity, use the following fields to capture specific email-related details.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **EmailMessageId** | Optional | string | Unique identifier for the email message, associated with the alert.e.g. `Request for Invoice Access` |
| **EmailSubject** | Optional | string | Subject of the email.e.g. `j5kl6mn7-op8q-r9st-0uv1-wx2yz3ab4c` |

### Entity correlation fields

Note

Contributors don't need to populate these fields. Applicable parsers will populate them when internal Microsoft support is added.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **FileEntityKey** | Optional | string | A stable, deterministic string identifier that uniquely identifies the file within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **ProcessEntityKey** | Optional | string | A stable, deterministic string identifier that uniquely identifies the process within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |
| **UserAdditionalIds** | Optional | dynamic | For the field structure and usage, see [Fields suffixed with AdditionalIds](normalization-common-fields#fields-suffixed-with-additionalids). |
| **UserEntityKey** | Optional | string | A stable, deterministic string identifier that uniquely identifies the user within a single namespace. This system-wide unique identifier enables correlation with entities in other events and entity inventories. |

## Schema updates

| Version | Changes |
| --- | --- |
| 0.1 | Initial release. |
| 1.0.0 | Added entity correlation fields. |