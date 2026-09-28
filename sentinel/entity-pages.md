---
layout: Conceptual
title: Entity pages in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/entity-pages
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
description: Entity pages display information about entities surfaced in your alerts, or that you otherwise come across in your incident investigations. Among this information is the timeline of alerts involving the entity, and curated insights into entity activities. Entity pages provide a rich foundation and context for your investigations, helping you detect, analyze, mitigate, and respond to security threats.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: concept-article
ms.date: 2024-10-16T00:00:00.0000000Z
ms.collection: usx-security
ms.custom: sfi-image-nochange
locale: en-us
document_id: 757fbf03-03ab-eb48-7bec-444483c7c173
document_version_independent_id: ae9d62b7-3065-116c-ec90-162efc7e76a2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/entity-pages.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/entity-pages
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/entity-pages.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: bcdd579d-c608-cf15-1823-12e993617764
---

# Entity pages in Microsoft Sentinel | Microsoft Learn

When you come across a user account, a hostname, an IP address, or an Azure resource in an incident investigation, you may decide you want to know more about it. For example, you might want to know its activity history, whether it's appeared in other alerts or incidents, whether it's done anything unexpected or out of character, and so on. In short, you want information that can help you determine what sort of threat these entities represent and guide your investigation accordingly.

This article describes Microsoft Sentinel entity pages in the Azure portal. For information about entity pages in the Defender portal, see:

- [User entity page in Microsoft Defender](/en-us/defender-xdr/investigate-users)
- [Device entity page in Microsoft Defender](/en-us/defender-xdr/entity-page-device)
- [IP address entity page in Microsoft Defender](/en-us/defender-xdr/entity-page-ip)

Important

