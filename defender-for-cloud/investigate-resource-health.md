---
layout: Conceptual
title: Tutorial - Investigate the health of your resources - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/investigate-resource-health
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
description: 'Tutorial: Learn how to investigate the health of your resources using Microsoft Defender for Cloud.'
ms.topic: tutorial
ms.date: 2025-05-20T00:00:00.0000000Z
ms.custom: sfi-image-blocked
ai-usage: ai-assisted
locale: en-us
document_id: 5103241f-3677-4ccb-c3ad-173e99caf345
document_version_independent_id: c0659832-f5ff-9ab5-1927-af887a56b735
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/investigate-resource-health.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/investigate-resource-health
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/investigate-resource-health.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: abf8fa4e-b2da-dc86-a935-c3c4c84edff9
---

# Tutorial - Investigate the health of your resources - Microsoft Defender for Cloud | Microsoft Learn

The resource health page provides a snapshot view of the overall health of a single resource. You can review detailed information about the resource and all recommendations that apply to that resource. Also, if you're using any of the [advanced protection plans of Microsoft Defender for Cloud](defender-for-cloud-introduction), you can see outstanding security alerts for that specific resource too.

This single page, in Defender for Cloud's portal pages shows:

- **Resource information** - The resource group and subscription it's attached to, the geographic location, and more.
- **Applied security feature** - Whether a Microsoft Defender plan is enabled for the resource.
- **Counts of outstanding recommendations and alerts** - The number of outstanding security recommendations and Defender for Cloud alerts.
- **Actionable recommendations and alerts** - Two tabs list the recommendations and alerts that apply to the resource.

![Microsoft Defender for Cloud's resource health page showing the health information for a virtual machine](media/investigate-resource-health/resource-health-page-virtual-machine.gif)

In this tutorial you'll learn how to:

- Access the resource health page for all resource types
- Evaluate the outstanding security issues for a resource
- Improve the security posture for the resource

## Prerequisites

To step through the features covered in this tutorial:

- You need an Azure subscription. If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.
- [Microsoft Defender for Cloud enabled on your subscription](connect-azure-subscription).
- **To apply security recommendations**: you must be signed in with an account that has the relevant permissions (Resource Group Contributor, Resource Group Owner, Subscription Contributor, or Subscription Owner)
- **To dismiss alerts**: you must be signed in with an account that has the relevant permissions (Security Admin, Subscription Contributor, or Subscription Owner)

## Access the health information for a resource

Tip

In the following screenshots, we're opening a virtual machine, but the resource health page can show you the details for all resource types.

**To open the resource health page for a resource**:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Microsoft Defender for Cloud**.
3. Select **Inventory**.
4. Select any resource.

    [![Select a resource from the asset inventory to view the resource health page.](media/investigate-resource-health/inventory-select-resource.png)](media/investigate-resource-health/inventory-select-resource.png#lightbox)
5. Review the left pane of the resource health page for an overview of the subscription, status, and monitoring information about the resource. You can also see whether enhanced security features are enabled for the resource:

    ![The left pane of Microsoft Defender for Cloud's resource health page shows the subscription, status, and monitoring information about the resource. It also includes the total number of outstanding security recommendations and security alerts.](media/investigate-resource-health/resource-health-left-pane.png)
6. Use the two tabs on the right pane to review the lists of security recommendations and alerts that apply to this resource:

    [![The right pane of Microsoft Defender for Cloud's resource health page has two tabs: recommendations and alerts.](media/investigate-resource-health/resource-health-right-pane.png)](media/investigate-resource-health/resource-health-right-pane.png#lightbox)

    Note

    Microsoft Defender for Cloud uses the terms "healthy" and "unhealthy" to describe the security status of a resource. These terms relate to whether the resource is compliant with a specific [security recommendation](security-policy-concept).

    In the screenshot above, you can see that recommendations are listed even when this resource is "healthy". One advantage of the resource health page is that all recommendations are listed so you can get a complete picture of your resources' health.

## Evaluate the outstanding security issues for a resource

The resource health page lists the recommendations for which your resource is "unhealthy" and the alerts that are active.

### Harden a resource

To ensure your resource is hardened according to the policies applied to your subscriptions, fix the issues described in the recommendations:

1. From the right pane, select a recommendation.
2. Continue as instructed on screen.

    Tip

    The instructions for fixing issues raised by security recommendations differ for each of Defender for Cloud's recommendations.

    To decide which recommendations to resolve first, look at the severity of each one and its [potential impact on your secure score](secure-score-security-controls).

### Investigate a security alert

1. From the right pane, select an alert.
2. Follow the instructions in [Respond to security alerts](manage-respond-alerts).