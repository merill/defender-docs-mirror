---
layout: Conceptual
title: Disable and remove Defender for Containers - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-containers-remove
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
description: Learn how to disable Microsoft Defender for Containers and remove its components for Kubernetes environments running on Azure, AWS, and Google Cloud.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: c5a4aa98-d71f-a1bb-c116-80433893077f
document_version_independent_id: 163c3f60-09cf-232f-a6c6-0842e341b091
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-containers-remove.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-containers-remove
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-containers-remove.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d44a5346-5de4-439c-b804-7b2a536cbb55
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/eea02214-631d-404a-92d1-5a3357c32a26
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/da41a22b-b7a0-42d3-9c35-50da1c2b7b87
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/f42c31d7-eed9-43b7-9757-54caffb53cdc
platformId: bbbf6fef-51e3-cb15-ca19-7b687a88e368
---

# Disable and remove Defender for Containers - Microsoft Defender for Cloud | Microsoft Learn

This article explains how to disable Microsoft Defender for Containers and remove its components by environment.

Turning off the Defender for Containers plan or disabling automatic provisioning stops future deployments, but doesn't uninstall Defender components that are already deployed to clusters. Defender components already deployed to clusters are removed separately.

Important

Removing Defender for Containers stops protection for your clusters. Make sure you have alternative security measures in place before you proceed.

Important

Disabling the plan doesn't delete historical security data stored in Microsoft Defender for Cloud or Log Analytics workspaces.

# [Azure Kubernetes Service (AKS)](#tab/aks)
## What stops working after removal

After you remove Defender for Containers components from an AKS cluster:

- Runtime threat detection based on Defender sensor telemetry stops.
- Kubernetes security recommendations related to Azure Policy for Kubernetes stop updating.
- Alerts based on AKS runtime signals and Kubernetes audit data stop being generated.
- New container image vulnerability findings for images in Azure Container Registry (ACR) are no longer generated for this environment.

## Disable Defender for Containers plan

To disable the Defender for Containers plan for the subscription that contains your AKS clusters:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the subscription that contains your AKS clusters.
4. In the Defender plans page, toggle **Containers** to **Off**.
5. Select **Save**.

## Remove Defender extensions from AKS clusters

After disabling the plan, remove the Defender-related components from each AKS cluster.

### Remove the Defender for Containers profile from the AKS cluster

Run the following command to remove the Defender for Containers profile from the AKS cluster:

```azurecli
az aks update \
  --name <cluster-name> \
  --resource-group <resource-group> \
  --disable-defender
```

### Disable Azure Policy add-on

If Azure Policy was enabled for this cluster, run the following command to disable the add-on:

```azurecli
az aks disable-addons \
  --addons azure-policy \
  --name <cluster-name> \
  --resource-group <resource-group>
```

## Verify removal

Use the following checks to confirm that Defender for Containers has been fully removed from your AKS cluster.

### Check AKS cluster pods

Run the following command to check all namespaces for remaining Defender pods and confirm that the uninstall completed successfully:

```bash
kubectl get pods -A | grep defender
```

No resources should be returned.

### Verify plan status

Run the following command to confirm that the Containers plan is disabled for the subscription:

```azurecli
az security pricing show --name 'Containers'
```

The output should show `pricingTier` as `Free`.

# [Amazon Elastic Kubernetes Service (EKS)](#tab/eks)
## What stops working after removal

After you remove Defender for Containers components from an EKS cluster:

- Runtime threat detection from the Defender sensor deployed through Azure Arc stops.
- Kubernetes security recommendations for that cluster stop updating.
- Alerts based on Kubernetes runtime and audit signals stop being generated.
- Container image vulnerability findings for images in Amazon ECR stop updating for this environment.
- Agentless discovery and control plane–based detections stop if related AWS-side permissions and integrations are removed.

## Remove Defender extensions from EKS clusters

Defender for Containers deploys components to EKS clusters by using Azure Arc-enabled Kubernetes. The following steps remove those Arc extensions.

### Remove the Defender extension

Run the following command to remove the Defender extension from the connected EKS cluster:

```azurecli
az k8s-extension delete \
  --name microsoft.azuredefender.kubernetes \
  --cluster-type connectedClusters \
  --cluster-name <cluster-name> \
  --resource-group <resource-group> \
  --yes
```

### Remove the Azure Policy extension (if installed)

If the Azure Policy extension is installed on the EKS cluster, run the following command to remove it:

