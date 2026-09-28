---
layout: Conceptual
title: Investigate security alerts - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/tutorial-investigate-security-alerts
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
description: Learn how to investigate Defender for IoT security alerts on your IoT devices.
ms.topic: tutorial
ms.date: 2022-01-13T00:00:00.0000000Z
locale: en-us
document_id: f7719bba-3f23-1e36-53ec-db9a239353cb
document_version_independent_id: ab50f701-541a-86d4-8779-e9435ad21883
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/tutorial-investigate-security-alerts.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/tutorial-investigate-security-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/tutorial-investigate-security-alerts.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/816835a3-1c5d-4536-835c-4b59dc9c9d97
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/a98c4e96-5248-4755-860b-6c76f1933f0c
platformId: 07d88772-e3ce-b5df-1774-734616de5be7
---

# Investigate security alerts - Microsoft Defender for IoT | Microsoft Learn

This tutorial will help you learn how to investigate, and remediate the alerts issued by Defender for IoT. Remediating alerts is the best way to ensure compliance, and protection across your IoT solution.

In this tutorial you'll learn how to:

- Investigate security alerts
- Investigate security alert details
- Investigate alerts in Log Analytics workspace

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
- Learned how to [investigate security recommendations](quickstart-investigate-security-recommendations).

## Investigate security alerts

The Defender for IoT security alert list displays all of the aggregated security alerts for your IoT Hub.

**To investigate security alerts**:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Navigate to **IoT Hub** &gt; **`Your hub`** &gt; **Defender for IoT** &gt; **Security Alerts**.
3. Select an alert from the list to open the alert's details.

## Investigate security alert details

Opening each aggregated alert displays the detailed alert description, remediation steps, and device ID for each device that triggered an alert. The alert severity and direct investigation is accessible using Log Analytics.

**To investigate security alert details**:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Navigate to **IoT Hub** &gt; **`Your hub`** &gt; **Defender for IoT** &gt; **Security Alerts**.
3. Select any security alert from the list to open it.
4. Review the alert **description**, **severity**, **source of the detection**, and **device details** of all devices that issued this alert in the aggregation period.

    [![Investigate and review the details of each device in an aggregated alert.](media/quickstart/drill-down-iot-alert-details.png)](media/quickstart/drill-down-iot-alert-details-expanded.png#lightbox)
5. After reviewing the alert specifics, use the **manual remediation step** instructions to help remediate and resolve the issue that caused the alert.

    ![Follow the manual remediation steps to help resolve or remediate your device security alerts](media/quickstart/iot-alert-manual-remediation-steps.png)

## Investigate alerts in your Log Analytics workspace

You can access your alerts and investigate them with the Log Analytics workspace.

**To access your alerts in your Log Analytics workspace after configuration**:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Navigate to **IoT Hub** &gt; **`Your hub`** &gt; **Defender for IoT** &gt; **Security Alerts**.
3. Select an alert.
4. Select **Investigate alerts in Log Analytics workspace**.

    ![Screenshot that shows where to select to investigate in the log analytics workspace.](media/how-to-configure-agent-based-solution/log-analytic.png)