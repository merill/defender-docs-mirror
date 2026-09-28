---
layout: Conceptual
title: Exclude Kubernetes clusters from automatic Defender sensor deployment - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-containers-exclude-cluster
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
description: Learn how to exclude specific Kubernetes clusters from automatic Defender for Containers sensor deployment by using resource tags.
ms.topic: how-to
ms.date: 2026-05-05T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: edd3050a-c488-d31b-8ae1-debeb28cf3b6
document_version_independent_id: 091bafb3-3a93-d247-a40a-2848d008df3b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/defender-for-containers-exclude-cluster.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/defender-for-containers-exclude-cluster
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/defender-for-containers-exclude-cluster.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/d44a5346-5de4-439c-b804-7b2a536cbb55
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/da41a22b-b7a0-42d3-9c35-50da1c2b7b87
platformId: 8112a47c-494f-88da-6c8a-4e0cadad953b
---

# Exclude Kubernetes clusters from automatic Defender sensor deployment - Microsoft Defender for Cloud | Microsoft Learn

When automatic provisioning is enabled in the Defender for Containers plan, Microsoft Defender for Cloud deploys the Defender sensor to supported Kubernetes clusters.

To manage sensor deployment manually for specific clusters, add an exclusion tag to prevent automatic deployment.

You can use exclusion tags on the following cluster types:

- Azure Kubernetes Service (AKS)
- Amazon Elastic Kubernetes Service (EKS)
- Google Kubernetes Engine (GKE)

Note

Exclusion tags aren't supported for Arc-enabled Kubernetes clusters in on-premises environments.

## Prerequisites

- [Defender for Containers is enabled](defender-for-containers-enable-plan) with automatic provisioning turned on.

## Exclude a cluster from automatic sensor deployment

To exclude a cluster from automatic Defender sensor deployment:

Important

Add the exclusion tag before automatic provisioning deploys the Defender sensor. If the Defender sensor is already deployed, adding the tag doesn't remove the existing deployment.

# [AKS](#tab/aks)
To exclude an AKS cluster from automatic Defender sensor deployment:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Kubernetes services**.
3. Select the relevant AKS cluster.
4. Select **Tags**.
5. Add the following tag:

    - **Name**: `ms_defender_container_exclude_sensors`
    - **Value**: `true`

    [![Screenshot of the Tags page for a Kubernetes cluster showing the ms_defender_container_exclude_sensors tag set to true.](media/defender-for-containers-exclude-cluster/exclude-cluster-from-automatic-defender-sensor-deployment.png)](media/defender-for-containers-exclude-cluster/exclude-cluster-from-automatic-defender-sensor-deployment.png#lightbox)
6. Select **Apply**.

# [EKS](#tab/eks)
To exclude an EKS cluster from automatic Defender sensor deployment:

1. Sign in to the AWS Management Console.
2. Go to **Amazon EKS**.
3. Select the relevant EKS cluster.
4. Select the **Tags** tab.
5. Add the following tag:

    - **Key**: `ms_defender_container_exclude_sensors`
    - **Value**: `true`
6. Select **Save changes**.

# [GKE](#tab/gke)
To exclude a GKE cluster from automatic Defender sensor deployment:

1. Sign in to the Google Cloud console.
2. Go to **Kubernetes Engine**.
3. Select the relevant GKE cluster.
4. In **Metadata**, select the edit icon next to **Labels**.
5. Add the following label:

    - **Key**: `ms_defender_container_exclude_sensors`
    - **Value**: `true`
6. Save your changes.

---