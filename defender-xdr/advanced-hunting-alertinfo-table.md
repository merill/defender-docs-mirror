---
layout: Conceptual
title: AlertInfo table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-alertinfo-table
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about alert generation events in the AlertInfo table of the advanced hunting schema
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
- msecd-doc-authoring-1015
ms.topic: reference
ms.date: 2026-08-07T00:00:00.0000000Z
locale: en-us
document_id: 6f30981b-9ba9-09c6-1ece-d6ed77259449
document_version_independent_id: 6f30981b-9ba9-09c6-1ece-d6ed77259449
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-alertinfo-table.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-alertinfo-table
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-alertinfo-table.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: b380b180-32bf-c908-ef24-42cda05f34b3
---

# AlertInfo table in the advanced hunting schema - Microsoft Defender XDR | Microsoft Learn

## Get access

To use advanced hunting or other [Microsoft Defender](microsoft-365-defender) capabilities, you need an appropriate role in Microsoft Entra ID. [Read about required roles and permissions for advanced hunting](custom-roles).

The `AlertInfo` table contains records from Microsoft Defender services. When Microsoft Sentinel is onboarded to the Defender portal, the table also contains Microsoft Sentinel alerts associated with incidents. Data availability depends on the services deployed and the Sentinel workspaces you can access. For more information, see [Deploy supported services](deploy-supported-services) and [Transition your Microsoft Sentinel environment to the Defender portal](/en-us/azure/sentinel/move-to-defender).

Also, your access to endpoint data is determined by role-based access control (RBAC) settings in Microsoft Defender for Endpoint. [Read about managing access to Microsoft Defender](m365d-permissions).

## AlertInfo

The `AlertInfo` table in the [advanced hunting](advanced-hunting-overview) schema contains alert information from Microsoft Defender for Endpoint, Microsoft Defender for Office 365, Microsoft Defender for Cloud Apps, Microsoft Defender for Identity, and onboarded Microsoft Sentinel workspaces. Use this reference to construct queries that return information from this table. Join `AlertInfo` with [`AlertEvidence`](advanced-hunting-alertevidence-table) on the `AlertId` column to retrieve the entities and evidence associated with each alert.

For information on other tables in the advanced hunting schema, [see the advanced hunting reference](advanced-hunting-schema-tables).

| Column name | Data type | Description |
| --- | --- | --- |
| `Timestamp` | `datetime` | Date and time when the record was generated |
| `AlertId` | `string` | Unique identifier for the alert |
| `Title` | `string` | Title of the alert |
| `Category` | `string` | Type of threat indicator or breach activity identified by the alert |
| `Severity` | `string` | Indicates the potential impact (high, medium, or low) of the threat indicator or breach activity identified by the alert |
| `ServiceSource` | `string` | Product or service that provided the alert information |
| `DetectionSource` | `string` | Detection technology or sensor that identified the notable component or activity |
| `AttackTechniques` | `string` | MITRE ATT&CK techniques associated with the activity that triggered the alert |