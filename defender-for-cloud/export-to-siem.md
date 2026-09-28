---
layout: Conceptual
title: Stream Alerts to Monitoring Solutions - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/export-to-siem
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
description: Learn how to stream your Microsoft Defender for Cloud security alerts to Microsoft Sentinel, SIEMs, SOAR, or ITSM solutions.
ms.topic: how-to
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1013
locale: en-us
document_id: 1a23bfde-bd0d-04ef-4a02-6b2e84298a88
document_version_independent_id: 424cba51-48ff-8151-5037-320e7a03db1f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/export-to-siem.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/export-to-siem
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/export-to-siem.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d774b87-7dcb-40bf-a0b9-5a7a9efff0d1
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/89dc5f37-0e4e-4b05-ad87-5fcd2b941a8a
platformId: 30caf917-5c37-828b-cc5b-71f8c88876d9
---

# Stream Alerts to Monitoring Solutions - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud can stream security alerts into various Security Information and Event Management (SIEM), Security Orchestration Automated Response (SOAR), and IT Service Management (ITSM) solutions. Security alerts are generated when threats are detected on your resources. Defender for Cloud prioritizes and lists the alerts on the Alerts page, along with information needed to quickly investigate the problem. Detailed steps are provided to assist you to remediate the detected threat. All alerts data is retained for 90 days.

Built-in Azure tools are available to ensure you can view your alert data in the following solutions:

- Microsoft Sentinel
- Splunk Enterprise and Splunk Cloud
- Power BI
- ServiceNow
- IBM QRadar
- Palo Alto Networks
- ArcSight
- Dynatrace

## Stream alerts to Defender XDR with the Defender XDR API

Defender for Cloud natively integrates with [Microsoft Defender XDR](/en-us/microsoft-365/security/defender/microsoft-365-defender) to allow you to use Defender XDR's incidents and alerts API to stream alerts and incidents into non-Microsoft solutions. Defender for Cloud customers can access one API for all Microsoft security products and can use this integration as an easier way to export alerts and incidents.

Learn how to [integrate SIEM tools with Defender XDR](/en-us/microsoft-365/security/defender/configure-siem-defender).

## Stream alerts to Microsoft Sentinel

Defender for Cloud natively integrates with [Microsoft Sentinel](/en-us/azure/sentinel/overview), Azure's cloud-native SIEM and SOAR solution.

### Microsoft Sentinel's connectors for Defender for Cloud

Microsoft Sentinel includes built-in connectors for Microsoft Defender for Cloud at the subscription and tenant levels.

You can:

