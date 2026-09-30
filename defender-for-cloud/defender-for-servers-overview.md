---
layout: Conceptual
title: Overview of Defender for Servers in Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-servers-overview
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
description: Get an overview of the Defender for Servers plan in Microsoft Defender for Cloud, including its features and integration with other Defender services.
ms.topic: concept-article
ms.date: 2026-08-10T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
locale: en-us
document_id: c44b3adb-a9ba-817f-a5cf-393b496a2c8e
document_version_independent_id: b84a2037-410b-dea7-4b8b-644fcf3f732e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-servers-overview.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-servers-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-servers-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: b32e1954-ae08-7ff0-467c-e7ce02fcbfca
---

# Overview of Defender for Servers in Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

The Defender for Servers plan in Microsoft Defender for Cloud reduces security risk and exposure for machines in your organization. It provides recommendations to improve and remediate security posture. Defender for Servers also protects machines against real-time security threats and attacks.

Note

Defender for Servers no longer uses the Log Analytics agent or Azure Monitor Agent (AMA) for most plan features. [Agentless machine scanning](concept-agentless-data-collection) and the [integration with Microsoft Defender for Endpoint](integration-defender-for-endpoint) replace these agents for those features. AMA remains a supported collection method for the [500-MB data ingestion benefit](data-ingestion-benefit).

## Benefits

Defender for Servers offers several security benefits.

- **Protect multicloud and on-premises machines**: Defender for Servers protects Windows and Linux machines in multicloud environments (Azure, Amazon Web Services (AWS), Google Cloud Platform (GCP)) and on-premises.
- **Centralize management and reporting**: Defender for Cloud offers a single view of monitored resources, including machines protected by Defender for Servers. Filter, sort, and cross-reference data to understand, investigate, and analyze machine security.
- **Integrate with Defender services**: Defender for Servers integrates with security capabilities provided by Defender for Endpoint and Microsoft Defender Vulnerability Management.
- **Improve posture and reduce risk**: Defender for Servers assesses the security posture of machines against compliance standards and provides security recommendations to remediate and improve security posture.
- **Benefit from agentless scanning**: Defender for Servers Plan 2 provides agentless machine scanning. Without an agent on endpoints, scan software inventory, assess machines for vulnerabilities, scan for machine secrets, and detect malware threats.
- **Protect against threats in near real-time**: Defender for Servers identifies and analyzes real-time threats and issues security alerts as needed.
- **Get intelligent threat detection**: Defender for Cloud evaluates events and detects threats using advanced security analytics and machine-learning technologies with multiple threat intelligence sources, including the [Microsoft Security Response Center (MSRC)](https://www.microsoft.com/msrc).

## Defender for Endpoint integration

Defender for Endpoint and Defender for Vulnerability Management integrate into Defender for Cloud.

This integration allows Defender for Servers to use the endpoint detection and response (EDR) capabilities of Defender for Endpoint. It also enables vulnerability scanning, software inventory, and premium features provided by Defender for Vulnerability Management.

[Learn more](integration-defender-for-endpoint) about the integration.

## Managed detection and response with Defender Experts for Servers

Microsoft Defender Experts for Servers is a managed extended detection and response (XDR) service for server workloads. Microsoft analysts work alongside automation to detect, prioritize, and respond to threats on machines protected by Defender for Servers Plan 1 or Plan 2.

Defender Experts for Servers covers all Plan 1 and Plan 2 alerts where the Detection Source is Microsoft Defender for Servers. Coverage includes Windows and Linux machines on Azure, Amazon Web Services (AWS), Google Cloud Platform (GCP), and on-premises environments. Domain Name System (DNS) alerts aren't in scope.

Defender Experts for Servers includes:

- **Managed detection and response**: Microsoft analysts triage, investigate, and contain incidents on your servers, then hand off with guided steps to fix what's left.
- **Proactive threat hunting**: Defender Experts for Hunting is included. Microsoft hunters search your Defender for Servers data for emerging threats.
- **Ask Defender Experts**: Submit questions about specific incidents, alerts, or threat-actor activity from the Microsoft Defender portal.

Defender Experts for Servers is sold separately. You need Defender for Servers Plan 1 or Plan 2 enabled and Microsoft Defender for Endpoint deployed on your Windows and Linux machines. Defender Experts for Servers is standalone, so you don't need Microsoft Defender Experts for XDR to use it. If you use both, the two complement each other.

Learn more about [Microsoft Defender Experts for Servers](/en-us/defender-xdr/dex-servers-overview).

Learn how to [enable Defender Experts for Servers](/en-us/defender-xdr/get-started-dex-servers).

## Defender for Servers plans

Defender for Servers offers two plans:

- **Defender for Servers Plan 1 (P1)** is entry-level and focuses on the EDR capabilities provided by the Defender for Endpoint integration.
- **Defender for Servers Plan 2 (P2)** provides the same features as Plan 1 and other capabilities.

## Plan pricing

For Defender for Servers pricing, review the [Defender for Cloud pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/). You can also [estimate costs with the Defender for Cloud cost calculator](cost-calculator).

For more details about billing scenarios and licensing, see [Common questions about Defender for Servers](/en-us/azure/defender-for-cloud/faq-defender-for-servers).

## Plan protection features

Plan features are summarized in the table.

For a comparison of AWS and GCP coverage by plan, see the [multicloud workload protection support matrix](multicloud-support-matrix).

| Feature | Plan 1 (P1) | Plan 2 (P2) | Cloud availability |
| --- | --- | --- | --- |
| **Multicloud and hybrid support** | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) | Protects Virtual Machines (VMs) on Azure, AWS and GCP VMs, and on-premises machines that are connected to Microsoft Defender for Cloud.  Review Defender for Servers [support and requirements](support-matrix-defender-for-servers). |
| **Defender for Endpoint automatic onboarding** | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |  |
| [Defender for Endpoint EDR](integration-defender-for-endpoint) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) | Azure, AWS, and GCP |
| [Integrated alerts and incidents](concept-integration-365) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) | Azure, AWS, and GCP |
| [Software inventory discovery](asset-inventory)^1^ | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) | Azure, AWS, and GCP |
| [Regulatory compliance assessment](concept-regulatory-compliance-standards) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) | Different standards are available for different environments. Learn more about [compliance cloud availability](concept-regulatory-compliance-standards#available-compliance-standards). |
| [Vulnerability scanning (agent-based)](auto-deploy-vulnerability-assessment) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) | Azure, AWS, and GCP |
| [Vulnerability scanning (agentless)](concept-agentless-data-collection) | - | ![](media/icons/yes-icon.png) | Azure, AWS, and GCP |
| [Defender for DNS alerts](defender-for-dns-introduction) | - | ![](media/icons/yes-icon.png) | Azure, AWS, and GCP |
| [Threat detection (Azure network layer)](alerts-azure-network-layer) | - | ![](media/icons/yes-icon.png) | Azure |
| [OS system updates](enable-periodic-system-updates) | - | ![](media/icons/yes-icon.png) | Azure, AWS, GCP and on-premises  Only applicable to machines onboarded with Azure ARC. [Learn more](enable-periodic-system-updates). |
| OS baseline misconfigurations based on [Microsoft Cloud Security Benchmark (MCSB)](/en-us/security/benchmark/azure/introduction) recommendations ^2^ | - | ![](media/icons/yes-icon.png) | Azure, AWS, and GCP.  Only applicable to machines onboarded with Azure ARC. |
| [Defender for Vulnerability Management premium features](/en-us/defender-vulnerability-management/defender-vulnerability-management-capabilities)^3^ | - | ![](media/icons/yes-icon.png) | Azure, AWS, GCP |
| [Malware scanning (agentless)](agentless-malware-scanning) | - | ![](media/icons/yes-icon.png) | Azure, AWS, and GCP |
| [Machine secrets scanning (agentless)](concept-agentless-data-collection) | - | ![](media/icons/yes-icon.png) | Azure, AWS, and GCP |
| [File integrity monitoring](file-integrity-monitoring-overview) | - | ![](media/icons/yes-icon.png) | Azure, AWS, and GCP  Only applicable to AWS and GCP machines onboarded with Azure ARC. |
| [Just-in-time virtual machine access](just-in-time-access-overview) | - | ![](media/icons/yes-icon.png) | Azure and AWS |
| [Network map](protect-network-resources) | - | ![](media/icons/yes-icon.png) | Azure |
| [Free data ingestion (500 MB)](data-ingestion-benefit) | - | ![](media/icons/yes-icon.png) |  |

