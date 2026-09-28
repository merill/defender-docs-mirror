---
layout: Conceptual
title: Create trends and statistics reports in Defender for IoT - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/how-to-create-trends-and-statistics-reports
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
description: Gain insight into network activity, statistics, and trends by using Defender for IoT Trends and Statistics widgets.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: eb32b8d7-b9e3-49c7-5dfb-bf3173c4ff75
document_version_independent_id: 70afe3d6-3440-3172-2c83-6137498937ec
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/how-to-create-trends-and-statistics-reports.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/how-to-create-trends-and-statistics-reports
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/how-to-create-trends-and-statistics-reports.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 2219d9ba-c925-bb98-2d8d-27372aa62953
---

# Create trends and statistics reports in Defender for IoT - Microsoft Defender for IoT | Microsoft Learn

Trends and statistics reports are dashboards that provide insight into network trends in traffic detected by a specific OT network sensor.

Create custom dashboards to track specific data needed by your organization, such as traffic, device state, alerts, connectivity, or protocols.

## Prerequisites

To create trends and statistics dashboards, you must be able to access the OT network sensor you want to generate data for, as an **Administrator** or **Security Analyst** user.

For role requirements, see [On-premises users and roles for OT monitoring with Defender for IoT](roles-on-premises)

## Create custom dashboards

Sign into your OT sensor and select **Trends & Statistics** &gt; **Create Dashboard**.

1. In the **Create Dashboard** pane, in the **Dashboard name** field, enter a meaningful name for your dashboard.
2. From the **Dashboard widget type** menu, either leave **All** selected, or select a specific type of widget to view.
3. Scroll down the list of available widgets and select any widget you want to add to your dashboard.
4. When you're done, select **Save** to add your dashboard to the drop-down menu under the toolbar.
5. Use any of the following tools to modify your dashboard:

    | Tool | Description |
    | --- | --- |
    | ![](media/how-to-generate-reports/edit-layout-icon.png)**Edit dashboards layout** | Change the layout of the gadgets in your selected dashboard. |
    | ![](media/how-to-generate-reports/add-icon.png)**Add widget** | Add another widget to your selected dashboard. |
    | ![](media/how-to-generate-reports/edit-icon.png)**Edit dashboard** | Edit the name of your selected dashboard. |
    | ![](media/how-to-generate-reports/delete-icon.png)**Delete dashboard** | Delete the selected dashboard. |
    | ![](media/how-to-generate-reports/default-icon.png)**Set as Default** | Set the selected dashboard as your default dashboard. |

Timestamps shown in each widget are set according to the sensor’s machine time.

By default, results display detections for the current day. Select the ![](media/how-to-generate-reports/filter-icon.png)**Filter** icon at the top left of each widget to change the date range. You can view data for up to a maximum of 14 days.

For example:

[![Screenshot of a widget in a custom dashboard.](media/how-to-generate-reports/custom-dashboard-widgets.png)](media/how-to-generate-reports/custom-dashboard-widgets.png#lightbox)

## Commonly used dashboard widgets

The following table summarizes common use cases for dashboard widgets.

| Widget name | Sample use case |
| --- | --- |
| **Busy devices** | Lists the five busiest devices. In **Edit** mode, you can filter by known protocols. |
| **Total bandwidth** | Tracks the bandwidth in Mbps (megabits per second). The bandwidth is indicated on the y-axis, with the date appearing on the x-axis. **Edit** mode allows you to filter the displayed bandwidth data. |
| **Channels bandwidth** | Displays the top five traffic channels. You can filter by Address, and set the number of Presented Results. Select the down arrow to show more channels. |
| **Traffic by port** | Displays the traffic by port using a pie chart where each port is a different color. For each port, the size of its slice of the pie reflects the amount of traffic in it. |
| **New devices** | Displays the new devices bar chart, showing how many new devices were discovered on a particular date. |
| **Protocol dissection** | Displays a pie chart showing the traffic per protocol, dissected by function codes and services. The size of each slice of the pie reflects the relative amount of traffic in it compared to the other slices. |
| **Active TCP connections** | Displays a chart showing the number of active TCP connections in the system. |
| **Incident by type** | Displays a pie chart showing the number of incidents by type. The count shown is the number of alerts generated by each engine over a predefined time period. |
| **Devices by vendor** | Displays a pie chart showing the number of devices by vendor. For each vendor, the size of their slice of the pie reflects the number of their devices. |
| **Number of devices per VLAN** | Displays a pie chart showing the number of discovered devices per VLAN. The size of each slice of the pie reflects the relative number of discovered device compared to the other slices. Each VLAN appears with the VLAN tag assigned by the sensor or the name that you've manually added. |
| **Top bandwidth by VLAN** | Displays the bandwidth consumption by VLAN. By default, the widget shows five VLANs with the highest bandwidth usage. You can filter the data by the period presented in the widget. Select the down arrow to show more results. |