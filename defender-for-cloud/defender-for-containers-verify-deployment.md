---
layout: Conceptual
title: Verify Defender for Containers deployment - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-containers-verify-deployment
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
description: Learn how to verify that Microsoft Defender for Containers sensors and extensions are running correctly on Kubernetes clusters.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 7b0051e9-7154-ced4-0e6f-a99196573a6c
document_version_independent_id: caabf599-7b66-043b-0f35-864d79112be9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-containers-verify-deployment.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-containers-verify-deployment
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-containers-verify-deployment.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/eea02214-631d-404a-92d1-5a3357c32a26
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/f42c31d7-eed9-43b7-9757-54caffb53cdc
platformId: 2b06b60f-349f-f15e-c452-a8a76e50ba73
---

# Verify Defender for Containers deployment - Microsoft Defender for Cloud | Microsoft Learn

After deploying Microsoft Defender for Containers components, verify that the sensor and related extensions are running correctly on your cluster.

## Verify recommendation health

If you deployed Defender components by remediating a security recommendation:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Recommendations**.
3. Locate the relevant recommendation.
4. Confirm that the recommendation status changes to **Healthy**.

## Verify Defender sensor deployment

To verify that the Defender sensor is enabled:

**For AKS clusters:**

```azurecli
az aks show \
  --name <aks-cluster-name> \
  --resource-group <resource-group> \
  --query "securityProfile.defender.securityMonitoring.enabled"
```

The output should be `true`.

**For Arc-enabled clusters and Helm:**

```azurecli
az k8s-extension list \
  --cluster-name <cluster-name> \
  --resource-group <resource-group> \
  --cluster-type connectedClusters \
  --subscription <subscription-id> \
  --query "[?extensionType=='microsoft.azuredefender.kubernetes' && provisioningState=='Succeeded']"
```

The command should return a non-empty array if the extension was installed successfully.

## Verify Azure Policy add-on on AKS

To verify that the Azure Policy add-on is enabled:

```azurecli
az aks show \
  --name <aks-cluster-name> \
  --resource-group <resource-group> \
  --query addonProfiles.azurepolicy
```

The output should show `enabled: true`.

## Verify extension installation for Arc-enabled clusters

For Amazon EKS, Google Kubernetes Engine (GKE), and Arc-enabled Kubernetes clusters, Defender components are installed as Azure Arc Kubernetes extensions.

To verify extension installation:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Azure Arc** &gt; **Kubernetes clusters**.
3. Select your Arc-enabled Kubernetes cluster.
4. In the cluster resource, select **Extensions**.
5. Confirm that the following extensions show **Succeeded**:

    - **Microsoft Defender for Containers**
    - **Azure Policy for Kubernetes** (if enabled)

You can also select the **Microsoft Defender for Containers** extension to view its status and configuration details.

## Verify Defender sensor pods

Verify that the Defender sensor pods are running in the cluster.

**For AKS clusters:**

```bash
kubectl get pods -n kube-system -l app=defender
```

**For Arc-enabled clusters and Helm:**

```bash
kubectl get pods -n mdc -l app=defender-k8s-sensor
```

Confirm that the Defender sensor pods are in a `Running` state.

## Verify the Defender DaemonSet (Arc-enabled clusters and Helm)

For Arc-enabled clusters and Helm deployments, the Defender collectors run as a Kubernetes DaemonSet, which ensures a pod is scheduled on each node. You can verify that the DaemonSet is deployed correctly:

```bash
kubectl get ds -n mdc microsoft-defender-collectors-ds
```

Confirm that the **DESIRED**, **CURRENT**, and **READY** values match the number of cluster nodes.