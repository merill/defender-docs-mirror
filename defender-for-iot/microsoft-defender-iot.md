---
layout: Conceptual
title: What is Microsoft Defender for IoT in the Defender portal? - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-iot/microsoft-defender-iot
breadcrumb_path: /defender-for-iot/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Microsoft Defender for IoT in the Defender portal is a unified security solution built specifically to identify IoT and OT devices, vulnerabilities, and threats.
ms.service: defender-for-iot
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.topic: concept-article
ms.date: 2024-06-11T00:00:00.0000000Z
locale: en-us
document_id: 833d341f-fc22-ee28-037c-cf6177a6a6be
document_version_independent_id: 833d341f-fc22-ee28-037c-cf6177a6a6be
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot/microsoft-defender-iot.md
site_name: Docs
depot_name: Learn.defender-for-iot
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: microsoft-defender-iot
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot/microsoft-defender-iot.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 4a6a50d4-864f-0ca2-fa5a-909d0b76c074
---

# What is Microsoft Defender for IoT in the Defender portal? - Microsoft Defender for IoT | Microsoft Learn

Operational Technology (OT) involves the specialized hardware and software used to monitor and control physical processes in critical sectors such as manufacturing, utilities, pharmaceuticals, and more. Microsoft Defender for IoT, available within the Microsoft Defender portal, is designed to secure OT environments, including networks, devices, vulnerabilities, and threats crucial for maintaining operational reliability and safety.

In this article, you learn how Microsoft Defender customers can extend their protection to OT environments by leveraging Defender for IoT in the Defender portal.

Important

This article discusses Microsoft Defender for IoT in the Defender portal (Preview).

Some features are not yet available in the Defender portal. If you're interested in these features, or you're an existing customer working on the Azure portal, see the [Defender for IoT on Azure documentation](/en-us/azure/defender-for-iot/organizations/overview).

Learn more about the [Defender for IoT management portals](/en-us/defender-for-iot/microsoft-defender-iot#what-are-the-different-management-portals-for-microsoft-defender-for-iot).

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## What are the different management portals for Microsoft Defender for IoT?

You can work with these different management portals:

| Portal | Details | Next steps |
| --- | --- | --- |
| Defender for IoT in the Defender portal (Preview) | Microsoft Defender customers can use this portal for a unified IT/OT experience, extending Defender XDR protection to OT environments. Learn about the main use cases. | [Get started](get-started) with Defender for IoT in the Defender portal. |
| Defender for IoT in the classic, Azure portal | All customers can use this portal to identify OT devices, vulnerabilities, and threats in the Azure portal. | See the [Defender for IoT on Azure overview](/en-us/azure/defender-for-iot/organizations/overview). |

Protection for enterprise IoT devices is available for Microsoft Defender customers. These customers can enable protection for enterprise IoT devices, like printers, smart TVs, and conferencing systems and purpose-built, proprietary devices. [Get started](/en-us/defender-for-iot/enterprise-iot-get-started) with enterprise IoT monitoring.

## Who uses Defender for IoT?

Defender for IoT is intended for:

- **CISOs** or security leaders that want to gain an overview of their organization's OT network and security.
- **OT security admins, industrial engineers, risk managers, and SOC analysts** that want to gain a high-level view of a site's risks, incidents, and vulnerabilities, get recommendations for remediation actions, manage and discover protected OT devices, and more.

## What are the main OT security challenges?

OT network challenges include: poor visibility into assets and networks, difficulty to create network segmentation, vulnerable legacy systems, dependence on external vendors, and lack of security expertise. When OT devices can't be protected by traditional security monitoring systems, each new wave of innovation increases the risk and possible attack surfaces across those networks.

## How does it work?

Defender for IoT in the Defender portal uses the following combination of technology built into Microsoft Defender for Endpoint and Microsoft's cloud service:

- **Endpoint network sensors**: Embedded in Windows 10, these sensors collect and process IoT/OT network signals and send sensor data to your cloud tenant.
- **Cloud security analytics**: Leveraging big-data and device learning, network signals are translated into insights, detections, and recommended responses to advanced threats.
- **Threat intelligence**: Generated by Microsoft OT security research teams, and augmented by threat intelligence provided by partners, threat intelligence enables Defender for IoT to identify IoT/OT attacks and techniques and generate alerts when they are observed.

## What are the main Defender for IoT use cases?

| Use case | Capabilities |
| --- | --- |
| **[Discover OT devices](manage-devices-inventory)** | Gather OT network data from Microsoft Defender for Endpoint; identify and manage OT devices. |
| **[Get an overview of your productions sites (site security)](site-security-overview)** | Get an overview of your production sites to gain insights into OT risks, make better-informed security investment decisions, and streamline communication between stakeholders. |
| **[Prioritize and remediate vulnerabilities](prioritize-vulnerabilities)** | Proactively manage OT network risks based on vulnerability details and recommended remediation advice. |
| **[Analyze incidents](investigate-threats) and respond to threats** | Review incidents and alerts with real-time details about events logged in your OT network and take recommended remediation actions. |
| **Extend Microsoft Defender** | Microsoft Defender and Defender for IoT form a unified pre- and post-breach enterprise defense suite. This suite natively integrates with endpoint, IoT/OT, identity, email, and applications to detect, prevent, investigate, and automatically respond to sophisticated attacks. |