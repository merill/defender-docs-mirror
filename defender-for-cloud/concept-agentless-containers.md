---
layout: Conceptual
title: Agentless container posture in Defender CSPM - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/concept-agentless-containers
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
description: Learn how agentless container posture offers discovery, visibility, and vulnerability assessment for containers without installing a sensor on your machines.
ms.topic: concept-article
ms.date: 2026-05-18T00:00:00.0000000Z
ms.custom: template-concept
ai-usage: ai-assisted
locale: en-us
document_id: 7ed26540-c6c0-ec37-3968-5cbfd6d4d0b4
document_version_independent_id: 333295df-7438-e1bf-4429-27f3b8b57b94
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/concept-agentless-containers.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/concept-agentless-containers
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/concept-agentless-containers.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: b0d873e0-7c65-41a6-10c9-5560ee541cd3
---

# Agentless container posture in Defender CSPM - Microsoft Defender for Cloud | Microsoft Learn

The Defender for Cloud Security Posture Management (CSPM) plan in Defender for Cloud provides container posture capabilities for Azure, AWS, and GCP. For requirements and support, see the [Containers support matrix in Defender for Cloud](support-matrix-defender-for-containers).

Agentless container posture provides easy and seamless visibility into your Kubernetes assets and security posture, with contextual risk analysis that empowers security teams to prioritize remediation based on actual risk behind security issues, and proactively hunt for posture issues.

## Capabilities

Agentless container posture provides the following capabilities:

- **Agentless discovery for Kubernetes** - provides zero footprint, API-based discovery of your Kubernetes clusters, their configurations, and deployments.
- **[Comprehensive inventory capabilities](how-to-manage-cloud-security-explorer#build-a-query)** - enables you to explore Kubernetes resources: clusters, workloads, networking, node pools, container registries, container image software, Kubernetes (K8s) configuration, and security insights through [security explorer](how-to-manage-cloud-security-explorer#build-a-query) to easily monitor and manage your assets.
- **[Agentless vulnerability assessment](agentless-vulnerability-assessment-azure)** - provides vulnerability assessment for Kubernetes node pools, container images, including recommendations for registry and runtime, near real-time scans of new images, daily refresh of results, exploitability insights, and more. Vulnerability information is added to the security graph for contextual risk assessment and calculation of attack paths, and hunting capabilities.
- **[Attack path analysis](concept-attack-path)** - Contextual risk assessment exposes exploitable paths that attackers might use to breach your environment and are reported as attack paths to help prioritize posture issues that matter most in your environment.
- **[Enhanced risk-hunting](how-to-manage-cloud-security-explorer)** - Enables security admins to actively hunt for posture issues in their containerized assets through queries (built-in and custom) and [security insights](attack-path-reference#insights) in the [security explorer](how-to-manage-cloud-security-explorer).
- **Control plane hardening** - Defender for Cloud continuously assesses the configurations of your clusters and compares them with the initiatives applied to your subscriptions. When it finds misconfigurations, Defender for Cloud generates security recommendations that are available on Defender for Cloud's Recommendations page. The recommendations let you investigate and remediate issues. For details on the recommendations included with this capability, check out the [container recommendations](recommendations-reference-container) of the type **control plane**.
- **Exposure and service misconfiguration signals** - Posture signals help identify Kubernetes networking misconfigurations, including service and ingress configurations that can unintentionally expose workloads to the internet. This context helps teams prioritize higher-risk findings, especially where public exposure combines with weak or missing authentication. For related alert context, see [alerts for Kubernetes clusters](alerts-containers).
- **Critical Asset protection** - enables security administrators to automatically tag "crown" jewels" resources that are most critical to their organizations, allowing Defender for Cloud to provide them with the highest level of protection and prioritize security issues on those assets above anything else.