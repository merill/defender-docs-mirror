---
layout: Conceptual
title: Overview of custom detections in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/custom-detections-overview
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Understand how you can use advanced hunting to create custom detections and generate alerts.
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.custom:
- cx-ti
- cx-ah
ms.topic: overview
ms.date: 2026-05-19T00:00:00.0000000Z
locale: en-us
document_id: d3bc7958-4828-b13c-3471-db4afa9eef15
document_version_independent_id: d3bc7958-4828-b13c-3471-db4afa9eef15
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/custom-detections-overview.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: custom-detections-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/custom-detections-overview.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c6f99e62-1cf6-4b71-af9b-649b05f80cce
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3f56b378-07a9-4fa1-afe8-9889fdc77628
platformId: 47f92d5e-b9a8-e087-71bc-ec14ad9329e6
---

# Overview of custom detections in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

With custom detections, you can proactively monitor for and respond to various events and system states, including suspected breach activity and misconfigured endpoints. Custom detections are customizable detection rules that automatically trigger alerts and response actions.

Custom detections work with [advanced hunting](advanced-hunting-overview), which provides a powerful, flexible query language that covers a broad set of event and system information from your network. You can set them to run at regular intervals, generating alerts and taking response actions whenever there are matches. You can create custom detection rules from the advanced hunting query editor or directly from the custom detection rules list.

Custom detections provide:

- Alerts for rule-based detections built from advanced hunting queries
- Automatic response actions

Optimizing your queries in custom detection rules is important in avoiding time-outs and ensuring efficiency. There are several resources available that provide guidance on optimizing your queries in [Advanced hunting query best practices](advanced-hunting-best-practices).

## Manage custom detections as code (Preview)

You can manage custom detection rules as code in a GitHub or Azure DevOps repository using the Microsoft Security BICEP extension. Deploy custom detections through Microsoft Sentinel Repositories for automatic sync, or use BICEP CLI for custom pipelines. For more information, see [Deploy custom detection rules as code](/en-us/azure/sentinel/ci-cd-custom-content#deploy-custom-detection-rules-as-code-preview).