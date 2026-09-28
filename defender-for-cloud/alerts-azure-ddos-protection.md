---
layout: Conceptual
title: Alerts for Azure DDoS Protection - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/alerts-azure-ddos-protection
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
description: This article lists the security alerts for Azure DDoS Protection visible in Microsoft Defender for Cloud.
ms.topic: reference
ms.custom: linux-related-content
ms.date: 2024-06-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: e7816008-d020-7b75-787a-b47393d275de
document_version_independent_id: fade3463-16fe-bb7b-90eb-a781b606bc5d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/alerts-azure-ddos-protection.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/alerts-azure-ddos-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/alerts-azure-ddos-protection.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/c31cd89d-61bc-4909-b223-b45dc81df005
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/4c3a5f3c-7f23-4f9e-a704-23ddb3d5da5e
platformId: 03203420-3a03-9ad8-5ebc-32070cf6c093
---

# Alerts for Azure DDoS Protection - Microsoft Defender for Cloud | Microsoft Learn

This article lists the security alerts you might get for Azure DDoS Protection from Microsoft Defender for Cloud and any Microsoft Defender plans you enabled. The alerts shown in your environment depend on the resources and services you're protecting, and your customized configuration.

Note

Some of the recently added alerts powered by Microsoft Defender Threat Intelligence and Microsoft Defender for Endpoint might be undocumented.

[Learn how to respond to these alerts](manage-respond-alerts).

[Learn how to export alerts](continuous-export).

Note

Alerts from different sources might take different amounts of time to appear. For example, alerts that require analysis of network traffic might take longer to appear than alerts related to suspicious processes running on virtual machines.

## Azure DDoS Protection alerts

[Further details and notes](other-threat-protections#azure-ddos)

### **DDoS Attack detected for Public IP**

(NETWORK\_DDOS\_DETECTED)

**Description**: DDoS Attack detected for Public IP (IP address) and being mitigated.

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Probing

**Severity**: High

### **DDoS Attack mitigated for Public IP**

(NETWORK\_DDOS\_MITIGATED)

**Description**: DDoS Attack mitigated for Public IP (IP address).

**[MITRE tactics](alerts-reference#mitre-attck-tactics)**: Probing

**Severity**: Low

Note

For alerts that are in preview: The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.