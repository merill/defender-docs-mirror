---
layout: Conceptual
title: Microsoft Sentinel in the Microsoft Defender portal | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/microsoft-sentinel-defender-portal
breadcrumb_path: breadcrumb/toc.json
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
description: Learn how Microsoft Sentinel integrates into the Microsoft Defender portal, compare capabilities with the Azure portal experience, and plan your transition.
ms.author: guywild
author: guywi-ms
ms.reviewer: soulisabag
ms.topic: overview
ms.date: 2026-06-18T00:00:00.0000000Z
ms.collection: usx-security
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: d90c1ec3-1323-0cf2-b10a-9bdc104b9f3a
document_version_independent_id: 591e2fc1-c503-258e-e0b2-fc4394590f5e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/microsoft-sentinel-defender-portal.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/microsoft-sentinel-defender-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/microsoft-sentinel-defender-portal.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 561d77c0-ef3a-ee02-3b45-ecd664f5299f
---

# Microsoft Sentinel in the Microsoft Defender portal | Microsoft Learn

Microsoft Defender provides a unified cybersecurity solution that integrates endpoint protection, cloud security, identity protection, email security, threat intelligence, exposure management, and SIEM into a centralized platform powered by a modern data lake. It uses AI-driven defense to help organizations anticipate and stop attacks, ensuring efficient and effective security operations.

Microsoft Sentinel is generally available in the Microsoft Defender portal, either with [Microsoft Defender](/en-us/defender-xdr/microsoft-365-defender) or on its own, delivering a unified SIEM and XDR experience for faster and more accurate threat detection and response, simplified workflows, and enhanced operational efficiency.

This article describes the Microsoft Sentinel experience in the Defender portal. The following sections compare capabilities, list navigation changes, and identify features that are limited without Defender services.

Microsoft Sentinel is generally available in the Microsoft Defender portal, including for customers without Microsoft Defender XDR or an E5 license. You can use Microsoft Sentinel in the Defender portal even if you aren't using other Microsoft Defender services.

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal.

If you're currently using Microsoft Sentinel in the Azure portal, we recommend that you start planning your transition to the Defender portal now to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

For more information, see:

- [Transition your Microsoft Sentinel environment to the Defender portal](move-to-defender)
- [Planning your move to Microsoft Defender portal for all Microsoft Sentinel customers](https://techcommunity.microsoft.com/blog/microsoft-security-blog/planning-your-move-to-microsoft-defender-portal-for-all-microsoft-sentinel-custo/4428613) (blog)

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Feature comparison: Microsoft Sentinel in the Azure portal vs. the Defender portal

The following tables compare Microsoft Sentinel capabilities in the Azure portal with capabilities in the Defender portal.

### Incidents and investigation

| **Capability area** | **Sentinel in Azure portal** | **Sentinel in Defender portal** | **Benefits** |
| --- | --- | --- | --- |
| Core SIEM capabilities | Full SIEM functionality (ingestion, analytics rules, incidents, workbooks, hunting) | Full SIEM functionality integrated into unified SIEM and Defender experience. | Same SIEM power, better operating model |
| Incident management | Sentinel incident queue separate from Defender | [Unified incident queue](/en-us/defender-xdr/incidents-overview) for SIEM and XDR, with [Security Copilot for incident investigation](sentinel-security-copilot) to summarize and respond. Incidents are automatically enriched with Defender signals. | Single pane of glass, deeper analyst insights |
| Alert correlation and threat detection | Separate correlation for Sentinel and Defender incidents | Automatic [cross-domain correlation](/en-us/defender-xdr/incidents-overview) with AI/ML for faster threat detection. | Reduced alert fatigue, full attack story in one incident |
| Investigation experience | Log-centric workflows | [Attack story and incident graph](/en-us/defender-xdr/investigate-incidents#attack-story) with [unified entity pages](entity-pages) for devices, users, IPs, and Azure resources. Includes [blast radius analysis](/en-us/defender-xdr/investigate-incidents#blast-radius-analysis) to visualize possible attack propagation paths and assess business impact. Entity pages combine Sentinel and Defender data to provide expanded investigation context. | Visual investigation, faster root-cause analysis |
| Threat intelligence (TI) | TI managed within Sentinel | Rich TI embedded in incidents, hunting, and investigations including premium Microsoft Threat Intelligence feed. | Better intelligence, operationalized out of the box |

### Hunting and AI

| **Capability area** | **Sentinel in Azure portal** | **Sentinel in Defender portal** | **Benefits** |
| --- | --- | --- | --- |
| Advanced hunting | Sentinel-only (Log Analytics) | Unified [advanced hunting](https://go.microsoft.com/fwlink/p/?linkid=2264410) for SIEM, Defender, and the data lake, with [Security Copilot in advanced hunting](/en-us/defender-xdr/advanced-hunting-security-copilot) for KQL generation. Supports hunting in the tenant and workspaces and reuse of existing Sentinel workspace queries and functions. | Broader dataset, richer context, no context-switching |
| AI-assisted SOC (Security Copilot) | Not available | Native Security Copilot: [automated incident summary](/en-us/defender-xdr/security-copilot-m365d-incident-summary), [guided response actions](/en-us/defender-xdr/security-copilot-m365d-guided-response), [script analysis](/en-us/defender-xdr/security-copilot-m365d-script-analysis), [file analysis](/en-us/defender-xdr/copilot-in-defender-file-analysis), [incident reports](/en-us/defender-xdr/security-copilot-m365d-create-incident-report), and [autonomous Security Copilot agents](/en-us/defender-xdr/security-copilot-agents-defender) for alert triage, threat intelligence briefing, and [threat hunting](/en-us/defender-xdr/advanced-hunting-security-copilot-threat-hunting-assistant). [Included capacity for E5/E7 customers](/en-us/copilot/security/security-copilot-inclusion). | Faster investigation, lower skill barrier, agentic defense |
| Post-incident recommendations | Not available | Tailored recommendations via [Exposure Management](/en-us/security-exposure-management/microsoft-security-exposure-management), including attack path analysis to identify exploitable vulnerabilities. | Proactive posture improvement |

### Automation and workflow

| **Capability area** | **Sentinel in Azure portal** | **Sentinel in Defender portal** | **Benefits** |
| --- | --- | --- | --- |
| Automation and SOAR | Manual playbook creation | AI-assisted [playbook generator](automation/generate-playbook) and integrated SOAR, including [automatic attack disruption](/en-us/defender-xdr/automatic-attack-disruption) | Faster response, reduced manual effort |
| Case management | Not available | [Case management](/en-us/defender-xdr/siem-defender-case-management) for managing incident response work, tasks, evidence, and activity history | Track response work and case activity in one place |
| SOC workflow / UX | Multiple portals, tool switching | Unified SecOps experience in the Defender portal | Less context-switching, faster response |
| SOC optimization | Limited, fragmented views | Guided [SOC optimization](soc-optimization/soc-optimization-access) recommendations, available [programmatically via API](soc-optimization/soc-optimization-api); see [optimization reference](soc-optimization/soc-optimization-reference) | More actionable guidance, measurable improvements |

### Data and cost

| **Capability area** | **Sentinel in Azure portal** | **Sentinel in Defender portal** | **Benefits** |
| --- | --- | --- | --- |
| Data lake and long-term analytics | Log Analytics-centric | Centralized [data lake](datalake/sentinel-lake-overview) with tiered retention, massive-scale analytics, and simplified onboarding | Enterprise-wide visibility, lower costs at scale |
| Cost and data optimization | Separate billing models | Unified schema for Sentinel and Defender, with [advanced hunting raw logs free for 30 days without ingestion](/en-us/defender-xdr/advanced-hunting-microsoft-defender#what-to-expect-for-defender-xdr-tables-streamed-to-microsoft-sentinel) | Simplified billing, reduced ingestion costs |
| Defender data integration | Enable the Defender XDR connector in Sentinel | Automatically integrates Sentinel with Defender | Defender data integrated by default |
| Unified data model | Separate schemas | Normalized schema for Defender and SIEM | Simpler queries, less transform work |

### Platform and administration

| **Capability area** | **Sentinel in Azure portal** | **Sentinel in Defender portal** | **Benefits** |
| --- | --- | --- | --- |
| Innovation focus / roadmap | Maintenance and parity only | Primary innovation surface, all new Sentinel experiences land here first | Faster access to new capabilities, optimized workflows |
| Multi-tenant / MSSP operations | Azure Lighthouse | Native multi-tenant operations (MTO) with easy delegation and management | Centralized SOC management |
| Cross-tenant visibility | Manual | Unified cross-tenant incidents and alerts | MSSP efficiency |
| RBAC model | Azure RBAC | Unified Defender RBAC, with row-level RBAC support | Granular permissions, simpler administration |
| Extensibility and APIs | Sentinel APIs | Unified Defender and Sentinel APIs | Broader integration surface |
| Support timeline | Supported until March 31, 2027 | Long-term home for Sentinel | Future-proof investment |

## Limited or unavailable capabilities with Microsoft Sentinel only in the Defender portal

When you onboard Microsoft Sentinel to the Defender portal without enabling Defender capabilities or other services, the following capabilities are limited or unavailable:

- [Microsoft Security Exposure Management](/en-us/security-exposure-management/microsoft-security-exposure-management)
- [Custom detection rules](/en-us/defender-xdr/custom-detections-overview), provided by Microsoft Defender
- The [Action center](/en-us/defender-xdr/m365d-action-center), provided by Microsoft Defender

## Quick reference

Some Microsoft Sentinel capabilities, like the unified incident queue, are integrated with other Microsoft Defender capabilities in the Defender portal. Many other Microsoft Sentinel capabilities are available in the **Microsoft Sentinel** section of the Defender portal.

The following image shows the Microsoft Sentinel menu in the Defender portal:

[![Screenshot of the Defender portal left navigation with the Microsoft Sentinel section.](media/microsoft-sentinel-defender-portal/navigation-defender-portal.png)](media/microsoft-sentinel-defender-portal/navigation-defender-portal.png#lightbox)

The following sections describe where to find Microsoft Sentinel features in the Defender portal. They're intended for existing customers who are moving to the Defender portal. The sections are organized as Microsoft Sentinel is in the Azure portal.

For more information, see [Transition your Microsoft Sentinel environment to the Defender portal](move-to-defender).

### General

The following table lists the changes in navigation between the Azure and Defender portals for the **General** section in the Azure portal.

| Azure portal | Defender portal |
| --- | --- |
| **Overview** | **Overview** |
| **Logs** | **Investigation & response** &gt; **Hunting** &gt; **Advanced hunting** |
| **News & guides** | Not available |
| **Search** | **Microsoft Sentinel** &gt; **Search** |

### Threat management

The following table lists the changes in navigation between the Azure and Defender portals for the **Threat management** section in the Azure portal.

| Azure portal | Defender portal |
| --- | --- |
| **Incidents** | **Investigation & response** &gt; **Incidents & alerts** &gt; **Incidents** |
| **Workbooks** | **Microsoft Sentinel** &gt; **Threat management** &gt; **Workbooks** |
| **Hunting** | **Microsoft Sentinel** &gt; **Threat management** &gt; **Hunting** |
| **Notebooks** | **Microsoft Sentinel** &gt; **Threat management** &gt; **Notebooks** |
| **Entity behavior** | *User entity page:***Assets** &gt; **Identities** &gt; *{user}* &gt; **Sentinel events**AND*Device entity page:***Assets** &gt; **Devices** &gt; *{device}* &gt; **Sentinel events**Also, find the entity pages for the user, device, IP, and Azure resource entity types from incidents and alerts as they appear. |
| **Threat intelligence** | **Threat intelligence** &gt; **Intel management** |
| **MITRE ATT&CK** | **Microsoft Sentinel** &gt; **Threat management** &gt; **MITRE ATT&CK** |

### Content management

The following table lists the changes in navigation between the Azure and Defender portals for the **Content management** section in the Azure portal.

| Azure portal | Defender portal |
| --- | --- |
| **Content hub** | **Microsoft Sentinel** &gt; **Content management** &gt; **Content hub** |
| **Repositories** | **Microsoft Sentinel** &gt; **Content management** &gt; **Repositories** |
| **Community** | **Microsoft Sentinel** &gt; **Content management** &gt; **Community** |

### Configuration

The following table lists the changes in navigation between the Azure and Defender portals for the **Configuration** section in the Azure portal.

| Azure portal | Defender portal |
| --- | --- |
| **Workspace manager** | Not available |
| **Data connectors** | **Microsoft Sentinel** &gt; **Configuration** &gt; **Data connectors** |
| **Analytics** | **Microsoft Sentinel** &gt; **Configuration** &gt; **Analytics**AND**Investigation and response** &gt; **Hunting** &gt; **Custom detection rules** |
| **Watchlists** | **Microsoft Sentinel** &gt; **Configuration** &gt; **Watchlists** |
| **Automation** | **Microsoft Sentinel** &gt; **Configuration** &gt; **Automation** |
| **Settings** | **System** &gt; **Settings** &gt;**Microsoft Sentinel** |