- [Stream alerts to Microsoft Sentinel at the subscription level](/en-us/azure/sentinel/connect-azure-security-center).
- [Connect all subscriptions in your tenant to Microsoft Sentinel](https://techcommunity.microsoft.com/t5/azure-sentinel/azure-security-center-auto-connect-to-sentinel/ba-p/1387539).

When you connect Defender for Cloud to Microsoft Sentinel, the status of Defender for Cloud alerts that get ingested into Microsoft Sentinel is synchronized between the two services. For example, when an alert is closed in Defender for Cloud, that alert is also shown as closed in Microsoft Sentinel. When you change the status of an alert in Defender for Cloud, the status of the alert in Microsoft Sentinel is also updated. However, the statuses of any Microsoft Sentinel *incidents* that contain the synchronized Microsoft Sentinel alert aren't updated.

You can enable the **bi-directional alert synchronization** feature to automatically sync the status of the original Defender for Cloud alerts with Microsoft Sentinel incidents that contain the copies of the Defender for Cloud alerts. For example, when you close a Microsoft Sentinel incident that contains a Defender for Cloud alert, Defender for Cloud automatically closes the corresponding original alert.

Learn how to [connect alerts from Microsoft Defender for Cloud](/en-us/azure/sentinel/connect-azure-security-center).

### Configure ingestion of all audit logs into Microsoft Sentinel

You can also investigate Defender for Cloud alerts in Microsoft Sentinel by streaming your audit logs into Microsoft Sentinel:

- [Connect Windows security events](/en-us/azure/sentinel/connect-windows-security-events)
- [Collect data from Linux-based sources using Syslog](/en-us/azure/sentinel/connect-syslog)
- [Connect data from Azure Activity log](/en-us/azure/sentinel/data-connectors/azure-activity)

Tip

Microsoft Sentinel bills based on the volume of data that it ingests for analysis in Microsoft Sentinel and stores in the Azure Monitor Log Analytics workspace. Microsoft Sentinel offers a flexible and predictable pricing model. [Learn more at the Microsoft Sentinel pricing page](https://azure.microsoft.com/pricing/details/azure-sentinel/).

## Stream alerts to QRadar and Splunk

To export security alerts to Splunk and QRadar, you need to use Event Hubs and a built-in connector. You can either use a PowerShell script or the Azure portal to set up the requirements for exporting security alerts for your subscription or tenant. After you put the requirements in place, install the connector in your SIEM platform by following the QRadar or Splunk steps described later in this article.

### Prerequisites

Before you set up the Azure services for exporting alerts, ensure you have:

- Azure subscription ([Create a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn))
- Azure resource group ([Create a resource group](/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal))
- **Owner** role on the alerts scope (subscription, management group, or tenant), or these specific permissions:

    - Write permissions for event hubs and the Event Hubs Policy
    - Create permissions for [Microsoft Entra applications](/en-us/azure/active-directory/develop/howto-create-service-principal-portal#permissions-required-for-registering-an-app), if you aren't using an existing Microsoft Entra application
    - Assign permissions for policies, if you're using the Azure Policy 'DeployIfNotExist'

### Set up the Azure services

Set up your Azure environment to support continuous export by using either a PowerShell script or the Azure portal.

#### Use PowerShell script (Recommended)

To set up the Azure services by using a PowerShell script, follow these steps:

1. Download and run the [Defender for Cloud third-party SIEM integration PowerShell scripts](https://github.com/Azure/Microsoft-Defender-for-Cloud/tree/main/Powershell%20scripts/3rd%20party%20SIEM%20integration).
2. Enter the required parameters.
3. Run the script.

The script performs all of the steps for you. When the script finishes, use the output to install the solution in the SIEM platform.

#### Use the Azure portal

To create the required resources in the Azure portal, follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Search for and select **Event Hubs**.
3. [Create an Event Hubs namespace and event hub](/en-us/azure/event-hubs/event-hubs-create).
4. Define a policy for the event hub with `Send` permissions.

    - If you're streaming alerts to QRadar:

        1. Create an event hub `Listen` policy.
        2. Copy and save the connection string of the policy to use in QRadar.
        3. Create a consumer group.
        4. Copy and save the name to use in the SIEM platform.
        5. Enable continuous export of security alerts to the defined event hub.
        6. Create a storage account.
        7. Copy and save the connection string to the account to use in QRadar.

        For more information about QRadar setup, see [Prepare Azure resources for exporting to Splunk and QRadar](export-to-splunk-or-qradar).
    - If you're streaming alerts to Splunk:

        1. Create an Entra application.
        2. Save the Tenant, App ID, and App password.
        3. Give permissions to the Entra Application to read from the event hub you created before.

        For more information about Splunk setup, see [Prepare Azure resources for exporting to Splunk and QRadar](export-to-splunk-or-qradar).

### Connect the event hub to your preferred solution using the built-in connectors

Each SIEM platform has a tool that enables it to receive alerts from Event Hubs. Install the tool for your platform to start receiving alerts.

| Tool | Hosted in Azure | Description |
| --- | --- | --- |
| IBM QRadar | No | The Microsoft Azure DSM and Microsoft Azure Event Hubs Protocol are available for download from the [IBM QRadar DSM guide for Microsoft Azure platform](https://www.ibm.com/docs/en/qsip/7.4?topic=microsoft-azure-platform). |
| Splunk | No | [Splunk Add-on for Microsoft Cloud Services](https://splunkbase.splunk.com/app/3110/) is an open source project available in Splunkbase.  If you can't install an add-on in your Splunk instance, for example if you're using a proxy or running on Splunk Cloud, you can forward these events to the Splunk HTTP Event Collector using [Azure Function For Splunk](https://github.com/splunk/azure-functions-splunk), which is triggered by new messages in the event hub. |

## Stream alerts with continuous export

To stream alerts into **ArcSight**, **SumoLogic**, **Syslog servers**, **LogRhythm**, **Logz.io Cloud Observability Platform**, **Dynatrace**, and other monitoring solutions, connect Defender for Cloud using continuous export and Azure Event Hubs.

Note

To stream alerts at the tenant level, use this Azure policy and set the scope at the root management group. You need permissions for the root management group as explained in [Defender for Cloud permissions](permissions): [Deploy export to an event hub for Microsoft Defender for Cloud alerts and recommendations](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2fproviders%2fMicrosoft.Authorization%2fpolicyDefinitions%2fcdfcce10-4578-4ecd-9703-530938e4abcb).

**To stream alerts with continuous export**:

1. Enable continuous export:

    - At the [subscription level with continuous export](continuous-export).
    - At the [Management Group level using Azure Policy](continuous-export-azure-policy).
2. Connect the event hub to your preferred solution using the built-in connectors:

    | Tool | Hosted in Azure | Description |
    | --- | --- | --- |
    | SumoLogic | No | Instructions for setting up SumoLogic to consume data from an event hub are available at [Collect Logs for the Azure Audit App from Event Hubs](https://help.sumologic.com/docs/send-data/collect-from-other-data-sources/azure-monitoring/collect-logs-azure-monitor/). |
    | ArcSight | No | The ArcSight Azure Event Hubs smart connector is available as part of [the ArcSight smart connector collection](https://community.microfocus.com/cyberres/arcsight/f/arcsight-product-announcements/163662/announcing-general-availability-of-arcsight-smart-connectors-7-10-0-8114-0). |
    | Syslog server | No | If you want to stream Azure Monitor data directly to a syslog server, you can use a [solution based on an Azure function](https://github.com/miguelangelopereira/azuremonitor2syslog/). |
    | LogRhythm | No | Instructions to set up LogRhythm to collect logs from an event hub are available at [Six tips for securing your Azure cloud environment](https://logrhythm.com/six-tips-for-securing-your-azure-cloud-environment/). |
    | Logz.io | Yes | For more information, see [Getting started with monitoring and logging using Logz.io for Java apps running on Azure](/en-us/azure/developer/java/fundamentals/java-get-started-with-logzio) |
    | Dynatrace | No | For instructions to set up the integration in Dynatrace, read [Ingest Microsoft Defender for Cloud security events](https://dt-url.net/ft03w4b) |
3. (Optional) Stream the raw logs to the event hub and connect to your preferred solution. Learn more in [Monitoring data available](/en-us/azure/azure-monitor/essentials/stream-monitoring-data-event-hubs#monitoring-data-available).

To view the event schemas of the exported data types, visit the [Event Hubs event schemas](https://aka.ms/ASCAutomationSchemas).

## Use the Microsoft Graph Security API to stream alerts to non-Microsoft applications

Defender for Cloud includes a built-in integration with [Microsoft Graph Security API](/en-us/graph/security-concept-overview/) that you can use to stream alerts without any further configuration requirements.

Use this API to stream alerts from your **entire tenant** and data from many Microsoft Security products into non-Microsoft SIEMs and other popular platforms:

- **Splunk Enterprise and Splunk Cloud**: [Use the Microsoft Graph Security API Add-On for Splunk](https://splunkbase.splunk.com/app/4564/).
- **Power BI**: [Connect to the Microsoft Graph Security API in Power BI Desktop](/en-us/power-bi/connect-data/desktop-connect-graph-security).
- **ServiceNow**: [Install and configure the Microsoft Graph Security API application from the ServiceNow Store](https://docs.servicenow.com/bundle/sandiego-security-management/page/product/secops-integration-sir/secops-integration-ms-graph/task/ms-graph-install.html?cshalt=yes).
- **QRadar**: [Use IBM's Device Support Module for Microsoft Defender for Cloud via Microsoft Graph API](https://www.ibm.com/support/knowledgecenter/SS42VS_DSM/com.ibm.dsm.doc/c_dsm_guide_ms_azure_security_center_overview.html).
- **Palo Alto Networks**, **Anomali**, **Lookout**, **InSpark**, and others: [Use the Microsoft Graph Security API](/en-us/graph/security-concept-overview).

Note

The preferred way to export alerts is through [Continuously export Microsoft Defender for Cloud data](continuous-export).