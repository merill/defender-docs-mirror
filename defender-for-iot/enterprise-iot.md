---
layout: Conceptual
title: Enterprise IoT for Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-iot/enterprise-iot
breadcrumb_path: /defender-for-iot/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to monitor IoT devices using Microsoft Enterprise IoT in the Microsoft Defender portal.
ms.service: defender-for-iot
author: limwainstein
ms.author: lwainstein
ms.localizationpriority: medium
ms.date: 2024-08-25T00:00:00.0000000Z
ms.topic: overview
locale: en-us
document_id: 006c686d-15cf-c964-b138-0f50d502ef78
document_version_independent_id: 006c686d-15cf-c964-b138-0f50d502ef78
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot/enterprise-iot.md
site_name: Docs
depot_name: Learn.defender-for-iot
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: enterprise-iot
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot/enterprise-iot.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 7915d8a8-0416-b2a2-5b33-755dd23e1812
---

# Enterprise IoT for Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn

The number of IoT devices continues to grow exponentially across enterprise networks in many office buildings. Enterprise IoT devices include devices such as printers, smart TVs, Voice over Internet Protocol (VoIP) devices, conferencing systems and purpose-built, proprietary devices.

While the number of IoT devices continues to grow, they often lack the security safeguards that are common on managed endpoints like laptops and mobile phones. To bad actors, these unmanaged devices can be used as a point of entry for lateral movement or evasion, and too often, the use of such tactics leads to the exfiltration of sensitive information.

Important

This article discusses Microsoft Defender for IoT in the Defender portal (Preview).

Some features are not yet available in the Defender portal. If you're interested in these features, or you're an existing customer working on the Azure portal, see the [Defender for IoT on Azure documentation](/en-us/azure/defender-for-iot/organizations/overview).

Learn more about the [Defender for IoT management portals](/en-us/defender-for-iot/microsoft-defender-iot#what-are-the-different-management-portals-for-microsoft-defender-for-iot).

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Enterprise IoT monitoring in the Defender portal

Extend Microsoft Defender for IoT's security features to include enterprise IoT devices. Add the enterprise IoT security feature to your existing Microsoft Defender for Endpoint license, and view related vulnerabilities and recommendations for IoT devices that are seamlessly integrated into the Microsoft Defender portal.

![The architecture showing the use of enterprise IoT](media/enterprise-iot/eiot-architecture.png)

## What's the difference between OT security and enterprise IoT security?

- Operational Technology (OT): OT network sensors use agentless, patented technology to discover, learn, and continuously monitor network devices for deep visibility into OT / Industrial Control System (ICS) risks. Sensors carry out data collection, analysis, and alerting on-site, making them ideal for locations with low bandwidth or high latency.
- Enterprise IoT: Enterprise IoT provides visibility and security for IoT devices in the corporate environment. Enterprise IoT network protection extends agentless features beyond operational environments, providing coverage for all IoT devices in your environment, such as printers, cameras, and purpose-built, proprietary, devices.

## Enterprise IoT data in the Defender portal

Enterprise IoT data for features such as recommendations and vulnerabilities, seamlessly integrates with other data in the Defender portal.

### Recommendations

The following Defender for Endpoint security recommendations are supported for enterprise IoT devices:

- Require authentication for Telnet management interface
- Disable insecure administration protocol – Telnet
- Remove insecure administration protocols SNMP V1 and SNMP V2
- Require authentication for VNC management interface

### Vulnerabilities

Known CVE vulnerabilities, already detected by the Defender portal, are also detected and displayed associated with the relevant enterprise IoT device in the Defender portal. Known CVEs can help you decide whether to patch, remove, or contain the device and mitigate risk to your network. Alternatively, use advanced hunting queries to collect vulnerabilities across all your devices.