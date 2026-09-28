---
layout: Conceptual
title: Configure Microsoft Defender for Endpoint system extensions on macOS - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/mac-sysext-policies
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn where to configure the macOS system extensions, network filter, and Full Disk Access required by Microsoft Defender for Endpoint.
ms.service: defender-endpoint
author: paulinbar
ms.author: painbar
ms.reviewer: joshbregman
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-macos
ms.topic: how-to
ROBOTS: noindex,nofollow
ms.subservice: macos
ms.date: 2026-09-08T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: f91fff45-1b99-908d-4f96-cdeede9f5ff5
document_version_independent_id: f91fff45-1b99-908d-4f96-cdeede9f5ff5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/mac-sysext-policies.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mac-sysext-policies
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/mac-sysext-policies.md
platformId: 51dc9ff5-b8d1-e108-4adb-fb369db848bd
---

# Configure Microsoft Defender for Endpoint system extensions on macOS - Microsoft Defender for Endpoint | Microsoft Learn

Microsoft Defender for Endpoint on macOS uses endpoint security and network system extensions. For managed deployments, preapprove the extensions and deploy the network filter and Full Disk Access profiles so that Defender for Endpoint can operate without user approval prompts.

Before you start, review the [Microsoft Defender for Endpoint on macOS prerequisites](microsoft-defender-endpoint-mac-prerequisites). Then use the current procedures for your management tool.

## Configure profiles with Jamf Pro

Use the maintained Jamf Pro deployment procedures:

- [Grant Full Disk Access to Microsoft Defender for Endpoint](mac-jamfpro-policies#step-6-grant-full-disk-access-to-microsoft-defender-for-endpoint).
- [Approve system extensions for Microsoft Defender for Endpoint](mac-jamfpro-policies#step-7-approve-system-extensions-for-microsoft-defender-for-endpoint).
- [Configure the network extension](mac-jamfpro-policies#step-8-configure-network-extension).

## Configure profiles with Microsoft Intune

Microsoft Intune is the recommended tool for configuring and distributing Defender for Endpoint features to devices. However, Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To use Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have Intune, you can use any of the other methods in this article. For more information, see [Microsoft Intune licensing](/en-us/intune/intune-service/fundamentals/licenses).

Note

The macOS **Extensions** template in Intune was deprecated in the August 2024 service release (2408). Policies created with the template continue to work, but you can't create new policies with it.

Don't use the deprecated **Extensions** template or the legacy combined `sysext.xml` profile. Use the following maintained procedures:

- [Approve Microsoft Defender for Endpoint macOS system extensions in Microsoft Intune](manage-profiles-approve-sys-extensions-intune).
- [Configure the network filter](mac-install-with-intune#step-2-network-filter).
- [Configure Full Disk Access](mac-install-with-intune#step-3-full-disk-access).