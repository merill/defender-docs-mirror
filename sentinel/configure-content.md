---
layout: Conceptual
title: Configure Microsoft Sentinel Content | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/configure-content
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
description: In this step of your deployment, you configure the Microsoft Sentinel security content, like your data connectors, analytics rules, automation rules, and more.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: krishsa
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 05e03fdc-bb7e-7e14-3c14-9b0bbc78c781
document_version_independent_id: 7a9b7dfa-446c-a0dd-df80-814b5eabc416
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/configure-content.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/configure-content
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/configure-content.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 9e4e027d-3788-ac94-629b-17fee7b41ebe
---

# Configure Microsoft Sentinel Content | Microsoft Learn

In the deployment step to [enable Microsoft Sentinel features and content](enable-sentinel-features-content), you enabled Microsoft Sentinel, health monitoring, and the required solutions. In this article, you learn how to configure the different types of Microsoft Sentinel security content, which allow you to detect, monitor, and respond to security threats across your systems. This article is part of the [Deployment guide for Microsoft Sentinel](deploy-overview).

## Configure your security content

Follow these steps to configure your security content.

| Step | Description |
| --- | --- |
| **Set up data connectors** | Based on the [data sources you selected when you planned your deployment](prioritize-data-connectors), and after [enabling Microsoft Sentinel features and content](enable-sentinel-features-content), you can now install or set up your data connectors.- If you're using an existing connector, find your connector from the [Microsoft Sentinel data connectors reference](data-connectors-reference).- If you're creating a custom connector, use the [custom connector creation resources](create-custom-connector).- If you're setting up a connector to ingest CEF or Syslog logs, review the [CEF and Syslog connection options](connect-cef-syslog-options). |
| **Set up analytics rules** | After you've set up Microsoft Sentinel to collect data from all over your organization, you can begin using [analytics rules](threat-detection) to detect threats. Select the steps you need to set up and configure your analytics rules:- [Create scheduled rules from templates](create-analytics-rule-from-template) or [create scheduled rules from scratch](create-analytics-rules): Create analytics rules to help discover threats and anomalous behaviors in your environment.- [Map data fields to entities](map-data-fields-to-entities): Add or change entity mappings in an analytics rule.- [Surface custom details in alerts](surface-custom-details-in-alerts): Add or change custom details in an analytics rule.- [Customize alert details](customize-alert-details): Override the default properties of alerts with content from the underlying query results.- [Export and import analytics rules](import-export-analytics-rules): Export your analytics rules to Azure Resource Manager (ARM) template files, and import rules from these files. The export action creates a JSON file in your browser's downloads location, that you can then rename, move, and otherwise handle like any other file.- [Create near-real-time (NRT) detection analytics rules](create-nrt-rules): Create near-time analytics rules for up-to-the-minute threat detection out-of-the-box. This type of rule was designed to be highly responsive by running its query at intervals just one minute apart.- [Work with anomaly detection analytics rules](work-with-anomaly-rules): Work with built-in anomaly templates that use thousands of data sources and millions of events, or change thresholds and parameters for the anomalies within the user interface.- [Manage template versions for your scheduled analytics rules](manage-analytics-rule-templates): Track the versions of your analytics rule templates, and either revert active rules to existing template versions, or update them to new ones.- [Handle ingestion delay in scheduled analytics rules](ingestion-delay): Learn how ingestion delay might impact your scheduled analytics rules and how you can fix them to cover these gaps. |
| **Set up automation rules** | [Create automation rules](create-manage-use-automation-rules). Define the triggers and conditions that determine when your [automation rule to automate incident handling](automate-incident-handling-with-automation-rules) runs, the various actions that you can have the rule perform, and the remaining features and functionalities. |
| **Set up playbooks** | A [Microsoft Sentinel playbook](automate-responses-with-playbooks) is a collection of remediation actions that you run from Microsoft Sentinel as a routine, to help automate and orchestrate your threat response. To set up playbooks:- Review [recommended playbooks](automate-responses-with-playbooks#recommended-playbooks)- [Create playbooks from templates](use-playbook-templates): A playbook template is a prebuilt, tested, and ready-to-use workflow that can be customized to meet your needs. Templates can also serve as a reference for best practices when developing playbooks from scratch, or as inspiration for new automation scenarios.- Review how to [create a Microsoft Sentinel playbook](automate-responses-with-playbooks#steps-for-creating-a-playbook) |
| **Set up workbooks** | [Workbooks](monitor-your-data) provide a flexible canvas for data analysis and the creation of rich visual reports within Microsoft Sentinel. Workbook templates allow you to quickly gain insights across your data as soon as you connect a data source. To set up workbooks:- Review [commonly used Microsoft Sentinel workbooks](top-workbooks)- [Use existing workbook templates available with packaged solutions](monitor-your-data)- [Create custom workbooks across your data](monitor-your-data#create-new-workbook) |
| **Set up watchlists** | [Watchlists](watchlists) allow you to correlate data from a data source you provide with the events in your Microsoft Sentinel environment. To set up watchlists:- [Create watchlists](watchlists-create)- [Build queries or detection rules with watchlists](watchlists-queries): Query data in any table against data from a watchlist by treating the watchlist as a table for joins and lookups. When you create a watchlist, you define the SearchKey. The search key is the name of a column in your watchlist that you expect to use as a join with other data or as a frequent object of searches. |

### Set up data connectors

Based on the [data sources you selected when you planned your deployment](prioritize-data-connectors), and after [enabling the relevant solutions](enable-sentinel-features-content), you can now install or set up your data connectors.

- If you're using an existing connector, [find your connector](data-connectors-reference) from this full list of data connectors.
- If you're creating a custom connector, use [these resources](create-custom-connector).
- If you're setting up a connector to ingest CEF or Syslog logs, review these [options](connect-cef-syslog-options).

### Set up analytics rules

After you've set up Microsoft Sentinel to collect data from all over your organization, you can begin using [analytics rules](threat-detection) to detect threats. Select the steps you need to set up and configure your analytics rules:

- Create scheduled rules [from templates](create-analytics-rule-from-template) or [from scratch](create-analytics-rules): Create analytics rules to help discover threats and anomalous behaviors in your environment.
- [Map data fields to entities](map-data-fields-to-entities): Add or change entity mappings in an analytics rule.
- [Surface custom details in alerts](surface-custom-details-in-alerts): Add or change custom details in an analytics rule.
- [Customize alert details](customize-alert-details): Override the default properties of alerts with content from the underlying query results.
- [Export and import analytics rules](import-export-analytics-rules): Export your analytics rules to Azure Resource Manager (ARM) template files and import rules from these files. The export action creates a JSON file in your browser's downloads location that you can then rename, move, and otherwise handle like any other file.
- [Create near-real-time (NRT) detection analytics rules](create-nrt-rules): Create near-time analytics rules for up-to-the-minute threat detection out of the box. This type of rule is designed to be highly responsive by running its query at intervals just one minute apart.
- [Work with anomaly detection analytics rules](work-with-anomaly-rules): Work with built-in anomaly templates that use thousands of data sources and millions of events, or change thresholds and parameters for the anomalies within the user interface.
- [Manage template versions for your scheduled analytics rules](manage-analytics-rule-templates): Track the versions of your analytics rule templates and either revert active rules to existing template versions, or update them to new ones.
- [Handle ingestion delay in scheduled analytics rules](ingestion-delay): Learn how ingestion delay might impact your scheduled analytics rules and how you can fix them to cover these gaps.

### Set up automation rules

First, [Create automation rules](create-manage-use-automation-rules). Define the triggers and conditions that determine when your [automation rule](automate-incident-handling-with-automation-rules) runs, the various actions that you can have the rule perform, and the remaining features and functionalities.

### Set up playbooks

A [playbook](automate-responses-with-playbooks) is a collection of remediation actions that you run from Microsoft Sentinel as a routine, to help automate and orchestrate your threat response. To set up playbooks:

- Review [recommended playbooks](automate-responses-with-playbooks#recommended-playbooks).
- [Create playbooks from templates](use-playbook-templates): A playbook template is a prebuilt, tested, and ready-to-use workflow that can be customized to meet your needs. Templates can also serve as a reference for best practices when developing playbooks from scratch, or as inspiration for new automation scenarios.
- Review these [steps for creating a playbook](automate-responses-with-playbooks#steps-for-creating-a-playbook).

### Set up workbooks

[Workbooks](monitor-your-data) provide a flexible canvas for data analysis and the creation of rich visual reports within Microsoft Sentinel. Workbook templates allow you to quickly gain insights across your data as soon as you connect a data source. To set up workbooks:

- Review [commonly used Microsoft Sentinel workbooks](top-workbooks).
- [Use existing workbook templates available with packaged solutions](monitor-your-data).
- [Create custom workbooks across your data](monitor-your-data#create-new-workbook).

### Set up watchlists

[Watchlists](watchlists) allow you to correlate data from a data source you provide with the events in your Microsoft Sentinel environment. To set up watchlists:

- [Create watchlists](watchlists-create).
- [Build queries or detection rules with watchlists](watchlists-queries): Query data in any table against data from a watchlist by treating the watchlist as a table for joins and lookups. When you create a watchlist, you define the SearchKey. The search key is the name of a column in your watchlist that you expect to use as a join with other data or as a frequent object of searches.