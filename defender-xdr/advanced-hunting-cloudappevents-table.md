---
layout: Conceptual
title: CloudAppEvents table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-cloudappevents-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about events from cloud apps and services in the CloudAppEvents table of the advanced hunting schema
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
ms.topic: reference
ms.date: 2025-05-15T00:00:00.0000000Z
locale: en-us
document_id: 10cb3d8b-fffd-2dcc-4019-94cb5a111a1d
document_version_independent_id: 10cb3d8b-fffd-2dcc-4019-94cb5a111a1d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-cloudappevents-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-cloudappevents-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-cloudappevents-table.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
platformId: 93135818-7ff9-bbf0-fe79-d74e579fcbca
---

# CloudAppEvents table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

The `CloudAppEvents` table in the [advanced hunting](advanced-hunting-overview) schema contains information about events involving accounts and objects in Office 365 and other cloud apps and services. Use this reference to construct queries that return information from this table.

## Prerequisites

This advanced hunting table is populated by records from Microsoft Defender for Cloud Apps. If your organization hasn’t deployed the service in Microsoft Defender XDR, queries that use the table aren’t going to work or return any results. For more information about how to deploy Defender for Cloud Apps in Defender XDR, read [Deploy supported services](deploy-supported-services).

To make sure the `CloudAppEvents` table is populated:

1. Go to the Defender portal and select **Settings &gt; Cloud apps &gt; App connectors**.
2. In the **Select Microsoft 365 components** page, select the **Microsoft 365 activities** checkbox.

For detailed instructions, see: [Connect Microsoft 365 to Microsoft Defender for Cloud Apps](/en-us/defender-cloud-apps/protect-office-365#prerequisites)

For information on other tables in the advanced hunting schema, [see the advanced hunting reference](advanced-hunting-schema-tables).

| Column name | Data type | Description |
| --- | --- | --- |
| `Timestamp` | `datetime` | Date and time when the event was recorded |
| `ActionType` | `string` | Type of activity that triggered the event |
| `Application` | `string` | Application that performed the recorded action |
| `ApplicationId` | `int` | Unique identifier for the application |
| `AppInstanceId` | `int` | Unique identifier for the instance of an application. To convert this to Microsoft Defender for Cloud Apps App-connector-ID, use `CloudAppEvents| distinct ApplicationId,AppInstanceId,binary_or(binary_shift_left(AppInstanceId,20),Application|order by ApplicationId,AppInstanceId` |
| `AccountObjectId` | `string` | Unique identifier for the account in Microsoft Entra ID |
| `AccountId` | `string` | An identifier for the account as found by Microsoft Defender for Cloud Apps. Could be Microsoft Entra ID, user principal name, or other identifiers. |
| `AccountDisplayName` | `string` | Name displayed in the address book entry for the account user. This is usually a combination of the given name, middle initial, and surname of the user. |
| `IsAdminOperation` | `bool` | Indicates whether the activity was performed by an administrator |
| `DeviceType` | `string` | Type of device based on purpose and functionality, such as network device, workstation, server, mobile, gaming console, or printer |
| `OSPlatform` | `string` | Platform of the operating system running on the device. This column indicates specific operating systems, including variations within the same family, such as Windows 11, Windows 10, and Windows 7. |
| `IPAddress` | `string` | IP address assigned to the device during communication |
| `IsAnonymousProxy` | `boolean` | Indicates whether the IP address belongs to a known anonymous proxy |
| `CountryCode` | `string` | Two-letter code indicating the country where the client IP address is geolocated |
| `City` | `string` | City where the client IP address is geolocated |
| `Isp` | `string` | Internet service provider associated with the IP address |
| `UserAgent` | `string` | User agent information from the web browser or other client application |
| `ActivityType` | `string` | Type of activity that triggered the event |
| `ActivityObjects` | `dynamic` | List of objects, such as files or folders, that were involved in the recorded activity |
| `ObjectName` | `string` | Name of the object that the recorded action was applied to |
| `ObjectType` | `string` | Type of object, such as a file or a folder, that the recorded action was applied to |
| `ObjectId` | `string` | Unique identifier of the object that the recorded action was applied to |
| `ReportId` | `string` | Unique identifier for the event |
| `AccountType` | `string` | Type of user account, indicating its general role and access levels, such as Regular, System, Admin, Application |
| `IsExternalUser` | `boolean` | Indicates whether a user inside the network doesn't belong to the organization's domain |
| `IsImpersonated` | `boolean` | Indicates whether the activity was performed by one user for another (impersonated) user |
| `IPTags` | `dynamic` | Customer-defined information applied to specific IP addresses and IP address ranges |
| `IPCategory` | `string` | Additional information about the IP address |
| `UserAgentTags` | `dynamic` | More information provided by Microsoft Defender for Cloud Apps in a tag in the user agent field. Can have any of the following values: Native client, Outdated browser, Outdated operating system, Robot |
| `RawEventData` | `dynamic` | Raw event information from the source application or service in JSON format |
| `AdditionalFields` | `dynamic` | Additional information about the entity or event |
| `LastSeenForUser` | `dynamic` | Indicates the number of days since a specific attribute was last seen for the user. A value of 0 means the attribute was seen today, a negative value indicates the attribute is being seen for the first time, and a positive value represents the number of days since the attribute was last seen. For example: `{"ActionType":"0","OSPlatform":"4","ISP":"-1"}` |
| `UncommonForUser` | `dynamic` | Lists the attributes in the event that are uncommon for the user, helping to rule out false positives and find anomalies. For example: `["ActivityType","ActionType"].` To filter out nonanomalous results: events with low or insignificant security value won't go through enrichment processes and will have a value of "", while high-value events will go through enrichment processes and, if no anomalies are found, will have a value of "[]". |
| `AuditSource` | `string` | Audit data source. Possible values are one of the following: - Defender for Cloud Apps access control - Defender for Cloud Apps session control  - Defender for Cloud Apps app connector |
| `SessionData` | `dynamic` | The Defender for Cloud Apps session ID for access or session control. For example: `{InLineSessionId:"232342"}` |
| `OAuthAppId` | `string` | A unique identifier that is assigned to an application when it's registered to Microsoft Entra with OAuth 2.0 protocol. |

## Apps and services covered

The **CloudAppEvents** table contains enriched logs from all SaaS applications connected to Microsoft Defender for Cloud Apps, such as:

- Office 365 and Microsoft Applications, including:
    - Exchange Online
    - SharePoint Online
    - Microsoft Teams
    - Dynamics 365
    - Skype for Business
    - Viva Engage
    - Power Automate
    - Power BI
    - Dropbox
    - Salesforce
    - GitHub
    - Atlassian

Connect supported cloud apps for instant, out-of-the-box protection, deep visibility into the app's user and device activities, and more. For more information, see [Protect connected apps using cloud service provider APIs](/en-us/defender-cloud-apps/protect-connected-apps).