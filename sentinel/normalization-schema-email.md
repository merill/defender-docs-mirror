---
layout: Conceptual
title: Microsoft Sentinel ASIM Email Event normalization schema reference | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/normalization-schema-email
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
description: Learn how the Microsoft Sentinel ASIM Email Event normalization schema represents email delivery, inspection, authentication, and threat data.
author: derricklee
ms.author: derricklee
ms.topic: reference
ai-usage: ai-assisted
ms.date: 2026-09-10T00:00:00.0000000Z
locale: en-us
document_id: e8f42407-3ba4-1d59-80a7-d4689f400607
document_version_independent_id: b31c25b5-ffab-a542-4dbf-13fdd6537228
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/normalization-schema-email.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/normalization-schema-email
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/normalization-schema-email.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 63c3dde4-8292-7f85-e544-3db0bba0814c
---

# Microsoft Sentinel ASIM Email Event normalization schema reference | Microsoft Learn

The Microsoft Sentinel Email Event normalization schema represents email delivery and inspection activity. It includes message addressing and routing details, email authentication results, delivery outcomes, and threats identified in email messages.

Use the Email Event schema to normalize records from mail servers, secure email gateways, email security services, and other systems that process or inspect email. Normalization lets you analyze these records with consistent field names and values, regardless of the source.

For more information about normalization in Microsoft Sentinel, see [Normalization and the Advanced Security Information Model (ASIM)](normalization).

## Schema overview

The main fields of an email event describe:

