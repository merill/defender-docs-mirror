---
layout: Conceptual
title: Connect Microsoft Defender for IoT with Microsoft Sentinel - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/iot-solution
breadcrumb_path: ../breadcrumb/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-iot-blog/bg-p/MicrosoftDefenderIoTBlog
feedback_help_link_type: ask-the-community
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
ms.service: defender-for-iot
author: limwainstein
manager: bagol
ms.author: lwainstein
description: This tutorial describes how to integrate Microsoft Sentinel and Microsoft Defender for IoT with the Microsoft Sentinel data connector to secure your entire environment. Detect and respond to threats, including multistage attacks that may cross IT and OT boundaries.
ms.topic: tutorial
ms.date: 2022-06-20T00:00:00.0000000Z
ms.custom: enterprise-iot
ms.subservice: sentinel-integration
locale: en-us
document_id: 9dc1b8ae-4872-e043-217e-f9b18d3012f2
document_version_independent_id: 20daebdd-e1fa-e0a1-e98c-b196cf94f9b5
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/iot-solution.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/iot-solution
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/iot-solution.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: ce1a83b1-6625-f2f4-a886-42bbad34fd75
---

# Connect Microsoft Defender for IoT with Microsoft Sentinel - Microsoft Defender for IoT | Microsoft Learn

​Microsoft Defender for IoT enables you to secure your entire OT and Enterprise IoT environment, whether you need to protect existing devices or build security into new innovations.

Microsoft Sentinel and Microsoft Defender for IoT help to bridge the gap between IT and OT security challenges, and to empower SOC teams with out-of-the-box capabilities to efficiently and effectively detect and respond to security threats. The integration between Microsoft Defender for IoT and Microsoft Sentinel helps organizations to quickly detect multistage attacks, which often cross IT and OT boundaries.

This connector allows you to stream Microsoft Defender for IoT data into Microsoft Sentinel, so you can view, analyze, and respond to Defender for IoT alerts, and the incidents they generate, in a broader organizational threat context.

In this tutorial, you will learn how to:

- Connect Defender for IoT data to Microsoft Sentinel
- Use Log Analytics to query Defender for IoT alert data

## Prerequisites

Before you start, make sure you have the following requirements on your workspace:

- **Read** and **Write** permissions on your Microsoft Sentinel workspace. For more information, see [Permissions in Microsoft Sentinel](/en-us/azure/sentinel/roles).
- **Contributor** or **Owner** permissions on the subscription you want to connect to Microsoft Sentinel.
- A Defender for IoT plan on your Azure subscription with data streaming into Defender for IoT. For more information, see [Quickstart: Get started with Defender for IoT](getting-started).

## Connect your data from Defender for IoT to Microsoft Sentinel

