---
layout: Conceptual
title: What is Cloud Security Posture Management (CSPM) - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/concept-cloud-security-posture-management
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
description: Learn more about Cloud Security Posture Management (CSPM) in Microsoft Defender for Cloud and how it helps improve your security posture.
ms.topic: concept-article
ms.date: 2026-09-11T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
locale: en-us
document_id: d3d7a83d-d602-559d-2604-b5d5c6132920
document_version_independent_id: ab8b4442-4792-64e7-4b3d-bc0562fa84af
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/concept-cloud-security-posture-management.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/concept-cloud-security-posture-management
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/concept-cloud-security-posture-management.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 1a9b642f-f55a-9411-701c-676abb819816
---

# What is Cloud Security Posture Management (CSPM) - Microsoft Defender for Cloud | Microsoft Learn

Cloud Security Posture Management (CSPM) is a core feature of Microsoft Defender for Cloud. CSPM provides continuous visibility into the security state of your cloud assets and workloads, offering actionable guidance to improve your security posture in Azure, AWS, and GCP.

Defender for Cloud continually assesses your cloud infrastructure against security standards defined for your Azure subscriptions, Amazon Web Services (AWS) accounts, and Google Cloud Platform (GCP) projects. Defender for Cloud issues security recommendations to help you identify and reduce cloud misconfigurations and security risks.

For Azure Database for PostgreSQL flexible server, Defender CSPM continuously evaluates server-level and database-level configurations against PostgreSQL security best practices. The assessments identify network security, auditing, and operational resilience issues. If Defender CSPM is already enabled, the assessments provide risk-prioritized recommendations without requiring other configuration.

When Foundational CSPM is enabled, the [Microsoft Cloud Security Benchmark (MCSB)](concept-regulatory-compliance) standard provides recommendations to help secure your multicloud environment. The [secure score](secure-score-security-controls) based on some of the MCSB recommendations helps you monitor cloud compliance. A higher score indicates a lower identified risk level.

Important

Starting October 27, 2026, Foundational CSPM will move to an opt-in model and will no longer be enabled by default for new Azure subscriptions. The free plan will continue to be available at no cost and can be enabled at any time based on your organization's needs. Existing subscriptions that already have Foundational CSPM enabled will remain enabled unless you turn off the plan. For more information, see [Opt in to Foundational CSPM](foundational-cspm-opt-in).

## CSPM plans

Defender for Cloud offers two CSPM plans:

- **Foundational CSPM** (free): Available at no cost. Starting October 27, 2026, new Azure subscriptions must opt in. AWS and GCP onboarding isn't affected.
- **Defender CSPM** (paid): Provides extra capabilities beyond the Foundational CSPM plan, including advanced CSPM tools for cloud visibility and compliance monitoring. This plan offers advanced security posture features such as AI security posture, attack path analysis, and risk prioritization.

### Plan availability

Defender CSPM supports multiple deployment models and cloud environments:

