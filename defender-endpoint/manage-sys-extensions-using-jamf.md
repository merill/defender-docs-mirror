---
layout: Conceptual
title: Configure Microsoft Defender for Endpoint system extensions using Jamf Pro - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/manage-sys-extensions-using-jamf
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Configure Full Disk Access, system extensions, and the network extension for Microsoft Defender for Endpoint on macOS using Jamf Pro.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.reviewer: joshbregman
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- mde-macos
ms.topic: how-to
ms.subservice: macos
ms.date: 2026-09-17T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: cdd1a44f-bf2e-23ff-ff77-1b1ecc071e29
document_version_independent_id: cdd1a44f-bf2e-23ff-ff77-1b1ecc071e29
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/manage-sys-extensions-using-jamf.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: manage-sys-extensions-using-jamf
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/manage-sys-extensions-using-jamf.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: bc7c2752-1958-acfc-d169-9daabc486e89
---

# Configure Microsoft Defender for Endpoint system extensions using Jamf Pro - Microsoft Defender for Endpoint | Microsoft Learn

Microsoft Defender for Endpoint on macOS requires configuration profiles for Full Disk Access, system extensions, and the network extension. Use the Microsoft-maintained profiles and current Jamf Pro upload procedure instead of manually recreating the payloads.

Jamf Pro is a separate product that isn't part of Defender for Endpoint and isn't included with Defender for Endpoint subscriptions. To use these procedures, your organization needs a separate Jamf Pro subscription. For product and subscription information, see [Jamf Pro](https://www.jamf.com/products/jamf-pro/). If your organization doesn't use Jamf Pro, you can [deploy Defender for Endpoint with Microsoft Intune](mac-install-with-intune) or [use another mobile device management (MDM) solution](mac-install-with-other-mdm).

Important

Microsoft provides information about Jamf Pro to support integration scenarios but doesn't provide troubleshooting support for this third-party product. For issues specific to Jamf Pro, contact Jamf support.

## Prerequisites

Before you configure the required profiles, review the [Defender for Endpoint on macOS prerequisites](microsoft-defender-endpoint-mac-prerequisites). Verify that your Jamf Pro account can upload and scope computer configuration profiles.

## Configure system extensions in Jamf Pro

The maintained Jamf Pro deployment article contains the current profile downloads, Defender-specific identifiers, and Jamf documentation links.

### Grant Full Disk Access

Follow [Step 6: Grant Full Disk Access to Microsoft Defender for Endpoint](mac-jamfpro-policies#step-6-grant-full-disk-access-to-microsoft-defender-for-endpoint). The current profile grants access to all required Defender components, including `com.microsoft.dlp.daemon`.

### Approve system extensions

Follow [Step 7: Approve system extensions for Microsoft Defender for Endpoint](mac-jamfpro-policies#step-7-approve-system-extensions-for-microsoft-defender-for-endpoint). The profile approves the endpoint security and network system extensions using Microsoft Team ID `UBF8T346G9`.

### Configure the network extension

Follow [Step 8: Configure the network extension](mac-jamfpro-policies#step-8-configure-network-extension). Use the current Microsoft-maintained `netfilter.mobileconfig` profile and the current Jamf Pro configuration-profile upload instructions linked from that section.