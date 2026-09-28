---
layout: Conceptual
title: Configure Azure Event Hubs for Microsoft Defender XDR event ingestion - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/configure-event-hub
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Configure Azure Event Hubs to ingest streaming events from Microsoft Defender XDR for downstream integration and analysis.
ms.service: defender-xdr
ms.author: edbaynash
author: EdB-MSFT
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.custom: admindeeplinkDEFENDER, msecd-doc-authoring-1016
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 5894d0c1-592b-4fca-0e19-7813ab52c869
document_version_independent_id: 5894d0c1-592b-4fca-0e19-7813ab52c869
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/configure-event-hub.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-event-hub
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/configure-event-hub.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f0234678-3067-4edc-abf7-8142d54bb7d2
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/b0f4f6b9-28ed-4892-be4e-517310289c68
platformId: 36a9130d-848b-216a-3af1-31f3fb1bf21e
---

# Configure Azure Event Hubs for Microsoft Defender XDR event ingestion - Microsoft Defender XDR | Microsoft Learn

Note

**Try our new APIs using MS Graph security API**. Find out more at: [Use the Microsoft Graph security API - Microsoft Graph | Microsoft Learn](/en-us/graph/api/resources/security-api-overview).

Learn how to configure Azure Event Hubs so that your event hub namespace can ingest events from Microsoft Defender XDR. This article walks you through registering the required resource provider, creating a Microsoft Entra app registration, setting up an Event Hubs namespace with the correct permissions, and configuring Microsoft Defender XDR to stream event data to your event hubs.

## Set up the required Resource Provider in the Event Hubs subscription

Register the resource provider in your Azure subscription for Event Hubs.

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Select **Subscriptions** &gt; **{ Select the subscription the event hubs will be deployed to }** &gt; **Resource providers**.
3. Check that **Microsoft.Insights** is registered. If not, register it.

