---
layout: Conceptual
title: Data handling and privacy in Microsoft Defender as part of Agent 365 - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/security-for-ai/privacy-defender-agent-365
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how Microsoft Defender handles customer data and supports your privacy requirements when delivered as part of Microsoft Agent 365.
ms.service: microsoft-defender
ms.update-cycle: 180-days
ms.topic: concept-article
ms.date: 2026-05-03T00:00:00.0000000Z
audience: Admin
author: guywi-ms
ms.author: guywild
ms.reviewer: shimie
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1012
locale: en-us
document_id: ac1456c0-d3ab-3153-1139-87561cc5eabc
document_version_independent_id: ac1456c0-d3ab-3153-1139-87561cc5eabc
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/security-for-ai/privacy-defender-agent-365.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-for-ai/privacy-defender-agent-365
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/security-for-ai/privacy-defender-agent-365.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 4ecfba98-cf6d-e7a7-a393-b4cd7f1993c4
---

# Data handling and privacy in Microsoft Defender as part of Agent 365 - Microsoft Defender XDR | Microsoft Learn

As part of [Microsoft Agent 365](https://www.microsoft.com/microsoft-agent-365), Microsoft Defender provides AI agent security capabilities, including agent discovery, posture assessment, threat detection, and real-time protection. These capabilities, which are part of the **Security for AI** experience in the Microsoft Defender portal, give security teams visibility into AI agents and infrastructure, supporting detection, investigation, and response to risks such as prompt-based attacks, unsafe tool usage, credential exposure, and data exfiltration. For more information, see [Protect AI agents using Microsoft Defender](defender-security-for-ai#protect-ai-agents-using-microsoft-defender).

This article describes how Microsoft Defender collects, stores, and uses data for these AI agent security capabilities. For commitments that apply to all Agent 365 services, see [Data handling, data residency, and compliance in Agent 365 observability](/en-us/microsoft-agent-365/admin/data-residency-protection-compliance).

## Data collected

As part of its AI agent security capabilities, Microsoft Defender collects:

- **Observability trace payloads** submitted by agents during execution. Payloads might include session inputs and outputs, depending on how the developer instruments the agent. Customers and developers control what's included in trace payloads by configuring their agent instrumentation.
- **Agent configuration attributes** from the Agent 365 registry and, for local agents on devices, from Microsoft Defender for Endpoint. Examples: agent name, type, version, configured tools, connected models, and published locations.
- **User identifiers**, such as Microsoft Entra user IDs, associated with agent sessions.
- **Pseudonymized identifiers** derived from user data, used for analytics and trend detection without directly exposing identifiable information.
- **Tenant, subscription, and agent identifiers** used to partition, route, and attribute observability data to the correct organization.

Administrators can independently enable or disable these capabilities from the [Defender settings page](https://security.microsoft.com), without affecting other Agent 365 services. Customers also control the data collected through agent instrumentation and Defender configuration settings.

## Data storage location

As part of Agent 365, Microsoft Defender operates in the following Azure regions:

| Tenant provisioning location | Data storage location |
| --- | --- |
| European Union or United Kingdom | European Union |
| All other regions | United States |

Once created, the tenant can't be moved to a different location.

## Data retention

As part of Agent 365, Microsoft Defender retains:

- **Observability and session data**, such as trace payloads, inputs and outputs, and user identifiers, for up to 30 days. During this time, the data is available in the Microsoft Defender portal.
- **Agent inventory data and data shared with [Microsoft Defender](/en-us/defender-xdr/data-privacy)** for up to 180 days.

Microsoft Defender deletes this customer data within 30 days of contract termination or expiration.

## Data use

Microsoft uses patterns and threat intelligence seen across multiple tenants to improve its prevention and detection capabilities, in accordance with the privacy commitments in the [Microsoft Privacy Statement](https://privacy.microsoft.com/privacystatement).

Microsoft doesn't use customer data to train AI models without user consent. As per the [Microsoft Product Terms](https://www.microsoft.com/licensing/terms/), Microsoft doesn't use customer data to train any generative AI foundation model, unless pursuant to the customer's documented instructions.

## Data sharing within Microsoft

As part of Agent 365, Microsoft Defender shares data, including customer data, with other Microsoft products the customer has licensed. These might include:

- Microsoft Defender
- Microsoft Defender for Endpoint
- Microsoft Security Exposure Management
- Microsoft Entra ID Protection

For customers in the Government Community Cloud (GCC), data sharing between government and commercial cloud environments might occur, depending on the location of the service offering.