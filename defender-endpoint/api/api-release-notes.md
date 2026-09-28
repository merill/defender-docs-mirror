---
layout: Conceptual
title: Microsoft Defender for Endpoint API release notes - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/api-release-notes
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Release notes for updates made to the Microsoft Defender for Endpoint set of APIs.
ms.service: defender-endpoint
ms.subservice: reference
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- must-keep
ms.topic: reference
ms.custom: api
ms.date: 2025-03-21T00:00:00.0000000Z
locale: en-us
document_id: 640db06a-3369-1afd-2dea-dacc052919bb
document_version_independent_id: 640db06a-3369-1afd-2dea-dacc052919bb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/api-release-notes.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/api-release-notes
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/api-release-notes.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 825d3dc8-b466-8230-6aa8-ed66ee7f32d1
---

# Microsoft Defender for Endpoint API release notes - Microsoft Defender for Endpoint | Microsoft Learn

The following information lists the updates made to the Microsoft Defender for Endpoint APIs and the dates they were made.

## Release notes - newest to oldest (dd.mm.yyyy)

### 08.08.2022

- Added new Export Device Health API method - GET /api/public/avdeviceshealth [Export device health methods and properties](device-health-api-methods-properties)

### 06.10.2021

- Added new Export assessment API method - *Delta Export software vulnerabilities assessment (JSON response)*[Export assessment methods and properties per device](get-assessment-methods-properties).

### 25.05.2021

- Added new API [Export assessment methods and properties per device](get-assessment-methods-properties).

### 03.05.2021

- Added new API: [Remediation activity methods and properties](get-remediation-methods-properties).

### 10.02.2021

- Added new API: [Batch update alerts](batch-update-alerts).

### 25.01.2021

- Updated rate limitations for [Advanced Hunting API](run-advanced-query-api) from 15 to 45 requests per minute.

### 21.01.2021

- Added new API: [Find devices by tag](../machine-tags).
- Added new API: [Import Indicators](import-ti-indicators).

### 03.01.2021

- Updated Alert evidence: added ***detectionStatus***, ***parentProcessFilePath*** and ***parentProcessFileName*** properties.
- Updated [Alert entity](alerts): added ***detectorId*** property.

### 15.12.2020

- Updated [Device](machine) entity: added ***IpInterfaces*** list. See [List devices](get-machines).

### 04.11.2020

- Added new API: [Set device value](set-device-value).
- Updated [Device](machine) entity: added ***deviceValue*** property.

### 01.09.2020

- Added option to expand the Alert entity with its related Evidence. See [List Alerts](get-alerts).

Tip

Do you want to learn more? Engage with the Microsoft Security community in our Tech Community: [Microsoft Defender for Endpoint Tech Community](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/bd-p/MicrosoftDefenderATP).