---
layout: Conceptual
title: Investigate apps discovered by Microsoft Defender for Endpoint - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/mde-investigation
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: Learn how to use Microsoft Defender for Cloud Apps to investigate Microsoft Defender for Endpoint discovered devices, network events, and app usage.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: Mravela
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: aee96322-3ff4-29a3-9552-b2dd98dec557
document_version_independent_id: aee96322-3ff4-29a3-9552-b2dd98dec557
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/mde-investigation.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mde-investigation
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/mde-investigation.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: dba39622-af0f-e8f2-9d3a-4de7d27bd603
---

# Investigate apps discovered by Microsoft Defender for Endpoint - Microsoft Defender for Cloud Apps | Microsoft Learn

The Microsoft Defender for Cloud Apps [integration with Microsoft Defender for Endpoint](mde-integration) provides a seamless Shadow IT visibility and control solution. Our integration enables Defender for Cloud Apps administrators to investigate discovered devices, network events, and app usage. Before you begin, make sure you meet the prerequisites, including configuring the Defender for Endpoint integration.

## Prerequisites

Before performing the procedures in this article, make sure that you've completed the [Defender for Endpoint and Defender for Cloud Apps integration](mde-integration).

## Investigate discovered devices in Defender for Cloud Apps

After you integrate Defender for Endpoint with Defender for Cloud Apps, investigate discovered device data in the cloud discovery dashboard.

1. In the Microsoft Defender portal, under **Cloud Apps**, select **Cloud Discovery** &gt; **Dashboard**.
2. At the top of the **Cloud Discovery Dashboard** page, select **Defender-managed endpoints**. The Defender-managed endpoints stream contains data from any operating systems mentioned in Defender for Cloud Apps [integration prerequisites](mde-integration#prerequisites).

At the top of the Cloud Discovery dashboard, you'll see the number of discovered devices added after the Defender for Endpoint and Defender for Cloud Apps integration was configured.

1. Select the **Devices** tab.
2. Drill down into each device that's listed, and use the tabs to view the investigation data. Find correlations between the devices, the users, IP addresses, and apps that were involved in incidents:

    - **Overview**:

        - **Device risk level**: Shows how risky the device's profile is relative to other devices in your organization, as indicated by the severity (high, medium, low, informational). Defender for Cloud Apps uses device profiles from Defender for Endpoint for each device based on advanced analytics. Activity that is anomalous to a device's baseline is evaluated and determines the device's risk level. Use the device risk level to determine which devices to investigate first.
        - **Transactions**: Information about the number of transactions that took place on the device over the selected period of time.
        - **Total traffic**: Information about the total amount of traffic (in MB) over the selected period of time.
        - Uploads: Information about the total amount of traffic (in MB) uploaded by the device over the selected period of time.
        - **Downloads**: Information about the total amount of traffic (in MB) downloaded by the device over the selected period of time.
    - **Discovered apps**: Lists all the discovered apps that were accessed by the device.
    - **User history**: Lists all the users who signed in to the device.
    - **IP address history**: Lists all the IP addresses that were assigned to the device.

As with any other cloud discovery source, you can export the data from the **Defender-managed endpoints** report for further investigation.

Note

- Defender for Endpoint forwards data to Defender for Cloud Apps in chunks of ~4 MB (~4000 endpoint transactions)
- If the 4 MB limit isn't reached within 1 hour, Defender for Endpoint reports all the transactions performed over the last hour.

### Discover apps via Defender for Endpoint when the endpoint is behind a network proxy

Defender for Cloud Apps can discover Shadow IT network events detected from Defender for Endpoint devices that are working in the same environment as a network proxy. For example, if your Windows 10 endpoint device is in the same environment as ZScalar, Defender for Cloud Apps can discover Shadow IT applications via the **Win10 Endpoint Users** stream.

## Investigate device network events in Microsoft Defender

Network events are timeline records of device connections captured by Defender for Endpoint that help you investigate app-related activity on specific devices.

Note

Network events should be used to investigate discovered apps and not used to debug missing data.

Use the following steps to gain more granular visibility on device's network activity in Microsoft Defender for Endpoint:

1. In the Microsoft Defender Portal, under **Cloud Apps**, select **Cloud Discovery**. Then select the **Devices** tab.
2. Select the machine you want to investigate and then in the top-left select **View in Microsoft Defender for Endpoint**.
3. In the Defender portal, under **Assets** -&gt; **Devices** &gt; {selected device}, select **Timeline**.
4. Under **Filters**, select **Network events**.
5. Investigate the device's network events as required.

![Screenshot of the Microsoft Defender XDR device timeline filtered to show network events for the selected device.](media/mde-selected-device.png)

## Investigate app usage in Microsoft Defender XDR with advanced hunting

[Advanced hunting](/en-us/defender-xdr/advanced-hunting-overview) is a query-based threat hunting tool in Microsoft Defender XDR that lets you explore raw telemetry data. Use the following steps to gain more granular visibility on app-related network events in Defender for Endpoint:

1. In the Microsoft Defender Portal, under **Cloud Apps**, select **Cloud Discovery**. Then select the **Discovered apps** tab.
2. Select the app you want to investigate to open its drawer.
3. Select the app's **Domain** list and then copy the list of domains.
4. In Microsoft Defender XDR, under **Hunting**, select **Advanced hunting**.
5. Paste the following query and replace `<DOMAIN_LIST>` with the list of domains you copied earlier.

    ```kusto
    DeviceNetworkEvents
    | where RemoteUrl has_any ("<DOMAIN_LIST>")
    | order by Timestamp desc
    ```
6. Run the query and investigate network events for this app.

    ![Screenshot of Advanced hunting query results in Microsoft Defender XDR showing network events for the investigated app domains.](media/mde-advanced-hunting.png)

## Investigate unsanctioned apps in Microsoft Defender

Every attempt to access an unsanctioned app triggers an alert in the Defender portal with in-depth details about the entire session. The alert details enable you to perform deeper investigations into attempts to access unsanctioned apps, as well as providing additional relevant information for use in endpoint device investigation.

Sometimes, access to an unsanctioned app isn't blocked, either because the endpoint device isn't configured correctly or if the enforcement policy hasn't yet propagated to the endpoint. When access to an unsanctioned app isn't blocked because of endpoint misconfiguration or policy propagation delays, Defender for Endpoint administrators receive an alert in the Defender portal that the unsanctioned app wasn't blocked.

![Screenshot of a Microsoft Defender XDR alert indicating that access to an unsanctioned app was detected but not blocked on an endpoint device.](media/mde-unsanctioned-app-alert.png)

Note

- It takes up to two hours after you tag an app as **Unsanctioned** for app domains to propagate to endpoint devices.
- By default, apps and domains marked as **Unsanctioned** in Defender for Cloud Apps, will be blocked for all endpoint devices in the organization.
- Currently, full URLs are not supported for unsanctioned apps. Therefore, when unsanctioning apps configured with full URLs, they are not propagated to Defender for Endpoint and will not be blocked. For example, `google.com/drive` is not supported, while `drive.google.com` is supported.
- In-browser notifications may vary between different browsers.