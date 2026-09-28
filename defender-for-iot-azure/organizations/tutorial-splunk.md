---
layout: Conceptual
title: Integrate Splunk with Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/tutorial-splunk
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
description: This article describes how to integrate Splunk with Microsoft Defender for IoT for multidimensional visibility across OT protocols and IIoT devices.
ms.topic: how-to
ms.date: 2026-06-12T00:00:00.0000000Z
ms.custom: how-to, msecd-doc-authoring-1014
ai-usage: ai-assisted
locale: en-us
document_id: 0c991bf8-6f7f-b733-bbc5-ab5b264c9c01
document_version_independent_id: 56a37c0c-2e14-53e7-3158-836c0b199c6e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/tutorial-splunk.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/tutorial-splunk
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/tutorial-splunk.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 4ee8cce7-1d06-1c75-effd-f83de5459393
---

# Integrate Splunk with Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn

This article describes how to integrate Splunk with Microsoft Defender for IoT, in order to view both Splunk and Defender for IoT information in a single place.

Viewing both Defender for IoT and Splunk information together provides SOC analysts with multidimensional visibility into the specialized OT protocols and IIoT devices deployed in industrial environments, along with ICS-aware behavioral analytics to rapidly detect suspicious or anomalous behavior.

Before you begin, make sure you have a Defender for IoT OT sensor deployed and a Splunk environment configured. If you're using the legacy integration, see the Prerequisites section for specific version and permission requirements.

If you're integrating with Splunk, we recommend that you use Splunk's own [OT Security Add-on for Splunk](https://apps.splunk.com/app/5151). For more information, see:

- [The Splunk documentation on installing add-ins](https://docs.splunk.com/Documentation/AddOns/released/Overview/Distributedinstall)
- [The Splunk documentation on the OT Security Add-on for Splunk](https://splunk.github.io/ot-security-solution/integrationguide/)

The OT Security Add-on for Splunk is supported for both cloud and on-premises integrations.

## Integrate cloud-based Splunk deployments with Defender for IoT

Tip

Cloud-based security integrations provide several benefits over on-premises solutions, such as centralized, simpler sensor management and centralized security monitoring.

Other benefits include real-time monitoring, efficient resource use, increased scalability and robustness, improved protection against security threats, simplified maintenance and updates, and seamless integration with third-party solutions.

To integrate a cloud-connected sensor with Splunk, we recommend that you use the [OT Security Add-on for Splunk](https://apps.splunk.com/app/5151).

## Integrate on-premises Splunk deployments with Defender for IoT

If you're working with an air-gapped, locally managed sensor, you might also want to configure your sensor to send syslog files directly to Splunk, or use Defender for IoT's built-in API.

For more information, see:

- [Forward on-premises OT alert information](how-to-forward-alert-information-to-partners)
- [Defender for IoT API reference](references-work-with-defender-for-iot-apis)

## Set up the legacy on-premises Splunk integration

The following instructions describe how to integrate Defender for IoT and Splunk using the legacy [CyberX ICS Threat Monitoring for Splunk](https://splunkbase.splunk.com/app/4313) application.

Important

The legacy **CyberX ICS Threat Monitoring for Splunk** application is supported through October 2024 using sensor version 23.1.3, and won't be supported in upcoming major software versions.

For customers using the legacy CyberX ICS Threat Monitoring for Splunk application, we recommend using one of the following methods instead:

- Use the [OT Security Add-on for Splunk](https://apps.splunk.com/app/5151)
- Configure your OT sensor to [forward syslog events](how-to-forward-alert-information-to-partners)
- Use [Defender for IoT APIs](references-work-with-defender-for-iot-apis)

Microsoft Defender for IoT was formally known as [CyberX](https://blogs.microsoft.com/blog/2020/06/22/microsoft-acquires-cyberx-to-accelerate-and-secure-customers-iot-deployments/). References to CyberX refer to Defender for IoT.

### Prerequisites

Before you begin, make sure that you have the following prerequisites:

| Prerequisites | Description |
| --- | --- |
| **Version requirements** | The following versions are required for the application to run: - Defender for IoT version 2.4 and above. - Splunkbase version 11 and above. - Splunk Enterprise version 7.2 and above. |
| **Permission requirements** | Make sure you have: - Access to a Defender for IoT OT sensor as an [Admin user](roles-on-premises). - Splunk user with an *Admin* level user role. |

Note

The Splunk application can be installed locally ('Splunk Enterprise') or run on a cloud ('Splunk Cloud'). The Splunk integration along with Defender for IoT supports 'Splunk Enterprise' only.

### Download the Defender for IoT application in Splunk

To access the Defender for IoT application within Splunk, you need to download the application from the Splunkbase application store.

To access the Defender for IoT application in Splunk:

1. Navigate to the [Splunkbase](https://splunkbase.splunk.com/) application store.
2. Search for `CyberX ICS Threat Monitoring for Splunk`.
3. Select the CyberX ICS Threat Monitoring for Splunk application.
4. Select the **LOGIN TO DOWNLOAD BUTTON**.