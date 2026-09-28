---
layout: Conceptual
title: IdentityAccountInfo table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-identityaccountinfo-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about the IdentityAccountInfo table in the advanced hunting schema, which provides account information from various sources, including Microsoft Entra ID.
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
ms.date: 2026-02-04T00:00:00.0000000Z
locale: en-us
document_id: 668172cc-f654-de43-3c93-8e63359d0742
document_version_independent_id: 668172cc-f654-de43-3c93-8e63359d0742
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-identityaccountinfo-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-identityaccountinfo-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-identityaccountinfo-table.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
platformId: bfd76fcf-3e86-af76-f50b-d88da9656514
---

# IdentityAccountInfo table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

The `IdentityAccountInfo` table in the [advanced hunting](advanced-hunting-overview) schema contains information about account information from various sources, including Microsoft Entra ID. This table also includes information and link to the identity that owns the account. Use this reference to construct queries that return information from this table.

For information on other tables in the advanced hunting schema, [see the advanced hunting reference](advanced-hunting-schema-tables).

| Column name | Data type | Description |
| --- | --- | --- |
| `Timestamp` | `datetime` | The date and time that the line was written to the database.This is used when there are multiple lines for each identity, such as when a change is detected, or if 24 hours have passed since the last database line was added. |
| `ReportId` | `string` | Unique identifier for the event |
| `SourceProviderAccountId` | `string` | Identifier for the account in the source provider (for example, object ID for a Microsoft Entra ID account) |
| `AccountId` | `string` | Internal identifier for the account |
| `IdentityId` | `string` | Identifier for the identity that the account is linked to |
| `IsPrimary ` | `bool` | Indicates if this account is considered as primary account for the linked identity |
| `IdentityLinkType` | `string` | Type of linkage between the account and identity; possible values: Manual, Strong identifiers |
| `IdentityLinkReason` | `string` | Reason for linking the account and identity. If the linkage type is manual, the value will be the justification comment added by the user. |
| `IdentityLinkTime` | `datetime` | Date and time the account was linked to the identity |
| `IdentityLinkBy` | `string` | The entity that linked the account to the identity. If the linkage type is based on strong identifiers, the value will be System |
| `DisplayName` | `string` | Name of the account user displayed in the address book. Typically a combination of a given or first name, a middle initial, and a last name or surname. |
| `AccountUpn` | `string` | User principal name (UPN) of the account |
| `EmailAddress` | `string` | SMTP address of the account |
| `CriticalityLevel` | `int` | The criticality score of the account |
| `DefenderRiskLevel` | `int` | The risk level of the account as calculated by Microsoft Defender |
| `DefenderRiskUpdateTime` | `datetime` | Date and time Microsoft Defender last updated the risk level of the account |
| `Type` | `string` | Type of identity; possible values: User, ServiceAccount |
| `GivenName` | `string` | Given name or first name of the account user |
| `Surname` | `string` | Surname, family name, or last name of the account user |
| `EmployeeId` | `string` | Employee identifier assigned to the user by the organization |
| `Department` | `string` | Name of the department that the account user belongs to |
| `JobTitle` | `string` | Job title of the account user |
| `Address` | `string` | Address of the account user |
| `City` | `string` | City where the account user is located |
| `Country` | `string` | Country/Region where the account user is located |
| `Phone` | `string` | The listed phone number of the account user |
| `Manager` | `string` | The listed manager of the account user |
| `Sid` | `string` | Security identifier (SID) of the account |
| `AccountStatus` | `string` | The status of the account; possible values: Disabled, Enabled, Deleted |
| `SourceProvider` | `string` | Source application or service of the account (for example, Microsoft Entra ID) |
| `SourceProviderInstanceId` | `string` | The identifier of the source application or service of the account. For example, in Microsoft Entra ID, this is the organization Globally Unique Identifier (GUID). |
| `SourceProviderInstanceDisplayName` | `string` | The display name of the source application or service of the account |
| `AuthenticationMethod` | `string` | Authentication method used to allow the account user to sign into the account; possible values: Credentials, Federated, Hybrid |
| `AuthenticationSourceAcccountId` | `string` | The identifier of the federating account, if the authentication method is Federated |
| `EnrolledMfas` | `dynamic` | Types of multifactor authentication methods configured for the account user and their status |
| `LastPasswordChangeTime` | `datetime` | Date and time the account password was last changed |
| `GroupMembership` | `dynamic` | Group identifiers assigned to the account |
| `AssignedRoles` | `dynamic` | Role identifiers assigned to the account |
| `EligibleRoles` | `dynamic` | Identifiers for roles the account are eligible to use (for example, Microsoft Entra Privileged Identity Management roles) |
| `TenantMembershipType` | `string` | User type; possible values: Guest, Member |
| `CreatedDateTime ` | `datetime` | Date and time when the user account was created |
| `DeletedDateTime` | `datetime` | Date and time when the user account was deleted |
| `Tags` | `dynamic` | Tags assigned to the account by Defender for Identity |
| `SourceProvderRiskLevel` | `dynamic` | Risk level of the account as it appears in the source provider; possible values: Low, Medium, High |
| `AdditionalFields` | `dynamic` | Additional information about the entity or event |
| `TenantId` | `string` | Universally unique identifier (UUID) for the tenant |