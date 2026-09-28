---
layout: Conceptual
title: IP address entity page in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/entity-page-ip
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: The IP address entity page in the Microsoft Defender portal helps you in your investigation of IP address entities that appear in incidents and alerts. The page has all the important information about each entity. If an alert or incident indicates that an IP address is the source or target of suspicious behavior, check and investigate the IP address.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- usx-security
ms.topic: concept-article
ms.date: 2026-06-12T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: b7dc85be-dc32-652c-7272-bdb341d436ce
document_version_independent_id: b7dc85be-dc32-652c-7272-bdb341d436ce
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/entity-page-ip.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: entity-page-ip
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/entity-page-ip.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 96da366c-3909-471a-796a-93c0f84c4589
---

# IP address entity page in Microsoft Defender - Microsoft Defender XDR | Microsoft Learn

The IP address entity page in the Microsoft Defender portal helps you examine possible communication between your devices and external internet protocol (IP) addresses.

Identifying all devices in the organization that communicated with a suspected or known malicious IP address, such as Command and Control (C2) servers, helps determine the potential scope of breach, associated files, and infected devices.

You can find information from the following sections in the IP address entity page:

- Overview
- Incidents and alerts
- Observed in organization
- Threat Intelligence Insights
- Sentinel events

Important

Microsoft Sentinel is generally available in the Microsoft Defender portal, with or without Microsoft Defender XDR or an E5 license. For more information, see [Microsoft Sentinel in the Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2263690).

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal.

If you're currently using Microsoft Sentinel in the Azure portal, we recommend that you start planning your transition to the Defender portal now to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview). For more information, see [Transition your Microsoft Sentinel environment to the Defender portal](/en-us/azure/sentinel/move-to-defender) and [Planning your move to Microsoft Defender portal for all Microsoft Sentinel customers](https://techcommunity.microsoft.com/blog/microsoft-security-blog/planning-your-move-to-microsoft-defender-portal-for-all-microsoft-sentinel-custo/4428613) (blog).

## Overview

In the left pane, the **Overview** page provides a summary of IP details (if available).

| Section | Details |
| --- | --- |
| Security info | - Open incidents<br>- Active alerts |
| IP details | - Organization (ISP)<br>- ASN<br>- Country/Region, State, City<br>- Carrier<br>- Latitude and longitude<br>- Postal code |

The left side also has a panel showing Log activity (time first seen/last seen, data source) collected from several log sources, and another panel showing a list of logged hosts collected from Azure Monitoring Agent heartbeat tables.

The main body of the **Overview** page contains dashboard cards showing a count of incidents and alerts (grouped by severity) containing the IP address, and a chart of the prevalence of the IP address in the organization over the indicated time period.

## Incidents and alerts

The **Incidents and alerts** page shows a list of incidents and alerts that include the IP address as part of their story. These incidents and alerts come from any of a number of Microsoft Defender detection sources, including, if onboarded, Microsoft Sentinel. This list is a filtered version of the [incidents queue](incidents-overview), and shows a short description of the incident or alert, its severity (high, medium, low, informational), its status in the queue (new, in progress, resolved), its classification (not set, false alert, true alert), investigation state, category, who is assigned to address it, and last activity observed.

You can customize which columns are displayed for each item. You can also filter the alerts by severity, status, or any other column in the display.

The *impacted assets* column refers to all the user, application, and other entities referenced in the incident or alert.

When an incident or alert is selected, a fly-out appears. From this panel you can manage the incident or alert and view more details such as incident/alert number and related devices. Multiple alerts can be selected at a time.

To see a full page view of an incident or alert, select its title.

## Observed in organization

The **Observed in organization** section provides a list of devices that have a connection with this IP and the last event details for each device (the list is limited to 100 devices).

## Threat Intelligence Insights

The **Threat Intelligence Insights** tab surfaces enrichment data from [Microsoft Threat Intelligence](defender-threat-intelligence) directly on the IP address entity page. These enrichments provide globally observed intelligence to help you assess the risk of an IP address during an investigation.

