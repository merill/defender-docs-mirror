---
layout: Conceptual
title: Resources for creating Microsoft Sentinel custom connectors | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/create-custom-connector
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
description: Learn about available resources for creating custom connectors for Microsoft Sentinel. Methods include the Log Analytics API, Logstash, Logic Apps, PowerShell, and Azure Functions.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: krishsa
ms.topic: concept-article
ms.date: 2024-11-06T00:00:00.0000000Z
locale: en-us
document_id: 500094f9-298f-db7e-329d-2476da3be139
document_version_independent_id: bae17852-c45f-de8c-8568-51d90a6d374b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/create-custom-connector.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/create-custom-connector
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/create-custom-connector.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/e60d1924-c4ad-4104-bd1b-973758bbac7a
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/91d5f984-ee3d-43c4-9daf-bb09a6bc4e1a
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 4c4fd58f-7484-9c80-0e1a-5ef24c1203f4
---

# Resources for creating Microsoft Sentinel custom connectors | Microsoft Learn

Microsoft Sentinel provides a wide range of [out-of-the-box connectors for Azure services and external solutions](connect-data-sources), and also supports ingesting data from some sources without a dedicated connector.

If you're unable to connect your data source to Microsoft Sentinel using any of the existing solutions available, consider creating your own data source connector.

For a full list of supported connectors, see the [Find your Microsoft Sentinel data connector)](data-connectors-reference).

## Compare custom connector methods

The following table compares essential details about each method for creating custom connectors described in this article. Select the links in the table for more details about each method.

| Method description | Capability | Serverless | Complexity |
| --- | --- | --- | --- |
| **Codeless Connector Framework (CCF)**Best for less technical audiences to create SaaS connectors using a configuration file instead of advanced development. | Supports all capabilities available with the code. | Yes | Low; simple, codeless development |
| **Azure Monitor Agent**Best for collecting files from on-premises and IaaS sources | File collection, data transformation | No | Low |
| **Logstash**Best for on-premises and IaaS sources, any source for which a plugin is available, and organizations already familiar with Logstash | Supports all capabilities of the Azure Monitor Agent | No; requires a VM or VM cluster to run | Low; supports many scenarios with plugins |
| **Logic Apps**High cost; avoid for high-volume data Best for low-volume cloud sources | Codeless programming allows for limited flexibility, without support for implementing algorithms. If no available action already supports your requirements, creating a custom action may add complexity. | Yes | Low; simple, codeless development |
| **Log Ingestion API in Azure Monitor**Best for ISVs implementing integration, and for unique collection requirements | Supports all capabilities available with the code. | Depends on the implementation | High |
| **Azure Functions**Best for high-volume cloud sources, and for unique collection requirements | Supports all capabilities available with the code. | Yes | High; requires programming knowledge |

Tip

For comparisons of using Logic Apps and Azure Functions for the same connector, see:

