---
layout: Conceptual
title: Enable Gated Deployment for AKS by Using the Managed Cluster API - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/gated-deployment-infrastructure-as-code
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
description: Learn how to enable gated deployment for AKS by configuring a managed identity for the gated deployment agent through the managed cluster API.
ms.custom: msecd-doc-authoring-1013
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
locale: en-us
document_id: c264fb33-a21b-9244-d98d-0cf31a611a79
document_version_independent_id: 7f6443d6-851d-0097-d9b6-0ce15c625a21
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/gated-deployment-infrastructure-as-code.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/gated-deployment-infrastructure-as-code
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/gated-deployment-infrastructure-as-code.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d44a5346-5de4-439c-b804-7b2a536cbb55
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/da41a22b-b7a0-42d3-9c35-50da1c2b7b87
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 24c61c72-1efd-84b6-0587-7063c2e96609
---

# Enable Gated Deployment for AKS by Using the Managed Cluster API - Microsoft Defender for Cloud | Microsoft Learn

This article shows you how to configure gated deployment for Azure Kubernetes Service (AKS) by using the managed cluster API. You can also [install the Defender for Containers sensor by using Helm](deploy-helm).

Gated deployment uses an admission controller to evaluate container images before it admits them into a Kubernetes cluster. For AKS, the gated deployment agent needs read access to the Azure Container Registry (ACRs) that the cluster uses so it can access vulnerability findings artifacts that Microsoft Defender for Containers generates.

Before you configure gated deployment by using the managed cluster API, enable the required Defender for Containers components for the AKS cluster and ACRs.

To provide the required ACR access, create a user-assigned managed identity, assign it read permissions on the relevant ACRs, configure federated identity credentials, and reference the managed identity in the managed cluster API.

## Prerequisites

Before you begin, ensure that:

- You have a Microsoft Azure subscription. If you don't have an Azure subscription, you can [sign up for a free subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- [Defender for Cloud is enabled](get-started#enable-defender-for-cloud-on-your-azure-subscription) on your Azure subscription.
- [Defender for Containers is enabled](defender-for-containers-enable-plan) for the Azure subscription or subscriptions that contain your AKS cluster and Azure Container Registries (ACRs), with the following components enabled:

    - **Defender sensor** with **Security Gating**
    - **Registry access** with **Security findings**

    Note

    You only need to install security gating once. The first time you enable the security gating toggle, it installs security gating. After that, security gating is already installed.

    When the installation runs again, the system detects this and does nothing. If you try to install it again through the API, it fails because security gating already exists.

    [![Screenshot that shows security gating is turned to on.](media/gated-deployment-infrastructure-as-code/security-gating-on.png)](media/gated-deployment-infrastructure-as-code/security-gating-on.png#lightbox)
- Your AKS cluster has:

    - An [OpenID Connect (OIDC) issuer](/en-us/azure/aks/use-oidc-issuer) enabled.
    - [Azure Workload Identity](/en-us/azure/aks/workload-identity-deploy-cluster?tabs=new-cluster) enabled.
- Permission to create and assign a user-assigned managed identity.
- Permission to assign the **AcrPull** role, or an equivalent read role, on all ACRs used by the cluster.

## Configure the managed identity

Perform the following steps to configure the managed identity for gated deployment:

1. [Create a Managed Service Identity (MSI) that the gated deployment agent uses](/en-us/entra/identity/managed-identities-azure-resources/manage-user-assigned-managed-identities-azure-portal).
2. [Assign the **AcrPull** role or an equivalent read role](/en-us/azure/container-registry/container-registry-rbac-built-in-roles-overview?tabs=registries-configured-with-rbac-registry-abac-repository-permissions) to the MSI on all ACRs the cluster uses.
3. [Add a Federated Identity Credential (FIC) to the MSI](/en-us/graph/api/resources/federatedidentitycredentials-overview?view=graph-rest-1.0&amp;preserve-view=true) that allows the gated deployment agent to authenticate by using AKS Workload Identity, with the following FIC parameters:

    - **Issuer**: The AKS OIDC issuer URL
    - **Subject**: The service account used by the gated deployment agent `system:serviceaccount:kube-system:defender-admission-controller-serviceaccount`.
    - **Audience**: `api://AzureADTokenExchange`
4. Under the [securityGating section of the managed cluster API configuration](/en-us/azure/templates/microsoft.containerservice/managedclusters?pivots=deployment-language-arm-template#resource-format-1), set the [MSI's objectId in the identities parameter](/en-us/azure/templates/microsoft.containerservice/managedclusters?pivots=deployment-language-arm-template#managedclustersecurityprofiledefendersecuritygating-1) under the security gating section of the managed cluster API configuration.

    [![Screenshot of the managed cluster API configuration showing the identities parameter in the security gating section.](media/gated-deployment-infrastructure-as-code/identities.png)](media/gated-deployment-infrastructure-as-code/identities.png#lightbox)

    Setting the MSI's `objectId` in the identities parameter ensures that the gated deployment agent can use the MSI at runtime.