After **March 31, 2027**, Microsoft Sentinel will no longer be supported in the Azure portal and will be available only in the Microsoft Defender portal. All customers using Microsoft Sentinel in the Azure portal will be [redirected to the Defender portal and will use Microsoft Sentinel in the Defender portal only](overview#microsoft-sentinel-in-the-azure-portal-retirement-timeline).

If you're still using Microsoft Sentinel in the Azure portal, we recommend that you start planning your [transition to the Defender portal](move-to-defender) to ensure a smooth transition and take full advantage of the [unified security operations experience offered by Microsoft Defender](/en-us/defender-xdr/isoc-overview).

## Entity pages

In these situations, you can select the entity (it will appear as a clickable link) and be taken to an **entity page**, a datasheet full of useful information about that entity. You can also arrive at an entity page by searching directly for entities on the Microsoft Sentinel **entity behavior** page. The types of information you will find on entity pages include basic facts about the entity, a timeline of notable events related to this entity and insights about the entity's behavior.

More specifically, entity pages consist of three parts:

- The left-side panel contains the entity's identifying information, collected from data sources like Microsoft Entra ID, Azure Monitor, Azure Activity, Azure Resource Manager, Microsoft Defender for Cloud, CEF/Syslog, and Microsoft Defender XDR (with all its components).
- The center panel shows a graphical and textual timeline of notable events related to the entity, such as alerts, bookmarks, [anomalies](soc-ml-anomalies), and activities. Activities are aggregations of notable events from Log Analytics. The queries that detect those activities are developed by Microsoft security research teams, and you can now [add your own custom queries to detect activities](customize-entity-activities) of your choosing.
- The right-side panel presents behavioral insights on the entity. These insights are continuously developed by Microsoft security research teams. They are based on various data sources and provide context for the entity and its observed activities, helping you to quickly identify [anomalous behavior](soc-ml-anomalies) and security threats.

If you're investigating an incident using the **[new investigation experience](investigate-incidents)**, you'll be able to see a panelized version of the entity page right inside the incident details page. You have a [list of all the entities in a given incident](investigate-incidents#explore-the-incidents-entities), and selecting an entity opens a side panel with three "cards"—**Info**, **Timeline**, and **Insights**— showing all the same information described above, within the specific time frame corresponding with that of the alerts in the incident.

If you're using the **[Microsoft Sentinel in the Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2263690)**, the **timeline** and **insights** panels appear in the **Sentinel events** tab of the Defender entity page.

[![Screenshot of an example of an entity page in the Azure portal.](media/entity-pages/entity-page-sentinel.png)](media/entity-pages/entity-page-sentinel.png#lightbox)

## The timeline

The timeline is a major part of the entity page's contribution to behavior analytics in Microsoft Sentinel. It presents a story about entity-related events, helping you understand the entity's activity within a specific time frame.

You can choose the **time range** from among several preset options (such as *last 24 hours*), or set it to any custom-defined time frame. Additionally, you can set filters that limit the information in the timeline to specific types of events or alerts.

The following types of items are included in the timeline.

- **Alerts**: any alerts in which the entity is defined as a **mapped entity**. Note that if your organization has created [custom alerts using analytics rules](detect-threats-custom), you should make sure that the rules' entity mapping is done properly.
- **Bookmarks**: any bookmarks that include the specific entity shown on the page.
- **Anomalies**: UEBA detections based on dynamic baselines created for each entity across various data inputs and against its own historical activities, those of its peers, and those of the organization as a whole.
- **Activities**: aggregation of notable events relating to the entity. A wide range of activities are collected automatically, and you can now [customize this section by adding activities](customize-entity-activities) of your own choosing.

[![Screenshot of an example of a timeline on an entity page in the Azure portal.](media/entity-pages/entity-pages-timeline-sentinel.png)](media/entity-pages/entity-pages-timeline-sentinel.png#lightbox)

## Entity insights

Entity insights are queries defined by Microsoft security researchers to help your analysts investigate more efficiently and effectively. The insights are presented as part of the entity page, and provide valuable security information on hosts and users, in the form of tabular data and charts. Having the information here means you don't have to detour to Log Analytics. The insights include data regarding sign-ins, group additions, anomalous events and more, and include advanced ML algorithms to detect anomalous behavior.

The insights are based on the following data sources:

- Syslog (Linux)
- SecurityEvent (Windows)
- AuditLogs (Microsoft Entra ID)
- SigninLogs (Microsoft Entra ID)
- OfficeActivity (Office 365)
- BehaviorAnalytics (Microsoft Sentinel UEBA)
- Heartbeat (Azure Monitor Agent)
- CommonSecurityLog (Microsoft Sentinel)

Generally speaking, each entity insight displayed on the entity page is accompanied by a link that will take you to a page where the query underlying the insight is displayed, along with the results, so you can examine the results in greater depth.

- In Microsoft Sentinel in the Azure portal, the link takes you to the **Logs** page.
- In the Microsoft Defender portal, the link takes you to the **Advanced hunting** page.

## How to use entity pages

Entity pages are designed to be part of multiple usage scenarios and can be accessed from incident management, the investigation graph, bookmarks, or directly from the entity search page under **Entity behavior** in the Microsoft Sentinel main menu.

![Diagram of areas from which you can access entity pages, corresponding with use cases.](media/identify-threats-with-entity-behavior-analytics/entity-pages-use-cases.png)

Entity page information is stored in the **BehaviorAnalytics** table, described in detail in the [Microsoft Sentinel UEBA reference](ueba-reference).

## Supported entity pages

Microsoft Sentinel currently offers the following entity pages:

- User account
- Host
- IP address (**Preview**)

    Note

    The **IP address entity page** (now in preview) contains **geolocation data** supplied by the **Microsoft Threat Intelligence service**. This service combines geolocation data from Microsoft solutions and third-party vendors and partners. The data is then available for analysis and investigation in the context of a security incident. For more information, see also [Enrich entities in Microsoft Sentinel with geolocation data via REST API (Public preview)](geolocation-data-api).
- Azure resource (**Preview**)
- IoT device (**Preview**)—only in Microsoft Sentinel in the Azure portal for now.