---
layout: Conceptual
title: Install Defender for Containers Sensor Using Helm - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/deploy-helm
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
description: Install the Defender for Containers sensor on AKS, EKS, and GKE clusters by using Helm, including prerequisites, deployment steps, and upgrade guidance.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 2a59635f-5a43-2f6f-5cdb-15329a23d987
document_version_independent_id: 76684fcd-d989-86d5-69a2-973e6a76a69b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/deploy-helm.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/deploy-helm
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/deploy-helm.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d44a5346-5de4-439c-b804-7b2a536cbb55
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/da41a22b-b7a0-42d3-9c35-50da1c2b7b87
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: b4170601-7d4a-5508-90a6-0d0216b35fd6
---

# Install Defender for Containers Sensor Using Helm - Microsoft Defender for Cloud | Microsoft Learn

To control deployment and upgrade timing across your Azure Kubernetes Service (AKS), Amazon Elastic Kubernetes Service (EKS), and Google Kubernetes Engine (GKE) clusters, install and configure the Defender for Containers sensor by using Helm. Before you begin, ensure you meet the prerequisites.

Defender for Containers supports multiple sensor deployment models, including automatic provisioning and Helm-based installation. Helm-based deployment gives you more control over versioning and upgrade timing, but you manage some of the operational work. When you use Helm-based deployment, consider:

- **Sensor upgrades**: By using Helm-based deployment, you manage sensor upgrades and timing. Automatic provisioning follows Microsoft-managed rollout schedules.
- **Automatic installation flows**: When you deploy the sensor by using Helm, skip automatic prompts and recommendations in the Azure portal to avoid conflicts with the existing deployment.

## Prerequisites

Before you install the sensor by using Helm, complete the following prerequisites:

