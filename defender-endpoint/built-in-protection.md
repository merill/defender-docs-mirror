---
layout: Conceptual
title: Built-in protection helps guard against ransomware - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/built-in-protection
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how built-in protection in Microsoft Defender for Endpoint applies default settings to help protect Windows and macOS devices from ransomware.
author: paulinbar
ms.author: painbar
ms.topic: overview
ms.date: 2026-09-16T00:00:00.0000000Z
ms.service: defender-endpoint
ms.subservice: ngp
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- mde-ngp
ms.custom:
- sfi-ga-nochange
- msecd-doc-authoring-1015
ms.reviewer: joshbregman
ai-usage: ai-assisted
locale: en-us
document_id: d2c0321c-5de1-d774-3c8e-40781c09c148
document_version_independent_id: d2c0321c-5de1-d774-3c8e-40781c09c148
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/built-in-protection.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: built-in-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/built-in-protection.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
platformId: fc8400df-fa77-4216-b9ad-34b8d498a4aa
---

# Built-in protection helps guard against ransomware - Microsoft Defender for Endpoint | Microsoft Learn

Built-in protection in [Microsoft Defender for Endpoint](microsoft-defender-endpoint) applies default security settings that help protect Windows and macOS devices from ransomware and other threats. Built-in protection complements [next-generation protection](next-generation-protection) and [attack surface reduction](attack-surface-reduction-overview) capabilities that help prevent, detect, investigate, and respond to advanced threats.

Use this article to understand how built-in protection works and find the appropriate method to manage tamper protection settings.

Tip

To strengthen protection for your organization's devices, configure these capabilities:

- [Enable cloud protection](cloud-protection-configure)
- [Turn tamper protection on](tamper-protection-overview)
- [Enable standard protection attack surface reduction (ASR) rules in Block mode](attack-surface-reduction-rules-overview#asr-rules)
- [Enable network protection in block mode](enable-network-protection)

## What is built-in protection, and how does it work?

Built-in protection applies default settings automatically as devices are onboarded to Defender for Endpoint. These settings help protect devices from ransomware and other threats. Built-in protection initially enabled [tamper protection](tamper-protection-overview) for your organization and later expanded to other default settings. For more information, see the Tech Community blog post, [Tamper protection will be turned on for all enterprise customers](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/tamper-protection-will-be-turned-on-for-all-enterprise-customers/ba-p/3616478).

Your security team can change the built-in protection settings to meet your organization's needs.

Note

Built-in protection sets default values for Windows and macOS devices. Endpoint security settings configured through baselines or policies in [Microsoft Intune](/en-us/intune/endpoint-manager-overview) override the built-in protection settings.

## Can I opt out?

You can opt out of built-in protection by configuring your own security settings. Settings that you configure through a supported management method override the built-in protection defaults. For available configuration methods, see the next section.

## Can I change built-in protection settings?

Built-in protection is a set of default settings. Your security team isn't required to keep these default settings in place. To meet your organization's business needs, your security team can change the following security features:

- **Cloud protection**: [Configure cloud protection in Microsoft Defender Antivirus](cloud-protection-configure)
- **Tamper protection**
    - [Configure tamper protection for Microsoft Defender Antivirus on Windows](tamper-protection-windows-configure)
    - [Configure tamper protection for Microsoft Defender for Endpoint on macOS](tamper-protection-macos-configure)
    - [Temporarily disable tamper protection by using troubleshooting mode](troubleshooting-mode-enable#temporarily-disable-tamper-protection)
- **Attack surface reduction (ASR) rules**: [Configure attack surface reduction rules and exclusions](attack-surface-reduction-rules-configure)
- **Network protection**: [Configure network protection in Microsoft Defender Antivirus](enable-network-protection)