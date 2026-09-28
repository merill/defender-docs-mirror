---
layout: Conceptual
title: IoT/OT security - protect enterprise IoT and OT assets - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/protect-against-iot-ot-threats
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how Defender for IoT detects and monitors IoT and OT devices to protect your environment against threats raised by IoT and OT devices.
ms.service: defender-xdr
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.topic: article
ms.date: 2024-01-20T00:00:00.0000000Z
locale: en-us
document_id: 099e2c74-4904-a205-a609-e718510d92e3
document_version_independent_id: 099e2c74-4904-a205-a609-e718510d92e3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/protect-against-iot-ot-threats.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: protect-against-iot-ot-threats
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/protect-against-iot-ot-threats.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
platformId: 04fecc83-6e0e-9efd-6cfe-fd25db055f4d
---

# IoT/OT security - protect enterprise IoT and OT assets - Microsoft Defender XDR | Microsoft Learn

The Internet of Things (IoT) connects billions of smart devices used in homes and businesses, while Operational Technology (OT) focuses on industrial systems like factory equipment and critical infrastructure. Securing OT/IoT environments comes with unique challenges, like unmanaged devices, increased attack surfaces, and the absence of traditional security controls (review more security challenges).

To maintain operational reliability and safety, organizations must use [tailored IoT/OT security approaches](/en-us/defender-for-iot/microsoft-defender-iot) due to the unique risks in these environments. Microsoft Defender for IoT addresses these unique risks, providing comprehensive OT security, including visibility into OT environments and advanced threat protection.

In this article, you learn about IoT/OT security challenges, and how Defender leverages Defender for IoT to detect and monitor enterprise IoT and OT devices.

Note

Microsoft E5 and E5 Security customers can enable enterprise IoT security as part of their license. Learn more about the Enterprise IoT device protection supported for different licenses.

## Enterprise IoT security challenges

When IoT/OT devices can't be protected by traditional security monitoring systems, each new wave of innovation increases the risk and possible attack surfaces across those IoT devices and OT networks.

Specifically, enterprise IoT security challenges include:

- Lack of visibility into unmanaged IoT devices, which create significant blind spots and increase the enterprise attack surface.
- Complex device authentication and identity management, where traditional security models like password-based authentication are often insufficient.
- Large amounts of sensitive data with insufficient data encryption.
- Lack of built-in security controls and security best practices, making enterprise IoT devices easy targets for sophisticated attacks.
- Limited computational capacity, making it difficult to implement standard security measures like encryption, authentication, and firmware updates.

## Enterprise IoT device protection in Defender for Endpoint and Defender

[Enterprise IoT security](/en-us/defender-for-iot/enterprise-iot) in Microsoft Defender for Endpoint and Defender provides IoT-specific security value for IoT devices, including risk and exposure levels, vulnerabilities, and recommendations.

While monitoring endpoints on the network, the existing Defender for Endpoint agent detects, identifies, assesses, and secures enterprise IoT assets on the monitored endpoints.

This table describes the supported protection for different licenses.

| License | Device discovery | Threat detection - managed/unmanaged devices | VM | Security recommendations | How to enable |
| --- | --- | --- | --- | --- | --- |
| Microsoft Defender for Endpoint P2 | ✅ | ✅ | ❌ | ❌ | - [Start with a free trial](/en-us/defender-for-iot/enterprise-iot-get-started#set-up-a-standalone-trial-license)- Purchase the [standalone full license](/en-us/defender-for-iot/enterprise-iot-get-started#set-up-a-standalone-full-license). |
| Enterprise IoT add-on device license (add-on to MDE P2) | ✅ | ✅ | ✅ | ✅ | [Enable enterprise IoT security](/en-us/defender-for-iot/enterprise-iot-get-started#add-enterprise-iot-security-in-the-defender-portal) |
| E5^1^ | ✅ | ✅ | ✅ | ✅ | [Enable enterprise IoT security](/en-us/defender-for-iot/enterprise-iot-get-started#add-enterprise-iot-security-in-the-defender-portal) |

^1^Includes the MDE P2 license and the enterprise IoT add-on. Each E5 user license supports five enterprise IoT add-on device licenses.

### Supported devices

Enterprise IoT protection includes devices connected to an IT network (for example, Voice over Internet Protocol (VoIP), printers, and smart TVs).

### Main features

| Feature | Location | More details |
| --- | --- | --- |
| Discover enterprise IoT assets for a full enterprise IoT inventory | **Assets &gt; Devices &gt; IoT devices** | [Device inventory overview](/en-us/defender-endpoint/machines-view-overview) |
| Review alerts triggered by enterprise IoT assets | **Device details** page &gt; **Alerts** tab | - Learn more about [Defender for Endpoint alerts](/en-us/defender-endpoint/review-alerts).- Simulate alerts in Microsoft 365 Defender for Enterprise IoT using the Raspberry Pi scenario available in the Microsoft 365 Defender [Evaluation & Tutorials page](https://security.microsoft.com/tutorials/all). |
| Review security recommendations for enterprise IoT assets | **Device details** page &gt; **Security recommendations** tab | [Security recommendations in Defender for Endpoint](/en-us/defender-endpoint/device-discovery#vulnerability-assessment-on-discovered-devices) |
| Discover vulnerabilities associated with enterprise IoT assets | **Device details** page &gt; **Discovered vulnerabilities** tab | [Vulnerabilities in your organization](/en-us/defender-vulnerability-management/tvm-weaknesses) |
| Use advanced hunting queries to [create custom alert rules](/en-us/defender-for-iot/enterprise-iot-manage#advanced-hunting-queries-for-enterprise-iot) or to [collect vulnerabilities](/en-us/defender-for-iot/enterprise-iot-manage#advanced-hunting-queries-for-enterprise-iot) across all your devices | **Advanced hunting** page in the Defender portal |  |

## Extend protection to OT devices

To go beyond the protection that the Defender for Endpoint agent provides for enterprise IoT assets, Defender for IoT provides full visibility and security protection into OT assets in relevant internal networks.

For more information:

- [Onboard Defender for IoT](/en-us/defender-for-iot/get-started) to enable OT protection.
- Learn about the [OT-specific security use-cases](/en-us/defender-for-iot/microsoft-defender-iot#what-are-the-main-defender-for-iot-use-cases) that Defender for IoT addresses.