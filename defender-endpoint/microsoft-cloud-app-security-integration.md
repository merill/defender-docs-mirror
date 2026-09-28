---
layout: Conceptual
title: Microsoft Defender for Cloud Apps integration overview - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/microsoft-cloud-app-security-integration
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: 
description: Microsoft Defender for Endpoint integrates with Defender for Cloud Apps by forwarding all cloud app networking activities.
ms.service: defender-endpoint
ms.subservice: onboard
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.topic: article
ms.date: 2025-03-27T00:00:00.0000000Z
locale: en-us
document_id: 0ad33b66-0e5c-e08d-ea40-893a8c349812
document_version_independent_id: 0ad33b66-0e5c-e08d-ea40-893a8c349812
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/microsoft-cloud-app-security-integration.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: microsoft-cloud-app-security-integration
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/microsoft-cloud-app-security-integration.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
platformId: 13c97cb7-da9c-34ba-dcb3-431d8009f5ea
---

# Microsoft Defender for Cloud Apps integration overview - Microsoft Defender for Endpoint | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

Microsoft Defender for Cloud Apps is a comprehensive solution that gives visibility into cloud apps and services by allowing you to control and limit access to cloud apps, while enforcing compliance requirements on data stored in the cloud. For more information, see [Defender for Cloud Apps](/en-us/cloud-app-security/what-is-cloud-app-security).

Note

This feature is available with an E5 license for [Enterprise Mobility + Security](https://www.microsoft.com/en-us/security) on devices running Windows 10 version 1809 or later, or Windows 11.

## Microsoft Defender for Endpoint and Defender for Cloud Apps integration

Defender for Cloud Apps discovery relies on cloud traffic logs being forwarded to it from enterprise firewall and proxy servers. Microsoft Defender for Endpoint integrates with Defender for Cloud Apps by collecting and forwarding all cloud app networking activities, providing unparalleled visibility to cloud app usage. The monitoring functionality is built into the device, providing complete coverage of network activity.

The integration provides the following major improvements to the existing Defender for Cloud Apps discovery:

- Available everywhere - Since the network activity is collected directly from the endpoint, it's available wherever the device is, on or off corporate network, as it's no longer depended on traffic routed through the enterprise firewall or proxy servers.
- Works out of the box, no configuration required - Forwarding cloud traffic logs to Defender for Cloud Apps requires firewall and proxy server configuration. With the Defender for Endpoint and Defender for Cloud Apps integration, there's no configuration required. Just switch it on in the Defender portal settings and you're good to go.
- Device context - Cloud traffic logs lack device context. Defender for Endpoint network activity is reported with the device context (which device accessed the cloud app), so you are able to understand exactly where (device) the network activity took place, in addition to who (user) performed it.

For more information about cloud discovery, see [Working with discovered apps](/en-us/cloud-app-security/discovered-apps).

## Related topic

- [Configure Microsoft Defender for Cloud Apps integration](microsoft-cloud-app-security-config)