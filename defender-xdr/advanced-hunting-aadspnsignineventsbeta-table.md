---
layout: Conceptual
title: AADSpnSignInEventsBeta table in the advanced hunting schema (deprecated) - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-aadspnsignineventsbeta-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about information associated with the Beta Microsoft Entra service principal and managed identity sign-in events table.
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
document_id: 015582eb-ea7e-1f66-75cc-c8d7251f4faa
document_version_independent_id: 015582eb-ea7e-1f66-75cc-c8d7251f4faa
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-aadspnsignineventsbeta-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-aadspnsignineventsbeta-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-aadspnsignineventsbeta-table.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: cac6ed56-3705-0fa3-f6bb-95f6ad5f00b9
---

# AADSpnSignInEventsBeta table in the advanced hunting schema (deprecated) - Microsoft Defender XDR | Microsoft Learn

Important

On October 19, 2026, the `AADSpnSignInEventsBeta` table will be deprecated and replaced by [`EntraIdSpnSignInEvents`](advanced-hunting-entraidspnsigninevents-table). This change removes the former's preview status and aligns it with the existing product branding.

The `EntraIdSpnSignInEvents` table is already available. All queries that use `AADSpnSignInEventsBeta` will be migrated automatically to `EntraIdSpnSignInEvents` on October 19, 2026.

Important

The `AADSpnSignInEventsBeta` table is currently in beta and is being offered on a short-term basis to allow you to hunt through Microsoft Entra sign-in events. Customers need to have a Microsoft Entra ID P2 license to collect and view activities for this table.

The `AADSpnSignInEventsBeta` table in the advanced hunting schema contains information about Microsoft Entra service principal and managed identity sign-ins. You can learn more about the different kinds of sign-ins in [Microsoft Entra sign-in activity reports - preview](/en-us/azure/active-directory/reports-monitoring/concept-all-sign-ins).

Use this reference to construct queries that return information from the table.

For information on other tables in the advanced hunting schema, see [the advanced hunting reference](/en-us/windows/security/threat-protection/microsoft-defender-atp/advanced-hunting-reference).

| Column name | Data type | Description |
| --- | --- | --- |
| `Timestamp` | `datetime` | Date and time when the record was generated |
| `Application` | `string` | Application that performed the recorded action |
| `ApplicationId` | `string` | Unique identifier for the application |
| `IsManagedIdentity` | `boolean` | Indicates whether the sign-in was initiated by a managed identity |
| `ErrorCode` | `int` | Contains the error code if a sign-in error occurs. To find a description of a specific error code, visit https://aka.ms/AADsigninsErrorCodes. |
| `CorrelationId` | `string` | Unique identifier of the sign-in event |
| `ServicePrincipalName` | `string` | Name of the service principal that initiated the sign-in |
| `ServicePrincipalId` | `string` | Unique identifier of the service principal that initiated the sign-in |
| `ResourceDisplayName` | `string` | Display name of the resource accessed. The display name can contain any character. |
| `ResourceId` | `string` | Unique identifier of the resource accessed |
| `ResourceTenantId` | `string` | Unique identifier of the tenant of the resource accessed |
| `IPAddress` | `string` | IP address assigned to the endpoint and used during related network communications |
| `Country` | `string` | Two-letter code indicating the country/region where the client IP address is geolocated |
| `State` | `string` | State where the sign-in occurred, if available |
| `City` | `string` | City where the account user is located |
| `Latitude` | `string` | The north to south coordinates of the sign-in location |
| `Longitude` | `string` | The east to west coordinates of the sign-in location |
| `RequestId` | `string` | Unique identifier of the request |
| `ReportId` | `string` | Unique identifier for the event |