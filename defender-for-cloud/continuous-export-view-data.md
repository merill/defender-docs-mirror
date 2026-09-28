---
layout: Conceptual
title: View exported data in Azure Monitor - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/continuous-export-view-data
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
description: Learn how to view the data you exported with continuous export in Azure Monitor and analyze it effectively.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ms.custom: msecd-doc-authoring-1013
ai-usage: ai-assisted
locale: en-us
document_id: e488160f-9731-16f9-b4e0-fc3939dc671f
document_version_independent_id: c88522da-8c1a-4e94-2239-bb655c3ecf11
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/continuous-export-view-data.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/continuous-export-view-data
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/continuous-export-view-data.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/f0234678-3067-4edc-abf7-8142d54bb7d2
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/b0f4f6b9-28ed-4892-be4e-517310289c68
platformId: f7221f5d-e484-2f4a-5faf-764eec789c60
---

# View exported data in Azure Monitor - Microsoft Defender for Cloud | Microsoft Learn

This article explains how to view Microsoft Defender for Cloud data exported to Azure Monitor. It covers Log Analytics and Azure Event Hubs, and it explains how to create Azure Monitor alert rules based on exported data.

## Prerequisites

Before you begin, set up continuous export with one of these methods:

- [Set up continuous export in the Azure portal](continuous-export)
- [Set up continuous export with Azure Policy](continuous-export-azure-policy)
- [Set up continuous export with Representational State Transfer (REST) API](continuous-export-rest-api).

## View exported data in Log Analytics

When you export Defender for Cloud data to a Log Analytics workspace, two main tables are created automatically:

- `SecurityAlert`
- `SecurityRecommendation`

You can query these tables in Log Analytics to confirm that continuous export is working.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Search for and select **Log Analytics workspaces**.
3. Select **the workspace** that you configured as your continuous export target.
4. In the workspace menu, under **General**, select **Logs**.
5. In the query window, enter one of the following queries and select **Run**:

    ```kusto
    SecurityAlert
    ```

    or

    ```kusto
    SecurityRecommendation
    ```

## View exported data in Azure Event Hubs

When you export data to Azure Event Hubs, Defender for Cloud continuously streams alerts and recommendations as event messages. You can view these exported events in the Azure portal and analyze them further by connecting a downstream service.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Search for and select **Event Hubs namespaces**.
3. Select **the namespace and event hub** that you configured for continuous export.
4. In the event hub menu, select **Metrics** to view message activity, or **Process data** &gt; **Capture** to review event contents stored in your capture destination.
5. Optionally, use a connected tool such as [Microsoft Sentinel](/en-us/azure/sentinel/), a security information and event management (SIEM) solution, or a custom consumer app to read and process the exported events.

Note

Defender for Cloud sends data in JavaScript Object Notation (JSON) format. You can use Event Hubs Capture or consumer groups to store and analyze the exported events.

## Create alert rules in Azure Monitor (optional)

You can create Azure Monitor alerts based on your exported Defender for Cloud data. These alerts let you automatically trigger actions, such as sending email notifications or creating information technology service management (ITSM) tickets, when specific security events occur.

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Search for and select **Monitor**.
3. Select **Alerts**.
4. Select **+ Create** &gt; **Alert rule**.

    [![Azure Monitor Alerts page with the + Create menu open and Alert rule selected.](media/continuous-export-view-data/azure-monitor-alerts.png)](media/continuous-export-view-data/azure-monitor-alerts.png#lightbox)
5. Set up your new rule by following the Azure Monitor log alert rule process. For details, see [Configure log alert rules](/en-us/azure/azure-monitor/alerts/alerts-unified-log):

    - For **Resource types**, select the Log Analytics workspace to which you exported security alerts and recommendations.
    - For **Condition**, select **Custom log search**. In the **Custom log search** configuration pane, configure the query, lookback period, and frequency period. In the query, enter **SecurityAlert** or **SecurityRecommendation**.
    - Optionally, create action groups to trigger automated responses. For setup guidance, see [Azure Monitor action groups](/en-us/azure/azure-monitor/alerts/action-groups). Action groups can send email, create ITSM tickets, run webhooks, and more.

After you save the rule, Defender for Cloud alerts or recommendations appear in Azure Monitor based on your continuous export configuration and alert rule conditions. If you’ve linked an action group, it triggers automatically when the rule criteria are met.