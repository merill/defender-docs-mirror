---
layout: Conceptual
title: Microsoft Sentinel data connectors | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/connect-data-sources
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
description: Learn about supported data connectors, like Microsoft Defender XDR (formerly Microsoft 365 Defender), Microsoft 365 and Office 365, Microsoft Entra ID, ATP, and Defender for Cloud Apps to Microsoft Sentinel.
ms.author: guywild
author: guywi-ms
ms.reviewer: ofshezaf
ms.topic: concept-article
ms.date: 2024-11-06T00:00:00.0000000Z
ms.collection: usx-security
locale: en-us
document_id: fbdb44e3-1cd4-646b-a684-092bb317cf6c
document_version_independent_id: 3d7337db-0b7b-d8dd-053d-3081f364212e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/connect-data-sources.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/connect-data-sources
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/connect-data-sources.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: bc171ab7-cc3a-98a5-e58b-862220504211
---

# Microsoft Sentinel data connectors | Microsoft Learn

After you onboard Microsoft Sentinel into your workspace, use data connectors to start ingesting your data into Microsoft Sentinel. Microsoft Sentinel comes with many out of the box connectors for Microsoft services, which integrate in real time. For example, the Microsoft Defender XDR connector is a service-to-service connector that integrates data from Office 365, Microsoft Entra ID, Microsoft Defender for Identity, and Microsoft Defender for Cloud Apps.

Built-in connectors enable connection to the broader security ecosystem for non-Microsoft products. For example, use Syslog, Common Event Format (CEF), or REST APIs to connect your data sources with Microsoft Sentinel.

Note

For information about feature availability in US Government clouds, see the Microsoft Sentinel tables in [Cloud feature availability for US Government customers](/en-us/azure/security/fundamentals/feature-availability).

Important

As per the [2024 announcement](/en-us/azure/azure-monitor/logs/custom-logs-migrate), after September 14, 2026, the legacy HTTP Data Collector API will no longer be supported. Data sources, custom integrations, or connectors that use the HTTP Data Collector API should transition to a supported alternative to avoid potential ingestion interruptions after this date.

If you're currently using the HTTP Data Collector API, we recommend that you start planning your migration to the [Logs Ingestion API](/en-us/azure/azure-monitor/logs/logs-ingestion-api-overview) or the [Codeless Connector Framework (CCF)](/en-us/azure/sentinel/create-codeless-connector) to ensure uninterrupted data ingestion, improved reliability, scalability, and long-term support.

## Data management considerations for Microsoft Sentinel data lake

The following considerations must be factored into your compliance and data management planning:

- **GDPR and Data Retention**

    - Tenant admins can exercise GDPR rights using the Purge feature for the analytics tier. This doesn't affect the data lake tier.
    - Specific records can't be purged from the Sentinel data lake. The data lake retains ingested data for the defined retention period, even if the data is deleted at the source or in the analytics tier.
- **Purview Integration**. Changes to Purview settings don't have any effect on data stored in the Sentinel data lake.
- **Storage Location** Sentinel data lake storage locations are selected by the tenant admin and may differ from the primary storage location of the source services.

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Data connectors provided with solutions

Microsoft Sentinel solutions provide packaged security content, including data connectors, workbooks, analytics rules, playbooks, and more. When you deploy a solution with a data connector, you get the data connector together with related content in the same deployment.

The Microsoft Sentinel **Data connectors** page lists the installed or in-use data connectors.

