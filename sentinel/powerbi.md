---
layout: Conceptual
title: Create a Power BI report from Microsoft Sentinel data | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/powerbi
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
description: Learn how to create a Power BI report from Microsoft Sentinel data by exporting a KQL query, building visualizations in Power BI Desktop, publishing to the Power BI service, and sharing the report in a Teams channel.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 3947b92b-3f93-afe5-6932-f0e1993ce997
document_version_independent_id: 0fd44b57-e700-b0cf-b899-3131ee3f2473
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/powerbi.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/powerbi
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/powerbi.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/d3197845-b4ce-44c6-a237-cd4be160e76c
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/aea905fb-0a9d-4d46-b30f-e9cbaf772d1b
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 98dcf0d2-dd64-7b37-4d3a-1560eceda87d
---

# Create a Power BI report from Microsoft Sentinel data | Microsoft Learn

[Power BI](https://powerbi.microsoft.com/) is a reporting and analytics platform that turns data into coherent, immersive, interactive visualizations. Power BI lets you easily connect to data sources, visualize and discover relationships, and share insights with whoever you want.

You can base Power BI reports on data from Microsoft Sentinel and share those reports with people who don't have access to Microsoft Sentinel. For example, you might want to share information about failed sign-in attempts with app owners, without granting them Microsoft Sentinel access. Power BI visualizations can provide the data at a glance.

Microsoft Sentinel runs on Log Analytics workspaces, and you can use Kusto Query Language (KQL) to query the data.

This article provides a scenario-based procedure to view analysis reports in Power BI for your Microsoft Sentinel data. For background on connecting Microsoft Sentinel to data sources, see [Connect data sources](connect-data-sources). For general guidance on creating visualizations in Microsoft Sentinel, see [Visualize collected data](get-visibility).

In this article, you:

- Export a KQL query to a Power BI M language query.
- Use the M query in Power BI Desktop to create visualizations and a report.
- Publish the report to the Power BI service, and share it with others.
- Add the report to a Teams channel.

People you granted access in the Power BI service, and members of the Teams channel, can see the report without needing Microsoft Sentinel permissions.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Prerequisites

To complete the steps in this article, you need:

- At least read access to a Microsoft Sentinel workspace that monitors sign-in attempts.
- A Power BI account that has read access to your Microsoft Sentinel workspace.
- [Power BI Desktop installed from the Microsoft Store](https://aka.ms/pbidesktopstore).

## Export a query from Microsoft Sentinel

Create, run, and export a KQL query from Microsoft Sentinel.

1. To create a simple query, in Microsoft Sentinel, select **Logs**. If your workspace is onboarded to the Microsoft Defender portal, select **General &gt; Logs**.
2. In the query editor, under **New Query 1**, enter the following query to summarize sign-in attempts by application over the last seven days, including failed and successful counts. You can also use any other Microsoft Sentinel query for your data:

    ```kusto
    SigninLogs
    | where TimeGenerated >ago(7d)
    | summarize Attempts = count(), Failed=countif(ResultType !=0), Succeeded = countif(ResultType ==0) by AppDisplayName
    | top 10 by Failed
    | sort by Failed
    ```

    See more information about the operators and functions used in the sample `SigninLogs` query, in the Kusto documentation:

    - [***where*** operator](/en-us/kusto/query/where-operator?view=microsoft-sentinel&amp;preserve-view=true)
    - [***summarize*** operator](/en-us/kusto/query/summarize-operator?view=microsoft-sentinel&amp;preserve-view=true)
    - [***top*** operator](/en-us/kusto/query/top-operator?view=microsoft-sentinel&amp;preserve-view=true)
    - [***sort*** operator](/en-us/kusto/query/sort-operator?view=microsoft-sentinel&amp;preserve-view=true)
    - [***ago()*** function](/en-us/kusto/query/ago-function?view=microsoft-sentinel&amp;preserve-view=true)
    - [***count()*** aggregation function](/en-us/kusto/query/count-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true)
    - [***countif()*** aggregation function](/en-us/kusto/query/countif-aggregation-function?view=microsoft-sentinel&amp;preserve-view=true)

    For more information on KQL, see [Kusto Query Language (KQL) overview](/en-us/kusto/query/?view=microsoft-sentinel&amp;preserve-view=true).

    Other resources:

    - [KQL quick reference](/en-us/kusto/query/kql-quick-reference?view=microsoft-sentinel&amp;preserve-view=true)
    - [Kusto Query Language learning resources](/en-us/kusto/query/kql-learning-resources?view=microsoft-sentinel&amp;preserve-view=true)
3. Select **Run** to execute the query. The results show a summary of sign-in attempts by application over the last seven days, including failed and successful counts.

    ![Screenshot showing the KQL query and results.](media/powerbi/query.png)
4. To export the query to Power BI M query format, select **Export**, and then select **Export to Power BI (M query)**. The query is exported to a text file called *PowerBIQuery.txt*.

    ![Screenshot showing query Export to Power BI M format.](media/powerbi/export.png)
5. Copy the contents of the exported file.

## Get the data in Power BI Desktop

Run the exported M query in Power BI Desktop to get data.

1. Open Power BI Desktop, and sign in to your Power BI account that has read access to your Microsoft Sentinel workspace.

    ![Screenshot showing sign-in to Power BI Desktop.](media/powerbi/sign-in.png)
2. In the Power BI ribbon, select **Get data** and then select **Blank query**. The **Power Query Editor** opens.

    ![Screenshot showing Blank query selected under Get data in Power BI Desktop.](media/powerbi/blank-query.png)
3. In the **Power Query Editor**, select **Advanced Editor**.
4. Paste the copied contents of the exported *PowerBIQuery.txt* file into the **Advanced Editor** window, and then select **Done**.

    ![Screenshot showing the M query pasted in to the Power BI Advanced Editor.](media/powerbi/advanced-editor.png)
5. In the **Power Query Editor**, rename the query to *App\_signin\_stats*, and then select **Close & Apply**.

    ![Screenshot showing the renamed query and Close &amp; Apply command in the Power Query Editor.](media/powerbi/close-apply.png)

## Create visualizations from the data

Now that the imported Microsoft Sentinel query results are in Power BI, you can create visualizations to provide insights into the data.

### Create a table visual

First, create a table that shows all the results of the query.

1. To add a table visualization to the Power BI Desktop canvas, select the **table** icon under **Visualizations**.

    ![Screenshot showing the table icon under Visualizations in Power BI Desktop.](media/powerbi/table.png)
2. Under **Fields**, select all the fields in your query, so they all appear in the table. If the table doesn't show all the data, enlarge the table by dragging its selection handles.

    ![Screenshot showing all fields selected for the table visualization.](media/powerbi/select-fields.png)

### Create a pie chart

Next, create a pie chart that shows which applications had the most failed sign-in attempts.

1. Deselect the table visual by clicking or tapping outside of it, and then under **Visualizations**, select the **pie chart** icon.

    ![Screenshot showing the pie chart icon under Visualizations in Power BI Desktop.](media/powerbi/pie-chart.png)
2. Select **AppDisplayName** in the **Legend** well, or drag it from the **Fields** pane. Select **Failed** in the **Values** well, or drag it from **Fields**. The pie chart now shows the number of failed sign-in attempts per application.

    ![Screenshot showing the pie chart with number of failed sign-in attempts per application.](media/powerbi/failed.png)

### Create a new quick measure

You also want to show what percentage of sign-in attempts failed for each application. Since your query doesn't have a percentage column, you can create a new measure to show this information.

1. Under **Visualizations**, select the **stacked column chart** icon to create a stacked column chart.

    ![Screenshot showing the stacked column chart icon under Visualizations in Power BI Desktop.](media/powerbi/column-chart.png)
2. With the new visualization selected, select **Quick measure** in the ribbon.
3. In the **Quick measures** window, under **Calculation**, select **Division**. Drag **Failed** from **Fields** into the **Numerator** field, and drag **Attempts** from **Fields** to **Denominator**.

    ![Screenshot showing the settings in the Quick measures window.](media/powerbi/quick-measures.png)
4. Select **OK**. The new measure appears in the **Fields** pane.
5. Select the new measure in the **Fields** pane, and under **Formatting** in the ribbon, select **Percentage**.

    ![Screenshot showing the new measure selected in the Fields pane, and Percentage selected under Formatting in the ribbon.](media/powerbi/percentage.png)
6. With the column chart visualization selected on the canvas, select or drag the **AppDisplayName** field into the **Axis** well, and the new **Failed divided by Attempts** measure into the **Values** well. The chart now shows the percentage of failed sign-in attempts for each application.

    ![Screenshot showing the column chart with percentage of failed attempts for each application.](media/powerbi/failed-percentage.png)

### Refresh the data and save the report

Refresh the Power BI dataset created from the exported Microsoft Sentinel query to retrieve the latest data, and then save the report.

1. Select **Refresh** to get the latest data from Microsoft Sentinel.

    ![Screenshot showing the Refresh button in the ribbon.](media/powerbi/refresh.png)
2. Select **File** &gt; **Save** and save your Power BI report.

## Create a Power BI online workspace

To create a Power BI workspace for sharing the report:

1. Sign in to the [Power BI service](https://powerbi.com) with the same account you used for Power BI Desktop and Microsoft Sentinel read access.
2. Under **Workspaces**, select **Create a workspace**. Name the workspace *Management Reports*, and select **Save**.

    ![Screenshot showing Create a workspace in the Power BI service.](media/powerbi/create-workspace.png)
3. To grant people and groups access to the workspace, select the **More options** dots next to the new workspace name, and then select **Workspace access**.

    ![Screenshot showing Workspace access in the workspace More options menu.](media/powerbi/workspace-access.png)
4. In the **Workspace access** side pane, you can add users' email addresses and assign each user a role. The roles are Admin, Member, Contributor, and Viewer.

## Publish the Power BI report

Now you can use Power BI Desktop to publish your Power BI report so other people can see it.

1. In your new report in Power BI Desktop, select **Publish**.

    ![Screenshot showing Publish in the Power BI Desktop ribbon.](media/powerbi/publish.png)
2. Select the **Management Reports** workspace to publish to, and select **Select**.

    ![Screenshot that shows selecting the Power BI Management Reports workspace to publish to.](media/powerbi/select-workspace.png)

## Import the report to a Microsoft Teams channel

You also want members of the Management Teams channel to be able to see the published Power BI report. To add the report to a Teams channel:

1. In the Management Teams channel, select **+** to add a tab, and in the **Add a tab** window, search for and select **Power BI**.

    ![Screenshot that shows selecting Power BI in the Add a tab window in Teams.](media/powerbi/add-tab.png)
2. Select your new report from the list of Power BI reports, and select **Save**. The report appears in a new tab in the Teams channel.

    ![Screenshot showing the Power BI report in a tab in the Teams channel.](media/powerbi/teams.png)

## Schedule report refresh

Configure a scheduled refresh for the report's dataset in the Power BI service, so updated data always appears in the report. Before you begin, make sure you have credentials for an account with read access to the Log Analytics workspace.

In Power BI, scheduled refresh is configured on the dataset that backs your report. When you publish a report, Power BI automatically creates a corresponding dataset in the workspace.

1. In the Power BI service, select the workspace you published your report to.
2. Next to the report's dataset, select **More options** &gt; **Settings**.

    ![Screenshot showing Settings under More options in the Power BI report dataset.](media/powerbi/settings.png)
3. Select **Edit credentials** to provide the credentials for an account that has read access to the Log Analytics workspace.
4. Under **Scheduled refresh**, set the slider to **On**, and set up a refresh schedule for the report.

    ![Screenshot showing Scheduled refresh settings for the Power BI report dataset.](media/powerbi/schedule.png)