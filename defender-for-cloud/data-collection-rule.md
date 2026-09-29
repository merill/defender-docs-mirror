---
layout: Conceptual
title: Use a Custom Data Collection Rule for Defender for Servers Ingestion - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/data-collection-rule
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Learn how to use Data Collection Rules (DCRs) to customize how Defender for Servers security events are collected and ingested.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: d106f630-1825-c0b6-c4ed-b56d5ceab6aa
document_version_independent_id: 5870d2f8-3810-0ff7-9b78-4a463ef1f866
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/data-collection-rule.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/data-collection-rule
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/data-collection-rule.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/691e3042-55ad-4ce1-b5e9-649b1cc47b5c
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b7d11190-096c-4ddb-87db-63764f603aac
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 8e4de81a-2f65-5ba9-ff26-927f4615e66d
---

# Use a Custom Data Collection Rule for Defender for Servers Ingestion - Microsoft Defender for Cloud | Microsoft Learn

You can use a custom Data Collection Rule (DCR) to control which Windows Security events are sent to Log Analytics for Defender for Servers. This approach can help reduce ingestion volume by filtering out events you don't need.

With a custom DCR, you can:

- Filter high-volume security events
- Collect a specific subset of Windows Security events
- Apply transformations before ingestion

## Prerequisites

Before you create a custom DCR, ensure that you have:

- Azure Monitor Agent (AMA) installed on the machines that send data to Log Analytics.
- A Log Analytics workspace in the same region as the DCR.

## Create a DCR

To create a custom DCR in the Azure portal, follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Go to **Monitor** &gt; **Settings** &gt; **Data Collection Rules**, and then select **+ Create**.
3. Enter a name and a subscription.
4. Choose or create a resource group.
5. Select the region. The region must match the region of the Log Analytics workspaces you send to.
6. Under **Platform type**, select **Windows** to collect Windows Security events for the `SecurityEvent` ingestion benefit.
7. Choose **Linux** or **All** if you also need those logs.
8. Under **Data Collection Endpoint**, leave **&lt;none&gt;** unless you're using a Data Collection Endpoint for Private Link or another advanced network setup.
9. Select **Next : Resources &gt;**.
10. Select **+ Add resources** and choose the relevant resources.
11. If your environment requires a Data Collection Endpoint, for example, when using Private Link, select **+ Create endpoint**. Create the endpoint in the same region as the DCR.
12. Select **Next : Collect and deliver &gt;**.
13. Select **+ Add data source**.
14. For **Data source type**, select **Windows Event Logs** and choose **Basic** or **Custom**:

    - **Basic:**

        - Under **Security**, select **Audit success** or **Audit failure** to send Windows Security events to the `SecurityEvent` table.
        - If needed, select **Application** or **System** event logs to collect more events. These events go to the `Event` table and are billed as regular ingestion. The Defender for Servers ingestion benefit doesn't cover them.
    - **Custom**:

        - Under **Use XPath queries to filter event logs and limit data collection**, enter an XPath query. For example, `Security!*[System[(EventID=4624 or EventID=4625 or EventID=4688)]]`

    ![Screenshot of the Add data source window in the Create Data Collection Rule wizard showing Windows Event Logs selected with Basic/Custom options.](media/data-ingestion-benefit/add-data-source-window.png)
15. Select **Add**.
16. Select **Next : Destination &gt;**.
17. Select **+ Add destination**.

    [![Screenshot of the Add data source pane showing the Destination tab, where you click + Add destination.](media/data-ingestion-benefit/add-data-source-destination-tab.png)](media/data-ingestion-benefit/add-data-source-destination-tab.png#lightbox)
18. For **Destination type**, choose **Azure Monitor Logs**.
19. Select at least one Log Analytics workspace in the same region as the DCR.
20. Select **Save**.
21. Select **Next : Tags &gt;** and add any tags you need for resource organization or cost management.
22. Select **Next : Review + create &gt;**.
23. Select **Create** to deploy the DCR.

## Verify data ingestion

After you deploy the DCR, wait a few minutes for data to start flowing.

Run the following KQL query in the Log Analytics workspace:

```kusto
SecurityEvent
| take 10
```

## Sample JSON fragment

The following example shows a DCR configuration that collects selected Windows Security events:

```json
{
  "dataSources": {
    "windowsEventLogs": [
      {
        "name": "SecurityEvents",
        "streams": ["Microsoft-SecurityEvent"],
        "xPathQueries": [
          "Security!*[System[(EventID=4624 or EventID=4625 or EventID=4688)]]"
        ]
      }
    ]
  },
  "destinations": {
    "logAnalytics": [
      { "workspaceId": "<workspace-id>" }
    ]
  }
}
```

## Deploy using Azure Policy

If you manage many subscriptions, use Azure Policy to create and assign DCRs at scale. The [Deploy AMA DCR for Security Events collection](https://github.com/Azure/Microsoft-Defender-for-Cloud/tree/main/Policy/Deploy%20AMA%20DCR%20for%20Security%20Events%20collection) policy initiative applies security event collection rules for your environment.