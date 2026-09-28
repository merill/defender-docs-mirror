---
layout: Conceptual
title: Use the streaming API with Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-business/mdb-streaming-api
breadcrumb_path: /defender-business/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: The Defender for Endpoint streaming API is available for Defender for Business and Microsoft 365 Business Premium. Stream of device file, registry, network, sign-in events, and other data to Azure Event Hubs, Azure Storage, and Microsoft Sentinel to support advanced hunting and attack detection.
author: chrisda
ms.author: chrisda
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.service: microsoft-365-security
ms.localizationpriority: medium
ms.collection:
- SMB
- m365-security
- m365solution-mdb-setup
- highpri
- tier1
ms.reviewer: davidb, nehabha, efratka
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 485951d1-4cd8-0e49-6034-fdc74926e554
document_version_independent_id: 485951d1-4cd8-0e49-6034-fdc74926e554
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-business/mdb-streaming-api.md
site_name: Docs
depot_name: Learn.defender-business
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdb-streaming-api
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-business/mdb-streaming-api.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d774b87-7dcb-40bf-a0b9-5a7a9efff0d1
- https://authoring-docs-microsoft.poolparty.biz/devrel/f0234678-3067-4edc-abf7-8142d54bb7d2
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/89dc5f37-0e4e-4b05-ad87-5fcd2b941a8a
- https://authoring-docs-microsoft.poolparty.biz/devrel/b0f4f6b9-28ed-4892-be4e-517310289c68
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 59c9a31b-b191-3c57-2d09-26480cb3484e
---

# Use the streaming API with Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn

If your organization has a Security Operations Center (SOC), the ability to use the [Microsoft Defender for Endpoint streaming API](/en-us/defender-endpoint/api/raw-data-export) is available for [Defender for Business](mdb-overview) and [Microsoft 365 Business Premium](/en-us/microsoft-365/business-premium/m365bp-overview). The Microsoft Defender for Endpoint streaming API enables you to stream data, such as device file, registry, network, sign-in events, and more to one of the following services:

- Microsoft Sentinel: A scalable, cloud-native solution that provides security information and event management (SIEM) and security orchestration, automation, and response (SOAR) capabilities.
- Azure Event Hubs: A modern, big data streaming platform and event ingestion service that can seamlessly integrate with other Azure and Microsoft services. For example, Stream Analytics, Power BI, and Event Grid, along with outside services like Apache Spark.
- [Azure Storage](/en-us/azure/storage/common/storage-introduction): Microsoft's cloud storage solution for modern data storage scenarios, with highly available, massively scalable, durable, and secure storage for a variety of data objects in the cloud.

With the Microsoft Defender for Endpoint streaming API, you can use [advanced hunting](/en-us/defender-xdr/advanced-hunting-overview) and [attack detection](/en-us/defender-endpoint/overview-endpoint-detection-response) with Defender for Business and Microsoft 365 Business Premium. The streaming API enables security operations centers to view more data about devices, understand better how an attack occurred, and take steps to improve device security.

## Use the streaming API with Microsoft Sentinel

To stream Defender for Business data to Microsoft Sentinel, complete the following steps.

Note

