---
layout: Conceptual
title: Data tables in the Microsoft Defender XDR advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-schema-tables
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about the tables in the advanced hunting schema to understand the data you can run threat hunting queries on.
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.custom:
- cx-ti
- cx-ah
- msecd-doc-authoring-1018
ms.topic: reference
ms.date: 2026-07-27T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 5ea94a55-ae13-98b1-1ded-bee037019f7a
document_version_independent_id: 5ea94a55-ae13-98b1-1ded-bee037019f7a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-schema-tables.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-schema-tables
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-schema-tables.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: dc25ecc3-7937-c18f-2325-c792835e763b
---

# Data tables in the Microsoft Defender XDR advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

The [advanced hunting](advanced-hunting-overview) schema is made up of multiple tables that provide either event information or information about devices, alerts, identities, and other entity types. To effectively build queries that span multiple tables, you need to understand the tables and the columns in the advanced hunting schema.

Microsoft Sentinel also ingests data from some of these tables through data connectors. For more information, see [Stream data from Microsoft Defender XDR to Microsoft Sentinel in the Azure portal](/en-us/azure/sentinel/connect-microsoft-365-defender).

## Get schema information

While constructing queries, use the built-in schema reference to quickly get the following information about each table in the schema:

- **Tables description**—type of data contained in the table and the source of that data.
- **Columns**—all the columns in the table.
- **Action types**—possible values in the `ActionType` column representing the event types supported by the table. This information is provided only for tables that contain event information.
- **Sample query**—example queries that feature how the table can be utilized.

### Access the schema reference

To quickly access the schema reference, select the **View reference** action next to the table name in the schema representation. You can also select **Schema reference** to search for a table.

