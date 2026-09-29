---
layout: Conceptual
title: Deploy Defender Sensor and Azure Policy to Clusters Using Azure CLI - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-containers-deploy-azure-cli
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
description: Learn how to deploy Microsoft Defender for Containers sensors and Azure Policy components to AKS, Amazon EKS, and Google Kubernetes Engine clusters by using Azure CLI.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 12087e31-49fb-5993-312b-8a920fe0acbb
document_version_independent_id: ce0769d6-19a6-b6ba-5c7b-b7c39e8938b4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-containers-deploy-azure-cli.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-containers-deploy-azure-cli
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-containers-deploy-azure-cli.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/d44a5346-5de4-439c-b804-7b2a536cbb55
- https://authoring-docs-microsoft.poolparty.biz/devrel/089c8ba6-d135-43ff-bfaf-b8197fb72fb9
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/da41a22b-b7a0-42d3-9c35-50da1c2b7b87
- https://authoring-docs-microsoft.poolparty.biz/devrel/32516e21-6665-416f-be21-413febe47d91
platformId: ef3984b6-6ae6-0985-2ee8-baa02fa13243
---

# Deploy Defender Sensor and Azure Policy to Clusters Using Azure CLI - Microsoft Defender for Cloud | Microsoft Learn

You can deploy the Microsoft Defender for Containers sensor and Azure Policy for Kubernetes to clusters by using Azure CLI. First, enable [the Defender for Containers plan in Microsoft Defender for Cloud](defender-for-containers-enable-plan).

For clusters that aren't running in Azure Kubernetes Service (AKS), Defender for Cloud uses Azure Arc-enabled Kubernetes to deploy the required extensions.

# [Azure Kubernetes Service (AKS)](#tab/aks)
## Prerequisites

- [Defender for Containers enabled on your Azure subscription](defender-for-containers-enable-plan?tab=aks).
- Azure CLI version 2.40.0 or later.
- Appropriate RBAC permissions: Contributor or Security Admin.
- AKS cluster supported by Defender for Containers. See the [support matrix](support-matrix-defender-for-containers).
- [An OpenId Connect (OIDC) issuer](/en-us/azure/aks/use-oidc-issuer) enabled on your cluster.

## Network requirements

The Defender sensor must connect to Microsoft Defender for Cloud to send security data and events. Make sure that the required endpoints are configured for outbound access.

### Connection requirements

The Defender sensor needs connectivity to:

- Microsoft Defender for Cloud (for sending security data and events)

By default, AKS clusters have unrestricted outbound (egress) internet access.