[Microsoft Sentinel](/en-us/azure/sentinel/overview) is a paid service. Several plans and pricing options are available. See [Microsoft Sentinel pricing](https://www.microsoft.com/security/pricing/microsoft-sentinel/).

1. Make sure that Defender for Business is set up and configured, and that devices are already onboarded. See [Set up and configure Microsoft Defender for Business](mdb-setup-configuration).
2. Create a Log Analytics workspace to use with Microsoft Sentinel. See [Create a Log Analytics workspace](/en-us/azure/azure-monitor/logs/quick-create-workspace?tabs=azure-portal).
3. Onboard to Microsoft Sentinel. See [Quickstart: Onboard Microsoft Sentinel](/en-us/azure/sentinel/quickstart-onboard).
4. Enable the Microsoft Defender connector. See [Connect data from Microsoft Defender to Microsoft Sentinel](/en-us/azure/sentinel/connect-microsoft-365-defender?tabs=MDE).

## Use the streaming API with Event Hubs

[Azure Event Hubs](/en-us/azure/event-hubs/event-hubs-about) requires an Azure subscription. Before you begin, make sure to create an [event hub](/en-us/azure/event-hubs/) in your organization. Then, sign in to the [Azure portal](https://ms.portal.azure.com/), go to **Subscriptions** &gt; **Your subscription** &gt; **Resource Providers** &gt; **Register to Microsoft.insights**.

To configure streaming to Azure Event Hubs, complete the following steps.

1. Go to the [Microsoft Defender portal](https://security.microsoft.com) and sign in.
2. Go to the [Data export settings page](https://security.microsoft.com/interoperability/dataexport).
3. Select **Add data export settings**.
4. Choose a name for your new settings.
5. Choose **Forward events to Azure Event Hubs**.
6. Type your **Event Hubs name** and your **Event Hubs ID**.

    Note

    Leaving the Event Hubs name field empty creates an event hub for each category in the selected namespace. If you're not using a [Dedicated Event Hubs Cluster](/en-us/azure/event-hubs/event-hubs-dedicated-overview) (a single-tenant deployment with dedicated capacity), keep in mind that there's a limit of 10 Event Hubs namespaces.

    To get your **Event Hubs ID**, go to your Azure Event Hubs namespace page in the [Azure portal](https://ms.portal.azure.com/). On the **Properties** tab, copy the text under **ID**.
7. Choose the events you want to stream and then select **Save**.

### View the event schema in Azure Event Hubs

The following JSON sample shows the format of each event hub message that Azure Event Hubs receives when event forwarding is enabled. Each message contains a `records` array with one or more event entries:

```json
{
    "records": [
                    {
                        "time": "<The time WDATP received the event>"
                        "tenantId": "<The Id of the organization that the event belongs to>"
                        "category": "<The Advanced Hunting table name with 'AdvancedHunting-' prefix>"
                        "properties": { <WDATP Advanced Hunting event as Json> }
                    }
                    ...
                ]
}
```

Each event hub message in Azure Event Hubs contains a list of records. Each record contains the event name, the time Defender for Business received the event, the organization to which it belongs (you get events from your organization only), and the event in JSON format in a property called "**properties**". For more information about the schema of Advanced Hunting events streamed to Azure Event Hubs, see [Proactively hunt for threats with advanced hunting in Microsoft Defender](/en-us/defender-xdr/advanced-hunting-overview).

## Use the streaming API with Azure Storage

To configure streaming to Azure Storage, complete the following steps.

Note

[Azure Storage](/en-us/azure/storage/common/storage-introduction) requires an Azure subscription. Before you begin, make sure to create a [Storage account](/en-us/azure/storage/common/storage-account-overview) in your organization. Then, sign in to your [Azure organization](https://ms.portal.azure.com/), and go to **Subscriptions** &gt; **Your subscription** &gt; **Resource Providers** &gt; **Register to Microsoft.insights**.

### Enable raw data streaming

Raw data streaming forwards security event data from Defender for Business directly to your Azure Storage account, where you can retain and analyze it. To enable raw data streaming to Azure Storage, complete the following steps.

1. Go to the [Microsoft Defender portal](https://security.microsoft.com) and sign in.
2. Go to [Data export settings page](https://security.microsoft.com/settings/mtp_settings/raw_data_export) in Microsoft Defender XDR.
3. Select **Add data export settings**.
4. Choose a name for your new settings.
5. Choose **Forward events to Azure Storage**.
6. Type your **Storage Account Resource ID**. In order to get your **Storage Account Resource ID**, go to your Storage account page in the [Azure portal](https://ms.portal.azure.com/). Then, on the **Properties** tab, copy the text under **Storage account resource ID**.
7. Choose the events you want to stream and then select **Save**.

### View the event schema in Azure Storage

A blob container is created for each event type. The following JSON sample shows the schema of a single event row written to Azure Storage. Each row includes the event timestamp, your tenant identifier, the Advanced Hunting category, and the event data in JSON format:

```json
{
  "time": "<The time WDATP received the event>"
  "tenantId": "<Your tenant ID>"
  "category": "<The Advanced Hunting table name with 'AdvancedHunting-' prefix>"
  "properties": { <WDATP Advanced Hunting event as Json> }
}
```

Each blob contains multiple rows. Each row contains the event name, the time Defender for Business received the event, the organization to which the event belongs (you get events from your organization only), and the event in JSON format properties. For more information about the advanced hunting event data streamed to Azure Storage, see [Proactively hunt for threats with advanced hunting in Microsoft Defender](/en-us/defender-xdr/advanced-hunting-overview).