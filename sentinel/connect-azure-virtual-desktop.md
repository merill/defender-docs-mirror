---
layout: Conceptual
title: Connect Azure Virtual Desktop to Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/connect-azure-virtual-desktop
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
description: Connect Azure Virtual Desktop to Microsoft Sentinel to monitor desktop environment activity and security data. Includes guidance for enabling the connector and using the ingested data for monitoring.
ms.author: guywild
author: guywi-ms
ms.reviewer: ofshezaf
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 2ca1fc75-1db4-9b15-141b-e4b22e657632
document_version_independent_id: 838c1881-f874-54de-48b0-23340fbfe1be
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/connect-azure-virtual-desktop.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/connect-azure-virtual-desktop
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/connect-azure-virtual-desktop.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/7814ca69-56be-4667-8a46-86327796c328
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/f15dfcd0-2664-48ba-bb88-f1f86eadbfd1
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: c791b5b5-5374-c5e6-dbdf-74df16844083
---

# Connect Azure Virtual Desktop to Microsoft Sentinel | Microsoft Learn

This article describes how you can monitor your Azure Virtual Desktop environments using Microsoft Sentinel.

For example, monitoring your Azure Virtual Desktop environments can enable you to provide more remote work using virtualized desktops, while maintaining your organization's security posture.

## Azure Virtual Desktop data in Microsoft Sentinel

Azure Virtual Desktop data in Microsoft Sentinel includes the following types:

| Data | Description |
| --- | --- |
| **Windows event logs** | Windows event logs from the Azure Virtual Desktop environment are streamed into a Microsoft Sentinel-enabled Log Analytics workspace in the same manner as Windows event logs from other Windows machines, outside of the Azure Virtual Desktop environment. Install the Azure Monitor Agent onto your Windows machine and configure the Windows event logs to be sent to the Log Analytics workspace.For more information, see:- [Install Azure Monitor Agent on Windows client devices using the client installer](/en-us/azure/azure-monitor/agents/azure-monitor-agent-windows-client)- [Collect Windows events with Azure Monitor Agent](/en-us/azure/azure-monitor/agents/data-collection-windows-events)- [Windows Security Events via AMA connector for Microsoft Sentinel](data-connectors-reference#windows-security-events-via-ama) |
| **Microsoft Defender for Endpoint alerts** | To configure Defender for Endpoint for Azure Virtual Desktop, use the same procedure as you would for any other Windows endpoint. For more information, see: - [Set up Microsoft Defender for Endpoint deployment](/en-us/windows/security/threat-protection/microsoft-defender-atp/production-deployment)- [Connect data from Microsoft Defender XDR to Microsoft Sentinel](connect-microsoft-365-defender) |
| **Azure Virtual Desktop diagnostics** | Azure Virtual Desktop diagnostics is a feature of the Azure Virtual Desktop PaaS service, which logs information whenever someone assigned Azure Virtual Desktop role uses the service. Each log contains information about which Azure Virtual Desktop role was involved in the activity, any error messages that appear during the session, tenant information, and user information. The diagnostics feature creates activity logs for both user and administrative actions. For more information, see [Use Log Analytics for the diagnostics feature in Azure Virtual Desktop](/en-us/azure/virtual-desktop/diagnostics-log-analytics). |

## Connect Azure Virtual Desktop data

To start ingesting Azure Virtual Desktop data into Microsoft Sentinel, use the instructions from the Azure Virtual Desktop documentation.

For more information, see [Push Azure Virtual Desktop data to your Log Analytics workspace](/en-us/azure/virtual-desktop/diagnostics-log-analytics).

## Find your data

After Azure Virtual Desktop data is connected to Microsoft Sentinel, run queries against your Log Analytics data.

For example, see sample queries from the [Azure Virtual Desktop documentation](/en-us/azure/virtual-desktop/diagnostics-log-analytics).

Microsoft Sentinel also provides built-in queries in the **General** &gt; **Logs** &gt; **Azure Virtual Desktop** area:

[![Screenshot showing Azure Virtual Desktop built-in queries in Microsoft Sentinel.](media/connect-windows-virtual-desktop/windows-virtual-desktop-queries.png)](media/connect-windows-virtual-desktop/windows-virtual-desktop-queries.png#lightbox#lightbox)