For clusters with restricted egress, you must allow specific FQDNs for Microsoft Defender for Containers to function properly. See [Microsoft Defender for Containers - Required FQDN/application rules](/en-us/azure/aks/outbound-rules-control-egress#microsoft-defender-for-containers) in the AKS outbound network documentation for the required endpoints.

### Private link configuration

For instructions, see [Microsoft Security Private Link for Microsoft Defender for Cloud](concept-private-links).

## Deploy the Defender sensor

If you enabled automatic provisioning when you turned on the Defender for Containers plan, the Defender sensor might already be installed. Before you run the following command, [verify whether the deployment is already complete](defender-for-containers-verify-deployment).

1. Deploy the Defender sensor to a specific AKS cluster:

    ```azurecli
    az aks update \
      --resource-group <resource-group> \
      --name <aks-cluster-name> \
      --enable-defender
    ```
2. Enable Azure Policy for Kubernetes to assess and enforce configuration best practices:

    ```azurecli
    az aks enable-addons \
      --addons azure-policy \
      --name <aks-cluster-name> \
      --resource-group <resource-group>
    ```

# [Amazon Elastic Kubernetes Service (EKS)](#tab/eks)
## Prerequisites

- [Defender for Containers enabled on your AWS connector](defender-for-containers-enable-plan?tab=eks).
- Azure CLI version 2.40.0 or later.
- `kubectl` configured to access your EKS cluster.
- The EKS cluster is [connected to Azure Arc](/en-us/azure/azure-arc/kubernetes/quickstart-connect-cluster).

## Network requirements

Validate that the following endpoints for public cloud deployments are configured for outbound access. Configuring them for outbound access helps ensure that the Defender sensor can connect to Microsoft Defender for Cloud to send security data and events.

Note

The Azure domains `*.ods.opinsights.azure.com` and `*.oms.opinsights.azure.com` are no longer required for outbound access. For more information, see the [deprecation announcement](release-notes-archive#deprecation-notice-update-outbound-rules-for-microsoft-defender-for-containers).

| Azure domain | Azure Government domain | Azure operated by 21Vianet domain | Port |
| --- | --- | --- | --- |
| \*.cloud.defender.microsoft.com | N/A | N/A | 443 |

You also need to validate the [Azure Arc-enabled Kubernetes network requirements](/en-us/azure/azure-arc/kubernetes/network-requirements).

## Deploy the Defender sensor

For EKS clusters, you deploy Defender components as Azure Arc Kubernetes extensions when you manually deploy them by using Azure CLI.

If you enabled automatic provisioning when you turned on the Defender for Containers plan, the Defender sensor might already be installed. Before you run the following command, [verify whether the deployment is already complete](defender-for-containers-verify-deployment).

Run the following command to deploy the Defender sensor extension to your Arc-connected EKS cluster:

```azurecli
az k8s-extension create \
  --name microsoft.azuredefender.kubernetes \
  --extension-type microsoft.azuredefender.kubernetes \
  --cluster-type connectedClusters \
  --cluster-name <cluster-name> \
  --resource-group <resource-group> \
```

## Deploy the Azure Policy extension

Install the Azure Policy extension to enable policy-based security recommendations and compliance assessments for your EKS cluster:

```azurecli
az k8s-extension create \
  --name azurepolicy \
  --extension-type Microsoft.PolicyInsights \
  --cluster-type connectedClusters \
  --cluster-name <cluster-name> \
  --resource-group <resource-group>
```

# [Google Kubernetes Engine (GKE)](#tab/gke)
## Prerequisites

- [Defender for Containers enabled on your GCP connector](defender-for-containers-enable-plan?tab=gke).
- Azure CLI version 2.40.0 or later.
- `kubectl` configured to access your GKE cluster.
- The GKE cluster is [connected to Azure Arc](/en-us/azure/azure-arc/kubernetes/quickstart-connect-cluster).

## Network requirements

Validate that the following endpoints for public cloud deployments are configured for outbound access. Configuring them for outbound access helps ensure that the Defender sensor can connect to Microsoft Defender for Cloud to send security data and events.

Note

The Azure domains `*.ods.opinsights.azure.com` and `*.oms.opinsights.azure.com` are no longer required for outbound access. For more information, see the [deprecation announcement](release-notes-archive#deprecation-notice-update-outbound-rules-for-microsoft-defender-for-containers).

| Azure domain | Azure Government domain | Azure operated by 21Vianet domain | Port |
| --- | --- | --- | --- |
| \*.cloud.defender.microsoft.com | N/A | N/A | 443 |

You also need to validate the [Azure Arc-enabled Kubernetes network requirements](/en-us/azure/azure-arc/kubernetes/network-requirements).

### Private GKE clusters

Private GKE clusters must allow outbound HTTPS (TCP 443) access to Microsoft Defender for Cloud endpoints.

If your private cluster blocks outbound traffic, create a firewall rule to allow cluster nodes to reach Microsoft Defender for Cloud endpoints over TCP 443:

```bash
gcloud compute firewall-rules create allow-azure-defender \
    --allow tcp:443 \
    --source-ranges <cluster-cidr> \
    --target-tags <node-tags>
```

## Cluster-specific considerations

Review the following considerations based on your GKE cluster type before deploying the Defender sensor.

### Standard GKE clusters

No special configuration is required. Follow the deployment steps in the Deploy the Defender sensor and Deploy the Azure Policy extension sections.

### GKE Autopilot clusters

For Autopilot clusters:

- The Defender sensor automatically adjusts resource requests.
- You don't need to configure resource limits.

Important

In GKE Autopilot clusters, you can't manually configure resource requests and limits for the Defender sensor. GKE Autopilot controls resource management and you can't override it.

## Deploy the Defender sensor

For GKE clusters, you deploy Defender components as Azure Arc Kubernetes extensions when you manually deploy them by using Azure CLI.

If you enabled automatic provisioning when you turned on the Defender for Containers plan, the Defender sensor might already be installed. Before you run the following command, [verify whether the deployment is already complete](defender-for-containers-verify-deployment).

Run the following command to install the Defender sensor extension on your Arc-connected GKE cluster:

```azurecli
az k8s-extension create \
  --name microsoft.azuredefender.kubernetes \
  --extension-type microsoft.azuredefender.kubernetes \
  --cluster-type connectedClusters \
  --cluster-name <cluster-name> \
  --resource-group <resource-group> \
```

## Deploy the Azure Policy extension

Install the Azure Policy extension on your Arc-connected GKE cluster to enable policy-based security recommendations and compliance assessments:

```azurecli
az k8s-extension create \
  --name azurepolicy \
  --extension-type Microsoft.PolicyInsights \
  --cluster-type connectedClusters \
  --cluster-name <cluster-name> \
  --resource-group <resource-group>
```

# [Arc-enabled Kubernetes](#tab/arc)
## Prerequisites

- [Defender for Containers enabled on your Azure subscription](defender-for-containers-enable-plan?tab=aks).
- Azure CLI version 2.40.0 or later.
- `kubectl` configured to access your Arc-enabled Kubernetes cluster.
- The cluster is [connected to Azure Arc](/en-us/azure/azure-arc/kubernetes/quickstart-connect-cluster).

## Network requirements

Validate that the following endpoints for public cloud deployments are configured for outbound access. Configuring them for outbound access helps ensure that the Defender sensor can connect to Microsoft Defender for Cloud to send security data and events.

Note

The Azure domains `*.ods.opinsights.azure.com` and `*.oms.opinsights.azure.com` are no longer required for outbound access. For more information, see the [deprecation announcement](release-notes-archive#deprecation-notice-update-outbound-rules-for-microsoft-defender-for-containers).

| Azure domain | Azure Government domain | Azure operated by 21Vianet domain | Port |
| --- | --- | --- | --- |
| \*.cloud.defender.microsoft.com | N/A | N/A | 443 |

You also need to validate the [Azure Arc-enabled Kubernetes network requirements](/en-us/azure/azure-arc/kubernetes/network-requirements).

## Deploy the Defender sensor

For Arc-enabled Kubernetes clusters, Defender components are deployed as Azure Arc Kubernetes extensions.

If you enabled automatic provisioning when you turned on the Defender for Containers plan, the Defender sensor might already be installed. Before you run the following command, [verify whether the deployment is already complete](defender-for-containers-verify-deployment).

Run the following command to install the Defender sensor extension on your Arc-enabled Kubernetes cluster:

```azurecli
az k8s-extension create \
  --name microsoft.azuredefender.kubernetes \
  --extension-type microsoft.azuredefender.kubernetes \
  --cluster-type connectedClusters \
  --cluster-name <cluster-name> \
  --resource-group <resource-group> \
```

## Deploy the Azure Policy extension

Install the Azure Policy extension on your Arc-enabled Kubernetes cluster to enable policy-based security recommendations and compliance assessments:

```azurecli
az k8s-extension create \
  --name azurepolicy \
  --extension-type Microsoft.PolicyInsights \
  --cluster-type connectedClusters \
  --cluster-name <cluster-name> \
  --resource-group <resource-group>
```

---