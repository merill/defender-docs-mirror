---
layout: Conceptual
title: Which OT appliances do I need? - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/ot-appliance-sizing
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
description: Learn about the deployment options for Microsoft Defender for IoT sensors and on-premises management consoles.
ms.date: 2024-03-10T00:00:00.0000000Z
ms.topic: limits-and-quotas
locale: en-us
document_id: 49346943-5b3d-ce6c-9eba-186857437fcb
document_version_independent_id: 56c72172-6fcc-b6ba-f496-0e1cf59072f7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/ot-appliance-sizing.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/ot-appliance-sizing
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/ot-appliance-sizing.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: fb1fcb37-952f-715d-9c9a-5df47efe9dc5
---

# Which OT appliances do I need? - Microsoft Defender for IoT | Microsoft Learn

This article is one in a series of articles describing the [deployment path](ot-deploy/ot-deploy-path) for OT monitoring with Microsoft Defender for IoT, and is intended to help you choose the right appliances for your system and which hardware profile best fits your organization's network monitoring needs.

You can use [physical](ot-pre-configured-appliances) or [virtual](ot-virtual-appliances) appliances, or use the supplied specifications to purchase hardware on your own. For more information, see [Microsoft Defender for IoT - OT monitoring appliance reference | Microsoft Learn](appliance-catalog/). Results depend on hardware and resources available to the monitoring sensor.

[![Diagram of a progress bar with Plan and prepare highlighted.](media/deployment-paths/progress-plan-and-prepare.png)](media/deployment-paths/progress-plan-and-prepare.png#lightbox)

Important

The performance, capacity, and activity of an OT/IoT network may vary depending on its size, capacity, protocols distribution, and overall activity. For deployments, it is important to factor in raw network speed, the size of the network to monitor, and application configuration. The selection of processors, memory, and network cards is heavily influenced by these deployment configurations. The amount of space needed on your disk will differ depending on how long you store data, and the amount and type of data you store.

*Performance values are presented as upper thresholds under the assumption of intermittent traffic profiles, such as those found in OT/IoT systems and machine-to-machine communication networks.*

## IT/OT mixed environments

Use the following hardware profiles for high bandwidth corporate IT/OT mixed networks:

| Hardware profile | SPAN/TAP throughput | Max monitored Assets | Deployment |
| --- | --- | --- | --- |
| C5600 | Up to 3 Gbps | 12 K | Physical / Virtual |

## Monitoring at the site level

Use the following hardware profiles for enterprise monitoring at the site level, typically collecting multiple traffic feeds:

| Hardware profile | SPAN/TAP throughput | Max monitored assets | Deployment |
| --- | --- | --- | --- |
| E1800 | Up to 1 Gbps | 10K | Physical / Virtual |
| E1000 | Up to 1 Gbps | 10K | Physical / Virtual |
| E500 | Up to 1 Gbps | 10K | Physical / Virtual |

## Production line monitoring (medium and small deployments)

Use the following hardware profiles for production line monitoring, typically in the production/mission-critical environments:

| Hardware profile | SPAN/TAP throughput | Max monitored assets | Deployment |
| --- | --- | --- | --- |
| L500 | Up to 200 Mbps | 1,000 | Physical / Virtual |
| L100 | Up to 10 Mbps | 800 | Physical / Virtual |

Important

Defender for IoT software versions require a minimum disk size of 100 GB. The L60 hardware profile, which only supports 60 GB of hard disk, has been deprecated.

If you have a legacy sensor, such as the L60 hardware profile, you can migrate it to a supported profile can be found by following the [back up and restore a sensor](back-up-restore-sensor) process.