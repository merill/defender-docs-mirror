---
layout: Conceptual
title: Microsoft Sentinel solution for SAP applications overview | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sap/sap-applications-overview
breadcrumb_path: ../breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
ms.reviewer: mapankra
description: Learn how the Microsoft Sentinel solution for SAP applications helps detect, investigate, and respond to threats in SAP systems.
ms.author: monaberdugo
author: mberdugo
ms.topic: overview
ms.date: 2026-08-13T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
locale: en-us
document_id: 1792328c-4720-4ba4-b313-5e186d235793
document_version_independent_id: e7c5f57b-afb4-3a73-948c-b6c8ca495f55
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sap/sap-applications-overview.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/sap/sap-applications-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sap/sap-applications-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 662fa381-b50a-a24c-8eab-a0eb397f956f
---

# Microsoft Sentinel solution for SAP applications overview | Microsoft Learn

The Microsoft Sentinel solution for SAP applications monitors SAP systems for threats at the business logic, application, database, and operating system layers. This article walks through what's in the solution: how it collects SAP data, the security content it ships, and what it detects.

For SIEM and SOAR capabilities, investigation guidance, certification, and pricing that apply to the wider Microsoft Sentinel solutions for SAP, see the [Microsoft Sentinel solutions for SAP overview](solution-overview).

## Solution components

The solution includes three main components:

- **Agentless data connector**: Collects SAP application logs from your onboarded SAP systems and sends them to your Microsoft Sentinel workspace. The connector uses SAP Cloud Integration as middleware, so no dedicated data-collector VM or container is required in your SAP landscape.
- **SAP Integration Suite solution package**: A prebuilt package that you deploy to your SAP Integration Suite tenant. It ships the integration flows and configuration that enrich and route the SAP logs through the SAP Cloud Connector to Microsoft Sentinel Solution for SAP.
- **Security content**: Out-of-the-box analytics rules, workbooks, playbooks, watchlists, and functions that turn SAP logs into actionable insights.

For deeper explanations of each component and how they fit together, see [Deployment overview](deployment-overview#solution-components).

## SAP data sources

The agentless data connector ingests security-relevant logs such as:

- SAP Security Audit Log.
- Change document logs (CDHDR, CDPOS).
- User master data, including roles and authorizations.

For the full list of logs and tables, see the [SAP solution log and table reference](sap-solution-log-reference).

Additional sources broaden the picture beyond the core ABAP application logs:

- **SAP HANA database audit logs** via the [HANA database connector](collect-sap-hana-audit-logs), covering database-level activity such as privileged access, schema changes, and sensitive queries.
- **SAP LogServ (RISE with SAP)** for infrastructure and platform logs — SAP Cloud Connector, AS Java, Web Dispatcher, HANA, operating system, network, and more — collected and forwarded by SAP Enterprise Cloud Services. See the [SAP LogServ overview](sap-logserv-overview).
- **Other Microsoft Sentinel connectors** for signals adjacent to your SAP estate, such as Microsoft Entra ID, Microsoft Defender for Cloud, Microsoft Defender for Endpoint, and firewall or proxy logs, so SAP activity can be correlated with identity, endpoint, and network events. Where these connectors emit data normalized to the [Advanced Security Information Model (ASIM)](../normalization), the SAP solution's analytics rules can reuse them directly. For the list of ASIM-aligned content, see [ASIM security content](../normalization-content).

## Threat detection coverage

The solution supports threat detections such as the following, and more:

- **Suspicious privilege operations**, such as privileged user creation or usage of break-glass users.
- **Attempts to bypass SAP security mechanisms**, such as disabling audit logging or executing sensitive function modules.
- **Backdoor creation (persistence)**, such as creating new Internet-facing interfaces (ICF) or directly accessing sensitive tables by remote function call.
- **Data exfiltration**, such as multiple file downloads.
- **Initial access**, such as brute force or multiple sign-ins from the same IP.

For more information, see [Built-in analytics rules](sap-solution-security-content#built-in-analytics-rules).

## Monitored SAP configuration

Beyond activity monitoring, the solution tracks changes to sensitive SAP security parameters and system health to help you catch drift and misconfigurations. For more information, see:

- [Monitored SAP security parameters](sap-suspicious-configuration-security-parameters)
- [Monitor SAP system health and role](../monitor-sap-system-health)

## Solution pricing

While the Microsoft Sentinel **SAP applications** solution is free to install, there's an extra hourly charge for activating and using the solution on production systems.

- The extra hourly charge applies to connected, active **production systems only**. Inactive systems aren't subject to charges. If a system's status is unknown to Microsoft Sentinel, such as because of permission issues, it's counted as a production system.
- Microsoft Sentinel identifies a production system by looking at the configuration on the SAP system.

Microsoft Sentinel ingestion costs might vary and are influenced by the volume of SAP logs ingested. For more information, see:

- [Plan costs and understand Microsoft Sentinel pricing and billing](../billing)
- [Reduce costs for Microsoft Sentinel](../billing-reduce-costs)
- [Manage and monitor costs for Microsoft Sentinel](../billing-monitor-costs)
- [Microsoft Sentinel solution for SAP applications](https://azure.microsoft.com/pricing/offers/microsoft-sentinel-sap-promo/).