---
layout: Conceptual
title: Migrate to Supported API Solutions - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/migrate-to-supported-api-solutions
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: This article describes how to transition from the legacy Defender for Cloud Apps SIEM agent to supported APIs.
ms.date: 2025-05-19T00:00:00.0000000Z
ms.topic: article
locale: en-us
document_id: 8d413275-3598-3a83-dec3-fbf1f070f815
document_version_independent_id: 8d413275-3598-3a83-dec3-fbf1f070f815
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/migrate-to-supported-api-solutions.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: migrate-to-supported-api-solutions
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/migrate-to-supported-api-solutions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 95c8fa68-7cea-4329-655d-2c4b449bdeb0
---

# Migrate to Supported API Solutions - Microsoft Defender for Cloud Apps | Microsoft Learn

Transitioning from the legacy [Defender for Cloud Apps SIEM agent](siem) to supported APIs enables continued access to enriched activities and alerts data. While the APIs might not have exact one-to-one mappings to the legacy Common Event Format (CEF) schema, they provide comprehensive, enhanced data through integration across multiple Microsoft Defender workloads.

## Recommended APIs for migration

> 
> To ensure continuity and access to data currently available through Microsoft Defender for Cloud Apps SIEM agents, we recommend transitioning to the following supported APIs:
> 
> - For alerts and activities, see: [Microsoft Defender XDR Streaming API](/en-us/defender-xdr/streaming-api).
> - For Microsoft Entra ID Protection logon events, see [IdentityLogonEvents](/en-us/defender-xdr/advanced-hunting-identitylogonevents-table) table in the advanced hunting schema.
> - For Microsoft Graph Security Alerts API, see: [List alerts_v2](/en-us/graph/api/security-list-alerts_v2?view=graph-rest-1.0&amp;tabs=http&amp;preserve-view=true)
> - To view Microsoft Defender for Cloud Apps alerts data in the Microsoft Defender XDR incidents API, see [Microsoft Defender XDR incidents APIs and the incidents resource type](/en-us/graph/api/security-list-alerts_v2?view=graph-rest-1.0&amp;tabs=http&amp;preserve-view=true)
> 

## Field Mapping from Legacy SIEM to Supported APIs

The table below compares the legacy SIEM agent’s CEF fields to the nearest equivalent fields in the Defender XDR Streaming API (advanced hunting event schema) and the Microsoft Graph Security Alerts API.

| CEF Field (MDA SIEM) | Description | Defender XDR Streaming API (CloudAppEvents/AlertEvidence/AlertInfo) | Graph Security Alerts API (v2) |
| --- | --- | --- | --- |
| `start` | Activity or alert timestamp | `Timestamp` | `firstActivityDateTime` |
| `end` | Activity or alert timestamp | None | `lastActivityDateTime` |
| `rt` | Activity or alert timestamp | `createdDateTime` | `createdDateTime` / `lastUpdateDateTime` / `resolvedDateTime` |
| `msg` | Alert or activity description as shown in the portal in a human readable format | The closest structured fields that contribute to a similar description: `actorDisplayName`, `ObjectName`, `ActionType`, `ActivityType` | `description` |
| `suser` | Activity or alert subject user | `AccountObjectId`, `AccountId`, `AccountDisplayName` | See `userEvidence` resource type |
| `destinationServiceName` | Activity or alert from the originating app (for example, SharePoint, Box) | `CloudAppEvents > Application` | See `cloudApplicationEvidence` resource type |
| `cs<X>Label`, `cs<X>` | Alert or activity dynamic fields (for example, target user, object) | `Entities`, `Evidence`, `additionalData`, `ActivityObjects` | Various `alertEvidence` resource types |
| `EVENT_CATEGORY_*` | High-level activity category | `ActivityType` / `ActionType` | `category` |
| `<name>` | Matched policy name | `Title`, `alertPolicyId` | `Title`, `alertPolicyId` |
| `<ACTION>` (Activities) | Specific activity type | `ActionType` | N/A |
| `externalId` (Activities) | Event ID | `ReportId` | N/A |
| `requestClientApplication` (activities) | User agent of the client device in activities | `UserAgent` | N/A |
| `Dvc` (activities) | Client device IP | `IPAddress` | N/A |
| `externalId` (Alert) | Alert ID | `AlertId` | `id` |
| `<alert type>` | Alert type (for example, ALERT\_CABINET\_EVENT\_MATCH\_AUDI) | - | - |
| `Src` / `c6a1` (alerts) | Source IP | `IPAddress` | `ipEvidence` resource type |