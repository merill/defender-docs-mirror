---
layout: Conceptual
title: Microsoft Defender for Cloud multicloud support matrix - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/multicloud-support-matrix
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
description: Review Azure, AWS, and GCP support for Microsoft Defender for Cloud workload protection and security posture features to plan a multicloud deployment.
ms.topic: limits-and-quotas
ms.date: 2026-09-11T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
locale: en-us
document_id: c9b5c0ed-9259-8884-0aea-adfd15c98ace
document_version_independent_id: 6cfab17a-addf-7fef-c4b0-9db303973d7a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/multicloud-support-matrix.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/multicloud-support-matrix
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/multicloud-support-matrix.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/cbe4ca68-43ac-4375-aba5-5945a6394c20
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ced846cc-6a3c-4c8f-9dfb-3de0e90e2742
platformId: b8cad84d-03a5-df8b-0717-67570972ee99
---

# Microsoft Defender for Cloud multicloud support matrix - Microsoft Defender for Cloud | Microsoft Learn

Important

All Microsoft Defender for Cloud features will be officially retired in the Azure in China region on October 1, 2026. Due to this upcoming retirement, Azure in China customers are no longer able to onboard new subscriptions to the service. A new subscription is any subscription that was not already onboarded to the Microsoft Defender for Cloud service prior to August 18, 2025, the date of the retirement announcement. For more information on the retirement, see [Microsoft Defender for Cloud Deprecation in Microsoft Azure Operated by 21Vianet Announcement](https://aka.ms/mdcretirementinchina).

Customers should work with their account representatives for Microsoft Azure operated by 21Vianet to assess the impact of this retirement on their own operations.

Compare Microsoft Defender for Cloud plan and feature support for Azure, Amazon Web Services (AWS), and Google Cloud Platform (GCP). Use the matrices to review workload protection coverage without checking each plan separately.

Note

Some features are in preview. The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include other legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

## Plan coverage at a glance for AWS and GCP

Use the following table to verify Defender for Cloud plan coverage in multicloud environments and review the primary capabilities of each plan. General availability (GA) indicates that a plan is released for production use. The table uses the abbreviations cloud security posture management (CSPM), endpoint detection and response (EDR), and continuous integration and continuous delivery (CI/CD).

| Defender for Cloud plan | AWS | GCP | Key plan features | Details |
| --- | --- | --- | --- | --- |
| Defender for Servers (Plan 1 and Plan 2) | GA | GA | EDR integration, vulnerability scanning, malware scanning, and secrets scanning | [Defender for Servers support matrix](support-matrix-defender-for-servers) |
| Defender for Containers | GA | GA | Kubernetes threat detection, container vulnerability assessment, control plane hardening | [Containers support matrix](support-matrix-defender-for-containers) |
| Defender CSPM | GA | GA | Agentless posture assessment, attack path analysis, governance and risk prioritization | [Defender CSPM overview](concept-cloud-security-posture-management) |
| Defender for SQL Servers on Machines | GA | GA | SQL threat detection and vulnerability assessment on multicloud machines | [Defender for SQL Servers on Machines overview](defender-for-sql-servers-introduction) |
| Defender for Open-Source Relational Databases | Preview | Not supported | Threat detection for PostgreSQL, MySQL, and MariaDB in supported environments | [Overview of Defender for Open-Source Relational Databases](defender-for-databases-introduction) |
| Defender for Azure SQL Databases | Not supported | Not supported | Threat detection and vulnerability assessment for Azure SQL services | [Defender for SQL overview](defender-for-sql-introduction) |
| Defender for Azure Cosmos DB | Not supported | Not supported | Threat protection for Azure Cosmos DB workloads | [Defender for Azure Cosmos DB](concept-defender-for-cosmos) |
| Defender for DevOps | GA | GA | CI/CD security posture, code-to-cloud insights, pull request annotations | [Defender for DevOps overview](defender-for-devops-introduction) |
| Defender for Storage | Not supported | Not supported | Malware scanning and threat detection for Azure Storage | [Defender for Storage overview](defender-for-storage-introduction) |
| Defender for Key Vault | Not supported | Not supported | Threat detection for suspicious key and secret access patterns | [Defender for Key Vault overview](defender-for-key-vault-introduction) |
| Defender for Resource Manager | Not supported | Not supported | Detection of suspicious Azure Resource Manager operations | [Defender for Resource Manager overview](defender-for-resource-manager-introduction) |
| Defender for DNS | Not supported | Not supported | DNS-layer threat detection for Azure resources | [Defender for DNS overview](defender-for-dns-introduction) |
| Defender for App Service | Not supported | Not supported | Threat detection for web apps and APIs running in App Service | [Defender for App Service overview](defender-for-app-service-introduction) |
| Defender for APIs | Not supported | Not supported | API security posture and threat detection in Azure API Management | [Defender for APIs overview](defender-for-apis-introduction) |
| Defender for AI Services | Not supported | Not supported | Threat protection for generative AI services and applications | [AI threat protection](ai-threat-protection) |

Note

**Defender for DevOps** protects CI/CD platforms (Azure DevOps, GitHub, GitLab) rather than specific cloud environments. Support is not cloud-specific.

## Plan availability by cloud

The following table provides a high-level view of Defender for Cloud plan availability for Azure, AWS, and GCP.

| Plan | Azure | AWS | GCP |
| --- | --- | --- | --- |
| [Defender for Servers (Plan 1 and Plan 2)](plan-defender-for-servers) | GA | GA | GA |
| [Defender for Containers](defender-for-containers-introduction) | GA | GA | GA |
| [Defender CSPM](concept-cloud-security-posture-management) | GA | GA | GA |
| [Defender for SQL Servers on Machines](defender-for-sql-introduction) | GA | GA | GA |
| [Defender for Open-Source Relational Databases](defender-for-databases-introduction) | GA | Preview | Not supported |
| [Defender for Azure SQL Databases](defender-for-sql-introduction) | GA | Not supported | Not supported |
| [Defender for Azure Cosmos DB](concept-defender-for-cosmos) | GA | Not supported | Not supported |
| [Defender for DevOps](defender-for-devops-introduction) | GA | GA | GA |
| [Defender for Storage](defender-for-storage-introduction) | GA | Not supported | Not supported |
| [Defender for Key Vault](defender-for-key-vault-introduction) | GA | Not supported | Not supported |
| [Defender for Resource Manager](defender-for-resource-manager-introduction) | GA | Not supported | Not supported |
| [Defender for DNS](defender-for-dns-introduction) | GA | Not supported | Not supported |
| [Defender for App Service](defender-for-app-service-introduction) | GA | Not supported | Not supported |
| [Defender for APIs](defender-for-apis-introduction) | GA | Not supported | Not supported |
| [Defender for AI Services](ai-threat-protection) | GA | Not supported | Not supported |

## Defender for Servers

Defender for Servers provides threat detection and advanced defenses for your machines in Azure, AWS, and GCP. For more information, see [Defender for Servers](plan-defender-for-servers).

Note

AWS and GCP machines require [Azure Arc](/en-us/azure/azure-arc/servers/overview) for onboarding. Some features, such as file integrity monitoring, depend on the Azure Monitor Agent (AMA) deployed through Arc.

### Shared features (Plan 1 and Plan 2)

| Feature | Azure | AWS | GCP |
| --- | --- | --- | --- |
| [Defender for Endpoint automatic onboarding](integration-defender-for-endpoint) | Supported | Supported | Supported |
| [Defender for Endpoint EDR](integration-defender-for-endpoint) | Supported | Supported | Supported |
| [Integrated alerts and incidents](concept-integration-365) | Supported | Supported | Supported |
| [Regulatory compliance assessment](concept-regulatory-compliance-standards) | Supported | Supported | Supported |
| [Software inventory discovery](asset-inventory) | Supported | Supported | Supported |
| [Vulnerability scanning (agent-based)](auto-deploy-vulnerability-assessment) | Supported | Supported | Supported |

### Plan 2 features

| Feature | Azure | AWS | GCP |
| --- | --- | --- | --- |
| [Vulnerability scanning (agentless)](concept-agentless-data-collection) | Supported | Supported | Supported |
| [Agentless malware scanning](agentless-malware-scanning) | Supported | Supported | Supported |
| [Agentless machine secrets scanning](concept-agentless-data-collection) | Supported | Supported | Supported |
| [Defender for DNS alerts](defender-for-dns-introduction) | Supported | Supported | Supported |
| [Defender for Vulnerability Management premium](/en-us/defender-vulnerability-management/defender-vulnerability-management-capabilities) | Supported | Supported | Supported |
| [File integrity monitoring](file-integrity-monitoring-overview) | Supported | Supported with Azure Arc | Supported with Azure Arc |
| [Free data ingestion (500 MB)](data-ingestion-benefit) | Supported | Supported | Supported |
| [Just-in-time virtual machine access](just-in-time-access-overview) | Supported | Supported | Not supported |
| [Network map](protect-network-resources) | Supported | Not supported | Not supported |
| [OS system updates](enable-periodic-system-updates) | Supported | Supported with Azure Arc | Supported with Azure Arc |
| [Threat detection (Azure network layer)](alerts-azure-network-layer) | Supported | Not supported | Not supported |

For detailed operating system, machine type, and feature-level support, see [Defender for Servers support matrix](support-matrix-defender-for-servers).

## Defender for Containers

Defender for Containers protects Kubernetes clusters and container workloads. It supports Azure Kubernetes Service (AKS), Amazon Elastic Kubernetes Service (EKS), and Google Kubernetes Engine (GKE). Learn more about [Defender for Containers](defender-for-containers-introduction).

| Feature | Azure (AKS) | AWS (EKS) | GCP (GKE) |
| --- | --- | --- | --- |
| Container registry vulnerability assessment | GA | GA | GA |
| Runtime container vulnerability assessment (registry scan-based) | GA | GA | GA |
| Control plane threat detection | GA | GA | GA |
| Workload threat detection | GA | GA | GA |
| Binary drift detection | GA | GA | GA |
| Binary drift blocking | Preview | Preview | Preview |
| Anti-malware | GA | GA | GA |
| Agentless discovery for Kubernetes | GA | GA | GA |
| Attack path analysis | GA | GA | GA |
| Control plane hardening | GA | GA | GA |
| Workload hardening | GA | GA | GA |

Note

Workload hardening on AWS and GCP requires the Azure Policy extension for Azure Arc-enabled Kubernetes.

Note

Container registry vulnerability assessment supports Azure Container Registry (ACR), Amazon Elastic Container Registry (ECR), Google Artifact Registry (GAR), Google Container Registry (GCR), Docker Hub, and JFrog Artifactory in all clouds.

For detailed support information, see [Containers support matrix](support-matrix-defender-for-containers).

## Defender CSPM

Defender CSPM provides cloud security posture management capabilities. Foundational CSPM is available for free in all supported clouds. The paid Defender CSPM plan provides advanced features. For more information, see [Defender CSPM](concept-cloud-security-posture-management).

### Foundational CSPM (free) features

| Feature | Azure | AWS | GCP | More availability |
| --- | --- | --- | --- | --- |
| [Asset inventory](asset-inventory) | Supported | Supported | Supported | On-premises, Docker Hub, JFrog Artifactory |
| [Data exporting](export-to-siem) | Supported | Supported | Supported | On-premises |
| Data visualization and reporting with Azure Workbooks | Supported | Supported | Supported | On-premises |
| [Microsoft Cloud Security Benchmark](concept-regulatory-compliance) | Supported | Supported | Supported | Not applicable |
| [Secure score](secure-score-security-controls) | Supported | Supported | Supported | On-premises, Docker Hub, JFrog Artifactory |
| [Security recommendations](review-security-recommendations) | Supported | Supported | Supported | On-premises, Docker Hub, JFrog Artifactory |
| Tools for remediation | Supported | Supported | Supported | On-premises, Docker Hub, JFrog Artifactory |
| [Workflow automation](workflow-automations) | Supported | Supported | Supported | On-premises |

### Paid plan features

| Feature | Azure | AWS | GCP | More availability |
| --- | --- | --- | --- | --- |
| [Agentless code-to-cloud containers vulnerability assessment](agentless-vulnerability-assessment-azure) | Supported | Supported | Supported | Not applicable |
| [Agentless discovery for Kubernetes](concept-agentless-containers) | Supported | Supported | Supported | Not applicable |
| [Agentless VM secrets scanning](secrets-scanning-servers) | Supported | Supported | Supported | Not applicable |
| [Agentless VM vulnerability scanning](enable-agentless-scanning-vms) | Supported | Supported | Supported | Not applicable |
| [AI security posture management](ai-security-posture) | Supported | Supported | Not supported | Not applicable |
| [API security posture management](api-security-posture-overview) | Supported | Not supported | Not supported | Not applicable |
| [Attack path analysis](how-to-manage-attack-path) | Supported | Supported | Supported | Docker Hub, JFrog Artifactory |
| [Azure Kubernetes Service security dashboard (Preview)](cluster-security-dashboard) | Supported | Not supported | Not supported | Not applicable |
| [Code-to-cloud mapping for containers](container-image-mapping) | Not supported | Not supported | Not supported | GitHub, Azure DevOps, Docker Hub, JFrog Artifactory |
| [Code-to-cloud mapping for infrastructure as code (IaC)](iac-template-mapping) | Not supported | Not supported | Not supported | Azure DevOps, Docker Hub, JFrog Artifactory |
| [Critical assets protection](critical-assets-protection) | Supported | Supported | Supported | Not applicable |
| [Custom recommendations](create-custom-recommendations) | Supported | Supported | Supported | Not applicable |
| [Data security posture management (DSPM)](concept-data-security-posture) | Supported | Supported | Supported | Not applicable |
| [External attack surface management](concept-easm) | Supported | Supported | Supported | Not applicable |
| [Governance to drive remediation at scale](governance-rules) | Supported | Supported | Supported | Not applicable |
| [Internet exposure analysis](internet-exposure-analysis) | Supported | Supported | Supported | Not applicable |
| [Pull request annotations](review-pull-request-annotations) | Not supported | Not supported | Not supported | GitHub, Azure DevOps |
| [Regulatory compliance assessments](concept-regulatory-compliance-standards) | Supported | Supported | Supported | Not applicable |
| [Risk hunting with security explorer](how-to-manage-cloud-security-explorer) | Supported | Supported | Supported | Docker Hub, JFrog Artifactory |
| [Risk prioritization](risk-prioritization) | Supported | Supported | Supported | Docker Hub, JFrog Artifactory |
| [Serverless protection](serverless-protection) | Supported | Supported | Not supported | Not applicable |
| [ServiceNow integration](integration-servicenow) | Supported | Supported | Supported | Not applicable |

For the AWS and GCP resource types that Defender CSPM can discover, see [AWS and GCP resources supported by Defender CSPM](defender-cloud-security-posture-management-supported-resources). For plan details, see the [Defender CSPM overview](concept-cloud-security-posture-management).

## Defender for Databases

Defender for Databases provides threat detection for database services. Multicloud coverage varies by database type. For more information, see [Defender for Databases](defender-for-databases-introduction).

| Sub-plan | Azure | AWS | GCP |
| --- | --- | --- | --- |
| Defender for Azure SQL Databases | GA | Not supported | Not supported |
| Defender for SQL Servers on Machines | GA | GA | GA |
| Defender for Open-Source Relational Databases | GA | Preview | Not supported |
| Defender for Azure Cosmos DB | GA | Not supported | Not supported |

Note

Defender for SQL Servers on Machines protects SQL Server instances running on Azure VMs, AWS EC2 instances (via Arc), and GCP Compute Engine instances (via Arc).

For detailed support information, see [Defender for SQL overview](defender-for-sql-introduction).

## Defender for DevOps

Defender for DevOps connects to your continuous integration and continuous delivery (CI/CD) platforms and provides security insights for your development pipelines. For more information, see [Defender for DevOps](defender-for-devops-introduction).

- **Azure DevOps**: GA.
- **GitHub**: GA.
- **GitLab**: GA.

## Defender for APIs

Defender for APIs protects APIs published in Azure API Management. It provides threat detection and security posture insights. For more information, see [Defender for APIs](defender-for-apis-introduction).

Note

Defender for APIs is available on Azure only. AWS and GCP environments are not supported.

| Feature | Azure | AWS | GCP |
| --- | --- | --- | --- |
| [API data classification](defender-for-apis-introduction) | Supported | Not supported | Not supported |
| [Azure API Management integration](defender-for-apis-introduction) | Supported | Not supported | Not supported |
| [Defender CSPM integration](defender-for-apis-introduction)^2^ | Supported | Not supported | Not supported |
| [Inventory](defender-for-apis-introduction) | Supported | Not supported | Not supported |
| [Security findings](defender-for-apis-introduction) | Supported | Not supported | Not supported |
| [Security posture](defender-for-apis-introduction) | Supported | Not supported | Not supported |
| [Security information and event management (SIEM) integrations](defender-for-apis-introduction) | Supported | Not supported | Not supported |
| [Threat detection (machine learning-based)](defender-for-apis-introduction) | Supported | Not supported | Not supported |

^2^ Requires the Defender CSPM plan and gives access to the cloud security graph.

For detailed support information, see [Defender for APIs overview](defender-for-apis-introduction).

## Azure-only plans

The following Defender for Cloud plans are available on Azure only and don't currently support AWS or GCP workloads.

| Plan | Azure | AWS | GCP |
| --- | --- | --- | --- |
| [Defender for Storage](defender-for-storage-introduction) | GA | Not supported | Not supported |
| [Defender for Key Vault](defender-for-key-vault-introduction) | GA | Not supported | Not supported |
| [Defender for Resource Manager](defender-for-resource-manager-introduction) | GA | Not supported | Not supported |
| [Defender for DNS](defender-for-dns-introduction) | GA | Not supported | Not supported |
| [Defender for App Service](defender-for-app-service-introduction) | GA | Not supported | Not supported |
| [Defender for APIs](defender-for-apis-introduction) | GA | Not supported | Not supported |
| [Defender for AI Services](ai-threat-protection) | GA | Not supported | Not supported |