Start by enabling the [Defender for IoT data connector](/en-us/azure/sentinel/data-connectors-reference#microsoft-defender-for-iot) to stream all your Defender for IoT events into Microsoft Sentinel.

**To enable the Defender for IoT data connector**:

1. In Microsoft Sentinel, under **Configuration**, select **Data connectors**, and then locate the **Microsoft Defender for IoT** data connector.
2. At the bottom right, select **Open connector page**.
3. On the **Instructions** tab, under **Configuration**, select **Connect** for each subscription whose alerts and device alerts you want to stream into Microsoft Sentinel.

    If you've made any connection changes, it can take 10 seconds or more for the **Subscription** list to update.

For more information, see [Connect Microsoft Sentinel to Azure, Windows, Microsoft, and Amazon services](/en-us/azure/sentinel/connect-azure-windows-microsoft-services).

## View Defender for IoT alerts

After you've connected a subscription to Microsoft Sentinel, you'll be able to view Defender for IoT alerts in the Microsoft Sentinel **Logs** area.

1. In Microsoft Sentinel, select **Logs &gt; AzureSecurityOfThings &gt; SecurityAlert**, or search for **SecurityAlert**.
2. Use the following sample queries to filter the logs and view alerts generated by Defender for IoT:

    **To see all alerts generated by Defender for IoT**:

    ```kusto
    SecurityAlert | where ProviderName == "IoTSecurity"
    ```

    **To see specific sensor alerts generated by Defender for IoT**:

    ```kusto
    SecurityAlert
    | where ProviderName == "IoTSecurity"
    | where tostring(parse_json(ExtendedProperties).SensorId) == “<sensor_name>”
    ```

    **To see specific OT engine alerts generated by Defender for IoT**:

    ```kusto
    SecurityAlert
    | where ProviderName == "IoTSecurity"
    | where ProductComponentName == "MALWARE"
    
    SecurityAlert
    | where ProviderName == "IoTSecurity"
    | where ProductComponentName == "ANOMALY"
    
    SecurityAlert
    | where ProviderName == "IoTSecurity"
    | where ProductComponentName == "PROTOCOL_VIOLATION"
    
    SecurityAlert
    | where ProviderName == "IoTSecurity"
    | where ProductComponentName == "POLICY_VIOLATION"
    
    SecurityAlert
    | where ProviderName == "IoTSecurity"
    | where ProductComponentName == "OPERATIONAL"
    ```

    **To see high severity alerts generated by Defender for IoT**:

    ```kusto
    SecurityAlert
    | where ProviderName == "IoTSecurity"
    | where AlertSeverity == "High"
    ```

    **To see specific protocol alerts generated by Defender for IoT**:

    ```kusto
    SecurityAlert
    | where PProviderName == "IoTSecurity"
    | where tostring(parse_json(ExtendedProperties).Protocol) == "<protocol_name>"
    ```

Note

The **Logs** page in Microsoft Sentinel is based on Azure Monitor's Log Analytics.

For more information, see [Log queries overview](/en-us/azure/azure-monitor/logs/log-query-overview) in the Azure Monitor documentation and the [Write your first KQL query](/en-us/training/modules/write-first-query-kusto-query-language/) Learn module.

### Understand alert timestamps

Defender for IoT alerts, in both the Azure portal and on the sensor console, track the time an alert was first detected, last detected, and last changed.

The following table describes the Defender for IoT alert timestamp fields, with a mapping to the relevant fields from Log Analytics shown in Microsoft Sentinel.

| Defender for IoT field | Description | Log Analytics field |
| --- | --- | --- |
| **First detection** | Defines the first time the alert was detected in the network. | `StartTime` |
| **Last detection** | Defines the last time the alert was detected in the network, and replaces the **Detection time** column. | `EndTime` |
| **Last activity** | Defines the last time the alert was changed, including manual updates for severity or status, or automated changes for device updates or device/alert de-duplication | `TimeGenerated` |

In Defender for IoT on the Azure portal and the sensor console, the **Last detection** column is shown by default. Edit the columns on the **Alerts** page to show the **First detection** and **Last activity** columns as needed.

For more information, see [View alerts on the Defender for IoT portal](how-to-manage-cloud-alerts) and [View alerts on your sensor](how-to-view-alerts).

### Understand multiple records per alert

Defender for IoT alert data is streamed to the Microsoft Sentinel and stored in your Log Analytics workspace, in the [SecurityAlert](/en-us/azure/sentinel/security-alert-schema) table.

Records in the **SecurityAlert** table are created each time an alert is generated or updated in Defender for IoT. Sometimes a single alert will have multiple records, such as when the alert was first created and then again when it was updated.

In Microsoft Sentinel, use the following query to check the records added to the **SecurityAlert** table for a single alert:

```kql
SecurityAlert
|  where ProviderName == "IoTSecurity"
|  where VendorOriginalId == "<Defender for IoT Alert ID>"
| sort by TimeGenerated desc
```

Updates for alert status or severity generate new records in the **SecurityAlert** table immediately.

Other types of updates are aggregated across up to 12 hours, and new records in the **SecurityAlert** table reflect only the latest change. Examples of aggregated updates include:

- Updates in the last detection time, such as when the same alert is detected multiple times
- A new device is added to an existing alert
- The device properties for an alert are updated