---
layout: Conceptual
title: Overview of endpoint detection and response capabilities - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/overview-endpoint-detection-response
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
ms.reviewer: 
description: Learn about the endpoint detection and response capabilities in Microsoft Defender for Endpoint
ms.service: defender-endpoint
ms.author: lwainstein
author: limwainstein
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- mde-edr
ms.topic: concept-article
ms.subservice: edr
ms.date: 2025-03-26T00:00:00.0000000Z
locale: en-us
document_id: 4e447420-572f-9b40-3469-3ab12a0b1674
document_version_independent_id: 4e447420-572f-9b40-3469-3ab12a0b1674
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/overview-endpoint-detection-response.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: overview-endpoint-detection-response
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/overview-endpoint-detection-response.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: a65e8e94-a810-f7b8-a993-91823eaeac40
---

# Overview of endpoint detection and response capabilities - Microsoft Defender for Endpoint | Microsoft Learn

**Applies to:**

- [Microsoft Defender for Endpoint Plans 1 and 2](microsoft-defender-endpoint)
- [Microsoft Defender XDR](/en-us/defender-xdr)

Endpoint detection and response capabilities in Defender for Endpoint provide advanced attack detections that are near real-time and actionable. Security analysts can prioritize alerts effectively, gain visibility into the full scope of a breach, and take response actions to remediate threats.

When a threat is detected, alerts are created in the system for an analyst to investigate. Alerts with the same attack techniques or attributed to the same attacker are aggregated into an entity called an *incident*. Aggregating alerts in this manner makes it easy for analysts to collectively investigate and respond to threats.

Note

Defender for Endpoint detection is not intended to be an auditing or logging solution that records every operation or activity that happens on a given endpoint. Our sensor has an internal throttling mechanism, so the high rate of repeat identical events don't flood the logs.

Important

[Defender for Endpoint Plan 1](defender-endpoint-plan-1) and [Microsoft Defender for Business](/en-us/defender-business/mdb-overview) include only the following manual response actions:

- Run antivirus scan
- Isolate device
- Stop and quarantine a file
- Add an indicator to block or allow a file

Inspired by the "assume breach" mindset, Defender for Endpoint continuously collects behavioral cyber telemetry. This includes process information, network activities, deep optics into the kernel and memory manager, user login activities, registry and file system changes, and others. The information is stored for six months, enabling an analyst to travel back in time to the start of an attack. The analyst can then pivot in various views and approach an investigation through multiple vectors.

The response capabilities give you the power to promptly remediate threats by acting on the affected entities.

## Automatic attack disruption

Defender for Endpoint signals contribute to [automatic attack disruption](/en-us/defender-xdr/automatic-attack-disruption) in Microsoft Defender XDR. Attack disruption uses signal correlation and AI to automatically contain active attacks in progress—such as ransomware, business email compromise, and adversary-in-the-middle attacks—limiting lateral movement and reducing overall impact. Automatic attack disruption works with other Defender XDR sources to contain compromised assets, including automatically disabling compromised user accounts and isolating affected devices.