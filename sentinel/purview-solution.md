---
layout: Conceptual
title: Integrate Microsoft Sentinel and Microsoft Purview | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/purview-solution
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
description: This article describes how to use the Microsoft Sentinel data connector and solution for Microsoft Purview to enable data sensitivity insights, create rules to monitor when classifications have been detected, and get an overview about data found by Microsoft Purview, and where sensitive data resides in your organization.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: a1be8312-1884-8d31-1fc4-d622c90aa10a
document_version_independent_id: bad8c97e-97a6-a66e-cd18-89a7a3cd2864
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/purview-solution.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/purview-solution
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/purview-solution.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/57eae111-0f3b-497e-be07-450fd1409dea
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ac8bf8ab-8134-4c9a-9f2e-58b31575b492
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: e16e5d23-04d4-060c-c5cf-2cf5cc21bd12
---

# Integrate Microsoft Sentinel and Microsoft Purview | Microsoft Learn

[Microsoft Purview](/en-us/azure/purview/) provides organizations with visibility into where sensitive information is stored, helping prioritize at-risk data for protection. Integrate Microsoft Purview with Microsoft Sentinel to help narrow down the high volume of incidents and threats surfaced in Microsoft Sentinel, and understand the most critical areas to start.

Start by ingesting your Microsoft Purview logs into Microsoft Sentinel through a data connector. Then use a Microsoft Sentinel workbook to view data such as assets scanned, classifications found, and labels applied by Microsoft Purview. Use analytics rules to create alerts for changes within data sensitivity.

Customize the Microsoft Purview workbook and analytics rules to best suit the needs of your organization, and combine Microsoft Purview logs with data ingested from other sources to create enriched insights within Microsoft Sentinel.

## Prerequisites

Before you start, make sure you have both a [Microsoft Sentinel workspace](quickstart-onboard) and [Microsoft Purview](/en-us/azure/purview/create-catalog-portal) onboarded, and that your user has the following roles:

- **A Microsoft Purview account [Owner](/en-us/azure/role-based-access-control/built-in-roles) or [Contributor](/en-us/azure/role-based-access-control/built-in-roles) role**, to set up diagnostic settings and configure the data connector.
- **A [Microsoft Sentinel Contributor](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-contributor) role**, with write permissions to enable data connector, view the workbook, and create analytic rules.
- **The Microsoft Purview** solution installed in your Log Analytics workspace enabled for Microsoft Sentinel.

    The **Microsoft Purview** solution is a set of bundled content, including a data connector, workbook, and analytics rules configured specifically for Microsoft Purview data. For more information, see [About Microsoft Sentinel content and solutions](sentinel-solutions) and [Discover and manage Microsoft Sentinel out-of-the-box content](sentinel-solutions-deploy).

    Instructions for enabling your data connector are also available in Microsoft Sentinel, on the **Microsoft Purview** data connector page.

## Start ingesting Microsoft Purview data in Microsoft Sentinel

Configure diagnostic settings to have Microsoft Purview data sensitivity logs flow into Microsoft Sentinel, and then run a Microsoft Purview scan to start ingesting your data.

Diagnostics settings send log events only after a full scan is run, or when a change is detected during an incremental scan. It typically takes about 10-15 minutes for the logs to start appearing in Microsoft Sentinel.

**To enable data sensitivity logs to flow into Microsoft Sentinel**:

1. Navigate to your Microsoft Purview account in the Azure portal and select **Diagnostic settings**.

    ![Screenshot of a Microsoft Purview account Diagnostic settings page.](media/purview-solution/diagnostic-settings.png)
2. Select **+ Add diagnostic setting** and configure the new setting to send logs from Microsoft Purview to Microsoft Sentinel:

    - Enter a meaningful name for your setting.
    - Under **Logs**, select **DataSensitivityLogEvent**.
    - Under **Destination details**, select **Send to Log Analytics workspace**, and select the subscription and workspace details used for Microsoft Sentinel.
3. Select **Save**.

For more information, see [Connect Microsoft Sentinel to other Microsoft services by using diagnostic settings-based connections](connect-services-diagnostic-setting-based).

**To run a Microsoft Purview scan and view data in Microsoft Sentinel**:

1. In Microsoft Purview, run a full scan of your resources. For more information, see [Scan data sources in Microsoft Purview](/en-us/azure/purview/scan-data-sources).
2. After your Microsoft Purview scans have completed, go back to the Microsoft Purview data connector in Microsoft Sentinel and confirm that data has been received.

## View recent data discovered by Microsoft Purview

The Microsoft Purview solution provides two analytics rule templates out-of-the-box that you can enable, including a generic rule and a customized rule.

- The generic version, *Sensitive Data Discovered in the Last 24 Hours*, monitors for the detection of any classifications found across your data estate during a Microsoft Purview scan.
- The customized version, *Sensitive Data Discovered in the Last 24 Hours - Customized*, monitors and generates alerts each time the specified classification, such as Social Security Number, has been detected.