# [Defender portal](#tab/defender-portal)
[![Screenshot of the data connectors gallery.](media/connect-data-sources/data-connector-list-defender.png)](media/connect-data-sources/data-connector-list-defender.png#lightbox)

# [Azure portal](#tab/azure-portal)
[![Screenshot of the data connectors gallery.](media/connect-data-sources/data-connector-list.png)](media/connect-data-sources/data-connector-list.png#lightbox)

---

To add more data connectors, install the solution associated with the data connector from the **Content Hub**. For more information, see the following articles:

- [Find your Microsoft Sentinel data connector](data-connectors-reference)
- [About Microsoft Sentinel content and solutions](sentinel-solutions)
- [Discover and manage Microsoft Sentinel out-of-the-box content](sentinel-solutions-deploy)
- [Microsoft Sentinel content hub catalog](sentinel-solutions-catalog)
- [Advanced Security Information Model (ASIM) based domain solutions for Microsoft Sentinel](domain-based-essential-solutions)

## Create custom connectors

If you're unable to connect your data source to Microsoft Sentinel using any of the existing solutions available, consider creating your own data source connector. For example, many security solutions provide a set of APIs for retrieving log files and other security data from their product or service. Those APIs connect to Microsoft Sentinel with one of the following methods:

- The data source APIs are configured with the [Codeless Connector Framework](isv/create-codeless-connector).
- The data connector uses the Log Ingestion API for Azure Monitor as part of an [Azure Function](connect-azure-functions-template) or [Logic App](create-custom-connector#connect-with-logic-apps).

You can also use Azure Monitor Agent directly or Logstash to create your custom connector. For more information, see [Resources for creating Microsoft Sentinel custom connectors](create-custom-connector).

## Agent-based integration for data connectors

Microsoft Sentinel can use agents provided by the Azure Monitor service (on which Microsoft Sentinel is based) to collect data from any data source that can perform real-time log streaming. For example, most on-premises data sources connect by using agent-based integration.

The following sections describe the different types of Microsoft Sentinel agent-based data connectors. To configure connections using agent-based mechanisms, follow the steps in each Microsoft Sentinel data connector page.

### Syslog and Common Event Format (CEF)

You can stream events from Linux-based, Syslog-supporting devices into Microsoft Sentinel by using the Azure Monitor Agent (AMA). Log formats vary, but many sources support CEF-based formatting. Depending on the device type, the agent is installed either directly on the device, or on a dedicated Linux-based log forwarder. The AMA receives plain Syslog or CEF event messages from the Syslog daemon over UDP. The Syslog daemon forwards events to the agent internally, communicating over TCP or UDS (Unix Domain Sockets), depending on the version. The AMA then transmits these events to the Microsoft Sentinel workspace.

Here's a simple flow that shows how Microsoft Sentinel streams Syslog data.

1. The device's built-in Syslog daemon collects local events of the specified types, and forwards the events locally to the agent.
2. The agent streams the events to your Log Analytics workspace.
3. After successful configuration, Syslog messages appear in the Log Analytics *Syslog* table, and CEF messages in the *CommonSecurityLog* table.

For more information, see [Syslog and Common Event Format (CEF) via AMA connectors for Microsoft Sentinel](cef-syslog-ama-overview).

### Custom logs

For some data sources, you can collect logs as files on Windows or Linux computers using the Log Analytics custom log collection agent.

To connect using the Log Analytics custom log collection agent, follow the steps in each Microsoft Sentinel data connector page. After successful configuration, the data appears in custom tables.

For more information, see [Custom Logs via AMA data connector - Configure data ingestion to Microsoft Sentinel from specific applications](unified-connector-custom-device).

## Service-to-service integration for data connectors

Microsoft Sentinel uses the Azure foundation to provide out-of-the-box service-to-service support for Microsoft services and Amazon Web Services.

For more information, see the following articles:

- [Connect Microsoft Sentinel to Azure, Windows, Microsoft, and Amazon services](connect-azure-windows-microsoft-services)
- [Find your Microsoft Sentinel data connector](data-connectors-reference)

## Data connector support

Both Microsoft and other organizations author Microsoft Sentinel data connectors. Each data connector has one of the following support types listed on the data connector page in Microsoft Sentinel.

| Support type | Description |
| --- | --- |
| **Microsoft-supported** | Applies to:<br>- Data connectors for data sources where Microsoft is the data provider and author.<br>- Some Microsoft-authored data connectors for non-Microsoft data sources.<br><br>Microsoft supports and maintains data connectors in this category according to the [Microsoft Azure Support Plans](https://azure.microsoft.com/support/options/#overview).Partners or the Community support data connectors authored by any party other than Microsoft. |
| **Partner-supported** | Applies to data connectors authored by parties other than Microsoft.The partner company provides support or maintenance for these data connectors. The partner company can be an Independent Software Vendor, a Managed Service Provider (MSP/MSSP), a Systems Integrator (SI), or any organization whose contact information is provided on the Microsoft Sentinel page for that data connector.For any issues with a partner-supported data connector, contact the specified data connector support contact. |
| **Community-supported** | Applies to data connectors authored by Microsoft or partner developers that don't have listed contacts for data connector support and maintenance on the data connector page in Microsoft Sentinel.For questions or issues with these data connectors, you can [file an issue](https://github.com/Azure/Azure-Sentinel/issues/new/choose) in the [Microsoft Sentinel GitHub community](https://aka.ms/threathunters). |

For more information, see [Find support for a data connector](configure-data-connector#find-support-for-a-data-connector).