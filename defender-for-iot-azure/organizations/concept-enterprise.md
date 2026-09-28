---
layout: Conceptual
title: Secure IoT devices - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/concept-enterprise
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
description: Learn how integrating Microsoft Defender for Endpoint and Microsoft Defender for IoT's security content enhances your IoT network security.
ms.topic: concept-article
ms.date: 2023-09-13T00:00:00.0000000Z
ms.custom: enterprise-iot
locale: en-us
document_id: 35aa8050-2308-c1ac-1380-bee0cffc17d4
document_version_independent_id: 05ee3b8f-b302-2abb-34cb-d7793804eb24
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/concept-enterprise.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/concept-enterprise
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/concept-enterprise.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 88595ae6-df5a-080e-db7b-8ba9e7fff559
---

# Secure IoT devices - Microsoft Defender for IoT | Microsoft Learn

The number of IoT devices continues to grow exponentially across enterprise networks, such as printers, Voice over Internet Protocol (VoIP) devices, smart TVs, and conferencing systems scattered around many office buildings.

While the number of IoT devices continues to grow, they often lack the security safeguards that are common on managed endpoints like laptops and mobile phones. To bad actors, these unmanaged devices can be used as a point of entry for lateral movement or evasion, and too often, the use of such tactics leads to the exfiltration of sensitive information.

[Microsoft Defender for IoT](./) seamlessly integrates with [Microsoft Defender](/en-us/microsoft-365/security/defender) and [Microsoft Defender for Endpoint](/en-us/microsoft-365/security/defender-endpoint/) to provide both IoT device discovery and security value for IoT devices, including purpose-built recommendations, and vulnerability data.

## Enterprise IoT security in Microsoft Defender

Enterprise IoT security in Microsoft Defender provides IoT-specific security value, including risk and exposure levels, vulnerabilities, and recommendations in Microsoft Defender.

- If you're a Microsoft 365 E5 (ME5)/ E5 Security and Defender for Endpoint P2 customer, [toggle on support](eiot-defender-for-endpoint) for **Enterprise IoT Security** in the Microsoft Defender Portal.
- If you don't have ME5/E5 Security licenses, but you're a Microsoft Defender for Endpoint customer, start with a [free trial](billing#enterprise-iot-free-trial) or purchase standalone, per-device licenses to gain the same IoT-specific security value.

![Diagram of the service architecture when you have an Enterprise IoT plan added to Defender for Endpoint.](media/enterprise-iot/architecture-endpoint-only.png)

### Recommendations

The following Defender for Endpoint security recommendations are supported for Enterprise IoT devices:

- **Require authentication for Telnet management interface**
- **Disable insecure administration protocol – Telnet**
- **Remove insecure administration protocols SNMP V1 and SNMP V2**
- **Require authentication for VNC management interface**

For more information, see [Security recommendations](/en-us/microsoft-365/security/defender-vulnerability-management/tvm-security-recommendation).

## Frequently asked questions

This section provides a list of frequently asked questions about securing Enterprise IoT networks with Microsoft Defender for IoT.

### What is the difference between OT and Enterprise IoT?

- **Operational Technology (OT)**: OT network sensors use agentless, patented technology to discover, learn, and continuously monitor network devices for a deep visibility into Operational Technology (OT) / Industrial Control System (ICS) risks. Sensors carry out data collection, analysis, and alerting on-site, making them ideal for locations with low bandwidth or high latency.
- **Enterprise IoT**: Enterprise IoT provides visibility and security for IoT devices in the corporate environment.

    Enterprise IoT network protection extends agentless features beyond operational environments, providing coverage for all IoT devices in your environment. For example, an enterprise IoT environment might include printers, cameras, and purpose-built, proprietary, devices.

### Which devices are supported for Enterprise IoT security?

Enterprise IoT security encompasses a broad spectrum of devices, identified by Defender for Endpoint using both passive and active discovery methods.

The supported devices include an extensive range of hardware models and vendors, spanning corporate IoT devices such as printers, cameras, and VoIP phones, among others.

For more information, see [Defender for IoT devices](billing#defender-for-iot-devices).

### How can I start using Enterprise IoT?

Microsoft E5 (ME5) and E5 Security customers already have devices supported for enterprise IoT security. If you only have a Defender for Endpoint P2 license, you can purchase standalone, per-device licenses for enterprise IoT monitoring, or use a trial.

For more information, see:

- [Get started with enterprise IoT monitoring in Microsoft Defender](eiot-defender-for-endpoint)
- [Manage enterprise IoT monitoring support with Microsoft Defender for IoT](manage-subscriptions-enterprise)

### What permissions do I need to use Enterprise IoT security with Defender for IoT?

For information on required permissions, see [Prerequisites](eiot-defender-for-endpoint#prerequisites).

### Which devices are billable?

For more information, see [Devices monitored by Defender for IoT](architecture#devices-monitored-by-defender-for-iot).

### How should I estimate the number of devices I want to monitor?

For more information, see [Calculate monitored devices for Enterprise IoT monitoring](manage-subscriptions-enterprise#calculate-monitored-devices-for-enterprise-iot-monitoring).

### How can I cancel Enterprise IoT?

For more information, see [Turn off enterprise IoT security](manage-subscriptions-enterprise#turn-off-enterprise-iot-security).

### What happens when the trial ends?

If you haven't added a standalone license by the time your trial ends, your trial is automatically canceled, and you lose access to Enterprise IoT security features.

For more information, see [Defender for IoT subscription billing](billing).

### How can I resolve billing issues associated with my Defender for IoT plan?

For any billing or technical issues, open a support ticket for Microsoft Defender.