---
layout: Conceptual
title: OAuthAppInfo table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-oauthappinfo-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about the OAuthAppInfo table which contains information about Microsoft 365-connected OAuth applications registered with Microsoft Entra ID and available in the Defender for Cloud Apps app governance capability.
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
ms.date: 2026-08-04T00:00:00.0000000Z
locale: en-us
document_id: 358df280-788a-9082-b623-5b20ebab76fa
document_version_independent_id: 358df280-788a-9082-b623-5b20ebab76fa
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-oauthappinfo-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-oauthappinfo-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-oauthappinfo-table.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
platformId: f3375817-eac5-d68b-ce22-7b1f1b8a5f25
---

# OAuthAppInfo table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

Important

Some information relates to prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

The `OAuthAppInfo` table in the advanced hunting schema contains information about Microsoft 365-connected OAuth applications in the organization that are registered with Microsoft Entra ID and available in the Microsoft Defender for Cloud Apps app governance capability.

The `OAuthAppInfo` table might not include all the app or service principal-related properties that are available on Entra ID. It also doesn't include data related to Microsoft first-party apps or Entra managed identities. The coverage of the table is based on the existing scope of Microsoft 365-connected apps covered by app governance.

## Prerequisites

This advanced hunting table is populated by app governance records from Microsoft Defender for Cloud Apps.

You need to turn on app governance to view the `OAuthAppInfo` table in advanced hunting. To turn on app governance, follow the steps in [Turn on app governance](/en-us/defender-cloud-apps/app-governance-get-started).

## Schema

For information on other tables in the advanced hunting schema, see [the advanced hunting reference](advanced-hunting-schema-tables).

| Column name | Data type | Description |
| --- | --- | --- |
| `ReportId` | `string` | Unique identifier for the record |
| `Timestamp` | `datetime` | Date and time when the record was created |
| `OAuthAppId` | `string` | The unique identifier for the app as assigned by Microsoft Entra ID |
| `ServicePrincipalId` | `string` | The unique identifier for the service principal instance of the application in the tenant |
| `AppName` | `string` | The application's display name as exposed by the associated service principal |
| `AddedOnTime` | `datetime` | Date and time when the application was registered |
| `LastModifiedTime` | `datetime` | Timestamp when the app was last modified |
| `AppStatus` | `string` | Status of the app; can be: Enabled, DisabledByMicrosoft, DisabledByAppGovernancePolicy, DisabledByUser, Deleted (information for apps with Deleted status is only available for 30 days since the app was deleted) |
| `VerifiedPublisher` | `dynamic` | Specifies details about the verified publisher of the application which this service principal represents. It includes information such as: DisplayName, VerifiedPublisherId, AddedDateTime |
| `PrivilegeLevel` | `string` | The privilege level of the app based on the highest classified permission granted to the app |
| `Permissions` | `dynamic` | Contains an array of permission objects; each permission object includes PermissionName, TargetAppId, TargetAppDisplayName, PermissionType, PrivilegeLevel, UsageStatus |
| `ConsentedUsersCount` | `integer` | Count of users who have consented to the app; this information is only available when the app isn't admin consented |
| `IsAdminConsented` | `boolean` | Value is True if a user has provided admin consent to the app on behalf of all the users in the org, otherwise the value is False |
| `AppOrigin` | `string` | Specifies whether the app is internal to the organization or registered in an external tenant |
| `LastUsedTime` | `datetime` | Date and time when the app last signed in. Tracking of this data goes back to June, 2022 |
| `AppOwnerTenantId` | `string` | Specifies the ID of the tenant where the app was registered |
| `RiskScore` | `integer` | The risk score of the app as calculated by Microsoft Defender |
| `AssignedRoles` | `dynamic` | Active roles assigned to the service principal. This currently covers only Entra roles. |

The `OAuthAppInfo` table updates information on an hourly basis to record any changes in metadata or insights for OAuth apps based on data from Defender for Cloud Apps app governance.

Additionally, to ensure that `OAuthAppInfo` table retains data for the covered apps, a complete snapshot of all OAuth apps is sent twice a month.