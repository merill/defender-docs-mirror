---
layout: Conceptual
title: Deploy Defender for Containers to private clusters (Preview) - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-containers-private-clusters
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
description: Learn how to deploy Microsoft Defender for Containers to private clusters by using preview Helm charts and the Azure Arc Preview release train.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: cc9e18e9-cd34-9519-d042-09a1b40133a3
document_version_independent_id: 753129c2-cb35-d2cc-86af-2a2d80b0cb29
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-containers-private-clusters.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-containers-private-clusters
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-containers-private-clusters.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/beac614b-f66d-40ed-a947-3996de709333
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/9da05372-4706-43ec-a899-f436adab380d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 93b0084d-c6e8-100b-3616-6556969c1725
---

# Deploy Defender for Containers to private clusters (Preview) - Microsoft Defender for Cloud | Microsoft Learn

This article explains how to deploy Microsoft Defender for Containers to private Kubernetes clusters by using Helm charts or an Azure Arc-enabled Kubernetes extension. Private clusters isolate Kubernetes environments from the internet, which means no direct access to the Kubernetes API server. Defender for Containers extends threat detection and security visibility to these environments, so you can maintain protection coverage while preserving private cluster network boundaries. Before you begin, review the prerequisites.

## Prerequisites

Before you begin, ensure the following prerequisites are met:

- Defender for Containers is enabled for your target environment.
- If you're deploying by using **Helm**, make sure [`helm`](https://helm.sh/docs/intro/install/), `curl`, and [`jq`](https://jqlang.org/download/) are installed and available in your command-line environment.

    To check whether the tools are available, run:

    ```bash
    helm version
    curl --version
    jq --version
    ```
- If you're deploying by using an **Azure Arc-enabled Kubernetes extension**, ensure that:

    - Your cluster [connected to Azure Arc](/en-us/azure/azure-arc/kubernetes/quickstart-connect-cluster).
    - The Azure command-line interface (Azure CLI) is installed and you're signed in.

## Install components for private clusters

Defender for Containers Helm charts are published to `mcr.microsoft.com/azuredefender/microsoft-defender-for-containers`. Private clusters are supported in 0.11.X chart versions. Use the **Helm on Amazon EKS**, **Helm on Google Kubernetes Engine**, or **Azure Arc-enabled Kubernetes** tab to install the components for your environment.

# [Helm on Amazon EKS](#tab/helm-eks)
You can list the published versions by running the following command:

```bash
curl https://mcr.microsoft.com/v2/azuredefender/microsoft-defender-for-containers/tags/list
```

To install the latest `0.11.X` chart and enable private cluster components:

```bash
helm install defender-k8s oci://mcr.microsoft.com/azuredefender/microsoft-defender-for-containers \
  --create-namespace \
  --namespace mdc \
  --set global.cloudIdentifiers.AWS.accountId="<aws-account-id>" \
  --set global.cloudIdentifiers.AWS.region="<cluster-location>" \
  --set global.cloudIdentifiers.AWS.clusterName="<cluster-name>" \
  --set microsoft-defender-for-containers-sensor.inventoryCollector.enabled=true \
  --set microsoft-defender-for-containers-sensor.configController.enabled=true
```

# [Helm on Google Kubernetes Engine](#tab/helm-gke)
You can list the published versions by running the following command:

```bash
curl https://mcr.microsoft.com/v2/azuredefender/microsoft-defender-for-containers/tags/list
```

To install the latest `0.11.X` chart and enable private cluster components:

```bash
helm install defender-k8s oci://mcr.microsoft.com/azuredefender/microsoft-defender-for-containers \
  --create-namespace \
  --namespace mdc \
  --set global.cloudIdentifiers.GCP.projectId="<gcp-project-id>" \
  --set global.cloudIdentifiers.GCP.location="<cluster-location>" \
  --set global.cloudIdentifiers.GCP.clusterName="<cluster-name>" \
  --set microsoft-defender-for-containers-sensor.inventoryCollector.enabled=true \
  --set microsoft-defender-for-containers-sensor.configController.enabled=true
```

# [Azure Arc-enabled Kubernetes](#tab/arc)
To install the Defender extension and enable private cluster components:

```azurecli
az k8s-extension create \
  --name microsoft.azuredefender.kubernetes \
  --cluster-type connectedClusters \
  --cluster-name $ARC_CLUSTER_NAME \
  --resource-group $ARC_RESOURCE_GROUP \
  --extension-type microsoft.azuredefender.kubernetes \
  --configuration-settings inventoryCollector.enabled='true' \
  --configuration-settings configController.enabled='true'
```

---

## Verify the deployment

To verify Helm-based deployment status:

```bash
helm list --namespace mdc
```

To verify the Azure Arc extension deployment:

```azurecli
az k8s-extension show \
  --name microsoft.azuredefender.kubernetes \
  --cluster-type connectedClusters \
  --cluster-name $ARC_CLUSTER_NAME \
  --resource-group $ARC_RESOURCE_GROUP
```