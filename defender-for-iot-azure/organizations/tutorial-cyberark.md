---
layout: Conceptual
title: Integrate CyberArk with Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/tutorial-cyberark
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
description: In this tutorial, you learn how to integrate Microsoft Defender for IoT with CyberArk.
ms.topic: tutorial
ms.date: 2024-10-14T00:00:00.0000000Z
ms.custom:
- how-to
- sfi-image-nochange
locale: en-us
document_id: 80d75a36-fc1d-bdc5-1f30-e79499260078
document_version_independent_id: 335990c6-fa4c-32b8-598a-8552a502aadd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/tutorial-cyberark.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/tutorial-cyberark
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/tutorial-cyberark.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 2c574eab-1216-3164-fa21-a3d6ff3d2b66
---

# Integrate CyberArk with Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn

This article helps you learn how to integrate and use CyberArk with Microsoft Defender for IoT.

Defender for IoT delivers ICS and IIoT cybersecurity platforms with ICS-aware threat analytics and machine learning.

Threat actors are using compromised remote access credentials to access critical infrastructure networks via remote desktop and VPN connections. By using trusted connections, this approach easily bypasses any OT perimeter security. Credentials are typically stolen from privileged users, such as control engineers and partner maintenance personnel, who require remote access to perform daily tasks.

The Defender for IoT integration along with CyberARK allows you to:

- Reduce OT risks from unauthorized remote access
- Provide continuous monitoring and privileged access security for OT
- Enhance incident response, threat hunting, and threat modeling

The Defender for IoT appliance is connected to the OT network via a SPAN port (mirror port) on network devices, such as switches and routers, via a one-way (inbound) connection to the dedicated network interfaces on the Defender for IoT appliance.

A dedicated network interface is also provided in the Defender for IoT appliance for centralized management and API access. This interface is also used for communicating with the CyberArk PSM solution that is deployed in the data center of the organization to manage privileged users and secure remote access connections.

[![The CyberArk PSM solution deployment](media/tutorial-cyberark/architecture.png)](media/tutorial-cyberark/architecture.png#lightbox)

In this article, you learn how to:

- Configure PSM in CyberArk
- Enable the integration in Defender for IoT
- View and manage detections
- Stop the integration

## Prerequisites

Before you begin, make sure that you have the following prerequisites:

- CyberARK version 2.0.
- Verify that you have [CLI](references-work-with-defender-for-iot-cli-commands) access to all Defender for IoT appliances in your enterprise.
- An Azure account. If you don't already have an Azure account, you can [create your Azure free account today](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).
- Access to a Defender for IoT OT sensor as an Admin user. For more information, see [On-premises users and roles for OT monitoring with Defender for IoT](roles-on-premises).

## Configure PSM CyberArk

CyberArk must be configured to allow communication with Defender for IoT. This communication is accomplished by configuring PSM.

**To configure PSM**:

1. Locate and open the `c:\Program Files\PrivateArk\Server\dbparam.xml` file.
2. Add the following parameters:

    `[SYSLOG]``UseLegacySyslogFormat=Yes``SyslogTranslatorFile=Syslog\CyberX.xsl``SyslogServerIP=<CyberX Server IP>``SyslogServerProtocol=UDP``SyslogMessageCodeFilter=319,320,295,378,380`
3. Save the file, then close it.
4. Place the Defender for IoT syslog configuration file `CyberX.xsl` in `c:\Program Files\PrivateArk\Server\Syslog\CyberX.xsl`.
5. Open the **Server Central Administration**.
6. Select the ![](media/tutorial-cyberark/stoplight.png)**Stop Traffic Light** to stop the server.
7. Select the **Start Traffic Light** to start the server.

## Enable the integration in Defender for IoT

In order to enable the integration, Syslog Server needs to be enabled in the OT sensor. By default, the Syslog Server listens to the IP address of the system using port 514 UDP.

**To configure Defender for IoT**:

1. Sign into your OT sensor, then navigate to **System Settings**.
2. Toggle the Syslog Server to **On**.

    ![Screenshot of the syslog server toggled to on.](media/tutorial-cyberark/toggle.png)
3. (Optional) Change the port by signing into the system via the CLI, navigating to `/var/cyberx/properties/syslog.properties`, and then changing to `listener: 514/udp`.

## View and manage detections

The integration between Microsoft Defender for IoT and CyberArk PSM is performed via syslog messages. These messages are sent by the PSM solution to Defender for IoT, notifying Defender for IoT of any remote sessions or verification failures.

Once the Defender for IoT platform receives these messages from PSM, it correlates them with the data it sees in the network. Thus, validating that any remote access connections to the network were generated by the PSM solution and not by an unauthorized user.

### View alerts

Whenever the Defender for IoT platform identifies remote sessions that haven't been authorized by PSM, it issues an `Unauthorized Remote Session`. To facilitate immediate investigation, the alert also shows the IP addresses and names of the source and destination devices.

**To view alerts**:

1. Sign into your OT sensor, then select **Alerts**.
2. From the list of alerts, select the alert titled **Unauthorized Remote Session**.

### Event timeline

Whenever PSM authorizes a remote connection, it's visible in the Defender for IoT Event Timeline page. The Event Timeline page shows a timeline of all alerts and notifications.

**To view the event timeline**:

1. Sign into your network sensor, then select **Event timeline**.
2. Locate any event titled PSM Remote Session.

### Auditing & forensics

Administrators can audit and investigate remote access sessions by querying the Defender for IoT platform via its built-in data mining interface. This information can be used to identify all remote access connections that have occurred, including forensic details such as from or to devices, protocols (RDP, or SSH), source and destination users, time-stamps, and whether the sessions were authorized using PSM.

**To audit and investigate**:

1. Sign into your network sensor, then select **Data mining**.
2. Select **Remote Access**.

## Stop the Integration

At any point in time, you can stop the integration from communicating.

**To stop the integration**:

1. In the OT sensor, navigate to **System Settings**.
2. Toggle the Syslog Server option to **Off** .

    ![A view of th Server status.](media/tutorial-cyberark/toggle.png)