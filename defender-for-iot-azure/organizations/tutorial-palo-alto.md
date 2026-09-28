---
layout: Conceptual
title: Integrate Palo Alto with Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/tutorial-palo-alto
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
description: Defender for IoT has integrated its continuous ICS threat monitoring platform with Palo Alto’s next-generation firewalls to enable blocking of critical threats, faster and more efficiently.
ms.date: 2023-09-06T00:00:00.0000000Z
ms.topic: tutorial
locale: en-us
document_id: 04362d4a-a274-c155-5815-c16683b0b445
document_version_independent_id: a8208c47-9d2a-d5de-d500-fb54733fff94
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/tutorial-palo-alto.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/tutorial-palo-alto
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/tutorial-palo-alto.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 804d6d84-2e25-7e19-4651-3330ab34dbaf
---

# Integrate Palo Alto with Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn

This article describes how to integrate Palo Alto with Microsoft Defender for IoT, in order to view both Palo Alto and Defender for IoT information in a single place, or use Defender for IoT data to configure blocking actions in Palo Alto.

Viewing both Defender for IoT and Palo Alto information together provides SOC analysts with multidimensional visibility so that they can block critical threats faster.

Note

Defender for IoT plans to retire the Palo Alto integration on December 1, 2025

## Cloud-based integrations

Tip

Cloud-based security integrations provide several benefits over on-premises solutions, such as centralized, simpler sensor management and centralized security monitoring.

Other benefits include real-time monitoring, efficient resource use, increased scalability and robustness, improved protection against security threats, simplified maintenance and updates, and seamless integration with third-party solutions.

If you're integrating a cloud-connected OT sensor with Palo Alto we recommend that you connect Defender for IoT to [Microsoft Sentinel](concept-sentinel-integration).

Install one or more of the following solutions to view both Palo Alto and Defender for IoT data in Microsoft Sentinel.

| Microsoft Sentinel solution | Learn more |
| --- | --- |
| [Palo Alto PAN-OS Solution](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azuresentinel.azure-sentinel-solution-paloaltopanos?tab=Overview) | [Palo Alto Networks (Firewall) connector for Microsoft Sentinel](/en-us/azure/sentinel/data-connectors/palo-alto-networks-firewall) |
| [Palo Alto Networks Cortex Data Lake Solution](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azuresentinel.azure-sentinel-solution-paloaltocdl?tab=Overview) | [Palo Alto Networks Cortex Data Lake (CDL) connector for Microsoft Sentinel](/en-us/azure/sentinel/data-connectors/palo-alto-networks-cortex-data-lake-cdl) |
| [Palo Alto Prisma Cloud CSPM solution](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azuresentinel.azure-sentinel-solution-paloaltoprisma?tab=Overview) | [Palo Alto Prisma Cloud CSPM (using Azure Function) connector for Microsoft Sentinel](/en-us/azure/sentinel/data-connectors/palo-alto-prisma-cloud-cspm-using-azure-function) |

Microsoft Sentinel is a scalable cloud service for security information event management (SIEM) security orchestration automated response (SOAR). SOC teams can use the integration between Microsoft Defender for IoT and Microsoft Sentinel to collect data across networks, detect and investigate threats, and respond to incidents.

In Microsoft Sentinel, the Defender for IoT data connector and solution brings out-of-the-box security content to SOC teams, helping them to view, analyze and respond to OT security alerts, and understand the generated incidents in the broader organizational threat contents.

For more information, see:

- [Tutorial: Connect Microsoft Defender for IoT with Microsoft Sentinel](iot-solution)
- [Tutorial: Investigate and detect threats for IoT devices](iot-advanced-threat-monitoring)

## On-premises integrations

If you're working with an air-gapped, locally managed OT sensor, you'll need an on-premises solution to view Defender for IoT and Palo Alto information in the same place.

In such cases, we recommend that you configure your OT sensor to send syslog files directly to Palo Alto, or use Defender for IoT's built-in API.

For more information, see:

- [Forward on-premises OT alert information](how-to-forward-alert-information-to-partners)
- [Defender for IoT API reference](references-work-with-defender-for-iot-apis)

## On-premises integration (legacy)

This section describes how to integrate and use Palo Alto with Microsoft Defender for IoT using the legacy, on-premises integration, which automatically creates new policies in the Palo Alto Network's NMS and Panorama.

Important

The legacy Palo Alto Panorama integration is supported through October 2024 using sensor version 23.1.3, and won't be supported in upcoming major software versions. For customers using the legacy integration, we recommend moving to one of the following methods:

- If you're integrating your security solution with cloud-based systems, we recommend that you use data connectors through Microsoft Sentinel.
- For on-premises integrations, we recommend that you either configure your OT sensor to forward syslog events, or use Defender for IoT APIs.

The following table shows which incidents this integration is intended for:

| Incident type | Description |
| --- | --- |
| **Unauthorized PLC changes** | An update to the ladder logic, or firmware of a device. This alert can represent legitimate activity, or an attempt to compromise the device. For example, malicious code, such as a Remote Access Trojan (RAT), or parameters that cause the physical process, such as a spinning turbine, to operate in an unsafe manner. |
| **Protocol Violation** | A packet structure, or field value that violates the protocol specification. This alert can represent a misconfigured application, or a malicious attempt to compromise the device. For example, causing a buffer overflow condition in the target device. |
| **PLC Stop** | A command that causes the device to stop functioning, thereby risking the physical process that is being controlled by the PLC. |
| **Industrial malware found in the ICS network** | Malware that manipulates ICS devices using their native protocols, such as TRITON and Industroyer. Defender for IoT also detects IT malware that has moved laterally into the ICS, and SCADA environment. For example, Conficker, WannaCry, and NotPetya. |
| **Scanning malware** | Reconnaissance tools that collect data about system configuration in a preattack phase. For example, the Havex Trojan scans industrial networks for devices using OPC, which is a standard protocol used by Windows-based SCADA systems to communicate with ICS devices. |

When Defender for IoT detects a preconfigured use case, the **Block Source** button is added to the alert. Then, when the Defender for IoT user selects the **Block Source** button, Defender for IoT creates policies on Panorama by sending the predefined forwarding rule.

The policy is applied only when the Panorama administrator pushes it to the relevant NGFW in the network.

In IT networks, there might be dynamic IP addresses. Therefore, for those subnets, the policy must be based on FQDN (DNS name) and not the IP address. Defender for IoT performs reverse lookup and matches devices with dynamic IP address to their FQDN (DNS name) every configured number of hours.

In addition, Defender for IoT sends an email to the relevant Panorama user to notify that a new policy created by Defender for IoT is waiting for the approval. The figure below presents the Defender for IoT and Panorama integration architecture:

