---
layout: Conceptual
title: Auditing and health monitoring in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/health-audit
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
description: Learn about the Microsoft Sentinel health and audit feature, which monitors service health drifts and user actions.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: concept-article
ms.date: 2025-08-24T00:00:00.0000000Z
locale: en-us
document_id: c008d4af-2715-e540-7ef2-432d62652b3c
document_version_independent_id: 015512aa-b6f6-bdc7-f11a-4d387f83446e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/health-audit.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/health-audit
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/health-audit.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/43093068-2dda-408b-b3fe-dfd705c84f78
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/e453d60d-ba7e-43bc-8028-ec38e6b62512
platformId: 72e0d3c5-c38b-ac66-cfcb-9e3789be3b26
---

# Auditing and health monitoring in Microsoft Sentinel | Microsoft Learn

Microsoft Sentinel is a critical service for advancing and protecting the security of your organization’s technological and information assets, so you want to be sure that it's always running smoothly and free of interference.

You want to verify that the service's many moving parts are always functioning as intended, and it isn't being manipulated by unauthorized actions, whether by internal users or otherwise. You might also like to configure notifications of health drifts or unauthorized actions to be sent to relevant stakeholders who can respond or approve a response. For example, you can set conditions to trigger the sending of emails or Microsoft Teams messages to operations teams, managers, or officers, launch new tickets in your ticketing system, and so on.

This article describes how Microsoft Sentinel’s health monitoring and auditing features let you monitor the activity of some of the service’s key resources and inspect logs of user actions within the service.

## Health and audit data storage

Health and audit data are collected in two tables in your Log Analytics workspace: *SentinelHealth* and *SentinelAudit*

**Audit data** is collected in the *SentinelAudit* table.

**Health data** is collected in the *SentinelHealth* table, which captures events that record each time an automation rule is run and the end results of those runs. The *SentinelHealth* table includes:

- Whether actions launched in the rule succeed or fail, and the playbooks called by the rule.
- Events that record the on-demand (manual or API-based) triggering of playbooks, including the identities that triggered them, and the end results of those runs

The *SentinelHealth* table doesn't include a record of the execution of a playbook's contents, only whether the playbook was launched successfully. A log of the actions taken within a playbook, which are Logic Apps workflows, are listed in the *AzureDiagnostics* table. The *AzureDiagnostics* provides you with a complete picture of your automation health when used in tandem with the *SentinelHealth* data.

The most common way you use this data is by querying these tables. For best results, build your queries on the **pre-built functions** on these tables, ***\_SentinelHealth()*** and ***\_SentinelAudit()***, instead of querying the tables directly. These functions ensure the maintenance of your queries' backward compatibility in the event of changes being made to the schema of the tables themselves.

The *SentinelHealth* table isn't billable and incurs no charges for ingesting health data. The *SentinelAudit* table is billable, and as in other areas of Microsoft Sentinel, costs incurred depend on the log volume, which might be affected by the number of activities and changes made on related rules. For more information, see [Plan costs and understand Microsoft Sentinel pricing and billing](billing).

### Questions to verify service health and audit data

Use the following questions to guide your monitoring of Microsoft Sentinel's health and audit data:

**Is the data connector running correctly?**

[Is the data connector receiving data](monitor-data-connector-health)? For example, if you've instructed Microsoft Sentinel to run a query every 5 minutes, you want to check whether that query is being performed, how it's performing, and whether there are any risks or vulnerabilities related to the query.

**Did an automation rule run as expected?**

[Did your automation rule run when it was supposed to](monitor-automation-health)—that is, when its conditions were met? Did all the actions in the automation rule run successfully?

**Did an analytics rule run as expected?**

[Did your analytics rule run when it was supposed to, and did it generate results](monitor-analytics-rule-integrity)? If you're expecting to see particular incidents in your queue but you don't, you want to know whether the rule ran but didn't find anything (or enough things), or didn't run at all.

**Were unauthorized changes made to an analytics rule?**

[Was something changed in the rule](monitor-analytics-rule-integrity)? You didn't get the results you expected from your analytics rule, and it didn't have any health issues. You want to see if any unplanned changes were made to the rule, and if so, what changes were made, by whom, from where, and when.

## Health and audit monitoring flow

To start collecting health and audit data, you need to [enable health and audit monitoring](enable-monitoring) in the Microsoft Sentinel settings. Then you can dive into the health and audit data that Microsoft Sentinel collects:

| Activity | More information |
| --- | --- |
| **Run queries** on the *SentinelHealth* and *SentinelAudit* data tables from the Microsoft Sentinel **Logs** page. | - [Data connectors](monitor-data-connector-health#run-queries-to-detect-health-drifts)<br>- [Automation rules and playbooks](monitor-automation-health#get-the-complete-automation-picture) (join query with Azure Logic Apps diagnostics)<br>- [Analytics rules](monitor-analytics-rule-integrity#run-queries-to-detect-health-and-integrity-issues) |
| **Use the auditing and health monitoring workbooks** provided in Microsoft Sentinel. | - [Data connectors](monitor-data-connector-health#use-the-health-monitoring-workbook)<br>- [Automation rules and playbooks](monitor-automation-health#use-the-health-monitoring-workbook)<br>- [Analytics rules](monitor-analytics-rule-integrity#use-the-auditing-and-health-monitoring-workbook) |
| **Use Microsoft Sentinel's execution management tools** to monitor and optimize scheduled analytics rules' execution | - [Monitor and optimize the execution of your scheduled analytics rules](monitor-optimize-analytics-rule-execution) |
| **Export the data into various destinations**, like your Log Analytics workspace, archiving to a storage account, and more. | - [Diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/diagnostic-settings) |