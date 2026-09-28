---
layout: Conceptual
title: Containers support matrix in Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/support-matrix-defender-for-containers
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
description: Review support requirements for container capabilities in Microsoft Defender for Cloud.
ms.topic: limits-and-quotas
ms.date: 2026-06-02T00:00:00.0000000Z
ms.custom: references_regions
ai-usage: ai-assisted
locale: en-us
document_id: 64c86ac7-b656-0b18-be4a-81bd0765bc10
document_version_independent_id: 081d6cd6-7a6f-8597-3f4b-e3ecf91c9231
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/support-matrix-defender-for-containers.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/support-matrix-defender-for-containers
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/support-matrix-defender-for-containers.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/cb49e66a-8528-497d-adaa-eade2d009d1b
- https://authoring-docs-microsoft.poolparty.biz/devrel/d44a5346-5de4-439c-b804-7b2a536cbb55
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/472c9d15-157b-443c-afa2-e209c8fecf58
- https://authoring-docs-microsoft.poolparty.biz/devrel/da41a22b-b7a0-42d3-9c35-50da1c2b7b87
platformId: 80ba40de-ac32-96a7-c2d1-be9cddbb1953
---

# Containers support matrix in Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

Important

All Microsoft Defender for Cloud features will be officially retired in the Azure in China region on October 1, 2026. Due to this upcoming retirement, Azure in China customers are no longer able to onboard new subscriptions to the service. A new subscription is any subscription that was not already onboarded to the Microsoft Defender for Cloud service prior to August 18, 2025, the date of the retirement announcement. For more information on the retirement, see [Microsoft Defender for Cloud Deprecation in Microsoft Azure Operated by 21Vianet Announcement](https://aka.ms/mdcretirementinchina).

Customers should work with their account representatives for Microsoft Azure operated by 21Vianet to assess the impact of this retirement on their own operations.

This article summarizes support information for container capabilities in Microsoft Defender for Cloud.

Note

- Specific features are in preview. The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include other legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.
- Defender for Cloud officially supports only the versions of AKS, EKS, and GKE that the cloud vendor supports.

The following table lists the features provided by Defender for Containers for the supported cloud environments and container registries.

## Microsoft Defender for Containers plan availability

| Aspect | Details |
| --- | --- |
| Release state: | General availability (GA) Certain features are in preview. For a full list, see the tables below |
| Pricing: | **Microsoft Defender for Containers** is billed as shown on the [pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/). You can also [estimate costs with the Defender for Cloud cost calculator](cost-calculator). |
| Required roles and permissions: | *To deploy the required components, see the [permissions for each of the components](monitoring-components#defender-for-containers-extensions)***Security admin** can dismiss alerts \* **Security reader** can view vulnerability assessment findings See also [Roles for remediation](permissions#roles-used-to-automatically-configure-agents-and-extensions) and [Azure Container Registry roles and permissions](/en-us/azure/container-registry/container-registry-roles) |

## Vulnerability assessment (VA) features

# [Azure](#tab/azureva)
| Feature | Description | Supported resources | Linux release state | Windows release state | Enablement method | Plans | Clouds availability |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Container registry VA | VA for images in container registries | ACR, ECR, GAR, GCR, Docker Hub, JFrog Artifactory | GA | GA | Requires **Registry access**^1^ or Connector creation for Docker Hub/JFrog | **Defender for Containers** or **Defender CSPM** | Commercial cloudsNational clouds: Azure Government, Azure operated by 21Vianet |
| Runtime container VA - Registry scan based | VA of containers running images from supported registries | ACR, ECR, GAR, GCR, Docker Hub, JFrog Artifactory | GA | GA | Requires **Registry access**^1^ or Connector creation for Docker Hub/JFrog and either **K8S API access** or **Defender sensor**^1^ | **Defender for Containers** or **Defender CSPM** | Commercial cloudsNational clouds: Azure Government, Azure operated by 21Vianet |
| Runtime container VA | Registry agnostic VA of container running images | All | GA | - | Requires **Agentless scanning for machines** and either **K8S API access** or **Defender sensor**^1^ | **Defender for Containers** or **Defender CSPM** | Commercial cloudsNational clouds: Azure Government, Azure operated by 21Vianet |
| Runtime Node VA | Kubernetes node vulnerability assessment | AKS nodes | GA | GA | Requires **Agentless scanning for machines** | **Defender for Containers** or **Defender for servers Plan 2** or **Defender CSPM** | Commercial cloudsNational clouds: Azure Government, Azure operated by 21Vianet |

^1^National clouds are automatically enabled and can't be disabled.

# [AWS](#tab/awsva)
| Feature | Description | Supported resources | Linux release state | Windows release state | Enablement method | Plans | Clouds availability |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Container registry VA | Vulnerability assessments for images in container registries | ACR, ECR, GAR, GCR, Docker Hub, JFrog Artifactory | GA | GA | Requires **Registry access** | **Defender for Containers** or **Defender CSPM** | AWS |
| Runtime container VA - Registry scan based | VA of containers running images from supported registries | ACR, ECR, GAR, GCR, Docker Hub, JFrog Artifactory | GA | - | Requires **Agentless scanning for machines** and either **K8S API access** or **Defender sensor** | **Defender for Containers** or **Defender CSPM** | AWS |
| Runtime Node VA | Kubernetes node vulnerability assessment | EKS nodes | Preview | - | Requires **Agentless scanning for machines** | **Defender for Containers** or **Defender CSPM** | AWS |

# [GCP](#tab/gcpva)
| Feature | Description | Supported resources | Linux release state | Windows release state | Enablement method | Plans | Clouds availability |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Container registry VA | Vulnerability assessments for images in container registries | ACR, ECR, GAR, GCR, Docker Hub, JFrog Artifactory | GA | GA | Requires **Registry access** | **Defender for Containers** or **Defender CSPM** | GCP |
| Runtime container VA - Registry scan based | VA of containers running images from supported registries | ACR, ECR, GAR, GCR, Docker Hub, JFrog Artifactory | GA | - | Requires **Agentless scanning for machines** and either **K8S API access** or **Defender sensor** | **Defender for Containers** or **Defender CSPM** | GCP |
| Runtime Node VA | Kubernetes node vulnerability assessment | GKE nodes | Preview | - | Requires **Agentless scanning for machines** | **Defender for Containers** or **Defender CSPM** | GCP |

# [Arc Connected clusters](#tab/arcva)
| Feature | Description | Supported resources | Linux release state | Windows release state | Enablement method | Plans | Clouds availability |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Container registry VA | Vulnerability assessments for images in container registries | ACR, ECR, GAR, GCR, Docker Hub, JFrog Artifactory | GA | GA | Requires **Registry access** | **Defender for Containers** or **Defender CSPM** | Arc Connected clusters |

---

#### Registries and images support for vulnerability assessment

| Aspect | Details |
| --- | --- |
| Registries and images | **Supported** \* Container images in Docker V2 format  \* Images with [Open Container Initiative (OCI)](https://github.com/opencontainers/image-spec/blob/main/spec.md) image format specification **Unsupported** \* Super-minimalist images such as [Docker scratch](https://hub.docker.com/_/scratch/) images are currently unsupported  \* Public repositories  \* Manifest lists |
| Operating systems | **Supported** \* Alpine Linux 3.12-3.22 \* Red Hat Enterprise Linux 6-9  \* CentOS 6-9 (CentOS is End Of Service as of June 30, 2024. For more information, see the [CentOS End Of Life guidance](/en-us/azure/virtual-machines/workloads/centos/centos-end-of-life).) \* Oracle Linux 6-9  \* Amazon Linux 1, 2  \* openSUSE Leap, openSUSE Tumbleweed  \* SUSE Enterprise Linux 11-15  \* Debian GNU/Linux 7-12  \* Google Distroless (based on Debian GNU/Linux 7-12) \* Ubuntu 12.04-24.04  \* Fedora 31-37 \* Azure Linux 1-3 \* Windows server 2016, 2019, 2022 \* Chainguard OS/Wolfi OS  \* Alma Linux 8.4 or later  \* Rocky Linux 8.7 or later \* Minimus  \* Photon OS 2.0-5.0  \* Docker Hardened Images (DHI) |
| Language specific packages | **Supported** \* Python  \* Node.js  \* PHP  \* Ruby  \* Rust  \* .NET  \* Java \* Go |

## Runtime protection features

# [Azure](#tab/azurert)
| Feature | Description | Supported resources | Linux release state | Windows release state | Enablement method | Plans | Clouds availability |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Advanced hunting in XDR | View cluster incidents and alerts in Microsoft XDR | AKS | GA | GA | Requires **Defender sensor** | **Defender for Containers** | Commercial clouds and National clouds: Azure Government, Azure operated by 21Vianet |
| Antimalware | Detection of malware | AKS | GA | - | Requires **Defender sensor via Helm** | **Defender for Containers** | Commercial cloudsNational clouds: Azure Government |
| Binary drift detection and blocking | Detects binary of runtime container from container image | AKS | GA | - | Requires **Defender sensor** | **Defender for Containers** | Commercial cloudsNational clouds: Azure Government, Azure operated by 21Vianet |
| DNS Detection | Detects suspicious DNS activity from container workloads | AKS | GA | - | Requires **Defender sensor via Helm** | **Defender for Containers** | Commercial cloudsNational clouds: Azure Government |
| Malware detection | Detection of malware | AKS nodes | GA | GA | Requires **Agentless scanning for machines** | **Defender for Containers** or **Defender for Servers Plan 2** | - |
| Response actions in XDR | Provides automated and manual remediation in Microsoft XDR | AKS | Preview | - | Requires **Defender sensor** and **K8S access API** | **Defender for Containers** | Commercial clouds and National clouds: Azure Government, Azure operated by 21Vianet |
| Workload detection | Monitors containerized workloads for threats and gives alerts to suspicious activities | AKS | GA | - | Requires **Defender sensor** | **Defender for Containers** | Commercial clouds and National clouds: Azure Government, Azure operated by 21Vianet |

#### Kubernetes distributions and configurations for runtime threat protection in Azure

| Aspect | Details |
| --- | --- |
| Kubernetes distributions and configurations | **Supported** \* [Azure Kubernetes Service (AKS)](/en-us/azure/aks/intro-kubernetes) with [Kubernetes RBAC](/en-us/azure/aks/concepts-identity#kubernetes-rbac)**Supported via Arc enabled Kubernetes**^1^^2^ \* [Azure Kubernetes Service hybrid](/en-us/azure/aks-hybrid-edge/aks-overview) \* [Kubernetes](https://kubernetes.io/docs/home/) \* [AKS Engine](https://github.com/Azure/aks-engine) |

^1^ Any Cloud Native Computing Foundation (CNCF) certified Kubernetes clusters should be supported, but only the specified clusters are tested on Azure.

^2^ To get [Microsoft Defender for Containers](defender-for-containers-introduction) protection for your environments, you need to onboard [Azure Arc-enabled Kubernetes](/en-us/azure/azure-arc/kubernetes/overview) and enable Defender for Containers as an Arc extension.

Note

For additional requirements for Kubernetes workload protection, see [existing limitations](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#limitations).

# [AWS](#tab/awsrt)
| Feature | Description | Supported resources | Linux release state | Windows release state | Enablement method | Plans | Clouds availability |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Advanced hunting in XDR | View cluster incidents and alerts in Microsoft XDR | EKS | GA | GA | Requires **Defender sensor** | **Defender for Containers** | AWS |
| Antimalware | Detection of malware | EKS | GA | - | Requires **Defender sensor via Helm** | **Defender for Containers** | AWS |
| Binary drift detection and blocking | Detects binary of runtime container from container image | EKS | GA | - | Requires **Defender sensor** | **Defender for Containers** | AWS |
| Control plane detection | Detection of suspicious activity for Kubernetes based on Kubernetes audit trail | EKS | GA | GA | Enabled with plan | **Defender for Containers** | AWS |
| DNS Detection | Detects suspicious DNS activity from container workloads | EKS | GA | - | Requires **Defender sensor via Helm** | **Defender for Containers** | AWS |
| Malware detection | Detection of malware | EKS nodes | GA | GA | Requires **Agentless scanning for machines** | **Defender for Containers** or **Defender for Servers Plan 2** | - |
| Response actions in XDR | Provides automated and manual remediation in Microsoft XDR | EKS | Preview | - | Requires **Defender sensor** and **K8S access API** | **Defender for Containers** | AWS |
| Workload detection | Monitors containerized workloads for threats and gives alerts to suspicious activities | EKS | GA | - | Requires **Defender sensor** | **Defender for Containers** | AWS |

#### Kubernetes distributions and configurations support for runtime threat protection in AWS

| Aspect | Details |
| --- | --- |
| Kubernetes distributions and configurations | **Supported***[Amazon Elastic Kubernetes Service (EKS)](https://aws.amazon.com/eks/)**Supported via Arc enabled Kubernetes**^1^^2^*[Kubernetes](https://kubernetes.io/docs/home/)**Unsupported** \* EKS private clusters |

^1^ Any Cloud Native Computing Foundation (CNCF) certified Kubernetes clusters should be supported, but only the specified clusters are tested.

^2^ To get [Microsoft Defender for Containers](defender-for-containers-introduction) protection for your environments, you need to onboard [Azure Arc-enabled Kubernetes](/en-us/azure/azure-arc/kubernetes/overview) and enable Defender for Containers as an Arc extension.

Note

For additional requirements for Kubernetes workload protection, see [existing limitations](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#limitations).

# [GCP](#tab/gcprt)
| Feature | Description | Supported resources | Linux release state | Windows release state | Enablement method | Plans | Clouds availability |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Advanced hunting in XDR | View cluster incidents and alerts in Microsoft XDR | GKE | GA | GA | Requires **Defender sensor** | **Defender for Containers** | GCP |
| Antimalware | Detection of malware | GKE | GA | - | Requires **Defender sensor via Helm** | **Defender for Containers** | GCP |
| Binary drift detection and blocking | Detects binary of runtime container from container image | GKE | GA | - | Requires **Defender sensor** | **Defender for Containers** | GCP |
| Control plane detection | Detection of suspicious activity for Kubernetes based on Kubernetes audit trail | GKE | GA | GA | Enabled with plan | **Defender for Containers** | GCP |
| DNS Detection | Detects suspicious DNS activity from container workloads | GKE | GA | - | Requires **Defender sensor via Helm** | **Defender for Containers** | GCP |
| Malware detection | Detection of malware | GKE nodes | GA | GA | Requires **Agentless scanning for machines** | **Defender for Containers** or **Defender for Servers Plan 2** | - |
| Response actions in XDR | Provides automated and manual remediation in Microsoft XDR | GKE | Preview | - | Requires **Defender sensor** and **K8S access API** | **Defender for Containers** | GCP |
| Workload detection | Monitors containerized workloads for threats and gives alerts to suspicious activities | GKE | GA | - | Requires **Defender sensor** | **Defender for Containers** | GCP |

#### Kubernetes distributions and configurations support for runtime threat protection in GCP

| Aspect | Details |
| --- | --- |
| Kubernetes distributions and configurations | **Supported***[Google Kubernetes Engine (GKE) Standard](https://cloud.google.com/kubernetes-engine/)**Supported via Arc enabled Kubernetes**^1^^2^*[Kubernetes](https://kubernetes.io/docs/home/)**Unsupported***Private network clusters* GKE autopilot \* GKE AuthorizedNetworksConfig |

^1^ Any Cloud Native Computing Foundation (CNCF) certified Kubernetes clusters should be supported, but only the specified clusters are tested.

^2^ To get [Microsoft Defender for Containers](defender-for-containers-introduction) protection for your environments, you need to onboard [Azure Arc-enabled Kubernetes](/en-us/azure/azure-arc/kubernetes/overview) and enable Defender for Containers as an Arc extension.

Note

For additional requirements for Kubernetes workload protection, see [existing limitations](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#limitations).

# [Arc enabled Kubernetes clusters](#tab/arcrt)
| Feature | Description | Supported resources | Linux release state | Windows release state | Enablement method | Plans | Clouds availability |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Control plane detection | Detection of suspicious activity for Kubernetes based on Kubernetes audit trail | Arc enabled K8s clusters | Preview | Preview | Requires **Defender sensor** | **Defender for Containers** |  |
| Workload detection | Monitors containerized workloads for threats and gives alerts to suspicious activities | Arc enabled Kubernetes clusters | Preview | - | Requires **Defender sensor** | **Defender for Containers** |  |
| Binary drift detection and blocking | Detects binary of runtime container from container image | - | - | - | - | - | - |
| Advanced hunting in XDR | View cluster incidents and alerts in Microsoft XDR | Arc enabled Kubernetes clusters | Preview - currently supports audit logs & process events | Preview - currently supports audit logs & process events | Requires **Defender sensor** | **Defender for Containers** |  |
| Response actions in XDR | Provides automated and manual remediation in Microsoft XDR | - | - | - | - | - | - |
| Malware detection | Detection of malware | - | - | - | - | - | - |

#### Kubernetes distributions and configurations for runtime threat protection in Arc enabled Kubernetes

| Aspect | Details |
| --- | --- |
| Kubernetes distributions and configurations | **Supported via Arc enabled Kubernetes**^1^^2^\* [Azure Kubernetes Service hybrid](/en-us/azure/aks-hybrid-edge/aks-overview)\* [Azure Red Hat OpenShift](https://azure.microsoft.com/services/openshift/) (Preview)\* [Red Hat OpenShift](https://www.openshift.com/learn/topics/kubernetes/) (version 4.6 or newer) (Preview) |

^1^ Any Cloud Native Computing Foundation (CNCF) certified Kubernetes clusters should be supported, but only the specified clusters are tested.

^2^ To get [Microsoft Defender for Containers](defender-for-containers-introduction) protection for your environments, you need to onboard [Azure Arc-enabled Kubernetes](/en-us/azure/azure-arc/kubernetes/overview) and enable Defender for Containers as an Arc extension.

Note

For additional requirements for Kubernetes workload protection, see [existing limitations](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#limitations).

---

## Security posture management features

# [Azure](#tab/azurespm)
| Feature | Description | Supported resources | Linux release state | Windows release state | Enablement method | Plans | Clouds availability |
| --- | --- | --- | --- | --- | --- | --- | --- |
| [Agentless discovery for Kubernetes](defender-for-containers-introduction#security-posture-management)^1^ | Provides zero footprint, API-based discovery of Kubernetes clusters, their configurations, and deployments. | AKS | GA | GA | Requires **K8S API access** | Defender for Containers **OR** Defender CSPM | Commercial cloudsNational clouds: Azure Government, Azure operated by 21Vianet |
| Comprehensive inventory capabilities | Enables you to explore resources, pods, services, repositories, images, and configurations through [security explorer](how-to-manage-cloud-security-explorer#build-a-query) to easily monitor and manage your assets. | ACR, AKS | GA | GA | Requires **K8S API access** | Defender for Containers **OR** Defender CSPM | Commercial cloudsNational clouds: Azure Government, Azure operated by 21Vianet |
| Attack path analysis | A graph-based algorithm that scans the cloud security graph. The scans expose exploitable paths that bad actors might use to breach your environment. | ACR, AKS | GA | GA | Requires **K8S API access** | Defender CSPM | Commercial cloudsNational clouds: Azure Government, Azure operated by 21Vianet |
| Enhanced risk-hunting | Enables security admins to actively hunt for posture issues in their containerized assets through queries (built-in and custom) and [security insights](attack-path-reference#insights) in the [security explorer](how-to-manage-cloud-security-explorer). | ACR, AKS | GA | GA | Requires **K8S API access** | Defender for Containers **OR** Defender CSPM | Commercial cloudsNational clouds: Azure Government, Azure operated by 21Vianet |
| [Control plane hardening](defender-for-containers-architecture)^1^ | Continuously assesses the configurations of your clusters and compares them with the initiatives applied to your subscriptions. When it finds misconfigurations, Defender for Cloud generates security recommendations that are available on Defender for Cloud's Recommendations page. The recommendations let you investigate and remediate issues. | ACR, AKS | GA | GA | Enabled with plan | Free | Commercial clouds National clouds: Azure Government, Azure operated by 21Vianet |
| [Workload hardening](kubernetes-workload-protections)^1^ | Protect workloads of your Kubernetes containers with best practice recommendations. | AKS | GA | - | Requires **Azure Policy** | Free | Commercial clouds National clouds: Azure Government, Azure operated by 21Vianet |
| CIS Azure Kubernetes Service | CIS Azure Kubernetes Service Benchmark | AKS | GA | - | Requires **K8S API access** and the security standard assigned | Defender for Containers **OR** Defender CSPM | Commercial cloudsNational clouds: Azure Government, Azure operated by 21Vianet |

^1^ This feature can be enabled for an individual cluster when enabling Defender for Containers at the cluster resource level.

# [AWS](#tab/awsspm)
| Feature | Description | Supported resources | Linux release state | Windows release state | Enablement method | Plans | Clouds availability |
| --- | --- | --- | --- | --- | --- | --- | --- |
| [Agentless discovery for Kubernetes](defender-for-containers-introduction#security-posture-management) | Provides zero footprint, API-based discovery of Kubernetes clusters, their configurations, and deployments. | EKS | GA | GA | Requires **K8S API access** | Defender for Containers **OR** Defender CSPM | AWS |
| Comprehensive inventory capabilities | Enables you to explore resources, pods, services, repositories, images, and configurations through [security explorer](how-to-manage-cloud-security-explorer#build-a-query) to easily monitor and manage your assets. | ECR, EKS | GA | GA | Requires **K8S API access** | Defender for Containers **OR** Defender CSPM | AWS |
| Attack path analysis | A graph-based algorithm that scans the cloud security graph. The scans expose exploitable paths that bad actors might use to breach your environment. | ECR, EKS | GA | GA | Requires **K8S API access** | Defender CSPM (requires Agentless discovery for Kubernetes to be enabled) | AWS |
| Enhanced risk-hunting | Enables security admins to actively hunt for posture issues in their containerized assets through queries (built-in and custom) and [security insights](attack-path-reference#insights) in the [security explorer](how-to-manage-cloud-security-explorer). | ECR, EKS | GA | GA | Requires **K8S API access** | Defender for Containers **OR** Defender CSPM | AWS |
| [Control plane hardening](defender-for-containers-architecture) | Continuously assesses the configurations of your clusters and compares them with the initiatives applied to your subscriptions. When it finds misconfigurations, Defender for Cloud generates security recommendations that are available on Defender for Cloud's Recommendations page. The recommendations let you investigate and remediate issues. | - | - | - | - | - | - |
| [Workload hardening](kubernetes-workload-protections) | Protect workloads of your Kubernetes containers with best practice recommendations. | EKS | GA | - | Requires **Auto provision Azure Policy extension for Azure Arc** | Free | AWS |
| CIS Azure Kubernetes Service | CIS Azure Kubernetes Service Benchmark | EKS | GA | - | Assigned as a security standard | Defender for Containers **OR** Defender CSPM | AWS |

# [GCP](#tab/gcpspm)
| Feature | Description | Supported resources | Linux release state | Windows release state | Enablement method | Plans | Clouds availability |
| --- | --- | --- | --- | --- | --- | --- | --- |
| [Agentless discovery for Kubernetes](defender-for-containers-introduction#security-posture-management) | Provides zero footprint, API-based discovery of Kubernetes clusters, their configurations, and deployments. | GKE | GA | GA | Requires **K8S API access** | Defender for Containers **OR** Defender CSPM | GCP |
| Comprehensive inventory capabilities | Enables you to explore resources, pods, services, repositories, images, and configurations through [security explorer](how-to-manage-cloud-security-explorer#build-a-query) to easily monitor and manage your assets. | GCR, GAR, GKE | GA | GA | Requires **K8S API access** | Defender for Containers **OR** Defender CSPM | GCP |
| Attack path analysis | A graph-based algorithm that scans the cloud security graph. The scans expose exploitable paths that bad actors might use to breach your environment. | GCR, GAR, GKE | GA | GA | Requires **K8S API access** | Defender CSPM | GCP |
| Enhanced risk-hunting | Enables security admins to actively hunt for posture issues in their containerized assets through queries (built-in and custom) and [security insights](attack-path-reference#insights) in the [security explorer](how-to-manage-cloud-security-explorer). | GCR, GAR, GKE | GA | GA | Requires **K8S API access** | Defender for Containers **OR** Defender CSPM | GCP |
| [Control plane hardening](defender-for-containers-architecture) | Continuously assesses the configurations of your clusters and compares them with the initiatives applied to your subscriptions. When it finds misconfigurations, Defender for Cloud generates security recommendations that are available on Defender for Cloud's Recommendations page. The recommendations let you investigate and remediate issues. | GKE | GA | GA | Activated with plan | Free | GCP |
| [Workload hardening](kubernetes-workload-protections) | Protect workloads of your Kubernetes containers with best practice recommendations. | GKE | GA | - | Requires **Auto provision Azure Policy extension for Azure Arc** | Free | GCP |
| CIS Azure Kubernetes Service | CIS Azure Kubernetes Service Benchmark | GKE | GA | - | Assigned as a security standard | Defender for Containers **OR** Defender CSPM | GCP |

# [Arc enabled Kubernetes](#tab/arcspm)
| Feature | Description | Supported resources | Linux release state | Windows release state | Enablement method | Plans | Clouds availability |
| --- | --- | --- | --- | --- | --- | --- | --- |
| [Agentless discovery for Kubernetes](defender-for-containers-introduction#security-posture-management) | Provides zero footprint, API-based discovery of Kubernetes clusters, their configurations, and deployments. | - | - | - | - | - | - |
| Comprehensive inventory capabilities | Enables you to explore resources, pods, services, repositories, images, and configurations through [security explorer](how-to-manage-cloud-security-explorer#build-a-query) to easily monitor and manage your assets. | - | - | - | - | - | - |
| Attack path analysis | A graph-based algorithm that scans the cloud security graph. The scans expose exploitable paths that bad actors might use to breach your environment. | - | - | - | - | - | - |
| Enhanced risk-hunting | Enables security admins to actively hunt for posture issues in their containerized assets through queries (built-in and custom) and [security insights](attack-path-reference#insights) in the [security explorer](how-to-manage-cloud-security-explorer). | - | - | - | - | - | - |
| [Control plane hardening](defender-for-containers-architecture) | Continuously assesses the configurations of your clusters and compares them with the initiatives applied to your subscriptions. When it finds misconfigurations, Defender for Cloud generates security recommendations that are available on Defender for Cloud's Recommendations page. The recommendations let you investigate and remediate issues. | - | - | - | - | - | - |
| [Workload hardening](kubernetes-workload-protections) | Protect workloads of your Kubernetes containers with best practice recommendations. | Arc enabled Kubernetes cluster | GA | - | Requires **Auto provision Azure Policy extension for Azure Arc** | Defender for Containers | Arc enabled Kubernetes cluster |
| CIS Azure Kubernetes Service | CIS Azure Kubernetes Service Benchmark | Arc enabled VMs | Preview | - | Assigned as a security standard | Defender for Containers **OR** Defender CSPM | Arc enabled Kubernetes cluster |

# [External registries](#tab/extspm)
| Feature | Description | Supported resources | Linux release state | Windows release state | Enablement method | Plans | Clouds availability |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Container registry vulnerability assessment | Assesses container images for vulnerabilities before deployment. | Docker Hub, JFrog Artifactory | GA | GA | Connector creation | Defender for Containers | - |
| Regulatory compliance and industry best practices | Assesses container images against regulatory compliance and industry best practices. | Docker Hub, JFrog Artifactory | GA | GA | Connector creation | Defender for Containers | - |
| Comprehensive inventory capabilities | Enables you to explore resources, pods, services, repositories, images, and configurations through [security explorer](how-to-manage-cloud-security-explorer#build-a-query) to easily monitor and manage your assets. | Docker Hub, JFrog Artifactory | GA | GA | Connector creation | Foundational CSPM **OR** Defender CSPM **OR** Defender for Containers | - |
| Attack path analysis | A graph-based algorithm that scans the cloud security graph. The scans expose exploitable paths that bad actors might use to breach your environment. | Docker Hub, JFrog Artifactory | GA | GA | Connector creation | Defender CSPM | - |
| Enhanced risk-hunting | Enables security admins to actively hunt for posture issues in their containerized assets through queries (built-in and custom) and [security insights](attack-path-reference#insights) in the [security explorer](how-to-manage-cloud-security-explorer). | Docker Hub, JFrog | GA | GA | Connector creation | Defender for Containers **OR** Defender CSPM |  |
| Agentless code-to-cloud containers vulnerability assessment | Provides contextual vulnerability assessment for container images connected to cloud workloads. | Docker Hub, JFrog Artifactory | GA | GA | Connector creation | Defender for Containers | - |

---

## Containers software supply chain protection features

# [Azure](#tab/azurecssc)
| Feature | Description | Supported resources | Linux release state | Windows release state | Enablement method | Cloud availability |
| --- | --- | --- | --- | --- | --- | --- |
| Gated deployment | Gated deployment of container images to your Kubernetes environment | AKS 1.31 or higher (including AKS Automatic)^1^ | GA | - | Requires **Defender sensor**, **Security gating**, **Security findings**, and **Registry access**. | Commercial clouds |
| Kubernetes misconfiguration enforcement | Audits or blocks Kubernetes deployments that don't meet Microsoft security best-practice rules | AKS | GA | - | Requires **Kubernetes API access**. For manual deployment, Helm is supported. | Commercial clouds |

^1^ On AKS Automatic clusters, the Defender sensor must be installed by using Helm in the `kube-system` namespace. Installation in the `mdc` namespace and add-on deployment aren’t supported for gated deployment.

# [AWS](#tab/awscssc)
| Feature | Description | Supported resources | Linux release state | Windows release state | Enablement method |
| --- | --- | --- | --- | --- | --- |
| Gated deployment | Gated deployment of container images to your Kubernetes environment | EKS 1.31 or higher, Amazon Elastic Container Registry (ECR) | GA | - | Requires **Defender Sensor**, **Security Gating**, **Security Findings**, and **Registry Access** |
| Kubernetes misconfiguration enforcement | Audits or blocks Kubernetes deployments that don't meet Microsoft security best-practice rules | EKS | GA | - | Requires **Agentless threat protection**. For manual deployment, Helm is supported. |

# [GCP](#tab/gcpcssc)
| Feature | Description | Supported resources | Linux release state | Windows release state | Enablement method |
| --- | --- | --- | --- | --- | --- |
| Gated deployment | Gated deployment of container images to your Kubernetes environment | GKE 1.31 or higher, Google Artifact Registry | GA | - | Requires **Defender Sensor**, **Security Gating**, **Security Findings**, and **Registry Access** |
| Kubernetes misconfiguration enforcement | Audits or blocks Kubernetes deployments that don't meet Microsoft security best-practice rules | GKE | GA | - | Requires **Agentless threat protection**. For manual deployment, Helm is supported. |

# [Arc enabled](#tab/arccssc)
| Feature | Description | Supported resources | Linux release state | Windows release state | Enablement method |
| --- | --- | --- | --- | --- | --- |
| Gated deployment | Gated deployment of container images to your Kubernetes environment | Arc enabled Kubernetes clusters | GA | - | Requires **Defender sensor**, **Security gating**, **Security findings**, and **Registry access** |
| Kubernetes misconfiguration enforcement | Audits or blocks Kubernetes deployments that don't meet Microsoft security best-practice rules | Arc enabled Kubernetes clusters | GA | - | Requires **Kubernetes API access**. For manual deployment, Helm is supported. |

---

## Network restrictions

# [AWS](#tab/awsnet)
| Aspect | Details |
| --- | --- |
| Outbound proxy support | Outbound proxy without authentication and outbound proxy with basic authentication are supported. Outbound proxy that expects trusted certificates isn't currently supported. |
| Clusters with IP restrictions | If your Kubernetes cluster in AWS has control plane IP restrictions enabled (see [Amazon EKS cluster endpoint access control - Amazon EKS](https://docs.aws.amazon.com/eks/latest/userguide/cluster-endpoint.html)), the control plane's IP restriction configuration is updated to include the CIDR block of Microsoft Defender for Cloud. |

# [GCP](#tab/gcpnet)
| Aspect | Details |
| --- | --- |
| Outbound proxy support | Outbound proxy without authentication and outbound proxy with basic authentication are supported. Outbound proxy that expects trusted certificates isn't currently supported. |
| Clusters with IP restrictions | If your Kubernetes cluster in GCP has control plane IP restrictions enabled (see [GKE - Add authorized networks for control plane access](https://cloud.google.com/kubernetes-engine/docs/how-to/authorized-networks) ), the control plane's IP restriction configuration is updated to include the CIDR block of Microsoft Defender for Cloud. |

# [Arc enabled](#tab/arcnet)
| Aspect | Details |
| --- | --- |
| Outbound proxy support | Outbound proxy without authentication and outbound proxy with basic authentication are supported. Outbound proxy that expects trusted certificates isn't currently supported. |

---

## Supported host operating systems

Defender for Containers relies on the Defender sensor for several features. The Defender sensor is supported only with Linux Kernel 5.4 and above, on the following host operating systems:

- Amazon Linux 2
- AWS Bottlerocket (provisioning via Helm only)
- CentOS 8 (CentOS reached end of service on June 30, 2024. For more information, see the [CentOS End Of Life guidance](/en-us/azure/virtual-machines/workloads/centos/centos-end-of-life).)
- Debian 10
- Debian 11
- Google Container-Optimized OS
- Azure Linux 1.0
- Azure Linux 2.0
- Red Hat Enterprise Linux 8
- Ubuntu 16.04
- Ubuntu 18.04
- Ubuntu 20.04
- Ubuntu 22.04

Ensure your Kubernetes node runs on one of these verified operating systems. Clusters with unsupported host operating systems don't get the benefits of features that rely on the Defender sensor.

## Defender sensor limitations

The Defender sensor in AKS version 1.28 and earlier versions doesn't support Arm64 nodes.