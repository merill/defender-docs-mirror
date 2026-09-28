---
layout: Conceptual
title: Enable Defender for Containers in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-containers-enable-plan
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
description: Learn how to enable the Microsoft Defender for Containers plan in Microsoft Defender for Cloud for Azure subscriptions, AWS connectors, and GCP connectors.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: f8a127ed-e3c4-edd0-67de-fc0256bbc094
document_version_independent_id: df399772-6d81-77d4-59aa-f3710e803c5e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-containers-enable-plan.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-containers-enable-plan
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-containers-enable-plan.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/d44a5346-5de4-439c-b804-7b2a536cbb55
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/da41a22b-b7a0-42d3-9c35-50da1c2b7b87
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 509e7fe1-7041-d497-1469-83ed6d86f161
---

# Enable Defender for Containers in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

Enable the Microsoft Defender for Containers plan in Microsoft Defender for Cloud to protect your Kubernetes clusters and container workloads. This article walks you through enabling the plan in the Azure portal for Azure Kubernetes Service (AKS), Amazon Elastic Kubernetes Service (EKS), Google Kubernetes Engine (GKE), and Azure Arc-enabled Kubernetes clusters. When you enable the plan, you can configure protection components such as runtime threat detection, vulnerability scanning, and security posture assessments.

# [Azure Kubernetes Service (AKS)](#tab/aks)
## Prerequisites

Before you begin, make sure that:

