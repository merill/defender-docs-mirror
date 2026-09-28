---
layout: Conceptual
title: Use the data ingestion benefit in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/data-ingestion-benefit
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
description: Defender for Servers Plan 2 includes 500 MB of free daily data ingestion per node to Log Analytics. Learn how the benefit is calculated and applied.
ms.topic: how-to
ms.custom: msecd-doc-authoring-1013
ms.date: 2026-07-12T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 27e0d128-1678-2064-a0d4-d5d7cec002d2
document_version_independent_id: 574161cc-b2ca-16f7-8573-860f840d81cb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/data-ingestion-benefit.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/data-ingestion-benefit
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/data-ingestion-benefit.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: a0e137e4-1c92-dfe9-79e8-cd14deb1e507
---

# Use the data ingestion benefit in Microsoft Defender for Cloud - Microsoft Defender for Cloud | Microsoft Learn

When you enable Defender for Servers Plan 2 in Microsoft Defender for Cloud, you receive 500 MB of free data ingestion per node daily.

- The total daily data allowance granted equals the number of machines × 500 MB.
- The daily data allowance is calculated across all machines in a subscription, not enforced per machine.
- You aren’t charged for ingestion as long as the total data ingested across all machines in the subscription remains within the daily allowance, even if individual machines ingest more than 500 MB.
- The benefit is applied at the Log Analytics workspace level.
- The benefit doesn't appear on your invoice because it has zero cost. You can see it in the product UI and in Microsoft Cost Management exports. Learn how to [view your data allocation benefits](/en-us/azure/azure-monitor/fundamentals/cost-usage#view-data-allocation-benefits).

## How the data ingestion benefit is applied

The 500 MB/day data ingestion benefit applies when:

- Defender for Servers Plan 2 is enabled on the Log Analytics workspace that your machines report to. The allowance is calculated daily and applies only while Plan 2 is active.
- Eligible security data is ingested into that workspace through Azure Monitor Agent (AMA), the Microsoft Defender for Endpoint sensor, or agentless file integrity monitoring (FIM). Agentless FIM events are reported to the `MDCFileIntegrityMonitoringEvents` table.

No separate configuration is required. The benefit is applied automatically to eligible tables.

Note

The benefit is applied based on the workspace billing model:

- **Microsoft Sentinel classic meters**: Applies to Log Analytics ingestion only.
- **Microsoft Sentinel simplified (unified) meters**: Applies to Microsoft Sentinel ingestion.

### Supported data types

The benefit supports the following security data types. For the full category list, see [Tables in the Security category](/en-us/azure/azure-monitor/reference/tables-category#security).

- [SecurityAlert](/en-us/azure/azure-monitor/reference/tables/securityalert)
- [SecurityBaseline](/en-us/azure/azure-monitor/reference/tables/securitybaseline)
- [SecurityBaselineSummary](/en-us/azure/azure-monitor/reference/tables/securitybaselinesummary)
- [SecurityDetection](/en-us/azure/azure-monitor/reference/tables/securitydetection)
- [SecurityEvent](/en-us/azure/azure-monitor/reference/tables/securityevent)
- [WindowsFirewall](/en-us/azure/azure-monitor/reference/tables/windowsfirewall)
- [ProtectionStatus](/en-us/azure/azure-monitor/reference/tables/protectionstatus)
- [Update](/en-us/azure/azure-monitor/reference/tables/update) and [UpdateSummary](/en-us/azure/azure-monitor/reference/tables/updatesummary) when the Update Management solution isn't running in the workspace or solution targeting is enabled.
- [MDCFileIntegrityMonitoringEvents](/en-us/azure/azure-monitor/reference/tables/mdcfileintegritymonitoringevents)
- [WindowsEvent](/en-us/azure/azure-monitor/reference/tables/windowsevent)
- [DeviceCustomFileEvents](/en-us/azure/azure-monitor/reference/tables/devicecustomfileevents)
- [DeviceCustomRegistryEvents](/en-us/azure/azure-monitor/reference/tables/devicecustomregistryevents)

Note

Although `WindowsEvent` is listed, only security events from the `Microsoft-SecurityEvent` stream that go to the `SecurityEvent` table qualify for the 500 MB/day allowance. Application, System, or other event log channels aren't covered and are billed as regular ingestion.

## Configure a workspace

Follow Azure Monitor instructions to [create a Log Analytics workspace](/en-us/azure/azure-monitor/logs/quick-create-workspace).

## Enable Defender for Servers Plan 2

To get the 500 MB/day data ingestion benefit, enable Defender for Servers Plan 2 on the Log Analytics workspace.

1. Sign into the [Azure portal](https://portal.azure.com).
2. Go to **Microsoft Defender for Cloud**.
3. Select **Environment settings**.
4. Select the Log Analytics workspace that you want to configure.
5. Turn on Defender for Servers Plan 2, and then select **Save**.

    [![Screenshot that shows the plan enablement page at the Log Analytics workspace level.](media/tutorial-enable-servers-plan/enable-workspace-servers.png)](media/tutorial-enable-servers-plan/enable-workspace-servers.png#lightbox)

Note

To disable Defender for Servers Plan 2, turn it off on each Log Analytics workspace where it's enabled.