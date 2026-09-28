---
layout: Conceptual
title: Visualize Microsoft Defender for IoT Data with Azure Monitor Workbooks - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/workbooks
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
description: Learn how to view and create Azure Monitor workbooks for Defender for IoT data.
ms.topic: how-to
ms.date: 2026-06-12T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: 0570f85e-8c1e-de4a-5736-67f128e9a881
document_version_independent_id: 091e5ce1-50d4-5aae-9c32-11f6f8e936be
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/workbooks.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/workbooks
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/workbooks.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/d3928677-9b71-43a6-875f-004dc4f98b65
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/6bbc70ca-58b2-4c69-8249-28ec92c08029
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: b9a25369-d795-3ff8-2a20-c609927fe43c
---

# Visualize Microsoft Defender for IoT Data with Azure Monitor Workbooks - Microsoft Defender for IoT | Microsoft Learn

## Overview

Azure Monitor workbooks provide graphs, charts, and dashboards that visually reflect data stored in your Azure Resource Graph subscriptions and are available directly in Microsoft Defender for IoT.

In the Azure portal, use the Defender for IoT **Workbooks** page to view workbooks created by Microsoft and provided out-of-the-box, or created by customers and shared across the community.

Each workbook graph or chart is based on an Azure Resource Graph (ARG) query running on your data. In Defender for IoT, you might use ARG queries to:

- Gather sensor statuses
- Identify new devices in your network
- Find alerts related to specific IP addresses
- Understand which alerts are seen by each sensor

## View workbooks

To view out-of-the-box workbooks created by Microsoft, or other workbooks already saved to your subscription:

1. In the Azure portal, go to **Defender for IoT** and select **Workbooks** on the left.

    [![Screenshot of the Workbooks page.](media/workbooks/workbooks.png)](media/release-notes/workbooks.png#lightbox)
2. Modify your filtering options if needed, and select a workbook to open it.

Defender for IoT provides the following workbooks out-of-the-box:

- **Sensor health**. Displays data about your sensor health, such as the sensor console software versions installed on your sensors.
- **Alerts**. Displays data about alerts occurring on your sensors, including alerts by sensor, alert types, recent alerts generated, and more.
- **Devices**. Displays data about your device inventory, including devices by vendor, subtype, and new devices identified.
- **Vulnerabilities**. Displays data about the Vulnerabilities detected in OT devices across your network. Select an item in the **Device vulnerabilities**, **Vulnerable devices**, or **Vulnerable components** tables to view related information in the tables on the right.

## Create custom workbooks

Use the Defender for IoT **Workbooks** page to create custom Azure Monitor workbooks directly in Defender for IoT.

1. On the **Workbooks** page, select **New**, or to start from another template, open the template workbook and select **Edit**.
2. In your new workbook, select **Add**, and select the option you want to add to your workbook. If you're editing an existing workbook or template, select the options (**...**) button on the right to access the **Add** menu.

    You can add any of the following elements to your workbook:

    | Option | Description |
    | --- | --- |
    | **Text** | Add text to describe the graphs shown on your workbook or any additional action required. |
    | **Parameters** | Define parameters to use in your workbook text and queries. |
    | **Links / tabs** | Add navigational elements to your workbook, including lists, links to other targets, extra tabs, or toolbars. |
    | **Query** | Add a query to use when creating your workbook graphs and charts. - Make sure to select **Azure Resource Graph** as your **Data source** and select all of your relevant subscriptions. - Add a graphical representation for your data by selecting a type from the **Visualization** options. |
    | **Metric** | Add metrics to use when creating workbook graphs and charts. |
    | **Group** | Add groups to organize your workbooks into sub-areas. |

    For each option, after you've defined all available settings, select the **Add...** or **Run...** button to create that workbook element. For example, **Add parameter** or **Run Query**.

    Tip

    You can build your queries in the [Azure Resource Graph Explorer](https://portal.azure.com/#blade/HubsExtension/ArgQueryBlade) and copy them into your workbook query.
3. In the toolbar, select **Save**![](media/workbooks/save-icon.png) or **Save as**![](media/workbooks/save-as-icon.png) to save your workbook, and then select **Done editing**.
4. Select **Workbooks** to go back to the main workbook page with the full workbook listing.

### Reference parameters in your queries

In a Defender for IoT workbook, after you add a **Parameters** element to your custom workbook, you can reference the parameter in your Azure Resource Graph queries using the following syntax: `{ParameterName}`. For example:

```kusto
iotsecurityresources
| where type == "microsoft.iotsecurity/sensors"
| extend Name=name
| extend Status= properties.sensorStatus
| where Name=={SensorName}
| project Name,Status
```

## Sample workbook queries for Defender for IoT

The following sample Azure Resource Graph (ARG) queries are commonly used in Defender for IoT workbooks.

### Alert queries

Use the following sample queries to analyze alert data in your Defender for IoT workbooks.

#### Distribution of alerts across sensors

```kusto
iotsecurityresources
| where type == "microsoft.iotsecurity/locations/devicegroups/alerts"
| extend Sensor=properties.extendedProperties.SensorId
| where properties.status!='Closed'
| summarize Alerts=count() by tostring(Sensor)
| sort by Alerts desc
```

#### New alerts from the last 24 hours

```kusto
iotsecurityresources
| where type == "microsoft.iotsecurity/locations/devicegroups/alerts"
| where properties.status!='Closed'
| extend AlertTime=properties.startTimeUtc
| extend Type=properties.displayName
| where AlertTime > ago(1d)
| project AlertTime, Type
```

#### Alerts by source IP address

Use the following query to list alerts associated with a specific source IP address, along with their destination IP and alert type.

```kusto
iotsecurityresources
| where type == "microsoft.iotsecurity/locations/devicegroups/alerts"
| extend Type=properties.displayName
| extend Source_IP=properties.extendedProperties.SourceDeviceAddress
| extend Destination_IP=properties.extendedProperties.DestinationDeviceAddress
| where Source_IP=='192.168.10.1'
| project Source_IP, Destination_IP, Type
```

### Device queries

The following sample queries help you explore OT device inventory and related device data in your Defender for IoT workbooks.

#### OT device inventory by vendor

The following query groups OT device inventory by hardware vendor to help you identify the distribution of vendors in your environment.

```kusto
iotsecurityresources
| extend Vendor= properties.hardware.vendor
| where properties.deviceDataSource=='OtSensor'
| summarize Devices=count() by tostring(Vendor)
| sort by Devices
```

#### OT device inventory by sub-type, such as PLC, embedded device, UPS, and so on

Use the following query to break down OT devices by sub-type, such as PLCs and UPS devices, for inventory analysis.

```kusto
iotsecurityresources
| where type == "microsoft.iotsecurity/locations/devicegroups/devices"
| extend SubType=properties.deviceSubTypeDisplayName
| summarize Devices=count() by tostring(SubType)
| sort by Devices
```

#### New OT devices by sensor, site, and IPv4 address

Use the following query to list new OT devices discovered in the last 24 hours, along with their sensor, site, and IPv4 address details.

```kusto
iotsecurityresources
| where type == "microsoft.iotsecurity/locations/devicegroups/devices"
| extend TimeFirstSeen=properties.firstSeen
| where TimeFirstSeen > ago(1d)
| extend DeviceName=properties.deviceName
| extend Site=properties.sensor.site
| extend Sensor=properties.sensor.name
| extend IPv4=properties.nics.[0].ipv4Address
| where properties.deviceDataSource=='OtSensor'
| project TimeFirstSeen, Site, Sensor, DeviceName, IPv4
```

#### Summarize alerts by Purdue level

Use the following query to count alerts by Purdue level, joining alert data with OT device information to help you understand which network layers generate the most alerts.

```kusto
iotsecurityresources
    | where type == "microsoft.iotsecurity/locations/devicegroups/alerts"
    | project 
        resourceId = id,
        affectedResource = tostring(properties.extendedProperties.DeviceResourceIds),
        id = properties.systemAlertId
    | join kind=leftouter (
        iotsecurityresources | where type == "microsoft.iotsecurity/locations/devicegroups/devices" 
        | project 
            sensor = properties.sensor.name,
            zone = properties.sensor.zone,
            site = properties.sensor.site,
            deviceProperties=properties,
            affectedResource = tostring(id)
    ) on affectedResource
    | project-away affectedResource1
    | where deviceProperties.deviceDataSource == 'OtSensor'
    | summarize Alerts=count() by tostring(deviceProperties.purdueLevel)
```