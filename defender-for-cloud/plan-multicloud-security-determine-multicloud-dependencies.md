---
layout: Conceptual
title: Determine Multicloud CSPM and CWPP Dependencies - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/plan-multicloud-security-determine-multicloud-dependencies
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
description: Learn about determining multicloud dependencies when planning multicloud deployment with Microsoft Defender for Cloud.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 8e774487-bfd7-456f-e5b1-966de2ad73e7
document_version_independent_id: 96bf1185-ef40-38be-c10a-38bcbf4b1000
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/plan-multicloud-security-determine-multicloud-dependencies.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/plan-multicloud-security-determine-multicloud-dependencies
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/plan-multicloud-security-determine-multicloud-dependencies.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/beac614b-f66d-40ed-a947-3996de709333
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/9da05372-4706-43ec-a899-f436adab380d
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
platformId: 8d7861e4-32e3-dc59-fec0-e9a2ef6780c0
---

# Determine Multicloud CSPM and CWPP Dependencies - Microsoft Defender for Cloud | Microsoft Learn

This article describes the dependencies and components you need to deploy cloud security posture management (CSPM) and cloud workload protection platform (CWPP) for Amazon Web Services (AWS) and Google Cloud Platform (GCP) resources with Microsoft Defender for Cloud. Identify agents, extensions, and networking requirements before you onboard multicloud connectors.

## Multicloud dependency planning goals

Identify dependencies that might influence the design of your multicloud security solution.

## Identify required multicloud components

As you design your multicloud solution, you need a clear picture of the components needed to use all multicloud features in Defender for Cloud.

## CSPM dependencies and requirements

Defender for Cloud provides cloud security posture management (CSPM) features for your Amazon Web Services (AWS) and Google Cloud Platform (GCP) workloads.

- After you onboard AWS and GCP, Defender for Cloud starts assessing your multicloud workloads against industry standards, and reports on your security posture.
- CSPM features are agentless and don't rely on other components beyond successful onboarding of AWS and GCP connectors.
- The Security Posture Management plan is turned on by default and can't be turned off.
- Learn about the [identity and access management (IAM) permissions](quickstart-onboard-aws?pivots=env-settings) needed to discover AWS resources for CSPM.

## CWPP dependencies and requirements

Note

The Log Analytics agent retired in August 2024. In Defender for Cloud, **Defender for Servers** features and capabilities are provided through Microsoft Defender for Endpoint integration or agentless scanning, without dependency on the Log Analytics agent (MMA) or Azure Monitor agent (AMA).

In Defender for Cloud, enable specific plans to get cloud workload protection platform (CWPP) features. Plans to protect multicloud resources include:

- [Defender for Servers](defender-for-servers-introduction): Protect AWS and GCP Windows and Linux machines.
- [Defender for Containers](defender-for-containers-introduction): Help secure your Kubernetes clusters with security recommendations and hardening, vulnerability assessments, and runtime protection.
- [Defender for SQL](defender-for-sql-usage): Protect SQL databases running in AWS and GCP.

### What extension do I need?

The following table summarizes extension requirements for CWPP.

| Extension | Defender for Servers | Defender for Containers | Defender for SQL on Machines |
| --- | --- | --- | --- |
| Azure Arc agent | Yes | Yes | Yes |
| Microsoft Defender for Endpoint extension | Yes | No | No |
| Vulnerability assessment | Yes | No | No |
| Agentless disk scanning | Yes | Yes | No |
| Defender sensor | No | Yes | No |
| Azure Policy for Kubernetes | No | Yes | No |
| Kubernetes audit log data | No | Yes | No |
| SQL Servers on machines | No | No | Yes |
| Automatic SQL Server discovery and registration | No | No | Yes |

### Defender for Servers dependencies

When you enable Defender for Servers on your AWS or GCP connector, Defender for Cloud can protect your Google Compute Engine VMs and AWS EC2 instances.

#### Review plans

Defender for Servers offers two plans:

- **Plan 1:**

    - **Microsoft Defender for Endpoint (MDE) integration:** Plan 1 integrates with [Microsoft Defender for Endpoint Plan 2](/en-us/microsoft-365/security/defender-endpoint/defender-endpoint-plan-1-2) to provide a full endpoint detection and response (EDR) solution for machines that run a [range of operating systems](/en-us/microsoft-365/security/defender-endpoint/minimum-requirements). Defender for Endpoint features include:

        - [Reducing the attack surface](/en-us/microsoft-365/security/defender-endpoint/overview-attack-surface-reduction) for machines.
        - Providing [antivirus](/en-us/microsoft-365/security/defender-endpoint/next-generation-protection) capabilities.
        - Threat management, including [threat hunting](/en-us/microsoft-365/security/defender-endpoint/advanced-hunting-overview), [detection](/en-us/microsoft-365/security/defender-endpoint/overview-endpoint-detection-response), [analytics](/en-us/microsoft-365/security/defender-endpoint/threat-analytics), and [automated investigation and response](/en-us/microsoft-365/security/defender-endpoint/overview-endpoint-detection-response).
    - **Provisioning:** Automatic provisioning of the Defender for Endpoint sensor on every supported machine that's connected to Defender for Cloud.
    - **Licensing:** Charges Defender for Endpoint licenses per hour instead of per device, lowering costs by protecting virtual machines only when they're in use.
