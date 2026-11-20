---
layout: Conceptual
title: SyntheticMediaDetectionEvents table in the advanced hunting schema - Microsoft Defender | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-synthetic-media-detection-events
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about the SyntheticMediaDetectionEvents table in the advanced hunting schema, which contains details about synthetic media (deepfake) detection events in Microsoft Teams.
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: dhagarwal
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.custom:
- cx-ti
- cx-ah
ms.topic: reference
ms.date: 2026-10-28T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 8c523293-47c9-bc1d-6ceb-cea3db762f9f
document_version_independent_id: 8c523293-47c9-bc1d-6ceb-cea3db762f9f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-synthetic-media-detection-events.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-synthetic-media-detection-events
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-synthetic-media-detection-events.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
platformId: c85198b6-dce4-56f0-01b3-1b90d72e5534
---

# SyntheticMediaDetectionEvents table in the advanced hunting schema - Microsoft Defender | Microsoft Learn

The `SyntheticMediaDetectionEvents` table in the [advanced hunting](advanced-hunting-overview) schema contains details about synthetic media (deepfake) detection events in Microsoft Teams in your organization.

This advanced hunting table is populated by records from Microsoft Defender for Office 365. If your organization hasn't deployed the service in Microsoft Defender, queries that use the table don't work or return any results. For more information about how to deploy Defender for Office 365 in the Defender portal, read [Deploy supported services](deploy-supported-services).

Note

This table contains data only if you're using an approved detection engine: Microsoft or a third-party engine (GetReal, Pindrop, Reality Defender, or Resemble AI).

## Schema

For information on other tables in the advanced hunting schema, [see the advanced hunting reference](advanced-hunting-schema-tables).

| Column name | Data type | Description |
| --- | --- | --- |
| `DetectionId` | `string` | Unique identifier for this detection event |
| `Timestamp` | `datetime` | Date and time when the activity was recorded |
| `Severity` | `string` | Severity of the detection; possible values: High, Medium, or Low |
| `ConfidenceScore` | `real` | Indicates whether the synthetic media was likely used with harmful intent (for example, impersonation, fraud, or social engineering), rather than benign use (AI-generated avatars or accessibility tools) |
| `IsMalicious` | `boolean` | Indicates whether the synthetic media was likely used with harmful intent (for example, impersonation, fraud, or social engineering), rather than benign use (AI-generated avatars or accessibility tools) |
| `SourceType` | `string` | The Microsoft 365 application where the detection event occurred |
| `SourceId` | `string` | Unique identifier of the source (for example, call ID for meetings or calls, network message ID for emails, and file ID for files) |
| `SourceContextUrl` | `string` | URL of the source (for example, the meeting URL or file URL) |
| `SourceContextName` | `string` | Name of the source (for example, the meeting, file, or email name) |
| `SourceContextType` | `string` | Context of the source (for example, scheduled meeting, ad hoc meeting, or recurring meeting) |
| `DetectedUserIdType` | `string` | Type of identifier to interpret DetectedUserId; possible values: PSTN (for phone number), Enterprise, Consumer, or Bot |
| `DetectedUserDisplayName` | `string` | Display name of the user flagged as using synthetic media |
| `DetectionProviderName` | `string` | Name of the detection bot or application that identified the synthetic media |
| `Modality` | `string` | Type of content analyzed; possible values: Audio, Video, Multimodal, or Image |
| `IsRealTime` | `boolean` | Indicates whether the detection happened live during the session (`true`) or after as a post-session analysis (`false`) |
| `ContentDurationSec` | `real` | Duration of the suspicious content segment in seconds |
| `Detections` | `dynamic` | Detailed results from each detection model; each entry includes model name, content type analyzed, detection tasks, time segment, and confidence score |
| `PrimaryModelTasks` | `string` | The primary types of synthetic media detected |

## Correlate detections with call activities

Join the `SourceId` column in `SyntheticMediaDetectionEvents` with the `CallId` column in the [CallActivityEvents](advanced-hunting-callactivityevents-table) table to view activities recorded for the same Microsoft Teams call or meeting.

The following query returns up to 500 matching detection and activity records, starting with the most recent call activities. The `inner` join returns only records with matching call IDs and preserves multiple detections and activities for the same call.

```kusto
CallActivityEvents
| join kind=inner (
    SyntheticMediaDetectionEvents
    | where isnotempty(SourceId)
) on $left.CallId == $right.SourceId
| project DetectionTimestamp = Timestamp, DetectionId, Severity,
    DetectedUserDisplayName, CallId, ActivityTimestamp, ActivityType,
    ActivityInitiatorDisplayName
| order by ActivityTimestamp desc
| take 500
```