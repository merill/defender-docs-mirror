---
layout: Conceptual
title: IdentityInfo table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-identityinfo-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about user account information in the IdentityInfo table of the advanced hunting schema
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- usx-security
- tier3
ms.custom:
- cx-ti
- cx-ah
ms.topic: reference
ms.date: 2025-12-22T00:00:00.0000000Z
locale: en-us
document_id: 4855ee67-f79f-16c5-58c7-562dc836239c
document_version_independent_id: 4855ee67-f79f-16c5-58c7-562dc836239c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-identityinfo-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-identityinfo-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-identityinfo-table.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 4c3acf5c-d121-efba-212b-514270f9d181
---

# IdentityInfo table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

The `IdentityInfo` table in the [advanced hunting](advanced-hunting-overview) schema contains information about user accounts obtained from various services, including Microsoft Entra ID. Use this reference to construct queries that return information from this table.

This table was renamed from `AccountInfo`. During renames, all queries saved in the portal are automatically updated. Check queries you saved elsewhere.

Microsoft Sentinel uses a slightly expanded version of this table in Log Analytics. For more information, see [Microsoft Sentinel UEBA reference](/en-us/azure/sentinel/ueba-reference#identityinfo-table).

For information on other tables in the advanced hunting schema, [see the advanced hunting reference](advanced-hunting-schema-tables).

The following schema is the unified `IdentityInfo` schema that streamlines a similar table in Microsoft Sentinel's log analytics and in Microsoft Defender advanced hunting. The complete set of columns is available for Defender portal users who onboarded Microsoft Sentinel and turned on the User and Entity Behavior Analytics (UEBA) service.

Defender portal users who don't onboard a Microsoft Sentinel workspace that has the UEBA service turned on can't view UEBA-specific columns. Read UEBA-specific columns.

This advanced hunting table is populated by records from Microsoft Defender for Identity or Microsoft Sentinel and Microsoft Entra ID. If your organization doesn't deploy the service in Microsoft Defender, queries that use the table don't work or return any results. For more information about how to deploy Defender for Identity in the Defender portal, read [Deploy supported services](deploy-supported-services).

| Column name | Data type | Description |
| --- | --- | --- |
| `Timestamp`* | `datetime` | The date and time that the line was written to the database. This is used when there are multiple lines for each identity, such as when a change is detected, or if 24 hours have passed since the last database line was added. |
| `ReportId`* | `string` | Unique identifier for the event |
| `AccountObjectId` | `string` | Unique identifier for the account in Microsoft Entra ID |
| `AccountUpn` | `string` | User principal name (UPN) of the account |
| `OnPremSid` | `string` | On-premises security identifier (SID) of the account |
| `AccountDisplayName` | `string` | Name of the account user displayed in the address book. Typically a combination of a given or first name, a middle initial, and a last name or surname. |
| `AccountName` | `string` | User name of the account |
| `AccountDomain`* | `string` | Domain of the account |
| `CriticalityLevel` | `int` | The criticality score of the account |
| `Type`* | `string` | Type of identity; possible values: User, ServiceAccount |
| `DistinguishedName`* | string | The user's [distinguished name](/en-us/previous-versions/windows/desktop/ldap/distinguished-names) |
| `CloudSid` | `string` | Cloud security identifier of the account |
| `GivenName` | `string` | Given name or first name of the account user |
| `Surname` | `string` | Surname, family name, or last name of the account user |
| `Department` | `string` | Name of the department that the account user belongs to |
| `JobTitle` | `string` | Job title of the account user |
| `EmailAddress` | `string` | SMTP address of the account |
| `SipProxyAddress` | `string` | Voice over IP (VOIP) session initiation protocol (SIP) address of the account |
| `Address` | `string` | Address of the account user |
| `City` | `string` | City where the account user is located |
| `Country` | `string` | Country/Region where the account user is located |
| `IsAccountEnabled` | `boolean` | Indicates whether the account is enabled or not |
| `Manager`* | `string` | The listed manager of the account user |
| `Phone`* | `string` | The listed phone number of the account user |
| `CreatedDateTime`* | `datetime` | Date and time when the account user was created |
| `ChangeSource`* | `string` | Identifies which identity provider or process triggered the addition of the new row. For example, the `System-UserPersistence` value is used for any rows added by an automated process. |
| `BlastRadius`** | `string` | A calculation based on the position of the user in the org tree and the user's Microsoft Entra roles and permissions; possible values: Low, Medium, High |
| `CompanyName`** | `string` | Name of the company for which the user works |
| `DeletedDateTime`** | `datetime` | Date and time when the user account was deleted |
| `EmployeeId`** | `string` | Employee identifier assigned to the user by the organization |
| `OtherMailAddresses`** | `dynamic` | Additional email addresses of the user account |
| `RiskLevel` | `string` | Microsoft Entra ID risk level of the user account; possible values: Low, Medium, High |
| `RiskLevelDetails` | `string` | Details regarding the Microsoft Entra ID risk level |
| `State`** | `string` | State where the sign-in occurred, if available |
| `Tags`* | `dynamic` | Tags assigned to the account user by Defender for Identity |
| `AssignedRoles`* | `dynamic` | For identities from Microsoft Entra-only, the roles assigned to the account user |
| `PrivilegedEntraPimRoles` (Preview) *** | `dynamic` | A snapshot of privileged role assignment schedules and eligibility schedules for the account as maintained by Microsoft Entra Privileged Identity Management (excluding activated assignments) |
| `TenantId` | `string` | Unique identifier representing your organization's instance of Microsoft Entra ID |
| `SourceSystem`* | `string` | The source system for the record |
| `OnPremObjectId` | `string` | Active Directory object ID of the user |
| `TenantMembershipType` | `string` | User type in Microsoft Entra ID; possible values: Guest, Member |
| `RiskStatus`** | `string` | Status of the user's risk; possible values: None, ConfirmedSafe, Remediated, Dismissed, AtRisk, ConfirmedCompromised, UnknownFutureValue |
| `UserAccountControl` | `string` | Security attributes of the user account in the Active Directory domain |
| `IdentityEnvironment` | `string` | Environment where the identity is used; possible values: CloudOnly, Hybrid, On-premises |
| `SourceProviders` | `dynamic` | Source providers of the accounts for the identity; possible values: ActiveDirectory, EntraID, Okta |
| `GroupMembership`** | `dynamic` | Microsoft Entra ID groups where the user account is a member |

\* Available only for tenants with Microsoft Defender for Identity, Microsoft Defender for Cloud Apps, or Microsoft Defender for Endpoint P2 licensing.\*\* Available only for tenants with Microsoft Sentinel. For more information about the freshness and limitations of these columns, see [Microsoft Sentinel UEBA reference](/en-us/azure/sentinel/ueba-reference#identityinfo-table)\*\*\* Available only for tenants with Microsoft Defender for Identity.

## UEBA-specific columns

If you use the Microsoft Defender portal but don't onboard a Microsoft Sentinel workspace with the UEBA service turned on, the following columns aren't available in your `IdentityInfo` table:

- `BlastRadius`
- `CompanyName`
- `DeletedDateTime`
- `EmployeeId`
- `OtherMailAddresses`
- `Tags`
- `State`
- `GroupMembership`
- `RiskStatus`

For more information about UEBA, see [Advanced threat detection with User and Entity Behavior Analytics (UEBA) in Microsoft Sentinel](/en-us/azure/sentinel/identify-threats-with-entity-behavior-analytics). For more information about the different data sources in UEBA, see [Microsoft Sentinel UEBA reference](/en-us/azure/sentinel/ueba-reference).