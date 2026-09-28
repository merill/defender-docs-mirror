---
layout: Conceptual
title: Attack path analysis and enhanced risk-hunting for containers - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/how-to-test-attack-path-and-security-explorer-with-vulnerable-container-image
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
description: Learn how to test attack path analysis and explore container risks with Cloud Security Explorer by deploying a mock vulnerable container image in Microsoft Defender for Cloud
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 435bce66-dbd7-bce0-3cef-0207e12c1a90
document_version_independent_id: 3ab76f01-e030-3088-1d54-8e58624e6e22
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/how-to-test-attack-path-and-security-explorer-with-vulnerable-container-image.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/how-to-test-attack-path-and-security-explorer-with-vulnerable-container-image
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/how-to-test-attack-path-and-security-explorer-with-vulnerable-container-image.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d44a5346-5de4-439c-b804-7b2a536cbb55
- https://authoring-docs-microsoft.poolparty.biz/devrel/cb49e66a-8528-497d-adaa-eade2d009d1b
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/da41a22b-b7a0-42d3-9c35-50da1c2b7b87
- https://authoring-docs-microsoft.poolparty.biz/devrel/472c9d15-157b-443c-afa2-e209c8fecf58
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: f339dffd-4d13-b688-7f3e-233a99b9a174
---

# Attack path analysis and enhanced risk-hunting for containers - Microsoft Defender for Cloud | Microsoft Learn

Attack path analysis identifies potential paths that attackers could use to reach high-impact resources in your environment. It analyzes relationships between resources and highlights issues that can be remediated to reduce risk.

This article shows how to test attack path analysis by deploying a mock vulnerable container image.

# [Azure](#tab/azure)
## Prerequisites

Before you begin, make sure you have the following prerequisites:

- [Defender CSPM enabled for your subscription](tutorial-enable-cspm-plan).
- Access to an Azure Kubernetes Service (AKS) cluster.
- An Azure Container Registry (ACR) that the cluster can access.

## Test the attack path and security explorer using a mock vulnerable container image

1. Pull a base image (for example, alpine) to your local environment by running the following command:

    ```azurecli
       docker pull alpine
    ```
2. Tag the image with the following label and push it to your ACR. Replace `<MYACR>` with your Azure Container Registry name:

    ```azurecli
        docker tag alpine <MYACR>.azurecr.io/mdc-mock-0001
        docker push <MYACR>.azurecr.io/mdc-mock-0001
    ```
3. If you don't have an AKS (Azure Kubernetes Service) cluster, use the following command to create a new AKS cluster:

    ```azurecli
        az aks create -n myAKSCluster -g myResourceGroup --generate-ssh-keys --attach-acr $MYACR
    ```
4. If your AKS isn't attached to your ACR, use the following Cloud Shell command line to point your AKS instance to pull images from the selected ACR:

    ```azurecli
        az aks update -n myAKSCluster -g myResourceGroup --attach-acr <acr-name>
    ```
5. Authenticate your Cloud Shell session to work with the cluster

    ```azurecli
    az aks get-credentials  --subscription <cluster-suid> --resource-group <your-rg> --name <your-cluster-name>    
    ```
