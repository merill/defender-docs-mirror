---
layout: Conceptual
title: Get devices onboarded to Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/configure-machines-onboarding
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Track onboarding of Intune-managed devices to Microsoft Defender for Endpoint and increase onboarding rate.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.topic: install-set-up-deploy
ms.subservice: onboard
ms.date: 2026-09-15T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 99712f9c-e9c2-793a-8d52-dcbb0608d58f
document_version_independent_id: 99712f9c-e9c2-793a-8d52-dcbb0608d58f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/configure-machines-onboarding.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-machines-onboarding
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/configure-machines-onboarding.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 365eea15-5e1c-8902-1552-32350ee405b2
---

# Get devices onboarded to Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Each onboarded device adds an additional endpoint detection and response (EDR) sensor and increases visibility over breach activity in your network. Onboarding also ensures that a device can be checked for vulnerable components, for security configuration issues, and can receive critical remediation actions during attacks.

Defender for Endpoint supports [multiple onboarding methods](deployment-strategy#step-2-select-your-deployment-method). For cloud-native and Intune-managed environments, [Microsoft Intune is the recommended approach](deployment-strategy#step-1-identify-your-architecture).

Before you begin, review the following prerequisites in the Intune documentation:

- [Review licensing and platform requirements](/en-us/intune/intune-service/protect/microsoft-defender-with-intune#prerequisites) for the Intune-Defender integration, including supported platforms and enrollment requirements
- [Ensure you have the necessary permissions](/en-us/intune/intune-service/protect/microsoft-defender-integrate#connect-microsoft-defender-for-endpoint-to-intune). The required roles are Endpoint Security Manager in Intune and Security Administrator in Microsoft Entra ID.

## Discover and track unprotected devices

On the **Device configuration management** page in the Microsoft Defender portal at https://security.microsoft.com/configuration_management, the **Onboarded via Intune** card provides a high-level view of your onboarding rate. The card compares the number of Intune-managed Windows devices onboarded to Defender for Endpoint with the total number of Intune-managed Windows devices.

Note

If you used Configuration Manager, the onboarding script, or other onboarding methods that don't use Intune profiles, you might encounter data discrepancies. To resolve these discrepancies, create a corresponding Intune configuration profile for Defender for Endpoint onboarding and assign that profile to your devices.

## Onboard more devices with Intune policies

Selecting **Onboard more devices** on the card opens the **Endpoint security | Microsoft Defender for Endpoint** page in the Microsoft Intune admin center at [https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/~/atp](https://intune.microsoft.com/#view/Microsoft_Intune_Workflows/SecurityManagementMenu/%7E/atp). This page controls the service-to-service connection between Intune and Defender for Endpoint and determines which device platforms participate in the integration. Deploying policies to onboard devices is a separate step done elsewhere in Intune.

To configure this connection and deploy onboarding policies, see [Configure Microsoft Defender for Endpoint with Intune and onboard devices](/en-us/intune/intune-service/protect/microsoft-defender-integrate) (opens in a new tab in the Intune documentation).