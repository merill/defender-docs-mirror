---
layout: Conceptual
title: Before you begin using the Microsoft Defender Experts Hunting service - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/defender-experts/defender-experts-hunting-prerequisites
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
ms.reviewer: 
description: Review the prerequisites for Microsoft Defender Experts Hunting, including required licensing, onboarding, and setup steps before you begin using the service.
ms.service: defender-experts-for-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- m365initiative-defender-endpoint
- tier1
- essentials-compliance
ms.topic: how-to
ms.custom:
- msecd-doc-authoring-1014
- cx-ti
- cx-ean
ms.date: 2026-06-16T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 95f70fe9-bc8a-b9c7-9991-8e7be27e7511
document_version_independent_id: 95f70fe9-bc8a-b9c7-9991-8e7be27e7511
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/defender-experts/defender-experts-hunting-prerequisites.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-experts/defender-experts-hunting-prerequisites
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/defender-experts/defender-experts-hunting-prerequisites.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: bf09b19f-4c64-2183-d557-700920e13df6
---

# Before you begin using the Microsoft Defender Experts Hunting service - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- [Microsoft Defender](../microsoft-365-defender)

[Microsoft Defender Experts Hunting](defender-experts-hunting-overview) is a managed service that provides hunting capabilities for novel emerging threats that aren't yet well known in the industry. The analysts for the hunting service review trends in the threat actor evolution based on world-renowned Microsoft Threat Intelligence and Research. They then apply the insights they gather to hunt for emerging attack vectors within the customer ecosystem.

With deep product expertise powered by threat intelligence, we're uniquely positioned to help you:

1. Focus on novel threat actor evolution in the context of your ecosystem.
2. Get detailed, step-by-step, and actionable guidance from our experts so you can respond to these emerging threats.
3. Seek assistance from Defender Experts.

This document outlines the key infrastructure requirements you must meet and important information on data access and compliance you must know before purchasing the **Microsoft Defender Experts Hunting - XDR** service and its add-on, **Microsoft Defender Experts Hunting - Servers**. Microsoft understands that customers who use our managed services entrust us with their most valued asset, their data.

## Eligibility and licensing

Defender Experts Hunting is a separate service from your existing Microsoft Defender products. Before enrolling in this service, make sure that you have the necessary license and access.

**Microsoft Defender Experts Hunting – XDR**

We require the following licensing prerequisites to enable us to get started with this threat hunting service:

- Microsoft Defender for Endpoint P2 must be licensed and enabled on eligible devices
- Microsoft Defender Antivirus must be licensed and enabled in active mode on devices onboarded to Defender for Endpoint (required for endpoint detection)

The following products are also eligible to get Defender Experts Hunting coverage, and you must have their appropriate product licenses to get started with the service:

- Microsoft Defender for Office 365 P2
- Microsoft Defender for Identity
- Microsoft Defender for Cloud Apps
- Microsoft Entra ID P2

The following product is **not** covered by this service:

- Microsoft Defender for IoT
- Other Microsoft services not mentioned in the previous lists

**Microsoft Defender Experts Hunting - Servers**

Customers who wish to have Defender Experts Hunting coverage for Microsoft Defender for Cloud servers must have the following:

- Defender Experts Hunting - XDR service enrollment
- Defender for Servers Plan 1 or Plan 2 in Microsoft Defender for Cloud

Note

You can't purchase Defender Experts Hunting for partial coverage. You must apply it at the tenant level. All identities and devices are automatically included.

### Defender Experts Hunting coverage

**Microsoft Defender Experts Hunting – XDR**

Defender Experts Hunting - XDR relies on event signals from Defender for Endpoint, Defender for Office 365, Defender for Cloud Apps, Defender for Identity. It also relies on proprietary Microsoft Threat Intelligence sources.

This service also covers servers that have Defender for Endpoint deployed on them with a **Microsoft Defender for Endpoint for Servers** license.

Any detection that's not from Microsoft Defender products (for example, detections from other security vendors) isn't within the scope of Defender Experts Hunting.

**Microsoft Defender Experts Hunting - Servers**

Defender Experts Hunting – Servers provides add-on server coverage, including hybrid and multicloud servers from Defender for Servers.

### Ask Defender Experts

