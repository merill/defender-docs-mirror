---
layout: Conceptual
title: Stream Microsoft Defender for Endpoint events to Azure Event Hubs - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/raw-data-export-event-hub
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to configure Microsoft Defender for Endpoint to stream Advanced Hunting events to your Event Hubs.
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
- must-keep
ms.topic: reference
ms.subservice: reference
ms.custom:
- api
- sfi-ga-nochange
- sfi-image-nochange
ms.date: 2024-06-28T00:00:00.0000000Z
locale: en-us
document_id: 3a67f173-1335-3719-ac10-9ac2c0b112e8
document_version_independent_id: 3a67f173-1335-3719-ac10-9ac2c0b112e8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/raw-data-export-event-hub.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/raw-data-export-event-hub
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/raw-data-export-event-hub.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f0234678-3067-4edc-abf7-8142d54bb7d2
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d774b87-7dcb-40bf-a0b9-5a7a9efff0d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b0f4f6b9-28ed-4892-be4e-517310289c68
- https://authoring-docs-microsoft.poolparty.biz/devrel/89dc5f37-0e4e-4b05-ad87-5fcd2b941a8a
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 21e1111c-c04a-c495-1541-233bd9748361
---

# Stream Microsoft Defender for Endpoint events to Azure Event Hubs - Microsoft Defender for Endpoint | Microsoft Learn

Note

For the full data streaming experience available, please visit [Stream Microsoft Defender XDR events | Microsoft Learn](/en-us/defender-xdr/streaming-api).

## Before you begin

1. Create an [event hub](/en-us/azure/event-hubs/) in your tenant.
2. Sign in to your [Azure tenant](https://ms.portal.azure.com/), go to **Subscriptions** &gt; **Your subscription** &gt; **Resource Providers** &gt; **Register to Microsoft.insights**.

Important

Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

## Enable raw data streaming

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com) as a ***Security Administrator***.
2. Go to the [Data export settings page](https://security.microsoft.com/securitysettings/defender/raw_data_export) in the Microsoft Defender portal.
3. Select **Add data export settings**.
4. Choose a name for your new settings.
5. Choose **Forward events to Azure Event Hubs**.
6. Type your **Event Hubs name** and your **Event Hubs resource ID**.

Note

Leaving Event Hubs name as empty will create an event hub for each category in the selected namespace. Event Hubs namespaces have a limit of 10 Event Hubs if you are not using a Dedicated Event Hubs Cluster.

In order to get your **Event Hubs resource ID**, go to your Azure Event Hubs namespace page on [Azure](https://ms.portal.azure.com/) &gt; properties tab &gt; copy the text under **Resource ID**:

[![The Event Hubs resource Id-1](/en-us/defender-xdr/media/streaming-api-event-hub/event-hub-resource-id.png)](/en-us/defender-xdr/media/streaming-api-event-hub/event-hub-resource-id.png#lightbox)

1. Choose the events you want to stream and select **Save**.

## The schema of the events in Azure Event Hubs

```json
{
    "records": [
                    {
                        "time": "<The time WDATP received the event>"
                        "tenantId": "<The Id of the tenant that the event belongs to>"
                        "category": "<The Advanced Hunting table name with 'AdvancedHunting-' prefix>"
                        "properties": { <WDATP Advanced Hunting event as Json> }
                    }
                    ...
                ]
}
```

- Each event hub message in Azure Event Hubs contains list of records.
- Each record contains the event name, the time Microsoft Defender for Endpoint received the event, the tenant it belongs (you only get events from your tenant), and the event in JSON format in a property called "**properties**".
- For more information about the schema of Microsoft Defender for Endpoint events, see [Advanced Hunting overview](/en-us/defender-xdr/advanced-hunting-overview).
- In Advanced Hunting, the **DeviceInfo** table has a column named **MachineGroup** which contains the group of the device. Here, every event is decorated with this column as well. For more information, see [Device Groups](../machine-groups).

    Note

    Device group creation is supported in Defender for Endpoint Plan 1 and Plan 2.

    The data transferred to Event Hubs might exceed the size estimated using `estimate_data_size()` from Advanced Hunting in the Microsoft Defender portal.

## Data types mapping

To get the data types for event properties, do the following:

1. Sign in to [Microsoft Defender portal](https://security.microsoft.com) and go to [Advanced Hunting page](https://security.microsoft.com/hunting-package).
2. Run the following query to get the data types mapping for each event:

    ```kusto
    {EventType}
    | getschema
    | project ColumnName, ColumnType
    ```

- Here's an example for Device Info event:

    [![The Event Hubs resource Id-2](../media/machine-info-datatype-example.png)](../media/machine-info-datatype-example.png#lightbox)