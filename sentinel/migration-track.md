---
layout: Conceptual
title: Track your Microsoft Sentinel Migration with a Workbook | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/migration-track
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
description: Learn how to track your migration with a workbook, how to customize and manage the workbook, and how to use the workbook tabs for useful Microsoft Sentinel actions.
author: EdB-MSFT
ms.author: edbaynash
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: usx-security
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 0561df23-fcfc-1625-3391-ef0855b9921b
document_version_independent_id: 8650ad5f-a866-0240-42a8-6f2d0752ff16
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/migration-track.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/migration-track
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/migration-track.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 8aacb313-31db-b11e-6d9e-c51f94d2c2d7
---

# Track your Microsoft Sentinel Migration with a Workbook | Microsoft Learn

As your organization's security operations center (SOC) handles growing amounts of data, it's essential to plan and monitor your deployment status. While you can track your migration process using generic tools such as Microsoft Project, Microsoft Excel, Microsoft Teams, or Azure DevOps, these tools aren’t specific to security information and event management (SIEM) migration tracking. To help you to track, we provide a dedicated workbook in Microsoft Sentinel named **Microsoft Sentinel Deployment and Migration**.

The workbook helps you to:

- Visualize migration progress
- Deploy and track data sources
- Deploy and monitor analytics rules and incidents
- Deploy and utilize workbooks
- Deploy and perform automation
- Deploy and customize user and entity behavioral analytics (UEBA)

This article describes how to track your migration with the **Microsoft Sentinel Deployment and Migration** workbook, how to customize and manage the workbook, and how to use the workbook tabs to deploy and monitor data connectors, analytics, incidents, playbooks, automation rules, UEBA, and data management. Learn more about how to use [Azure Monitor workbooks](monitor-your-data) in Microsoft Sentinel.

## Deploy the workbook content and view the workbook

To get the workbook, first install the standalone item from the **Content hub** in Microsoft Sentinel.

1. In the Microsoft Sentinel **Content hub**, filter the content listed by **Content type** = **Workbooks**, and then enter *migration* in the search bar.
2. From the search results, select the **Microsoft Sentinel Deployment and Migration** workbook, then select **Install**. Microsoft Sentinel deploys the workbook and saves the workbook in your environment.
3. In Microsoft Sentinel, under **Threat management**, select **Workbooks** &gt; **Templates**.
4. Select the **Microsoft Sentinel Deployment and Migration** workbook and **View template**.

## Deploy the watchlist

The **DeploymentandMigration** watchlist stores the deployment and migration actions that the workbook uses to track your progress. Deploy this watchlist from the Microsoft Sentinel GitHub repository.

