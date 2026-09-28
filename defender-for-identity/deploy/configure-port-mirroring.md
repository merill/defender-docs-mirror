---
layout: Conceptual
title: Configure port mirroring - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/deploy/configure-port-mirroring
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: Learn about Defender for Identity port mirroring options.
ms.date: 2026-06-15T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: martin77s
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: e2042451-5449-56a3-b522-e415ff51070a
document_version_independent_id: e2042451-5449-56a3-b522-e415ff51070a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/deploy/configure-port-mirroring.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: deploy/configure-port-mirroring
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/deploy/configure-port-mirroring.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: 247c1f3f-b369-60a4-3750-aa5b627cfb4d
---

# Configure port mirroring - Microsoft Defender for Identity | Microsoft Learn

This article describes port mirroring options for Microsoft Defender for Identity, and is relevant only for standalone sensors. Defender for Identity mainly uses deep packet inspection over network traffic to and from your domain controllers. For Defender for Identity standalone sensors to see network traffic, you must either configure port mirroring, or use a Network TAP. Port mirroring copies the traffic from one port (the source port) to another port (the destination port).

When using port mirroring, configure port mirroring for each domain controller that you're monitoring as the source of your network traffic. We recommend working with your networking or virtualization team to configure port mirroring.

Important

Defender for Identity standalone sensors do not support the collection of Event Tracing for Windows (ETW) log entries that provide the data for multiple detections. For full coverage of your environment, we recommend deploying the Defender for Identity sensor.

## Choose a port mirroring method

Your domain controllers and Defender for Identity standalone sensor can be either physical or virtual. The following are common methods for port mirroring and some considerations. Your switch manufacturer might use different terminology. Refer to your specific switch or virtualization server product documentation for detailed configuration steps.

| Method | Description |
| --- | --- |
| **Switched Port Analyzer (SPAN)** | Copies network traffic from one or more switch ports to another switch port on the same switch. Both the Defender for Identity standalone sensor and domain controllers must be connected to the same physical switch. |
| **Remote Switch Port Analyzer (RSPAN)** | Allows you to monitor network traffic from source ports distributed over multiple physical switches. RSPAN copies the source traffic into a special RSPAN configured VLAN. This VLAN needs to be trunked to the other switches involved. RSPAN works at Layer 2. |
| **Encapsulated Remote Switch Port Analyzer (ERSPAN)** | A Cisco proprietary technology working at Layer 3. ERSPAN allows you to monitor traffic across switches without the need for VLAN trunks and uses generic routing encapsulation (GRE) to copy monitored network traffic.  Defender for Identity currently cannot directly receive ERSPAN traffic. Instead:  1. Configure the ERSPAN destination where the traffic is decapsulated as a switch or router that can decapsulate the traffic.  1. Configure the switch or router to forward the decapsulated traffic to the Defender for Identity standalone sensor using either SPAN or RSPAN. |

Note

- If the domain controller being port mirrored is connected over a WAN link, make sure the WAN link can handle the additional load of the ERSPAN traffic.
- Defender for Identity only supports traffic monitoring when the traffic reaches the NIC and the domain controller in the same manner. Defender for Identity does not support traffic monitoring when the traffic is broken out to different ports.

## Supported port mirroring options

The following table describes Defender for Identity's support for port mirroring configurations:

| Defender for Identity standalone sensor | Domain controller | Considerations |
| --- | --- | --- |
| Virtual | Virtual on same host | The virtual switch needs to support port mirroring.Moving one of the virtual machines to another host by itself may break the port mirroring. |
| Virtual | Virtual on different hosts | Make sure your virtual switch supports this scenario. |
| Virtual | Physical | Requires a dedicated network adapter otherwise Defender for Identity sees all of the traffic coming in and out of the host, even the traffic the host sends to the Defender for Identity cloud service. |
| Physical | Virtual | Make sure your virtual switch supports this scenario - and port mirroring configuration on your physical switches based on the scenario:If the virtual host is on the same physical switch, you need to configure a switch level span.If the virtual host is on a different switch, you need to configure RSPAN or ERSPAN\*. |
| Physical | Physical on the same switch | Physical switch must support SPAN/Port Mirroring. |
| Physical | Physical on a different switch | Requires physical switches to support RSPAN or ERSPAN ERSPAN is only supported when decapsulation is performed before the traffic is analyzed by Defender for Identity. |

Note

The time on your domain controllers and the connected Defender for Identity sensor must be synchronized to within 5 minutes of eachother.