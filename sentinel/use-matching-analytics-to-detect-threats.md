---
layout: Conceptual
title: Use matching analytics to detect threats - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/use-matching-analytics-to-detect-threats
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
description: This article explains how to detect threats with Microsoft-generated threat intelligence in Microsoft Sentinel.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.collection: usx-security
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: b5db9833-78ef-09a3-acd4-89da46fd92a9
document_version_independent_id: bc88f7cb-3e0f-3006-e9e7-d5dfc61ab8cf
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/use-matching-analytics-to-detect-threats.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/use-matching-analytics-to-detect-threats
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/use-matching-analytics-to-detect-threats.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
platformId: a20b56d0-76cf-3197-fb36-8960278e4d85
---

# Use matching analytics to detect threats - Microsoft Sentinel | Microsoft Learn

Use Microsoft threat intelligence to generate high-fidelity alerts and incidents. Enable the **Microsoft Defender Threat Intelligence Analytics** rule, a built-in rule in Microsoft Sentinel. This rule matches indicators with Common Event Format (CEF) logs, Windows DNS events, syslog data, and more. It checks for domain and IPv4 threat indicators across these data sources.

## Prerequisites

Install one or more supported data connectors. You don't need a premium Microsoft Defender Threat Intelligence license. To connect your data sources, install the right solutions from the **Content hub**. The following data sources are supported:

- Common Event Format (CEF) via Legacy Agent
- Windows DNS via Legacy Agent (Preview)
- Syslog via Legacy Agent
- Microsoft 365 (formerly, Office 365)
- Azure activity logs
- Windows DNS via AMA
- Advanced Security Information Model (ASIM) Network sessions

![A screenshot that shows the Microsoft Defender Threat Intelligence Analytics rule data source connections.](media/use-matching-analytics-to-detect-threats/matching-analytics-template-ga.png)

For example, depending on your data source, you might use the following solutions and data connectors:

| Solution | Data connector |
| --- | --- |
| [Common Event Format solution for Sentinel](https://azuremarketplace.microsoft.com/marketplace/apps/azuresentinel.azure-sentinel-solution-commoneventformat?tab=Overview) | [Common Event Format connector for Microsoft Sentinel](data-connectors-reference#syslog-and-common-event-format-cef-connectors) |
| [Windows Server DNS](https://azuremarketplace.microsoft.com/marketplace/apps/azuresentinel.azure-sentinel-solution-dns?tab=Overview) | [DNS connector for Microsoft Sentinel](connect-dns-ama) |
| [Syslog solution for Sentinel](https://azuremarketplace.microsoft.com/marketplace/apps/azuresentinel.azure-sentinel-solution-syslog?tab=Overview) | [Syslog connector for Microsoft Sentinel](cef-syslog-ama-overview) |
| [Microsoft 365 solution for Sentinel](https://azuremarketplace.microsoft.com/marketplace/apps/azuresentinel.azure-sentinel-solution-office365?tab=Overview) | [Office 365 connector for Microsoft Sentinel](data-connectors-reference#microsoft-365-formerly-office-365) |
| [Azure Activity solution for Sentinel](https://azuremarketplace.microsoft.com/marketplace/apps/azuresentinel.azure-sentinel-solution-azureactivity?tab=Overview) | [Azure Activity connector for Microsoft Sentinel](data-connectors-reference#azure-activity) |
| [Windows Firewall](https://azuremarketplace.microsoft.com/marketplace/apps/azuresentinel.azure-sentinel-solution-windowsfirewall?tab=Overview) | [Windows Firewall Events via AMA connector](data-connectors-reference#windows-firewall-events-via-ama) |

## Configure the matching analytics rule

Matching analytics is configured when you enable the **Microsoft Defender Threat Intelligence Analytics** rule.

Important

Before you enable this rule, install at least one supported data connector and its corresponding Content hub solution. See Prerequisites for the full list of supported data sources.

1. Under the **Configuration** section, select the **Analytics** menu.
2. Select the **Rule templates** tab.
3. In the search window, enter **threat intelligence**.
4. Select the **Microsoft Defender Threat Intelligence Analytics** rule template.
5. Select **Create rule**. The rule details are read only, and the default status of the rule is enabled.
6. Select **Review** &gt; **Create**.

[![Screenshot that shows the Microsoft Defender Threat Intelligence Analytics rule enabled on the Active rules tab.](media/use-matching-analytics-to-detect-threats/configure-matching-analytics-rule.png)](media/use-matching-analytics-to-detect-threats/configure-matching-analytics-rule.png#lightbox)

## Review supported data sources and indicators

Microsoft Defender Threat Intelligence Analytics matches your logs with domain, IP, and URL indicators in the following ways:

- **CEF logs** ingested into the Log Analytics `CommonSecurityLog` table match URL and domain indicators if populated in the `RequestURL` field, and IPv4 indicators in the `DestinationIP` field.
- **Windows DNS logs**, where `SubType == "LookupQuery"` ingested into the `DnsEvents` table matches domain indicators populated in the `Name` field, and IPv4 indicators in the `IPAddresses` field.
- **Syslog events**, where `Facility == "cron"` ingested into the `Syslog` table matches domain and IPv4 indicators directly from the `SyslogMessage` field.
- **Office activity logs** ingested into the `OfficeActivity` table match IPv4 indicators directly from the `ClientIP` field.
- **Azure activity logs** ingested into the `AzureActivity` table match IPv4 indicators directly from the `CallerIpAddress` field.
- **ASIM DNS logs** ingested into the `ASimDnsActivityLogs` table match domain indicators if populated in the `DnsQuery` field, and IPv4 indicators in the `DnsResponseName` field.
- **ASIM Network Sessions** ingested into the `ASimNetworkSessionLogs` table match IPv4 indicators if populated in one or more of the following fields: `DstIpAddr`, `DstNatIpAddr`, `SrcNatIpAddr`, `SrcIpAddr`, `DvcIpAddr`.

## Triage an incident generated by matching analytics

If the **Microsoft Defender Threat Intelligence Analytics** rule finds a match, any alerts generated are grouped into incidents.

Use the following steps to triage through the incidents generated by the **Microsoft Defender Threat Intelligence Analytics** rule:

1. In the Microsoft Sentinel workspace where you enabled the **Microsoft Defender Threat Intelligence Analytics** rule, select **Incidents**, and search for *Microsoft Defender Threat Intelligence Analytics*.

    Any incidents that are found appear in the grid.
2. Select **View full details** to view entities and other details about the incident, such as specific alerts.

    Here's an example.

    ![Screenshot of incident generated by matching analytics with details pane.](media/use-matching-analytics-to-detect-threats/matching-analytics.png)
3. Check the severity of the alerts and the incident. Alert severity ranges from `Informational` to `High` based on how the indicator is matched. For example, an indicator matched with firewall logs that allowed traffic produces a high-severity alert. The same indicator matched with firewall logs that blocked traffic produces a low or medium alert.

    Alerts are grouped by the indicator they match. For example, all alerts in a 24-hour period that match the `contoso.com` domain are grouped into one incident. The incident severity is based on the highest alert severity.
4. Observe the indicator information. When a match is found, the indicator is published to the Log Analytics `ThreatIntelligenceIndicators` table, and it appears on the **Threat Intelligence** page. For any indicators published from this rule, the source is defined as `Microsoft Threat Intelligence Analytics`.

Here's an example of the `ThreatIntelligenceIndicators` table.

[![Screenshot that shows the ThreatIntelligenceIndicator table showing indicator with SourceSystem of Microsoft Threat Intelligence Analytics.](media/use-matching-analytics-to-detect-threats/matching-analytics-logs.png)](media/use-matching-analytics-to-detect-threats/matching-analytics-logs.png#lightbox)

Here's an example of searching for the indicators in the management interface.

[![Screenshot that shows the Threat Intelligence overview with indicator selected showing the source as Microsoft Threat Intelligence Analytics.](media/use-matching-analytics-to-detect-threats/matching-analytics-threat-intelligence.png)](media/use-matching-analytics-to-detect-threats/matching-analytics-threat-intelligence.png#lightbox)

## Get more context from Microsoft Defender Threat Intelligence

Some Microsoft Defender Threat Intelligence indicators also include a link to a related Intel Explorer article. Use this link to get more details about the indicator.

![Screenshot that shows an incident with a link to the Microsoft Defender Threat Intelligence reference article.](media/use-matching-analytics-to-detect-threats/mdti-article-link.png)

For more information, see [Threat analytics in Microsoft Defender XDR](/en-us/defender-xdr/threat-analytics).