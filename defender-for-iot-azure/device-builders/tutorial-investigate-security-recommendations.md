---
layout: Conceptual
title: Investigate security recommendations - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/tutorial-investigate-security-recommendations
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
description: Learn how to investigate security recommendations with the Defender for IoT.
ms.topic: tutorial
ms.date: 2022-01-12T00:00:00.0000000Z
locale: en-us
document_id: a2ce65dd-2d6d-f9ae-5919-d6ab077a0de0
document_version_independent_id: fe4a25e9-3532-4e5f-27f4-283f8e028356
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/tutorial-investigate-security-recommendations.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/tutorial-investigate-security-recommendations
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/tutorial-investigate-security-recommendations.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/816835a3-1c5d-4536-835c-4b59dc9c9d97
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/a98c4e96-5248-4755-860b-6c76f1933f0c
platformId: d2a1076b-541a-c025-6f69-f69fb5a12211
---

# Investigate security recommendations - Microsoft Defender for IoT | Microsoft Learn

This tutorial will help you learn how to explore the information available in each IoT security recommendation, and explain how to use the details of each recommendation and related devices, to reduce risks.

Timely analysis and mitigation of recommendations by Defender for IoT is the best way to improve security posture and reduce attack surface across your IoT solution.

In this tutorial you'll learn how to:

- Investigate new recommendations
- Investigate security recommendation details
- Investigate recommendations in a Log Analytics workspace

Note

Defender for IoT plans to retire the micro agent on June 1, 2027.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- An [IoT hub](/en-us/azure/iot-hub/iot-hub-create-through-portal).
- You must have [enabled Microsoft Defender for IoT on your Azure IoT Hub](quickstart-onboard-iot-hub).
- You must have [added a resource group to your IoT solution](quickstart-configure-your-solution).
- You must have [created a Defender for IoT micro agent module twin](quickstart-create-micro-agent-module-twin).
- You must have [installed the Defender for IoT micro agent](quickstart-standalone-agent-binary-installation).
- You must have [configured the Microsoft Defender for IoT agent-based solution](how-to-configure-agent-based-solution).

## Investigate recommendations

The IoT Hub recommendations list displays all of the aggregated security recommendations for your IoT Hub.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Navigate to **IoT Hub** &gt; **`Your hub`** &gt; **Defender for IoT** &gt; **Recommendations**.
3. Select a recommendation from the list to open the recommendation's details.

## Investigate security recommendation details

Open each aggregated recommendation to display the detailed recommendation description, remediation steps, and device ID for each device that triggered a recommendation. It also displays recommendation severity and direct-investigation access using Log Analytics.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Navigate to **IoT Hub** &gt; **`Your hub`** &gt; **Defender for IoT** &gt; **Recommendations**.
3. Review the recommendation **description**, **severity**, **device details** of all devices that issued this recommendation in the aggregation period.
4. After reviewing recommendation specifics, use the **manual remediation step** instructions to help remediate and resolve the issue that caused the recommendation.

    [![Remediate security recommendations with Defender for IoT](media/quickstart/remediate-security-recommendations-inline.png)](media/quickstart/remediate-security-recommendations-expanded.png#lightbox)
5. Explore the recommendation details for a specific device by selecting the desired device in the drill-down page.

    [![Investigate specific security recommendations for a device with Defender for IoT](media/quickstart/explore-security-recommendation-detail-inline.png)](media/quickstart/explore-security-recommendation-detail-expanded.png#lightbox)

## Investigate recommendations in a Log Analytics workspace

**To access your recommendations in a Log Analytics workspace**:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Navigate to **IoT Hub** &gt; **`Your hub`** &gt; **Defender for IoT** &gt; **Recommendations**.
3. Select a recommendation from the list.
4. Select **Investigate recommendations in Log Analytics workspace**.

    ![Screenshot showing how to view a recommendation in the log analytics workspace.](media/how-to-configure-agent-based-solution/recommendation-alert.png)

For more information on querying data from Log Analytics, see [Get started with log queries in Azure Monitor](/en-us/azure/azure-monitor/logs/get-started-queries).

## Clean up resources

There are no resources to clean up.