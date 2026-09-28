---
layout: Conceptual
title: Set up traffic mirroring - Defender for IoT - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/traffic-mirroring/set-up-traffic-mirroring
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
description: A quick guide for the correct placement and mirroring of the OT sensor in your network for Microsoft Defender for IoT.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: bfb70df9-1407-4262-26ac-a121d4c57146
document_version_independent_id: 4dbd942d-3b55-c1bb-26cf-14435d596d15
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/traffic-mirroring/set-up-traffic-mirroring.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/traffic-mirroring/set-up-traffic-mirroring
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/traffic-mirroring/set-up-traffic-mirroring.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: 3974b554-a634-01ac-8ae0-d825fb9d7318
---

# Set up traffic mirroring - Defender for IoT - Microsoft Defender for IoT | Microsoft Learn

This article provides a step-by-step guide to deploying your Microsoft Defender for IoT OT network sensor, ensuring the correct traffic mirroring options are chosen to achieve accurate and reliable network data collection. It covers reviewing your network architecture, selecting sensor locations and a mirroring method (such as SPAN or TAP), validating the sensor placement, and confirming monitoring after deployment.

## Review the network architecture

Before you deploy the sensor to the network, review the following network architecture tasks:

- Review the network diagram. For more information, see [Review OT network architecture](../best-practices/understand-network-architecture) or [Create an OT network diagram](../best-practices/plan-prepare-deploy#create-a-network-diagram).
- Estimate the total number of devices to be monitored. For more information, see [Calculate devices in your OT network](../best-practices/plan-prepare-deploy#calculate-devices-in-your-network).
- Identify VLANs that contain OT networks. For more information, see [Customize a VLAN name for monitored traffic](../how-to-control-what-traffic-is-monitored#customize-a-vlan-name).
- Determine which OT protocols need to be monitored (Profinet, S7, Modbus, etc.). For more information, see [OT sensor supported protocols](../concept-supported-protocols).

## Select the sensor locations and traffic mirroring method

Based on your network architecture and selected traffic mirroring approach (such as SPAN or TAP), select the best locations for your network sensors to ensure that they capture the necessary Layer 2 (L2) traffic.

Compile a list all of the locations in the network where the sensors should be placed. For more information, see [Identify interesting OT network traffic points](../best-practices/understand-network-architecture#identifying-interesting-traffic-points).

## Validate the sensor location

After deciding on a potential location for the sensor, validate the presence of Layer 2 (L2) and operational technology (OT) protocols. It's recommended to use tools like Wireshark to verify these protocols at the potential sensor location. For example:

![Screenshot of the wireshark program used to confirm and validate OT sensor set up and network protocols communicating with the newly deployed OT sensor.](media/guide/deployment-guide-analyzer.png)

Wireshark displays the list of protocols identified by the sensor and the amount of data being monitored, thereby validating the location of your sensor. If protocols don't appear or no data is detected, this result indicates that the sensor is incorrectly placed or set up in the network. For example:

![Screenshot of the wireshark program protocol output used to confirm and validate OT sensor set up and network protocols communicating with the newly deployed OT sensor.](media/guide/deployment-guide-protocols.png)

Validating the presence of L2 and OT protocols at the potential sensor location is crucial to ensure effective monitoring of your OT networks. For steps to validate traffic mirroring, see [Validate traffic mirroring](configure-mirror-span#validate-traffic-mirroring).

## Deploy your sensor

After validating the sensor and mirroring method, deploy the sensors. For more information, see [install software on OT sensors](../ot-deploy/install-software-ot-sensor).

## Validate after deployment

It's essential to validate the monitoring interfaces and activate them. We recommend using the Deployment tool in the sensor system setting to monitor the networks monitored by the sensor.

[![Screenshot of the OT sensor systems settings screen, highlighting the Deployment box to be used to help validate the post OT sensor deployment.](media/guide/deployment-guide-post-deployment-system-settings.png)](media/guide/deployment-guide-post-deployment-system-settings.png#lightbox)

To validate your sensor:

1. Verify that the number of devices in the inventory is reasonable.
2. Check the type classification for devices listed in the inventory.
3. Confirm the visibility of OT protocol names on the device's inventory.
4. Ensure L2 protocols are monitored by identifying MAC addresses in the inventory.

If device inventory data, OT protocol names, or MAC addresses don't appear, review the SPAN configuration and recheck the Deployment tool in the sensor, which provides visibility of the subnets monitored and the status of the OT protocols, for example:

[![Screenshot of the OT sensor Analyze feature screen used to help validate the post OT sensor deployment.](media/guide/deployment-guide-post-deployment-analyze.png)](media/guide/deployment-guide-post-deployment-analyze.png#lightbox)