For a general overview of entity enrichments, see [View threat intelligence in entity pages](entity-page-threat-intelligence).

### Reputation

The reputation section displays a risk assessment for the IP address based on Microsoft's detection rules and intelligence. The reputation score indicates whether the IP address is known to be malicious, suspicious, or benign, helping analysts quickly prioritize their investigation.

### Attributed threat reports

When Microsoft has linked the IP address to a known threat actor or campaign, this section shows related threat analytics reports. These reports provide context about the threat actor's tactics, techniques, and procedures (TTPs).

### Infrastructure relationships

The infrastructure relationships section provides detailed data about the IP address, including:

| Data set | Description |
| --- | --- |
| **DNS records** | Historical and current DNS resolution data associated with the IP address. |
| **WHOIS information** | Registration details for the IP address, including registrant, dates, and registrar. |
| **Host pairs** | Relationships between hosts based on observed connections in web content. |
| **Subdomains** | Known subdomains that resolve to the IP address. |
| **TLS/SSL certificates** | Certificate details including issuer, validity, and subject alternative names. |
| **Services** | Detected network services running on the IP address. |
| **Components** | Web technologies and frameworks identified on the IP address. |
| **Trackers** | Web analytics and tracking codes observed on the IP address. |
| **Cookies** | Cookie names observed in responses from the IP address. |

## Sentinel events

If your organization onboarded Microsoft Sentinel to the Defender portal, this additional tab is on the IP address entity page. This tab imports the [IP entity page from Microsoft Sentinel](/en-us/azure/sentinel/entity-pages).

### Sentinel timeline

This timeline shows alerts associated with the IP address entity. These alerts include those seen on the **Incidents and alerts** tab and those created by Microsoft Sentinel from third-party, non-Microsoft data sources.

This timeline also shows [bookmarked hunts](/en-us/azure/sentinel/bookmarks) from other investigations that reference this IP entity, IP activity events from external data sources, and unusual behaviors detected by Microsoft Sentinel's [anomaly rules](/en-us/azure/sentinel/soc-ml-anomalies).

### Insights

Entity insights are queries defined by Microsoft security researchers to help you investigate more efficiently and effectively. These insights automatically ask the big questions about your IP entity, providing valuable security information in the form of tabular data and charts. The insights include data from various IP threat intelligence sources, network traffic inspection, and more, and include advanced machine learning algorithms to detect anomalous behavior.

The following are some of the insights shown:

- Microsoft Defender Threat Intelligence reputation.
- Virus Total IP Address.
- Recorded Future IP Address.
- Anomali IP Address
- AbuseIPDB.
- Anomalies count by IP address.
- Network traffic inspection.
- IP address remote connections with TI match.
- IP address remote connections.
- This IP has a TI match.
- Watchlist insights (Preview).

The insights are based on the following data sources:

- Syslog (Linux)
- SecurityEvent (Windows)
- AuditLogs (Microsoft Entra ID)
- SigninLogs (Microsoft Entra ID)
- OfficeActivity (Office 365)
- BehaviorAnalytics (Microsoft Sentinel UEBA)
- Heartbeat (Azure Monitor Agent)
- CommonSecurityLog (Microsoft Sentinel)

If you want to further explore any of the insights in this panel, select the link accompanying the insight. The link takes you to the **Advanced hunting** page, where it displays the query underlying the insight, along with its raw results. You can modify the query or drill down into the results to expand your investigation or just satisfy your curiosity.

## Response actions

Response actions offer shortcuts to analyze, investigate, and defend against threats.

Response actions run along the top of a specific IP entity page and include:

| Action | Description |
| --- | --- |
| **Add indicator** | Opens a wizard for you to add this IP address as an Indicator of Compromise (IoC) to your Threat Intelligence knowledgebase. |
| **Open cloud app IP settings** | Opens the IP address ranges configuration screen for you to add the IP address to it. |
| **Investigate in Activity log** | Opens the Microsoft 365 Activity log screen for you to look for the IP address in other logs. |
| **Go hunt** | Opens the **Advanced hunting** page, with a built-in hunting query to find instances of this IP address. |