---
layout: Conceptual
title: Defender for IoT micro agent troubleshooting - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/device-builders/troubleshoot-defender-micro-agent
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
description: Learn how to handle unexpected or unexplained errors.
ms.date: 2021-11-09T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: 1c57a92c-ceea-3d72-2d9f-f3a4f28f2c88
document_version_independent_id: c740c04c-0d80-e013-8a6d-ff8c0415c193
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/device-builders/troubleshoot-defender-micro-agent.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/device-builders/troubleshoot-defender-micro-agent
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/device-builders/troubleshoot-defender-micro-agent.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 6155068c-5160-a4e7-3f83-3123398d55e4
---

# Defender for IoT micro agent troubleshooting - Microsoft Defender for IoT | Microsoft Learn

If an unexpected error occurs, you can use these troubleshooting methods in an attempt to resolve the issue.

Note

Defender for IoT plans to retire the micro agent on June 1, 2027.

## Service status

To view the status of the service:

1. Run the following command

    ```bash
    systemctl status defender-iot-micro-agent.service 
    ```
2. Check that the service is stable by making sure it's `active`, and that the uptime in the process is appropriate.

    ![Ensure your service is stable by checking to see that it's active and the uptime is appropriate.](media/troubleshooting/active-running.png)

If the service is listed as `inactive`, use the following command to start the service:

```bash
systemctl start defender-iot-micro-agent.service 
```

You will know that the service is crashing if, the process uptime is less than 2 minutes. To resolve this issue, you must review the logs.

## Validate micro agent root privileges

Use the following command to verify that the Defender for IoT micro agent service is running with root privileges.

```bash
ps -aux | grep "defender_iot_micro_agent"
```

The following sample result shows that the folder 'defender\_iot\_micro\_agent' has root privileges due to the word 'root' appearing as shown by the red box.

![Verify the Defender for IoT micro agent service is running with root privileges.](media/troubleshooting/root-privileges.png)

## Review the logs

To review the logs, use the following command: 

```bash
sudo journalctl -u defender-iot-micro-agent | tail -n 200 
```

### Quick log review

If an issue occurs when the micro agent is run, you can run the micro agent in a temporary state, which will allow you to view the logs using the following command:

```bash
sudo systectl stop defender-iot-micro-agent
cd /etc/defender_iot_micro_agent/
sudo ./defender_iot_micro_agent
```

## Restart the service

To restart the service, use the following command:

```bash
sudo systemctl restart defender-iot-micro-agent 
```