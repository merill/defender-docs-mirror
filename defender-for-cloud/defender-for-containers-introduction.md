---
layout: Conceptual
title: Introduction to Microsoft Defender for Containers - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-containers-introduction
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
description: Learn about Microsoft Defender for Containers, a cloud-native solution that secures your containerized assets across multicloud and on-premises environments.
ms.topic: overview
ms.date: 2026-08-10T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1015
locale: en-us
document_id: 3f6e81d1-78a0-8f52-2379-fb7f4fe6b7e5
document_version_independent_id: 0741d9c7-dd69-bb27-25d1-c67474a4e18c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-containers-introduction.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-containers-introduction
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-containers-introduction.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 00c6617c-ce9e-647b-0635-555205d6eae8
---

# Introduction to Microsoft Defender for Containers - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Containers is a cloud-native solution that enhances, monitors, and maintains the security of your containerized assets. These assets include Kubernetes clusters, nodes, workloads, registries, images, and more. It protects applications across multicloud and on-premises environments.

For a comparison of AWS and GCP coverage by plan, see the [multicloud workload protection support matrix](multicloud-support-matrix).

Defender for Containers helps you with five core domains of container security:

- **Security posture management**: Runs continuous monitoring of cloud APIs, Kubernetes APIs, and Kubernetes workloads. It discovers cloud resources, provides comprehensive inventory capabilities, detects misconfigurations with mitigation guidelines, provides contextual risk assessment, and empowers users to perform enhanced risk hunting capabilities through the Defender for Cloud security explorer.
- **Vulnerability assessment**: Performs agentless vulnerability assessment of [container registry images, running containers, and supported Kubernetes nodes](support-matrix-defender-for-containers) with remediation guidelines, zero configuration, daily re-scans, coverage for OS and language packages, and exploitability insights. The vulnerability findings artifact is signed with a Microsoft certificate for integrity and authenticity and is associated with the container image in the registry for validation needs.
- **Run-time threat protection**: A rich threat detection suite for Kubernetes clusters, nodes, and workloads, powered by Microsoft leading threat intelligence, provides mapping to MITRE ATT&CK framework for easy understanding of risk and relevant context, and automated response. Security operators can also investigate and respond to threats to Kubernetes services through the [Microsoft Defender XDR portal](/en-us/defender-xdr/investigate-respond-container-threats).
- [**Software supply chain protection**](containers-software-supply-chain-security-introduction): Helps reduce the risk of deploying vulnerable container images by scanning images, associating vulnerability findings with images in the registry, and using those findings to support gated deployment for Kubernetes. You can use gated deployment rules to audit or block deployments when images don't meet your organization's vulnerability policy.
- **Deployment & monitoring**: Monitors your Kubernetes clusters for missing sensors and provides frictionless at-scale deployment for sensor-based capabilities, support for standard Kubernetes monitoring tools, and management of unmonitored resources.

You can learn more by watching this video from the Defender for Cloud in the Field video series: [Microsoft Defender for Containers](episode-three).

Defender for Containers provides the following core capabilities:

- **Security posture management**: Continuously monitors cloud APIs, Kubernetes APIs, and Kubernetes workloads to discover resources, detect misconfigurations, and surface security recommendations with mitigation guidance. Posture data is available through inventory views, recommendations, and [Security Explorer](how-to-manage-cloud-security-explorer) for risk investigation and hunting.
- **Vulnerability assessment**: Performs agentless vulnerability assessment of [container registry images, running containers, and supported Kubernetes nodes](support-matrix-defender-for-containers). Findings include remediation guidance, exploitability insights, and integration with the [cloud security graph](concept-attack-path#what-is-the-cloud-security-graph) for contextual risk analysis.
- **Run-time threat protection**: Detects suspicious activity in Kubernetes clusters, nodes, and workloads using Kubernetes-aware analytics and threat intelligence. Alerts are mapped to the MITRE ATT&CK® framework for Containers and can be investigated through [Microsoft Defender XDR](/en-us/defender-xdr/investigate-respond-container-threats).
- **Software supply chain protection**: Helps reduce the risk of deploying vulnerable images by scanning container images and associating vulnerability assessment findings with images in the registry. These findings can be used by other Defender for Containers capabilities, such as gated deployments for Kubernetes.
- **Deployment & monitoring**: Supports at-scale deployment and monitoring of Defender components, including visibility into Kubernetes clusters that are missing sensors or not fully protected.

## Security posture management

### Agentless capabilities

- **Agentless discovery for Kubernetes**: Provides zero footprint, API-based discovery of your Kubernetes clusters, configurations, and deployments.
- **Agentless vulnerability assessment**: Provides vulnerability assessment for [cluster nodes](kubernetes-nodes-va) and for [all container images](agentless-vulnerability-assessment-azure), including recommendations for registry and runtime, quick scans of new images, daily refresh of results, exploitability insights, and more. Vulnerability information is added to the security graph for contextual risk assessment and calculation of attack paths, and hunting capabilities.
- **Comprehensive inventory capabilities**: Enables you to explore resources, pods, services, repositories, images, and configurations through [security explorer](how-to-manage-cloud-security-explorer#build-a-query) to easily monitor and manage your assets.
- **[Enhanced risk-hunting](how-to-manage-cloud-security-explorer)**: Enables security admins to actively hunt for posture issues in their containerized assets through queries (built-in and custom) and [security insights](attack-path-reference#insights) in the [security explorer](how-to-manage-cloud-security-explorer)
- **Control plane hardening**: Continuously assesses the configurations of your clusters and compares them with the initiatives applied to your subscriptions. When it finds misconfigurations, Defender for Cloud generates security recommendations that are available on Defender for Cloud's Recommendations page. The recommendations let you investigate and remediate issues.

    You can use the resource filter to review the outstanding recommendations for your container-related resources, whether in asset inventory or the recommendations page:

    For details included with this capability, review [container recommendations](recommendations-reference-container), and look for recommendations with type "Control plane"

### Sensor-based capabilities

**Antimalware**: Defender for Containers provides a sensor-based capability that detects and alerts you to malicious activities within containers. This helps in identifying and mitigating potential security threats proactively. For more information, see [Antimalware protection](anti-malware).

**DNS detection**: Defender for Containers provides a sensor-based capability that detects suspicious DNS activity from container workloads to help identify network-based threats. For runtime protection availability by cloud, see [Runtime protection features](support-matrix-defender-for-containers#runtime-protection-features).

**Binary drift detection**: Defender for Containers provides a sensor-based capability that alerts you about potential security threats by detecting unauthorized external processes within containers. You can define drift policies to specify conditions under which alerts should be generated, helping you distinguish between legitimate activities and potential threats. For more information, see [Binary drift protection](binary-drift-detection).

**Binary drift blocking**: Defender for Containers provides a sensor-based capability that blocks unauthorized external processes within containers. You can define drift policies to specify conditions under which processes should be blocked, helping you prevent potential security threats. For more information, see [Binary drift protection](binary-drift-detection).

**Kubernetes data plane hardening**: To protect the workloads of your Kubernetes containers with best practice recommendations, you can install the [Azure Policy for Kubernetes](/en-us/azure/governance/policy/concepts/policy-for-kubernetes). Learn more about [monitoring components](monitoring-components) for Defender for Cloud.

With the policies defined for your Kubernetes cluster, every request to the Kubernetes API server is monitored against the predefined set of best practices before being persisted to the cluster. You can then configure it to enforce the best practices and mandate them for future workloads.

For example, you can mandate that privileged containers shouldn't be created, and any future requests to do so are blocked.

You can learn more about [Kubernetes data plane hardening](kubernetes-workload-protections).

## Vulnerability assessment

Defender for Containers scans the cluster node OS and application software, container images in Azure Container Registry (ACR), Amazon AWS Elastic Container Registry (ECR), Google Artifact Registry (GAR), Google Container Registry (GCR), and [supported external image registries](support-matrix-defender-for-containers#vulnerability-assessment-va-features) to provide agentless vulnerability assessment.

Now for [public preview in multicloud environments](agentless-vulnerability-assessment-azure), Defender for Containers also performs a daily scan of all running containers to provide an updated vulnerability assessment, agnostic to the container's image registry.

Vulnerability information powered by Microsoft Defender Vulnerability Management is added to the [cloud security graph](concept-attack-path#what-is-the-cloud-security-graph) for contextual risk, calculation of attack paths, and hunting capabilities.

Learn more about [vulnerability assessments for Defender for Containers supported environments](agentless-vulnerability-assessment-azure), including [vulnerability assessment for cluster nodes](kubernetes-nodes-va).

## Run-time protection for Kubernetes nodes and clusters

Defender for Containers provides real-time threat protection for [supported containerized environments](support-matrix-defender-for-containers#runtime-protection-features) and generates alerts for suspicious activities. You can use this information to quickly remediate security issues and improve the security of your containers.

Threat protection is provided for Kubernetes at the cluster, node, and workload levels. Both sensor-based coverage that requires the [Defender sensor](defender-for-cloud-glossary#defender-sensor) and agentless coverage based on analysis of the Kubernetes audit logs are used to detect threats. Security alerts are only triggered for actions and deployments that occur after you enable Defender for Containers on your subscription.

### Runtime detection examples

Examples of security events that Microsoft Defender for Containers monitors include:

- Exposed Kubernetes dashboards
- Exposed Kubernetes service detected (when a Kubernetes Service of type `LoadBalancer` is created or updated and publicly exposes workloads)
- Creation of high privileged roles
- Creation of sensitive mounts

Prioritize exposure alerts when internet-facing access is unintended or when the exposed service has weak or missing authentication.

For more information about alerts detected by Defender for Containers, including an alert simulation tool, see [alerts for Kubernetes clusters](alerts-containers).

Defender for Containers includes threat detection with over 60 Kubernetes-aware analytics, AI, and anomaly detections based on your runtime workload.

Defender for Cloud monitors the attack surface of multicloud Kubernetes deployments based on the MITRE ATT&CK® matrix for Containers, a framework developed by the [Center for Threat-Informed Defense](https://mitre-engenuity.org/cybersecurity/center-for-threat-informed-defense/) in close partnership with Microsoft.

Defender for Cloud is [integrated with Microsoft Defender XDR](concept-integration-365). When Defender for Containers is enabled, security operators can use [Defender XDR to investigate and respond](/en-us/defender-xdr/investigate-respond-container-threats) to security issues in supported Kubernetes services.

### Microsoft-maintained container images

Defender for Containers deploys container images that are maintained and updated by Microsoft as part of the runtime protection components. These images are published to Microsoft Container Registry (MCR).

Customers don't modify or patch these images directly. Microsoft maintains and updates them as part of the Defender for Containers release process.

The following images are used by Defender for Containers runtime protection components:

| Image | Purpose | MCR path |
| --- | --- | --- |
| `security-publisher` | Publishes security findings collected from Kubernetes environments | `mcr.microsoft.com/azuredefender/stable/security-publisher` |
| `low-level-collector` | Collects low-level runtime telemetry from Kubernetes nodes | `mcr.microsoft.com/azuredefender/stable/low-level-collector` |
| `pod-collector` | Collects Kubernetes pod runtime data used for threat detection | `mcr.microsoft.com/azuredefender/stable/pod-collector` |
| `anti-malware-collector` | Collects malware detection signals for container workloads | `mcr.microsoft.com/azuredefender/stable/anti-malware-collector` |
| `old-file-cleaner` | Cleans up temporary and stale files as part of initialization workflows | `mcr.microsoft.com/azuredefender/stable/old-file-cleaner` |
| `audit-logs-enabler` | Enables audit log collection for supported environments (for example, on-premises clusters) | `mcr.microsoft.com/azuredefender/stable/audit-logs-enabler` |
| `defender-admission-controller` | Enforces runtime gating policies for Kubernetes workloads | `mcr.microsoft.com/mdc/prd/defender-admission-controller` |

Updates are delivered through the deployment mechanism used by your environment. For example:

- When deployed using the **AKS add-on**, updates are delivered through the AKS release lifecycle.
- When deployed using **Helm**, updates are released within 30 days through updated chart versions.

If you detect a vulnerability in a Microsoft-maintained Defender image, open an Azure support request and include the image name, tag, and CVE identifier.