[![The list of service providers page in the Microsoft Azure portal](media/configure-event-hub/f893db7a7b1f7aa520e8b9257cc72562.png)](media/configure-event-hub/f893db7a7b1f7aa520e8b9257cc72562.png#lightbox)

## Set up Microsoft Entra App Registration

A service principal is the identity your app uses to access Azure resources. When you create an app registration, Azure automatically creates a service principal for it.

Note

You need the Administrator role, or Microsoft Entra ID must allow non-admins to register apps. You also need an Owner or User Access Administrator role to assign a role to the service principal. For more information, see [Create a Microsoft Entra app & service principal in the portal - Microsoft identity platform](/en-us/azure/active-directory/develop/howto-create-service-principal-portal).

1. Create a new registration in **Microsoft Entra ID** &gt; **App registrations** &gt; **New registration.** This step also creates a service principal.
2. Fill out the form with just the Name. No Redirect URI is required.

    [![The application name display section in the Microsoft Azure portal](media/configure-event-hub/336bc84e6be23900c43232b4ef0c253c.png)](media/configure-event-hub/336bc84e6be23900c43232b4ef0c253c.png#lightbox)

    [![The Overview information section in the Microsoft Azure portal](media/configure-event-hub/06ac04c4ff713c2065cec2ef2f99a294.png)](media/configure-event-hub/06ac04c4ff713c2065cec2ef2f99a294.png#lightbox)
3. Create a secret by clicking on **Certificates & secrets** &gt; **New client secret**:

    Warning

    **You can view this client secret only once. Copy and save it before leaving this page.**

    [![The Client secret section in the Microsoft Azure portal](media/configure-event-hub/d2ef88d3d2310d2c60c294b569cdf02e.png)](media/configure-event-hub/d2ef88d3d2310d2c60c294b569cdf02e.png#lightbox)

Microsoft Graph APIs use this client secret to authenticate your app registration.

## Set up Event Hubs namespace

Create an Event Hubs namespace and capture its Resource ID for use in the Microsoft Defender XDR export configuration.

1. Create an Event Hubs Namespace:

    Go to **Event Hub &gt; Add**. Select the pricing tier, throughput units, and Auto-Inflate settings for your expected load. Auto-Inflate requires standard pricing. For more information, see [Pricing - Event Hubs | Microsoft Azure](https://azure.microsoft.com/pricing/details/event-hubs/).

    Note

    You can use an existing event hub. However, throughput and scaling apply at the namespace level. Microsoft recommends placing each event hub in its own namespace.

    [![The event hubs section in the Microsoft Azure portal](media/configure-event-hub/ebc4ca37c342ad1da75c4aee4018e51a.png)](media/configure-event-hub/ebc4ca37c342ad1da75c4aee4018e51a.png#lightbox)
2. Get the Resource ID for this namespace. Go to your Event Hubs namespace page &gt; Properties. Copy the **Resource ID** value and save it for the Microsoft 365 configuration.

    [![The event hubs properties section in the Microsoft Azure portal](media/configure-event-hub/759498162a4e93cbf17c4130d704d164.png)](media/configure-event-hub/759498162a4e93cbf17c4130d704d164.png#lightbox)

### Add role assignments for Event Hubs namespace access

You're required to add permissions to the following roles to entities that are involved in Event Hubs data management:

- **Contributor**: The permissions related to this role are added to entity who logs in to the Microsoft Defender portal.
- **Reader** and **Azure Event Hub data Receiver**: The permissions related to these roles are assigned to the entity who is already assigned the role of a **Service Principal** and logs in to the Microsoft Entra application.

To ensure that these roles are added, perform the following step:

Go to **Event Hub Namespace** &gt; **Access Control (IAM)** &gt; **Add** and verify under **Role assignments**.

[![An application registration service principal section in the Microsoft Azure portal](media/configure-event-hub/9c9c29137b90d5858920202d87680d16.png)](media/configure-event-hub/9c9c29137b90d5858920202d87680d16.png#lightbox)

## Set up Event Hubs

You can send all selected event types to a single event hub or create a separate event hub for each event type. Choose the option that fits your needs.

**Option 1:**

You can create Event Hubs within your Namespace and **all** the Event Types (Tables) you select to export are written into this **one** Event Hub.

**Option 2:**

Instead of exporting all the Event Types (Tables) into one Event Hub, you can export each table into different Event Hubs inside your Event Hubs Namespace (one Event Hub per Event Type).

In this option, Microsoft Defender creates Event Hubs for you.

Note

If you are using an Event Hub Namespace that is **not** part of an Event Hub Cluster, you're only able to choose up to 10 Event Types (Tables) to export in each Export Settings you define, due to an Azure limitation of 10 Event Hub per Event Hub Namespace.

For example:

[![An event hubs section in the Microsoft Azure portal](media/configure-event-hub/005c1f6c10c34420d387f594987f9ffe.png)](media/configure-event-hub/005c1f6c10c34420d387f594987f9ffe.png#lightbox)

If you choose Option 2, don't manually create event hubs. Instead, skip to Configure Microsoft Defender XDR to export email tables to Event Hubs to set up the export in the Defender portal. Microsoft Defender XDR creates the event hubs for you.

To create event hubs in your namespace, select **Event Hub** &gt; **+ Event Hub**.

A higher partition count allows more throughput. Increase this value based on your expected load. Use the default values for Message Retention (1) and Capture (Off).

[![An event hubs creation section in the Microsoft Azure portal](media/configure-event-hub/1db04b8ec02a6298d7cc70419ac6e6a9.png)](media/configure-event-hub/1db04b8ec02a6298d7cc70419ac6e6a9.png#lightbox)

For these Event Hubs (not namespace), you need to configure a Shared Access Policy with Send, Listen Claims. Click on your **Event Hub** &gt; **Shared access policies** &gt; **+ Add** and then give it a Policy name (not used elsewhere) and check **Send** and **Listen**.

[![The Shared access policies page in the Microsoft Azure portal](media/configure-event-hub/1867d13f46dc6a0f4cdae6cf00df24db.png)](media/configure-event-hub/1867d13f46dc6a0f4cdae6cf00df24db.png#lightbox)

## Configure Microsoft Defender XDR to export email tables to Event Hubs

After your Event Hubs namespace and event hubs are set up, configure Microsoft Defender XDR to export event data through Event Hubs.

### Set up Microsoft Defender XDR to send email tables to Splunk through Event Hubs

Use the following steps to configure Microsoft Defender XDR to export email tables to Splunk through Event Hubs.

Before you begin, make sure your account has the following roles:

- **Contributor** role (or higher) at the Event Hubs *Namespace* resource level for the event hubs you're exporting to. Without this role, an error occurs when you try to save the export settings.
- **Security Admin** role on the tenant tied to Microsoft Defender XDR and Azure.

1. Sign in to [Microsoft Defender XDR](https://go.microsoft.com/fwlink/p/?linkid=2077139).

    [![The Settings page of the Microsoft Defender portal](media/configure-event-hub/55d5b1c21dd58692fb12a6c1c35bd4fa.png)](media/configure-event-hub/55d5b1c21dd58692fb12a6c1c35bd4fa.png#lightbox)
2. Click on **Raw Data Export &gt; +Add**.

    Use the Event Hubs namespace Resource ID you recorded in Set up Event Hubs namespace, the event hub name, and the client secret from Set up Microsoft Entra App Registration.

    **Name**: This value is local and should be whatever works in your environment.

    **Forward events to event hub**: Select this checkbox.

    **Event-Hub Resource ID**: Enter the Event Hubs namespace Resource ID you recorded in Set up Event Hubs namespace.

    **Event-Hub name**: If you created an event hub in your namespace during Set up Event Hubs, paste that event hub name here.

    If you choose to let Microsoft Defender XDR create Event Hubs per Event Types (Tables) for you, leave the **Event-Hub name** field empty.

    **Event Types**: Select the Advanced Hunting tables that you want to forward to the Event Hubs and then on to your custom app. Alert tables are from Microsoft Defender XDR, Devices tables are from Microsoft Defender for Endpoint (EDR), and Email tables are from Microsoft Defender for Office 365. Email Events records all Email Transactions. The URL (Safe Links), Attachment (Safe Attachments), and Post Delivery Events (ZAP) are also recorded and can be joined to the Email Events on the NetworkMessageId field.

    [![The Streaming API settings page in the Microsoft Azure portal](media/configure-event-hub/3b2ad64b6ef0f88cf0175f8d57ef8b97.png)](media/configure-event-hub/3b2ad64b6ef0f88cf0175f8d57ef8b97.png#lightbox)
3. Make sure to click **Submit**.

### Verify event export to Event Hubs

You can verify that events are being sent to the Event Hubs by running a basic Advanced Hunting query. The query uses the `EmailEvents`, `EmailAttachmentInfo`, `EmailUrlInfo`, and `EmailPostDeliveryEvents` Advanced Hunting tables to confirm that email-related data is flowing through the export pipeline. Select **Hunting** &gt; **Advanced Hunting** &gt; **Query** and enter the following query. This query uses full outer joins to correlate email events with attachment, URL, and post-delivery details by `NetworkMessageId`, giving you a count of all email activity in the last hour:

```console
EmailEvents
|join kind=fullouter EmailAttachmentInfo on NetworkMessageId
|join kind=fullouter EmailUrlInfo on NetworkMessageId
|join kind=fullouter EmailPostDeliveryEvents on NetworkMessageId
|where Timestamp > ago(1h)
|count
```

This query shows you how many emails were received in the last hour joined across all the other tables. The query result also shows whether events are available that could be exported to the Event Hubs. If this count shows 0, then you won't see any data going out to the Event Hubs.

[![The advanced hunting page in the Microsoft Azure portal](media/configure-event-hub/c305e57dc6f72fa9eb035943f244738e.png)](media/configure-event-hub/c305e57dc6f72fa9eb035943f244738e.png#lightbox)

Once you've verified there's data to export, you can view the Event Hubs page to verify that messages are incoming. Exported messages can take up to one hour to appear in Event Hubs.

1. In Azure, go to **Event Hub** &gt; Click on the **Namespace** &gt; **Event Hub** &gt; Click on the **Event Hub**.
2. Under **Overview**, scroll down and in the Messages graph you should see Incoming Messages. If you don't see any results, then there are no messages for your custom app to ingest.

[![ The Overview page in the Microsoft 365 Azure portal](media/configure-event-hub/e88060e315d76e74269a3fc866df047f.png)](media/configure-event-hub/e88060e315d76e74269a3fc866df047f.png#lightbox)