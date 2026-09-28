---
layout: Conceptual
title: Determine Data Residency Requirements and Agent Considerations for Multicloud Security - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/plan-multicloud-security-determine-data-residency-requirements
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
description: Learn about determining data residency requirements when planning multicloud deployment with Microsoft Defender for Cloud.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: ff58667b-746c-d0c9-0180-5e9e7c0d1ee1
document_version_independent_id: 3a37d0b1-28e2-3340-68ca-bc81a1112a85
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/plan-multicloud-security-determine-data-residency-requirements.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/plan-multicloud-security-determine-data-residency-requirements
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/plan-multicloud-security-determine-data-residency-requirements.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/beac614b-f66d-40ed-a947-3996de709333
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/9da05372-4706-43ec-a899-f436adab380d
platformId: e0649438-b61f-77b9-0bcb-b867a349ec74
---

# Determine Data Residency Requirements and Agent Considerations for Multicloud Security - Microsoft Defender for Cloud | Microsoft Learn

This article helps you determine data residency requirements for a multicloud deployment that uses cloud security posture management (CSPM) and cloud workload protection platform (CWPP) solutions in Microsoft Defender for Cloud.

## Data residency planning goals

Identify data residency requirements for your multicloud deployment and understand how Defender for Cloud plans and agents affect where data is processed and stored.

## Get started with data residency planning

When you protect assets in clouds, identify which plans to enable and whether each plan requires agents.

As part of this analysis, identify regional and legal requirements for data handling.

## Agent considerations for data residency

Consider data residency and data handling implications for the agents and extensions used by Defender for Cloud.

- **CSPM**: Cloud security posture management (CSPM) functionality in Defender for Cloud is agentless. No agents are required for CSPM to work.
- **CWPP**: Cloud workload protection platform (CWPP) functionality in Defender for Cloud can require agents to collect data.

## Data residency considerations for Defender for Servers

The Defender for Servers plan uses agents as follows:

- Non-Azure public clouds connect to Azure by using the [Azure Arc](/en-us/azure/azure-arc/servers/overview) service.
- You install the [Azure Connected Machine agent](/en-us/azure/azure-arc/servers/agent-overview) on multicloud machines that onboard as Azure Arc machines. Enable Defender for Cloud in the subscription where the Azure Arc machines are located.
- Defender for Cloud uses the Connected Machine agent to install extensions, such as Microsoft Defender for Endpoint, that are needed for [Defender for Servers](defender-for-servers-introduction) functionality.

## Data residency considerations for Defender for Containers

[Defender for Containers](defender-for-containers-introduction) protects your multicloud container deployments running in:

- **Azure Kubernetes Service (AKS)**: Microsoft's managed service for developing, deploying, and managing containerized applications.
- **Amazon Elastic Kubernetes Service (EKS) in a connected AWS account**: Amazon's managed service for running Kubernetes on AWS without needing to install, operate, and maintain your own Kubernetes control plane or nodes.
- **Google Kubernetes Engine (GKE) in a connected GCP project**: Google's managed environment for deploying, managing, and scaling applications using Google Cloud Platform (GCP) infrastructure.
- **Other Kubernetes distributions**: By using [Azure Arc-enabled Kubernetes](/en-us/azure/azure-arc/kubernetes/overview) you can attach and configure Kubernetes clusters running anywhere, including other public clouds and on-premises.

Defender for Containers has both sensor-based and agentless components.

- **Agentless collection of Kubernetes audit log data**: [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) or GCP Cloud Logging collects audit log data and sends the data to Defender for Cloud for further analysis.
- **Agentless collection for Kubernetes inventory**: Collect data on your Kubernetes clusters and their resources, such as Namespaces, Deployments, Pods, and Ingresses.
- **Sensor-based Azure Arc-enabled Kubernetes**: Connects your EKS and GKE clusters to Azure using [Azure Arc agents](/en-us/azure/azure-arc/kubernetes/conceptual-agent-overview), so that they're treated as Azure Arc resources.
- **[Defender sensor](defender-for-cloud-glossary#defender-sensor)**: A DaemonSet that collects signals from hosts by using extended Berkeley Packet Filter (eBPF) technology and provides runtime protection. The extension is registered with a Log Analytics workspace and used as a data pipeline. Kubernetes audit log data isn't stored in the Log Analytics workspace.
- **Azure Policy for Kubernetes**: configuration information is collected by Azure Policy for Kubernetes.

    - Azure Policy for Kubernetes extends the open-source Gatekeeper v3 admission controller webhook for Open Policy Agent.
    - The extension registers as a web hook to Kubernetes admission control and makes it possible to apply at-scale enforcement, safeguarding your clusters in a centralized, consistent manner.

Important

Kubernetes audit log data collection uses the Amazon EKS or GCP logging service in the source cloud. Confirm regional storage and transfer behavior to meet your organization's privacy and internal residency requirements.

## Data residency considerations for Defender for Databases

For the [Defender for Databases plan](quickstart-enable-database-protections) in a multicloud scenario, use Azure Arc to manage multicloud Structured Query Language (SQL) Server databases. The SQL Server instance is installed on a virtual or physical machine connected to Azure Arc.

- Set **Automatic SQL server discovery and registration** to **On** to allow SQL database discovery on the machines.
- The [Azure Connected Machine agent](/en-us/azure/azure-arc/servers/agent-overview) is installed on machines connected to Azure Arc.
- Enable the Defender for Databases plan in the subscription where the Azure Arc machines are located.
- Provision the Log Analytics agent for Microsoft Defender SQL Servers on the Azure Arc machines. It collects security-related configuration settings and event logs from machines.

For AWS and GCP resources protected by Defender for Cloud, AWS and GCP directly determine the resource location.