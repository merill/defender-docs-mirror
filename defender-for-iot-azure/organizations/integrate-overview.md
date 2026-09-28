---
layout: Conceptual
title: Integrate with partner services - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/integrate-overview
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
description: Learn about supported integrations across your organization's security stack with Microsoft Defender for IoT.
ms.date: 2023-09-06T00:00:00.0000000Z
ms.topic: overview
ms.custom: enterprise-iot
locale: en-us
document_id: fe08fdd6-84a2-84f4-1ed9-0debe7d0e8e2
document_version_independent_id: a635c611-cea8-7c98-0cc7-2b23ec5281cf
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/integrate-overview.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/integrate-overview
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/integrate-overview.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 5a3693ef-f738-9a49-a2a6-695656e7043f
---

# Integrate with partner services - Microsoft Defender for IoT | Microsoft Learn

Integrate Microsoft Defender for IoT with partner services to view data from across your security stack data in Defender for IoT, or to view Defender for IoT data in one of your security ecosystem integrations.

Important

Defender for IoT is refreshing its security stack integrations to improve the overall robustness, scalability, and ease of maintenance of various security solutions.

If you're integrating your security solution with cloud-based systems, we recommend that you use data connectors through [Microsoft Sentinel](concept-sentinel-integration). For on-premises integrations, we recommend that you either configure your OT sensor to [forward syslog events](how-to-forward-alert-information-to-partners)), or use [Defender for IoT APIs](references-work-with-defender-for-iot-apis).

The legacy Aruba ClearPass, Palo Alto Panorama, and Splunk integrations are supported through October 2024 using sensor version 23.1.3, and won't be supported in upcoming major software versions. For customers using legacy integration methods, we recommend moving your integrations to the standard cloud or on-premises methods.

Defender for IoT plans to retire the ArcSight, SPOOL, FortiSIEM, Webhook, Palo Alto and NetWitness integrations on December 1, 2025.

## Aruba ClearPass

| Name | Description | Support scope | Supported by | Learn more |
| --- | --- | --- | --- | --- |
| **Aruba ClearPass** (cloud) | View Defender for IoT data together with Aruba ClearPass data, using Microsoft Sentinel to create custom dashboards, custom alerts, and improve your investigation ability. Connect to [Microsoft Sentinel](concept-sentinel-integration), and install the [Aruba ClearPass data connector](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azuresentinel.azure-sentinel-solution-arubaclearpass?tab=Overview). | - OT networks - Cloud-connected or locally managed OT sensors | Microsoft | [Microsoft Sentinel documentation](/en-us/azure/sentinel/data-connectors/aruba-clearpass) |
| **Aruba ClearPass** (on-premises) | View Defender for IoT data together with Aruba ClearPass data by doing one of the following:- Configure your sensor to send syslog files directly to ClearPass. | - OT networks - Cloud-connected or locally managed OT sensors | Microsoft | [Forward on-premises OT alert information](how-to-forward-alert-information-to-partners)[Defender for IoT API reference](references-work-with-defender-for-iot-apis) |

## Axonius

| Name | Description | Support scope | Supported by | Learn more |
| --- | --- | --- | --- | --- |
| **Axonius Cybersecurity Asset Management** | Import and manage device inventory discovered by Defender for IoT in your Axonius instance. | - OT networks- Locally managed sensors | Axonius | [Axonius documentation](https://docs.axonius.com/docs/azure-defender-for-iot) |

## CyberArk PSM

| Name | Description | Support scope | Supported by | Learn more |
| --- | --- | --- | --- | --- |
| **CyberArk Privileged Session Manager (PSM)** | Send CyberArk PSM syslog data on remote sessions and verification failures to Defender for IoT for data correlation. | - OT networks- Locally managed sensors | Microsoft | [Integrate CyberArk with Microsoft Defender for IoT](tutorial-cyberark) |

## Forescout

| Name | Description | Support scope | Supported by | Learn more |
| --- | --- | --- | --- | --- |
| **Forescout** | Automate actions in Forescout based on activity detected by Defender for IoT, and correlate Defender for IoT data with other *Forescout eyeExtended* modules that oversee monitoring, incident management, and device control. | - OT networks- Locally managed sensors | Microsoft | [Integrate Forescout with Microsoft Defender for IoT](tutorial-forescout) |

## Fortinet

| Name | Description | Support scope | Supported by | Learn more |
| --- | --- | --- | --- | --- |
| **Fortinet FortiSIEM and FortiGate** | Send Defender for IoT data to Fortinet services for: - Enhanced network visibility in FortiSIEM- Extra abilities in FortiGate to stop anomalous behavior | - OT networks- Locally managed sensors | Microsoft | [Integrate Fortinet with Microsoft Defender for IoT](tutorial-fortinet) |

## IBM QRadar

| Name | Description | Support scope | Supported by | Learn more |
| --- | --- | --- | --- | --- |
| **IBM QRadar** | Send Defender for IoT alerts to IBM QRadar | - OT networks - Cloud connected sensors | Microsoft | [Stream Defender for IoT cloud alerts to a partner SIEM](integrations/send-cloud-data-to-partners) |
| **IBM QRadar** | Forward Defender for IoT alerts to IBM QRadar. | - OT networks- Locally managed sensors | Microsoft | [Integrate Qradar with Microsoft Defender for IoT](tutorial-qradar) |

## LogRhythm

| Name | Description | Support scope | Supported by | Learn more |
| --- | --- | --- | --- | --- |
| **LogRhythm** | Forward Defender for IoT alerts to LogRhythm. | - OT networks- Locally managed sensors | Microsoft | [Integrate LogRhythm with Microsoft Defender for IoT](integrations/logrhythm) |

## Micro Focus ArcSight

| Name | Description | Support scope | Supported by | Learn more |
| --- | --- | --- | --- | --- |
| **Micro Focus ArcSight** | Forward Defender for IoT alerts to ArcSight. | - OT networks- Locally managed sensors | Microsoft | [Integrate ArcSight with Microsoft Defender for IoT](integrations/arcsight) |

## Microsoft Defender for Endpoint

| Name | Description | Support scope | Supported by | Learn more |
| --- | --- | --- | --- | --- |
| **Microsoft Defender for Endpoint** | Integrates Defender for IoT data in Defender for Endpoint's device inventory, alerts, recommendations, and vulnerabilities. Displays device data about Defender for Endpoint endpoints in the Defender for IoT **Device inventory** page on the Azure portal. | - Enterprise IoT networks and sensors | Microsoft | [Onboard with Microsoft Defender for IoT](/en-us/microsoft-365/security/defender-endpoint/enable-microsoft-defender-for-iot-integration) |

## Microsoft Sentinel

| Name | Description | Support scope | Supported by | Learn more |
| --- | --- | --- | --- | --- |
| **Defender for IoT data connector in Microsoft Sentinel** (cloud) | Displays Defender for IoT cloud data in Microsoft Sentinel, supporting end-to-end SOC investigations for Defender for IoT alerts. Connects to other partner services, allowing you to synchronize your data between Defender for IoT and supported partner systems, across Microsoft Sentinel. | - OT and Enterprise IoT networks - Cloud-connected sensors | Microsoft | - [OT threat monitoring in enterprise SOCs](concept-sentinel-integration)- [Tutorial: Connect Microsoft Defender for IoT with Microsoft Sentinel](iot-solution)- [Tutorial: Investigate and detect threats for IoT devices](iot-advanced-threat-monitoring) |
| **Microsoft Sentinel** (on-premises) | View Defender for IoT data together with Microsoft Sentinel data by configuring your sensor to send syslog files directly to Microsoft Sentinel. | - OT networks - Cloud-connected or locally managed OT sensors | Microsoft | [Forward on-premises OT alert information](how-to-forward-alert-information-to-partners) |
| **Microsoft Sentinel** (legacy) | Send Defender for IoT alerts from on-premises resources to Microsoft Sentinel. | - OT networks - Locally managed sensors | Microsoft | [Connect on-premises OT network sensors to Microsoft Sentinel](integrations/on-premises-sentinel) |

## Palo Alto

| Name | Description | Support scope | Supported by | Learn more |
| --- | --- | --- | --- | --- |
| **Palo Alto Panorama** (cloud) | View Defender for IoT data together with Panorama data. Use Microsoft Sentinel solutions, which include out-of-the-box workbooks, hunting queries, automation playbooks, and analytics rules, or create custom dashboards, alerts, and more.  Connect to [Microsoft Sentinel](concept-sentinel-integration), and install one or more of the following solutions: - [Palo Alto PAN-OS Solution](/en-us/azure/sentinel/data-connectors/palo-alto-networks-firewall)- [Palo Alto Networks Cortex Data Lake Solution](/en-us/azure/sentinel/data-connectors/palo-alto-networks-cortex-data-lake-cdl)- [Palo Alto Prisma Cloud CSPM solution](/en-us/azure/sentinel/data-connectors/palo-alto-prisma-cloud-cspm-using-azure-function) | - OT networks - Cloud-connected or locally managed OT sensors | Microsoft | Microsoft Sentinel documentation: - [Palo Alto PAN-OS Solution](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azuresentinel.azure-sentinel-solution-paloaltopanos?tab=Overview)- [Palo Alto Networks Cortex Data Lake Solution](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azuresentinel.azure-sentinel-solution-paloaltocdl?tab=Overview)- [Palo Alto Prisma Cloud CSPM solution](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azuresentinel.azure-sentinel-solution-paloaltoprisma?tab=Overview) |
| **Palo Alto Panorama** (on-premises) | View Defender for IoT data together with Panorama data by configuring your sensor to send syslog files directly to Palo Alto Panorama. | - OT networks - Cloud-connected or locally managed OT sensors | Microsoft | [Forward on-premises OT alert information](how-to-forward-alert-information-to-partners) |
| **Palo Alto** (legacy) | Use Defender for IoT data to block critical threats with Palo Alto firewalls, either with automatic blocking or with blocking recommendations. | - OT networks- Locally managed sensors | Microsoft | [Integrate Palo-Alto with Microsoft Defender for IoT](tutorial-palo-alto) |

## RSA NetWitness

| Name | Description | Support scope | Supported by | Learn more |
| --- | --- | --- | --- | --- |
| **RSA NetWitness** | Forward Defender for IoT alerts to RSA NetWitness | - OT networks- Locally managed sensors | Microsoft | [Integrate RSA NetWitness with Microsoft Defender for IoT](integrations/netwitness)[Defender for IoT - RSA NetWitness CEF Parser Implementation Guide](https://community.netwitness.com//t5/netwitness-platform-integrations/cyberx-platform-rsa-netwitness-cef-parser-implementation-guide/ta-p/554364) |

## ServiceNow

| Name | Description | Support scope | Supported by | Learn more |
| --- | --- | --- | --- | --- |
| **Vulnerability Response Integration with Microsoft Defender for IoT** | View Defender for IoT device vulnerabilities in ServiceNow. | - Supports the Central Manager - Locally managed sensors | ServiceNow | [ServiceNow store](https://store.servicenow.com/sn_appstore_store.do#!/store/application/463a7907c3313010985a1b2d3640dd7e/1.0.1?referer=%2Fstore%2Fsearch%3Flistingtype%3Dallintegrations%25253Bancillary_app%25253Bcertified_apps%25253Bcontent%25253Bindustry_solution%25253Boem%25253Butility%25253Btemplate%26q%3Ddefender%2520for%2520iot&amp;sl=sh)[Integrate ServiceNow with Microsoft Defender for IoT](tutorial-servicenow) |
| **Vulnerability Response Integration with Defender for IoT** | View Defender for IoT device vulnerabilities in ServiceNow. | - Supports the Central Manager - Locally managed sensors | ServiceNow | [ServiceNow store](https://store.servicenow.com/sn_appstore_store.do#!/store/application/463a7907c3313010985a1b2d3640dd7e/1.0.5?referer=%2Fstore%2Fsearch%3Flistingtype%3Dallintegrations%25253Bancillary_app%25253Bcertified_apps%25253Bcontent%25253Bindustry_solution%25253Boem%25253Butility%25253Btemplate%25253Bgenerative_ai%25253Bsnow_solution%26q%3Ddefender%2520for%2520IoT&amp;sl=sh)[Integrate ServiceNow with Microsoft Defender for IoT](tutorial-servicenow) |
| **Service Graph Connector Integration with Microsoft Defender for IoT** | View Defender for IoT device detections, sensors, and network connections in ServiceNow. | - Supports the Azure based sensor- Locally managed sensors | ServiceNow | [ServiceNow store](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ddd4bf1b53f130104b5cddeeff7b1229/1.0.0?referer=%2Fstore%2Fsearch%3Flistingtype%3Dallintegrations%25253Bancillary_app%25253Bcertified_apps%25253Bcontent%25253Bindustry_solution%25253Boem%25253Butility%25253Btemplate%26q%3Ddefender%2520for%2520iot&amp;sl=sh)[Integrate ServiceNow with Microsoft Defender for IoT](tutorial-servicenow) |
| **Service Graph Connector for Microsoft Defender for IoT** | View Defender for IoT device detections, sensors, and network connections in ServiceNow. | - Supports the On Premises sensor - Locally managed sensors | ServiceNow | [ServiceNow store](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ddd4bf1b53f130104b5cddeeff7b1229/1.0.4?referer=%2Fstore%2Fsearch%3Flistingtype%3Dallintegrations%25253Bancillary_app%25253Bcertified_apps%25253Bcontent%25253Bindustry_solution%25253Boem%25253Butility%25253Btemplate%25253Bgenerative_ai%25253Bsnow_solution%26q%3Ddefender%2520for%2520IoT&amp;sl=sh)[Integrate ServiceNow with Microsoft Defender for IoT](tutorial-servicenow) |
| **Microsoft Defender for IoT** (Legacy) | View Defender for IoT device detections and alerts in ServiceNow. | - Supports the Legacy version - Locally managed sensors | Microsoft | [ServiceNow store](https://store.servicenow.com/sn_appstore_store.do#!/store/application/6dca6137dbba13406f7deeb5ca961906/3.1.5?referer=%2Fstore%2Fsearch%3Flistingtype%3Dallintegrations%25253Bancillary_app%25253Bcertified_apps%25253Bcontent%25253Bindustry_solution%25253Boem%25253Butility%25253Btemplate%26q%3Ddefender%2520for%2520iot&amp;sl=sh)[Integrate ServiceNow with Microsoft Defender for IoT (legacy)](integrations/service-now-legacy) |

## Skybox

| Name | Description | Support scope | Supported by | Learn more |
| --- | --- | --- | --- | --- |
| **Skybox** | Import vulnerability occurrence data discovered by Defender for IoT in your Skybox platform. | - OT networks- Locally managed sensors | Skybox | [Skybox documentation](https://docs.skyboxsecurity.com)[Skybox integration page](https://www.skyboxsecurity.com/products/integrations) |

## Splunk

| Name | Description | Support scope | Supported by | Learn more |
| --- | --- | --- | --- | --- |
| **Splunk** (cloud) | Send Defender for IoT alerts to Splunk using a SIEM that supports Event Hubs, such as Microsoft Sentinel | - OT networks - Cloud-connected or locally managed OT sensors | Microsoft and Splunk | - [Stream Defender for IoT cloud alerts to a partner SIEM](integrations/send-cloud-data-to-partners) |
| **Splunk** (on-premises) | View Defender for IoT data together with Splunk data by configuring your sensor to send syslog files directly to Splunk. | - OT networks - Cloud-connected or locally managed OT sensors | Microsoft | [Forward on-premises OT alert information](how-to-forward-alert-information-to-partners) |
| **Splunk** (on-premises, legacy integration) | Send Defender for IoT alerts to Splunk | - OT networks- Locally managed sensors | Microsoft | [Integrate Splunk with Microsoft Defender for IoT](tutorial-splunk) |