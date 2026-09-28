---
layout: Conceptual
title: View and Remediate Vulnerabilities for Running Containers - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/view-and-remediate-vulnerabilities-containers
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
description: Learn how to view and remediate vulnerability findings for running containers in Microsoft Defender for Cloud.
ms.custom: build-2023, sfi-image-nochange, msecd-doc-authoring-1013
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: e84e7d81-0396-1292-95a9-38185dc8b77d
document_version_independent_id: b4be0c0f-36d3-6a9f-77fe-abdd4f5a2436
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/view-and-remediate-vulnerabilities-containers.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/view-and-remediate-vulnerabilities-containers
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/view-and-remediate-vulnerabilities-containers.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 32d462f4-47ac-3d9f-74ad-347102a6a8d2
---

# View and Remediate Vulnerabilities for Running Containers - Microsoft Defender for Cloud | Microsoft Learn

Defender for Cloud helps you find and fix vulnerabilities in images that your Kubernetes workloads use.

To create these findings, Defender for Cloud first builds a list of your Kubernetes workloads. It uses supported discovery and protection components to build the list. Then it matches that list against known vulnerability data for the images those workloads run.

Findings for running containers appear as security recommendations. The following steps use the **Flat list** view, which shows results at the resource level. Learn more about [reviewing recommendations by title or by resource](review-security-recommendations#recommendation-title-view).

Note

You might see both grouped and individual recommendation formats in the portal during this transition. Learn more about [transitioning from grouped to individual recommendations](transition-grouped-individual-recommendations).

## Prerequisites

Before you begin, enable [Defender for Containers](defender-for-containers-enable-plan) or [Defender CSPM](tutorial-enable-cspm-plan) on your subscription. Turn on one of these component sets:

- **Registry access** and either **Kubernetes API access** or **Defender sensor**. This option links scanned registry images to running workloads.
- **Agentless scanning for machines** and either **Kubernetes API access** or **Defender sensor**. This option checks for runtime vulnerabilities without a registry.

## View vulnerabilities for running containers

To view vulnerabilities for a running container:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud** &gt; **Recommendations**.
3. Select the **Vulnerabilities** tab.
4. Select the **Flat list** view.
5. Select **Add filter**.
6. Select **Resource type**.
7. Select **Container**.

    [![Screenshot of the Resource type filter in Microsoft Defender for Cloud Recommendations with Container selected.](media/view-and-remediate-vulnerabilities-containers/resource-type-container.png)](media/view-and-remediate-vulnerabilities-containers/resource-type-container.png#lightbox)
8. Select **Apply**.
9. Select a recommendation.
10. Review the details, including risk info, fix steps, and metadata.
11. Select the **Associated CVEs** tab to see the CVEs for that item.
12. Select a CVE to view its severity, affected components, and fix version.