---
layout: Conceptual
title: Integrate Microsoft Defender for Endpoint with other Microsoft solutions - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/threat-protection-integration
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how Microsoft Defender for Endpoint integrates with other Microsoft solutions, including Microsoft Defender for Identity and Microsoft Defender for Cloud.
author: limwainstein
ms.author: lwainstein
ms.service: defender-endpoint
ms.subservice: onboard
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.topic: concept-article
ms.date: 2025-03-26T00:00:00.0000000Z
locale: en-us
document_id: e7d6bed4-4a3a-5356-a354-89b8463c9407
document_version_independent_id: e7d6bed4-4a3a-5356-a354-89b8463c9407
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/threat-protection-integration.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: threat-protection-integration
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/threat-protection-integration.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 7d73a280-1c45-dec7-94d0-c2e4f24b833b
---

# Integrate Microsoft Defender for Endpoint with other Microsoft solutions - Microsoft Defender for Endpoint | Microsoft Learn

## Integrate with other Microsoft solutions

Microsoft Defender for Endpoint directly integrates with various Microsoft solutions.

### Microsoft Defender for Cloud

Microsoft Defender for Cloud provides a comprehensive server protection solution, including endpoint detection and response (EDR) capabilities on Windows Servers.

### Microsoft Sentinel

The Microsoft Defender for Endpoint connector lets you stream alerts from Microsoft Defender for Endpoint into Microsoft Sentinel. This will enable you to more comprehensively analyze security events across your organization and build playbooks for effective and immediate response.

### Azure Information Protection

We recently deprecated the Azure Information Protection integration as our Endpoint DLP capabilities incorporate an improved discovery and protection solution for sensitive data stored on endpoint devices that facilitates greater visibility and integration between solutions. This was announced in the following [blog](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/protecting-sensitive-information-on-devices/ba-p/2143555). We recommend that customers move to using Endpoint DLP.

### Conditional Access

Microsoft Defender for Endpoint's dynamic device risk score is integrated into the Conditional Access evaluation, ensuring that only secure devices have access to resources.

### Microsoft Defender for Cloud Apps

Microsoft Defender for Cloud Apps leverages Microsoft Defender for Endpoint signals to allow direct visibility into cloud application usage including the use of unsupported cloud services (shadow IT) from all Microsoft Defender for Endpoint monitored devices.

### Microsoft Defender for Identity

Suspicious activities are processes running under a user context. The integration between Microsoft Defender for Endpoint and Microsoft Defender for Identity provides the flexibility of conducting cyber security investigation across activities and identities.

### Microsoft Defender for Office

[Defender for Office 365](/en-us/defender-office-365/mdo-about) helps protect your organization from malware in email messages or files through Safe Links, Safe Attachments, advanced Anti-Phishing, and spoof intelligence capabilities. The integration between Microsoft Defender for Office 365 and Microsoft Defender for Endpoint enables security analysts to go upstream to investigate the entry point of an attack. Through threat intelligence sharing, attacks can be contained and blocked.

Note

Defender for Office 365 data is displayed for events within the last 30 days. For alerts, Defender for Office 365 data is displayed based on first activity time. After that, the data is no longer available in Defender for Office 365.

### Skype for Business

The Skype for Business integration provides a way for analysts to communicate with a potentially compromised user or device owner through a simple button from the portal.

## Microsoft Defender

With Microsoft Defender XDR, Microsoft Defender for Endpoint, and various Microsoft security solutions form a unified pre- and post-breach enterprise defense suite that natively integrates across endpoint, identity, email, and applications to detect, prevent, investigate, and automatically respond to sophisticated attacks.

[Learn more about Microsoft Defender XDR](/en-us/defender-xdr/microsoft-365-defender)