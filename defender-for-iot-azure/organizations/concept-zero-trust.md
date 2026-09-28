---
layout: Conceptual
title: Zero Trust and your OT networks - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/concept-zero-trust
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
description: Learn about how implementing a Zero Trust security strategy with Microsoft Defender for IoT can protect your operational technology (OT) networks.
ms.date: 2024-05-22T00:00:00.0000000Z
ms.topic: concept-article
ms.collection:
- zerotrust-services
locale: en-us
document_id: 71540eb3-441f-27b4-99b8-111f25ad6c2c
document_version_independent_id: ba12a77f-57f2-6dbf-fdc2-f62124500561
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/concept-zero-trust.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/concept-zero-trust
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/concept-zero-trust.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: e1590823-f666-a8b3-ac62-76bdd222daeb
---

# Zero Trust and your OT networks - Microsoft Defender for IoT | Microsoft Learn

[Zero Trust](/en-us/security/zero-trust/zero-trust-overview) is a security strategy for designing and implementing the following sets of security principles:

| Verify explicitly | Use least privilege access | Assume breach |
| --- | --- | --- |
| Always authenticate and authorize based on all available data points. | Limit user access with Just-In-Time and Just-Enough-Access (JIT/JEA), risk-based adaptive policies, and data protection. | Minimize blast radius and segment access. Verify end-to-end encryption and use analytics to get visibility, drive threat detection, and improve defenses. |

Implement Zero Trust principles across your operational technology (OT) networks to help you with challenges, such as:

- Controlling remote connections into your OT systems, securing your network jump posts, and preventing lateral movement across your network
- Reviewing and reducing interconnections between dependent systems, simplifying identity processes, such as for contractors signing into your network
- Finding single points of failure in your network, identifying issues in specific network segments, and reducing delays and bandwidth bottlenecks

## Unique risks and challenges for OT networks

OT network architectures often differ from traditional IT infrastructure. OT systems use unique technology with proprietary protocols, and may have aging platforms and limited connectivity and power. OT networks also may have specific safety requirements and unique exposures to physical or local attacks, such as via external contractors signing into your network.

Since OT systems often support critical network infrastructures, they're often designed to prioritize physical safety or availability over secure access and monitoring. For example, your OT networks might function separately from other enterprise network traffic to avoid downtime for regular maintenance or to mitigate specific security issues.

As more OT networks migrate to cloud-based environments, applying Zero Trust principles may present specific challenges. For example:

- OT systems may not be designed for multiple users and role-based access policies, and may only have simple authentication processes.
- OT systems may not have the processing power available to fully apply secure access policies, and instead trust all traffic received as safe.
- Aging technology presents challenges in retaining organizational knowledge, applying updates, and using standard security analytics tools to get visibility and drive threat detection.

However, a security compromise in your mission critical systems can lead to real-world consequences beyond traditional IT incidents, and non-compliance can affect your organization's ability to conform to government and industry regulations.

## Applying Zero Trust principles to OT networks

Continue to apply the same Zero Trust principles in your OT networks as you would in traditional IT networks, but with some logistical modifications as needed. For example:

- **Make sure that all connections between networks and devices are identified and managed**, preventing unknown interdependencies between systems and containing any unexpected downtime during maintenance procedures.

    Since some OT systems may not support all of the security practices you need, we recommend limiting connections between networks and devices to a limited number of jump hosts. Jump hosts can then be used to start remote sessions with other devices.

    Make sure your jump hosts have stronger security measures and authentication practices, such as multi-factor authentication and privileged access management systems.
- **Segment your network to limit data access**, ensuring that all communication between devices and segments is encrypted and secured, and preventing lateral movement between systems. For example, make sure that all devices that access the network are pre-authorized and secured according to your organization's policies.

    You may need to trust communication across your entire industrial control and safety information systems (ICS and SIS). However, you can often further segment your network into smaller areas, making it easier to monitor for security and maintenance.
- **Evaluate signals like device location, health, and behavior**, using health data to gate access or flag for remediation. Require that devices must be up-to-date for access, and use analytics to get visibility and scale defenses with automated responses.
- **Continue to monitor security metrics**, such as authorized devices and your network traffic baseline, to ensure that your security perimeter retains its integrity and changes in your organization happen over time. For example, you may need to modify your segments and access policies as people, devices, and systems change.

## Zero Trust with Defender for IoT

Deploy [Microsoft Defender for IoT network sensors](architecture) to detect devices and monitor traffic across your OT networks. Defender for IoT assesses your devices for vulnerabilities and provides risk-based mitigation steps, and continuously monitors your devices for anomalous or unauthorized behavior.

When [deploying OT network sensors](onboard-sensors), use *sites*, and *zones* to segment your network.

- **Sites** reflect many devices grouped by a specific geographical location, such the office at a specific address.
- **Zones** reflect a logical segment within a site to define a functional area, such as a specific production line.

Assign each OT sensor to a specific site and zone to ensure that each OT sensor covers a specific area of the network. Segmenting your sensor across sites and zones helps you monitor for any traffic passing between segments and enforce security policies for each zone.

Make sure to assign [site-based access policies](manage-users-portal#manage-site-based-access-control-public-preview) so that you can provide least-privileged access to Defender for IoT data and activities.

For example, if your growing company has factories and offices in Paris, Lagos, Dubai, and Tianjin, you might segment your network as follows:

| Site | Zones |
| --- | --- |
| **Paris office** | - Ground floor (Guests) - Floor 1 (Sales) - Floor 2 (Executive) |
| **Lagos office** | - Ground floor (Offices) - Floors 1-2 (Factory) |
| **Dubai office** | - Ground floor (Convention center) - Floor 1 (Sales)- Floor 2 (Offices) |
| **Tianjin office** | - Ground floor (Offices) - Floors 1-2 (Factory) |