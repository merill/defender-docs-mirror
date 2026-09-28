---
layout: Conceptual
title: Stream Microsoft Defender XDR events to Azure Event Hubs - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/streaming-api-event-hub
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Configure Microsoft Defender XDR to stream events to Azure Event Hubs for downstream processing and integration.
ms.service: defender-xdr
ms.author: edbaynash
author: EdB-MSFT
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.custom: admindeeplinkDEFENDER, msecd-doc-authoring-1016
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: d58a8573-2739-f389-8c7e-880d27909b9a
document_version_independent_id: d58a8573-2739-f389-8c7e-880d27909b9a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/streaming-api-event-hub.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: streaming-api-event-hub
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/streaming-api-event-hub.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f0234678-3067-4edc-abf7-8142d54bb7d2
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d774b87-7dcb-40bf-a0b9-5a7a9efff0d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b0f4f6b9-28ed-4892-be4e-517310289c68
- https://authoring-docs-microsoft.poolparty.biz/devrel/89dc5f37-0e4e-4b05-ad87-5fcd2b941a8a
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 82371899-8b2e-1956-f994-35432455643b
---

# Stream Microsoft Defender XDR events to Azure Event Hubs - Microsoft Defender XDR | Microsoft Learn

Learn how to configure Microsoft Defender XDR to stream Advanced Hunting events to Azure Event Hubs for downstream processing, integration, and long-term storage.

This article explains how to configure the Microsoft Defender XDR streaming API to forward Advanced Hunting events to Azure Event Hubs for downstream processing, integration, and long-term storage. Security administrators can use this guide to set up streaming, understand the event schema, and estimate the required Event Hub capacity. Before you begin, review the prerequisites to ensure your Event Hubs environment and permissions are in place.

**Applies to:**

- [Microsoft Defender XDR](microsoft-365-defender)

Note

**Try our new APIs using MS Graph security API**. Find out more at: [Use the Microsoft Graph security API - Microsoft Graph | Microsoft Learn](/en-us/graph/api/resources/security-api-overview).

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Prerequisites

Before you configure Microsoft Defender to stream data to Event Hubs, ensure the following prerequisites are fulfilled:

1. Create an Event Hubs (for information, see [Set up Event Hubs](configure-event-hub#set-up-event-hubs)).
2. Creating an Event Hubs Namespace (for information, see [Set up Event Hubs namespace](configure-event-hub#set-up-event-hubs-namespace)).
3. Add permissions to the entity who has the privileges of a **Contributor** so that this entity can export data to the Event Hubs. For more information on adding permissions, see [Add permissions](configure-event-hub#add-permissions)

Note

The Streaming API can be integrated either via Event Hubs or Azure Storage Account.

## Enable raw data streaming

To enable raw data streaming to your Azure event hub, complete the following steps in the Microsoft Defender portal:

1. Sign in [Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2077139) as a ***Security Administrator*** or higher.
2. Go to the [Streaming API settings page](https://sip.security.microsoft.com/settings/mtp_settings/raw_data_export).
3. Select **Add**.
4. Choose a name for your new settings.
5. Choose **Forward events to Azure Event Hub**.
6. You can select if you want to export the event data to a single Event Hub, or to export each event table to a different Event Hubs in your Event Hubs namespace.
7. To export the event data to a single Event Hub, enter your **event hub name** and your **event hub Namespace resource ID**.

    To get your **event hub Namespace resource ID**, go to your Azure Event Hubs namespace page on the [Azure portal](https://ms.portal.azure.com/) &gt; **Properties** tab &gt; copy the text under **Resource ID**:

    [![An Event Hub resource ID](media/streaming-api-event-hub/event-hub-resource-id.png)](media/streaming-api-event-hub/event-hub-resource-id.png#lightbox)
8. Go to the [Supported Microsoft Defender XDR event types in event streaming API](supported-event-types) to review the support status of event types in the Microsoft 365 Streaming API.
9. Choose the events you want to stream and select **Save**.

## Event schema in Azure Event Hub

The following JSON sample shows the structure of an event payload delivered to Azure Event Hubs by the streaming API:

```JSON
{
   "records": [
               {
                  "time": "<The time Microsoft Defender XDR received the event>"
                  "tenantId": "<The Id of the tenant that the event belongs to>"
                  "category": "<The Advanced Hunting table name with 'AdvancedHunting-' prefix>"
                  "properties": { <Microsoft Defender XDR Advanced Hunting event as Json> }
               }
               ...
            ]
}
```

- Each Event Hubs message in Azure Event Hubs contains list of records.
- Each record contains the event name, the time Microsoft Defender received the event, the tenant it belongs (you only get events from your tenant), and the event in JSON format in a property called "**properties**".
- For more information about the schema of Microsoft Defender events, see [Advanced Hunting overview](advanced-hunting-overview).
- In Advanced Hunting, the **DeviceInfo** table has a column named **MachineGroup** which contains the group of the device. Here, every event is decorated with this column as well.

## Data type mappings

To get the data types for event properties:

1. Sign in [Microsoft Defender XDR](https://go.microsoft.com/fwlink/p/?linkid=2077139) and go to [Advanced Hunting page](https://security.microsoft.com/hunting-package).
2. Replace `{EventType}` with your event table name and run the following query to retrieve the column names and data types for that event:

    ```kusto
    {EventType}
    | getschema
    | project ColumnName, ColumnType
    ```

- Here's an example for Device Info event:

    [![An example query for device info](/en-us/defender-endpoint/media/machine-info-datatype-example.png)](/en-us/defender-endpoint/media/machine-info-datatype-example.png#lightbox)

## Estimating initial Event Hub capacity

The following advanced hunting query can help provide a rough estimate of data volume throughput and initial event hub capacity based on events/sec and estimated MB/sec. We recommend running the query during regular business hours so as to capture 'real' throughput.

Use this query to estimate table volume over the past seven days. The output shows the average events per second and estimated MB/sec for each table, which you can use to determine the required event hub throughput units.

```kusto
let bytes_ = 1000;
union withsource=MDTables MyDefenderTable // TODO: Insert desired tables one by one separated by a comma (for example: DeviceEvents, DeviceInfo) or with a wildcard (Device*)
| where Timestamp > startofday(ago(7d))
| summarize count() by bin(Timestamp, 1m), MDTables
| extend EPS = count_ /60 
| summarize avg(EPS), estimatedMBPerSec = avg(EPS) * bytes_ / (1024*1024) by MDTables, bin(Timestamp, 3h)
| summarize avg_EPS=max(avg_EPS), estimatedMBPerSec = max(estimatedMBPerSec) by MDTables
| sort by toint(estimatedMBPerSec) desc
| project MDTables, avg_EPS, estimatedMBPerSec
```

To check the different Event Hub limits, review [Azure Event Hubs quota and limits](/en-us/azure/event-hubs/event-hubs-quotas).

## Monitoring created resources

You can monitor the resources created by the streaming API using **Azure Monitor**. To learn how to export log data for analyzing streaming API resources, see [Log Analytics workspace data export in Azure Monitor](/en-us/azure/azure-monitor/logs/logs-data-export).