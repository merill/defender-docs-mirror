---
layout: Conceptual
title: Install the Microsoft Defender for IoT micro agent - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/tutorial-standalone-agent-binary-installation
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
description: Learn how to install and authenticate the Defender for IoT micro agent.
ms.date: 2022-04-26T00:00:00.0000000Z
ms.topic: tutorial
ms.custom:
- mode-other
- sfi-ropc-blocked
locale: en-us
document_id: 4c92ad57-8656-92bd-c4de-326ac2d6f8dc
document_version_independent_id: 8ea91e77-0004-3573-adad-1cd528f8585b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/tutorial-standalone-agent-binary-installation.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/tutorial-standalone-agent-binary-installation
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/tutorial-standalone-agent-binary-installation.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/816835a3-1c5d-4536-835c-4b59dc9c9d97
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/a98c4e96-5248-4755-860b-6c76f1933f0c
platformId: b278afa8-8bf8-497d-d96f-ed16b324a2be
---

# Install the Microsoft Defender for IoT micro agent - Microsoft Defender for IoT | Microsoft Learn

This tutorial will help you learn how to install and authenticate the Defender for IoT micro agent.

In this tutorial you'll learn how to:

- Download and install the micro agent
- Authenticate the micro agent
- Validate the installation
- Test the system
- Install a specific micro agent version

Note

Defender for IoT plans to retire the micro agent on June 1, 2027.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- An [IoT hub](/en-us/azure/iot-hub/iot-hub-create-through-portal).
- Verify you're running one of the following [operating systems](concept-agent-portfolio-overview-os-support).
- You must have [enabled Microsoft Defender for IoT on your Azure IoT Hub](quickstart-onboard-iot-hub).
- You must have [added a resource group to your IoT solution](quickstart-configure-your-solution).
- You must have [created a Defender for IoT micro agent module twin](quickstart-create-micro-agent-module-twin).

## Download and install the micro agent

Depending on your setup, the appropriate Microsoft package will need to be installed.

**To add the appropriate Microsoft package repository**:

1. Download the repository configuration that matches your device operating system.

    - For Ubuntu 18.04:

        ```bash
        curl https://packages.microsoft.com/config/ubuntu/18.04/multiarch/prod.list > ./microsoft-prod.list
        ```
    - For Ubuntu 20.04:

        ```bash
            curl https://packages.microsoft.com/config/ubuntu/20.04/prod.list > ./microsoft-prod.list
        ```
    - For Debian 9 (both AMD64 and ARM64):

        ```bash
        curl https://packages.microsoft.com/config/debian/stretch/multiarch/prod.list > ./microsoft-prod.list
        ```
2. Use the following command to copy the repository configuration to the `sources.list.d` directory:

    ```bash
    sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
    ```
