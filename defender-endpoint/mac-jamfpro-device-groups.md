---
layout: Conceptual
title: Set up device groups for Microsoft Defender for Endpoint in Jamf Pro - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/mac-jamfpro-device-groups
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to create Jamf Pro computer groups to target Microsoft Defender for Endpoint profiles and policies to specific macOS devices.
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
ms.subservice: macos
ms.date: 2026-09-17T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
locale: en-us
document_id: cf700801-e77b-19ed-c46b-c38c609b6f56
document_version_independent_id: cf700801-e77b-19ed-c46b-c38c609b6f56
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/mac-jamfpro-device-groups.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mac-jamfpro-device-groups
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/mac-jamfpro-device-groups.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 73ccce86-c97c-945a-a6f0-da857faeac2f
---

# Set up device groups for Microsoft Defender for Endpoint in Jamf Pro - Microsoft Defender for Endpoint | Microsoft Learn

Use static or smart computer groups in Jamf Pro to target Microsoft Defender for Endpoint configuration profiles and deployment policies to specific macOS devices.

Jamf Pro is a separate product that isn't part of Defender for Endpoint and isn't included with Defender for Endpoint subscriptions. To use these procedures, your organization needs a separate Jamf Pro subscription. For product and subscription information, see [Jamf Pro](https://www.jamf.com/products/jamf-pro/). If your organization doesn't use Jamf Pro, you can [deploy Defender for Endpoint with Microsoft Intune](mac-install-with-intune) or [use another MDM solution](mac-install-with-other-mdm).

Important

Microsoft provides information about Jamf Pro to support integration scenarios but doesn't provide troubleshooting support for this third-party product. For issues specific to Jamf Pro, contact Jamf support.

Note

These deployment instructions apply to Defender for Endpoint Plan 1 and Plan 2.

## Prerequisites

Before you create computer groups, make sure you meet the following requirements:

- You can sign in to your organization's Jamf Pro instance.
- Your Jamf Pro account has permission to create and manage computer groups.
- You identified the macOS devices that should receive the Defender for Endpoint configuration profiles and deployment policies.

## Create computer groups in Jamf Pro

Create one or more computer groups for the macOS devices where you plan to deploy Defender for Endpoint. Choose the group type that fits how you manage membership:

- **Static computer group**: Manually assign a fixed set of computers. For current Jamf Pro instructions, see [Creating a Static Group](https://learn.jamf.com/r/jamf-pro-documentation-current/Creating_a_Static_Group).
- **Smart computer group**: Define criteria that Jamf Pro uses to determine membership. For current Jamf Pro instructions, see [Creating a Smart Group](https://learn.jamf.com/r/jamf-pro-documentation-current/Creating_a_Smart_Group).

Use the computer groups as the scope when you [deploy and configure Defender for Endpoint on macOS with Jamf Pro](mac-jamfpro-policies).

For the initial deployment, don't base smart group membership on whether Defender for Endpoint is installed. The required configuration profiles must be delivered before the Defender for Endpoint package is installed.