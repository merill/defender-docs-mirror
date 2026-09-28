---
layout: Conceptual
title: Onboard agentless containers for CSPM - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/how-to-enable-agentless-containers
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
description: Learn how to onboard agentless containers in Defender CSPM.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 4c49c395-c030-28ce-21b6-ad01773fd510
document_version_independent_id: d2930612-c881-1fc7-101b-f91cabd05338
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/how-to-enable-agentless-containers.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/how-to-enable-agentless-containers
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/how-to-enable-agentless-containers.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 15606799-e2ea-7218-0040-044d8685437b
---

# Onboard agentless containers for CSPM - Microsoft Defender for Cloud | Microsoft Learn

Enable agentless container posture in Defender CSPM to gain visibility into Kubernetes clusters and container images without deploying agents.

Agentless container posture is available for Azure, AWS, and GCP environments. This article walks you through enabling agentless container posture in each supported cloud so you can discover running containers, assess vulnerabilities in container registries, and analyze Kubernetes cluster configurations.

## Prerequisites

- [Defender CSPM plan is enabled for your environment](connect-azure-subscription).

## How to onboard agentless container posture in Defender CSPM

Use the following steps to onboard agentless container posture in Defender CSPM for your cloud environment.

# [Azure](#tab/azure)
1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the relevant subscription.
4. Under **Defender plans**, locate **Defender CSPM**.
5. Select **Settings**.
6. Enable the following settings:

    - **Kubernetes API access**
    - **Registry access**
7. Select **Continue**.
8. Select **Save**.

# [AWS](#tab/aws)
1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the relevant AWS connector.
4. Under **Defender plans**, locate **Defender CSPM**.
5. Select **Settings**.
6. Enable the following settings:

    - **Kubernetes API access**
    - **Registry access**

    [![Screenshot of the Defender CSPM plan configuration for AWS showing Kubernetes API access and Registry access enabled.](media/concept-agentless-containers/toggle-on-components-amazon.png)](media/concept-agentless-containers/toggle-on-components-amazon.png#lightbox)
7. Select **Continue**.
8. Select **Save**.
9. Select **Next: Configure access**.
10. Redeploy the CloudFormation or Terraform template.
11. Select **Next: Review and generate**.
12. Select **Update**.

# [GCP](#tab/gcp)
1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the relevant GCP connector.
4. Under **Defender plans**, locate **Defender CSPM**.
5. Select **Settings**.
6. Enable the following settings:

    - **Kubernetes API access**
    - **Registry access**

    [![Screenshot of the Defender CSPM plan configuration for GCP showing Kubernetes API access and Registry access enabled.](media/concept-agentless-containers/toggle-on-components-google.png)](media/concept-agentless-containers/toggle-on-components-google.png#lightbox)
7. Select **Continue**.
8. Select **Save**.
9. Select **Next: Configure access**.
10. Redeploy the Cloud Shell or Terraform template.
11. Select **Next: Review and generate**.
12. Select **Update**.

Note

Kubernetes API access uses Azure Kubernetes Service (AKS) trusted access, a feature that lets Azure resources securely access AKS clusters. For more information, see [Enable Azure resources to access Azure Kubernetes Service (AKS) clusters using Trusted Access](/en-us/azure/aks/trusted-access-feature).

---