1. In the [Microsoft Sentinel GitHub repository](https://github.com/Azure/Azure-Sentinel/tree/master/Watchlists), select the **DeploymentandMigration** folder, and select **Deploy to Azure** to begin the template deployment in Azure.
2. Provide the Microsoft Sentinel resource group and workspace name. ![Screenshot of deploying the watchlist to Azure.](media/migration-track/migration-track-azure-deployment.png)
3. Select **Review and create**.
4. After the information is validated, select **Create**.

## Update the watchlist with deployment and migration actions

Updating the watchlist with deployment and migration actions is crucial to the tracking setup process. If you skip updating the watchlist, the workbook doesn't reflect the items for tracking.

To update the watchlist with deployment and migration actions:

1. In the Azure or Microsoft Defender portal, select Microsoft Sentinel and then select **Watchlist**.
2. Select the watchlist with the **Deployment** alias.
3. Then select **Update watchlist &gt; edit watchlist items**.
4. Provide the information for the actions needed for the deployment and migration. [![Screenshot of updating watchlist items with deployment and migration actions.](media/migration-track/migration-track-update-watchlist.png)](media/migration-track/migration-track-update-watchlist.png#lightbox)
5. Select **Save**.

You can now view the watchlist within the migration tracker workbook. Learn how to [manage watchlists](watchlists-manage).

In addition, your team might update or complete tasks during the deployment process. To address these changes, update existing actions or add new actions as you identify new use cases or set new requirements. To update or add actions, edit the **Deployment** watchlist that you deployed. To simplify the process, in the workbook, select **Edit Deployment Watchlist** to open the watchlist directly from the workbook.

## View deployment status

To quickly view the deployment progress, in the **Microsoft Sentinel Deployment and Migration** workbook, select **Deployment** and scroll down to locate the **Summary of progress**. The **Summary of progress** section displays the deployment status, including the following information:

- Tables reporting data
- Number of tables reporting data
- Number of reported logs and which tables report the log data
- Number of enabled rules vs. undeployed rules
- Recommended workbooks deployed
- Total number of workbooks deployed
- Total number of playbooks deployed

## Deploy and monitor data connectors

To monitor deployed resources and deploy new connectors, in the **Microsoft Sentinel Deployment and Migration** workbook, select **Data Connectors &gt; Monitor**. The **Monitor** view lists:

- Current ingestion trends
- Tables ingesting data
- How much data each table is reporting
- Endpoints reporting with Azure Monitor Agent (AMA)
- Data collection rules in the resource group and the devices linked to the rules
- Data connector health (changes and failures)
- Health logs within the specified time range

[![Screenshot of the workbook's Data Connectors tab Monitor view.](media/migration-track/migration-track-data-connectors.png)](media/migration-track/migration-track-data-connectors.png#lightbox)

To configure a data connector:

1. Select the **Configure** view.
2. Select the button with the name of the connector you want to configure.
3. Configure the connector in the connector status screen that opens. If you can't find a connector you need, select the connector name to open the connector gallery or solution gallery. ![Screenshot of the workbook's Configure view.](media/migration-track/migration-track-configure-data-connectors.png)

## Deploy and monitor analytics and incidents

When the data is reported in the workspace, configure and monitor analytics rules. In the **Microsoft Sentinel Deployment and Migration** workbook, select the **Analytics** tab to view all deployed rule templates and lists. The **Analytics** tab indicates which rules are currently in use and how often the rules generate incidents.

[![Screenshot of the workbook's Analytics tab.](media/migration-track/migration-track-analytics.png)](media/migration-track/migration-track-analytics.png#lightbox)

The MITRE coverage view maps your deployed analytics rules to the MITRE ATT&CK framework, so you can identify gaps in threat detection. If you need more coverage, select **Review MITRE coverage** below the table on the left. Use this option to define which areas receive more coverage and which rules are deployed, at any stage of the migration project.

[![Screenshot of the workbook's MITRE Coverage view.](media/migration-track/migration-track-mitre.png)](media/migration-track/migration-track-mitre.png#lightbox)

When you deploy the analytics rules and the Defender product connector is configured to send the alerts, monitor incident creation and frequency under **Deployment &gt; Summary of progress**. The **Summary of progress** section displays metrics regarding alert generation by product, title, and classification, to indicate the health of the SOC and which alerts require the most attention. If alerts are generating too much volume, return to the **Analytics** tab to modify the logic.

[![Screenshot of the summary of progress under the workbook's Analytics tab.](media/migration-track/migration-track-analytics-monitor.png)](media/migration-track/migration-track-analytics-monitor.png#lightbox)

## Deploy and utilize workbooks

To visualize information regarding the data ingestion and detections that Microsoft Sentinel performs, in the **Microsoft Sentinel Deployment and Migration** workbook, select **Workbooks**. Use the **Monitor** view for monitoring information and the **Configure** view for configuration information.

Here are some useful tasks to do in the **Workbooks** tab:

- To view a list of all workbooks in the environment and how many workbooks are deployed, select **Monitor**.
- To view a specific workbook within the **Microsoft Sentinel Deployment and Migration** workbook, select a workbook and then select **Open Selected Workbook**.

    [![Screenshot of selecting a workbook in the Workbook tab.](media/migration-track/migration-track-workbook.png)](media/migration-track/migration-track-workbook.png#lightbox)
- If you haven't yet deployed workbooks, select **Configure** to view a list of commonly used and recommended workbooks. If a workbook isn't listed, select **Go to Workbook Gallery** or **Go to Content Hub** to deploy the relevant workbook.

    ![Screenshot of viewing a workbook from the Workbook tab.](media/migration-track/migration-track-view-workbooks.png)

## Deploy and monitor playbooks and automation rules

When you configure data ingestion, detections, and visualizations, you can now look into automation. In the **Microsoft Sentinel Deployment and Migration** workbook, select **Automation** to view deployed playbooks, and to see which playbooks are currently connected to an automation rule. If automation rules exist, the workbook highlights the following information regarding each rule:

- Name
- Status
- Action or actions of the rule
- The last date the rule was modified and the user that modified the rule
- The date the rule was created

To view, deploy, and test automation in the **Automation** section of the workbook, select **Deploy automation resources** on the bottom left.

Learn about Microsoft Sentinel SOAR capabilities for playbooks and automation rules: [Automate responses with playbooks](automate-responses-with-playbooks) and [Automate incident handling with automation rules](automate-incident-handling-with-automation-rules).

[![Screenshot of the workbook's Automation tab.](media/migration-track/migration-track-automation.png)](media/migration-track/migration-track-automation.png#lightbox)

## Deploy and monitor UEBA

Because data reporting and detections happen at the entity level, it's essential to monitor entity behavior and trends. User and entity behavior analytics (UEBA) helps you do this. To enable the UEBA feature within Microsoft Sentinel, in the **Microsoft Sentinel Deployment and Migration** workbook, select **UEBA**. Here you can customize the entity timelines for entity pages, and view which entity related tables are populated with data.

![Screenshot of the workbook's UEBA tab.](media/migration-track/migration-track-ueba.png)

To enable UEBA:

1. Select **Enable UEBA** above the list of tables.
2. To enable UEBA, select **On**.
3. Select the data sources you want to use to generate insights.
4. Select **Apply**.

After you enable UEBA, monitor and ensure that Microsoft Sentinel is generating UEBA data.

To customize the timeline:

1. Select **Customize Entity Timeline** above the list of tables.
2. Create a custom item, or select one of the out-of-the-box templates.
3. To deploy the template and complete the wizard, select **Create**.

Learn more about [UEBA](identify-threats-with-entity-behavior-analytics) or learn how to [customize the timeline](customize-entity-activities).

## Configure and manage the data lifecycle

When you deploy or migrate to Microsoft Sentinel, it's essential to manage the usage and lifecycle of the incoming logs. In the **Microsoft Sentinel Deployment and Migration** workbook, select **Data Management** to view and configure table retention and archival.

[![Screenshot of the workbook's Data Management tab.](media/migration-track/migration-track-data-management.png)](media/migration-track/migration-track-data-management.png#lightbox)

View information regarding:

- Tables configured for basic log ingestion
- Tables configured for analytics tier ingestion
- Tables configured to be archived
- Tables on the default workspace retention

To modify the existing retention policy for tables:

1. Select the **Default Retention Tables** view.
2. Select the table you want to modify and select **Update Retention**. Edit the following information as needed:
    - Current retention in the workspace
    - Current retention in the archive
    - Total number of days the data lives in the environment
3. Edit the **TotalRetention** value to set a new total number of days that the data should exist within the environment.

The **ArchiveRetention** value is calculated by subtracting the **TotalRetention** value from the **InteractiveRetention** value. If you need to adjust the workspace retention, the change doesn't impact tables that include configured archives and data isn't lost. If you edit the **InteractiveRetention** value and the **TotalRetention** value doesn't change, Azure Log Analytics adjusts the archive retention to compensate the change.

If you prefer to make changes in the UI, select **Update Retention in UI** to open the relevant page.

Learn about [data lifecycle management](/en-us/azure/azure-monitor/logs/data-retention-configure).

## Enable migration tips and instructions

To assist with the deployment and migration process, the workbook includes tips that explain how to use the different tabs, and links to relevant resources. The tips are based on Microsoft Sentinel migration documentation and are relevant to your current SIEM. To enable tips and instructions, in the **Microsoft Sentinel Deployment and Migration** workbook, on the top right, set **MigrationTips** and **Instruction** to **Yes**.

[![Screenshot of the workbook's migration tips and instructions.](media/migration-track/migration-track-tips.png)](media/migration-track/migration-track-tips.png#lightbox)