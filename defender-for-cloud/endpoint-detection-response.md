---
layout: Conceptual
title: Assess Defender for Endpoint EDR settings - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/endpoint-detection-response
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
description: Learn how Microsoft Defender for Cloud integrates with Defender for Endpoint as an EDR solution and assesses EDR settings to detect and remediate misconfigurations.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: sfi-image-nochange, msecd-doc-authoring-1013
locale: en-us
document_id: a5436ea8-3f3d-3217-e1a9-755f02491089
document_version_independent_id: f5557b86-072f-d732-6348-87aa47bdf998
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/endpoint-detection-response.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/endpoint-detection-response
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/endpoint-detection-response.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 618d0af5-0fe6-0c2f-8444-353382b82f95
---

# Assess Defender for Endpoint EDR settings - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud integrates natively with Microsoft Defender for Endpoint as an endpoint detection and response (EDR) solution. This article explains how Defender for Cloud uses agentless scanning to assess EDR settings, detect misconfigurations, and surface actionable recommendations to help you remediate them.

## Understand EDR capabilities in Defender for Endpoint

EDR capabilities in Defender for Endpoint detect, investigate, and respond to advanced threats. These capabilities include advanced threat hunting (see [Advanced threat hunting overview](/en-us/defender-xdr/advanced-hunting-overview)) and automatic investigation and remediation (see [Automatic investigation and remediation](/en-us/defender-xdr/m365d-autoir)).

- Defender for Cloud uses agentless scanning to assess EDR settings. See [About agentless data collection](concept-agentless-data-collection).
- Agentless scanning for EDR settings is available when Defender for Cloud is running in your Azure subscription and either Defender for Servers Plan 2 ([Enable Defender for Servers Plan 2](tutorial-enable-servers-plan)) or the Defender cloud security posture management (Defender CSPM) plan ([Enable Defender CSPM](tutorial-enable-cspm-plan)) is enabled.

## Assess Defender for Endpoint settings

When machines run Defender for Endpoint as their EDR solution, Defender for Servers scans them agentlessly. These checks confirm that Defender for Endpoint is configured correctly. Checks include:

- Full and quick scans are older than seven days
- Signatures are out of date
- Antivirus is off or partially configured

If misconfigurations are found, Defender for Cloud presents recommendations such as:

- `EDR configuration issues should be resolved on virtual machines`
- `EDR configuration issues should be resolved on EC2s`
- `Anti-Virus component in your EDR is off or partially configured`
- `Anti-Virus component of your EDR uses outdated signatures`

Once you locate these recommendations ([Review security recommendations](review-security-recommendations)), you can remediate them ([Implement security recommendations](implement-security-recommendations)).