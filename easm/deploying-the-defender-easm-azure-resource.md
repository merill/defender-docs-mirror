---
layout: Conceptual
title: Create a Defender EASM Azure Resource | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/external-attack-surface-management/deploying-the-defender-easm-azure-resource
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/133/azure
feedback_help_link_type: get-help-at-qna
feedback_product_url: https://feedback.azure.com/d365community/forum/79b1327d-d925-ec11-b6e6-000d3a4f06a4
feedback_system: Standard
learn_banner_products:
- azure
permissioned-type: public
recommendations: true
recommendation_types:
- Training
- Certification
uhfHeaderId: azure
ms.suite: office
adobe-target: true
ms.service: defender-easm
description: This article explains how to create a Microsoft Defender External Attack Surface Management (Defender EASM) Azure resource by using the Azure portal.
author: danielledennis
ms.author: dandennis
ms.date: 2022-07-14T00:00:00.0000000Z
ms.topic: quickstart
ms.custom: references_regions
locale: en-us
document_id: 2cd27500-4271-db61-48ec-c180d1f19c7f
document_version_independent_id: 0f5b14ae-fc60-3c26-56c4-241416dd9f62
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/easm/deploying-the-defender-easm-azure-resource.md
site_name: Docs
depot_name: Azure.easm-azure
page_type: conceptual
toc_rel: toc.json
asset_id: external-attack-surface-management/deploying-the-defender-easm-azure-resource
moniker_range_name: 
monikers: []
item_type: Content
source_path: easm/deploying-the-defender-easm-azure-resource.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: e6a39723-931f-180e-fdf5-069d0ef5a673
---

# Create a Defender EASM Azure Resource | Microsoft Learn

This article explains how to create a Microsoft Defender External Attack Surface Management (Defender EASM) Azure resource by using the Azure portal. Users can begin their usage of Defender EASM with a 30-day free trial. Once the trial is nearing expiration, you will be notified via banners and push notifications.

Creating the Defender EASM Azure resource involves two steps:

- Create a resource group.
- Create a Defender EASM resource in the resource group.

## Prerequisites

Before you create a Defender EASM resource group, become familiar with how to access and use the [Azure portal](https://portal.azure.com/). Also read the [Defender EASM Overview article](overview) for key context on the product. You need:

- A valid Azure subscription or free Defender EASM trial account. If you don’t have an [Azure subscription](/en-us/azure/guides/developer/azure-developer-guide#understanding-accounts-subscriptions-and-billing), create a free Azure account before you begin.
- A Contributor role assigned for you to create a resource. To get this role assigned to your account, follow the steps in the [Assign roles](/en-us/azure/role-based-access-control/role-assignments-steps) documentation. Or you can contact your administrator.

## Create a resource group

1. To create a new resource group, select **Resource groups** in the Azure portal.

    ![Screenshot that shows the Resource groups option highlighted on the Azure home page.](media/quickstart-1.png)
2. Under **Resource groups**, select **Create**.

    ![Screenshot that shows Create highlighted in the Resource groups list view.](media/quickstart-2.png)
3. Select or enter the following property values:

    - **Subscription**: Select an Azure subscription.
    - **Resource group**: Give the resource group a name.
    - **Region**: Specify an Azure location. This location is where the resource group stores metadata about the resource. For compliance reasons, you might want to specify where that metadata is stored. In general, we recommend that you specify a location where most of your resources will be. Using the same location can simplify your template. The following regions are supported:
        - southcentralus
        - eastus
        - australiaeast
        - westus3
        - swedencentral
        - eastasia
        - japaneast
        - westeurope
        - northeurope
        - switzerlandnorth
        - canadacentral
        - centralus
        - norwayeast
        - francecentral

    ![Screenshot that shows the Create a resource group Basics tab.](media/quickstart-3.png)
4. Select **Review + create**.
5. Review the values and select **Create**.
6. Select **Refresh** to view the new resource group in the list.

## Create resources in a resource group

After you create a resource group, you can create Defender EASM resources in the group by searching for Defender EASM in the Azure portal.

1. In the search box, enter **Microsoft Defender EASM** and select Enter.
2. Select **Create** to create a Defender EASM resource.

    ![Screenshot that shows the Create button highlighted in the Defender EASM list view.](media/quickstart-5.png)
3. Select or enter the following property values:

    - **Subscription**: Select an Azure subscription.
    - **Resource group**: Select the resource group created in the earlier step. You can also create a new one as part of the process of creating this resource.
    - **Name**: Give the Defender EASM workspace a name.
    - **Region**: Select an Azure location. See the supported regions listed in the preceding section.

    ![Screenshot that shows the Create Microsoft Defender EASM workspace Basics tab.](media/quickstart-6.png)
4. Select **Review + create**.
5. Review the values and select **Create**.
6. Select **Refresh** to see the status of the resource creation. Now you can go to the resource to get started.