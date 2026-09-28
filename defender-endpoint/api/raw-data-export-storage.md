---
layout: Conceptual
title: Stream Microsoft Defender for Endpoint events to your Storage account - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/api/raw-data-export-storage
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to configure Microsoft Defender for Endpoint to stream Advanced Hunting events to your Storage account.
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
document_id: d3857c42-0179-ea34-6f64-fb39d02beea3
document_version_independent_id: d3857c42-0179-ea34-6f64-fb39d02beea3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/api/raw-data-export-storage.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: api/raw-data-export-storage
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/api/raw-data-export-storage.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d774b87-7dcb-40bf-a0b9-5a7a9efff0d1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/89dc5f37-0e4e-4b05-ad87-5fcd2b941a8a
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 98a651a0-f657-dd57-1434-e1f384c64252
---

# Stream Microsoft Defender for Endpoint events to your Storage account - Microsoft Defender for Endpoint | Microsoft Learn

Note

For the full data streaming experience available, please visit [Stream Microsoft Defender XDR events | Microsoft Learn](/en-us/defender-xdr/streaming-api).

## Before you begin

1. Create a [Storage account](/en-us/azure/storage/common/storage-account-overview) in your tenant.
2. Sign in to your [Azure tenant](https://ms.portal.azure.com/), go to **Subscriptions** &gt; **Your subscription** &gt; **Resource Providers** &gt; **Register to Microsoft.insights**.

Important

Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

## Enable raw data streaming

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com).
2. Go to [Data export settings page](https://security.microsoft.com/settings/mtp_settings/raw_data_export) in Microsoft Defender XDR.
3. Select on **Add data export settings**.
4. Choose a name for your new settings.
5. Choose **Forward events to Azure Storage**.
6. Type your **Storage Account Resource ID**. In order to get your **Storage Account Resource ID**, go to your Storage account page on [Azure portal](https://ms.portal.azure.com/) &gt; properties tab &gt; copy the text under **Storage account resource ID**:

    [![The Event Hubs with resource ID1](../media/storage-account-resource-id.png)](../media/storage-account-resource-id.png#lightbox)
7. Choose the events you want to stream and select **Save**.

## The schema of the events in the Storage account

- A blob container is created for each event type:

    [![The Event Hubs with resource ID2](/en-us/defender-xdr/media/streaming-api-storage/storage-account-event-schema.png)](/en-us/defender-xdr/media/streaming-api-storage/storage-account-event-schema.png#lightbox)
- The schema of each row in a blob is the following JSON:

    ```json
    {
      "time": "<The time WDATP received the event>"
      "tenantId": "<Your tenant ID>"
      "category": "<The Advanced Hunting table name with 'AdvancedHunting-' prefix>"
      "properties": { <WDATP Advanced Hunting event as Json> }
    }
    ```
- Each blob contains multiple rows.
- Each row contains the event name, the time Defender for Endpoint received the event, the tenant it belongs (you get events only from your tenant), and the event in JSON format in a property called `properties`.
- For more information about the schema of Microsoft Defender for Endpoint events, see [Advanced Hunting overview](/en-us/defender-xdr/advanced-hunting-overview).
- In Advanced Hunting, the **DeviceInfo** table has a column named **MachineGroup** which contains the group of the device. Here, every event is decorated with this column as well. For more information, see [Device Groups](../machine-groups).

    Note

    Device group creation is supported in Defender for Endpoint Plan 1 and Plan 2.

## Data types mapping

In order to get the data types for our events properties, take the following steps:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com) and go to [Advanced Hunting page](https://security.microsoft.com/hunting-package).
2. Run the following query to get the data types mapping for each event:

    ```kusto
    {EventType}
    | getschema
    | project ColumnName, ColumnType
    ```

    Here's an example for Device Info event:

    [![The Event Hubs with resource ID3](../media/data-types-mapping-query.png)](../media/data-types-mapping-query.png#lightbox)