---
layout: Conceptual
title: Microsoft Defender for Endpoint alongside other security solutions - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/mde-side-by-side
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: See recommendations for running Defender for Endpoint alongside other security solutions.
ms.service: defender-endpoint
ms.localizationpriority: medium
ms.date: 2025-06-13T00:00:00.0000000Z
ms.topic: article
author: limwainstein
ms.author: lwainstein
ms.custom:
- nextgen
- partner-contribution
ms.reviewer: pahuijbr
ms.collection:
- m365-security
- tier2
locale: en-us
document_id: a4963cde-84b4-a200-5903-82cfb0d3d73e
document_version_independent_id: a4963cde-84b4-a200-5903-82cfb0d3d73e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/mde-side-by-side.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mde-side-by-side
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/mde-side-by-side.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/540ac133-a371-4dbb-8f94-28d6cc77a70b
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/60bfc045-f127-4841-9d00-ea35495a5800
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 71b7d40e-71e3-d22c-d00a-5d4e1d5cd2c7
---

# Microsoft Defender for Endpoint alongside other security solutions - Microsoft Defender for Endpoint | Microsoft Learn

## Considerations with concurrent security solutions

Large organizations use a wide variety of security solutions, and running multiple security solutions concurrently can lead to performance issues and conflicts. To help minimize interoperability issues, trusted security solutions can often be configured to mitigate conflicts with each other. Organizations should understand the potential benefits, risks, and mitigation recommendations to make informed choices.

1. **Avoid duplication**. Running multiple security solutions that perform the same function can lead to performance issues and conflicts. It's generally recommended to avoid redundant capabilities, as this increases the likelihood of problematic product interactions.

    Microsoft Defender for Endpoint can be configured to disable endpoint detection and response (EDR) in block mode, automated investigation & remediation, protection from potentially unwanted applications (PUA protection), network discovery & response, and other capabilities. This can reduce overlap with detection and response functions provided by non-Microsoft endpoint security solutions. Responsibility for these functions falls to the solution actively providing those functions.

    Similarly, setting Microsoft Defender Antivirus in passive mode ensures that when another anti-malware solution is present, Microsoft Defender Antivirus doesn't perform active protection, remediation, or malware blocking. Responsibility for malware protection shifts to the active anti-malware solution.
2. **Configure mutual exclusions**. Security exclusions are used to prevent certain entities from being scanned or blocked by security software. Creating mutual exclusions between security solutions can help avoid performance issues and compatibility problems. Exclusions can potentially decrease protection, so it's important to only exclude processes and paths that are confidently benign.

    When creating mutual exclusions between two security solutions, organizations are deferring protection for those solutions to their respective vendors. If a non-Microsoft EDR solution is unable to monitor Defender for Endpoint binaries, for example, then Microsoft is being trusted to protect its own solution. Likewise, if Defender for Endpoint is unable to monitor a non-Microsoft solution, then that vendor is being trusted to protect its own solution. These gaps in protection need to be actively managed as solutions change, to help minimize risk.

    Note

    For Microsoft Windows performance, for example, see [Performance overview - Windows Client | Microsoft Learn](/en-us/troubleshoot/windows-client/performance/performance-overview) and [Performance overview - Windows Server | Microsoft Learn](/en-us/troubleshoot/windows-server/performance/performance-overview).
3. **Consider system configuration**. In side-by-side scenarios, even well configured security tools can be impacted by underlying system limitations. Ensure that endpoints meet hardware requirements and stagger resource-heavy tasks. Built-in telemetry can monitor performance to help isolate interoperability issues from system constraints. Solutions and scenario guides are available to help troubleshoot and self-solve performance-related issues, or organizations can leverage available support resources.

Delegating security functionality, creating exclusions, and configuring settings can help reduce the likelihood of interoperability issues, but these might not be eliminated completely. Acceptable risk is different for every organization; optimizing for usability might increase risk, and optimizing for security will likely impact usability. Organizations should weigh the benefits of interoperability over potential risks.

## Customer support

Commercially reasonable support is provided through Microsoft Customer Service & Support and Microsoft-managed support offerings. In troubleshooting performance, reliability, and other issues, customers might be asked to temporarily remove potentially conflicting solutions to identify the source of the issue. Depending on the issue, customers might be asked to engage with the vendor of the non-Microsoft solution.