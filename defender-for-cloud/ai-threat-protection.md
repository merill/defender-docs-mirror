---
layout: Conceptual
title: AI threat protection in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/ai-threat-protection
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Learn how AI threat protection in Microsoft Defender for Cloud detects and helps you respond to threats targeting generative AI applications and agents.
ms.date: 2026-05-19T00:00:00.0000000Z
ms.topic: overview
ai-usage: ai-assisted
locale: en-us
document_id: 3950fa77-7be1-6e5c-5c2a-2176f18aaa22
document_version_independent_id: 43df3425-0940-5603-6e88-9c99bc0c9742
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/ai-threat-protection.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/ai-threat-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/ai-threat-protection.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 9fe738e7-6d58-4050-ae8e-78a5a4b50a51
---

# AI threat protection in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud's threat protection for artificial intelligence (AI) services identifies threats to generative AI applications in real time and helps respond to security issues. Defender for Cloud's AI threat protection works with [Azure AI Content Safety Prompt Shields](/en-us/azure/ai-services/content-safety/concepts/jailbreak-detection) and Microsoft's threat intelligence to provide security alerts for threats like data leakage, data poisoning, jailbreak, credential theft, and more.

## Defender XDR integration

Threat protection for AI services integrates with [Defender Extended Detection and Response (XDR)](concept-integration-365), allowing security teams to centralize AI workload alerts in the Defender XDR portal. Security teams can correlate AI workload alerts and incidents in the Defender XDR portal to understand the full scope of an attack, including malicious activities related to their generative AI applications.

## Availability

The following table summarizes feature availability, pricing, and support requirements for AI threat protection.

| Aspect | Details |
| --- | --- |
| Release state | Generally available (GA) |
| Feature availability | Activity monitoring (security alerts)Prompt evidence (security alerts) |
| Pricing | Defender for AI Services billing is shown on the [Defender for Cloud pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/). You can also [estimate costs with the Defender for Cloud cost calculator](cost-calculator). Defender for AI Services includes a 30-day free trial, capped at 75 billion tokens scanned. Billing begins if the cap is reached within the 30-day period. |
| Supported AI services | [Azure OpenAI supported models](/en-us/azure/ai-services/openai/overview)[Azure AI Model Inference service supported models](/en-us/azure/ai-studio/ai-services/model-inference)Defender for Cloud currently supports text tokens only. Image and audio tokens aren't scanned. |
| Required roles and permissions | To enable threat detection at subscription level, you need the Owner role at subscription scope or specific roles with corresponding data actions. |
| Clouds | Commercial clouds: YesAzure Government: NoMicrosoft Azure operated by 21Vianet: NoConnected AWS accounts: No |