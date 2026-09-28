---
layout: Conceptual
title: Configure Microsoft Defender for Cloud Apps integration - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/microsoft-cloud-app-security-config
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: 
description: Learn how to turn on the settings to enable the Microsoft Defender for Endpoint integration with Microsoft Defender for Cloud Apps.
ms.service: defender-endpoint
ms.subservice: onboard
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 3dc5c842-ee37-5d6d-44cf-211d3105263e
document_version_independent_id: 3dc5c842-ee37-5d6d-44cf-211d3105263e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/microsoft-cloud-app-security-config.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: microsoft-cloud-app-security-config
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/microsoft-cloud-app-security-config.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 50bdcb77-1c4d-fd13-a5f8-3d3f444bc94b
---

# Configure Microsoft Defender for Cloud Apps integration - Microsoft Defender for Endpoint | Microsoft Learn

Turn on Microsoft Defender for Cloud Apps integration to use cloud app discovery signals from Defender for Endpoint.

Note

This feature will be available with an E5 license for [Enterprise Mobility + Security](https://www.microsoft.com/en-us/security) on devices running Windows 10 and Windows 11.

Tip

See [Microsoft Defender for Endpoint integration with Microsoft Defender for Cloud Apps](/en-us/cloud-app-security/mde-integration) for detailed integration of Microsoft Defender for Endpoint with Microsoft Defender for Cloud Apps.

## Enable Microsoft Defender for Cloud Apps in Microsoft Defender for Endpoint

To enable the Microsoft Defender for Cloud Apps integration, follow these steps:

1. In the navigation pane, select **Preferences setup** &gt; **Advanced features**.
2. Select **Microsoft Defender for Cloud Apps** and switch the toggle to **On**.
3. Click **Save preferences**.

After you turn on this integration, Defender for Endpoint starts forwarding discovery signals to Defender for Cloud Apps right away.

## View the data collected

To view and access Microsoft Defender for Endpoint data in Microsoft Defender for Cloud Apps, see [Investigate devices in Defender for Cloud Apps](/en-us/cloud-app-security/mde-integration#investigate-devices-in-cloud-app-security).

For more information about cloud discovery, see [Working with discovered apps](/en-us/cloud-app-security/discovered-apps).

If you're interested in trying Microsoft Defender for Cloud Apps, see [Microsoft Defender for Cloud Apps Trial](https://signup.microsoft.com/Signup?OfferId=757c4c34-d589-46e4-9579-120bba5c92ed&amp;ali=1).