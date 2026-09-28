---
layout: Conceptual
title: 'Quickstart: Enable Microsoft Defender for IoT on your Azure IoT Hub - Microsoft Defender for IoT | Microsoft Learn'
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/quickstart-onboard-iot-hub
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
description: Learn how to enable Defender for IoT in an Azure IoT hub.
ms.topic: quickstart
ms.date: 2022-01-16T00:00:00.0000000Z
ms.custom: mode-other
locale: en-us
document_id: 23c5f002-b1a3-c05f-6194-ea5e1bb6f815
document_version_independent_id: 8ef04890-a1e7-7eda-5f9d-63fd77efead8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/quickstart-onboard-iot-hub.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/quickstart-onboard-iot-hub
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/quickstart-onboard-iot-hub.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/816835a3-1c5d-4536-835c-4b59dc9c9d97
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/a98c4e96-5248-4755-860b-6c76f1933f0c
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: d376e576-2624-8d7c-0d90-c6d30ec0815a
---

# Quickstart: Enable Microsoft Defender for IoT on your Azure IoT Hub - Microsoft Defender for IoT | Microsoft Learn

This article explains how to enable Microsoft Defender for IoT on an Azure IoT hub.

[Azure IoT Hub](/en-us/azure/iot-hub/iot-concepts-and-iot-hub) is a managed service that acts as a central message hub for communication between IoT applications and IoT devices. You can connect millions of devices and their backend solutions reliably and securely. Almost any device can be connected to an IoT Hub. Defender for IoT integrates into Azure IoT Hub to provide real-time monitoring, recommendations, and alerts.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- The ability to create a standard tier IoT Hub.
- For the resource group and access management setup process, you need the following roles:

    - To add role assignments, you need the Owner, Role Based Access Control Administrator and User Access Administrator roles.
    - To register resource providers, you need th Owner and Contributor roles.

    Learn more about [privileged administrator roles in Azure](/en-us/azure/role-based-access-control/role-assignments-steps#privileged-administrator-roles).

Note

Defender for IoT currently only supports standard tier IoT Hubs.

## Create an IoT Hub with Microsoft Defender for IoT

You can create a hub in the Azure portal. For all new IoT hubs, Defender for IoT is set to **On** by default.

**To create an IoT Hub**:

1. Follow the steps to [create an IoT hub using the Azure portal](/en-us/azure/iot-hub/iot-hub-create-through-portal#create-an-iot-hub).
2. Under the **Management** tab, ensure that **Defender for IoT** is set to **On**. By default, Defender for IoT will be set to **On** .

    ![Ensure the Defender for IoT toggle is set to on.](media/quickstart-onboard-iot-hub/management-tab.png)
3. Follow these steps to allow access to the IoT Hub.

## Enable Defender for IoT on an existing IoT Hub

You can onboard Defender for IoT to an existing IoT Hub, where you can then monitor the device identity management, device to cloud, and cloud to device communication patterns.

**To enable Defender for IoT on an existing IoT Hub**:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Follow these steps to allow access to the IoT Hub.
3. Navigate to **IoT Hub** &gt; **`Your hub`** &gt; **Defender for IoT** &gt; **Overview**.
4. Select **Secure your IoT solution**, and complete the onboarding form.

    [![Select the secure your IoT solution button to secure your solution.](media/quickstart-onboard-iot-hub/secure-your-iot-solution.png)](media/quickstart-onboard-iot-hub/secure-your-iot-solution-expanded.png#lightbox)

    The **Secure your IoT solution** button will only appear if the IoT Hub hasn't already been onboarded, or if you set the Defender for IoT toggle to **Off** while onboarding.

    ![If your toggle was set to off during onboarding.](media/quickstart-onboard-iot-hub/toggle-is-off.png)

## Verify that Defender for IoT is enabled

**To verify that Defender for IoT is enabled**:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Navigate to **IoT Hub** &gt; **`Your hub`** &gt; **Defender for IoT** &gt; **Overview**.

    The Threat prevention and Threat detection screen will appear.

    [![Screenshot showing that Defender for IoT is enabled.](media/quickstart-onboard-iot-hub/threat-prevention.png)](media/quickstart-onboard-iot-hub/threat-prevention-expanded.png#lightbox)

## Configure data collection

Configure data collection settings for Defender for IoT in your IoT hub, such as a Log Analytics workspace and other advanced settings.

**To configure Defender for IoT data collection**:

1. In your IoT hub, select **Defender for IoT &gt; Settings**. The **Enable Microsoft Defender for IoT** option is toggled on by default.
2. In the **Workspace configuration** area, toggle the **On** option to connect to a Log Analytics workspace, and then select the Azure subscription and Log Analytics workspace you want to connect to.

    If you need to create a new workspace, select the **Create New Workspace** link.

    Select **Access to raw security data** to export raw security events from your devices to the Log Analytics workspace that you'd selected above.
3. In the **Advanced settings** area, the following options are selected by default. Clear the selection as needed:

    - **In-depth security recommendations and custom alerts**. Allows Defender for IoT access to the device's twin data in order to generate alerts based on that data.
    - **IP data collection**. Allows Defender for IoT access to the device's incoming and outgoing IP addresses to generate alerts based on suspicious connections.
4. Select **Save** to save your settings.

## Set up resource providers and access control

To set up permissions needed to access the IoT hub:

1. Set up resource providers and access control for the IoT hub.
2. To allow access to a Log Analytics workspace, also set up resource providers and access control for Log Analytics workspace.

Learn more about [resource providers and resource types](/en-us/azure/azure-resource-manager/management/resource-providers-and-types#register-resource-provider).

### Allow access to the IoT Hub

To allow access to the IoT Hub:

#### Set up resource providers for the IoT hub

1. Sign in to the [Azure portal](https://portal.azure.com/) and navigate to the **Subscriptions** page.
2. In the subscriptions table, select your subscription.
3. In the subscription page that opens, from the left menu bar, select **Resource providers**.
4. In the search bar, type: *Microsoft.iot*.
5. Select the **Microsoft.IoTSecurity** provider and verify that its status is **Registered**.

#### Set up access control for the IoT hub

1. In your IoT hub's resource group, from the left menu bar, select **Access control (IAM)**, and from the top menu, select **Add &gt; Add role assignment**.
2. In the **Role tab**, select the **Privileged administrator roles** tab, and select the **Contributor** role.
3. Select the **Members** tab, and next to **Members**, select **Select members**.
4. In the **Select members** page, in the **Select** field, type *Azure security*, select **Azure Security for IoT**, and select **Select** at the bottom.
5. Back in the **Members** tab, select **Review + assign** at the bottom of the tab, in the **Review and assign tab**, select **Review + assign** at the bottom again.

### Allow access to a Log Analytics workspace

To connect to a Log Analytics workspace:

#### Set up resource providers for the Log Analytics workspace

1. In the Azure portal, navigate to the **Subscriptions** page.
2. In the subscriptions table, select your subscription.
3. In the subscription page that opens, from the left menu bar, select **Resource providers**.
4. In the search bar, type: *Microsoft.OperationsManagement*.
5. Select the **Microsoft.OperationsManagement** provider and verify that its status is **Registered**.

#### Set up access control for the Log Analytics workspace

1. In the Azure portal, search for and navigate to the **Log analytics workspaces** page, select your workspace, and from the left menu, select **Access control (IAM)**.
2. From the top menu, select **Add &gt; Add role assignment**.
3. In the **Role tab**, under **Job function roles**, search for *Log analytics*, and select the **Log Analytics Contributor** role.
4. Select the **Members** tab, and next to **Members**, select **Select members**.
5. In the **Select members** page, in the **Select** field, type *Azure security*, select **Azure Security for IoT**, and select **Select** at the bottom.
6. Back in the **Members** tab, select **Review + assign** at the bottom of the tab, in the **Review and assign tab**, select **Review + assign** at the bottom again.

#### Enable Defender for IoT

1. In your IoT hub, from the left menu, select **Settings**, and in the **Settings page**, select **Data Collection**.
2. Toggle on **Enable Microsoft Defender for IoT**, and select **Save** at the bottom.
3. Under **Choose the Log Analytics workspace you want to connect to**, set the toggle to **On**.
4. Select the subscription for which you set up the resource provider and workspace.