Use the procedure in Modify the Microsoft Purview analytics rule templates to customize the Microsoft Purview analytics rules' queries to detect assets with specific classification, sensitivity label, source region, and more. Combine the data generated with other data in Microsoft Sentinel to enrich your detections and alerts.

Note

Microsoft Sentinel analytics rules are KQL queries that trigger alerts when suspicious activity has been detected. Customize and group your rules together to create incidents for your SOC team to investigate.

### Modify the Microsoft Purview analytics rule templates

Use the following steps to create and customize a Microsoft Purview analytics rule from the built-in template.

1. In Microsoft Sentinel, open the **Microsoft Purview** solution, and then locate and select the **Sensitive Data Discovered in the Last 24 Hours - Customized** rule. On the side pane, select **Create rule** to create a new rule based on the template.
2. Go to the **Configuration** &gt; **Analytics** page and select **Active rules**. Search for a rule named **Sensitive Data Discovered in the Last 24 Hours - Customized**.

    By default, analytics rules created by Microsoft Sentinel solutions are set to disabled. Make sure to enable the rule for your workspace before continuing:

    1. Select the rule. In the side pane, select **Edit**.
    2. In the analytics rule wizard, at the bottom of the **General** tab, toggle the **Status** to **Enabled**.
3. On the **Set rule logic** tab, adjust the **Rule query** to query for the data fields and classifications you want to generate alerts for. For more information on what can be included in your query, see:

    - Supported data fields are the columns of the [PurviewDataSensitivityLogs](/en-us/azure/azure-monitor/reference/tables/purviewdatasensitivitylogs) table
    - [Supported classifications](/en-us/azure/purview/supported-classifications)

    Formatted queries have the following syntax: `| where {data-field} contains {specified-string}`.

    For example:

    ```Kusto
    PurviewDataSensitivityLogs
    | where Classification contains “Social Security Number”
    | where SourceRegion contains “westeurope”
    | where SourceType contains “Amazon”
    | where TimeGenerated > ago (24h)
    ```

    See more information on the following items used in the sample `PurviewDataSensitivityLogs` query, in the Kusto documentation:

    - [***where*** operator](/en-us/kusto/query/where-operator?view=microsoft-sentinel&amp;preserve-view=true)
    - [***ago()*** function](/en-us/kusto/query/ago-function?view=microsoft-sentinel&amp;preserve-view=true)

    For more information on KQL, see [Kusto Query Language (KQL) overview](/en-us/kusto/query/?view=microsoft-sentinel&amp;preserve-view=true).

    Other resources:

    - [KQL quick reference](/en-us/kusto/query/kql-quick-reference?view=microsoft-sentinel&amp;preserve-view=true)
    - [Kusto Query Language learning resources](/en-us/kusto/query/kql-learning-resources?view=microsoft-sentinel&amp;preserve-view=true)
4. Under **Query scheduling**, define settings so that the rules show data discovered in the last 24 hours. We also recommend that you set **Event grouping** to group all events into a single alert.

    ![Screenshot of the analytics rule wizard defined to show data detected in the last 24 hours.](media/purview-solution/analytics-rule-wizard.png)
5. If needed, customize the **Incident settings** and **Automated response** tabs. For example, in the **Incidents settings** tab, verify that **Create incidents from alerts triggered by this analytics rule** is selected.
6. On the **Review + create** tab, select **Save**.

For more information, see [Create custom analytics rules to detect threats](detect-threats-custom).

### View Microsoft Purview data in Microsoft Sentinel workbooks

Use the following steps to add the Microsoft Purview workbook to your workspace and open it.

1. In Microsoft Sentinel, open the **Microsoft Purview** solution, and then locate and select the **Microsoft Purview** workbook. On the side pane, select **Configuration** to add the workbook to your workspace.
2. In Microsoft Sentinel, under **Threat management**, select **Workbooks** &gt; **My workbooks**, and locate the **Microsoft Purview** workbook. Save the workbook to your workspace, and then select **View saved workbook**. For example:

    ![Screenshot of the Microsoft Purview workbook.](media/purview-solution/purview-workbook.png)

The Microsoft Purview workbook displays the following tabs:

- **Overview**: Displays the regions and resource types where the data is located.
- **Classifications**: Displays assets that contain specified classifications, like Credit Card Numbers.
- **Sensitivity labels**: Displays the assets that have confidential labels, and the assets that currently have no labels.

To drill down in the Microsoft Purview workbook:

- Select a specific data source to jump to that resource in Azure.
- Select an asset path link to show more details, with all the data fields shared in the ingested logs.
- Select a row in the **Data Source**, **Classification**, or **Sensitivity Label** tables to filter the Asset Level data as configured.

### Investigate incidents triggered by Microsoft Purview events

When investigating incidents triggered by the Microsoft Purview analytics rules, find detailed information on the assets and classifications found in the incident's **Events**.

For example:

![Screenshot of an incident triggered by Purview events.](media/purview-solution/purview-incident.png)