- **Commercial clouds**: Available in all Azure commercial regions.
- **Government clouds**: Available in Azure Government and Azure Government Secret.
- **Multi-cloud**: Support for Azure, AWS, and GCP environments.
- **Hybrid**: On-premises resources connected through Azure Arc.
- **DevOps**: GitHub, Azure DevOps, and GitLab integration.
- **External registries**: Docker Hub and JFrog Artifactory connectors support selected Foundational CSPM and Defender CSPM capabilities. Defender for Containers also supports selected container image capabilities. For plan-specific availability, see [external registry capabilities](devops-support#external-registries) and [Defender for Containers feature access patterns](defender-for-containers-feature-access-patterns).

For specific regional availability and government cloud support details, see the [support matrix for cloud environments](support-matrix-defender-for-cloud).

## Plan pricing

Defender CSPM billing is based on specific resources enabled in your subscriptions or connectors.

- See [Defender for Cloud pricing](https://azure.microsoft.com/pricing/details/defender-for-cloud/) and use the [cost calculator](cost-calculator) to estimate costs.
- Advanced DevOps security posture features (pull request annotations, code-to-cloud mapping, attack path analysis, and security explorer) require the paid Defender CSPM plan. The free plan provides basic Azure DevOps recommendations. For details, see [DevOps security features](devops-support#azure-devops).
- The Azure and AWS billable-resource tables in this article list covered resource types, activation requirements, and billing-effective dates for Serverless protection and Serverless containers.

## Azure Cloud Security Posture Management

Defender CSPM provides Cloud Security Posture Management for Azure infrastructure, compute, data, and application workloads. Learn how to [enable Defender CSPM on your Azure subscription](tutorial-enable-cspm-plan).

### Azure billable resources

Defender CSPM protects all Azure workloads, but billing applies only to specific resources listed in the following table:

| Service | Resource Types | Exclusions |
| --- | --- | --- |
| Compute | Virtual machines, Virtual Machine scale sets, classic VMs | Deallocated VMs, Databricks VMs |
| Storage | Storage accounts | Accounts without blob containers or file shares |
| Databases | SQL servers, Azure Database for PostgreSQL flexible servers, Azure Database for MySQL flexible servers, Synapse workspaces | - |
| Serverless protection ^1^ | Function Apps, Web Apps | - |
| Serverless containers ^2^ | Azure Container Apps (ACA), Azure Container Instances (ACI) | - |

^1^ To protect Function Apps and Web Apps and begin billing for this capability, [enable Serverless protection](serverless-protection#enable-serverless-protection-for-your-environment) in Defender CSPM. Billing became effective April 1, 2026.

^2^ To protect Azure Container Apps and Azure Container Instances and begin billing for this capability, [enable the Serverless Containers component](posture-for-serverless-containers#requirements-and-availability) in Defender CSPM. Enable **Registry access** for full Serverless Containers coverage. Billing became effective July 1, 2026.

### Azure features and capabilities

The following table summarizes Azure features available in Foundational CSPM and Defender CSPM:

| Feature | Foundational CSPM | Defender CSPM |
| --- | --- | --- |
| [Asset inventory](asset-inventory) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| [Data exporting](export-to-siem) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| Data visualization and reporting with Azure Workbooks | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| [Microsoft Cloud Security Benchmark](concept-regulatory-compliance) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| [Secure score](secure-score-security-controls) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| [Security recommendations](review-security-recommendations) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| Tools for remediation | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| [Workflow automation](workflow-automations) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| [Agentless code-to-cloud containers vulnerability assessment](agentless-vulnerability-assessment-azure) | - | ![](media/icons/yes-icon.png) |
| [Agentless discovery for Kubernetes](concept-agentless-containers) | - | ![](media/icons/yes-icon.png) |
| [Agentless VM secrets scanning](secrets-scanning-servers) | - | ![](media/icons/yes-icon.png) |
| [Agentless VM vulnerability scanning](enable-agentless-scanning-vms) | - | ![](media/icons/yes-icon.png) |
| [AI security posture management](ai-security-posture) | - | ![](media/icons/yes-icon.png) |
| [API security posture management](enable-api-security-posture) | - | ![](media/icons/yes-icon.png) |
| [Attack path analysis](how-to-manage-attack-path) | - | ![](media/icons/yes-icon.png) |
| [Azure Kubernetes Service security dashboard (Preview)](cluster-security-dashboard) | - | ![](media/icons/yes-icon.png) |
| [Critical assets protection](critical-assets-protection) | - | ![](media/icons/yes-icon.png) |
| [Custom Recommendations](create-custom-recommendations) | - | ![](media/icons/yes-icon.png) |
| [Data security posture management (DSPM), Sensitive data scanning](concept-data-security-posture) | - | ![](media/icons/yes-icon.png) |
| [Discovery and posture for serverless container workloads](posture-for-serverless-containers) | - | ![](media/icons/yes-icon.png) |
| [Governance to drive remediation at-scale](governance-rules) | - | ![](media/icons/yes-icon.png) |
| [Internet exposure analysis](internet-exposure-analysis) | - | ![](media/icons/yes-icon.png) |
| [External attack surface management](concept-easm) | - | ![](media/icons/yes-icon.png) |
| [Regulatory compliance assessments](concept-regulatory-compliance-standards) | - | ![](media/icons/yes-icon.png) |
| [Risk hunting with security explorer](how-to-manage-cloud-security-explorer) | - | ![](media/icons/yes-icon.png) |
| [Risk prioritization](risk-prioritization) | - | ![](media/icons/yes-icon.png) |
| [Serverless protection](serverless-protection) | - | ![](media/icons/yes-icon.png) |

## AWS Cloud Security Posture Management

Defender CSPM connects to Amazon Web Services (AWS) accounts to provide Cloud Security Posture Management, security assessments, vulnerability scanning, and risk context for AWS resources. Learn how to [connect your AWS accounts to Defender for Cloud](quickstart-onboard-aws) and review [AWS prerequisites](quickstart-onboard-aws#prerequisites).

### AWS billable resources

The following table lists billable resources and exclusions when you enable Defender CSPM on AWS connectors:

| Service | Resource Types | Exclusions |
| --- | --- | --- |
| Compute | EC2 instances | Deallocated VMs |
| Storage | S3 buckets | – |
| Databases | RDS instances | – |
| Serverless protection ^3^ | AWS Lambda functions | – |
| Serverless containers ^4^ | Amazon ECS on AWS Fargate | – |

^3^ To protect AWS Lambda functions and begin billing for this capability, [enable Serverless protection](serverless-protection#enable-serverless-protection-for-your-environment) in Defender CSPM. Billing became effective April 1, 2026. A billable resource represents eight AWS Lambda functions.

^4^ To protect Amazon ECS on AWS Fargate workloads and begin billing for this capability, [enable the Serverless Containers component](posture-for-serverless-containers#requirements-and-availability) in Defender CSPM. Enable **Registry access** for full Serverless Containers coverage. Billing became effective July 1, 2026. A billable resource represents two Amazon ECS on AWS Fargate workloads.

### AWS features and capabilities

The following table summarizes AWS capabilities available in Foundational CSPM and Defender CSPM:

| Feature | Foundational CSPM | Defender CSPM |
| --- | --- | --- |
| [Asset inventory](asset-inventory) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| [Data exporting](export-to-siem) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| Data visualization and reporting with Azure Workbooks | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| [Microsoft Cloud Security Benchmark](concept-regulatory-compliance) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| [Secure score](secure-score-security-controls) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| [Security recommendations](review-security-recommendations) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| Tools for remediation | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| [Workflow automation](workflow-automations) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| [Agentless code-to-cloud containers vulnerability assessment](agentless-vulnerability-assessment-azure) | - | ![](media/icons/yes-icon.png) |
| [Agentless discovery for Kubernetes](concept-agentless-containers) | - | ![](media/icons/yes-icon.png) |
| [Agentless VM secrets scanning](secrets-scanning-servers) | - | ![](media/icons/yes-icon.png) |
| [Agentless VM vulnerability scanning](enable-agentless-scanning-vms) | - | ![](media/icons/yes-icon.png) |
| [AI security posture management](ai-security-posture) | - | ![](media/icons/yes-icon.png) |
| [Attack path analysis](how-to-manage-attack-path) | - | ![](media/icons/yes-icon.png) |
| [AWS CloudTrail ingestion (Preview)](integrate-cloud-trail) | - | ![](media/icons/yes-icon.png) |
| [Critical assets protection](critical-assets-protection) | - | ![](media/icons/yes-icon.png) |
| [Custom Recommendations](create-custom-recommendations) | - | ![](media/icons/yes-icon.png) |
| [Data security posture management (DSPM), Sensitive data scanning](concept-data-security-posture) | - | ![](media/icons/yes-icon.png) |
| [Discovery and posture for serverless container workloads](posture-for-serverless-containers) | - | ![](media/icons/yes-icon.png) |
| [Governance to drive remediation at-scale](governance-rules) | - | ![](media/icons/yes-icon.png) |
| [Internet exposure analysis](internet-exposure-analysis) | - | ![](media/icons/yes-icon.png) |
| [External attack surface management](concept-easm) | - | ![](media/icons/yes-icon.png) |
| [Regulatory compliance assessments](concept-regulatory-compliance-standards) | - | ![](media/icons/yes-icon.png) |
| [Risk hunting with security explorer](how-to-manage-cloud-security-explorer) | - | ![](media/icons/yes-icon.png) |
| [Risk prioritization](risk-prioritization) | - | ![](media/icons/yes-icon.png) |
| [Serverless protection](serverless-protection) | - | ![](media/icons/yes-icon.png) |

## GCP Cloud Security Posture Management

Defender CSPM connects to Google Cloud Platform (GCP) projects to provide Cloud Security Posture Management and vulnerability assessment for GCP environments. Learn how to [connect your GCP projects to Defender for Cloud](quickstart-onboard-gcp) and review [GCP prerequisites](quickstart-onboard-gcp#prerequisites).

### GCP billable resources

The following table lists billable resources and exclusions when you enable Defender CSPM on GCP projects:

| Service | Resource Types | Exclusions |
| --- | --- | --- |
| Compute | Compute instances, Instance Groups | Nonrunning instances |
| Storage | Storage buckets | Nearline/coldline/archive classes, unsupported regions |
| Databases | Cloud SQL instances | – |

### GCP features and capabilities

The following table summarizes GCP capabilities available in Foundational CSPM and Defender CSPM:

| Feature | Foundational CSPM | Defender CSPM |
| --- | --- | --- |
| [Asset inventory](asset-inventory) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| [Data exporting](export-to-siem) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| Data visualization and reporting with Azure Workbooks | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| [Microsoft Cloud Security Benchmark](concept-regulatory-compliance) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| [Secure score](secure-score-security-controls) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| [Security recommendations](review-security-recommendations) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| Tools for remediation | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| [Workflow automation](workflow-automations) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| [Agentless code-to-cloud containers vulnerability assessment](agentless-vulnerability-assessment-azure) | - | ![](media/icons/yes-icon.png) |
| [Agentless discovery for Kubernetes](concept-agentless-containers) | - | ![](media/icons/yes-icon.png) |
| [Agentless VM secrets scanning](secrets-scanning-servers) | - | ![](media/icons/yes-icon.png) |
| [Agentless VM vulnerability scanning](enable-agentless-scanning-vms) | - | ![](media/icons/yes-icon.png) |
| [AI security posture management](ai-security-posture) | - | ![](media/icons/yes-icon.png) |
| [Attack path analysis](how-to-manage-attack-path) | - | ![](media/icons/yes-icon.png) |
| [Critical assets protection](critical-assets-protection) | - | ![](media/icons/yes-icon.png) |
| [Custom Recommendations](create-custom-recommendations) | - | ![](media/icons/yes-icon.png) |
| [Data security posture management (DSPM), Sensitive data scanning](concept-data-security-posture) | - | ![](media/icons/yes-icon.png)^5^ |
| [External attack surface management](concept-easm) | - | ![](media/icons/yes-icon.png) |
| [Governance to drive remediation at-scale](governance-rules) | - | ![](media/icons/yes-icon.png) |
| [Internet exposure analysis](internet-exposure-analysis) | - | ![](media/icons/yes-icon.png) |
| [Regulatory compliance assessments](concept-regulatory-compliance-standards) | - | ![](media/icons/yes-icon.png) |
| [Risk hunting with security explorer](how-to-manage-cloud-security-explorer) | - | ![](media/icons/yes-icon.png) |
| [Risk prioritization](risk-prioritization) | - | ![](media/icons/yes-icon.png) |

^5^ GCP sensitive data discovery [only supports Cloud Storage](concept-data-security-posture-prepare#whats-supported).

## Azure Arc Cloud Security Posture Management

Defender for Cloud extends Cloud Security Posture Management to on-premises and hybrid resources connected through Azure Arc. Learn how to [connect on-premises machines to Azure Arc](quickstart-onboard-machines) and review [hybrid onboarding prerequisites](quickstart-onboard-machines#prerequisites). Use Foundational CSPM to view Arc-enabled resources in [asset inventory](asset-inventory), assess their security configuration, and review [security recommendations](review-security-recommendations) and [secure score](secure-score-security-controls).

The following Foundational CSPM capabilities support Arc-enabled resources:

| Feature | Foundational CSPM | Defender CSPM |
| --- | --- | --- |
| [Asset inventory](asset-inventory) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| [Data exporting](export-to-siem) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| Data visualization and reporting with Azure Workbooks | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| [Secure score](secure-score-security-controls) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| [Security recommendations](review-security-recommendations) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| Tools for remediation | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| [Workflow automation](workflow-automations) | ![](media/icons/yes-icon.png) | ![](media/icons/yes-icon.png) |
| [Container registry vulnerability assessment for Arc-connected clusters](support-matrix-defender-for-containers) | - | ![](media/icons/yes-icon.png) |

Container registry vulnerability assessment requires **Registry access** and is also available through Defender for Containers.

Defender CSPM adds advanced posture management capabilities for supported Arc-enabled resources. Availability depends on the resource type and connected environment. For supported Arc scenarios and cloud availability, see the [support matrix for cloud environments](support-matrix-defender-for-cloud).

## DevOps Cloud Security Posture Management

DevOps Cloud Security Posture Management capabilities provide code-to-cloud contextualization, pull request annotations, security explorer risk hunting, and attack path analysis for DevOps environments.

For feature availability, prerequisites, the complete feature matrix, and permission requirements, see [Support and prerequisites for DevOps security](devops-support). You can also go directly to [Azure DevOps](devops-support#azure-devops) or [external registry](devops-support#external-registries) requirements.

## Integrations and external posture

Defender for Cloud integrates with partner systems and external security platforms for unified security posture and incident response.

- **[External attack surface management (EASM)](concept-easm)**: Discovers internet-facing assets and security risks in cloud and on-premises environments.
- **[ServiceNow Integration](integration-servicenow)**: Integrates Defender for Cloud recommendations with ServiceNow for automated ticketing and incident management (preview).

## Azure cloud support

For commercial and national cloud coverage, see [Azure cloud environment support matrix](support-matrix-defender-for-cloud).