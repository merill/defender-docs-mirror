---
layout: Conceptual
title: Investigate incidents in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/investigate-incidents
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: See associated alerts, manage the incident, and see alert metadata to help you investigate an incident
ms.service: defender-endpoint
ms.author: chrisda
author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- mde-edr
ms.topic: concept-article
ms.subservice: edr
ms.date: 2024-06-05T00:00:00.0000000Z
ms.custom: sfi-image-nochange
locale: en-us
document_id: c713d839-99c0-d24b-f39b-261a677ff417
document_version_independent_id: c713d839-99c0-d24b-f39b-261a677ff417
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/investigate-incidents.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: investigate-incidents
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/investigate-incidents.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: d9c292eb-1677-a0d9-fef1-3b5999eed9f7
---

# Investigate incidents in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

Investigate incidents that affect your network, understand what they mean, and collate evidence to resolve them.

When you investigate an incident, you'll see:

- Incident details
- Incident comments and actions
- Tabs (alerts, devices, investigations, evidence, graph)

## Analyze incident details

Click an incident to see the **Incident pane**. Select **Open incident page** to see the incident details and related information (alerts, devices, investigations, evidence, graph).

[![The details of an incident](media/atp-incident-details.png)](media/atp-incident-details.png#lightbox)

### Alerts

You can investigate the alerts and see how they were linked together in an incident. Alerts are grouped into incidents based on the following reasons:

- Automated investigation - The automated investigation triggered the linked alert while investigating the original alert
- File characteristics - The files associated with the alert have similar characteristics
- Manual association - A user manually linked the alerts
- Proximate time - The alerts were triggered on the same device within a certain timeframe
- Same file - The files associated with the alert are exactly the same
- Same URL - The URL that triggered the alert is exactly the same

[![The Alerts tab with incident details page showing the reasons the alerts were linked together in that incident](media/atp-incidents-alerts-reason.png)](media/atp-incidents-alerts-reason.png#lightbox)

You can also manage an alert and see alert metadata along with other information. For more information, see [Investigate alerts](investigate-alerts).

### Devices

You can also investigate the devices that are part of, or related to, a given incident. For more information, see [Investigate devices](investigate-machines).

[![The Devices tab in incident details page](media/atp-incident-device-tab.png)](media/atp-incident-device-tab.png#lightbox)

### Investigations

Select **Investigations** to see all the automatic investigations launched by the system in response to the incident alerts.

[![The investigations tab in the incident details page](media/atp-incident-investigations-tab.png)](media/atp-incident-investigations-tab.png#lightbox)

## Going through the evidence

Microsoft Defender for Endpoint automatically investigates all the incidents' supported events and suspicious entities in the alerts, providing you with autoresponse and information about the important files, processes, services, and more.

Each of the analyzed entities will be marked as infected, remediated, or suspicious.

[![The Evidence tab in incident details page](media/atp-incident-evidence-tab.png)](media/atp-incident-evidence-tab.png#lightbox)

## Visualizing associated cybersecurity threats

Microsoft Defender for Endpoint aggregates the threat information into an incident so you can see the patterns and correlations coming in from various data points. You can view such correlation through the incident graph.

### Incident graph

The **Graph** tells the story of the cybersecurity attack. For example, it shows you what was the entry point, which indicator of compromise or activity was observed on which device. etc.

[![The incident graph](media/atp-incident-graph-tab.png)](media/atp-incident-graph-tab.png#lightbox)

You can click the circles on the incident graph to view the details of the malicious files, associated file detections, how many instances have there been worldwide, whether it's been observed in your organization, if so, how many instances.

[![The incident details page](media/atp-incident-graph-details.png)](media/atp-incident-graph-details.png#lightbox)