---
layout: Conceptual
title: Enable and configure Microsoft Defender Antivirus protection features - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/configure-protection-features-microsoft-defender-antivirus
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Enable behavior-based, heuristic, and real-time protection in Microsoft Defender Antivirus.
ms.service: defender-endpoint
ms.subservice: ngp
ms.localizationpriority: medium
author: chrisda
ms.author: chrisda
ms.topic: install-set-up-deploy
ms.custom: nextgen
ms.reviewer: yongrhee
ms.collection:
- m365-security
- tier2
- mde-ngp
ms.date: 2025-10-20T00:00:00.0000000Z
locale: en-us
document_id: 12cb9fb7-c001-510a-a023-de1ce972d090
document_version_independent_id: 12cb9fb7-c001-510a-a023-de1ce972d090
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/configure-protection-features-microsoft-defender-antivirus.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-protection-features-microsoft-defender-antivirus
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/configure-protection-features-microsoft-defender-antivirus.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 500c21c3-bbf0-cda9-7826-a77f1c5b6b1a
---

# Enable and configure Microsoft Defender Antivirus protection features - Microsoft Defender for Endpoint | Microsoft Learn

Microsoft Defender Antivirus uses several methods to provide threat protection:

- Cloud protection for near-instant detection and blocking of new and emerging threats
- Always-on scanning, using file and process behavior monitoring and other heuristics (also known as "real-time protection")
- Dedicated protection updates based on machine learning, human and automated big-data analysis, and in-depth threat resistance research

You can configure how Microsoft Defender Antivirus uses these methods with [Microsoft Defender for Endpoint Security Configuration Management](/en-us/intune/intune-service/protect/mde-security-integration), [Microsoft Intune](use-intune-config-manager-microsoft-defender-antivirus), Microsoft Configuration Manager, [Group Policy](use-group-policy-microsoft-defender-antivirus), [PowerShell cmdlets](use-powershell-cmdlets-microsoft-defender-antivirus), and [Windows Management Instrumentation (WMI)](use-wmi-microsoft-defender-antivirus).

This section covers configuration for always-on scanning, including how to detect and block apps that are deemed unsafe, but might not be detected as malware.

See [Use next-gen Microsoft Defender Antivirus technologies through cloud protection](cloud-protection-microsoft-defender-antivirus) for how to enable and configure Microsoft Defender Antivirus cloud protection.

## Prerequisites

### Supported operating systems

- Windows