[Ask Defender Experts](defender-experts-hunting-ask-experts) is intended to provide a better understanding of complex threats affecting your organization. It focuses on products included in Microsoft Defender Experts services. [See sample questions you can ask Defender Experts](defender-experts-hunting-ask-experts#sample-questions-you-can-ask-from-defender-experts).

Defender Experts Hunting customers are assigned 10 Ask Defender Experts credits, which you can use to submit questions, at the start of each calendar quarter. Unused credits from the current quarter roll up to the next one. You can use up to 20 credits only per quarter. All unused credits expire by the end of the calendar year or at the end of your subscription term, whichever comes first.

[Learn more about Microsoft's commercial licensing terms](https://www.microsoft.com/licensing/terms/productoffering/Microsoft365/MCA)

## Access requirements

Anyone from your organization can apply for the Defender Experts Hunting service. However, you need to work with your Commercial Executive to transact the SKU.

You might need certain roles and permissions to fully access the service capabilities. Refer to [Custom roles in role-based access control for Microsoft Defender](../custom-roles) for details.

## Service availability and data protection

Defender Experts Hunting - XDR and Defender Experts Hunting - Servers are managed threat hunting services that proactively hunt for threats across endpoints, email, identity, cloud apps, and servers. To carry out hunting on your behalf, Microsoft experts need access to your Microsoft Defender advanced hunting data. Enrolling in this service means you're granting permission to Microsoft experts to access the said data.

The following sections enumerate additional information about the service's data usage, compliance, and availability. For more information about Microsoft's commitment in valuing and protecting your data, visit the [Trust Center](https://www.microsoft.com/trust-center/product-overview) then scroll down to **Additional products and services** &gt; **Managed Security Services** &gt; **Microsoft Defender Experts**.

### Data collection, usage, and retention

- All data used for hunting from existing Defender services continues to reside in the customer's original Microsoft Defender service storage location.
- Data generated for Defender Experts reports and other experiences in the Defender portal is stored in the customer's Microsoft Defender service storage location.
- Defender Experts Hunting for Gov operational data, such as case tickets and analyst notes, is generated and stored in Microsoft data centers in the US region for GCC customers.
- Defender Experts Hunting operational data, such as case tickets and analyst notes, is generated and stored in Microsoft data centers in the EU region for customers whose Defender data is in scope of European Union data boundary.
- Defender Experts Hunting operational data, such as case tickets and analyst notes, is generated and stored in Microsoft data centers worldwide for other customers, irrespective of their Microsoft Defender service storage location.
- Reporting data and operational data will be retained for a grace period of no more than 90 days after a customer's subscription expires. If the customer terminates their subscription, data will be deleted within 30 days.
- Microsoft experts hunt over [advanced hunting logs](../advanced-hunting-schema-tables) in Microsoft Defender advanced hunting tables. The data in these tables depends on the set of Defender services the customer is enabled for (for example, Microsoft Defender for Endpoint, Microsoft Defender for Office 365, Microsoft Defender for Identity, Microsoft Defender for Cloud Apps, and Microsoft Entra ID). Experts also use a large set of internal threat intelligence data to inform their hunting and automation.

Note

Microsoft Defender for Cloud is integrated with Microsoft Defender. This integration allows security teams to access Defender for Cloud alerts and incidents within the Microsoft Defender portal. The Defender Experts Hunting - Servers add-on service accesses data through the Defender portal, so the same data collection, usage, and retention policies apply to this service.

### Security and compliance

When you purchase and onboard to Defender Experts Hunting, you're granting permission to Microsoft experts to access your advanced hunting data.

### Availability

Defender Experts Hunting follows Microsoft 365 and Office 365 international availability. The service is available for customers in our commercial public cloud. In addition, the Defender Experts Hunting for Gov service is available to GCC customers who do not require FedRAMP authorization, such as many State & Local Government (SLG) customers. Defender Experts Hunting is not available in government cloud (i.e. to GCC-H, DoD, etc. customers) and sovereign cloud at this time.

### Languages

This service is currently delivered in English language only.

## Apply for Microsoft Defender Experts Hunting service

You can apply for the Defender Experts Hunting by performing the following steps:

1. Complete the [customer interest form](https://aka.ms/DEX4HuntingCustomerInterestForm).
2. Enter your name, company name, and company email ID.
3. Select **Submit**. Someone from our sales team will reach out within five business days.

### Next step

Continue to the following article to start using Defender Experts Hunting:

- [Start using Defender Experts Hunting](defender-experts-hunting-onboarding)

Tip

Do you want to learn more? Engage with the Microsoft Security community in our Tech Community: [Microsoft Defender XDR Tech Community](https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection).