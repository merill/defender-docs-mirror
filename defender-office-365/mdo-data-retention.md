---
layout: Conceptual
title: Microsoft Defender for Office 365 data retention - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/mdo-data-retention
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
f1.keywords:
- NOCSH
ms.author: dansimp
author: Dansimp
ms.date: 2025-05-08T00:00:00.0000000Z
audience: ITPro
ms.topic: article
ms.service: defender-office-365
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- essentials-compliance
- essentials-security
ms.custom: 
description: Admins can learn how long Defender for Office 365 features retain data.
search.appverid: met150
locale: en-us
document_id: 68233506-74c7-f016-dbc1-ab1c36c33950
document_version_independent_id: 68233506-74c7-f016-dbc1-ab1c36c33950
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/mdo-data-retention.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdo-data-retention
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/mdo-data-retention.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
platformId: 1ef91bb4-615f-3575-8dd3-791750cd684a
---

# Microsoft Defender for Office 365 data retention - Microsoft Defender for Office 365 | Microsoft Learn

By default, data across different features is retained for a maximum of 30 days. However, for some of the features, you can specify the retention period based on policy. See the following table for the different retention periods for each feature.

Note

Microsoft Defender for Office 365 comes in two different subscriptions: **Plan 1** and **Plan 2**. If you have **Threat Explorer** at https://security.microsoft.com/threatexplorer, you have Plan 2. Otherwise, you have **Real-time Detections** at https://security.microsoft.com/realtimereports as part of **Plan 1**.

Your Defender for Office 365 subscription affects the tools that are available to you, so make sure you know which subscription you have as you learn.

## Defender for Office 365 Plan 1

| Feature | Retention period |
| --- | --- |
| Alert metadata details (Defender for Office 365 alerts) | 90 days. |
| Entity metadata details (Email) | 30 days. |
| Activity alert details (audit logs) | 7 days. |
| Email entity page | 30 days. |
| Quarantine | 30 days (configurable; 30 days is the maximum). |
| Reports | 90 days for aggregated data.  30 days for detailed information. |
| Submissions | 30 days. |
| Real-Time detections | 30 days. |

## Defender for Office 365 Plan 2

Defender for Office 365 Plan 1 capabilities, plus:

| Feature | Retention period |
| --- | --- |
| Action Center | 180 days.  Office Action Center 30 days. |
| Advanced Hunting | 30 days. |
| AIR (Automated investigation and response) | 60 days for investigations metadata.  30 days for email metadata. |
| Attack simulation training data | 18 months. |
| Campaigns | 30 days. |
| Incidents | 30 days. |
| Remediation | 30 days |
| Threat Analytics | 30 days. |
| Threat Explorer | 30 days. |
| Threat Trackers | 30 days. |