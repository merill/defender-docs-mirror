---
layout: Conceptual
title: Create a learned baseline of OT traffic - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/ot-deploy/create-learned-baseline
breadcrumb_path: ../../breadcrumb/toc.json
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
description: Learn about how to create a baseline of learned traffic on your OT sensor.
ms.date: 2023-01-22T00:00:00.0000000Z
ms.topic: install-set-up-deploy
locale: en-us
document_id: 31638c62-d861-9dce-1f58-ea4144b45249
document_version_independent_id: 22209af2-9453-dde4-2fd7-8a27d6d97ee4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/ot-deploy/create-learned-baseline.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/ot-deploy/create-learned-baseline
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/ot-deploy/create-learned-baseline.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
platformId: 71e76a39-f288-6c18-a411-cfe8bbb5cb7c
---

# Create a learned baseline of OT traffic - Microsoft Defender for IoT | Microsoft Learn

This article is one in a series of articles describing the [deployment path](ot-deploy-path) for OT monitoring with Microsoft Defender for IoT, and describes how to create a baseline of learned traffic on your OT sensor.

[![Diagram of a progress bar with Fine-tune OT monitoring highlighted.](../media/deployment-paths/progress-fine-tuning-ot-monitoring.png)](../media/deployment-paths/progress-fine-tuning-ot-monitoring.png#lightbox)

## Overview of the multi stage monitoring process

An OT network sensor starts monitoring your network automatically after it connects to the network and you [sign in](activate-deploy-sensor#sign-in-to-the-sensor-console-and-change-the-default-password). Network devices start appearing in your device inventory, and [alerts](../alerts) are triggered for any security or operational incidents that occur in your network.

Defender for IoT employs a three stage monitoring process that learns your network's normal traffic behavior. These three stages ensure accurate detection while reducing unnecessary alerts, are:

1. Learning mode
2. Dynamic mode
3. Operational mode

### Summary of the monitoring stages

| Mode | Purpose | Trigger alerts | User actions needed |
| --- | --- | --- | --- |
| **Learning** | Builds a baseline of normal network traffic | Malware alerts, anomaly alerts, operational alerts, protocol violation alerts | Turn off manually after 2–6 weeks or when baseline reflects accurate network activity |
| **Dynamic** | Refines the baseline while gradually introducing Policy Violations alerts to ensure accuracy and reduce alert noise | Policy Violation alerts are introduced | Optional: Adjust settings for specific scenarios (e.g. during POCs) |
| **Operational** | Monitors all network traffic with a stable baseline, triggering all alerts to reflect deviations or suspicious activity | All types of alerts | None. Automatically transitions when baseline stabilizes |

### Learning mode

Initially, the sensor runs in *learning* mode to monitor all of your network traffic and build a baseline of all normal traffic patterns. This baseline includes all of the devices and protocols in your network, and the regular file transfers that occur between devices. This process normally takes between 2 and 6 weeks, depending on your network size and complexity. Additionally, any devices discovered later enter learning mode for 7 days in order to establish their network traffic baseline.

In learning mode, the sensor monitors and protects your environment by triggering relevant security alerts, such as malware, anomaly and operational alerts. However, Policy Violation alerts, which indicate deviations from the baseline, aren't triggered while the system is in learning mode.

### Dynamic mode

Once the discovery process and network traffic are stable, you should manually turn off learning mode. At this point, the sensor transitions to dynamic mode. In dynamic mode the sensor continues to monitor your network, validating and refining the baseline. The sensor assesses each alert category and scenario individually, dynamically changing them to operational mode when their baselines are confirmed to be accurate. Alternatively, if the sensor detects significant changes in traffic, it might automatically extend the learning mode for specific alerts or scenarios.

In dynamic mode, Policy Violation alerts are gradually introduced and start to appear in the alert inventory.

### Operational mode

Once the sensor identifies that the baseline is stable and complete it automatically transitions into operational mode, monitoring all of the network traffic and triggering all alert types.

The **Learn** action becomes relevant after learning mode is turned off, when the scenario transitions to operational mode, and you wish to mark specific operations as authorized or expected activity. Once learned, similar activity won't generate new alerts in the future.

[Turn off learning mode manually](../how-to-manage-individual-sensors#turn-off-learning-mode-manually) when the level of alerts accurately reflect your network activity.

For more information, see [Microsoft Defender for IoT alerts](../alerts).

## Prerequisites

You can perform the procedures in this article from the Azure portal or an OT sensor.

Before you start, make sure that you have:

- An OT sensor [installed](install-software-ot-sensor), [configured, and activated](activate-deploy-sensor), with alerts triggered by detected traffic.
- Access to your OT sensor as **Security Analyst** or **Admin** user. For more information, see [On-premises users and roles for OT monitoring with Defender for IoT](../roles-on-premises).

## Triage alerts

Triage alerts towards the end of your deployment to create an initial baseline for your network activity.

1. Sign into your OT sensor and select the **Alerts** page.
2. Use sorting and grouping options to view your most critical alerts first. Review each alert to update statuses and learn alerts for OT authorized traffic.

For more information, see [View and manage alerts on your OT sensor](../how-to-view-alerts).