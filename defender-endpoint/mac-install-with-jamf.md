---
layout: Conceptual
title: Deploy Microsoft Defender for Endpoint on macOS with Jamf Pro - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/mac-install-with-jamf
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to use Jamf Pro to deploy Microsoft Defender for Endpoint on macOS, configure required profiles and policies, and enroll devices.
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
ms.custom: msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: a1aeb88e-a899-2137-7122-354df50cfd00
document_version_independent_id: a1aeb88e-a899-2137-7122-354df50cfd00
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/mac-install-with-jamf.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mac-install-with-jamf
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/mac-install-with-jamf.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 68edb020-b831-4d29-79a0-d3ad4cfb7e26
---

# Deploy Microsoft Defender for Endpoint on macOS with Jamf Pro - Microsoft Defender for Endpoint | Microsoft Learn

You can use Jamf Pro to deploy the Microsoft Defender for Endpoint installation package and required configuration profiles to organization-owned macOS devices.

Jamf Pro is a separate product that isn't part of Defender for Endpoint and isn't included with Defender for Endpoint subscriptions. To use these procedures, your organization needs a separate Jamf Pro subscription. For product and subscription information, see [Jamf Pro](https://www.jamf.com/products/jamf-pro/). To compare this method with [Microsoft Intune](mac-install-with-intune), [another mobile device management (MDM) solution](mac-install-with-other-mdm), or [manual deployment](mac-install-manually), see [Deploy Defender for Endpoint on macOS](microsoft-defender-endpoint-mac#deploy-defender-for-endpoint-on-macos).

Important

This article contains information about third-party tools. This is provided to help complete integration scenarios, however, Microsoft does not provide troubleshooting support for third-party tools.  Contact the third-party vendor for support.

## Prerequisites

Before you begin the Jamf Pro deployment, make sure you meet the following requirements:

- Review the [Defender for Endpoint on macOS prerequisites](microsoft-defender-endpoint-mac-prerequisites), including licensing, supported macOS versions, system extensions and permissions, and network connectivity.
- Verify that your organization has a Jamf Pro subscription.
- Verify that your Jamf Pro account can manage computer groups, configuration profiles, policies, packages, scripts, and enrollment.
- Sign in to your organization's Jamf Pro instance.

## Deploy Defender for Endpoint using Jamf Pro

Complete the deployment articles in this order:

1. [Set up device groups for Defender for Endpoint in Jamf Pro](mac-jamfpro-device-groups).
2. [Deploy and configure Defender for Endpoint on macOS with Jamf Pro](mac-jamfpro-policies).
3. [Enroll macOS devices in Jamf Pro for Defender for Endpoint](mac-jamfpro-enroll-devices).

Warning

Repackaging the Defender for Endpoint installation package is not a supported scenario. Doing so can negatively impact the integrity of the product and lead to adverse results, including but not limited to triggering tampering alerts and updates failing to apply.