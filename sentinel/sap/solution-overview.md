---
layout: Conceptual
title: Microsoft Sentinel solutions for SAP overview | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sap/solution-overview
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
description: Learn how Microsoft Sentinel solutions address threats in SAP applications, SAP BTP, and partner integrations.
ms.author: monaberdugo
author: mberdugo
ms.topic: overview
ms.date: 2026-08-13T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
locale: en-us
document_id: 1c9d0078-d309-fe1a-08d2-37e31830b795
document_version_independent_id: 63b922b0-48d3-93b9-d046-0cfd6fffbf8f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sap/solution-overview.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/sap/solution-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sap/solution-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 32f4a907-b278-0f5c-9354-23fa9b22a19e
---

# Microsoft Sentinel solutions for SAP overview | Microsoft Learn

SAP systems pose a unique security challenge, as they handle sensitive information, are a prime target for attackers, and traditionally provide little visibility for security operations teams.

An SAP system breach could result in stolen files, exposed data, or a disrupted supply chain. Once an attacker is in the system, there are few controls to detect exfiltration or other bad acts. SAP activity needs to be correlated with other data throughout the organization for effective threat detection.

## Learn from recent SAP attacks

SAP cyber threats can reach beyond the SAP system itself. In April 2026, a supply chain attack on SAP Cloud Application Programming Model (CAP) showed how compromised development components can put SAP BTP environments and business data at risk. Read the [Microsoft Security blog](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/the-worm-in-the-supply-chain-how-defender-for-endpoint-and-sentinel-for-sap-btp-/4526246) to learn how Defender for Endpoint and Microsoft Sentinel help detect and investigate this type of threat.

Watch the [end-to-end attack replay](https://aka.ms/sentinel-for-sap-hero-demo) to see the detection and response flow and Security Copilot assistance in action.

## Sentinel solutions and extensions for SAP

Microsoft Sentinel provides two Microsoft-owned foundation solutions for SAP. Deploy the one (or both) that matches your SAP footprint:

- [Microsoft Sentinel solution for SAP applications](sap-applications-overview): Monitors SAP application layers such as business logic, applications, databases, and operating systems. This is the foundation most SAP customers start with.
- [Microsoft Sentinel solution for SAP BTP](sap-btp-solution-overview): Monitors SAP Business Technology Platform (BTP), including BTP-based applications and services. It's independent of the SAP applications solution, so you can deploy it alongside or on its own if BTP is your only SAP footprint.

Extend the SAP applications foundation with:

- [SAP LogServ](sap-logserv-overview): Add infrastructure and platform logs collected by SAP SE as part of the RISE with SAP offering.
- [Partner add-ons](solution-partner-overview): Add SAP SE–provided and third-party partner integrations with specialized detections, connectors, and playbooks.
- [Community contributions](solution-partner-overview#solutions-provided-by-the-community): Adopt extension patterns, integration recipes, and scenario blueprints that customers, partners, and Microsoft engineers share in the [Sentinel for SAP community repository](https://github.com/Azure-Samples/Sentinel-For-SAP-Community) on GitHub.

## Understand the solution boundaries

The Microsoft-owned [Microsoft Sentinel solution for SAP applications](sap-applications-overview) and [Microsoft Sentinel solution for SAP BTP](sap-btp-solution-overview) are separate solutions for different SAP layers. The BTP solution isn't the agentless data connector. The connector uses SAP Integration Suite, which runs on BTP, as middleware to collect SAP application data.

## SIEM and SOAR features

The Microsoft-owned Sentinel solutions for SAP combine SIEM and SOAR to cover your SAP landscape end-to-end:

- **Security information and event management (SIEM)**: Correlate SAP application and SAP BTP activity with other signals throughout your organization. Use out-of-the-box and custom detections to monitor business risks such as privilege escalation, unapproved changes, unauthorized access, and misuse of sensitive transactions or BTP services.
- **Security orchestration, automation, and response (SOAR)**: Build automated response processes that interact with your SAP systems and BTP tenants to stop active security threats.

## Investigation support

Investigate SAP incidents just as you would any other incidents in Microsoft Sentinel and Microsoft Defender. For more information, see:

- [Navigate and investigate incidents in Microsoft Sentinel](../investigate-incidents)
- [Investigate and respond with Microsoft Defender XDR](/en-us/defender-xdr/incident-response-overview)

## Certification

The Microsoft-owned Microsoft Sentinel solutions for SAP are officially listed on the [SAP Business Accelerator Hub](https://api.sap.com/package/MicrosoftSentinelSolutionforSAP/overview). The certified [Microsoft Sentinel solution for SAP applications](sap-applications-overview) is available for:

- SAP ECC, Business Suite, and other SAP NetWeaver-based products running in any cloud or on-premises.
- SAP S/4HANA Cloud Private Edition (RISE).
- Hybrid deployments that cover the entire customer estate.

The [Microsoft Sentinel solution for SAP BTP](sap-btp-solution-overview) covers SAP Business Technology Platform tenants using the official audit log API. For SAP SE–owned and partner-owned solutions, see [SAP LogServ](sap-logserv-overview) and [Partner add-ons](solution-partner-overview).