---
layout: Conceptual
title: IdentityEvents table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-identityevents-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about the IdentityEvents table in the advanced hunting schema, which contains information about identity events obtained from other cloud identity service providers.
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
ms.date: 2025-08-07T00:00:00.0000000Z
locale: en-us
document_id: 8052238c-f2c0-0a59-6145-de74b8d159ae
document_version_independent_id: 8052238c-f2c0-0a59-6145-de74b8d159ae
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-identityevents-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-identityevents-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-identityevents-table.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 8ea7feae-4222-99f9-c9f8-297bdeb654f7
---

# IdentityEvents table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

The `IdentityEvents` table in the [advanced hunting](advanced-hunting-overview) schema contains information about identity events obtained from other cloud identity service providers. Use this reference to construct queries that return information from this table.

Important

Some information relates to prereleased product, which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

This advanced hunting table is populated by records from Microsoft Defender for Identity. If your organization hasn't deployed the service in Microsoft Defender, queries that use the table aren't going to work or return any results. For more information about how to deploy Defender for Identity in the Defender portal, read [Deploy supported services](deploy-supported-services).

Note

This advanced hunting table is populated only when other identity services like Okta are connected to Defender for Identity.

For information on other tables in the advanced hunting schema, see the [advanced hunting reference](advanced-hunting-schema-tables).

| Column name | Data type | Description |
| --- | --- | --- |
| `Timestamp ` | `datetime` | Date and time when the record was generated |
| `ReportId ` | `string` | Unique identifier for the event |
| `AccountId ` | `string` | Unique identifier for the account in the source application |
| `AccountType` | `string` | Type of user account, indicating its general role like User, SystemPrincipal |
| `AccountDisplayName` | `string` | Name displayed in the address book entry for the account user. This is usually a combination of the given name, middle initial, and surname of the user. |
| `AccountUpn` | `string` | Alternate ID, email, or name for the account in the source application |
| `ActionType` | `string` | Type of activity that triggered the event in the raw format received from the source application |
| `ActionResult` | `string` | Result of the action |
| `ActionFailureReason` | `string` | Information explaining why the recorded action failed |
| `IPAddress` | `string` | IP address assigned to the device and used during related network communications |
| `UserAgent` | `string` | User agent information from the web browser or other client application |
| `TargetObjects` | `dynamic` | List of the target objects of this activity. Target object can be user, group, role, domain, application, and more. |
| `Application` | `string` | The source application where this event was received from |
| `ApplicationInstanceId` | `string` | Domain of the source application |
| `ApplicationEventId` | `string` | Raw event ID provided by the source application |
| `ApplicationSessionId` | `string` | Raw session ID provided by the source application |
| `RawEventData` | `dynamic` | Full raw event information from the source application in JSON format |
| `AdditionalFields` | `dynamic` | Additional information about the entity or event |