---
layout: Conceptual
title: Networking requirements - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/networking-requirements
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
description: Learn about Microsoft Defender for IoT's networking requirements, from network sensors, and deployment workstations.
ms.date: 2023-01-15T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: b5569979-21f1-4a10-968c-cc2dd4386348
document_version_independent_id: 0bec3656-fc99-e776-9c7d-afc72bb4281e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/networking-requirements.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/networking-requirements
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/networking-requirements.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 4a105bef-19f9-e9f5-174c-3afb1d792e21
---

# Networking requirements - Microsoft Defender for IoT | Microsoft Learn

This article lists the interfaces that must be accessible on Microsoft Defender for IoT network sensors, and deployment workstations in order for services to function as expected.

Make sure that your organization's security policy allows access for the interfaces listed in the tables below.

## User access to the sensor

| Protocol | Transport | In/Out | Port | Used | Purpose | Source | Destination |
| --- | --- | --- | --- | --- | --- | --- | --- |
| SSH | TCP | In/Out | 22 | CLI | To access the CLI | Client | Sensor |
| HTTPS | TCP | In/Out | 443 | To access the sensor | Access to Web console | Client | Sensor |

## Sensor access to Azure portal

| Protocol | Transport | In/Out | Port | Purpose | Source | Destination |
| --- | --- | --- | --- | --- | --- | --- |
| HTTPS | TCP | Out | 443 | Access to Azure | Sensor | OT network sensors connect to Azure to provide alert and device data and sensor health messages, access threat intelligence packages, and more. Connected Azure services include IoT Hub, Blob Storage, Event Hubs, and the Microsoft Download Center.Download the list from the **Sites and sensors** page in the Azure portal. Select an OT sensor with software versions 22.x or higher, or a site with one or more supported sensor versions. Then, select **More options &gt; Download endpoint details**. For more information, see [Sensor management options from the Azure portal](how-to-manage-sensors-on-the-cloud#sensor-management-options-from-the-azure-portal). |

## Sensor access to the OT sensor

| Protocol | Transport | In/Out | Port | Used | Purpose | Source | Destination |
| --- | --- | --- | --- | --- | --- | --- | --- |
| NTP | UDP | In/Out | 123 | Time Sync | Connects the NTP to the OT sensor | Sensor | OT sensor |
| TLS/SSL | TCP | In/Out | 443 | Give the sensor access to the OT sensor | The connection between the sensor, and the OT sensor | Sensor | OT sensor |

## Other firewall rules for external services (optional)

Open these ports to allow extra services for Defender for IoT.

| Protocol | Transport | In/Out | Port | Used | Purpose | Source | Destination |
| --- | --- | --- | --- | --- | --- | --- | --- |
| SMTP | TCP | Out | 25 | Email | Used to open the customer's mail server, in order to send emails for alerts, and events | Sensor and OT sensor | Email server |
| DNS | TCP/UDP | In/Out | 53 | DNS | The DNS server port | OT sensor and Sensor | DNS server |
| HTTP | TCP | Out | 80 | The CRL download for certificate validation when uploading certificates. | Access to the CRL server | Sensor and OT sensor | CRL server |
| [WMI](how-to-configure-windows-endpoint-monitoring) | TCP/UDP | Out | 135, 1025-65535 | Monitoring | Windows Endpoint Monitoring | Sensor | Relevant network element |
| [SNMP](how-to-set-up-snmp-mib-monitoring) | UDP | Out | 161 | Monitoring | Monitors the sensor's health | OT sensor and Sensor | SNMP server |
| LDAP | TCP | In/Out | 389 | Active Directory | Allows Active Directory management of users that have access, to sign in to the system | OT sensor and Sensor | LDAP server |
| Proxy | TCP/UDP | In/Out | 443 | Proxy | To connect the sensor to a proxy server | OT sensor and Sensor | Proxy server |
| Syslog | UDP | Out | 514 | LEEF | The logs that are sent from the OT sensor to Syslog server | OT sensor and Sensor | Syslog server |
| LDAPS | TCP | In/Out | 636 | Active Directory | Allows Active Directory management of users that have access, to sign in to the system | OT sensor and Sensor | LDAPS server |
| Tunneling | TCP | In | 9000  In addition to port 443  Allows access from the sensor, or end user, to the OT sensor  Port 22 from the sensor to the OT sensor | Monitoring | Tunneling | Endpoint, Sensor | OT sensor |