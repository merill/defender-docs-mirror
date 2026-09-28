---
layout: Conceptual
title: Move an iotSecuritySolutions Resource to Another Region by using the Azure Portal - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/how-to-region-move
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
description: Move an iotSecuritySolutions resource from one Azure region to another by using the Azure portal.
ms.topic: how-to
ms.custom: subject-moving-resources, msecd-doc-authoring-1016
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: c8a77ab2-a103-7192-3f02-e73eea301104
document_version_independent_id: 86d68148-fb44-97a0-8b2d-f71c50a15cb9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/how-to-region-move.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/how-to-region-move
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/how-to-region-move.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/816835a3-1c5d-4536-835c-4b59dc9c9d97
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/a98c4e96-5248-4755-860b-6c76f1933f0c
platformId: b90c3142-cd43-0105-2320-bc24b8e2e9a0
---

# Move an iotSecuritySolutions Resource to Another Region by using the Azure Portal - Microsoft Defender for IoT | Microsoft Learn

There are various scenarios for moving an existing resource from one region to another. For example, you might want to take advantage of features, and services that are only available in specific regions, to meet internal policy and governance requirements, or in response to capacity planning requirements.

You can move a Microsoft Defender for IoT iotSecuritySolutions resource to a different Azure region. The iotSecuritySolutions resource is a hidden resource that is connected to a specific IoT hub resource that is used to enable security on the hub. Learn how to [configure, and create](/en-us/azure/templates/microsoft.security/iotsecuritysolutions?tabs=bicep) the iotSecuritySolutions resource.

## Resource prerequisites

Before you begin the move, make sure the following prerequisites are met:

- Make sure that the resource is in the Azure region that you want to move from.
- An existing iotSecuritySolutions resource.
- Make sure that your Azure subscription allows you to create iotSecuritySolutions resources in the target region.
- Make sure that your subscription has enough resources to support the addition of resources for this process. For more information, see [Azure subscription and service limits, quotas, and constraints](/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits#azure-networking-limits)

## Prepare alerts before moving the resource

Prepare the iotSecuritySolutions resource for the region move by locating it and confirming its current region.

Before transitioning the resource to the new region, we recommend that you create a [Log Analytics workspace](/en-us/azure/azure-monitor/logs/quick-create-workspace) to preserve your existing alerts and raw events. A Log Analytics workspace provides a central location to retain existing alerts and raw events so that they remain available after the move.

To find the resource you want to move:

1. Sign in to the [Azure portal](https://portal.azure.com) and select **All Resources**.
2. Select **Show hidden types**.

    ![Screenshot showing where the Show hidden resources checkbox is located.](media/region-move/hidden-resources.png)
3. Select the **Type** filter, and enter `iotsecuritysolutions` in the search field.

    ![Screenshot showing you how to filter by type.](media/region-move/filter-type.png)
4. Select **Apply**.
5. Select your hub from the list.
6. Ensure that you've selected the correct hub, and that it is in the region you want to move it from.

    ![Screenshot showing you the region your hub is located in.](media/region-move/location.png)

## Move the IoT Hub to another region

The hidden iotSecuritySolutions resource is tied to its associated IoT Hub, so moving the resource to another region requires cloning the IoT Hub to the target region. To clone the IoT Hub and its linked iotSecuritySolutions resource, follow the instructions in [Clone and migrate an IoT Hub to another region](/en-us/azure/iot-hub/iot-hub-how-to-clone).

After the move is complete and Defender for IoT is re-enabled, reconnect the hub to the Log Analytics workspace that you set up earlier.

## Verify the moved resource in the target region

After the move, verify that the iotSecuritySolutions resource is in the target region, that the Defender for IoT connection to the IoT Hub is enabled, and that recommendations are working correctly.

To verify the resource is in the correct region:

1. Sign in to the [Azure portal](https://portal.azure.com) and select **All Resources**.
2. Select **Show hidden types**.

    ![Screenshot showing where the Show hidden resources checkbox is located.](media/region-move/hidden-resources.png)
3. Select the **Type** filter, and enter `iotsecuritysolutions` in the search field.
4. Select **Apply**.
5. Select your hub from the list.
6. Ensure that the region has been changed.

    ![Screenshot that shows you the region your hub is located in.](media/region-move/location-changed.png)

To ensure everything is working correctly:

1. Navigate to **IoT Hub** &gt; **`Your hub`** &gt; **Defender for IoT**, and select Recommendations.

    ![Screenshot showing you where to go to see recommendations.](media/region-move/recommendations.png)

The recommendations should have transferred and everything should be working correctly.

## Clean up source resources

Don't clean up until you've finished verifying that the resource has moved and the recommendations have transferred. When you're ready, clean up the old resources by performing these steps:

Warning

Deleting the old hub removes all active devices from the hub.

- If you haven't already, delete the old hub.
- If you have routing resources that you moved to the new location, you can delete the old routing resources.