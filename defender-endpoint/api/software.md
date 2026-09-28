---
layout: Conceptual
title: Software methods and properties - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/software
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Retrieves top recent alerts.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- must-keep
ms.topic: reference
ms.subservice: reference
ms.custom: api
ms.date: 2025-03-01T00:00:00.0000000Z
locale: en-us
document_id: 8ac7f936-9d7c-80ec-d9ca-ab549b98949e
document_version_independent_id: 8ac7f936-9d7c-80ec-d9ca-ab549b98949e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/software.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/software
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/software.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: b2e98043-ca68-19fc-9e60-6957d41e155c
---

# Software methods and properties - Microsoft Defender for Endpoint | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Properties

| Property | Type | Description |
| --- | --- | --- |
| id | String | Software ID |
| Name | String | Software name |
| Vendor | String | Software publisher name |
| Weaknesses | Long | Number of discovered vulnerabilities |
| publicExploit | Boolean | Public exploit exists for some of the vulnerabilities |
| activeAlert | Boolean | Active alert is associated with this software |
| exposedMachines | Long | Number of exposed devices |
| impactScore | Double | Exposure score impact of this software |