- **Plan 2:** Includes all the components of Plan 1 along with extra capabilities such as File Integrity Monitoring (FIM), Just-in-time (JIT) VM access, and more.

Review the [features of each plan](defender-for-servers-introduction) before onboarding to Defender for Servers.

#### Review components for Defender for Servers

To get full protection from the Defender for Servers plan, you need the following components and requirements:

- **Azure Arc agent**: AWS and GCP machines connect to Azure by using Azure Arc. The Azure Arc agent connects them.

    - The Azure Arc agent is needed to read security information on the host level and allow Defender for Cloud to deploy the agents and extensions required for complete protection.
    - To autoprovision the Azure Arc agent, configure the OS Config agent on [GCP VM instances](quickstart-onboard-gcp?pivots=env-settings) and the AWS Systems Manager (SSM) agent for [AWS EC2 instances](quickstart-onboard-aws?pivots=env-settings). For more information, see [Azure Arc agent overview](/en-us/azure/azure-arc/servers/agent-overview).
- **Defender for Endpoint capabilities**: The [Microsoft Defender for Endpoint](integration-defender-for-endpoint?tabs=linux) agent provides comprehensive endpoint detection and response (EDR) capabilities.
- **Vulnerability assessment**: Using either the integrated [Qualys vulnerability scanner](deploy-vulnerability-assessment-vm) or the [Microsoft Defender Vulnerability Management](/en-us/microsoft-365/security/defender-vulnerability-management/defender-vulnerability-management) solution.

#### Check networking requirements

Machines must meet [network requirements](/en-us/azure/azure-arc/servers/network-requirements?tabs=azure-cloud) before onboarding the agents. Autoprovisioning is enabled by default.

### Defender for Containers dependencies

When you enable Defender for Containers, your GKE and EKS clusters and underlying hosts get [agentless security capabilities](defender-for-containers-introduction#agentless-capabilities).

#### Review components for Defender for Containers

The following components are [required for Defender for Containers](defender-for-containers-introduction):

- **Azure Arc agent**: Connects your GKE and EKS clusters to Azure and onboards the Defender sensor.
- [Defender sensor](defender-for-cloud-glossary#defender-sensor): Provides host-level runtime threat protection.
- **Azure Policy for Kubernetes**: Extends Gatekeeper v3, an admission controller that enforces policies on Kubernetes clusters. It monitors every request to the Kubernetes API server and ensures that security best practices are being followed on clusters and workloads.
- **Kubernetes audit logs**: Audit logs from the Kubernetes API server allow Defender for Containers to identify suspicious activity in your multicloud servers and provide deeper insights during alert investigation. Enable Kubernetes audit log collection at the connector level.

#### Check networking requirements for Defender for Containers

Ensure that your clusters meet network requirements so that the Defender sensor can connect with Defender for Cloud.

### Defender for SQL dependencies

Defender for SQL provides threat detection for Google Compute Engine and AWS workloads. Enable the Defender for SQL Servers on Machines plan on the subscription where the connector is located.

#### Review components for Defender for SQL

To receive the full benefits of Defender for SQL on your multicloud workload, you need these components:

- **Azure Arc agent**: AWS and GCP machines connect to Azure by using Azure Arc. The Azure Arc agent connects them.

    - The Azure Arc agent is needed to read security information on the host level and allow Defender for Cloud to deploy the agents and extensions required for complete protection.
    - To autoprovision the Azure Arc agent, the operating system configuration agent on [GCP VM instances](quickstart-onboard-gcp?pivots=env-settings) and the AWS Systems Manager (SSM) agent for [AWS EC2 instances](quickstart-onboard-aws?pivots=env-settings) must be configured. For more information, see the [Azure Arc agent overview](/en-us/azure/azure-arc/servers/agent-overview).
- **[Azure Monitor agent (AMA)](/en-us/azure/azure-monitor/agents/agents-overview)**: Collects security-related configuration information and event logs from machines.
- **Automatic SQL Server discovery and registration**: Supports automatic discovery and registration of SQL Servers.