---
layout: Conceptual
title: Methods for connecting sensors to Azure - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/architecture-connections
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
description: Learn about the architecture models available for connecting your sensors to Microsoft Defender for IoT.
ms.topic: concept-article
ms.date: 2023-02-23T00:00:00.0000000Z
locale: en-us
document_id: 9352add3-43c6-3b2f-5327-ccdc4bfdcc12
document_version_independent_id: 9fef1745-8a2e-9e58-7adb-d538891634b1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/architecture-connections.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/architecture-connections
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/architecture-connections.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: c9aad92f-7472-e1a5-1c34-e0afb8539f08
---

# Methods for connecting sensors to Azure - Microsoft Defender for IoT | Microsoft Learn

This article is one in a series of articles describing the [deployment path](ot-deploy/ot-deploy-path) for OT monitoring with Microsoft Defender for IoT.

Use the content below to learn about the architectures and methods supported for connecting Defender for IoT sensors to the Azure portal in the cloud.

[![Diagram of a progress bar with Plan and prepare highlighted.](media/deployment-paths/progress-plan-and-prepare.png)](media/deployment-paths/progress-plan-and-prepare.png#lightbox)

Network sensors connect to Azure to provide data about detected devices, alerts, and sensor health, to access threat intelligence packages, and more. For example, connected Azure services include IoT Hub, Blob Storage, Event Hubs, Aria, the Microsoft Download Center.

All connection methods provide:

- **Improved security**, without additional security configurations. [Connect to Azure using specific and secure endpoints](networking-requirements#sensor-access-to-azure-portal), without the need for any wildcards.
- **Encryption**, Transport Layer Security (TLS1.2/AES-256) provides encrypted communication between the sensor and Azure resources.
- **Scalability** for new features supported only in the cloud

Important

To ensure that your network is ready, we recommend that you first run your connections in a lab or testing environment so that you can safely validate your Azure service configurations.

## Choose a sensor connection method

Use this section to help determine which connection method is right for your cloud-connected Defender for IoT sensor.

| If ... | ... Then use |
| --- | --- |
| - You want to connect your sensor to Azure directly | **Direct connections** |
| - Your sensor needs a proxy to reach from the OT network to the cloud, or - You want multiple sensors to connect to Azure through a single point | **Proxy connections with proxy chaining** |
| - You require private connectivity between your sensor and Azure, - Your site is connected to Azure via ExpressRoute, or - Your site is connected to Azure over a VPN | **Proxy connections with an Azure proxy** |
| - You have sensors hosted in multiple public clouds | **Multicloud connections** |

Note

While most connection methods are relevant for OT sensors only, Direct connections are also used for [Enterprise IoT sensors](eiot-sensor).

## Direct connections

The following image shows how you can connect your sensors to the Defender for IoT portal in Azure directly over the internet from remote sites, without traversing the enterprise network.

![Diagram of a direct connection to Azure.](media/architecture-connections/direct.png)

With direct connections:

- Any sensors connected to Azure data centers directly over the internet or Azure ExpressRoute have a secure and encrypted connection to the Azure data centers. Transport Layer Security (TLS1.2/AES-256) provides *always-on* communication between the sensor and Azure resources.
- The sensor initiates all connections to the Azure portal. Initiating connections only from the sensor protects internal network devices from unsolicited inbound connections, but also means that you don't need to configure any inbound firewall rules.

For more information, see [Provision sensors for cloud management](ot-deploy/provision-cloud-management).

## Proxy connections with proxy chaining

The following image shows how you can connect your sensors to the Defender for IoT portal in Azure through multiple proxies, using different levels of the Purdue model and the enterprise network hierarchy.

![Diagram of a proxy connection using proxy chaining.](media/architecture-connections/proxy-chaining.png)

This method supports connecting your sensors with either direct internet access, private VPN or ExpressRoute, the sensor will establish an SSL-encrypted tunnel to transfer data from the sensor to the service endpoint via multiple proxy servers. The proxy server doesn't perform any data inspection, analysis, or caching.

It is the customer's responsibility to set up and maintain third-party proxy services with proxy chaining; Microsoft does not provide support for them.

For more information, see [Connect via proxy chaining](connect-sensors#connect-via-proxy-chaining).

## Proxy connections with an Azure proxy

The following image shows how you can connect your sensors to the Defender for IoT portal in Azure through a proxy in the Azure VNET. This configuration ensures confidentiality for all communications between your sensor and Azure.

![Diagram of a proxy connection using an Azure proxy.](media/architecture-connections/proxy.png)

Depending on your network configuration, you can access the VNET via a VPN connection or an ExpressRoute connection.

This method uses a proxy server hosted within Azure. To handle load balancing and failover, the proxy is configured to scale automatically behind a load balancer.

For more information, see [Connect via an Azure proxy](connect-sensors#set-up-an-azure-proxy).

## Multicloud connections

You can connect your sensors to the Defender for IoT portal in Azure from other public clouds for OT/IoT management process monitoring.

Depending on your environment configuration, you might connect using one of the following methods:

- ExpressRoute with customer-managed routing
- ExpressRoute with a cloud exchange provider
- A site-to-site VPN over the internet.

For more information, see [Connect via multicloud vendors](connect-sensors#set-up-connectivity-for-multicloud-environments).