[![The Schema Reference page on the Advanced Hunting page in the Microsoft Defender portal](/en-us/defender/media/understand-schema-1.png)](/en-us/defender/media/understand-schema-1.png#lightbox)

## Learn the schema tables

The following reference lists all the tables in the schema. Each table name links to a page describing the column names for that table. Table and column names are also listed in Microsoft Defender XDR as part of the schema representation on the advanced hunting screen.

| Table name | Description |
| --- | --- |
| **[AADSignInEventsBeta](advanced-hunting-aadsignineventsbeta-table)** | Microsoft Entra interactive and non-interactive sign-ins |
| **[AADSpnSignInEventsBeta](advanced-hunting-aadspnsignineventsbeta-table)** | Microsoft Entra service principal and managed identity sign-ins |
| **[AgentsInfo](advanced-hunting-agentsinfo-table)** (Preview) | Information about AI agents and their properties from various platforms |
| **[AIAgentsInfo](advanced-hunting-aiagentsinfo-table)** (Preview) | Information about AI agents created with Microsoft Copilot Studio, including agent configuration and ownership details |
| **[AlertEvidence](advanced-hunting-alertevidence-table)** | Files, IP addresses, URLs, users, or devices associated with alerts |
| **[AlertInfo](advanced-hunting-alertinfo-table)** | Alerts from Microsoft Defender for Endpoint, Microsoft Defender for Office 365, Microsoft Defender for Cloud Apps, and Microsoft Defender for Identity, including severity information and threat categorization |
| **[BehaviorEntities](advanced-hunting-behaviorentities-table)** (Preview) | Entities (file, process, device, user, and others) that are involved in a behavior in Microsoft Defender for Cloud Apps (not available for GCC) and User and Entity Behavior Analytics (UEBA) |
| **[BehaviorInfo](advanced-hunting-behaviorinfo-table)** (Preview) | Behaviors from Microsoft Defender for Cloud Apps (not available for GCC) and User and Entity Behavior Analytics (UEBA) |
| **[CallActivityEvents](advanced-hunting-callactivityevents-table)** | Activities performed during Microsoft Teams calls in your organization |
| **[CampaignInfo](advanced-hunting-campaigninfo-table)** (Preview) | Email campaigns identified by Microsoft Defender for Office 365 |
| **[CloudAppEvents](advanced-hunting-cloudappevents-table)** | Events involving accounts and objects in Office 365 and other cloud apps and services |
| **[CloudAuditEvents](advanced-hunting-cloudauditevents-table)** | Cloud audit events for various cloud platforms protected by the organization's Microsoft Defender for Cloud |
| **[CloudDnsEvents](advanced-hunting-clouddnsevents-table)** | DNS activity events from cloud infrastructure environments |
| **[CloudPolicyEnforcementEvents](advanced-hunting-cloudpolicyenforcementevents-table)** (Preview) | Policy enforcement evaluation decisions and metadata of security gating events for various cloud platforms protected by the organization's Microsoft Defender for Cloud |
| **[CloudProcessEvents](advanced-hunting-cloudprocessevents-table)** (Preview) | Cloud process events for various cloud platforms protected by the organization's Microsoft Defender for Containers |
| **[CloudStorageAggregatedEvents](advanced-hunting-cloudstorageaggregatedevents-table)** (Preview) | Cloud storage activity and related events |
| **[DataSecurityBehaviors](advanced-hunting-datasecuritybehaviors-table)** (Preview) | Insights about potentially suspicious user behaviors that violate user-defined or default policies configured in the Microsoft Purview suite of solutions |
| **[DataSecurityEvents](advanced-hunting-datasecurityevents-table)** (Preview) | Information about user activities that violate user-defined or default policies in the Microsoft Purview suite of solutions |
| **[DeviceBaselineComplianceAssessment](advanced-hunting-devicebaselinecomplianceassessment-table)** (Preview) | Baseline compliance assessment snapshot, which indicates the status of various security configurations related to baseline profiles on devices |
| **[DeviceBaselineComplianceAssessmentKB](advanced-hunting-devicebaselinecomplianceassessmentkb-table)** (Preview) | Information about various security configurations used by baseline compliance to assess devices |
| **[DeviceBaselineComplianceProfiles](advanced-hunting-devicebaselinecomplianceprofiles-table)** (Preview) | Baseline profiles used for monitoring device baseline compliance |
| **[DeviceEvents](advanced-hunting-deviceevents-table)** | Multiple event types, including events triggered by security controls such as Microsoft Defender Antivirus and exploit protection |
| **[DeviceFileCertificateInfo](advanced-hunting-devicefilecertificateinfo-table)** | Certificate information of signed files obtained from certificate verification events on endpoints |
| **[DeviceFileEvents](advanced-hunting-devicefileevents-table)** | File creation, modification, and other file system events |
| **[DeviceImageLoadEvents](advanced-hunting-deviceimageloadevents-table)** | DLL loading events |
| **[DeviceInfo](advanced-hunting-deviceinfo-table)** | Machine information, including OS information |
| **[DeviceLogonEvents](advanced-hunting-devicelogonevents-table)** | Sign-ins and other authentication events on devices |
| **[DeviceNetworkEvents](advanced-hunting-devicenetworkevents-table)** | Network connection and related events |
| **[DeviceNetworkInfo](advanced-hunting-devicenetworkinfo-table)** | Network properties of devices, including physical adapters, IP and MAC addresses, as well as connected networks and domains |
| **[DeviceProcessEvents](advanced-hunting-deviceprocessevents-table)** | Process creation and related events |
| **[DeviceRegistryEvents](advanced-hunting-deviceregistryevents-table)** | Creation and modification of registry entries |
| **[DeviceTvmBrowserExtensions](advanced-hunting-devicetvmbrowserextensions-table)** (Preview) | Browser extension installations found on devices from Microsoft Defender Vulnerability Management |
| **[DeviceTvmBrowserExtensionsKB](advanced-hunting-devicetvmbrowserextensionskb-table)** (Preview) | Browser extension details and permission information used in the Microsoft Defender Vulnerability Management browser extensions page |
| **[DeviceTvmCertificateInfo](advanced-hunting-devicetvmcertificateinfo-table)** (Preview) | Certificate information for devices in the organization from Microsoft Defender Vulnerability Management |
| **[DeviceTvmHardwareFirmware](advanced-hunting-devicetvmhardwarefirmware-table)** | Hardware and firmware information of devices as checked by Defender Vulnerability Management |
| **[DeviceTvmInfoGathering](advanced-hunting-devicetvminfogathering-table)** | Defender Vulnerability Management assessment events including configuration and attack surface area states |
| **[DeviceTvmInfoGatheringKB](advanced-hunting-devicetvminfogatheringkb-table)** | Metadata for assessment events collected in the `DeviceTvmInfogathering` table |
| **[DeviceTvmSecureConfigurationAssessment](advanced-hunting-devicetvmsecureconfigurationassessment-table)** | Microsoft Defender Vulnerability Management assessment events, indicating the status of various security configurations on devices |
| **[DeviceTvmSecureConfigurationAssessmentKB](advanced-hunting-devicetvmsecureconfigurationassessmentkb-table)** | Knowledge base of various security configurations used by Microsoft Defender Vulnerability Management to assess devices; includes mappings to various standards and benchmarks |
| **[DeviceTvmSoftwareEvidenceBeta](advanced-hunting-devicetvmsoftwareevidencebeta-table)** | Evidence info about where a specific software was detected on a device |
| **[DeviceTvmSoftwareInventory](advanced-hunting-devicetvmsoftwareinventory-table)** | Inventory of software installed on devices, including their version information and end-of-support status |
| **[DeviceTvmSoftwareVulnerabilities](advanced-hunting-devicetvmsoftwarevulnerabilities-table)** | Software vulnerabilities found on devices and the list of available security updates that address each vulnerability |
| **[DeviceTvmSoftwareVulnerabilitiesKB](advanced-hunting-devicetvmsoftwarevulnerabilitieskb-table)** | Knowledge base of publicly disclosed vulnerabilities, including whether exploit code is publicly available |
| **[DisruptionAndResponseEvents](advanced-hunting-disruptionandresponseevents-table)** (Preview) | [Automatic attack disruption](automatic-attack-disruption) events in Microsoft Defender XDR |
| **[EmailAttachmentInfo](advanced-hunting-emailattachmentinfo-table)** | Information about files attached to emails |
| **[EmailEvents](advanced-hunting-emailevents-table)** | Microsoft 365 email events, including email delivery and blocking events |
| **[EmailPostDeliveryEvents](advanced-hunting-emailpostdeliveryevents-table)** | Security events that occur post-delivery, after Microsoft 365 delivers the emails to the recipient mailbox |
| **[EmailUrlInfo](advanced-hunting-emailurlinfo-table)** | Information about URLs on emails |
| **[EntraIdSignInEvents](advanced-hunting-entraidsigninevents-table)** | Microsoft Entra interactive and non-interactive sign-ins |
| **[EntraIdSpnSignInEvents](advanced-hunting-entraidspnsigninevents-table)** | Microsoft Entra service principal and managed identity sign-ins |
| **[ExposureGraphEdges](advanced-hunting-exposuregraphedges-table)** | Microsoft Security Exposure Management exposure graph edge information provides visibility into relationships between entities and assets in the graph |
| **[ExposureGraphNodes](advanced-hunting-exposuregraphnodes-table)** | Microsoft Security Exposure Management exposure graph node information, about organizational entities and their properties |
| **[FileMaliciousContentInfo](advanced-hunting-filemaliciouscontentinfo-table)** (Preview) | Files that were processed by Microsoft Defender for Office 365 in SharePoint Online, OneDrive, and Microsoft Teams. |
| **[GraphAPIAuditEvents](advanced-hunting-graphapiauditevents-table)** | Microsoft Entra ID API requests made to Microsoft Graph API for resources in the tenant |
| **[IdentityAccountInfo](advanced-hunting-identityaccountinfo-table)** | Account information from various sources, including Microsoft Entra ID. This table also includes information and link to the identity that owns the account. |
| **[IdentityDirectoryEvents](advanced-hunting-identitydirectoryevents-table)** | Events involving an on-premises domain controller running Active Directory (AD). This table covers a range of identity-related events and system events on the domain controller. |
| **[IdentityEvents](advanced-hunting-identityevents-table)** (Preview) | Information about identity events obtained from other cloud identity service providers |
| **[IdentityInfo](advanced-hunting-identityinfo-table)** | Account information from various sources, including Microsoft Entra ID |
| **[IdentityLogonEvents](advanced-hunting-identitylogonevents-table)** | Authentication events on Active Directory and Microsoft online services |
| **[IdentityQueryEvents](advanced-hunting-identityqueryevents-table)** | Queries for Active Directory objects, such as users, groups, devices, and domains |
| **[MessageContents](advanced-hunting-messagecontents-table)** | Microsoft Teams message snippets and related message metadata |
| **[MessageEvents](advanced-hunting-messageevents-table)** | Messages sent and received within your organization at the time of delivery |
| **[MessagePostDeliveryEvents](advanced-hunting-messagepostdeliveryevents-table)** | Security events that occurred after the delivery of a Microsoft Teams message in your organization |
| **[MessageUrlInfo](advanced-hunting-messageurlinfo-table)** | URLs sent through Microsoft Teams messages in your organization |
| **[OAuthAppInfo](advanced-hunting-oauthappinfo-table)** (Preview) | Microsoft 365-connected OAuth applications registered with Microsoft Entra ID and available in the Defender for Cloud Apps app governance capability |
| **[UrlClickEvents](advanced-hunting-urlclickevents-table)** | Safe Links clicks from email messages, Teams, and Office 365 apps |