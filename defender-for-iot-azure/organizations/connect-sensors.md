---
layout: Conceptual
title: Configure proxy connections from your OT sensor to Azure - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/connect-sensors
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
description: Learn how to configure proxy settings on your OT sensors to connect to Azure.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 1f58275c-b434-68b1-1944-d2f7b81fd29f
document_version_independent_id: 93754174-8263-27a3-f722-53202b4e189b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/connect-sensors.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/connect-sensors
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/connect-sensors.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/20ed8455-bc18-4537-87a4-83784e7b2a39
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/9a7f703b-30bb-4d62-9eb4-97213f571849
platformId: 257bf027-574f-1e52-8833-271493009568
---

# Configure proxy connections from your OT sensor to Azure - Microsoft Defender for IoT | Microsoft Learn

This article is one in a series of articles describing the [deployment path](ot-deploy/ot-deploy-path) for OT monitoring with Microsoft Defender for IoT, and describes how to configure proxy settings on your OT sensor to connect to Azure.

[![Diagram of a progress bar with Deploy your sensors highlighted.](media/deployment-paths/progress-deploy-your-sensors.png)](media/deployment-paths/progress-deploy-your-sensors.png#lightbox)

You can skip this step in the following cases:

- If you're working in air-gapped environment and locally managed sensors
- If you're using a [direct connection](architecture-connections#direct-connections) between your OT sensor and Azure. In this case, you've already performed all required steps when you [provisioned your sensor for cloud management](ot-deploy/provision-cloud-management)

## Prerequisites

To perform the steps described in this article, you'll need:

- An OT network sensor [installed](ot-deploy/install-software-ot-sensor), [configured, and activated](ot-deploy/activate-deploy-sensor).
- An understanding of the [supported connection methods](architecture-connections) for cloud-connected Defender for IoT sensors, and a plan for your [OT site deployment](best-practices/plan-prepare-deploy) that includes the connection method you want to use for each sensor.
- Access to the OT sensor as an **Admin** user. For more information, see [On-premises users and roles for OT monitoring with Defender for IoT](roles-on-premises).

Configuring proxy settings on the OT sensor is performed by your deployment and connectivity teams.

## Configure proxy settings on your OT sensor

This section describes how to configure settings for an existing proxy on your OT sensor console. If you don't yet have a proxy, configure one using the following procedures:

- Set up an Azure proxy
- Connect via proxy chaining
- Set up connectivity for multicloud environments

To define proxy settings on your OT sensor:

1. Sign into your OT sensor and select **System settings &gt; Sensor Network Settings**.
2. Toggle on the **Enable Proxy** option and then enter the following details for your proxy server:

    - Proxy Host
    - Proxy Port
    - Proxy Username (optional)
    - Proxy Password (optional)

    For example:

    [![Screenshot of the proxy setting page.](media/connect-sensors/configure-a-proxy.png)](media/connect-sensors/configure-a-proxy.png#lightbox)
3. If relevant, select **Client certificate** to upload a proxy authentication certificate for access to an SSL/TLS proxy server.

    Note

    A client SSL/TLS certificate is required for proxy servers that inspect SSL/TLS traffic, such as when using services like Zscaler and Palo Alto Prisma.
4. Select **Save**.

## Set up an Azure proxy

You might use an Azure proxy to connect your sensor to Defender for IoT in the following situations:

- You require private connectivity between your sensor and Azure
- Your site is connected to Azure via ExpressRoute
- Your site is connected to Azure over a VPN

If you already have a proxy configured, continue directly with Configure proxy settings on your OT sensor.

If you don't yet have a proxy configured, use the procedures in this section to set one up in your Azure VNET.

### Prerequisites

Before you start, make sure that you have:

- A Log Analytics workspace for monitoring logs
- Remote site connectivity to the Azure VNET
- Outbound HTTPS traffic on port 443 allowed to from your sensor to the required endpoints for Defender for IoT. For more information, see [Provision OT sensors for cloud management](ot-deploy/provision-cloud-management).
- A proxy server resource, with firewall permissions to access Microsoft cloud services. The procedure described in this article uses a Squid server hosted in Azure.

Important

Microsoft Defender for IoT does not offer support for Squid or any other proxy services. It is the customer's responsibility to set up and maintain the proxy service.

### Configure sensor proxy settings

This section describes how to configure a proxy in your Azure VNET for use with an OT sensor, and includes the following steps:

1. Define a storage account for NSG logs
2. Define virtual networks and subnets
3. Define a virtual or local network gateway
4. Define network security groups
5. Define an Azure virtual machine scale set
6. Create an Azure load balancer
7. Configure a NAT gateway

#### Step 1: Define a storage account for NSG logs

In the Azure portal, create a new storage account with the following settings:

| Area | Settings |
| --- | --- |
| **Basics** | **Performance**: Standard **Account kind**: Blob storage **Replication**: LRS |
| **Network** | **Connectivity method**: Public endpoint (selected network) **In Virtual Networks**: None **Routing Preference**: Microsoft network routing |
| **Data Protection** | Keep all options cleared |
| **Advanced** | Keep all default values |

#### Step 2: Define virtual networks and subnets

Create the following VNET and contained subnets:

| Name | Recommended size |
| --- | --- |
| `MD4IoT-VNET` | /26 or /25 with Bastion |
| **Subnets**: |  |
| - `GatewaySubnet` | /27 |
| - `ProxyserverSubnet` | /27 |
| - `AzureBastionSubnet` (optional) | /26 |
|  |  |

#### Step 3: Define a virtual or local network gateway

Create a VPN or ExpressRoute Gateway for virtual gateways, or create a local gateway, depending on how you connect your on-premises network to Azure.

Attach the gateway to the `GatewaySubnet` subnet you created in Step 2: Define virtual networks and subnets.

For more information, see:

- [About VPN gateways](/en-us/azure/vpn-gateway/vpn-gateway-about-vpngateways)
- [Connect a virtual network to an ExpressRoute circuit using the portal](/en-us/azure/expressroute/expressroute-howto-linkvnet-portal-resource-manager)
- [Modify local network gateway settings using the Azure portal](/en-us/azure/vpn-gateway/vpn-gateway-modify-local-network-gateway-portal)

#### Step 4: Define network security groups

1. Create an NSG and define the following inbound rules:

    - Create rule `100` to allow traffic from your sensors (the sources) to the load balancer's private IP address (the destination). Use port `tcp3128`.
    - Create rule `4095` as a duplicate of the `65001` system rule. This is because rule `65001` will get overwritten by rule `4096`.
    - Create rule `4096` to deny all traffic for micro-segmentation.
    - Optional. If you're using Bastion, create rule `4094` to allow Bastion SSH to the servers. Use the Bastion subnet as the source.
2. Assign the NSG to the `ProxyserverSubnet` you created in Step 2: Define virtual networks and subnets.
3. Define your NSG logging:

    1. Select your new NSG and then select **Diagnostic setting &gt; Add diagnostic setting**.
    2. Enter a name for your diagnostic setting. Under **Category** ,select **allLogs**.
    3. Select **Sent to Log Analytics workspace**, and then select the Log Analytics workspace you want to use.
    4. Select to send **NSG flow logs** and then define the following values:

        **On the Basics tab**:

        - Enter a meaningful name
        - Select the storage account you created in Step 1: Define a storage account for NSG logs
        - Define your required retention days

        **On the Configuration tab**:

        - Select **Version 2**
        - Select **Enable Traffic Analytics**
        - Select your Log Analytics workspace

#### Step 5: Define an Azure virtual machine scale set

Define an Azure virtual machine scale set to create and manage a group of load-balanced virtual machine, where you can automatically increase or decrease the number of virtual machines as needed.

For more information, see [What are virtual machine scale sets?](/en-us/azure/virtual-machine-scale-sets/overview)

**To create a scale set to use with your sensor connection**:

1. Create a scale set with the following parameter definitions:

    - **Orchestration Mode**: Uniform
    - **Security Type**: standard
    - **Image**: Ubuntu Server LTS (24.04 or later)
    - **Size**: Standard\_DS1\_V2
    - **Authentication**: Based on your corporate standard

    Keep the default value for **Disks** settings.
2. Create a network interface in the `Proxyserver` subnet you created in Step 2: Define virtual networks and subnets, but don't yet define a load balancer.
3. Define your scaling settings as follows:

    - Define the initial instance count as **1**
    - Define the scaling policy as **Manual**
4. Define the following management settings:

    - For the upgrade mode, select **Automatic - instance will start upgrading**
    - Disable boot diagnostics
    - Clear the settings for **Identity** and **Microsoft Entra ID**
    - Select **Overprovisioning**
    - Select **Enabled automatic OS upgrades**
5. Define the following health settings:

    - Select **Enable application health monitoring**
    - Select the **TCP** protocol and port **3128**
6. Under advanced settings, define the **Spreading algorithm** as **Max Spreading**.
7. For the custom data script, do the following:

    1. Create the following configuration script, depending on the port and services you're using:

        ```txt
        # Recommended minimum configuration:
        # Squid listening port
        http_port 3128
        # Do not allow caching
        cache deny all
        # allowlist sites allowed
        acl allowed_http_sites dstdomain .azure-devices.net
        acl allowed_http_sites dstdomain .blob.core.windows.net
        acl allowed_http_sites dstdomain .servicebus.windows.net
        acl allowed_http_sites dstdomain .download.microsoft.com
        http_access allow allowed_http_sites
        # allowlisting
        acl SSL_ports port 443
        acl CONNECT method CONNECT
        # Deny CONNECT to other unsecure ports
        http_access deny CONNECT !SSL_ports
        # default network rules
        http_access allow localhost
        http_access deny all
        ```
    2. Encode the contents of your script file in [base-64](https://www.base64encode.org/).
    3. Copy the contents of the encoded file, and then create the following configuration script:

        ```txt
        #cloud-config
        # updates packages
        apt_upgrade: true
        # Install squid packages
        packages:
         - squid
        run cmd:
         - systemctl stop squid
         - mv /etc/squid/squid.conf /etc/squid/squid.conf.factory
        write_files:
        - encoding: b64
          content: <replace with base64 encoded text>
          path: /etc/squid/squid.conf
          permissions: '0644'
        run cmd:
         - systemctl start squid
         - apt-get -y upgrade; [ -e /var/run/reboot-required ] && reboot
        ```

#### Step 6: Create an Azure load balancer

Azure Load Balancer is a layer-4 load balancer that distributes incoming traffic among healthy virtual machine instances using a hash-based distribution algorithm.

For more information, see the [Azure Load Balancer documentation](/en-us/azure/load-balancer/load-balancer-overview).

**To create an Azure load balancer for your sensor connection**:

1. Create a load balancer with a standard SKU and an **Internal** type to ensure that the load balancer is closed to the internet.
2. Define a dynamic frontend IP address in the `proxysrv` subnet you created in Step 2: Define virtual networks and subnets, setting the availability to zone-redundant.
3. For a backend, choose the virtual machine scale set you created in Step 5: Define an Azure virtual machine scale set.
4. On the port defined in the sensor, create a TCP load balancing rule connecting the frontend IP address with the backend pool. The default port is 3128.
5. Create a new health probe, and define a TCP health probe on port 3128.
6. Define your load balancer logging:

    1. In the Azure portal, go to the load balancer you've created.
    2. Select **Diagnostic setting** &gt; **Add diagnostic setting**.
    3. Enter a meaningful name, and define the category as **allMetrics**.
    4. Select **Sent to Log Analytics workspace**, and then select your Log Analytics workspace.

#### Step 7: Configure a NAT gateway

To configure a NAT gateway for your sensor connection:

1. Create a new NAT Gateway.
2. In the **Outbound IP** tab, select **Create a new public IP address**.
3. In the **Subnet** tab, select the `ProxyserverSubnet` subnet you created in Step 2: Define virtual networks and subnets.

Your proxy is now fully configured. Continue by defining the proxy settings on your OT sensor.

## Connect via proxy chaining

You might connect your sensor to Defender for IoT in Azure using proxy chaining in the following situations:

- Your sensor needs a proxy to reach from the OT network to the cloud
- You want multiple sensors to connect to Azure through a single point

If you already have a proxy configured, continue directly with Configure proxy settings on your OT sensor.

If you don't yet have a proxy configured, use the procedures in this section to configure your proxy chaining.

For more information, see [Proxy connections with proxy chaining](architecture-connections#proxy-connections-with-proxy-chaining).

### Prerequisites

Before you start, make sure that you have:

- A host server running a proxy process within the site network. The proxy process must be accessible to both the sensor and the next proxy in the chain.
- Outbound HTTPS traffic on port 443 allowed from your sensor to the required endpoints for Defender for IoT. For more information, see [Provision OT sensors for cloud management](ot-deploy/provision-cloud-management).

We've validated this procedure using the open-source [Squid](http://www.squid-cache.org/) proxy. This proxy uses HTTP tunneling and the HTTP CONNECT command for connectivity. Any other proxy chaining connection that supports the CONNECT command can be used for this connection method.

Important

Microsoft Defender for IoT does not offer support for Squid or any other proxy services. It is the customer's responsibility to set up and maintain the proxy service.

### Configure a proxy chaining connection

This procedure describes how to install and configure a connection between your sensors and Defender for IoT using the latest version of Squid on an Ubuntu server.

1. Define your proxy settings on each sensor:

    1. Sign into your OT sensor and select **System settings &gt; Sensor Network Settings**.
    2. Toggle on the **Enable Proxy** option and define your proxy host, port, username, and password.
2. Install the Squid proxy:

    1. Sign into your proxy Ubuntu machine and launch a terminal window.
    2. Update your system and install Squid. For example:

        ```bash
        sudo apt-get update
        sudo apt-get install squid
        ```
    3. Locate the Squid configuration file. For example, at `/etc/squid/squid.conf` or `/etc/squid/conf.d/`, and open the file in a text editor.
    4. In the Squid configuration file, search for the following text: `# INSERT YOUR OWN RULE(S) HERE TO ALLOW ACCESS FROM YOUR CLIENTS`.
    5. Add `acl <sensor-name> src <sensor-ip>`, and `http_access allow <sensor-name>` into the file. For example:

        ```text
        # INSERT YOUR OWN RULE(S) HERE TO ALLOW ACCESS FROM YOUR CLIENTS
        acl sensor1 src 10.100.100.1
        http_access allow sensor1
        ```

        Add more sensors as needed by adding extra lines for sensor.
    6. Configure the Squid service to start at launch. Run:

        ```bash
        sudo systemctl enable squid
        ```
3. Connect your proxy to Defender for IoT. Ensure that outbound HTTPS traffic on port 443 is allowed to from your sensor to the required endpoints for Defender for IoT.

    For more information, see [Provision OT sensors for cloud management](ot-deploy/provision-cloud-management).

Your proxy is now fully configured. Continue by configuring proxy settings on your OT sensor.

## Set up connectivity for multicloud environments

This section describes how to connect your sensor to Defender for IoT in Azure from sensors deployed in one or more public clouds. For more information, see [Multicloud connections](architecture-connections#multicloud-connections).

### Prerequisites

Before you start, make sure that you have a sensor deployed in a public cloud, such as AWS or Google Cloud, and configured to monitor [SPAN traffic](traffic-mirroring/configure-mirror-span).

### Select a multicloud connectivity method

Use the following flow chart to determine which connectivity method to use:

![Flow chart to determine which connectivity method to use.](media/architecture-connections/multicloud-flow-chart.png)

- **Use public IP addresses over the internet** if you don't need to exchange data using private IP addresses
- **Use site-to-site VPN over the internet** only if you don't\* require any of the following:

    - Predictable throughput
    - SLA
    - High data volume transfers
    - Avoid connections over the public internet
- **Use ExpressRoute** if you require predictable throughput, SLA, high data volume transfers, or to avoid connections over the public internet.

    In this case:

    - If you want to own and manage the routers making the connection, use ExpressRoute with customer-managed routing.
    - If you don't need to own and manage the routers making the connection, use ExpressRoute with a cloud exchange provider.

### Configure multicloud connectivity

Use the following steps to configure multicloud connectivity and then define proxy settings on the sensor.

1. Configure your sensor to connect to the cloud using one of the Azure Cloud Adoption Framework recommended methods. For more information, see [Connectivity to other cloud providers](/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/connectivity-to-other-providers).
2. To enable private connectivity between your VPCs and Defender for IoT, connect your VPC to an Azure VNET over a VPN connection. For example if you're connecting from an AWS VPC, see our TechCommunity blog: [How to create a VPN between Azure and AWS using only managed solutions](https://techcommunity.microsoft.com/t5/fasttrack-for-azure/how-to-create-a-vpn-between-azure-and-aws-using-only-managed/ba-p/2281900).
3. After your VPC and VNET are configured, configure the sensor proxy settings on your OT sensor.