---
layout: Conceptual
title: Standalone sensor prerequisites - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/deploy/prerequisites-standalone
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
description: This article describes the prerequisites required for a successful Microsoft Defender for Identity deployment using a standalone sensor.
ms.date: 2023-11-26T00:00:00.0000000Z
ms.topic: install-set-up-deploy
ms.reviewer: rlitinsky
locale: en-us
document_id: 794db7e5-8fbe-b790-310c-83ad16c8b46e
document_version_independent_id: 794db7e5-8fbe-b790-310c-83ad16c8b46e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/deploy/prerequisites-standalone.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: deploy/prerequisites-standalone
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/deploy/prerequisites-standalone.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 0d77395c-3e5d-e7a2-e5b3-1d4f6185c426
---

# Standalone sensor prerequisites - Microsoft Defender for Identity | Microsoft Learn

This article lists prerequisites for deploying a Microsoft Defender for Identity standalone sensor where they differ from the [main deployment prerequisites](../prerequisites).

For more information, see [Plan capacity for Microsoft Defender for Identity deployment](../capacity-planning).

Important

Defender for Identity standalone sensors do not support the collection of Event Tracing for Windows (ETW) log entries that provide the data for multiple detections. For full coverage of your environment, we recommend deploying the Defender for Identity sensor.

## Extra system requirements for standalone sensors

Standalone sensors differ from Defender for Identity sensor [prerequisites](../prerequisites) as follows:

- Standalone sensors require a minimum of 5 GB of disk space
- Standalone sensors can also be installed on servers that are in a workgroup.
- Standalone sensors can support monitoring multiple domain controllers, depending on the amount of network traffic to and from the domain controllers.
- If you're working with [multiple forests](multi-forest), your standalone sensor machines must be allowed to communicate with all remote forest domain controllers using LDAP.

For information on using virtual machines with the Defender for Identity standalone sensor, see [Configure port mirroring](configure-port-mirroring).

## Network adapters for standalone sensors

Standalone sensors require at least one of each of the following network adapters:

- **Management adapters** - used for communications on your corporate network. The sensor uses this adapter to query the DC it's protecting and performing resolution to machine accounts.

    Configure management adapters with static IP addresses, including a default gateway, and preferred and alternate DNS servers.

    The **DNS suffix for this connection** should be the DNS name of the domain for each domain being monitored.

    Note

    If the Defender for Identity standalone sensor is a member of the domain, this may be configured automatically.
- **Capture adapter** - used to capture traffic to and from the domain controllers.

    Important

    - [Configure port mirroring](configure-port-mirroring) for the capture adapter as the destination of the domain controller network traffic. Typically, you need to work with the networking or virtualization team to configure port mirroring.
    - Configure a static non-routable IP address (with /32 mask) for your environment with no default sensor gateway and no DNS server addresses. For example: `10.10.0.10/32. This configuration ensures that the capture network adapter can capture the maximum amount of traffic and that the management network adapter is used to send and receive the required network traffic.

Note

If you run Wireshark on Defender for Identity standalone sensor, restart the Defender for Identity sensor service after you've stopped the Wireshark capture. If you don't restart the sensor service, the sensor stops capturing traffic.

If you attempt to install the Defender for Identity sensor on a machine configured with a NIC Teaming adapter, you receive an installation error. If you want to install the Defender for Identity sensor on a machine configured with NIC teaming, see [Defender for Identity sensor NIC teaming issue](../troubleshooting-known-issues#defender-for-identity-sensor-nic-teaming-issue).

### Ports for standalone sensors

The following table lists the extra ports that the Defender for Identity standalone sensor requires configured on the management adapter, in addition to ports listed for the [Defender for Identity sensor](../prerequisites#required-ports).

| Protocol | Transport | Port | From | To |
| --- | --- | --- | --- | --- |
| **Internal ports** |  |  |  |  |
| **LDAP** | TCP and UDP | 389 | Defender for Identity sensor | Domain controllers |
| **Secure LDAP (LDAPS)** | TCP | 636 | Defender for Identity sensor | Domain controllers |
| **LDAP to Global Catalog** | TCP | 3268 | Defender for Identity sensor | Domain controllers |
| **LDAPS to Global Catalog** | TCP | 3269 | Defender for Identity sensor | Domain controllers |
| **Kerberos** | TCP and UDP | 88 | Defender for Identity sensor | Domain controllers |
| **Windows Time** | UDP | 123 | Defender for Identity sensor | Domain controllers |
| **Syslog** (optional) | TCP/UDP | 514, depending on configuration | SIEM Server | Defender for Identity sensor |

## Windows event log requirements

Defender for Identity detection relies on specific [Windows Event logs](configure-windows-event-collection) that the sensor parses from your domain controllers. For the correct events to be audited and included in the Windows Event log, your domain controllers require accurate Windows Advanced Audit Policy settings.

For more information, see, [Advanced audit policy check](../configure-windows-event-collection) and [Advanced security audit policies](/en-us/windows/security/threat-protection/auditing/advanced-security-auditing) in the Windows documentation.

- To make sure that [Windows Event 8004 is audited](../configure-windows-event-collection#configure-ntlm-auditing) as needed by the service, review your [NTLM audit settings](/en-us/archive/blogs/askds/ntlm-blocking-and-you-application-analysis-and-auditing-methodologies-in-windows-7).
- For sensors running on AD FS / AD CS servers, configure the auditing level to **Verbose**. For more information, see [Event auditing information for AD FS](/en-us/windows-server/identity/ad-fs/troubleshooting/ad-fs-tshoot-logging#event-auditing-information-for-ad-fs-on-windows-server-2016) and [Event auditing information for AD CS](/en-us/windows-server/identity/ad-fs/troubleshooting/ad-fs-tshoot-logging).