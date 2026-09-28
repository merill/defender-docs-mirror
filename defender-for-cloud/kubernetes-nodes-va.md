---
layout: Conceptual
title: Review and Remediate Kubernetes Node Vulnerabilities - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/kubernetes-nodes-va
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
description: Learn how to review and remediate vulnerability findings for Kubernetes nodes in Microsoft Defender for Cloud.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-image-nochange, msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: 7709f818-49fa-f928-6c57-8a4c7ef654e3
document_version_independent_id: adc33c56-57c7-8f43-2bcf-6f9eab112cec
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/kubernetes-nodes-va.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/kubernetes-nodes-va
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/kubernetes-nodes-va.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/d44a5346-5de4-439c-b804-7b2a536cbb55
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/da41a22b-b7a0-42d3-9c35-50da1c2b7b87
platformId: 8770323e-26d3-5bf2-937a-cc817a8ec1c1
---

# Review and Remediate Kubernetes Node Vulnerabilities - Microsoft Defender for Cloud | Microsoft Learn

Defender for Cloud scans the virtual machines (VMs) that host [Kubernetes nodes](kubernetes-nodes-overview) for vulnerabilities in the operating system and installed software. When it detects vulnerabilities, Defender for Cloud generates recommendations with detailed findings to help you review and remediate them.

This capability is supported on Azure Kubernetes Service (AKS), Amazon Elastic Kubernetes Service (EKS), and Google Kubernetes Engine (GKE). EKS and GKE support is currently in preview.

Reviewing and remediating these vulnerabilities is part of the [shared responsibility](kubernetes-nodes-overview#shared-responsibility) for maintaining Kubernetes node security.

## Prerequisites

Before you begin, ensure that:

- Have an active Azure, AWS, or GCP subscription.
- [Microsoft Defender for Cloud is enabled on your subscription](connect-azure-subscription) with one of the following plans enabled:

    - Defender for Containers
    - Defender for Servers P2
    - Defender Cloud Security Posture Management
- Agentless scanning for machines enabled.
- For EKS or GKE nodes, your AWS or GCP environment must be [connected to Defender for Cloud](quickstart-onboard-aws).

## Review vulnerability findings for Kubernetes nodes

To review vulnerability findings for Kubernetes nodes, follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Recommendations**.
3. Search for and select the relevant recommendation for your environment:

    - **AKS**: `AKS nodes should have vulnerability findings resolved`
    - **EKS**: `EKS nodes should have vulnerability findings resolved` (Preview)
    - **GKE**: `GKE nodes should have vulnerability findings resolved` (Preview)
4. Review the recommendation details, including affected node pools and clusters.

    [![Screenshot showing the details of the recommendation for the Kubernetes node.](media/kubernetes-nodes-va/recommendation-node-details.png)](media/kubernetes-nodes-va/recommendation-node-details.png#lightbox)
5. Select **Findings** to view the list of CVEs.

    [![Screenshot of selecting the findings tab to view a list of CVEs related to the Kubernetes node.](media/kubernetes-nodes-va/recommendation-node-details-findings.png)](media/kubernetes-nodes-va/recommendation-node-details-findings.png#lightbox)
6. Select a CVE to view detailed vulnerability information, including affected resources.

## Remediate Kubernetes node vulnerabilities

To remediate vulnerabilities found on your Kubernetes nodes, follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Recommendations**.
3. Search for and select the relevant recommendation for your environment:

    - **AKS**: `AKS nodes should have vulnerability findings resolved`
    - **EKS**: `EKS nodes should have vulnerability findings resolved` (Preview)
    - **GKE**: `GKE nodes should have vulnerability findings resolved` (Preview)
4. Select **Fix**.

    [![Screenshot showing the details of the recommendation for the Kubernetes node and the highlighted Fix button.](media/kubernetes-nodes-va/recommendation-node-details-select-fix.png)](media/kubernetes-nodes-va/recommendation-node-details-select-fix.png#lightbox)
5. Select **Update image** to apply the latest patched node pool VM image, or **Upgrade Kubernetes** to move the cluster to a newer Kubernetes version.

    [![Screenshot showing the overview details of the Kubernetes node pool for updating its image.](media/kubernetes-nodes-va/node-pool-overview.png)](media/kubernetes-nodes-va/node-pool-overview.png#lightbox)