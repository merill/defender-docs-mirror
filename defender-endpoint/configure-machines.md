---
layout: Conceptual
title: Review device configuration in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/configure-machines
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Use Device configuration management in Microsoft Defender for Endpoint to review management, onboarding, attack surface, and web protection coverage.
ms.service: defender-endpoint
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.custom:
- admindeeplinkDEFENDER
- sfi-ga-nochange
- msecd-doc-authoring-1015
ms.topic: overview
ms.subservice: onboard
ms.date: 2026-09-15T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 7356fc06-9022-28ea-989b-fa8c343e4b82
document_version_independent_id: 7356fc06-9022-28ea-989b-fa8c343e4b82
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/configure-machines.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-machines
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/configure-machines.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/a72e95ff-4b4f-4cc1-90c6-7dcba67ff05f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/24dc3ccd-591a-4415-a1fe-8759afafcb12
platformId: 2fbb2d3f-864a-6fb3-7388-03f66502fcbb
---

# Review device configuration in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Device configuration management in Microsoft Defender for Endpoint (MDE) summarizes how endpoint security settings are managed and highlights gaps in onboarding and protection coverage. Use the dashboard to review your organization's devices and open the appropriate management experiences.

The cards you see depend on your enabled features, integrations, and permissions.

## Review device configuration management

On the **Device configuration management** page in the Microsoft Defender portal at https://security.microsoft.com/configuration_management, review the available cards:

- **Device security management**: Shows which security configuration management tool is used on devices, grouped by operating system. The data includes endpoints last seen in the past six months.
- **Onboarded via MDE security management**: Shows the onboarding and health status of devices managed through Defender for Endpoint security settings management.
- **Onboarded via Intune**: Compares Intune-managed devices that are onboarded to Defender for Endpoint with devices that aren't onboarded.
- **Attack surface management**: Provides access to attack surface management for devices.
- **Web protection coverage**: Summarizes device coverage for web content filtering policies and custom URL and domain indicators.

Depending on your environment, the page might also show a **Domain Controller Configuration** card.

## Choose a device management method

You can manage Defender security settings on devices enrolled in Intune or on supported devices that aren't enrolled in Intune.

Microsoft Intune is the recommended tool for configuring and distributing Defender for Endpoint features to devices. However, Intune is a separate product that isn't part of Defender for Endpoint, and it isn't included in all subscriptions. To enroll and manage devices with Intune, you need a subscription that includes it, or you can buy it separately as a standalone subscription or add-on. If you don't have an Intune subscription, use Defender for Endpoint security settings management to manage supported devices that aren't enrolled in Intune. For more information, see [Microsoft Intune licensing](/en-us/intune/fundamentals/licensing).

### Enroll devices in Intune

Intune-managed devices receive the policies and profiles you assign in Intune. Choose an enrollment method based on your device ownership and deployment scenario. For guidance, see [Windows device enrollment guide for Microsoft Intune](/en-us/intune/device-enrollment/windows/guide).

An Intune license is required for each user or device that benefits from the Intune service. For user-driven enrollment, assign the user an Intune license before enrollment. For instructions, see [Assign Microsoft Intune licenses](/en-us/intune/fundamentals/assign-licenses).

To connect the services and onboard devices through Intune, see [Configure Microsoft Defender for Endpoint with Intune and onboard devices](/en-us/intune/device-security/microsoft-defender/configure-integration).

### Manage devices that aren't enrolled in Intune

Defender for Endpoint security settings management uses Intune endpoint security policies to manage supported devices that are onboarded to Defender for Endpoint but aren't enrolled in Intune. The Defender for Endpoint subscription provides access to the **Endpoint security** area of the Intune admin center for this scenario.

For supported platforms, licensing requirements, and configuration instructions, see [Use Intune to manage Defender settings on devices that aren't enrolled in Intune](/en-us/intune/device-security/microsoft-defender/security-settings-management).

## Get the required permissions

Use a role with the least permissions required for each task:

- **Connect Intune and Defender for Endpoint**: In Intune, use the built-in **Endpoint Security Manager** role or a custom role with **Read** and **Modify** permissions for **Mobile Threat Defense**. In the Defender portal, use the **Security Administrator** role in Microsoft Entra ID or a Defender for Endpoint role with the **Manage security settings in Windows Security Center** permission.
- **Create and assign an endpoint detection and response policy**: Use **Endpoint Security Manager** or a custom Intune role with **Assign**, **Create**, **Delete**, **Read**, **Update**, and **View Reports** permissions for **Endpoint Detection and Response**.
- **Manage security baselines**: Use **Policy and Profile Manager** or a custom Intune role with **Assign**, **Create**, **Delete**, **Read**, and **Update** permissions for **Security baselines** and **Read** permission for **Organization**.

For complete integration requirements, see [Role-based access control prerequisites for Intune and Defender for Endpoint](/en-us/intune/device-security/microsoft-defender/overview#role-based-access-control).

To create a role with only the permissions your administrators need, see [Create a custom role in Intune](/en-us/intune/fundamentals/role-based-access-control/create-custom-role).

## More information

- [Get devices onboarded to Defender for Endpoint](configure-machines-onboarding): Track the onboarding status of Intune-managed devices and onboard more devices through Intune.
- [Increase compliance with the Defender for Endpoint security baseline](configure-machines-security-baseline): Create, assign, and monitor the Defender for Endpoint security baseline in Intune.
- [Monitor ASR rule activity](attack-surface-reduction-rules-monitor): Monitor attack surface reduction (ASR) rule events by using advanced hunting and the ASR rules report in the [Microsoft Defender portal](https://security.microsoft.com).