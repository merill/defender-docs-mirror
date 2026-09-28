---
layout: Conceptual
title: Prioritize incidents in the Microsoft Defender portal (Legacy) - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/incident-queue
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to prioritize and filter incidents in the Microsoft Defender portal to improve your organization's security response. Discover actionable steps to manage incidents effectively.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- usx-security
- tier1
ms.custom: admindeeplinkDEFENDER
ms.topic: concept-article
ms.date: 2025-10-26T00:00:00.0000000Z
locale: en-us
document_id: 8128cc6e-dff1-8376-d819-59dd1bd2d370
document_version_independent_id: 8128cc6e-dff1-8376-d819-59dd1bd2d370
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/incident-queue.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: incident-queue
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/incident-queue.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 7d045be4-c00f-59d9-1e96-4f209b86c289
---

# Prioritize incidents in the Microsoft Defender portal (Legacy) - Microsoft Defender XDR | Microsoft Learn

Note

This article describes the legacy incident experience in the Microsoft Defender portal. Incident cases are in preview and are the recommended experience for managing incidents. The legacy incident experience remains available during this preview. For the recommended incident case experience, see [Prioritize incident cases in the Microsoft Defender portal](prioritize-incident-cases).

The Microsoft Defender portal applies correlation analytics and aggregates related alerts and automated investigations from different products into an incident. Microsoft Sentinel and Defender also trigger unique alerts on activities that can only be identified as malicious given the end-to-end visibility in the unified platform across the entire suite of products. This view gives your security analysts the broader attack story, which helps them better understand and deal with complex threats across your organization.

Important

Microsoft Sentinel is generally available in the Microsoft Defender portal, with or without Microsoft Defender XDR or an E5 license. For more information, see [Microsoft Sentinel in the Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2263690).

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal.

If you're currently using Microsoft Sentinel in the Azure portal, we recommend that you start planning your transition to the Defender portal now to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview). For more information, see [Transition your Microsoft Sentinel environment to the Defender portal](/en-us/azure/sentinel/move-to-defender) and [Planning your move to Microsoft Defender portal for all Microsoft Sentinel customers](https://techcommunity.microsoft.com/blog/microsoft-security-blog/planning-your-move-to-microsoft-defender-portal-for-all-microsoft-sentinel-custo/4428613) (blog).

## Incident queue

The **Incident queue** shows a queue of incidents that were created across devices, users, mailboxes, and other resources. It helps you triage the incidents, prioritize and create an informed cybersecurity response decision.

Find the incident queue at **Incidents & alerts &gt; Incidents** on the quick launch of the [Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2077139).

Select **Most recent incidents and alerts** to toggle a timeline chart of the number of alerts received and incidents created in the last 24 hours.

