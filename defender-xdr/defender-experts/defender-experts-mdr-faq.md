---
layout: Conceptual
title: FAQs related to Microsoft Defender Experts MDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/defender-experts/defender-experts-mdr-faq
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
ms.reviewer: 
description: Frequently asked questions related to Defender Experts MDR
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
ms.date: 2026-07-28T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 617bcbcd-6ddc-4a56-3c46-f7e14824d562
document_version_independent_id: 617bcbcd-6ddc-4a56-3c46-f7e14824d562
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/defender-experts/defender-experts-mdr-faq.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-experts/defender-experts-mdr-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/defender-experts/defender-experts-mdr-faq.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: eb2addc9-58f3-99c2-9b13-4931c544a85c
---

# FAQs related to Microsoft Defender Experts MDR - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- [Microsoft Defender](../microsoft-365-defender)

| Questions | Answers |
| --- | --- |
| **What's the difference between Defender Experts MDR Plan 1 and Plan 2?** | Plan 1 provides expert triage, investigation, and response for your Microsoft Defender workloads. Plan 2 includes everything in Plan 1 and extends expert triage and investigation to supported third-party sources that you ingest through Microsoft Sentinel. [Learn more about the plans](defender-experts-mdr-overview) |
| **How is Microsoft Defender Experts MDR different from Microsoft Defender Experts Hunting?** | [Microsoft Defender Experts Hunting](defender-experts-hunting-overview) provides proactive threat hunting service to proactively find threats. This service is meant for customers that have a robust security operations center and want that deep expertise in hunting to expose advanced threats. Microsoft Defender Experts MDR provides end-to-end security operations capabilities to monitor, investigate, and respond to security alerts. This service is meant for customers with constrained security operations centers (SOCs) that are overburdened with alert volume, in need of skilled experts, or both. Defender Experts MDR also includes the proactive threat hunting offered by Defender Experts Hunting |
| **Does Defender Experts MDR require Microsoft Sentinel?** | It depends on the plan. Plan 1 doesn't require Microsoft Sentinel, because Defender Experts can use Microsoft Defender data in customers' original locations for each Microsoft Defender product deployed. A Microsoft Sentinel workspace is required for Plan 2, because Plan 2 operates on the telemetry you ingest into Microsoft Sentinel. |
| **Does Defender Experts MDR manage my Microsoft Sentinel deployment?** | No. Plan 2 isn't a managed security information and event management (SIEM) service. Defender Experts operates on the supported data in your workspace and on the detection content that Defender Experts authors. You continue to own your Microsoft Sentinel deployment, including connector deployment, custom ingestion pipelines, SIEM migration, your own analytics rules, and data retention, permissions, and ingestion costs. |
| **What products does Defender Experts MDR operate on?** | Refer to [Before you begin using Defender Experts MDR](defender-experts-mdr-prerequisites) for details. To discuss the sources that Plan 2 covers in your environment, contact your Microsoft account team. |
| **Does Defender Experts MDR replace my SOC team?** | No. Defender Experts MDR provides coverage for Microsoft Defender incidents, and with Plan 2, for incidents from supported third-party sources. It's the ideal way to augment your SOC team, reduce their workload, and collaborate with them to protect your organization from activity groups. |
| **What actions can your experts take during incident investigation?** | Our expert analysts can take actions based on the roles granted to them in your Microsoft Defender portal. If our analysts are granted a security reader role, they can investigate and provide managed response for your SOC team to act on. If our analysts are granted a security operator role, they can also take specific remediation actions agreed upon with your SOC team.For supported third-party sources covered by Plan 2, our analysts provide guidance on the response actions to take rather than acting in the third-party product. |
| **What types of incidents can your experts investigate?** | Defender Experts MDR covers incidents categorized as High or Medium severity in Windows, Linux, and macOS devices. Incidents categorized as Compliance, Data Loss Prevention (DLP), or Custom Detections and those affecting internet of things (IoT), iOS, or Android devices are outside the service's scope. |
| **Can your experts help me improve my security posture?** | Yes, our experts provide necessary guidance regularly to improve your security posture. |
| **Can Defender Experts MDR help with an active compromise or vulnerability?** | No, Defender Experts currently don't provide incident response services. Contact your Microsoft representative or fill out the [Experiencing a Cybersecurity Incident?](https://customervoice.microsoft.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbRypQlJUvhTFIvfpiAfrpFQdUOTdRRFpDUFQ1TzNLVFZXV0VUOVlVN0szUiQlQCN0PWcu) form to engage Microsoft Defender Experts Cybersecurity Incident Response for incident response assistance. |
| **How can my organization participate in the Defender Experts MDR and Microsoft Defender Experts for Servers services?** | Contact your Microsoft representative to express interest in Defender Experts MDR and Defender Experts for Servers services. |
| **How is AI used in the Defender Experts service?** | AI is used to support the Defender Experts service by enhancing the speed, scale, and consistency of security operations. We use a combination of generative, agentic, and foundational AI to power workflows such as incident triage, investigation, and summarization by analyzing signals like telemetry and historical analyst actions. Defender Experts analysts review and validate these AI-generated insights to ensure quality and accuracy. AI helps scale expert capabilities, and human analysts remain central to the service, ensuring customers receive trusted outcomes. |

### See also

[How Microsoft Defender Experts MDR permissions work](defender-experts-mdr-permissions)

Tip

Do you want to learn more? Engage with the Microsoft Security community in our Tech Community: [Microsoft Defender XDR Tech Community](https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection).