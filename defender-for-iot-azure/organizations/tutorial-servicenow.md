---
layout: Conceptual
title: Integrate ServiceNow with Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/tutorial-servicenow
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
description: Connect ServiceNow with Microsoft Defender for IoT to centralize OT and IoT asset visibility, monitoring, and threat management using the Operational Technology Manager integration.
ms.topic: how-to
ms.date: 2026-06-12T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: 8116bb75-052f-09f7-1ad7-7cb277b17214
document_version_independent_id: 647bde5b-1507-2c28-d28a-761afb639db4
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/tutorial-servicenow.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/tutorial-servicenow
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/tutorial-servicenow.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 016fa756-13df-181f-0f1e-ac41d2c713d3
---

# Integrate ServiceNow with Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn

The Defender for IoT integration with ServiceNow provides an extra level of centralized visibility, monitoring, and control for the IoT and OT landscape. The Microsoft Defender for IoT and ServiceNow platforms together enable automated device visibility and threat management for previously unreachable ICS & IoT devices.

The [Operational Technology Manager](https://store.servicenow.com/sn_appstore_store.do#!/store/application/31eed0f72337201039e2cb0a56bf65ef/1.1.2?referer=%2Fstore%2Fsearch%3Flistingtype%3Dallintegrations%25253Bancillary_app%25253Bcertified_apps%25253Bcontent%25253Bindustry_solution%25253Boem%25253Butility%25253Btemplate%26q%3Doperational%2520technology%2520manager&amp;sl=sh) integration is available from the ServiceNow store, which streamlines Microsoft Defender for IoT sensor appliances, OT assets, network connections, and vulnerabilities to ServiceNow’s Operational Technology (OT) data model.

## ServiceNow integrations with Microsoft Defender for IoT

The Operational Technology Manager is a ServiceNow application that serves as the base platform for Defender for IoT integrations. Once you have the Operational Technology Manager application installed, two integrations are available: Service Graph Connector (SGC) and Vulnerability Response (VR).

### Use the Service Graph Connector (SGC) integration

Import Microsoft Defender for IoT sensors with more attributes, including connection details and Purdue model zones, into the Network Intrusion Detection Systems (NIDS) class. Provide visibility into your OT network status and manage it within the ServiceNow application.

For more information about the Microsoft Defender for IoT option, see the [Service Graph Connector (SGC) Integration with Microsoft Defender for IoT](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ddd4bf1b53f130104b5cddeeff7b1229) information on the ServiceNow store.

### Use the Vulnerability Response (VR) integration

Track and resolve vulnerabilities of your OT assets with the data imported from Defender for IoT into the ServiceNow Operational Technology Vulnerability Response application.

For more information about the Microsoft Defender for IoT option, see the [Vulnerability Response (VR)](https://store.servicenow.com/sn_appstore_store.do#!/store/application/a187f54f9713e91088ae3e0e6253afcf/1.0.1?referer=%2Fstore%2Fsearch%3Flistingtype%3Dallintegrations%25253Bancillary_app%25253Bcertified_apps%25253Bcontent%25253Bindustry_solution%25253Boem%25253Butility%25253Btemplate%25253Bgenerative_ai%25253Bsnow_solution%26q%3Ddefender%2520for%2520IoT&amp;sl=sh) information on the ServiceNow store.

For more information, see the [ServiceNow documentation](https://docs.servicenow.com/) and the [ServiceNow terms of service](https://www.servicenow.com/standard-privacy/terms-of-service.html).