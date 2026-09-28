---
layout: Conceptual
title: Build Cloud Security Explorer queries for container vulnerabilities - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/cloud-security-explorer-container-vulnerabilities
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
description: Learn how to build Cloud Security Explorer queries in Microsoft Defender for Cloud to identify vulnerabilities in registry images and running containers.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: cf12e647-2cf1-1cdd-90ff-f82e2463866b
document_version_independent_id: 82c1d3db-2673-6001-12e8-fd868c3fdc21
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/cloud-security-explorer-container-vulnerabilities.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/cloud-security-explorer-container-vulnerabilities
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/cloud-security-explorer-container-vulnerabilities.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 1c35d66c-3aba-a627-7eda-f1c5f6442511
---

# Build Cloud Security Explorer queries for container vulnerabilities - Microsoft Defender for Cloud | Microsoft Learn

Use Cloud Security Explorer to identify vulnerabilities in registry images and running containers. This article shows you how to build queries that find vulnerable container images in registries and in running Kubernetes workloads, and how to review the results.

For an introduction to Cloud Security Explorer, see [Build queries with Cloud Security Explorer](how-to-manage-cloud-security-explorer).

## Create a query to identify vulnerabilities in registry images

Find registry container images that have known vulnerabilities.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Cloud Security Explorer**.
3. In **Query builder**, select **Select resource types**.
4. Select **Container Images**.
5. Select **Done**.
6. Select **+**.
7. Select **Select condition**.
8. In **Vulnerabilities**, select **All vulnerabilities**.

    [![Screenshot showing a Cloud Security Explorer query to identify vulnerabilities in container images stored in registries.](media/cloud-security-explorer-container-vulnerabilities/registry-images-query.png)](media/cloud-security-explorer-container-vulnerabilities/registry-images-query.png#lightbox)
9. Select **Search**.
10. Select **View details &gt;** for a container image.
11. In **Result details**, review the affected packages and severity.
12. Select **Open the vulnerability page** for more details.

## Create a query to identify vulnerabilities in running containers

Find running containers in Kubernetes clusters that have known vulnerabilities.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Cloud Security Explorer**.
3. In **Query builder**, select **Select resource types**.
4. In **Containers**, select **Containers**.
5. Select **Done**.
6. Select **+**.
7. Select **Select condition**.
8. In **Application**, select **Created by**.
9. Select **Select resource types**.
10. Select **Container Images**.
11. Select **+**.
12. Select **Select condition**.
13. In **Vulnerabilities**, select **Has vulnerabilities**.

    [![Screenshot showing a Cloud Security Explorer query to identify vulnerabilities in container images used by running containers in Kubernetes clusters.](media/cloud-security-explorer-container-vulnerabilities/running-containers-query.png)](media/cloud-security-explorer-container-vulnerabilities/running-containers-query.png#lightbox)
14. Select **Search**.
15. Select **View details &gt;** for a container.
16. In **Result details**, review the affected images, severity, and related resources.
17. Select **Open the vulnerability page** for more details.