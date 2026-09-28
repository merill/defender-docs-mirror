---
layout: Conceptual
title: Enable Sensitive Data Threat Detection in Defender for Storage - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/enable-defender-for-storage-data-sensitivity
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Sensitive data threat detection helps you prioritize storage alerts fast. See what it scans, how to interpret findings, and how to tune Purview settings.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: a84c4253-cc12-2402-5913-abadaf4d4bf5
document_version_independent_id: cbbddc17-9f96-d2ce-2e08-7338339688f6
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/enable-defender-for-storage-data-sensitivity.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/enable-defender-for-storage-data-sensitivity
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/enable-defender-for-storage-data-sensitivity.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: bd872312-977c-d620-eae7-9a6497cc6c51
---

# Enable Sensitive Data Threat Detection in Defender for Storage - Microsoft Defender for Cloud | Microsoft Learn

Sensitive data threat detection is enabled by default when you enable Defender for Storage. You can enable or disable it in the Azure portal or with other at-scale methods. For more information, see [Configure Defender for Storage](/en-us/azure/storage/common/azure-defender-storage-configure). Sensitive data threat detection is included in the price of Defender for Storage.

This article explains what sensitive data threat detection includes, how to interpret sensitivity findings in alerts, and how to align detection with Microsoft Purview sensitivity settings.

## Use the sensitivity context in the security alerts

Sensitive data threat detection helps security teams identify and prioritize incidents faster. Defender for Storage alerts include sensitivity scan findings and indicate operations performed on resources that contain sensitive data.

In the alert's extended properties, you can find sensitivity scanning findings for a blob container:

- **Sensitivity scanning time (UTC)**: When the last scan was performed.
- **Top sensitivity label**: The most sensitive label found in the blob container.
- **Sensitive information types**: Information types that were found and whether they're based on custom rules.
- **Sensitive file types**: The file types of the sensitive data.

[![Screenshot of a Defender for Storage alert that lists sensitive data findings in the extended properties panel.](media/defender-for-storage-data-sensitivity/sensitive-data-alerts.png)](media/defender-for-storage-data-sensitivity/sensitive-data-alerts.png#lightbox)

## Integrate with the organizational sensitivity settings in Purview (optional)

When you enable sensitive data threat detection, the sensitive data categories include built-in sensitive information types (SITs) in the default list of Purview. Including built-in SITs in the default list affects the alerts you receive from Defender for Storage. Storage accounts or containers that include these SITs are marked as containing sensitive data.

Of the built-in sensitive information types in the default list of Purview, a subset is supported by sensitive data discovery. You can view a [supported sensitive information types reference](sensitive-info-types), which indicates which information types are enabled by default. To change these defaults, see [Configure data sensitivity settings](data-sensitivity-settings).

To customize data sensitivity discovery for your organization, create custom sensitive information types and connect to organizational settings by using a single-step integration. For more information, see [Create a custom sensitive information type](/en-us/microsoft-365/compliance/create-a-custom-sensitive-information-type) and [advanced customization options for data sensitivity discovery](episode-two).

You can also create and publish sensitivity labels for your tenant in Purview. The sensitivity label scope includes items, schematized data assets, and autolabeling rules (recommended). For details, see [Sensitivity labels in Microsoft Purview](/en-us/microsoft-365/compliance/sensitivity-labels).