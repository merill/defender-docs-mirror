---
layout: Conceptual
title: Hardware acceleration and Microsoft Defender Antivirus. - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/hardware-acceleration-and-mdav
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: How Microsoft Defender Antivirus incorporates hardware acceleration and Microsoft Defender Antivirus.
author: chrisda
ms.author: chrisda
ms.reviewer: yongrhee
ms.service: defender-endpoint
ms.topic: overview
ms.date: 2024-12-05T00:00:00.0000000Z
ms.subservice: ngp
ms.collection:
- m365-security
- tier2
ms.localizationpriority: medium
ms.custom: partner-contribution
ROBOTS: NOINDEX, NOFOLLOW
locale: en-us
document_id: ba18acce-0fde-bcb4-6c02-d0e398f7cc36
document_version_independent_id: ba18acce-0fde-bcb4-6c02-d0e398f7cc36
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/hardware-acceleration-and-mdav.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: hardware-acceleration-and-mdav
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/hardware-acceleration-and-mdav.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: d5412d95-0458-c6a5-a1e7-3867ada3a968
---

# Hardware acceleration and Microsoft Defender Antivirus. - Microsoft Defender for Endpoint | Microsoft Learn

Note

The features described in this article are currently in Preview, aren't available in all organizations, and are subject to change.

**Platforms:**

- Windows 11, Windows 10

**Known limitations:**

- Intel TDT doesn't support processors designated as servers.
- Multi-level virtualization isn't currently supported.
- Windows Server workloads aren't supported.
- Windows clients running on Xeon processors aren't supported due to Intel Xeon processors not supporting Intel TDT functionality.

## Microsoft Defender Antivirus (MDAV) and Intel Threat Detection Technology (TDT)

This table shows the Intel TDT technologies Microsoft collaborated with Intel on to provide security while also balancing performance:

| Available since | Intel TDT technology | Intel Threat Detection Technology (TDT) available on |
| --- | --- | --- |
| 2018 | Intel TDT - Accelerated Memory Scanning (AMS) | Intel integrated graphic sixth Gen Core (circa 2015) or newer family of processors, running on laptops, tablets, and desktop systems. |
| 2021 | Intel TDT - Cryptojacking detector | Intel sixth Gen Core (circa 2015) or newer family of processors, running on laptops, tablets, and desktop systems. |
| 2022 | Intel TDT - Ransomware detector | Intel eighth Gen Core or newer family of processors. |

**Intel Threat Detection Technology (TDT) - Accelerated Memory Scanning (AMS):** Introduced extra memory scanning capabilities to detect fileless attacks that are expensive on the Central Processing Unit (CPU), and then offload them to the integrated Graphics Processor Unit (integrated GPU). Two benefits are:

- lower CPU consumption
- A reduction of System-on-a-chip (SoC) power consumption leading to longer battery life on laptops and tablets

**Intel Threat Detection Technology (TDT) - Cryptojacking:** Enhanced detection by using Intel's Central Processing Unit (CPU) performance monitoring unit (PMU) and offloading to the integrated Graphics Processor Unit (integrated GPU) to detect the malware code execution (fingerprint) of repeated mathematical operations at runtime. Machine learning processes signals with minimal overhead.

### How do you enable Intel TDT AMS or Cryptojacking integration?

Enabled by default when Microsoft Defender Antivirus is running.

### What do the detections show up as?

The regular Microsoft Defender Antivirus Event ID **1116**.

### What type of attacks does it help with?

- We use the Intel TDT - Cryptojacking detector to thwart various cryptojacking malware. The following Coinminer campaigns were successfully detected and blocked using the TDT Cryptojacking detector: [YouTube Pirated Software Videos Deliver Triple Threat: Vidar Stealer, LaPlasa Clipper, XMRig Miner](https://www.fortinet.com/blog/threat-research/youtube-pirated-software-videos-deliver-triple-threat-vidar-stealer-laplas-clipper-xmrig-miner)
- We use the Intel TDT detector to identify instances of CryptoJacking malware abusing Windows binaries (lolbins), and then employ Defender behavior monitoring to prevent and block such activities effectively. For more information, see [Hardware-based threat defense against increasingly complex cryptojackers](https://www.microsoft.com/security/blog/2022/08/18/hardware-based-threat-defense-against-increasingly-complex-cryptojackers/).