- [Ingest Fastly Web Application Firewall logs into Microsoft Sentinel](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/ingest-fastly-web-application-firewall-logs-into-azure-sentinel/1238804)
- Office 365 (Microsoft Sentinel GitHub community): [Logic App connector](https://github.com/Azure/Azure-Sentinel/tree/master/Playbooks/Get-O365Data) | [Azure Function connector](https://github.com/Azure/Azure-Sentinel/tree/master/DataConnectors/O365%20Data)

## Connect with the Codeless Connector Framework

The Codeless Connector Framework (CCF) provides a configuration file that can be used by both customers and partners, and then deployed to your own workspace, or as a solution to Microsoft Sentinel's content hub.

Connectors created using the CCF are fully SaaS, without any requirements for service installations, and also include health monitoring and full support from Microsoft Sentinel.

For more information, see [Create a codeless connector for Microsoft Sentinel](isv/create-codeless-connector).

## Connect with the Azure Monitor Agent

If your data source delivers events in text files, we recommend that you use the Azure Monitor Agent to create your custom connector.

- For more information, see [Collect logs from a text file with Azure Monitor Agent](/en-us/azure/azure-monitor/agents/data-collection-log-text).
- For an example of this method, see [Collect logs from a JSON file with Azure Monitor Agent](/en-us/azure/azure-monitor/agents/data-collection-log-json).

## Connect with Logstash

If you're familiar with [Logstash](https://www.elastic.co/logstash), you may want to use Logstash with the [Logstash output plug-in for Microsoft Sentinel](connect-logstash) to create your custom connector.

With the Microsoft Sentinel Logstash Output plugin, you can use any Logstash input and filtering plugins, and configure Microsoft Sentinel as the output for a Logstash pipeline. Logstash has a large library of plugins that enable input from various sources, such as Event Hubs, Apache Kafka, Files, Databases, and Cloud services. Use filtering plug-ins to parse events, filter unnecessary events, obfuscate values, and more.

For examples of using Logstash as a custom connector, see:

- [Hunting for Capital One Breach TTPs in AWS logs using Microsoft Sentinel](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/hunting-for-capital-one-breach-ttps-in-aws-logs-using-azure-sentinel---part-i/1014258) (blog)
- [Radware Microsoft Sentinel implementation guide](https://support.radware.com/ci/okcsFattach/get/1025459_3)

For examples of useful Logstash plugins, see:

- [Cloudwatch input plugin](https://www.elastic.co/guide/en/logstash/current/plugins-inputs-cloudwatch.html)
- [Azure Event Hubs plugin](https://www.elastic.co/guide/en/logstash/current/plugins-inputs-azure_event_hubs.html)
- [Google Cloud Storage input plugin](https://www.elastic.co/guide/en/logstash/current/plugins-inputs-google_cloud_storage.html)
- [Google_pubsub input plugin](https://www.elastic.co/guide/en/logstash/current/plugins-inputs-google_pubsub.html)

Tip

Logstash also enables scaled data collection using a cluster. For more information, see [Using a load-balanced Logstash VM at scale](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/scaling-up-syslog-cef-collection/1185854).

## Connect with Logic Apps

Use [Azure Logic Apps](/en-us/azure/logic-apps/) to create a serverless, custom connector for Microsoft Sentinel.

Note

While creating serverless connectors using Logic Apps may be convenient, using Logic Apps for your connectors may be costly for large volumes of data.

We recommend that you use this method only for low-volume data sources, or enriching your data uploads.

1. **Use one of the following triggers to start your Logic Apps**:

    | Trigger | Description |
    | --- | --- |
    | **A recurring task** | For example, schedule your Logic App to retrieve data regularly from specific files, databases, or external APIs. For more information, see [Create, schedule, and run recurring tasks and workflows in Azure Logic Apps](/en-us/azure/connectors/connectors-native-recurrence). |
    | **On-demand triggering** | Run your Logic App on-demand for manual data collection and testing. For more information, see [Call, trigger, or nest logic apps using HTTPS endpoints](/en-us/azure/logic-apps/logic-apps-http-endpoint). |
    | **HTTP/S endpoint** | Recommended for streaming, and if the source system can start the data transfer. For more information, see [Call service endpoints over HTTP or HTTPS](/en-us/azure/connectors/connectors-native-http). |
2. **Use any of the Logic App connectors that read information to get your events**. For example:

    - [Connect to a REST API](/en-us/connectors/custom-connectors/)
    - [Connect to a SQL Server](/en-us/connectors/sql/)
    - [Connect to a file system](/en-us/connectors/filesystem/)

    Tip

    Custom connectors to REST APIs, SQL Servers, and file systems also support retrieving data from on-premises data sources. For more information, see [Install on-premises data gateway](/en-us/connectors/filesystem/) documentation.
3. **Prepare the information you want to retrieve**.

    For example, use the [parse JSON action](/en-us/azure/logic-apps/logic-apps-perform-data-operations#parse-json-action) to access properties in JSON content, enabling you to select those properties from the dynamic content list when you specify inputs for your Logic App.

    For more information, see [Perform data operations in Azure Logic Apps](/en-us/azure/logic-apps/logic-apps-perform-data-operations).
4. **Write the data to Log Analytics**.

    For more information, see the [Azure Log Analytics Data Collector](/en-us/connectors/azureloganalyticsdatacollector/) documentation.

For examples of how you can create a custom connector for Microsoft Sentinel using Logic Apps, see:

- [Create a data pipeline with the Data Collector API](/en-us/connectors/azureloganalyticsdatacollector/)
- [Palo Alto Prisma Logic App connector using a webhook](https://github.com/Azure/Azure-Sentinel/tree/master/Playbooks/Ingest-Prisma) (Microsoft Sentinel GitHub community)
- [Secure your Microsoft Teams calls with scheduled activation](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/secure-your-calls--monitoring-microsoft-teams-callrecords-activity-logs-using-az/1574600) (blog)
- [Ingesting AlienVault OTX threat indicators into Microsoft Sentinel](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/ingesting-alien-vault-otx-threat-indicators-into-azure-sentinel/1086566) (blog)

## Connect with the Log Ingestion API

You can stream events to Microsoft Sentinel by using the Log Analytics Data Collector API to call a RESTful endpoint directly.

While calling a RESTful endpoint directly requires more programming, it also provides more flexibility.

For more information, see the following articles:

- [Log Ingestion API in Azure Monitor](/en-us/azure/azure-monitor/logs/logs-ingestion-api-overview).
- [Sample code to send data to Azure Monitor using Logs ingestion API](/en-us/azure/azure-monitor/logs/tutorial-logs-ingestion-code).

## Connect with Azure Functions

Use Azure Functions together with a RESTful API and various coding languages, such as [PowerShell](/en-us/azure/azure-functions/functions-reference-powershell), to create a serverless custom connector.

For examples of this method, see:

- [Connect your VMware Carbon Black Cloud Endpoint Standard to Microsoft Sentinel with Azure Function](data-connectors/vmware-carbon-black-cloud-using-azure-functions)
- [Connect your Okta Single Sign-On to Microsoft Sentinel with Azure Function](data-connectors/okta-single-sign-on-using-azure-function)
- [Connect your Proofpoint TAP to Microsoft Sentinel with Azure Function](data-connectors/proofpoint-tap-using-azure-functions)
- [Connect your Qualys VM to Microsoft Sentinel with Azure Function](data-connectors/qualys-vulnerability-management-using-azure-functions)
- [Ingesting XML, CSV, or other formats of data](/en-us/azure/azure-monitor/logs/create-pipeline-datacollector-api#ingesting-xml-csv-or-other-formats-of-data)
- [Monitoring Zoom with Microsoft Sentinel](https://techcommunity.microsoft.com/blog/microsoftsentinelblog/monitoring-zoom-with-azure-sentinel/1341516) (blog)
- [Deploy a Function App for getting Office 365 Management API data into Microsoft Sentinel](https://github.com/Azure/Azure-Sentinel/tree/master/DataConnectors/O365%20Data) (Microsoft Sentinel GitHub community)

## Parse your custom connector data

To take advantage of the data collected with your custom connector, [develop Advanced Security Information Model (ASIM) parsers](normalization-develop-parsers) to work with your connector. Using [ASIM](normalization) enables Microsoft Sentinel's built-in content to use your custom data and makes it easier for analysts to query the data.

If your connector method allows for it, you can implement part of the parsing as part of the connector to improve query time parsing performance:

- **If you've used Logstash**, use the [Grok](https://www.elastic.co/guide/en/logstash/current/plugins-filters-grok.html) filter plugin to parse your data.
- **If you've used an Azure function**, parse your data with code.

You will still need to implement ASIM parsers, but implementing part of the parsing directly with the connector simplifies the parsing and improves performance.