---
layout: Conceptual
title: Deploying Microsoft Sentinel side-by-side to an existing SIEM. | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/deploy-side-by-side
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
description: Learn how to deploy Microsoft Sentinel side-by-side to an existing SIEM.
ms.author: edbaynash
author: EdB-MSFT
ms.reviewer: abhiag
ms.topic: concept-article
ms.date: 2024-07-24T00:00:00.0000000Z
locale: en-us
document_id: 2766d708-6f4f-5b2f-eddb-9b6411dc6ad8
document_version_independent_id: 1b6f5858-fde2-965a-f2ca-b1bcc655df62
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/deploy-side-by-side.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/deploy-side-by-side
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/deploy-side-by-side.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 23472405-81ef-4db3-e783-d741970fb2af
---

# Deploying Microsoft Sentinel side-by-side to an existing SIEM. | Microsoft Learn

Your security operations center (SOC) team uses centralized security information and event management (SIEM) and security orchestration, automation, and response (SOAR) solutions to protect your increasingly decentralized digital estate.

This article describes the approach and methods to consider when deploying Microsoft Sentinel in a side-by-side configuration together with your existing SIEM.

## Side-by-side approach

Use a side-by-side architecture either as a short-term, transitional phase that leads to a cloud-hosted SIEM, or as a medium- to long-term operational model, depending on the SIEM needs of your organization.

For example, while the recommended architecture is to use a side-by-side architecture just long enough to complete a migration to Microsoft Sentinel, your organization might want to stay with your side-by-side configuration for longer, such as if you aren't ready to move away from your legacy SIEM. Typically, organizations who use a long-term, side-by-side configuration use Microsoft Sentinel to analyze only their cloud data. Many organizations avoid running multiple on-premises analytics solutions because of cost and complexity.

Microsoft Sentinel provides [pay-as-you-go pricing](billing) and flexible infrastructure, giving SOC teams time to adapt to the change. Deploy and test your content at a pace that works best for your organization, and learn about how to [fully migrate to Microsoft Sentinel](migration).

Consider the pros and cons for each approach when deciding which one to use.

### Short-term approach

The following table describes the pros and cons of using a side-by-side architecture for a relatively short period of time.

| **Pros** | **Cons** |
| --- | --- |
| • Gives SOC staff time to adapt to new processes as you deploy workloads and analytics.• Gains deep correlation across all data sources for hunting scenarios.• Eliminates having to do analytics between SIEMs, create forwarding rules, and close investigations in two places.• Enables your SOC team to quickly downgrade legacy SIEM solutions, eliminating infrastructure and licensing costs. | • Can require a steep learning curve for SOC staff. |

### Medium- to long-term approach

The following table describes the pros and cons of using a side-by-side architecture for a relatively medium or longer period of time.

| **Pros** | **Cons** |
| --- | --- |
| • Lets you use key Microsoft Sentinel benefits, like AI, ML, and investigation capabilities, without moving completely away from your legacy SIEM.• Saves money compared to your legacy SIEM, by analyzing cloud or Microsoft data in Microsoft Sentinel. | • Increases complexity by separating analytics across different databases.• Splits case management and investigations for multi-environment incidents.• Incurs greater staff and infrastructure costs.• Requires SOC staff to be knowledgeable about two different SIEM solutions. |

## Side-by-side method

Determine how you'll configure and use Microsoft Sentinel side-by-side with your legacy SIEM.

### Method 1: Send alerts from a legacy SIEM to Microsoft Sentinel (Recommended)

Send alerts, or indicators of anomalous activity, from your legacy SIEM to Microsoft Sentinel.

- Ingest and analyze cloud data in Microsoft Sentinel
- Use your legacy SIEM to analyze on-premises data and generate alerts.
- Forward the alerts from your on-premises SIEM into Microsoft Sentinel to establish a single interface.

