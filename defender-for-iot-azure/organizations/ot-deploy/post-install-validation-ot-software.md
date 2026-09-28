---
layout: Conceptual
title: Validate an OT sensor software installation - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/ot-deploy/post-install-validation-ot-software
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
description: Learn how to test your system post installation of OT network monitoring software for Microsoft Defender for IoT. Use this article after you've reinstalled software on a pre-configured appliance, or if you've chosen to install software on your own appliances.
ms.date: 2023-12-19T00:00:00.0000000Z
ms.topic: install-set-up-deploy
locale: en-us
document_id: 04dbdbd8-b1c4-a38e-9444-6f026779f9be
document_version_independent_id: 2768ccc2-5dbf-71e6-5cf9-a30fff3b7387
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/ot-deploy/post-install-validation-ot-software.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: defender-for-iot/organizations/ot-deploy/post-install-validation-ot-software
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/ot-deploy/post-install-validation-ot-software.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: dee12920-eec0-1730-dbef-23882beceff0
---

# Validate an OT sensor software installation - Microsoft Defender for IoT | Microsoft Learn

This article is one in a series of articles describing the [deployment path](ot-deploy-path) for OT monitoring with Microsoft Defender for IoT.

[![Diagram of a progress bar with Deploy your sensors highlighted.](../media/deployment-paths/progress-deploy-your-sensors.png)](../media/deployment-paths/progress-deploy-your-sensors.png#lightbox)

After you've installed OT software on your [OT sensors](install-software-ot-sensor), test your system to make sure that processes are running correctly. The same validation process applies to all appliance types.

System health validations are supported via UI or CLI and are available for the default, privileged *admin* user.

If you're using pre-configured appliances, continue directly with [activating and setting up your OT network sensor](activate-deploy-sensor) instead.

## Prerequisites

The procedures in this article assume that you've just installed Defender for IoT software on an OT network sensor.

For more information, see [Install OT monitoring software on OT sensors](install-software-ot-sensor).

This step is performed by your deployment teams.

## General tests

After installing OT monitoring software, make sure to run the following tests:

- **Sanity test**: Verify that the system is running.
- **Version**: Verify that the version is correct.
- **ifconfig**: Verify that all the input interfaces configured during the installation process are running.

## Gateway checks

Use the `route` command to show the gateway's IP address. For example:

```CLI
<root@xsense:/# route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
0.0.0.0         172.18.0.1      0.0.0.0         UG    0      0        0 eth0
172.18.0.0      0.0.0.0         255.255.0.0     U     0      0        0 eth0
>
```

Use the `arp -a` command to verify that there's a binding between the MAC address and the IP address of the default gateway. For example:

```CLI
<root@xsense:/# arp -a
cusalvtecca101-gi0-02-2851.network.microsoft.com (172.18.0.1) at 02:42:b0:3a:e8:b5 [ether] on eth0
mariadb_22.2.6.27-r-c64cbca.iot_network_22.2.6.27-r-c64cbca (172.18.0.5) at 02:42:ac:12:00:05 [ether] on eth0
redis_22.2.6.27-r-c64cbca.iot_network_22.2.6.27-r-c64cbca (172.18.0.3) at 02:42:ac:12:00:03 [ether] on eth0
>
```

## DNS checks

Use the `cat /etc/resolv.conf` command to find the IP address that's configured for DNS traffic. For example:

```CLI
<root@xsense:/# cat /etc/resolv.conf
search reddog.microsoft.com
nameserver 127.0.0.11
options ndots:0
>
```

Use the `host` command to resolve an FQDN. For example:

```CLI
<root@xsense:/# host www.apple.com
www.apple.com is an alias for www.apple.com.edgekey.net.
www.apple.com.edgekey.net is an alias for www.apple.com.edgekey.net.globalredir.akadns.net.
www.apple.com.edgekey.net.globalredir.akadns.net is an alias for e6858.dscx.akamaiedge.net.
e6858.dscx.akamaiedge.net has address 72.246.148.202
e6858.dscx.akamaiedge.net has IPv6 address 2a02:26f0:5700:1b4::1aca
e6858.dscx.akamaiedge.net has IPv6 address 2a02:26f0:5700:182::1aca
>
```

## Firewall checks

Use the `wget` command to verify that port 443 is open for communication. For example:

```CLI
<root@xsense:/# wget https://www.apple.com
--2022-11-09 11:21:15--  https://www.apple.com/
Resolving www.apple.com (www.apple.com)... 72.246.148.202, 2a02:26f0:5700:1b4::1aca, 2a02:26f0:5700:182::1aca
Connecting to www.apple.com (www.apple.com)|72.246.148.202|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 99966 (98K) [text/html]
Saving to: 'index.html.1'

index.html.1        100%[===================>]  97.62K  --.-KB/s    in 0.02s

2022-11-09 11:21:15 (5.88 MB/s) - 'index.html.1' saved [99966/99966]

>
```

For more information, see [Check system health](../how-to-troubleshoot-sensor#check-system-health) in our sensor troubleshooting article.