[![Screenshot of 24-hour incident graph.](media/incidents-queue/most-recent-incidents.png)](media/incidents-queue/most-recent-incidents.png#lightbox)

The incident queue includes Defender Queue Assistant that helps security teams cut through the large number of incidents and focus on the incidents that matter most. Using a machine learning prioritization algorithm, the Queue Assistant surfaces the highest-priority incidents, explains the reasoning behind the prioritization, and provides intuitive tools for sorting and filtering the incident queue. The algorithm runs for all alerts, Microsoft native alerts, custom detections, or third-party signals. The algorithm is trained on real-world anonymized data and considers, among other things, the following data points when calculating the priority score:

- Attack disruption signals
- Threat analytics
- Severity
- SnR
- MITRE techniques
- Asset criticality
- Alert types and rarity
- High profile threats such as ransomware and nation-state attacks.

Incidents are automatically assigned a priority score from 0 to 100, with 100 being the highest priority. Score ranges are color-coded as follows:

- Red: Top priority (score &gt; 85)
- Orange: Medium priority (15–85)
- Gray: Low priority (&lt;15)

[![Screenshot of the Incidents queue in the Microsoft Defender portal.](media/incidents-queue/incidents-page.png)](media/incidents-queue/incidents-page.png#lightbox)

Select the incident row anywhere except the incident name, to display a summary pane with key information about the incident. The pane includes the priority assessment, the factors influencing the priority score, the incident's details, recommended actions, and related threats. Use the up and down arrows at the top of the pane to navigate to the previous or next incident in the incident queue. For more information on investigating the incident, see [Investigate incidents](investigate-incidents).

[![Selecting an incident in the Microsoft Defender portal](media/investigate-incidents/incident-side-panel.png)](media/investigate-incidents/incident-side-panel.png#lightbox)

By default, the incident queue show incidents created in the last week. Choose a different time frame by selecting time selector drop-down above the queue.

[![Screenshot of the time selector for the incident queue.](media/incidents-queue/time-selector.png)](media/incidents-queue/time-selector.png#lightbox)

The **total number of incidents** in the queue is displayed next to the time selector. The number of incidents varies depending on the filters in use. You can search for incidents by name or incident ID

Select **Customize columns** to select columns displayed in the queue. Check or uncheck the columns you want to see in the incident queue. Arrange the order of the columns by dragging them up and down.

[![Screenshot of Incident page filter and column controls.](media/incidents-queue/incident-toolbar.png)](media/incidents-queue/incident-toolbar.png#lightbox)

The **Export** button allows you to export the filtered data in the incident queue to a CSV file. The maximum number of records you can export to a CSV file is 10,000.

### Incident names

For more visibility at a glance, Microsoft Defender generates incident names automatically, based on alert attributes such as the number of endpoints affected, users affected, detection sources, or categories. This specific naming allows you to quickly understand the scope of the incident.

For example: *Multi-stage incident on multiple endpoints reported by multiple sources.*

If you onboarded Microsoft Sentinel to the Defender portal, then any alerts and incidents coming from Microsoft Sentinel are likely to have their names changed (regardless of whether they were created before or since the onboarding).

We recommend that you avoid using the incident name as a condition for triggering [automation rules](/en-us/azure/sentinel/automate-incident-handling-with-automation-rules). If the incident name is a condition, and the incident name changes, the rule will not be triggered.

## Filters

The incident queue also provides multiple filtering options, that when applied, enable you to perform a broad sweep of all existing incidents in your environment, or decide to focus on a specific scenario or threat. Applying filters on the incident queue can help determine which incident requires immediate attention.

[![The incident queue filters list.](media/incidents-queue/incidents-filter-bar.png)](media/incidents-queue/incidents-filter-bar.png#lightbox)

The **Filters** list above the incident queue shows the current filters currently applied to the queue. Select **Add filter** to apply more filters to limit the set of incidents shown.

[![The Filters pane for the incident queue in the Microsoft Defender portal.](media/incidents-queue/incident-filters-small.png)](media/incidents-queue/incident-filters.png#lightbox)

Select the filters you want to use, then select **Add**. The selected filters are shown along with the existing applied filters. Select the new filter to specify its conditions. For example, if you chose the "Service/detection sources" filter, select it to choose the sources by which to filter the list.

You can remove a filter by selecting the **X** on the filter name in the filters list.

The following table lists the available filters.

| Filter name | Description/Conditions |
| --- | --- |
| **Status** | Select **New**, **In progress**, or **Resolved**. |
| **Alert severityIncident severity** | The severity of an alert or incident is indicative of the impact it can have on your assets. The higher the severity, the bigger the impact and typically requires the most immediate attention. Select **High**, **Medium**, **Low**, or **Informational**. |
| **Incident assignment** | Select the assigned user or users. |
| **Multiple service sources** | Specify whether the filter is for more than one service source. |
| **Service/detection sources** | Specify incidents that contain alerts from one or more of the following:- Microsoft Defender for Identity<br>- Microsoft Defender for Cloud Apps<br>- Microsoft Defender for Endpoint<br>- Microsoft Defender XDR<br>- Microsoft Defender for Office 365<br>- App Governance<br>- Microsoft Entra ID Protection<br>- Microsoft Data Loss Prevention<br>- Microsoft Defender for Cloud<br>- Microsoft Sentinel<br>- Microsoft Purview Insider Risk ManagementMany of these services can be expanded in the menu to reveal further choices of detection sources within a given service. |
| **Tags** | Select one or multiple tag names from the list. |
| **Multiple category** | Specify whether the filter is for more than one category. |
| **Categories** | Choose categories to focus on specific tactics, techniques, or attack components seen. |
| **Entities** | Specify the name of an asset such as a user, device, mailbox, or application name. |
| **Sensitivity label** | Filter incidents based on the sensitivity label applied on the data. Some attacks focus on exfiltrating sensitive or valuable data. By applying a filter for specific sensitivity labels, you can quickly determine if sensitive information is potentially compromised and prioritize addressing those incidents. |
| **Device groups** | Specify a [device group](/en-us/windows/security/threat-protection/microsoft-defender-atp/machine-groups) name. |
| **OS platform** | Specify device operating systems. |
| **Classification** | Specify the set of classifications of the related alerts. |
| **Automated investigation state** | Specify the status of automated investigation. |
| **Associated threat** | Specify a named threat. |
| **Policy/policy rule** | Filter incidents based on policy or policy rule. |
| **Product names** | Filter incidents based on product name. |
| **Data stream** | Filter incidents based on the location or workload. |

Note

If you have provisioned access to Microsoft Purview Insider Risk Management, you can view and manage insider risk management alerts and hunt for insider risk management events in the Microsoft Defender portal. For more information, see [Investigate insider risk threats in the Microsoft Defender portal](irm-investigate-alerts-defender).

The default filter is to show all alerts and incidents with a status of **New** and **In progress** and with a severity of **High**, **Medium**, or **Low**.

You can also create filter sets within the incidents page by selecting **Saved filter queries &gt; Create filter set**. If no filter sets have been created, select **Save** to create one.

[![The create filter sets option for the incident queue in the Microsoft Defender portal.](media/incidents-queue/fig2-newfilters.png)](media/incidents-queue/fig2-newfilters.png#lightbox)

Note

Microsoft Defender XDR customers can now filter incidents with alerts where a compromised device communicated with operational technology (OT) devices connected to the enterprise network through the [device discovery integration of Microsoft Defender for IoT and Microsoft Defender for Endpoint](/en-us/defender-endpoint/device-discovery#device-discovery-integration). To filter these incidents, select **Any** in the Service/detection sources, then select **Microsoft Defender for IoT** in the Product name or see [Investigate incidents and alerts in Microsoft Defender for IoT in the Defender portal](/en-us/defender-for-iot/investigate-threats/). You can also use device groups to filter for site-specific alerts. For more information about Defender for IoT prerequisites, see [Get started with enterprise IoT monitoring in Microsoft Defender XDR](/en-us/azure/defender-for-iot/organizations/eiot-defender-for-endpoint/).

### Save custom filters as URLs

Once you've configured a useful filter in the incidents queue, you can bookmark the URL of the browser tab or otherwise save it as a link on a Web page, a Word document, or a place of your choice. Bookmarking gives you single-click access to key views of the incident queue, such as:

- New incidents
- High-severity incidents
- Unassigned incidents
- High-severity, unassigned incidents
- Incidents assigned to me
- Incidents assigned to me and for Microsoft Defender for Endpoint
- Incidents with a specific tag or tags
- Incidents with a specific threat category
- Incidents with a specific associated threat
- Incidents with a specific actor

Once you have compiled and stored your list of useful filter views as URLs, use it to quickly process and prioritize the incidents in your queue and [manage](manage-incidents) them for subsequent assignment and analysis.

## Search

From the **Search for name or ID** box above the list of incidents, you can search for incidents in a number of ways, to quickly find what you're looking for.

### Search by incident name or ID

Search directly for an incident by typing the incident ID or the incident name. When you select an incident from the list of search results, the Microsoft Defender portal opens a new tab with the properties of the incident, from which you can start your [investigation](investigate-incidents).

### Search by impacted assets

You can name an asset—such as a user, device, mailbox, application name, or cloud resource—and find all the incidents related to that asset.

## Specify a time range

The default list of incidents is for those that occurred in the last week. You can specify a new time range from the drop-down box next to the calendar icon by selecting:

- One day
- Three days
- One week
- 30 days
- Six months
- A custom range in which you can specify both dates and times