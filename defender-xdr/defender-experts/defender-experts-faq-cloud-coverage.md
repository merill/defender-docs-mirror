---
layout: Conceptual
title: FAQs related to Microsoft Defender Experts coverage for servers and cloud workloads - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/defender-experts/defender-experts-faq-cloud-coverage
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
ms.reviewer: 
description: Frequently asked questions related to server and cloud workload coverage in Microsoft Defender Experts
ms.service: defender-experts-for-xdr
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.topic: faq
ms.custom:
- cx-ti
- cx-dex
- msecd-doc-authoring-1018
ms.date: 2026-07-27T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 81363b05-abff-ea00-f1f8-317ff08e9583
document_version_independent_id: 81363b05-abff-ea00-f1f8-317ff08e9583
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/defender-experts/defender-experts-faq-cloud-coverage.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-experts/defender-experts-faq-cloud-coverage
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/defender-experts/defender-experts-faq-cloud-coverage.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 4ec3db85-2a76-93e3-a14c-3acce456983b
---

# FAQs related to Microsoft Defender Experts coverage for servers and cloud workloads - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- [Microsoft Defender](../microsoft-365-defender)

The following section lists down questions you or your SOC team might have regarding Microsoft Defender Experts coverage for servers and cloud workloads.

| Questions | Answers |
| --- | --- |
| **Can I configure which servers the Defender Experts will cover?** | This service covers **all** your servers in your tenant that have [Defender for Servers](/en-us/azure/defender-for-cloud/defender-for-servers-overview) protection enabled in Defender for Cloud. |
| **Do the Defender Experts investigate all Defender for Servers alerts?** | The Defender for Servers plan in Defender for Cloud covers multicloud servers, such as Microsoft Azure, Amazon Web Services, and Google Cloud Platform, provided the Microsoft Defender for Endpoint is installed on the servers. All Defender for Servers P1 and P2 alerts (Detection Source = Microsoft Defender for Servers) are in scope except for [DNS alerts](/en-us/azure/defender-for-cloud/alerts-dns) due to limited data available for investigation. |
| **I only have Microsoft Defender Endpoint. How can I get server coverage?** | If you have servers that have Defender for Endpoint deployed on them with a Microsoft Defender for Endpoint for Server license, you can get the server coverage through the Defender Experts MDR service. The service doesn't cover Microsoft Defender for Cloud workloads. [Learn more](defender-experts-mdr-prerequisites#product-configuration-and-service-coverage)If you want coverage for servers in Defender for Cloud, you need to avail the Microsoft Defender Experts for Servers or Defender Experts Hunting - Servers. |
| **Does Defender Experts MDR Plan 2 cover my Microsoft Defender for Cloud workloads?** | No. Plan 2 extends expert coverage to supported third-party sources, including multicloud sources, that you ingest through Microsoft Sentinel. That telemetry coverage is separate from Microsoft Defender for Cloud workload protection, and neither Defender Experts MDR plan covers Defender for Cloud workloads such as storage, containers, and databases. For expert coverage of servers protected by Defender for Cloud, use Microsoft Defender Experts for Servers or Defender Experts Hunting - Servers. [Learn more about the Defender Experts MDR plans](defender-experts-mdr-overview) |

### See also

- [General information on Defender Experts MDR service](defender-experts-mdr-faq)
- [General information on Microsoft Defender Experts Hunting service](defender-experts-hunting-faq)

Tip

Do you want to learn more? Engage with the Microsoft Security community in our Tech Community: [Microsoft Defender XDR Tech Community](https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection).