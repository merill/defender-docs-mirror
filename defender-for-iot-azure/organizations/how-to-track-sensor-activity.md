---
layout: Conceptual
title: Track Network and Sensor Activity with the Event Timeline in Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/how-to-track-sensor-activity
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
description: Track network and sensor activity in the event timeline.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: abdd7c5c-e076-8dc3-c748-bfba0d02ddac
document_version_independent_id: c84d93c5-e363-4e39-9010-6f6a2745edda
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/how-to-track-sensor-activity.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/how-to-track-sensor-activity
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/how-to-track-sensor-activity.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 5e1aa6d7-880e-0898-186e-ad7d538c845e
---

# Track Network and Sensor Activity with the Event Timeline in Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn

Activity your Microsoft Defender for IoT sensors detect is recorded in the event timeline. Activity includes alerts and alert management actions, network events, and user operations such as user sign-in or user deletion.

The OT sensor's event timeline provides a chronological view and context of all network activity to help determine the cause and effect of incidents. The timeline view makes it easy to extract information from network events and more efficiently analyze alerts and events observed on the network. With the ability to store vast amounts of data, the event timeline view can be a valuable resource for security teams to perform investigations and gain a deeper understanding of network activity.

Use the event timeline during investigations to understand and analyze the chain of events that preceded and followed an attack or incident. The centralized view of multiple security-related events on the same timeline helps to identify patterns and correlations, and enable security teams to quickly assess the impact of incidents and respond accordingly.

For more information, see:

- View events on the timeline
- [Audit user activity](track-user-activity)
- [View and manage alerts](how-to-view-alerts#view-details-and-remediate-a-specific-alert)
- [Analyze programming details and changes](how-to-analyze-programming-details-changes)

## Permissions required to view the event timeline

Before you perform the event timeline procedures described in this article, make sure that you have access to an OT sensor as an **Admin** or **Security Analyst** role. For more information, see [On-premises users and roles for OT monitoring with Defender for IoT](roles-on-premises).

## View the event timeline

1. Sign in to the sensor console and select **Event Timeline** from the left menu.
2. Review and filter the events as needed.
3. Select an event row to view the event details in a pane on the right, where you can also filter to view events of related devices. The **User Operations** filter is on by default, you can select to hide or show user events as needed.

    For example:

    [![Screenshot of events on the event timeline.](media/track-sensor-activity/event-timeline-view-events.png)](media/track-sensor-activity/event-timeline-view-events.png#lightbox)

You can also view the event timeline of a specific device from the **Device inventory**.

To view the event timeline of a specific device:

1. In the sensor console, go to **Device inventory**.
2. Select the specific device to open the device details pane, and then select **View full details** to open the device properties page.
3. Select the **Event timeline** tab to view all events associated with this device, and filter events on the timeline as needed.

    For example:

    [![Screenshot of event timeline tab in device properties page.](media/track-sensor-activity/device-properties-page-event-timeline.png)](media/track-sensor-activity/device-properties-page-event-timeline.png#lightbox)

## Filter events on the timeline

Use the following steps to filter events shown on the timeline:

1. On the event timeline page, select **Add filter** to specify the events shown.
2. Select the filter **Type**. Use any of the following options to filter the devices shown:

    | Type | Description |
    | --- | --- |
    | **User operations** | This filter is on by default, choose to show or hide user operation events. |
    | **Date** | Search for events in a specific date range. |
    | **Device group** | Filter specific devices by group as defined in the device map. |
    | **Event severity** | Show **Alerts Only**, **Alerts and Notices**, or **All Events**. |
    | **Exclude devices** | Search for and filter devices you want to exclude. |
    | **Include devices** | Search for and filter devices you want to include. |
    | **Exclude Event Types** | Search for and filter specific event types to exclude. |
    | **Include Event Types** | Search for and filter specific event types to include. |
    | **Keywords** | Filter events by specific keywords. |
3. Select **Apply** to set the filter.

## Export the event timeline to CSV

You can export the event timeline to a CSV file. The exported data is according to any filters applied when exporting.

To export the event timeline:

On the **Event timeline** page, select **Export** from the top menu to export the event timeline to a CSV file.

## Create an event

In addition to viewing the events that the sensor has detected, you can manually add events to the timeline. This process is useful if an external system event impacts your network and you want to record it on the timeline.

**To manually add an event to the timeline**:

1. On the **Event timeline** page, select **Create Event**.
2. In the **Create Event** dialog, add the following event details:

    - **Type**: Specify the event type (Info, Notice, or Alert).
    - **Timestamp**: Set the date and time of the event.
    - **Device**: Select the device the event should be connected with.
    - **Description**: Provide a description of the event.
3. Select **Save** to add the event to the timeline.

For example:

[![Screenshot of creating a new event in the timeline.](media/track-sensor-activity/create-new-event.png)](media/track-sensor-activity/create-new-event.png#lightbox)

## Event timeline capacity

The amount of data that can be stored in the event timeline depends on various factors, such as the size of the network, the frequency of events, and the storage capacity of your sensor. The data stored in the event timeline can include information about network traffic, security events, and other relevant data points.

The maximum number of events shown in the event timeline is dependent on [the OT appliance sizing and hardware profile](ot-appliance-sizing) selected during sensor installation. Each hardware profile has a maximum capacity of events. For more information on maximum event capacity by OT appliance hardware profile, see [OT event timeline retention](references-data-retention#ot-event-timeline-retention).