---
layout: Conceptual
title: Enhance your OT security with Defender for IoT - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/overview
breadcrumb_path: ../breadcrumb/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-iot-blog/bg-p/MicrosoftDefenderIoTBlog
feedback_help_link_type: ask-the-community
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
ms.service: defender-for-iot
author: limwainstein
manager: bagol
ms.author: lwainstein
description: Learn about Microsoft Defender for IoT's features for OT/IoT security for OT and Enterprise IoT networks.
ms.topic: overview
ms.date: 2025-01-30T00:00:00.0000000Z
ms.custom: enterprise-iot
locale: en-us
document_id: a2e27234-df4e-a16f-f06e-c0d6c0a5b47a
document_version_independent_id: b3c8dc07-a7f0-98a8-a147-ab87d34d432a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/overview.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 11acd6de-021a-0d8a-bea4-d857e631e850
---

# Enhance your OT security with Defender for IoT - Microsoft Defender for IoT | Microsoft Learn

Note

This article discusses Microsoft Defender for IoT in the Azure portal.

If you're a Microsoft Defender customer looking for a unified IT/OT experience, see the documentation for [Microsoft Defender for IoT in the Microsoft Defender portal (Preview) documentation](/en-us/defender-for-iot/).

Learn more about the [Defender for IoT management portals](/en-us/defender-for-iot/microsoft-defender-iot#what-are-the-different-management-portals-for-microsoft-defender-for-iot).

The Internet of Things (IoT) supports billions of connected devices that use both operational technology (OT) and IoT networks. IoT/OT devices and networks are often built using specialized protocols, and might prioritize operational challenges over security.

When IoT/OT devices can't be protected by traditional security monitoring systems, each new wave of innovation increases the risk and possible attack surfaces across those IoT devices and OT networks.

Microsoft Defender for IoT is a unified security solution built specifically to identify IoT and OT devices, vulnerabilities, and threats. Use Defender for IoT to secure your entire IoT/OT environment, including existing devices that might not have built-in security agents.

Defender for IoT provides agentless, network layer monitoring, and integrates with both industrial equipment and security operation center (SOC) tools.

![Diagram showing an example of Defender for IoT's end-to-end coverage solution.](media/overview/end-to-end-coverage.png)

## Agentless device monitoring for OT security

If your IoT and OT devices don't have embedded security agents, they might remain unpatched, misconfigured, and invisible to IT and security teams. Unmonitored devices can be soft targets for threat actors looking to pivot deeper into corporate networks.

Defender for IoT uses agentless monitoring to provide visibility and security across your network, and identifies specialized protocols, devices, or machine-to-machine (M2M) behaviors.

- **Discover IoT/OT devices** in your network, their details, and how they communicate. Gather data from network sensors, Microsoft Defender for Endpoint, and third-party sources.
- **Assess risks and manage vulnerabilities** using machine learning, threat intelligence, and behavioral analytics. For example:

    - Identify unpatched devices, open ports, unauthorized applications, unauthorized connections, changes to device configurations, PLC code, firmware, and more.
    - Run searches in historical traffic across all relevant dimensions and protocols. Access full-fidelity PCAPs to drill down further.
    - Detect advanced threats that you might have missed by static indicators of compromise (IOCs), such as zero-day malware, fileless malware, and living-off-the-land tactics.
- **Respond to threats** by integrating with Microsoft services such as Microsoft Sentinel, other partner systems, and APIs. Integrate with security information and event management (SIEM) services, security operations and response (SOAR) services, extended detection and response (XDR) services, and more.

Defender for IoT's centralized user experience in the Azure portal lets the security and OT monitoring teams visualize and secure all their IT, IoT, and OT devices regardless of where the devices are located.

## Support for cloud, on-premises, and hybrid OT networks

Install OT network sensors on-premises, at strategic locations in your network to detect devices across your entire OT environment. Then, use any of the following configurations to view your devices and security value:

- **Cloud services**:

    While OT network sensors have their own UI console that displays details and security data about detected devices, connect your sensors to Azure to extend your journey to the cloud.

    From the Azure portal, view data from all connected sensors in a central location, and integrate with other Microsoft services, like Microsoft Sentinel.
- **Air-gapped and on-premises services**:

    If you have an air-gapped environment and want to keep all your OT network data fully on-premises, connect your OT network sensors to the OT sensor console using the UI or CLI commands for central visibility and control.

    Continue to view detailed device data and security value in each sensor console.
- **Hybrid services**:

    You might have hybrid network requirements where you can deliver some data to the cloud and other data must remain on-premises.

    In this case, set up your system in a flexible and scalable configuration to fit your needs. Connect some of your OT sensors to the cloud and view data on the Azure portal, and keep other sensors managed on-premises only.

For more information, see [System architecture for OT system monitoring](architecture).

## Protect enterprise IoT networks

Extend Defender for IoT's agentless security features beyond OT environments to enterprise IoT devices by using enterprise IoT security with Microsoft Defender for Endpoint, and view related alerts, vulnerabilities, and recommendations for IoT devices in Microsoft Defender.

Enterprise IoT devices can include devices such as printers, smart TVs, and conferencing systems and purpose-built, proprietary devices.

For more information, see [Securing IoT devices in the enterprise](concept-enterprise).

## Supported service regions

Defender for IoT routes all traffic from all European regions to the *West Europe* regional datacenter. It routes traffic from all remaining regions to the *East US* regional datacenter.