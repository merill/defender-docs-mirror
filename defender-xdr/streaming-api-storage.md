---
layout: Conceptual
title: Stream Microsoft Defender XDR events to your Storage account - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/streaming-api-storage
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to configure Microsoft Defender XDR to stream Advanced Hunting events to your Storage account.
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
document_id: 4f163d47-823d-2d92-69b0-75f5558bb7f3
document_version_independent_id: 4f163d47-823d-2d92-69b0-75f5558bb7f3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/streaming-api-storage.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: streaming-api-storage
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/streaming-api-storage.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d774b87-7dcb-40bf-a0b9-5a7a9efff0d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://authoring-docs-microsoft.poolparty.biz/devrel/5fc61396-d075-4560-aece-fdbda73d243f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/89dc5f37-0e4e-4b05-ad87-5fcd2b941a8a
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://authoring-docs-microsoft.poolparty.biz/devrel/ad9437c1-8cda-4537-ad69-b4b263652e13
platformId: 348a6b29-3b70-b343-b721-56467961b0e2
---

# Stream Microsoft Defender XDR events to your Storage account - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- [Microsoft Defender XDR](microsoft-365-defender)

Note

**Try our new APIs using MS Graph security API**. Find out more at: [Use the Microsoft Graph security API - Microsoft Graph | Microsoft Learn](/en-us/graph/api/resources/security-api-overview).

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Before you begin

Before you start, complete the following prerequisites:

- Create a [Storage account](/en-us/azure/storage/common/storage-account-overview) in your tenant.
- Sign in to the [Azure portal](https://ms.portal.azure.com/), and go to **Subscriptions** &gt; **Your subscription** &gt; **Resource Providers** &gt; **Register to Microsoft.Insights**.

### Add contributor permissions

After the storage account is created, assign the Contributor role to the user account that will configure the Streaming API settings.

1. Go to **Storage Account** &gt; **Access control (IAM)**, and then select **Add**.
2. Verify that the user account or service principal you assigned the Contributor role to is listed under **Role assignments**.

## Enable raw data streaming

Note

When using the Streaming API, ensure that the `Allow trusted Microsoft services to access this storage account` option is enabled in the target Azure Storage account settings to allow data to be streamed from Microsoft Defender for Endpoint.

1. Go to the [Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2077139) and sign in using an account with at least Security Administrator permissions.
2. Go to **Settings** &gt; **Microsoft Defender XDR** &gt; **Streaming API**. To go directly to the **Streaming API** page, use the [Streaming API settings page](https://security.microsoft.com/settings/mtp_settings/raw_data_export).
3. Select **Add**.
4. In the **Add new Streaming API settings** flyout that appears, configure the following settings:

    - **Name**: Choose a name for your new settings.
    - Select **Forward events to Azure Storage**.
5. To display the Azure Resource Manager resource ID for a storage account in the Azure portal, follow these steps:

    1. Navigate to your storage account in the [Azure portal](https://portal.azure.com).
    2. In the **Overview** page, in the **Essentials** section, select the **JSON View** link.
    3. The resource ID for the storage account is displayed at the top of the page. Copy the text under **Storage Account Resource ID**.
    4. In the **Add new Streaming API settings** flyout, choose the **Event types** that you want to stream.
    5. When you're finished, select **Submit**.

## Event schema in the storage account

Exported events are stored in blob containers, and each row follows a defined JSON schema.

- A blob container is created for each event type:

    [![Example of a blob container](media/streaming-api-storage/storage-account-event-schema.png)](media/streaming-api-storage/storage-account-event-schema.png#lightbox)
- The following JSON sample shows the structure of each row in a blob, so you can identify the fields and data types in a streamed event record:

    ```JSON
    {
            "time": "<The time Microsoft Defender XDR received the event>"
            "tenantId": "<Your tenant ID>"
            "category": "<The Advanced Hunting table name with 'AdvancedHunting-' prefix>"
            "properties": { <Microsoft Defender XDR Advanced Hunting event as Json> }
    }
    ```
- Each blob contains multiple rows.
- Each row contains the event name, the time Defender for Endpoint received the event, the tenant it belongs (you'll only get events from your tenant), and the event in JSON format in a property called "properties".
- For more information about the schema of Microsoft Defender events, see [Advanced Hunting overview](advanced-hunting-overview).

## Data type mappings

To get the data types for events properties, follow these steps:

1. Go to the [Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2077139) and sign in.
2. Go to **Hunting** &gt; **Advanced hunting**. To go directly to the **Advanced hunting** page, use the [Advanced hunting page](https://security.microsoft.com/advanced-hunting).
3. On the **Query** tab, run the following Kusto query to list the column names and data types for a specific event table. This information helps you map streamed event properties to their correct schema. Replace `{EventType}` with the Advanced Hunting table name you want to inspect (for example, `DeviceInfo`):

    ```kusto
    {EventType}
    | getschema
    | project ColumnName, ColumnType
    ```

    The following example shows the column names and data types returned for a DeviceInfo event, so you can map event properties to their schema:

    [![An example device info query](/en-us/defender-endpoint/media/machine-info-datatype-example.png)](/en-us/defender-endpoint/media/machine-info-datatype-example.png#lightbox)

## Monitoring created resources

You can monitor the Azure Storage export resources and related diagnostics by using **Azure Monitor**. For more information, see [Monitor destinations - Azure Monitor](/en-us/azure/azure-monitor/logs/logs-data-export?tabs=portal#monitor-destinations).