For example, forward alerts using [Logstash](connect-logstash-data-connection-rules), [APIs](/en-us/rest/api/securityinsights/), or [Syslog](connect-cef-syslog-ama), and store them in [JSON](https://techcommunity.microsoft.com/t5/azure-sentinel/tip-easily-use-json-fields-in-sentinel/ba-p/768747) format in your Microsoft Sentinel Log Analytics workspace.

By sending alerts from your legacy SIEM to Microsoft Sentinel, your team can cross-correlate and investigate those alerts in Microsoft Sentinel. The team can still access the legacy SIEM for deeper investigation if needed. Meanwhile, you can continue deploying data sources over an extended transition period.

This recommended, side-by-side deployment method provides you with full value from Microsoft Sentinel and the ability to deploy data sources at the pace that's right for your organization. This approach avoids duplicating costs for data storage and ingestion while you move your data sources over.

For more information, see:

- [Migrate QRadar offenses to Microsoft Sentinel](https://techcommunity.microsoft.com/t5/azure-sentinel/migrating-qradar-offenses-to-azure-sentinel/ba-p/2102043)
- [Export data from Splunk to Microsoft Sentinel](https://techcommunity.microsoft.com/t5/azure-sentinel/how-to-export-data-from-splunk-to-azure-sentinel/ba-p/1891237).

If you want to fully migrate to Microsoft Sentinel, review the full [migration guide](migration).

### Method 2: Send alerts and enriched incidents from Microsoft Sentinel to a legacy SIEM

Analyze some data in Microsoft Sentinel, such as cloud data, and then send the generated alerts to a legacy SIEM. Use the *legacy* SIEM as your single interface to do cross-correlation with the alerts that Microsoft Sentinel generated. You can still use Microsoft Sentinel for deeper investigation of the Microsoft Sentinel-generated alerts.

This configuration is cost effective, as you can move your cloud data analysis to Microsoft Sentinel without duplicating costs or paying for data twice. You still have the freedom to migrate at your own pace. As you continue to shift data sources and detections over to Microsoft Sentinel, it becomes easier to migrate to Microsoft Sentinel as your primary interface. However, simply forwarding enriched incidents to a legacy SIEM limits the value you get from Microsoft Sentinel's investigation, hunting, and automation capabilities.

For more information, see:

- [Send enriched Microsoft Sentinel alerts to your legacy SIEM](https://techcommunity.microsoft.com/t5/azure-sentinel/sending-enriched-azure-sentinel-alerts-to-3rd-party-siem-and/ba-p/1456976)
- [Send enriched Microsoft Sentinel alerts to IBM QRadar](https://techcommunity.microsoft.com/t5/azure-sentinel/azure-sentinel-side-by-side-with-qradar/ba-p/1488333)
- [Ingest Microsoft Sentinel alerts into Splunk](https://techcommunity.microsoft.com/t5/azure-sentinel/azure-sentinel-side-by-side-with-splunk/ba-p/1211266)

### Other methods

The following table describes side-by-side configurations that are *not* recommended, with details as to why:

| Method | Description |
| --- | --- |
| **Send Microsoft Sentinel logs to your legacy SIEM** | With this method, you'll continue to experience the cost and scale challenges of your on-premises SIEM. You'll pay for data ingestion in Microsoft Sentinel, along with storage costs in your legacy SIEM, and you can't take advantage of Microsoft Sentinel's SIEM and SOAR detections, analytics, User Entity Behavior Analytics (UEBA), AI, or investigation and automation tools. |
| **Send logs from a legacy SIEM to Microsoft Sentinel** | While this method provides you with the full functionality of Microsoft Sentinel, your organization still pays for two different data ingestion sources. Besides adding architectural complexity, this model can result in higher costs. |
| **Use Microsoft Sentinel and your legacy SIEM as two fully separate solutions** | You could use Microsoft Sentinel to analyze some data sources, like your cloud data, and continue to use your on-premises SIEM for other sources. This setup allows for clear boundaries for when to use each solution, and avoids duplication of costs. However, cross-correlation becomes difficult, and you can't fully diagnose attacks that cross both sets of data sources. In today's landscape, where threats often move laterally across an organization, such visibility gaps can pose significant security risks. |

## Streamline processes by using automation

Use automated workflows to group and prioritize alerts into a common incident, and modify its priority.

For more information, see:

- [Automation in Microsoft Sentinel: Security orchestration, automation, and response (SOAR)](automation/automation)
- [Automate threat response with playbooks in Microsoft Sentinel](automate-responses-with-playbooks)
- [Automate incident handling in Microsoft Sentinel with automation rules](automate-incident-handling-with-automation-rules)