- Install and make available in your command-line environment [`helm`](https://helm.sh/docs/intro/install/) and `curl`.

    To confirm that Helm and curl are installed and available before you deploy Defender for Containers, run the following commands:

    ```bash
    helm version
    curl --version
    ```
- Implement all prerequisite requirements for the Defender for Containers sensor as described in the [Defender sensor network requirements](defender-for-containers-enable?tabs=aks-deploy-portal,k8s-deploy-asc,k8s-verify-asc,k8s-remove-arc,aks-removeprofile-api&amp;pivots=defender-for-container-aks#network-requirements).
- Enable Defender for Containers in the target subscription or security connector:

    - Azure subscription: [Enable Defender for Containers on AKS by using the Azure portal](defender-for-containers-azure-enable-portal)
    - Amazon Web Services (AWS): [Enable Defender for Containers on AWS (EKS) by using the Azure portal](defender-for-containers-aws-enable-portal)
    - Google Cloud Platform (GCP): [Enable Defender for Containers on GCP (GKE) by using the Azure portal](defender-for-containers-gcp-enable-portal)
    - Arc-enabled Kubernetes: [Enable Defender for Containers on Arc-enabled Kubernetes by using the Azure portal](defender-for-containers-arc-enable-portal)
- Enable the following components of the Defender for Containers plan:

    - Defender sensor
    - Kubernetes API access
- For Amazon Web Services (AWS) and Google Cloud Platform (GCP) environments, clear **Auto provision Defender's sensor for Azure Arc**.

    If you want to keep automatic provisioning enabled for other Arc-enabled clusters in the AWS account or GCP project, apply the `ms_defender_e2e_discovery_exclude=true` tag to clusters where you intend to deploy the sensor by using Helm.
- Ensure your environment doesn't have conflicting policy assignments that can deploy the generally available sensor version.

    Review policy assignments that use the following policy definition ID, and remove any conflicting assignments:

    `64def556-fbad-4622-930e-72d1d5589bf5`

    To review policy definitions, go to [Policy definitions in the Azure portal](https://ms.portal.azure.com/#view/Microsoft_Azure_Policy/PolicyMenuBlade/%7E/Definitions), and search for the policy definition ID.

## Install the Helm chart

Defender for Containers Helm charts are published to `mcr.microsoft.com/azuredefender/microsoft-defender-for-containers`.

The chart requires cluster identifier values under `global.cloudIdentifiers`. You can provide these values inline with `--set`, as shown in the following examples, or by using a values file.

To install the latest chart version, use the base Helm install command. Provide the required `global.cloudIdentifiers` values by using a values file or inline with `--set`, as shown in the environment-specific examples:

```bash
helm install defender-k8s oci://mcr.microsoft.com/azuredefender/microsoft-defender-for-containers
```

You can list the published versions by running the following command:

```bash
curl https://mcr.microsoft.com/v2/azuredefender/microsoft-defender-for-containers/tags/list
```

To install a specific version, include the version tag:

```bash
helm install defender-k8s oci://mcr.microsoft.com/azuredefender/microsoft-defender-for-containers:<tag>
```

To inspect configurable chart values, such as feature flags or pod resource limits, pull the chart and review the `values.yaml` file:

```bash
helm pull oci://mcr.microsoft.com/azuredefender/microsoft-defender-for-containers
```

To install the sensor for your environment:

# [AKS](#tab/aks)
For standard AKS clusters, use the `mdc` namespace.

For AKS Automatic clusters, use the `kube-system` namespace.

If your AKS cluster already has an existing Defender for Containers deployment, disable the existing deployment as described in [Configure Defender for Containers for Azure](/en-us/azure/defender-for-cloud/defender-for-containers-azure-configure), and remove any leftover resources by running the following commands:

```bash
kubectl delete crd/policies.defender.microsoft.com || true
kubectl delete crd/policytemplates.defender.microsoft.com || true
kubectl delete crd/runtimepolicies.defender.microsoft.com || true
kubectl delete crd/securityartifactpolicies.defender.microsoft.com || true
kubectl delete ClusterRole defender-admission-controller-cluster-role || true
kubectl delete ClusterRole defender-admission-controller-resource-cluster-role || true
kubectl delete ClusterRoleBinding defender-admission-controller-cluster-role-binding || true
kubectl delete ClusterRoleBinding defender-admission-controller-cluster-resource-role-binding || true
```

Install the sensor:

```bash
helm install defender-k8s oci://mcr.microsoft.com/azuredefender/microsoft-defender-for-containers \
    --create-namespace --namespace <namespace> \
    --set global.cloudIdentifiers.Azure.subscriptionId="<cluster-subscription-id>" \
    --set global.cloudIdentifiers.Azure.resourceGroupName="<cluster-resource-group>" \
    --set global.cloudIdentifiers.Azure.clusterName="<cluster-name>" \
    --set global.cloudIdentifiers.Azure.region="<cluster-region>"
```

Replace `<namespace>` with:

- `mdc` for standard AKS clusters.
- `kube-system` for AKS Automatic clusters.

# [EKS](#tab/eks)
Install the sensor:

```bash
helm install defender-k8s oci://mcr.microsoft.com/azuredefender/microsoft-defender-for-containers \
    --create-namespace --namespace mdc \
    --set global.cloudIdentifiers.AWS.accountId="<aws-account-id>" \
    --set global.cloudIdentifiers.AWS.region="<cluster-region>" \
    --set global.cloudIdentifiers.AWS.clusterName="<cluster-name>"
```

# [GKE](#tab/gke)
Install the sensor:

```bash
helm install defender-k8s oci://mcr.microsoft.com/azuredefender/microsoft-defender-for-containers \
    --create-namespace --namespace mdc \
    --set global.cloudIdentifiers.GCP.projectId="<gcp-project-id>" \
    --set global.cloudIdentifiers.GCP.location="<cluster-location>" \
    --set global.cloudIdentifiers.GCP.clusterName="<cluster-name>"
```

---

## Verify the installation

Verify the installation by using the same namespace you used to install the chart.

# [Standard AKS, EKS, and GKE](#tab/standard)
```bash
helm list --namespace mdc
```

# [AKS Automatic](#tab/aks-automatic)
```bash
helm list --namespace kube-system
```

---

If the `STATUS` field shows `deployed`, the installation succeeded.

## Configure security rules for gated deployment

Note

Kubernetes gated deployment is supported on AKS Automatic clusters only when the sensor is installed by using Helm in the `kube-system` namespace. Add-on deployment isn't supported for this scenario.

Important

When you create rules, the selected subscription might show as `not supported for Gated deployment`. This status occurs because you installed the Defender for Containers components by using Helm rather than through the dashboard's automatic installation.

Define security rules to control what you can deploy into your Kubernetes clusters. These rules can block or audit container images that don't meet your security criteria.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Defender for Cloud** &gt; **Environment settings**.
3. Select **Security rules**.
4. Select **Gated deployment** &gt; **Vulnerability assessment**.
5. Select a rule to edit it, or select **+ Add rule** to create a new one.

## Handle existing recommendations

Important

If you install the sensor by using Helm, don't use existing Defender for Cloud recommendations to install the Defender profile or Arc extension for the same cluster. Remediating these recommendations can create a conflicting deployment.

Depending on your deployment type, the following recommendations might still appear in Defender for Cloud. Review them to confirm they refer to automatic deployment flows, and then ignore them for clusters where you deployed with Helm.

- **Azure**: [Azure Kubernetes Service clusters should have Defender profile enabled - Microsoft Azure](https://ms.portal.azure.com/#view/Microsoft_Azure_Security/GenericRecommendationDetailsBlade/assessmentKey/56a83a6e-c417-42ec-b567-1e6fcb3d09a9/showSecurityCenterCommandBar%7E/false)

    [![Screenshot of the Azure portal that shows the Defender profile recommendation for AKS.](media/deploy-helm/recommendation-aks.png)](media/deploy-helm/recommendation-aks.png#lightbox)
- **Arc-enabled Kubernetes clusters**: [Azure Arc-enabled Kubernetes clusters should have the Defender extension installed - Microsoft Azure](https://ms.portal.azure.com/#view/Microsoft_Azure_Security/GenericRecommendationDetailsBlade/assessmentKey/3ef9848c-c2c8-4ff3-8b9c-4c8eb8ddfce6/showSecurityCenterCommandBar%7E/false)

    [![Screenshot of the Azure portal that shows the Defender extension recommendation for Arc-enabled Kubernetes clusters.](media/deploy-helm/recommendation-arc.png)](media/deploy-helm/recommendation-arc.png#lightbox)

## Upgrade an existing Helm-based deployment

With a Helm-based deployment, you manage sensor upgrades. Defender for Cloud doesn't automatically apply them.

Run the following command to update an existing Helm-based deployment. Use the namespace you used during installation.

```bash
helm upgrade defender-k8s \
    oci://mcr.microsoft.com/azuredefender/microsoft-defender-for-containers \
    --namespace <namespace> \
    --reuse-values
```

Replace `<namespace>` with the namespace you used during installation.

The `--reuse-values` parameter keeps your existing custom values during the upgrade.

For `<namespace>`, use:

- `mdc` for standard AKS, EKS, and GKE clusters.
- `kube-system` for AKS Automatic clusters.

If the upgrade fails because of resource conflicts, add the following options to the upgrade command:

```bash
--server-side=true --resolve-conflicts
```