- You have an AKS cluster. See the [Defender for Containers support matrix](support-matrix-defender-for-containers).
- You reviewed the [Defender for Containers feature access patterns](defender-for-containers-feature-access-patterns).
- You reviewed the required [Defender for Containers network access and permissions](defender-for-containers-network-access#microsoft-defender-for-cloud-to-kubernetes-clusters).

## Enable the Defender for Containers plan

To enable the Defender for Containers plan for your AKS clusters in the Azure portal:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the subscription where your AKS clusters are located.
4. On the Defender plans page, find the **Containers** row and toggle the status to **On**.
5. Select **Settings** in the Containers plan row.
6. Toggle **On** or **Off** the relevant Defender for Containers components:

    - **Agentless scanning for machines** Performs agentless vulnerability and secret scanning on Kubernetes nodes.

        - To exclude machines from agentless scanning, add the exclusion tag name and value.
    - **Defender sensor** Deploys the Defender sensor to cluster nodes to collect runtime security telemetry used for threat detection.

        - **Enable Defender Security Gating:** Adds an admission control layer that evaluates deployments against security policies before workloads run in the cluster.
        - **Enable Defender Runtime Anti Malware:** Enables runtime malware detection for Kubernetes hosts and containers and can optionally block malicious file execution in real time.
    - **Azure Policy** Deploys the Azure Policy for Kubernetes add-on to enable Kubernetes security posture assessments and related security recommendations.
    - **Kubernetes API access** Allows Defender for Cloud to access the Kubernetes API for cluster inventory, configuration analysis, and capabilities that rely on Kubernetes metadata.
    - **Registry access** Enables agentless vulnerability assessment for container images stored in connected registries.

        - **Security findings:** Generates findings and links them to container images when new images are pushed or existing images are updated.

            Note

            The **Security findings** component can't be enabled through Azure Policy. To enable it, toggle it on in the plan **Settings** page.

    [![Screenshot of the Settings and monitoring page for the Containers plan in Microsoft Defender for Cloud, showing available Defender for Containers components.](media/defender-for-containers-enable-plan/azure-defender-plans.png)](media/defender-for-containers-enable-plan/azure-defender-plans.png#lightbox)
7. Select **Continue**.
8. Select **Save**.

# [Amazon Elastic Kubernetes Service (EKS)](#tab/eks)
## Prerequisites

Before you begin, make sure that:

- You have an [AWS project onboarded to Microsoft Defender for Cloud](quickstart-onboard-aws).
- You have one or more Amazon EKS clusters running a supported Kubernetes version. See the [Defender for Containers support matrix](support-matrix-defender-for-containers).
- You reviewed the [Defender for Containers feature access patterns](defender-for-containers-feature-access-patterns).
- You reviewed the required [Defender for Containers network access and permissions](defender-for-containers-network-access#microsoft-defender-for-cloud-to-kubernetes-clusters).
- You reviewed the required [cloud IAM permissions](containers-permissions).

## Enable the Defender for Containers plan

To enable the Defender for Containers plan for your EKS clusters:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the relevant AWS connector.
4. On the Defender plans page, find the **Containers** row and toggle the status to **On**.
5. Select **Settings** in the Containers plan row.
6. Toggle **On** the relevant Defender for Containers components:

    - **Agentless threat protection** Collects Kubernetes control plane audit logs and analyzes them for control plane threat detections. Logs are routed through AWS services (such as CloudWatch, S3, Kinesis, and SQS).

        - If enabled, set the audit log retention period (in days) to control how long control plane audit logs are stored.
    - **Auto provision Defender's sensor for Azure Arc** Deploys the Defender sensor as an Azure Arc Kubernetes extension. The sensor runs as a DaemonSet on cluster nodes and provides runtime threat detection based on node and workload telemetry.

        Note

        When automatic provisioning is enabled, the Defender sensor is installed after the cluster is discovered and can take several hours to complete.
    - **Auto provision Azure Policy extension for Azure Arc** Deploys the Azure Policy extension to the cluster to enable Kubernetes security posture assessments and related security recommendations.
    - **Kubernetes API access** Allows Defender for Cloud to access the Kubernetes API server for cluster inventory, configuration analysis, and capabilities that rely on Kubernetes metadata and state.
    - **Registry access** Enables agentless vulnerability assessment for container images in Amazon ECR. Images pushed to ECR are scanned automatically (typically within 24 hours).

        - **Security findings:** Generates findings and links them to container images when new images are pushed or existing images are updated.

            Note

            The **Security findings** component can't be enabled through Azure Policy. To enable it, toggle it on in the plan **Settings** page.

    [![Screenshot of the Defender for Containers configuration pane for an AWS connector in Microsoft Defender for Cloud.](media/defender-for-containers-enable-plan/amazon-web-services-select-plans.png)](media/defender-for-containers-enable-plan/amazon-web-services-select-plans.png#lightbox)
7. Select **Save**.
8. Select **Next : Configure access &gt;**.
9. Regenerate the AWS CloudFormation template for the connector, and use it to [update the existing stack in AWS CloudFormation](quickstart-onboard-aws#update-the-cloudformation-template).

    [![Screenshot of the Configure access step for an AWS connector in Microsoft Defender for Cloud, showing the AWS CloudFormation deployment template.](media/defender-for-containers-enable-plan/amazon-web-services-configure-access.png)](media/defender-for-containers-enable-plan/amazon-web-services-configure-access.png#lightbox)
10. Select **Next: Review and generate &gt;**.
11. Select **Update**.

# [Google Kubernetes Engine (GKE)](#tab/gke)
## Prerequisites

Before you begin, make sure that:

- You have a [GCP project onboarded to Microsoft Defender for Cloud](quickstart-onboard-gcp).
- You have one or more Google Kubernetes Engine (GKE) clusters running a supported Kubernetes version. See the [Defender for Containers support matrix](support-matrix-defender-for-containers).
- You reviewed the [Defender for Containers feature access patterns](defender-for-containers-feature-access-patterns).
- You reviewed the required [Defender for Containers network access and permissions](defender-for-containers-network-access#microsoft-defender-for-cloud-to-kubernetes-clusters).
- You reviewed the required [cloud IAM permissions](containers-permissions).

## Enable the Defender for Containers plan

To enable the Defender for Containers plan for your GKE clusters:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the relevant GCP connector.
4. On the Defender plans page, find the **Containers** row and toggle the status to **On**.
5. Select **Settings** in the Containers plan row.
6. Toggle **On** the relevant Defender for Containers components:

    - **Agentless threat protection** Collects Kubernetes control plane audit logs and analyzes them for control plane threat detections. Logs are exported from GKE to your Google Cloud project.
    - **Auto provision Defender's sensor for Azure Arc** Deploys the Defender sensor as an Azure Arc Kubernetes extension. The sensor runs as a DaemonSet on cluster nodes and provides runtime threat detection based on node and workload telemetry.

        - **Enable Defender Security Gating** Adds an admission control layer that evaluates deployments against security policies before workloads run in the cluster.

        Note

        When automatic provisioning is enabled, the Defender sensor is installed after the cluster is discovered and can take several hours to complete.
    - **Auto provision Azure Policy extension for Azure Arc** Deploys the Azure Policy extension to the cluster to enable Kubernetes security posture assessments and related security recommendations.
    - **Kubernetes API access** Allows Defender for Cloud to access the Kubernetes API server for cluster inventory, configuration analysis, and capabilities that rely on Kubernetes metadata and cluster state.
    - **Registry access** Enables agentless vulnerability assessment for container images stored in Google Container Registry (GCR) and Artifact Registry.

        - **Security findings:** Generates findings and links them to container images when new images are pushed or existing images are updated.

            Note

            The **Security findings** component can't be enabled through Azure Policy. To enable it, toggle it on in the plan **Settings** page.

    [![Screenshot of the Defender for Containers configuration pane for a GCP connector in Microsoft Defender for Cloud.](media/defender-for-containers-enable-plan/google-cloud-platform-select-plans.png)](media/defender-for-containers-enable-plan/google-cloud-platform-select-plans.png#lightbox)
7. Select **Save**.
8. Select **Next : Configure access &gt;**.
9. Regenerate and rerun the onboarding script in your GCP project.

    [![Screenshot of the Configure access step for a GCP connector in Microsoft Defender for Cloud, showing the GCP Cloud Shell deployment script.](media/defender-for-containers-enable-plan/google-cloud-platform-configure-access.png)](media/defender-for-containers-enable-plan/google-cloud-platform-configure-access.png#lightbox)
10. Select **Next: Review and generate &gt;**.
11. Select **Update**.

# [Azure Arc-enabled Kubernetes](#tab/arc)
## Prerequisites

Before you begin, make sure that:

- Your cluster is:

    - [Connected to Azure Arc](/en-us/azure/azure-arc/kubernetes/quickstart-connect-cluster).
    - Supported by Defender for Containers. See the [Defender for Containers support matrix](support-matrix-defender-for-containers).
- You reviewed the [Defender for Containers feature access patterns](defender-for-containers-feature-access-patterns).
- You reviewed the required [network access and permissions](defender-for-containers-network-access#microsoft-defender-for-cloud-to-kubernetes-clusters).

## Enable the Defender for Containers plan

To enable the Defender for Containers plan for your Azure Arc-enabled Kubernetes clusters:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the **Azure subscription** that contains the Azure Arc-enabled Kubernetes cluster resource.
4. On the Defender plans page, find the **Containers** row and toggle the status to **On**.
5. Select **Settings** in the Containers plan row.
6. Toggle **On** the relevant Defender for Containers components:

    - **Agentless scanning for machines** Performs agentless vulnerability and secret scanning on Kubernetes nodes.
    - **Defender sensor** Deploys the Defender sensor to cluster nodes to collect runtime security telemetry used for threat detection.
    - **Azure Policy** Deploys the Azure Policy for Kubernetes add-on to enable Kubernetes security posture assessments and related security recommendations.
    - **Kubernetes API access** Allows Defender for Cloud to access the Kubernetes API for cluster inventory, configuration analysis, and capabilities that rely on Kubernetes metadata.
    - **Registry access** Enables agentless vulnerability assessment for container images stored in connected registries.

    [![Screenshot of the Settings and monitoring page for the Containers plan in Microsoft Defender for Cloud, showing available Defender for Containers components.](media/defender-for-containers-enable-plan/azure-defender-plans.png)](media/defender-for-containers-enable-plan/azure-defender-plans.png#lightbox)
7. Select **Save**.

---

## Verify the plan is enabled

To confirm that the Defender for Containers plan is enabled and the required components are active:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the subscription or connector where you enabled Defender for Containers.
4. Verify that **Containers** is set to **On**.
5. Select **Settings** next to Containers and confirm the required components are enabled.