3. Install the Microsoft GPG public key with the following command:

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
    sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
    ```
4. Ensure that you've updated the apt using the following command:

    ```bash
    sudo apt-get update
    ```
5. Use the following command to install the Defender for IoT micro agent package on Debian, or Ubuntu based Linux distributions:

    ```bash
    sudo apt-get install defender-iot-micro-agent 
    ```

## Connect via a proxy

This procedure describes how you can connect the Defender for IoT micro agent to the IoT Hub via a proxy.

**To configure connections via a proxy**:

1. On your micro agent machine, create a `/etc/defender_iot_micro_agent/conf.json` file with the following content:

    ```json
    {
        "IothubModule_ProxyConfig": "<proxy_ipv4>,<port>,<username>,<password>",
        "IothubModule_TransportProtocol": "MQTT_WebSocket_Protocol"
    }
    ```

    User and password fields are optional. If you don't need them, use the following syntax instead:

    ```json
    {
        "IothubModule_ProxyConfig": "<proxy_ipv4>,<port>",
        "IothubModule_TransportProtocol": "MQTT_WebSocket_Protocol"
    }
    
    ```
2. Delete any cached file at **/var/lib/defender\_iot\_micro\_agent/cache.json**.
3. Restart the micro agent. Run:

    ```bash
    sudo systemctl restart defender-iot-micro-agent.service
    ```

## Add AMQP protocol support

This procedure describes additional steps required to support the AMQP protocol.

**To add AMQP protocol support**:

1. On your micro agent machine, open the `/etc/defender_iot_micro_agent/conf.json` file and add the following content:

    ```json
    {
    "IothubModule_TransportProtocol": "AMQP_Protocol"
    }
    ```
2. Delete any cached file at **/var/lib/defender\_iot\_micro\_agent/cache.json**.
3. Restart the micro agent. Run:

    ```bash
    sudo systemctl restart defender-iot-micro-agent.service
    ```

**To add AMQP over web socket protocol support**:

1. On your micro agent machine, open the `/etc/defender_iot_micro_agent/conf.json` file and add the following content:

    ```json
    {
    "IothubModule_TransportProtocol": "AMQP_WebSocket_Protocol"
    }
    ```
2. Delete any cached file at **/var/lib/defender\_iot\_micro\_agent/cache.json**.
3. Restart the micro agent. Run:

    ```bash
    sudo systemctl restart defender-iot-micro-agent.service
    ```

The agent will use this protocol, and communicate with the IoT Hub on port 443. HTTP Proxy configuration is supported for this protocol, in the case that proxy is also configured, the port of communication with the proxy will be as defined in the proxy configuration.

## Authenticate the micro agent

There are two options that can be used to authenticate the Defender for IoT micro agent:

- Authenticate using a module identity connection string.
- Authenticate using a certificate.

### Authenticate using a module identity connection string

You will need to copy the module identity connection string from the DefenderIoTMicroAgent module identity details.

**To copy the module identity's connection string**:

1. Navigate to the **IoT Hub** &gt; **`Your hub`** &gt; **Device management** &gt; **Devices**.

    ![Select IoT devices from the left-hand menu.](media/quickstart-standalone-agent-binary-installation/iot-devices.png)
2. Select a device from the Device ID list.
3. Select the **Module Identities** tab.
4. Select the **DefenderIotMicroAgent** module from the list of module identities associated with the device.

    ![Select the module identities tab.](media/quickstart-standalone-agent-binary-installation/module-identities.png)
5. Copy the Connection string (primary key) by selecting the **copy** button.

    ![Select the copy button to copy the Connection string (primary key).](media/quickstart-standalone-agent-binary-installation/copy-button.png)
6. Create a file named `connection_string.txt` containing the copied connection string encoded in utf-8 in the Defender for IoT agent directory `/etc/defender_iot_micro_agent` path by entering the following command:

    ```bash
    sudo bash -c 'echo "<connection string>" > /etc/defender_iot_micro_agent/connection_string.txt'
    ```

    The `connection_string.txt` will now be located in the following path location `/etc/defender_iot_micro_agent/connection_string.txt`.

    Note

    The connection string includes a key that enables direct access to the module itself, therefore includes sensitive information that should only be used and readable by root users.
7. Restart the service using this command:

    ```bash
    sudo systemctl restart defender-iot-micro-agent.service 
    ```

### Authenticate using a certificate

**To authenticate using a certificate**:

1. Procure a certificate by following [these instructions](/en-us/azure/iot-hub/tutorial-x509-scripts).
2. Place the PEM-encoded public part of the certificate, and the private key, in `/etc/defender_iot_micro_agent`, to files called `certificate_public.pem`, and `certificate_private.pem`.
3. Place the appropriate connection string in to the `connection_string.txt` file. The connection string should look like this:

    `HostName=<the host name of the iot hub>;DeviceId=<the id of the device>;ModuleId=<the id of the module>;x509=true`

    This string alerts the Defender for IoT agent to expect a certificate to be provided for authentication.
4. Restart the service using the following command:

    ```bash
    sudo systemctl restart defender-iot-micro-agent.service
    ```

## Validate the installation

**To validate your installation**:

1. Use the following command to ensure the micro agent is running properly:

    ```bash
    systemctl status defender-iot-micro-agent.service
    ```
2. Ensure that the service is stable by making sure it's `active`, and that the uptime of the process is appropriate.

    ![Check to make sure your service is stable and active.](media/quickstart-standalone-agent-binary-installation/active-running.png)

## Test the system

You can test the system by creating a trigger file on the device. The trigger file will cause the baseline scan in the agent to detect the file as a baseline violation.

1. Create a file on the file system with the following command:

    ```bash
    sudo touch /tmp/DefenderForIoTOSBaselineTrigger.txt
    ```
2. Make sure that your Log Analytics workspace is attached to your IoT hub. For more information, see [Create a log analytics workspace](tutorial-configure-agent-based-solution#create-a-log-analytics-workspace).
3. Restart the agent using the command:

    ```bash
    sudo systemctl restart defender-iot-micro-agent.service
    ```

Allow up to one hour for the recommendation to appear in the hub.

A baseline recommendation called 'IoT\_CISBenchmarks\_DIoTTest' is created. You can query this recommendation from Log Analytics as follows:

```kusto
SecurityRecommendation

| where RecommendationName contains "IoT_CISBenchmarks_DIoTTest"

| where DeviceId contains "<device-id>"

| top 1 by TimeGenerated desc
```

For example:

![Screenshot of the IoT_CISBenchmarks_DIoTTest query run in Log Analytics.](media/tutorial-standalone-agent-binary-installation/iot_cisbenchmarks_diottest.png)

## Install a specific micro agent version

You can install a specific version of the micro agent using a specific command.

**To install a specific version of the Defender for IoT micro agent**:

1. Open a terminal.
2. Run the following command:

    ```bash
    sudo apt-get install defender-iot-micro-agent=<version>
    ```

## Clean up resources

There are no resources to clean up.