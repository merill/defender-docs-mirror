---
layout: Conceptual
title: Defender for Containers deployment overview - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-containers-deployment-overview
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
description: Learn about Microsoft Defender for Containers capabilities, architecture, and deployment options for Kubernetes environments across Azure, AWS, and Google Cloud.
ms.topic: overview
ms.date: 2025-12-09T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 5ebcef68-33fe-7248-aa44-86dd8d9b7267
document_version_independent_id: d849dda3-f704-a837-cdd0-2a75b74d29f8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-containers-deployment-overview.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-containers-deployment-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-containers-deployment-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d44a5346-5de4-439c-b804-7b2a536cbb55
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/da41a22b-b7a0-42d3-9c35-50da1c2b7b87
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 8a15a45a-1df2-3781-2930-96df9bd38f2e
---

# Defender for Containers deployment overview - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Containers provides threat protection, vulnerability assessment, and security posture management for Kubernetes clusters across cloud environments through Microsoft Defender for Cloud.

Defender for Containers is enabled and deployed differently depending on the Kubernetes environment. Azure Kubernetes Service (AKS) uses Azure-native integrations, while Amazon Elastic Kubernetes Service (EKS) and Google Kubernetes Engine (GKE) rely on multicloud connectors, Azure Arc-enabled Kubernetes, and environment-specific components.

# [Azure Kubernetes Service (AKS)](#tab/aks)
Microsoft Defender for Containers extends security monitoring and protection to Azure Kubernetes Service (AKS) clusters through Microsoft Defender for Cloud. It helps security and DevOps teams gain visibility into container image vulnerabilities, runtime activity, and Kubernetes configuration risks in Azure environments.

## Integration with Azure

Defender for Containers integrates natively with Azure services to protect AKS clusters. When enabled on an Azure subscription, the solution:

- Discovers AKS clusters in the subscription
- Deploys Defender for Containers components by using Azure-managed integrations
- Assesses container images stored in Azure Container Registry (ACR) for vulnerabilities
- Collects runtime security signals from AKS clusters
- Generates security recommendations based on observed configuration and posture
- Surfaces alerts that integrate with Microsoft security tooling

The integration is designed to operate using Azure-native capabilities and doesn't require inbound connectivity to AKS clusters.

Note

AKS control plane audit logs are collected through Azure-managed control plane integration. Defender for Containers doesn’t rely on Kubernetes-native audit log pipelines or require you to enable audit logging in the cluster.

## Key capabilities

Defender for Containers provides the following capabilities for AKS environments:

- **Container image vulnerability assessment** for images stored in Azure Container Registry (ACR)
- **Threat detection and alerting** based on runtime signals collected from AKS nodes, workloads, and Kubernetes audit logs
- **Security posture insights** for Kubernetes clusters and workloads, aligned with Kubernetes and Azure security best practices

Note

Available signals and detections depend on cluster configuration and enabled components.

# [Amazon Elastic Kubernetes Service (EKS)](#tab/eks)
Microsoft Defender for Containers extends security monitoring and protection to Amazon Elastic Kubernetes Service (EKS) clusters to provide visibility into container image vulnerabilities, runtime activity, and cluster configuration risks through Microsoft Defender for Cloud.

## Integration with AWS

Defender for Containers integrates with AWS through a secure connector that connects your AWS account to Microsoft Defender for Cloud. Once connected, the solution:

- Discovers EKS clusters in your AWS account
- Deploys lightweight security sensors to collect runtime signals
- Integrates with Amazon ECR to assess container images for vulnerabilities
- Generates security recommendations based on observed configuration and posture
- Surfaces alerts for suspicious activity related to EKS workloads

The integration is designed to work alongside existing AWS security services, such as AWS GuardDuty and AWS Security Hub.

## Key capabilities

Defender for Containers provides the following capabilities for Amazon EKS environments:

- **Container image vulnerability assessment** for images stored in Amazon ECR
- **Threat detection, alerting, and response** based on runtime signals
- **Security posture insights** aligned with security best practices

Note

Available signals and detections depend on cluster configuration and enabled data sources.

# [Google Kubernetes Engine (GKE)](#tab/gke)
Microsoft Defender for Containers extends security monitoring and protection to Google Kubernetes Engine (GKE) clusters by integrating with Microsoft Defender for Cloud.

## Integration with GCP

Defender for Containers integrates with Google Cloud through a secure GCP connector that connects your GCP projects to Microsoft Defender for Cloud. Once connected, the solution:

- Discovers GKE clusters in connected GCP projects
- Connects selected clusters to Azure Arc
- Deploys a Defender sensor
- Integrates with Google Container Registry and Artifact Registry
- Generates security recommendations
- Surfaces alerts for suspicious activity

The integration is designed to work alongside native GCP security features and doesn't require inbound connectivity.

## Key capabilities

Defender for Containers provides the following capabilities for GKE environments:

- **Container image vulnerability assessment** for GCR and Artifact Registry
- **Threat detection and alerting** based on runtime signals
- **Security posture insights** aligned with Kubernetes and GKE best practices

Note

Available signals and detections depend on cluster configuration and enabled data sources.

# [Arc-enabled Kubernetes](#tab/arc)
Microsoft Defender for Containers provides security monitoring and protection for Kubernetes clusters that are connected to Azure through Azure Arc. This includes Kubernetes clusters running on-premises, at the edge, or in other non-Azure environments.

Defender for Containers on Arc-enabled Kubernetes is managed through Microsoft Defender for Cloud and relies on Azure Arc-enabled Kubernetes for cluster connectivity and component deployment.

## Integration with Azure Arc

Defender for Containers integrates with Arc-enabled Kubernetes clusters by using Azure Arc as the control plane. After a cluster is connected to Azure Arc and the Containers plan is enabled, Defender for Containers:

- Discovers Arc-enabled Kubernetes clusters in the subscription
- Deploys Defender components by using Azure Arc extensions
- Collects runtime security signals from Kubernetes nodes and workloads
- Evaluates cluster and workload configurations
- Generates security recommendations and alerts in Defender for Cloud

The integration doesn't require inbound connectivity to the Kubernetes cluster. Communication is initiated from the cluster to Azure through the Azure Arc agents.

Note

Arc-enabled Kubernetes is required to deploy Defender for Containers components to Kubernetes clusters that aren’t running in Azure.

## Key capabilities

Defender for Containers provides the following capabilities for Arc-enabled Kubernetes environments:

- **Threat detection and alerting** based on runtime signals collected from Kubernetes nodes, workloads, and audit logs
- **Security posture insights** for Kubernetes clusters and workloads
- **Policy-based configuration assessment** through Azure Policy for Kubernetes

Note

Available signals, detections, and posture assessments depend on enabled components and cluster configuration.

---

## View your current coverage

Defender for Cloud provides access to [workbooks](custom-dashboards-azure-workbooks) through [Azure workbooks](/en-us/azure/azure-monitor/visualize/workbooks-overview). Workbooks are customizable reports that help you understand your security posture.

The [coverage workbook](custom-dashboards-azure-workbooks#coverage-workbook) shows which Defender for Cloud plans and components are enabled across your subscriptions and connected environments.

## Pricing

Defender for Containers is billed as part of Microsoft Defender for Cloud. Pricing depends on the enabled components and the number of protected resources.

For pricing details, see [Microsoft Defender for Cloud pricing](https://azure.microsoft.com/pricing/details/defender-for-cloud/).