---
layout: Conceptual
title: Plan your OT monitoring system with Defender for IoT - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/best-practices/plan-corporate-monitoring
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
description: Learn how to plan your overall OT network monitoring structure and requirements.
ms.topic: install-set-up-deploy
ms.date: 2023-02-16T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: 259bb486-5d07-1409-040e-495c402cc798
document_version_independent_id: 22081022-4ce1-c651-18a6-6c2d1c69185f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/best-practices/plan-corporate-monitoring.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/best-practices/plan-corporate-monitoring
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/best-practices/plan-corporate-monitoring.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 44a2691f-b00e-2e96-5d9b-2d546c8deac7
---

# Plan your OT monitoring system with Defender for IoT - Microsoft Defender for IoT | Microsoft Learn

This article is one in a series of articles describing the [deployment path](../ot-deploy/ot-deploy-path) for OT monitoring with Microsoft Defender for IoT.

Use the content below to learn how to plan your overall OT monitoring with Microsoft Defender for IoT, including the sites you're going to monitor, your user groups and types, and more.

[![Diagram of a progress bar with Plan and prepare highlighted.](../media/deployment-paths/progress-plan-and-prepare.png)](../media/deployment-paths/progress-plan-and-prepare.png#lightbox)

## Prerequisites

Before you start planning your OT monitoring deployment, make sure that you have an Azure subscription and an OT plan onboarded to Defender for IoT. For more information, see [Manage Defender for IoT plans for OT monitoring](../how-to-manage-subscriptions).

This step is performed by your architecture teams.

## Plan OT sites and zones

When working with OT networks, we recommend that you list all of the locations where your organization has resources connected to a network, and then segment those locations out into *sites* and *zones*.

Each physical location can have its own site, which is further segmented into zones. You'll associate each OT network sensor with a specific site and zone, so that each sensor covers only a specific area of your network.

Using sites and zones supports the principles of [Zero Trust](/en-us/security/zero-trust/), and provides extra monitoring and reporting granularity.

For example, if your growing company has factories and offices in Paris, Lagos, Dubai, and Tianjin, you might segment your network as follows:

| Site | Zones |
| --- | --- |
| **Paris office** | - Ground floor (Guests) - Floor 1 (Sales) - Floor 2 (Executive) |
| **Lagos office** | - Ground floor (Offices) - Floors 1-2 (Factory) |
| **Dubai office** | - Ground floor (Convention center) - Floor 1 (Sales)- Floor 2 (Offices) |
| **Tianjin office** | - Ground floor (Offices) - Floors 1-2 (Factory) |

If you don't plan any detailed sites and zones, Defender for IoT still uses a default site and zone to assign to all OT sensors.

For more information, see [Zero Trust and your OT networks](../concept-zero-trust).

### Separating zones for recurring IP ranges

Each zone can support multiple sensors, and if you're deploying Defender for IoT at scale, each sensor might detect different aspects of the same device. Defender for IoT automatically consolidates devices that are detected in the same zone, with the same logical combination of device characteristics, such the same IP and MAC address.

If you're working with multiple networks and have unique devices with similar characteristics, such as recurring IP address ranges, assign each sensor to a separate zone so that Defender for IoT knows to differentiate between the devices and identifies each device uniquely.

For example, your network might look like the following image, with six network segments logically allocated across two Defender for IoT sites and zones. Note that this image shows two network segments with the same IP addresses from different production lines.

![Diagram of recurring networks in the same zone.](../media/plan-corporate-monitoring/recurring-segments-option-no.png)

In this case, we recommend separating **Site 2** into two separate zones, so that devices in the segments with recurring IP addresses aren't consolidated incorrectly, and are identified as separate and unique devices in the device inventory.

For example:

![Diagram of recurring networks in the different zones.](../media/plan-corporate-monitoring/recurring-segments-option-yes.png)

## Plan your users

Understand who in your organization will be using Defender for IoT, and what their use cases are. While your security operations center (SOC) and IT personnel will be the most common users, you may have others in your organization who will need read-access to resources in Azure or on local resources.

- **In Azure**, user assignments are based on their Microsoft Entra ID and RBAC roles. If you're segmenting your network into multiple sites, decide which permissions you'll want to apply per site.
- **OT network sensors** support both local users and Active Directory synchronizations. If you'll be using Active Directory, make sure that you have the access details for the Active Directory server.

For more information, see:

- [Microsoft Defender for IoT user management](../manage-users-overview)
- [Azure user roles and permissions for Defender for IoT](../roles-azure)
- [On-premises users and roles for OT monitoring with Defender for IoT](../roles-on-premises)

## Plan OT sensor and management connections

For cloud-connected sensors, determine how you'll be connecting each OT sensor to Defender for IoT in the Azure cloud, such as what sort of proxy you might need. For more information, see [Methods for connecting sensors to Azure](../architecture-connections).

If you're working in an air-gapped or hybrid environment and will have multiple, locally-managed OT network sensors, see the [Air-gapped OT sensor management deployment path](../ot-deploy/air-gapped-deploy).

## Plan on-premises SSL/TLS certifications

We recommend using a [CA-signed SSL/TLS certificate](../ot-deploy/create-ssl-certificates) with your production system to ensure your appliances' ongoing security.

Plan which certificates and which certificate authority (CA) you'll use for each OT sensor, what tools you'll use to generate the certificates, and which attributes you'll include in each certificate.

For more information, see [SSL/TLS certificate requirements for on-premises resources](certificate-requirements).