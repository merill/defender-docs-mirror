---
layout: Conceptual
title: Access patterns and private cluster support for Defender for Containers features - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-containers-feature-access-patterns
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
description: Reference which Microsoft Defender for Containers features require registry access, Kubernetes API access, cloud-provider access, or sensor outbound connectivity, and whether they support private clusters.
ms.topic: reference
ms.date: 2026-05-31T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 656d7bc1-0c90-af1f-6e10-8dbeff17c824
document_version_independent_id: 25d68460-3eb6-6bdb-ff61-9f97f4b76153
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-containers-feature-access-patterns.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-containers-feature-access-patterns
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-containers-feature-access-patterns.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/d44a5346-5de4-439c-b804-7b2a536cbb55
- https://authoring-docs-microsoft.poolparty.biz/devrel/cb49e66a-8528-497d-adaa-eade2d009d1b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/da41a22b-b7a0-42d3-9c35-50da1c2b7b87
- https://authoring-docs-microsoft.poolparty.biz/devrel/472c9d15-157b-443c-afa2-e209c8fecf58
platformId: 85a80079-ca7b-c591-9795-234056d8247e
---

# Access patterns and private cluster support for Defender for Containers features - Microsoft Defender for Cloud | Microsoft Learn

This page summarizes the access patterns used by Microsoft Defender for Containers features, the required enablement method, the applicable plan, and private cluster support.

View the [network access and permissions reference](defender-for-containers-network-access) for detailed network and permission requirements for each access pattern.

Note

The **Private cluster support** column includes support requirements and related prerequisites for some features.

- **Supported by enabling a restricted public API endpoint** means the feature supports private clusters when the Kubernetes API is exposed through a restricted public endpoint.
- **Requires outbound HTTPS access** means the cluster must allow outbound HTTPS connectivity to Microsoft Defender for Cloud.
- Some entries describe feature prerequisites instead of private cluster support behavior.

For preview deployment instructions for private clusters, see [Deploy Defender for Containers to private clusters (Preview)](defender-for-containers-private-clusters).

## Connectivity patterns used by Defender for Containers

Microsoft Defender for Containers uses multiple connectivity patterns to collect security signals and provide protection across your environment, including:

- **Registry access**: Connections from Microsoft Defender for Cloud to container registries to scan images for vulnerabilities and, in some cases, publish assessment results back to the registry.
- **Kubernetes API access**: Connections from Microsoft Defender for Cloud to Kubernetes API endpoints for cluster discovery, posture assessment, and risk analysis.
- **Sensor outbound connectivity**: Runtime telemetry sent from Kubernetes worker nodes to Microsoft Defender for Cloud for threat detection.
- **Cloud-native audit log ingestion**: Ingestion of Kubernetes audit logs from cloud-native logging services for control plane threat detection.
- **Cloud-provider access**: Connections from Microsoft Defender for Cloud to cloud-provider APIs for resource discovery, posture assessment, inventory, and risk analysis.

## Vulnerability assessment features

The following table summarizes vulnerability assessment features and their access patterns.

| Feature | Supported resources | Enablement method | Defender plans | Access pattern | Private cluster support and prerequisites |
| --- | --- | --- | --- | --- | --- |
| Container registry vulnerability assessment | ACR, ECR, GAR, GCR, Docker Hub, JFrog Artifactory | Registry access | Containers; CSPM | Registry access | Supported |
| Runtime container vulnerability assessment (registry scan-based) | ACR, ECR, GAR, GCR, Docker Hub, JFrog Artifactory | Agentless scanning for machines and Kubernetes API access or Defender sensor | Containers; CSPM | Registry access and Kubernetes API access | Supported by enabling a restricted public API endpoint |
| Runtime container vulnerability assessment (registry-agnostic) | AKS | Agentless scanning for machines and Kubernetes API access or Defender sensor | Containers; CSPM | Cloud-provider access and Kubernetes API access | Supported by enabling a restricted public API endpoint |
| Gated deployment | AKS, EKS, GKE | Defender sensor, security findings, and registry access | Containers | Kubernetes API access and sensor outbound connectivity | Supported by enabling a restricted public API endpoint or by using Defender Sensor private clusters version (Preview) |

## Runtime protection features

The following table summarizes runtime protection features and their access patterns.

| Feature | Supported resources | Enablement method | Defender plans | Access pattern | Private cluster support and prerequisites |
| --- | --- | --- | --- | --- | --- |
| Control plane detection | AKS, EKS, GKE | Enabled with Containers plan | Containers | Cloud-native audit log ingestion | Supported |
| Workload detection | AKS, EKS, GKE | Defender sensor | Containers | Sensor outbound connectivity | Requires outbound HTTPS access |
| Binary drift detection | AKS, EKS, GKE | Defender sensor | Containers | Kubernetes API access and sensor outbound connectivity | Policy definitions require enabling a restricted public API endpoint or by using Defender Sensor private clusters version (Preview). Requires outbound HTTPS access. |
| DNS detection | AKS, EKS, GKE | Defender sensor installed by using Helm | Containers | Sensor outbound connectivity | Requires outbound HTTPS access |
| Advanced hunting in XDR | AKS, EKS, GKE | Defender sensor | Containers | Sensor outbound connectivity | Requires outbound HTTPS access |
| Response actions in XDR | AKS, EKS, GKE | Defender sensor and Kubernetes API access | Containers | Kubernetes API access | Supported by enabling a restricted public API endpoint |
| Malware detection | AKS, EKS, GKE nodes | Agentless scanning for machines | Containers; Servers P2 | Kubernetes API access and sensor outbound connectivity | Supported by enabling a restricted public API endpoint or by using Defender Sensor private clusters version (Preview). Requires outbound HTTPS access. |

## Posture management features

The following table summarizes posture management features and their access patterns.

| Feature | Supported resources | Enablement method | Defender plans | Access pattern | Private cluster support and prerequisites |
| --- | --- | --- | --- | --- | --- |
| Agentless discovery for Kubernetes | AKS, EKS, GKE | Kubernetes API access | Containers; CSPM | Cloud-provider access | Supported |
| Comprehensive inventory capabilities | Registries: ACR, ECR, GAR, GCR, Docker Hub, JFrog Artifactory. Clusters: AKS, EKS, GKE | Kubernetes API access | Containers; CSPM | Kubernetes API access and cloud-provider access | Supported by enabling a restricted public API endpoint or by using Defender Sensor private clusters version (Preview) |
| Attack path analysis | Registries: ACR, ECR, GAR, GCR, Docker Hub, JFrog Artifactory. Clusters: AKS, EKS, GKE | Kubernetes API access | Defender CSPM | Kubernetes API access and cloud-provider access | Inventory capabilities are a prerequisite |
| Enhanced risk-hunting | Registries: ACR, ECR, GAR, GCR, Docker Hub, JFrog Artifactory. Clusters: AKS, EKS, GKE | Kubernetes API access | Containers; CSPM | Kubernetes API access and cloud-provider access | Inventory capabilities are a prerequisite |
| Control plane hardening | Registries: ACR. Clusters: AKS, EKS, GKE | Enabled with Containers plan | Free | Cloud-provider access | Supported |
| Workload hardening | AKS, EKS, GKE | Azure Policy for Kubernetes | Free | Kubernetes API access | Supported by enabling a restricted public API endpoint or by using Defender Sensor private clusters version (Preview) |
| CIS Kubernetes Service | AKS, EKS, GKE | Assigned as a security standard | Containers; CSPM | Kubernetes API access | Supported by enabling a restricted public API endpoint or by using Defender Sensor private clusters version (Preview) |