[![Diagram of the Defender for IoT-Panorama Integration Architecture.](media/tutorial-palo-alto/structure.png)](media/tutorial-palo-alto/structure.png#lightbox)

### Prerequisites

Before you begin, make sure that you have the following prerequisites:

- Confirmation by the Panorama Administrator to allow automatic blocking.
- Access to a Defender for IoT OT sensor as an [Admin user](roles-on-premises).

### Configure DNS lookup

The first step in creating Panorama blocking policies in Defender for IoT is to configure DNS lookup.

**To configure DNS lookup**:

1. Sign in to your OT sensor and select **System settings** &gt; **Network monitoring** &gt; **DNS Reverse Lookup**.
2. Turn on the **Enabled** toggle to activate the lookup.
3. In the **Schedule Reverse Lookup** field, define the scheduling options:

    - By specific times: Specify when to perform the reverse lookup daily.
    - By fixed intervals (in hours): Set the frequency for performing the reverse lookup.
4. Select **+ Add DNS Server**, and then add the following details:

    | Parameter | Description |
    | --- | --- |
    | **DNS Server Address** | Enter the IP address or the FQDN of the network DNS Server. |
    | **DNS Server Port** | Enter the port used to query the DNS server. |
    | **Number of Labels** | To configure DNS FQDN resolution, add the number of domain labels to display.  Up to 30 characters are displayed from left to right. |
    | **Subnets** | Set the Dynamic IP address subnet range.  The range that Defender for IoT reverses lookup their IP address in the DNS server to match their current FQDN name. |
5. To ensure your DNS settings are correct, select **Test**. The test ensures that the DNS server IP address, and DNS server port are set correctly.
6. Select **Save**.

When you're done, continue by creating forwarding rules as needed:

- Configure immediate blocking by a specified Palo Alto firewall
- Block suspicious traffic with the Palo Alto firewall

### Configure immediate blocking by a specified Palo Alto firewall

Configure automatic blocking in cases such as malware-related alerts, by configuring a Defender for IoT forwarding rule to send a blocking command directly to a specific Palo Alto firewall.

When Defender for IoT identifies a critical threat, it sends an alert that includes an option of blocking the infected source. Selecting **Block Source** in the alert’s details activates the forwarding rule, which sends the blocking command to the specified Palo Alto firewall.

When creating your forwarding rule:

1. In the **Actions** area, define the server, host, port, and credentials for the Palo Alto NGFW.
2. Configure the following options to allow blocking of the suspicious sources by the Palo Alto firewall:

    | Parameter | Description |
    | --- | --- |
    | **Block illegal function codes** | Protocol violations - Illegal field value violating ICS protocol specification (potential exploit). |
    | **Block unauthorized PLC programming / firmware updates** | Unauthorized PLC changes. |
    | **Block unauthorized PLC stop** | PLC stop (downtime). |
    | **Block malware related alerts** | Blocking of industrial malware attempts (TRITON, NotPetya, etc.).  You can select the option of **Automatic blocking**.  In that case, the blocking is executed automatically and immediately. |
    | **Block unauthorized scanning** | Unauthorized scanning (potential reconnaissance). |

For more information, see [Forward on-premises OT alert information](how-to-forward-alert-information-to-partners).

### Block suspicious traffic with the Palo Alto firewall

Configure a Defender for IoT forwarding rule to block suspicious traffic with the Palo Alto firewall.

When creating your forwarding rule:

1. In the **Actions** area, define the server, host, port, and credentials for the Palo Alto NGFW.
2. Define how the blocking is executed, as follows:

    - **By IP Address**: Always creates blocking policies on Panorama based on the IP address.
    - **By FQDN or IP Address**: Creates blocking policies on Panorama based on FQDN if it exists, otherwise by the IP Address.
3. In the **Email** field, enter the email address for the policy notification email.

    Note

    Make sure you have configured a Mail Server in the Defender for IoT. If no email address is entered, Defender for IoT does not send a notification email.
4. Configure the following options to allow blocking of the suspicious sources by the Palo Alto Panorama:

    | Parameter | Description |
    | --- | --- |
    | **Block illegal function codes** | Protocol violations - Illegal field value violating ICS protocol specification (potential exploit). |
    | **Block unauthorized PLC programming / firmware updates** | Unauthorized PLC changes. |
    | **Block unauthorized PLC stop** | PLC stop (downtime). |
    | **Block malware related alerts** | Blocking of industrial malware attempts (TRITON, NotPetya, etc.).  You can select the option of **Automatic blocking**.  In that case, the blocking is executed automatically and immediately. |
    | **Block unauthorized scanning** | Unauthorized scanning (potential reconnaissance). |

For more information, see [Forward on-premises OT alert information](how-to-forward-alert-information-to-partners).

### Block specific suspicious sources

After you've created your forwarding rule, use the following steps to block specific, suspicious sources:

1. In the OT sensor's **Alerts** page, locate and select the alert related to the Palo Alto integration.
2. To automatically block the suspicious source, select **Block Source**.
3. In the **Please Confirm** dialog box, select **OK**.

The suspicious source is now blocked by the Palo Alto firewall.