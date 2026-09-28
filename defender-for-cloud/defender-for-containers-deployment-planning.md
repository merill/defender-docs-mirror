---
layout: Conceptual
title: Deployment planning for Microsoft Defender for Containers - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-containers-deployment-planning
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
description: Learn how to plan deployment of Microsoft Defender for Containers across Kubernetes environments, including onboarding, deployment methods, and post-deployment verification.
ms.topic: concept-article
ms.date: 2026-03-16T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 50efac4e-65c6-0e8f-994b-fb512a64d54a
document_version_independent_id: 8b941632-9096-21b0-1d99-36b6b056533d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-containers-deployment-planning.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-containers-deployment-planning
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-containers-deployment-planning.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/d44a5346-5de4-439c-b804-7b2a536cbb55
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/da41a22b-b7a0-42d3-9c35-50da1c2b7b87
platformId: 8096d788-fe09-1088-0117-ee15ef4485e4
---

# Deployment planning for Microsoft Defender for Containers - Microsoft Defender for Cloud | Microsoft Learn

This article helps you plan how to deploy Microsoft Defender for Containers across Kubernetes environments. It focuses on the Defender for Containers components that are deployed to Kubernetes clusters, including the Defender sensor and Azure Policy for Kubernetes.

Other capabilities, such as Registry access, Kubernetes API access, and agentless threat protection, are enabled through Defender for Containers plan or connector settings.

## Onboard the environment

Before Defender for Containers can deploy cluster components, the Kubernetes environment must be connected to Microsoft Defender for Cloud.

| Environment | Onboarding path |
| --- | --- |
| **AKS** | No additional connector is required. AKS clusters are native Azure resources. |
| **EKS** | [Onboard AWS to Defender for Cloud](quickstart-onboard-aws). |
| **GKE** | [Onboard GCP to Defender for Cloud](quickstart-onboard-gcp). |
| **On-premises and other Arc-enabled Kubernetes clusters** | [Connect your existing Kubernetes cluster to Azure Arc](/en-us/azure/azure-arc/kubernetes/quickstart-connect-cluster). |

## Deployment options

| Deployment approach | Description |
| --- | --- |
| **Automatic provisioning** | Supported components are deployed automatically after the Defender for Containers plan or relevant settings are enabled. |
| **Manual deployment** | Automatic provisioning is turned off and supported components are installed manually. Manual deployment also includes the preview deployment path for private clusters. |
| **Mixed deployment** | Automatic provisioning is enabled, but specific AKS, EKS, or GKE clusters are excluded and deployed manually. Mixed deployment isn't supported for on-premises or other Kubernetes clusters connected directly to Azure Arc. |

## Automatic provisioning

With automatic provisioning enabled, Microsoft Defender for Cloud installs supported cluster components after the Defender for Containers plan and the relevant settings are enabled.

For AKS clusters, Defender sensor deployment uses the **Defender AKS add-on**. For EKS and GKE clusters, deployment uses Azure Arc Kubernetes extensions on the Arc-enabled Kubernetes resources created through the AWS or GCP connector flow.

For on-premises and other Kubernetes clusters connected directly to Azure Arc, the cluster must first be connected to Azure Arc. Deployment then uses Azure Arc Kubernetes extensions after the relevant Defender for Containers settings are enabled.

You can customize automatic Defender sensor provisioning by excluding specific clusters using tags before enabling the Defender for Containers plan, and then deploying the sensor manually.

Note

Exclusion tags apply to automatic Defender sensor deployment. They don't apply to on-premises or other Kubernetes clusters connected directly to Azure Arc.

With automatic provisioning, the Defender sensor is installed after the cluster is discovered and can take several hours to complete.

Use manual deployment or exclude specific clusters from automatic Defender sensor provisioning and deploy the sensor manually to install the Defender sensor immediately.

## Manual deployment

If automatic provisioning is disabled, supported cluster components aren't deployed automatically. You can deploy supported components manually.

Manual deployment can also be used for Defender sensor deployment on clusters that are excluded from automatic Defender sensor provisioning.

You can deploy components manually by using one of the following methods:

- [Deploy Defender sensor and Azure Policy to clusters using Azure CLI](defender-for-containers-deploy-azure-cli)
- [Deploy Defender for Containers to private clusters (Preview)](defender-for-containers-private-clusters)
- [Install Defender for Containers sensor by using Helm](deploy-helm)

## Post-deployment steps

After deployment, verify that Defender components are running correctly and address any issues.

- [Verify Defender for Containers deployment](defender-for-containers-verify-deployment)
- [Troubleshoot Defender for Containers deployment](defender-for-containers-troubleshoot)