6. Install the [ngnix ingress Controller](https://docs.nginx.com/nginx-ingress-controller/installation/installing-nic/installation-with-helm/) :

    ```azurecli
    helm install ingress-controller oci://ghcr.io/nginxinc/charts/nginx-ingress --version 1.0.1
    ```
7. Deploy the mock vulnerable image to expose the vulnerable container to the internet by running the following command:

    ```azurecli
    helm install dcspmcharts  oci://mcr.microsoft.com/mdc/stable/dcspmcharts --version 1.0.0 --namespace mdc-dcspm-demo --create-namespace --set image=<your-image-uri> --set distribution=AZURE
    ```

### Verify deployment

1. Look for an entry with **mdc-dcspm-demo** as namespace.
2. Go to **Workloads** &gt; **Deployments**.
3. Verify `pod1` and `pod2` are created 3/3 and **ingress-controller-nginx-ingress-controller** is created 1/1.
4. Go to **Services and Ingresses**.
5. Verify that **service1** and **ingress-controller-nginx-ingress-controller** are listed.
6. Verify one **ingress** is created with an IP address and nginx class.

# [AWS](#tab/aws)
## Prerequisites

Before you begin, ensure you have the following prerequisites:

- [Defender CSPM enabled for your AWS account](tutorial-enable-cspm-plan).
- Access to an Amazon Elastic Kubernetes Service (EKS) cluster.
- An Amazon Elastic Container Registry (ECR) repository that the cluster can access.

## Test the attack path and security explorer using a mock vulnerable container image

1. Create an Amazon ECR repository named `mdc-mock-0001`.
2. In your AWS account, select **Command line or programmatic access**.
3. Select **Option 1: Set AWS environment variables (Short-term credentials)**.
4. Copy the values for the following credentials:

    - *AWS\_ACCESS\_KEY\_ID*
    - *AWS\_SECRET\_ACCESS\_KEY*
    - *AWS\_SESSION\_TOKEN*
5. Run the following command to get the authentication token for your Amazon ECR registry. Replace `<REGION>` with the region of your registry and `<ACCOUNT>` with your AWS account ID.

    ```awscli
    aws ecr get-login-password --region <REGION> | docker login --username AWS --password-stdin <ACCOUNT>.dkr.ecr.<REGION>.amazonaws.com
    ```
6. Create a Docker image that is tagged as vulnerable by name. The image name must include *mdc-mock-0001*.
7. Push the image to your ECR registry. Replace `<ACCOUNT>` and `<REGION>` with your AWS account ID and region.

    ```awscli
    docker pull alpine
    docker tag alpine <ACCOUNT>.dkr.ecr.<REGION>.amazonaws.com/mdc-mock-0001
    docker push <ACCOUNT>.dkr.ecr.<REGION>.amazonaws.com/mdc-mock-0001
    ```
8. Connect to your EKS cluster.
9. Configure `kubectl` to work with your EKS cluster. Replace `<your-region>` and `<your-cluster-name>` with your EKS cluster region and name.

    ```awscli
    aws eks --region <your-region> update-kubeconfig --name <your-cluster-name>
    ```
10. Check if `kubectl` is correctly configured by running:

    ```awscli
    kubectl get nodes
    ```
11. Install the [ngnix ingress Controller](https://docs.nginx.com/nginx-ingress-controller/installation/installing-nic/installation-with-helm/) :

    ```awscli
    helm install ingress-controller oci://ghcr.io/nginxinc/charts/nginx-ingress --version 1.0.1
    ```
12. Install the following Helm chart. The Helm chart deploys resources onto your cluster that you can use to infer attack paths. It also includes the vulnerable image.

    ```awscli
    helm install dcspmcharts oci://mcr.microsoft.com/mdc/stable/dcspmcharts --version 1.0.0 --namespace mdc-dcspm-demo --create-namespace --set image=<ACCOUNT>.dkr.ecr.<REGION>.amazonaws.com/mdc-mock-0001 --set distribution=AWS
    ```

# [GCP](#tab/gcp)
## Prerequisites

Before you begin, make sure the following prerequisites are met:

- [Defender CSPM enabled for your GCP project](tutorial-enable-cspm-plan).
- Access to a Google Kubernetes Engine (GKE) cluster.
- A Google Artifact Registry repository that the cluster can access.

## Test the attack path and security explorer using a mock vulnerable container image

1. Sign in to the GCP portal.
2. Search for **Artifact Registry**.
3. Create a GCP repository named *mdc-mock-0001*.
4. Follow the GCP documentation, [Push and pull images](https://cloud.google.com/artifact-registry/docs/docker/pushing-and-pulling), to push the image to your repository. Run these commands:

    ```docker
    docker pull alpine
    docker tag alpine <LOCATION>-docker.pkg.dev/<PROJECT_ID>/<REGISTRY>/<REPOSITORY>/mdc-mock-0001
    docker push <LOCATION>-docker.pkg.dev/<PROJECT_ID>/<REGISTRY>/<REPOSITORY>/mdc-mock-0001
    ```
5. Go to **Kubernetes Engine** &gt; **Clusters**.
6. Select the **Connect** button.
7. Run the following command in the Cloud Shell:

    ```gcloud
    gcloud container clusters get-credentials contra-bugbash-gcp --zone us-central1-c --project onboardingc-demo-gcp-1
    ```
8. Check if `kubectl` is correctly configured by running:

    ```gcloud
    kubectl get nodes
    ```
9. To install the Helm chart, follow these steps:

    1. Go to **Artifact registry** &gt; **Repository**.
    2. Search for the image URI under **Pull by digest**.
    3. Run the following command to install the Helm chart: The Helm chart deploys resources onto your cluster that you can use to infer attack paths. It also includes the vulnerable image.

        ```gcloud
        helm install dcspmcharts oci:/mcr.microsoft.com/mdc/stable/dcspmcharts --version 1.0.0 --namespace mdc-dcspm-demo --create-namespace --set image=<IMAGE_URI> --set distribution=GCP
        ```

---

Note

It can take up to 24 hours for results to appear in Attack path analysis and Cloud Security Explorer.

## View attack paths

After deploying the mock scenario, you can view the generated attack path in **Microsoft Defender for Cloud**:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Defender for Cloud** &gt; **Attack path analysis**.
3. Locate the attack path related to the deployed resources.

For more information, see [Identify and remediate attack paths](how-to-manage-attack-path).

## Investigate container risks with Cloud Security Explorer

After deploying the mock vulnerable image, you can use Cloud Security Explorer to identify related risks and explore how they contribute to attack paths.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Defender for Cloud** &gt; **Cloud Security Explorer**.

You can build queries in one of the following ways:

- [Use built-in query templates](how-to-manage-cloud-security-explorer#query-templates)
- [Create custom queries](how-to-manage-cloud-security-explorer#build-a-query)