^1^ Software inventory discovery (provided by [Defender Vulnerability Management](/en-us/defender-vulnerability-management/tvm-software-inventory)) is integrated into Defender for Cloud. ^2^ OS baseline misconfigurations for MCSB are included in the [free foundational posture management](concept-cloud-security-posture-management). ^3^ This is only available in the [Defender portal](https://security.microsoft.com/homepage).

## Deployment scope

You should [enable Defender for Servers](tutorial-enable-servers-plan) at the subscription level, but you can enable and disable Defender for Servers at the resource level if you need deployment granularity, as follows:

| **Scope** | **Plan 1** | **Plan 2** |
| --- | --- | --- |
| **Enable for an Azure subscription** | Yes | Yes |
| **Enable for a resource** | Yes | No |
| **Disable for a resource** | Yes | Yes |

- Enable and disable Plan 1 at the resource level per server. A server is defined as a device running a server operating system. For information, refer to [Common questions about Defender for Servers](faq-defender-for-servers).
- Plan 2 can't be enabled at the resource level, but you can disable it at the resource level.

## After enabling

After you enable a Defender for Servers plan, the following rules apply:

- **Trial period**: A 30-day trial period begins. You can't stop, pause, or extend this trial period. To enjoy the full 30-day trial, plan ahead to meet your evaluation goals.
- **Endpoint protection**: Microsoft Defender for Endpoint extension is automatically installed on all supported machines connected to Microsoft Defender for Cloud. Disable automatic provisioning if needed.
- **Vulnerability assessment**: Microsoft Defender Vulnerability Management is enabled by default on machines with the Microsoft Defender for Endpoint extension installed.
- **Agentless scanning**: [Agentless scanning](concept-agentless-data-collection) is enabled by default when you enable Defender for Servers Plan 2.
- **OS configuration assessment**: When you enable Defender for Servers Plan 2, Microsoft Defender for Cloud [assesses operation system configuration settings](operating-system-misconfiguration) against compute security baselines in Microsoft Cloud Security Benchmark. To use this feature, machines must run the Azure Machine Configuration extension. [Learn more](security-baseline-guest-configuration) about setting up the extension.
- **File integrity monitoring**: You set up [file integrity monitoring](file-integrity-monitoring-overview) after enabling Defender for Servers Plan 2.