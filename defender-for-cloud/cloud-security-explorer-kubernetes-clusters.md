---
layout: Conceptual
title: Build Cloud Security Explorer queries to identify vulnerabilities in Kubernetes clusters - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/cloud-security-explorer-kubernetes-clusters
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
description: Learn how to build queries with Cloud Security Explorer in Microsoft Defender for Cloud to investigate vulnerabilities in Kubernetes clusters.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: f1fd9f16-a4f2-2784-4886-1e93ded68685
document_version_independent_id: 9ed6cf87-2ee8-7e2b-7452-72e9ffcd046c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/cloud-security-explorer-kubernetes-clusters.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/cloud-security-explorer-kubernetes-clusters
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/cloud-security-explorer-kubernetes-clusters.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 51186bb2-abb5-d8a6-8160-f8f5b9b2eb2b
---

# Build Cloud Security Explorer queries to identify vulnerabilities in Kubernetes clusters - Microsoft Defender for Cloud | Microsoft Learn

Use Cloud Security Explorer to find vulnerabilities in your Kubernetes clusters. The following examples show how to build queries that check container images and cluster nodes. You can adapt these queries to filter results based on your needs.

For an introduction to Cloud Security Explorer queries, see [Build queries with Cloud Security Explorer](how-to-manage-cloud-security-explorer).

## Create a query to identify software vulnerabilities in container images

To create a query that finds software vulnerabilities in container images:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Cloud Security Explorer**.
3. In **Query builder**, select **Select resource types**.
4. Select **Container Images**.
5. Select **+**.
6. Select **Select condition**.
7. In **Application**, select **Has installed software**.

    [![Screenshot of query for identifying software vulnerabilities in container images.](media/cloud-security-explorer-kubernetes-clusters/software-vulnerabilities-in-container-images.png)](media/cloud-security-explorer-kubernetes-clusters/software-vulnerabilities-in-container-images.png#lightbox)
8. Select **Search**.
9. Select **View details &gt;** for the relevant container image.
10. In the **Result details** pane, review **Insights - Has installed software**.

    [![Screenshot shows results of Cloud Security Explorer query to retrieve container images with software installed.](media/cloud-security-explorer-kubernetes-clusters/security-explorer-containers-query-result-details.png)](media/cloud-security-explorer-kubernetes-clusters/security-explorer-containers-query-result-details.png#lightbox)

## Create a query to identify vulnerabilities in cluster nodes

To create a query that finds vulnerabilities in cluster nodes:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Cloud Security Explorer**.
3. In **Query builder**, select **Select resource types**.
4. Under **Kubernetes clusters**, select **Azure Kubernetes Service**.
5. Select **Done**.
6. Select **+**.
7. Select **Select condition**.
8. In **Application**, select **Maintains**.
9. Select **Select resource types** &gt; **Kubernetes Node Pools**.
10. Select **Done**.
11. Select **+**.
12. Select **Select condition**.
13. Select **Maintains**.
14. Select **Select resource types** &gt; **Virtual machines clusters**.
15. Select **Done**.
16. Select **+**.
17. **Select condition**.
18. In **Vulnerabilities**, select **All vulnerabilities**.

    [![Screenshot of query for identifying vulnerabilities in cluster nodes.](media/cloud-security-explorer-kubernetes-clusters/vulnerabilities-in-cluster-nodes.png)](media/cloud-security-explorer-kubernetes-clusters/vulnerabilities-in-cluster-nodes.png#lightbox)
19. Select **Search**.
20. Select **View details &gt;** for the relevant Kubernetes node pool.

    [![Screenshot of Cloud Security Explorer query options to retrieve list of cluster nodes with vulnerabilities.](media/cloud-security-explorer-kubernetes-clusters/security-cloud-explorer-kubernetes-nodes-results.png)](media/cloud-security-explorer-kubernetes-clusters/security-cloud-explorer-kubernetes-nodes-results.png#lightbox)
21. In the **Result details** pane, select the **Virtual machine scale set** icon to view vulnerabilities.

    [![Screenshot shows results of Cloud Security Explorer query to retrieve vulnerabilities in cluster nodes.](media/cloud-security-explorer-kubernetes-clusters/security-cloud-explorer-kubernetes-nodes-results-details.png)](media/cloud-security-explorer-kubernetes-clusters/security-cloud-explorer-kubernetes-nodes-results-details.png#lightbox)