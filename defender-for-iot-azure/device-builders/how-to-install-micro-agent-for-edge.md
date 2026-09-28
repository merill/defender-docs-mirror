---
layout: Conceptual
title: Install Defender for IoT Micro Agent for Microsoft Edge - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/how-to-install-micro-agent-for-edge
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
description: Learn how to install, and authenticate the Defender Micro agent for Microsoft Edge.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 39eb36db-ca92-7c54-1a52-ca6343cab168
document_version_independent_id: e4e44b71-ab26-28da-3119-f08c2f925957
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/how-to-install-micro-agent-for-edge.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/how-to-install-micro-agent-for-edge
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/how-to-install-micro-agent-for-edge.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5287f575-02f0-405f-92b7-800456526b0c
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/816835a3-1c5d-4536-835c-4b59dc9c9d97
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/06e86142-34c2-4b94-ab9c-9477c21f7152
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/a98c4e96-5248-4755-860b-6c76f1933f0c
platformId: 4ef54c11-07ba-875d-b3f9-af81a089eccd
---

# Install Defender for IoT Micro Agent for Microsoft Edge - Microsoft Defender for IoT | Microsoft Learn

This article explains how to install and set up the Defender micro agent for Edge. The micro agent runs as a module on Azure IoT Edge devices. It monitors security threats and helps manage your IoT security posture. Before you begin, make sure you complete the prerequisites. You'll learn how to add the required package sources, install the agent on Debian and Ubuntu-based Linux systems, and check that it works.

Note

Defender for IoT plans to retire the micro agent on June 1, 2027.

## Prerequisites

Before you install the Defender micro agent for Edge, complete the following prerequisites:

1. Navigate to your IoT Hub or, [create a new IoT hub](/en-us/azure/iot-hub/iot-hub-create-through-portal#create-an-iot-hub).
2. [Register an IoT Edge device in IoT Hub](/en-us/azure/iot-edge/how-to-register-device) and [retrieve the device connection strings](/en-us/azure/iot-edge/how-to-register-device#view-registered-devices-and-retrieve-connection-strings).
3. Add the appropriate Microsoft package repository.
4. Download the repository configuration that matches your device operating system.

    - For Ubuntu 18.04:

        ```bash
        curl https://packages.microsoft.com/config/ubuntu/18.04/multiarch/prod.list > ./microsoft-prod.list
        ```
    - For Ubuntu 20.04

        ```bash
        curl https://packages.microsoft.com/config/ubuntu/20.04/prod.list > ./microsoft-prod.list
        ```
    - For Debian 9 (both AMD64 and ARM64)

        ```bash
        curl https://packages.microsoft.com/config/debian/stretch/multiarch/prod.list > ./microsoft-prod.list
        ```
5. Copy the repository configuration to the `sources.list.d` directory.

    ```bash
    sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
    ```
6. Update the list of packages from the repository that you added with the following command:

    ```bash
    sudo apt-get update
    ```
7. Install and configure [Edge runtime version 1.2](/en-us/azure/iot-edge/how-to-install-iot-edge)

## Install the Defender for IoT micro agent for Edge

Perform the following steps to install and validate the Defender for IoT micro agent on supported Linux distributions.

1. Install the Defender micro agent package. Run the following command on Debian or Ubuntu-based Linux systems:

    ```bash
    sudo apt-get install defender-iot-micro-agent-edge
    ```
2. Validate your installation.

    1. Ensure the micro agent is running properly with the following command:

        ```bash
        systemctl status defender-iot-micro-agent.service
        ```
    2. Ensure that the service is stable by making sure it's `active` and that the uptime of the process is appropriate

        ![Check to make sure your service is stable and active.](media/quickstart-standalone-agent-binary-installation/active-running.png)
3. Test the system end-to-end by creating a trigger file on the device. The trigger file causes a baseline scan in the agent that detects the file as a baseline violation.

    Create a file on the file system with the following command:

    ```bash
    sudo touch /tmp/DefenderForIoTOSBaselineTrigger.txt 
    ```

    A baseline validation failure recommendation occurs in the hub, with a `CceId` of `CIS-debian-9-DEFENDER_FOR_IOT_TEST_CHECKS-0.0`:

    [![The baseline validation failure recommendation that occurs in the hub.](media/quickstart-standalone-agent-binary-installation/validation-failure.png)](media/quickstart-standalone-agent-binary-installation/validation-failure-expanded.png#lightbox)

    Allow up to one hour for the baseline validation failure recommendation to appear in your IoT Hub.
4. Install a specific version of the Defender IoT micro agent, use the following command:

    ```bash
    sudo apt-get install defender-iot-micro-agent-edge=<version>
    ```