```azurecli
az k8s-extension delete \
  --name azurepolicy \
  --cluster-type connectedClusters \
  --cluster-name <cluster-name> \
  --resource-group <resource-group> \
  --yes
```

### Disconnect clusters from Azure Arc

Note

Disconnecting a cluster from Azure Arc removes access to all Arc extensions, not only Defender for Containers.

```azurecli
az connectedk8s delete \
  --name <cluster-name> \
  --resource-group <resource-group> \
  --yes
```

## Disable Defender for Containers plan on the AWS connector

To disable the Defender for Containers plan on the AWS connector:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the relevant AWS connector.
4. Select **Settings**.
5. Toggle **Containers** to **Off**.
6. Select **Save**.

## Delete the AWS connector (optional)

If you no longer want Defender for Cloud to monitor your AWS account:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Find your AWS connector.
4. Select the ellipsis (...).
5. Select **Delete**.
6. Confirm deletion.

## Remove AWS resources created for runtime protection (optional)

Remove the S3 bucket, SQS queue, and Kinesis Data Firehose delivery stream only if runtime threat protection for EKS was enabled and you no longer use Defender for Containers for that cluster.

- [Delete the S3 bucket created for the cluster](https://docs.aws.amazon.com/AmazonS3/latest/userguide/delete-bucket.html).
- [Delete the SQS queue created for the cluster](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/step-delete-queue.html).
- [Delete the Kinesis Data Firehose delivery stream created for the cluster](https://docs.aws.amazon.com/firehose/latest/APIReference/API_DeleteDeliveryStream.html).

Note

The S3 bucket, SQS queue, and Kinesis Data Firehose delivery stream are created per cluster. If you remove them while runtime protection is still enabled, data collection can stop.

## Remove AWS IAM roles and identity providers (optional)

If you are completely offboarding your AWS account from Microsoft Defender for Cloud, you can manually delete the IAM roles and identity providers that were created during onboarding.

Use the AWS console or CLI to delete the following roles if they exist:

- `MDCContainersImageAssessmentRole`
- `MDCContainersK8sRole`
- `MDCContainersK8sDataCollectionRole`
- `MDCContainersK8sCloudWatchToKinesisRole`
- `MDCContainersK8sKinesisToS3RoleName`
- `MDCContainersAgentlessDiscoveryK8sRole`

Warning

Only delete the `ASCDefendersOIDCIdentityProvider` OpenID Connect provider if you are removing **all** Defender for Cloud components from this AWS account. Deleting this shared component will affect other Defender for Cloud plans.

## Verify removal

### Check Azure Arc extensions

Run the following command to list the installed Arc extensions for your cluster and confirm that the Defender extension is no longer present:

```azurecli
az k8s-extension list \
  --cluster-type connectedClusters \
  --cluster-name <cluster-name> \
  --resource-group <resource-group>
```

Confirm that `microsoft.azuredefender.kubernetes` is not listed.

### Check EKS cluster pods

Run the following command to verify that no Defender pods remain in the `mdc` namespace on your EKS cluster:

```bash
kubectl get pods -n mdc
```

No resources should be returned.

# [Google Kubernetes Engine (GKE)](#tab/gke)
## What stops working after removal

After you remove Defender for Containers components from a GKE cluster:

- Runtime threat detection from the Defender sensor deployed through Azure Arc stops.
- Kubernetes security recommendations for that cluster stop updating.
- Alerts based on Kubernetes runtime and audit signals stop being generated.
- Container image vulnerability findings for images in Google Container Registry or Artifact Registry stop updating for this environment.

## Remove Defender extensions from GKE clusters

Use the following steps to remove Defender-related extensions from the GKE cluster.

### Remove the Defender extension

Run the following command to delete the Microsoft Defender for Containers extension from your Arc-connected GKE cluster:

```azurecli
az k8s-extension delete \
  --name microsoft.azuredefender.kubernetes \
  --cluster-type connectedClusters \
  --cluster-name <cluster-name> \
  --resource-group <resource-group> \
  --yes
```

### Remove the Azure Policy extension (if installed)

Azure Policy is installed as a separate Arc extension on the cluster. If it was deployed, delete it to fully remove Defender-related cluster integrations:

```azurecli
az k8s-extension delete \
  --name azurepolicy \
  --cluster-type connectedClusters \
  --cluster-name <cluster-name> \
  --resource-group <resource-group> \
  --yes
```

### Disconnect GKE clusters from Azure Arc

Note

Disconnecting a cluster from Azure Arc removes access to all Arc extensions, not only Defender for Containers.

```azurecli
az connectedk8s delete \
  --name <cluster-name> \
  --resource-group <resource-group> \
  --yes
```

## Disable Defender for Containers plan on the GCP connector

To disable the Defender for Containers plan for the GCP connector:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the relevant GCP connector.
4. Select **Settings**.
5. Toggle **Containers** to **Off**.
6. Select **Save**.

## Delete the GCP connector (optional)

If you no longer need the GCP connector, use the following steps to delete it:

1. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
2. Find your GCP connector.
3. Select the **...** (more options) menu.
4. Select **Delete**.
5. Confirm deletion.

## Remove GCP resources created for runtime protection (optional)

Remove the Pub/Sub topic and subscription and the Cloud Logging sink only if runtime threat protection for GKE was enabled and you no longer use Defender for Containers for that project.

- Delete the Pub/Sub topic and subscription that use the `MicrosoftDefender-` prefix.
- Delete the Cloud Logging sink that was created for Defender for Containers.

## Remove GCP service accounts and roles (optional)

If you are completely offboarding your GCP project from Microsoft Defender for Cloud, you can manually delete the service accounts and roles created during onboarding.

Use the Google Cloud console or gcloud CLI to delete the following service accounts:

- `ms-defender-containers`
- `ms-defender-containers-stream`
- `mdc-containers-k8s-operator`
- `mdc-containers-artifact-assess`

Delete the following custom roles:

- `MicrosoftDefenderContainersDataCollectionRole`
- `MicrosoftDefenderContainersRole`
- `MDCGkeClusterWriteRole`

Warning

Only delete the `containers` and `containers-streams` OIDC workload identity pool providers if you are removing **all** Defender for Cloud components. The `containers` and `containers-streams` providers are shared components. Additionally, ensure no other non-Defender services are using the `logging.googleapis.com` API before disabling it.

## Verify removal

### Check Azure Arc extensions

Run the following command to confirm that the Defender extension is no longer installed on the GKE cluster:

```azurecli
az k8s-extension list \
  --cluster-type connectedClusters \
  --cluster-name <cluster-name> \
  --resource-group <resource-group>
```

Confirm that `microsoft.azuredefender.kubernetes` is not listed.

### Check GKE cluster pods

Run the following command to verify that the `mdc` namespace no longer contains any Defender pods on your GKE cluster:

```bash
kubectl get pods -n mdc
```

No resources should be returned.

### Check Azure portal

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Verify the GCP connector is removed or shows **Containers** as disabled.
4. Check that no GKE-related recommendations appear.

# [Arc-enabled Kubernetes](#tab/arc)
## What stops working after removal

After you remove Defender for Containers components from an Arc-enabled Kubernetes cluster:

- Runtime threat detection from the Defender sensor stops.
- Kubernetes security recommendations for that cluster stop updating.
- Alerts based on Kubernetes runtime and audit signals stop being generated.
- Azure Policy–based configuration assessments for Kubernetes workloads stop if the Azure Policy extension is removed.

## Disable Defender for Containers plan

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the subscription that contains your Arc-enabled Kubernetes clusters.
4. In the Defender plans page, toggle **Containers** to **Off**.
5. Select **Save**.

## Remove Defender extensions from Arc-enabled clusters

### Remove the Defender extension

```azurecli
az k8s-extension delete \
  --name microsoft.azuredefender.kubernetes \
  --cluster-type connectedClusters \
  --cluster-name <cluster-name> \
  --resource-group <resource-group> \
  --yes
```

### Remove the Azure Policy extension (if installed)

```azurecli
az k8s-extension delete \
  --name azurepolicy \
  --cluster-type connectedClusters \
  --cluster-name <cluster-name> \
  --resource-group <resource-group> \
  --yes
```

### Disconnect the cluster from Azure Arc (optional)

Note

Disconnecting a cluster from Azure Arc removes access to all Arc extensions, not only Defender for Containers.

```azurecli
az connectedk8s delete \
  --name <cluster-name> \
  --resource-group <resource-group> \
  --yes
```

## Verify removal

### Check Azure Arc extensions

```azurecli
az k8s-extension list \
  --cluster-type connectedClusters \
  --cluster-name <cluster-name> \
  --resource-group <resource-group>
```

Confirm that `microsoft.azuredefender.kubernetes` is not listed.

### Check Arc-enabled cluster pods

Run the following command to verify that no Defender pods remain in the `mdc` namespace on your Arc-enabled cluster:

```bash
kubectl get pods -n mdc
```

No resources should be returned.

---