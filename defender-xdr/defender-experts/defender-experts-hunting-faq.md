---
layout: Conceptual
title: FAQs related to Microsoft Defender Experts Hunting service - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/defender-experts/defender-experts-hunting-faq
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
ms.reviewer: 
description: Frequently asked questions related to the Microsoft Defender Experts Hunting service
ms.service: defender-experts-for-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- essentials-get-started
ms.topic: faq
ms.custom:
- cx-ti
- cx-ean
ms.date: 2025-06-27T00:00:00.0000000Z
locale: en-us
document_id: 60ab99bf-076d-6455-9cd4-824b067d40f3
document_version_independent_id: 60ab99bf-076d-6455-9cd4-824b067d40f3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/defender-experts/defender-experts-hunting-faq.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-experts/defender-experts-hunting-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/defender-experts/defender-experts-hunting-faq.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 221e4ddf-a0ab-3e58-39cb-54c560b62004
---

# FAQs related to Microsoft Defender Experts Hunting service - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- [Microsoft Defender Experts Hunting](defender-experts-hunting-overview)
- [Microsoft Defender](../microsoft-365-defender)

The following section lists down questions your security operations center (SOC) team might have about the Microsoft Defender Experts Hunting service:

| Questions | Answers |
| --- | --- |
| **What is the Microsoft Defender Experts Hunting service?** | [Microsoft Defender Experts Hunting](defender-experts-hunting-overview) provides a proactive threat hunting service to identify threats in advance. [Microsoft Defender Experts MDR](defender-experts-mdr-overview) also includes the proactive threat hunting offered by Defender Experts Hunting. |
| **Does Defender Experts Hunting use or require Microsoft Sentinel or a security information and event management (SIEM) platform?** | No. This service doesn't use any non-Microsoft data ingested either through Microsoft Sentinel or any other SIEM platform. |
| **What products does Defender Experts Hunting operate on?** | Defender Experts Hunting relies on event signals from Microsoft Defender for Endpoint, Microsoft Defender for Office 365, Microsoft Defender for Cloud Apps, Microsoft Entra ID protection, and Microsoft Defender for Identity. It also relies on proprietary Microsoft Threat Intelligence sources. Any event definitions not authored by Microsoft Defender products, such as third-party events or detections, fall outside the scope of this service. |
| **What is the role of Defender Experts Hunting in the context of a purple team (red team and blue team coordinated work stream) exercise?** | Defender Experts Hunting is part of the blue team in a purple team exercise. It complements your internal hunting team by enhancing their capabilities rather than replacing them. |
| **What actions can your experts take during a hunting investigation that results in a Defender Experts Notification?** | During threat hunting investigations, our analysts refrain from taking direct actions on customer assets. Instead, they provide detailed information, including a threat summary and hunting queries that show the timeline of events for the identified attack, and remediation action recommendations. Defender Experts Notifications provide guidance on how you can review and address the novel threat. |
| **What types of incidents can your experts investigate?** | The Defender Experts Hunting service specializes in addressing the evolving threat landscape, bridging industry knowledge gaps, and recommending the most effective ways to identify these threats. Our experts don't prioritize well-established threats that Microsoft Defender products address adequately. However, when a well-known tactic is employed to generate a novel attack, our experts identify both the novel and existing attack tactics diligently. [Learn more about novel attacks in our in the Microsoft Security Experts Blog](https://techcommunity.microsoft.com/tag/Defender%20Experts%20for%20Hunting?nodeId=board%3AMicrosoftSecurityExperts) |
| **Can your experts help me improve my security posture?** | The scope of the posture change recommendation is limited to the scope of a Defender Experts Notification and is limited to preventing the attack identified in the context of the notification. |
| **Can Defender Experts Hunting help with an active compromise or vulnerability?** | No, Defender Experts currently don't provide incident response services. |
| **How can my organization participate in the Defender Experts Hunting service?** | Reach out to your Microsoft representative to express your interest in Defender Experts Hunting. |
| **Does Defender Experts Hunting cover cloud servers that have Microsoft Defender for Endpoint deployed on them?** | Defender Experts Hunting covers servers—whether on premises or on a hyperscale cloud service provider—that have Microsoft Defender for Endpoint deployed on them with a Microsoft Defender for Endpoint for Servers license. For Defender Experts coverage, a server is considered as a license for billing. The service doesn't cover Microsoft Defender for Cloud. [Learn more about specific hardware and software requirements](/en-us/defender-endpoint/minimum-requirements) |
| **Once I see a Defender Experts Notification, if I have questions, how do I communicate with the Defender Experts Hunting team?** | The **Ask Defender Experts** option in the Microsoft Defender portal delivers swift and accurate responses to all your threat-hunting questions. However, this service is limited to questions related specifically to Defender Experts Hunting. [Learn more about Ask Defender Experts](defender-experts-hunting-ask-experts) |
| **What kinds of inquiries could I submit in Ask Defender Experts?** | Ask Defender Experts is intended to provide a better understanding of complex threats affecting your organization. It focuses on products included in Microsoft Defender (Defender for Endpoint, Defender for Office 365, Defender for Cloud Apps, and Defender for Identity). It doesn't answer inquiries related to custom detections in the above products (that is, non-Defender and third-party cybersecurity products), bugs in your product experience in the Defender portal, and those related to security incident response services. [See some sample questions you can ask our Defender Experts](defender-experts-hunting-ask-experts#sample-questions-you-can-ask-from-defender-experts) |
| **What certifications does the Defender Experts Hunting service have?** | Defender Experts Hunting is certified for [HIPAA and ISO](/en-us/compliance/regulatory/offering-hipaa-hitech). |
| **How is customer data protected?** | For more information about Microsoft's commitment in valuing and protecting your data, see [Data collection, usage, and retention](defender-experts-hunting-prerequisites#data-collection-usage-and-retention). You can also visit the [Trust Center](https://www.microsoft.com/trust-center/product-overview) then scroll down to **Additional products and services** &gt; **Managed Security Services** &gt; **Microsoft Defender Experts**. |
| **Does the hunting service offer real-time threat remediation with boots on ground?** | No, the hunting service doesn't cover real-time threat remediation.Despite this, Microsoft provides professional on-site service through our [Microsoft Defender Experts Cybersecurity Incident Response team](https://www.microsoft.com/security/business/microsoft-incident-response?msockid=2c408e0b54cc68301f9a9b55554869f3). This service requires a separate contract. We prioritize customer needs and have a swift turnaround time. Contact your Customer Service Account Manager for further assistance. |
| **Is there a graph API that can fetch Defender Experts Notifications content?** | Yes. For more information, see [Access incident notifications using Graph API](defender-experts-hunting-graph-api). |
| **How is AI used in the Defender Experts service?** | AI is used to support the Defender Experts service by enhancing the speed, scale, and consistency of security operations. We use a combination of generative, agentic, and foundational AI to power workflows such as incident triage, investigation, and summarization by analyzing signals like telemetry and historical analyst actions. Defender Experts analysts review and validate these AI-generated insights to ensure quality and accuracy. AI helps scale expert capabilities, and human analysts remain central to the service, ensuring customers receive trusted outcomes. |

### See also

- [Before you begin using Defender Experts Hunting](defender-experts-hunting-prerequisites)
- [Start using Defender Experts Hunting](defender-experts-hunting-onboarding)

Tip

Do you want to learn more? Engage with the Microsoft Security community in our Tech Community: [Microsoft Defender XDR Tech Community](https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection).