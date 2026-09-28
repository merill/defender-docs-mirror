---
layout: Conceptual
title: Add a resource group to your IoT solution - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/tutorial-configure-your-solution
breadcrumb_path: ../breadcrumb/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-iot-blog/bg-p/MicrosoftDefenderIoTBlog
feedback_help_link_type: ask-the-community
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
ms.service: defender-for-iot
author: limwainstein
manager: bagol
ms.author: lwainstein
ms.subservice: device-builders
description: In this quickstart, learn how to configure your end-to-end IoT solution using Microsoft Defender for IoT.
ms.topic: tutorial
ms.date: 2022-01-13T00:00:00.0000000Z
ms.custom: mode-other
locale: en-us
document_id: 0c3d2983-a84a-0594-f6a3-3ecc970eb433
document_version_independent_id: 69aee95e-4e89-df6c-736f-10cee7732263
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/tutorial-configure-your-solution.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/tutorial-configure-your-solution
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/tutorial-configure-your-solution.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 2093db86-5c8c-ed5d-7a0d-7aade891e659
---

# Add a resource group to your IoT solution - Microsoft Defender for IoT | Microsoft Learn

This article explains how to add a resource group to your Microsoft Defender for IoT solution. To learn more about resource groups, see [Manage Azure resource groups by using the Azure portal](/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal).

With Defender for IoT, you can monitor your entire IoT solution in one dashboard. From that dashboard, you can surface all of your IoT devices, IoT platforms, and back-end resources in Azure.

Once enabled, Defender for IoT will automatically identify other Azure services, and connect to related services that are affiliated with your IoT solution.

You can select other Azure resource groups that are part of your IoT solution. Your selections allow you to add entire subscriptions, resource groups, or single resources.

In this tutorial you'll learn how to:

- Add a resource group to your IoT solution

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- An [IoT hub](/en-us/azure/iot-hub/iot-hub-create-through-portal).
- You must have [enabled Microsoft Defender for IoT on your Azure IoT Hub](quickstart-onboard-iot-hub).

## Add Azure resources to your IoT solution

**To add new resource to your IoT solution**:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Search for, and select **IoT Hub**.
3. Navigate to **Defender for IoT** &gt; **Settings** &gt; **Monitored Resources**.
4. Select **Edit**, and select the monitored resources that belong to your IoT solution.
5. In the Solution Management window, select your subscription from the drop-down menu.
6. Select all applicable resource groups from the drop-down menu.
7. Select **Apply**.

A new resource group will now be added to your IoT solution.

Defender for IoT will now monitor your newly added resource groups, and surface relevant security recommendations and alerts as part of your IoT solution.