---
layout: Conceptual
title: Turn on auditing and health monitoring in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/enable-monitoring
breadcrumb_path: breadcrumb/toc.json
feedback_help_link_url: https://learn.microsoft.com/answers/tags/423/microsoft-sentinel/
feedback_help_link_type: get-help-at-qna
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
manager: orspodek
ms.service: microsoft-sentinel
ms.subservice: sentinel-siem
search.appverid: met150
description: Turn on auditing and health monitoring in Microsoft Sentinel to collect resource health and audit data in the SentinelHealth and SentinelAudit tables for monitoring, alerting, and investigation.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: ae3854ed-616a-3cf4-f140-afb3328dbdd6
document_version_independent_id: a3eb6699-ea17-91b0-c9a5-54e2037b53f9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/enable-monitoring.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/enable-monitoring
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/enable-monitoring.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: f6449cec-9cb3-cc0c-7b5d-5b550aa07f09
---

# Turn on auditing and health monitoring in Microsoft Sentinel | Microsoft Learn

Monitor the health of supported Microsoft Sentinel resources and audit their integrity. Turn on auditing and health monitoring in Microsoft Sentinel's **Settings** page. Get insights on health drifts, such as the latest failure events or changes from success to failure states. Track unauthorized actions, and use audit and health data to create notifications and other automated actions.

The [*SentinelHealth*](health-table-reference) data table stores health data. The [*SentinelAudit*](audit-table-reference) data table stores audit information. To use these tables, first turn on auditing and health monitoring for your workspace. This article shows you how.

To implement the health and audit feature using API (Bicep/AZURE RESOURCE MANAGER (ARM)/REST), review the [Diagnostic Settings operations](/en-us/rest/api/monitor/diagnostic-settings). To configure the retention time for your audit and health events, see [Manage data retention in a Log Analytics workspace](/en-us/azure/azure-monitor/logs/data-retention-configure).

## Prerequisites

- Before you start, learn more about health monitoring and auditing in Microsoft Sentinel. For more information, see [Auditing and health monitoring in Microsoft Sentinel](health-audit).

## Turn on auditing and health monitoring for your workspace

To get started, enable auditing and health monitoring from the Microsoft Sentinel settings.

1. For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), under **Configuration**, select **Settings** &gt; **Settings**. For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), under **System**, select **Settings** &gt; **Microsoft Sentinel**.
2. Select **Auditing and health monitoring**.
3. Select **Enable** to enable auditing and health monitoring across all resource types and to send the auditing and monitoring data to your Microsoft Sentinel workspace (and nowhere else).

    Or, select the **Configure diagnostic settings** link to enable health monitoring only for the data collector and/or automation resources, or to configure advanced options, like more places to send the data.

# [Defender portal](#tab/defender-portal)
![Screenshot shows how to get to the health monitoring settings in the Defender portal.](media/enable-monitoring/enable-health-monitoring-defender.png)

# [Azure portal](#tab/azure-portal)
![Screenshot shows how to get to the health monitoring settings.](media/enable-monitoring/enable-health-monitoring.png)

---

    If you selected **Enable**, the button grays out and shows **Enabling...**, then **Enabled**. Auditing and health monitoring is now turned on. The system adds the right diagnostic settings for you. To view or edit them, select the **Configure diagnostic settings** link.
4. If you selected **Configure diagnostic settings**, then in the **Diagnostic settings** screen, select **+ Add diagnostic setting**.

    (If you're editing an existing setting, select it from the list of diagnostic settings.)

    - In the **Diagnostic setting name** field, enter a meaningful name for your setting.
    - In the **Logs** column, select the appropriate **Categories** for the resource types you want to monitor, for example **Data Collection - Connectors**. Select **allLogs** if you want to monitor analytics rules.
    - Under **Destination details**, select **Send to Log Analytics workspace**, and select your **Subscription** and **Log Analytics workspace** from the dropdown menus.

        ![Screenshot of diagnostic settings screen for enabling auditing and health monitoring.](media/enable-monitoring/diagnostic-settings.png)

        If you require, you might select other destinations to which to send your data, in addition to the Log Analytics workspace.
5. Select **Save** on the top banner to save your new setting.

The *SentinelHealth* and *SentinelAudit* data tables are created at the first event generated for the selected resources.

## Verify that the tables are receiving data

Run Kusto Query Language (KQL) queries in the Azure portal or the Defender portal to make sure you're getting health and auditing data.

1. For Microsoft Sentinel in the [Azure portal](https://portal.azure.com), under **General**, select **Logs**. For Microsoft Sentinel in the [Defender portal](https://security.microsoft.com/), under **Investigation & response**, select **Hunting** &gt; **Advanced hunting**.
2. Run a query on the *SentinelHealth* table to retrieve recent health records and confirm that data is flowing. For example:

    ```kusto
    _SentinelHealth()
     | take 20
    ```
3. Run a query on the *SentinelAudit* table to retrieve recent audit events, such as changes to analytics rules. For example:

    ```kusto
    _SentinelAudit()
     | take 20
    ```

## Supported data tables and resource types

After you turn on the feature, the [*SentinelHealth*](health-table-reference) and [*SentinelAudit*](audit-table-reference) data tables are created. The tables appear when the first event occurs for the selected resources.

Health monitoring supports these resource types:

- Analytics rules
- Data connectors
- Automation rules
- Playbooks (Azure Logic Apps workflows)

Note

When monitoring playbook health, make sure to collect Azure Logic Apps diagnostic events from your playbooks to get the full picture of your playbook activity. For more information, see [Monitor the health of your automation rules and playbooks](monitor-automation-health).

Only the analytics rule resource type is currently supported for auditing.