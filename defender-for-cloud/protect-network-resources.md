---
layout: Conceptual
title: Protecting your network resources - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/protect-network-resources
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
description: This document addresses recommendations in Microsoft Defender for Cloud that help you protect your Azure network resources and stay in compliance with security policies.
ms.topic: concept-article
ms.date: 2025-12-22T00:00:00.0000000Z
ms.custom: sfi-image-nochange
ai-usage: ai-assisted
locale: en-us
document_id: 75501de0-a9da-6577-c85f-64c33c0937e5
document_version_independent_id: 133826a6-cc0c-a96c-efc5-7c8dad49e67d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/protect-network-resources.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/protect-network-resources
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/protect-network-resources.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: aaf29ec4-9df7-0d42-f37f-da170fb639bb
---

# Protecting your network resources - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud continuously analyzes the security state of your Azure resources for network security best practices. When Defender for Cloud identifies potential security vulnerabilities, it creates recommendations that guide you through the process of configuring the needed controls to harden and protect your resources.

Review Defender for Cloud [networking recommendations](recommendations-reference-networking).

This article addresses recommendations that apply to your Azure resources from a network security perspective. Networking recommendations center around next generation firewalls, Network Security Groups, Just In Time (JIT) Virtual Machine (VM) access, overly permissive inbound traffic rules, and more. For a list of networking recommendations and remediation actions, see [Managing security recommendations in Microsoft Defender for Cloud](review-security-recommendations).

## Review networking resources and their recommendations

The [inventory page](asset-inventory) shows your resources by type. Use the resource type filter to see only the networking resources in your environment.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Go to **Microsoft Defender for Cloud** &gt; **Inventory**.

    [![Screenshot that shows where the inventory page is located in Defender for Cloud.](media/protect-network-resources/inventory.png)](media/protect-network-resources/inventory.png#lightbox)
3. Select the **Resource type** filter.
4. Enter **Network**.

    [![Screenshot that shows asset inventory network resource types.](media/protect-network-resources/network-filters-inventory.png)](media/protect-network-resources/network-filters-inventory.png#lightbox)
5. Select the relevant resource types.
6. Select **Apply**.
7. Hover over the recommendation indicator to see the number of active recommendations for each resource.

    [![Screenshot that shows the active recommendations for a resource.](media/protect-network-resources/resource-recommendations.png)](media/protect-network-resources/resource-recommendations.png#lightbox)
8. Select a resource to view the affiliated recommendations.
9. Select a recommendation.
10. [Remediate the recommendation](implement-security-recommendations).