- The email activity, represented by EventType and EventSubType.
- The sender and recipients, represented by EmailFromAddress, EmailToRecipients, EmailCCRecipients, and EmailBCCRecipients.
- The message, represented by fields such as EmailSubject, EmailSizeBytes, EmailFiles, and EmailUrls.
- Email authentication, represented by the SPF, DKIM, and DMARC fields.
- The delivery outcome, represented by DvcAction, EmailDeliveryLocation, [EventResult](normalization-common-fields#eventresult), and EventResultDetails.
- Threats and inspection rules associated with the message, represented by the inspection fields.

The `Dvc` fields describe the reporting or inspecting system.

## Parsers

### Deploy and use email event parsers

Deploy ASIM parsers from the [Microsoft Sentinel GitHub repository](https://aka.ms/DeployASIM). To query all normalized email event sources, use the unifying parser `_Im_EmailEvent` as the table name in your query.

For more information about using ASIM parsers, see the [ASIM parsers overview](normalization-parsers-overview).

### Add your own normalized parsers

When you implement custom parsers for the Email Event information model, use the following naming syntax:

- `ASimEmailEvent<vendor><Product>` for regular parsers.
- `vimEmailEvent<vendor><Product>` for parameterized parsers.

To add custom parsers to the Email Event unifying parser, see [Manage ASIM parsers](normalization-manage-parsers).

### Filter parser results

The Email Event filtering parser supports [filtering parameters](normalization-about-parsers#optimizing-parsing-using-parameters) to improve query performance.

| Name | Type | Description |
| --- | --- | --- |
| **starttime** | datetime | Filter events that started at or after this time. |
| **endtime** | datetime | Filter events that ended at or before this time. |
| **ipaddr\_has\_any\_prefix** | dynamic | Filter events for which an IP address starts with one of the listed prefixes. |
| **emailfromaddress\_has\_any** | dynamic | Filter events for which `EmailFromAddress` contains one of the listed values. |
| **emailrecipient\_has\_any** | dynamic | Filter events that have one of the listed email recipients. |
| **emailsubject\_has\_any** | dynamic | Filter events for which `EmailSubject` contains one of the listed values. |
| **emaildirection\_in** | dynamic | Filter events for which `EmailDirection` is one of the listed values. |
| **emaildeliverylocation\_in** | dynamic | Filter events for which `EmailDeliveryLocation` is one of the listed values. |
| **eventresult** | String | Filter events for which `EventResult` equals the specified value. The default value, `*`, doesn't filter by result. |
| **pack** | Boolean | When set to `true`, pack unmapped source fields into the `AdditionalFields` dynamic field. The default is `false`. |

For example, use the following query to return inbound email sent by addresses that contain `contoso.com` during the last day:

```kusto
_Im_EmailEvent(starttime=ago(1d),endtime=now(),emailfromaddress_has_any=dynamic(['contoso.com']),emaildirection_in=dynamic(['Inbound'])
)
```

## Schema details

### Common ASIM fields

Important

Fields common to all schemas are described in detail in [ASIM common fields](normalization-common-fields). Guidelines in this article override the general guidelines for a field.

#### Common fields with specific guidelines

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **EventType** | Mandatory | Enumerated | Describes the normalized email activity. Allowed values are `EmailDelivery` and `EmailInspection`. |
| **EventSubType** | Optional | Enumerated | Provides more detail about the email activity. Allowed values are `EmailSent` and `EmailReceived`. |
| **EventSchema** | Mandatory | Enumerated | The schema name is `EmailEvent`. |
| **EventSchemaVersion** | Mandatory | SchemaVersion (String) | The version of the schema. The version documented here is `1.0.0`. |
| **EventResultDetails** | Recommended | Enumerated | Provides details about the result. Allowed values are `InvalidAddress`, `MailboxFull`, `MessageTooLarge`, `MessageRateLimitExceeded`, `RecipientRateLimitExceeded`, `BlockedByPolicy`, `BlockedBySpamFilter`, `PhishingDetected`, `MalwareDetected`, and `Other`. |
| **EventSeverity** | Recommended | Enumerated | The event severity. Allowed values are `Informational`, `Low`, `Medium`, and `High`. |

#### All common fields

| Class | Fields |
| --- | --- |
| Mandatory | - [EventCount](normalization-common-fields#eventcount)- [EventStartTime](normalization-common-fields#eventstarttime)- [EventEndTime](normalization-common-fields#eventendtime)- EventType- [EventResult](normalization-common-fields#eventresult)- [EventProduct](normalization-common-fields#eventproduct)- [EventVendor](normalization-common-fields#eventvendor)- [EventSchema](normalization-common-fields#eventschema)- [EventSchemaVersion](normalization-common-fields#eventschemaversion)- [Dvc](normalization-common-fields#dvc) |
| Recommended | - EventResultDetails- [EventSeverity](normalization-common-fields#eventseverity)- [EventUid](normalization-common-fields#eventuid)- [DvcIpAddr](normalization-common-fields#dvcipaddr)- [DvcHostname](normalization-common-fields#dvchostname)- [DvcDomain](normalization-common-fields#dvcdomain) |
| Optional | - [EventMessage](normalization-common-fields#eventmessage)- EventSubType- [EventOriginalUid](normalization-common-fields#eventoriginaluid)- [EventOriginalType](normalization-common-fields#eventoriginaltype)- [EventOriginalResultDetails](normalization-common-fields#eventoriginalresultdetails)- [EventOriginalSeverity](normalization-common-fields#eventoriginalseverity)- [EventProductVersion](normalization-common-fields#eventproductversion)- [EventReportUrl](normalization-common-fields#eventreporturl)- [EventOwner](normalization-common-fields#eventowner)- [DvcDescription](normalization-common-fields#dvcdescription)- [DvcFQDN](normalization-common-fields#dvcfqdn)- [DvcId](normalization-common-fields#dvcid)- [DvcInterface](normalization-common-fields#dvcinterface)- [DvcMacAddr](normalization-common-fields#dvcmacaddr)- [DvcOriginalAction](normalization-common-fields#dvcoriginalaction)- [DvcOs](normalization-common-fields#dvcos)- [DvcOsVersion](normalization-common-fields#dvcosversion)- [DvcScope](normalization-common-fields#dvcscope)- [DvcScopeId](normalization-common-fields#dvcscopeid)- [DvcZone](normalization-common-fields#dvczone)- [AdditionalEntities](normalization-common-fields)- [AdditionalFields](normalization-common-fields#additionalfields) |
| Conditional | - [DvcDomainType](normalization-common-fields#dvcdomaintype)- [DvcIdType](normalization-common-fields#dvcidtype) |

### Email fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **EmailFromAddress** | Recommended | String | The email address in the message `From` header. |
| **EmailFromDomain** | Optional | String | The domain from the address in the message `From` header. |
| **EmailMailFromAddress** | Optional | String | The envelope sender address used by the mail transport protocol. |
| **EmailMailFromDomain** | Optional | String | The domain of the envelope sender address. |
| **EmailReplyToAddress** | Recommended | String | The email address in the message `Reply-To` header. |
| **EmailReplyToDomain** | Optional | String | The domain from the address in the message `Reply-To` header. |
| **EmailToRecipients** | Recommended | Dynamic | An array of recipients in the message `To` header. |
| **EmailCCRecipients** | Optional | Dynamic | An array of recipients in the message `Cc` header. |
| **EmailBCCRecipients** | Optional | Dynamic | An array of recipients in the message `Bcc` header. |
| **EmailSubject** | Recommended | String | The email subject. |
| **EmailLanguage** | Optional | String | The language of the email content, as reported by the source. |
| **EmailSizeBytes** | Recommended | Long | The total email size in bytes. |
| **EmailProtocolName** | Recommended | Enumerated | The protocol used to transfer or retrieve the email. Allowed values are `SMTP`, `IMAP`, and `POP3`. |
| **EmailDirection** | Recommended | Enumerated | The direction of the email relative to the reporting environment. Allowed values are `Inbound`, `Outbound`, `Internal`, `Local`, and `Unknown`. |
| **EmailDeliveryLocation** | Optional | Enumerated | The normalized location where the email was delivered. Allowed values are `Inbox`, `Junk`, `Quarantine`, and `DeletedItems`. |
| **EmailOriginalDeliveryLocation** | Optional | String | The delivery location as reported by the source. |
| **EmailFileCount** | Recommended | Integer | The number of files attached to the email. |
| **EmailFiles** | Optional | Dynamic | An array that describes files attached to the email. |
| **EmailUrlCount** | Recommended | Integer | The number of URLs found in the email. |
| **EmailUrls** | Optional | Dynamic | An array of URLs found in the email. |

### Email authentication fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **EmailSpfResult** | Optional | Enumerated | The normalized Sender Policy Framework (SPF) result. Allowed values are `Pass`, `Fail`, `SoftFail`, `Neutral`, `None`, `TemporaryError`, and `PermanentError`. |
| **EmailSpfOriginalResult** | Optional | String | The SPF result as reported by the source. |
| **EmailDkimDomain** | Optional | String | The domain that signed the message with DomainKeys Identified Mail (DKIM). |
| **EmailDkimSignature** | Optional | String | The DKIM signature associated with the message. |
| **EmailDkimResult** | Optional | Enumerated | The normalized DKIM result. Allowed values are `Pass`, `Fail`, `TemporaryError`, `PermanentError`, and `None`. |
| **EmailDkimOriginalResult** | Optional | String | The DKIM result as reported by the source. |
| **EmailDmarcResult** | Optional | Enumerated | The normalized Domain-based Message Authentication, Reporting, and Conformance (DMARC) result. Allowed values are `Pass`, `Fail`, `BestGuessPass`, and `None`. |
| **EmailDmarcOriginalResult** | Optional | String | The DMARC result as reported by the source. |
| **EmailDmarcPolicy** | Optional | Enumerated | The DMARC policy applied to the email. Allowed values are `Quarantine`, `Reject`, and `None`. |
| **EmailDmarcOverride** | Optional | Enumerated | The reason the DMARC policy was overridden. Allowed values are `Forwarded`, `LocalPolicy`, `MailingList`, `SampleOut`, `TrustedForwarder`, and `Other`. |

### Delivery and destination fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **DvcAction** | Optional | Enumerated | The normalized action taken on the email. Allowed values are `Delivered`, `Modified`, `Redirected`, `Blocked`, `Quarantined`, `Deleted`, `Purged`, and `NA`. |
| **Dst** | Mandatory | String | A unique identifier for the email destination. |
| **DstIpAddr** | Recommended | IP address | The IP address of the email destination. |

### Source system fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **Src** | Recommended | String | A unique identifier for the source system. |
| **SrcIpAddr** | Optional | IP address | The source IP address. |
| **IpAddr** | Alias | IP address | Alias to SrcIpAddr. |
| **SrcHostname** | Recommended | Hostname | The source device hostname, excluding domain information. |
| **SrcDomain** | Recommended | Domain | The domain of the source device. |
| **SrcDomainType** | Conditional | Enumerated | The type of `SrcDomain`. Allowed values are `Windows`, `FQDN`, and `ResourceGroup`. Required when `SrcDomain` is used. |
| **SrcFQDN** | Optional | FQDN | The fully qualified domain name of the source device. |
| **SrcDvcId** | Optional | String | The ID of the source device. |
| **SrcDvcIdType** | Conditional | Enumerated | The type of `SrcDvcId`. Allowed values are `AzureResourceId`, `MDEid`, `MD4IoTid`, `VMConnectionId`, `AwsVpcId`, `VectraId`, `ForcepointId`, `AppGateId`, and `Other`. Required when `SrcDvcId` is used. |
| **SrcDvcScope** | Optional | String | The cloud platform scope to which the source device belongs. |
| **SrcDvcScopeId** | Optional | String | The ID of the cloud platform scope to which the source device belongs. |
| **SrcDeviceType** | Optional | Enumerated | The source device type. |
| **SrcDescription** | Optional | String | A description of the source device. |
| **SrcIsp** | Optional | String | The internet service provider associated with the source IP address. |
| **SrcGeoCountry** | Optional | String | The country or region associated with the source IP address. |
| **SrcGeoRegion** | Optional | String | The region associated with the source IP address. |
| **SrcGeoCity** | Optional | String | The city associated with the source IP address. |
| **SrcGeoLatitude** | Optional | Real | The latitude associated with the source IP address. |
| **SrcGeoLongitude** | Optional | Real | The longitude associated with the source IP address. |

### Source user fields

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **SrcUserName** | Optional | String | The source user's name. |
| **User** | Alias | String | Alias to `SrcUserName`. |
| **SrcUserUpn** | Recommended | String | The source user's User Principal Name (UPN). |
| **SrcUserId** | Optional | String | A machine-readable identifier for the source user. |
| **SrcUserIdType** | Optional | Enumerated | The type of `SrcUserId`. Allowed values are `SID`, `UID`, `AADID`, `OktaId`, `AWSId`, `PUID`, `SalesforceId`, `VectraUserId`, `MD4IoTid`, and `Other`. |
| **SrcUsernameType** | Optional | Enumerated | The type of the value in `SrcUserName`. |
| **SrcUserScope** | Optional | String | The scope in which the source user is defined. |
| **SrcUserScopeId** | Optional | String | The ID of the scope in which the source user is defined. |

### Inspection fields

The following fields describe the rule, threat, or indicator associated with email inspection.

| Field | Class | Type | Description |
| --- | --- | --- | --- |
| **RuleName** | Optional | String | The name or ID of the inspection rule. |
| **RuleNumber** | Optional | Integer | The numeric ID of the inspection rule. |
| **Rule** | Alias | String | Alias to `RuleName`. |
| **RuleDescription** | Optional | String | A description of the inspection rule. |
| **IndicatorType** | Optional | Enumerated | The type of indicator identified in the email event. |
| **IndicatorAssociation** | Optional | Enumerated | The association between the indicator and the email event. |
| **ThreatId** | Optional | String | The ID of the threat identified in the email. |
| **ThreatName** | Optional | String | The name of the threat identified in the email. |
| **ThreatCategory** | Optional | String | The normalized threat category. |
| **ThreatOriginalCategory** | Optional | String | The threat category as reported by the source. |
| **ThreatRiskLevel** | Optional | RiskLevel (Integer) | The normalized threat risk level, from `0` through `100`. |
| **ThreatOriginalRiskLevel** | Optional | String | The threat risk level as reported by the source. |
| **ThreatConfidence** | Optional | ConfidenceLevel (Integer) | The normalized confidence level, from `0` through `100`. |
| **ThreatOriginalConfidence** | Optional | String | The threat confidence as reported by the source. |
| **ThreatIsActive** | Optional | Boolean | Indicates whether the identified threat is active. |
| **ThreatFirstReportedTime** | Optional | Datetime | The first time the threat was reported. |
| **ThreatLastReportedTime** | Optional | Datetime | The last time the threat was reported. |
| **ThreatIpAddr** | Optional | IP address | An IP address associated with the identified threat. |
| **ThreatField** | Conditional | Enumerated | The field for which the threat was identified. |
| **AttackTactics** | Optional | String | The MITRE ATT&CK tactics associated with the email event. |
| **AttackTechniques** | Optional | String | The MITRE ATT&CK techniques associated with the email event. |
| **AttackRemediationSteps** | Optional | String | Recommended steps to remediate the identified attack or threat. |

## Schema updates

Version `1.0.0` is the initial release of the Email Event schema.