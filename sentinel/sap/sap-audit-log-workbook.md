---
layout: Conceptual
title: Microsoft Sentinel solution for SAP applications - SAP -Security Audit log and Initial Access workbook | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sap/sap-audit-log-workbook
breadcrumb_path: ../breadcrumb/toc.json
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
ms.reviewer: mapankra
description: Learn about the SAP - Security Audit log and Initial Access workbook, used to monitor and track data across your SAP systems.
ms.author: monaberdugo
author: mberdugo
ms.topic: reference
ms.date: 2024-09-15T00:00:00.0000000Z
ms.collection: usx-security
ms.custom: sfi-image-nochange
locale: en-us
document_id: 655d7363-41a0-fc12-197f-a9e93ba25e9f
document_version_independent_id: 86fc77a8-3c1e-f613-bc18-dd21f820bdba
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sap/sap-audit-log-workbook.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/sap/sap-audit-log-workbook
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sap/sap-audit-log-workbook.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
platformId: 923cfcba-359e-dbb3-18ec-b00bb750a4d0
---

# Microsoft Sentinel solution for SAP applications - SAP -Security Audit log and Initial Access workbook | Microsoft Learn

This article describes the **SAP - Security Audit log and Initial Access** workbook, used for monitoring and tracking user audit activity across your SAP systems. Use the workbook to get a bird's eye view of user audit activity, better secure your SAP systems, and gain quick visibility into suspicious actions. Drill down into suspicious events as needed.

Use the workbook either for ongoing monitoring of your SAP systems, or to review the systems following a security incident or other suspicious activity.

For example:

[![Screenshot of the top of the SAP -Security Audit log and Initial Access workbook.](media/sap-audit-log-workbook/workbook-overview.png)](media/sap-audit-log-workbook/workbook-overview.png#lightbox)

Content in this article is intended for your **security** team.

## Prerequisites

Before you can start using the **SAP - Security Audit log and Initial Access** workbook, you must have:

- A Microsoft Sentinel solution for SAP installed and a data connector configured. For more information, see [Deploy a Microsoft Sentinel solution for SAP applications](deployment-overview).
- The **SAP - Security Audit log and Initial Access** workbook installed in your Log Analytics workspace enabled for Microsoft Sentinel. For more information, see [Visualize and monitor your data by using workbooks in Microsoft Sentinel](../monitor-your-data).
- At least one incident in your Microsoft Sentinel workspace, with at least one entry available in the `SecurityIncident` table. This doesn't need to be an SAP incident, and you can generate a demo incident using a basic analytics rule if you don't have another one.
- If your Microsoft Entra data is in a different Log Analytics workspace, make sure you select the relevant subscriptions and workspaces at the top of the workbook, under **Azure audit and activities**.

We recommend that you configure auditing for *all* messages from the audit log, instead of only specific logs. Ingestion cost differences are generally minimal and the data is useful for Microsoft Sentinel detections and in post-compromise investigations and hunting. For more information, see [Configure SAP auditing](preparing-sap#configure-sap-auditing).

## Supported filters

The **SAP - Security Audit log and Initial Access** workbook supports the following filters to help you focus on the data you need:

- **Time Range**. From four hours to 90 days.
- **System Roles**. The SAP system roles, for example: Development.
- **System Usage**. For example: SAP GTS.
- **SAP systems**. You can select all systems, a specific system, or select multiple systems.

If you select systems that aren't configured in the [*SAP systems* watchlist](sap-solution-security-content#available-watchlists), the workbook shows an error, specifying the systems with issues. In this case, [configure the watchlist](deployment-solution-configuration#configure-watchlists) to correctly include these systems.

## Logon analysis report data

The **Logon analysis report** tab on the **SAP - Security Audit log and Initial Access** workbook shows data about sign-in failures, such as anomalous data, Microsoft Entra data, and more.

The data is based on the [*SAP systems* watchlist](sap-solution-security-content#available-watchlists).

The **Logon analysis report** tab includes the following areas:

- Logon analysis
- Logon failures - anomaly detection
- Logon failures - trends

### Logon analysis

The **Logon analysis** area shows regarding user sign-ins. For example:

[![Screenshot of the Logon Analysis area of the SAP Audit workbook.](media/sap-audit-log-workbook/logon-analysis.png)](media/sap-audit-log-workbook/logon-analysis.png#lightbox)

The following table describes each metric in the **Logon analysis** area:

| Area | Description |
| --- | --- |
| **Unique user logons per system** | Shows the number of unique sign-ins for each SAP system, and a graph with the sign-in trends over the selected time for each system. For example: the 012 system has 1.4-K unique logon attempts in the last 14 days, and in these 14 days the graph shows a relatively rising sign-in trend. |
| **Logon types trend** | Shows a trend of the number of sign ins according to type, for example, login via dialog. Hover over the graph to show the number of logons for different dates. |
| **Logon failures Vs. success by unique users - trend** | Shows a trend of successful and failed sign ins in the selected period. Hover over the graph to show the amount of successful and failed sign ins for different dates. |

### Logon failures - anomaly detection

The areas under **Anomaly detection - filtering out noisy failed login attempts** show login failure data for SAP systems and users. To see only data flagged by, select **Anomalous only** next to **Failed logons** on the right.

For more information, see [Monitor the SAP audit log](sap-solution-security-content#monitor-the-sap-audit-log).

For example:

[![Screenshot of the sections in the Logon failures area of the SAP Audit workbook that you can filter by anomalous data.](media/sap-audit-log-workbook/logon-failures.png)](media/sap-audit-log-workbook/logon-failures.png#lightbox)

The following table describes each metric in the **Anomaly detection** area:

| Area | Description |
| --- | --- |
| **Logon failure rate** &gt; **Logon failure anomalies** &gt; **Unique User failed logons per SAP system** | Shows the number of unique failed sign ins for each SAP system. |
| **SAP and Active Directory are better together** | The **Anomalous login failures** table shows a combination of Microsoft Sentinel and Microsoft Entra data, listing users according to risk, with the most risky users at the top. For each user, the table shows: - A timeline of failed sign-in attempts- A timeline showing at which point an anomalous failed attempt occurred- The type of anomaly- The user's email address- The Microsoft Entra risk indicator- The number of incidents and alerts in Microsoft Sentinel  Select a user's row to see a list of related alerts and incidents. Microsoft Entra risk events are listed under **Azure audit and signin risks for user**. |
| **Logon failure rate per system** | Shows the selected SAP systems, grouped by type, with the number of failures in the selected period. The system's color indicates the number of failed attempts: Green for a few suspicious sign-in attempts, and red for more.Select a system to see a list of failed sign-ins, with details about the failures. |

In the following screenshot, note the data shown when the first line is selected in the **Anomalous login failures** table. The specific alerts and incident URLs are shown in the **Incidents/alerts overview for user** table.

[![Screenshot of data shown when a line is selected in the Anomalous login failures table.](media/sap-audit-log-workbook/anomalous-logon-failures-table.png)](media/sap-audit-log-workbook/anomalous-logon-failures-table.png#lightbox)

In the following screenshot, the **Azure audit and signin risks for user** table shows data for the sign-in risk related to this user.

[![Screenshot of audit and sign-in risk data shown when a line is selected in the Anomalous login failures table.](media/sap-audit-log-workbook/azure-audit-signin-risks.png)](media/sap-audit-log-workbook/azure-audit-signin-risks.png#lightbox)

In the following screenshot, note the **Login failure rate per system** area, where the **84e** system under the **Test** group is selected. The **Failed logons for system** area on the right shows failure events for this system.

[![Screenshot of the Login failure rate per system area of the SAP Audit workbook.](media/sap-audit-log-workbook/logon-failure-rate.png)](media/sap-audit-log-workbook/logon-failure-rate.png#lightbox)

### Logon failures - trends

The **Logon failures trends** area shows the trends and number of failed sign-ins, grouped by different types of data. For example:

[![Screenshot of the Logon failures trends area of the SAP Audit workbook.](media/sap-audit-log-workbook/logon-failure-trends.png)](media/sap-audit-log-workbook/logon-failure-trends.png#lightbox)

The following table describes each metric in the **Logon failures trends** area:

| Area | Description |
| --- | --- |
| **Login failure by cause** | Shows the trend of the number of sign-in failures according to failure cause, such as incorrect sign-in data. |
| **Login failure by type** | Shows the trend of the number of sign-in failures according to type, such as *the sign-in triggered a background job*, or the *sign-in was via HTTP*. |
| **Login failure by method** | Shows the trend of the number of sign-in failures according to method, such as *SNC* or a *sign-in ticket*. |

## Audit log alerts report tab

The **Audit log alerts** tab shows data about the SAP Audit log events that the Microsoft Sentinel solution for SAP applications watches. The data is based on the [*SAP\_Dynamic\_Audit\_Log\_Monitor\_Configuration* watchlist](sap-solution-security-content#available-watchlists).

The **Audit log alerts** tab shows the severity and audit trends for each SAP system and user. All areas in this tab show data flagged by anomaly detection only. For all events, select **All** next to **Failed logons** on the right.

For more information, see [Monitor the SAP audit log](sap-solution-security-content#monitor-the-sap-audit-log).

For example:

[![Screenshot of the Audit Log Alerts area of the SAP Audit workbook.](media/sap-audit-log-workbook/audit-log-alerts.png)](media/sap-audit-log-workbook/audit-log-alerts.png#lightbox)

The following table describes each metric on the **Audit log alerts** tab:

| Area | Description |
| --- | --- |
| **Alert severity trends per system ID** | Shows a list of systems, with a graph of *Medium* and *High* severity event trends per system. For example, the *012* system had many *High* severity events over the entire period, and a few *Medium* severity events, with a spike that shows more *Medium* severity events in the middle of the period. |
| **Audit trend per user** | Shows a combination of Microsoft Sentinel and Microsoft Entra data, listing users according to risk, with the most risky users at the top. For each user the workbook shows the following data: - A timeline of *High* and *Medium* severity events- The user's email address- The Microsoft Entra risk indicator- The number of incidents and alerts in Microsoft Sentinel  Select a row to see a list of alerts and incidents for that user under **Incidents/alerts overview for user**. View Microsoft Entra risk events under **Azure audit and signin risks for user**. |
| **Risk score per system** | Visually represents each system in a cell shape, showing the risk score for each system and grouping systems by type. The system's color indicates the system's risk score: Green for a lower risk score and red for a higher risk score. Select a system to see a list of SAP events per system. |
| **Events by MITRE ATT&CK tactics** | Shows a list of SAP events grouped by MITRE ATT&CK tactics, like *Initial Access* or *Defense Evasion*. Hover over the graph to show the number of sign-ins for different dates. |
| **Events by category** | Shows a list of SAP event trends grouped by category, like *RFC Start* or *Logon*. Hover over the graph to show the sign-in number for different dates. |
| **Events by authorization group** | Shows a list of SAP event trends grouped by the SAP authorization group, like *USER* or *SUPER*.Hover over the graph to show the number of sign-ins for different dates. |
| **Events by user type** | Shows a list of SAP event trends grouped by the SAP user type, like *Dialog* or *System*. Hover over the graph to show the number of sign-ins for different dates. |

In the following screenshot, note the data shown when the first line is selected in the **Audit trends per user** table. The specific alerts and incident URLs are shown in the **Incidents/alerts overview for user** table.

[![Screenshot of data shown when a line is selected in the Audit trends per user table.](media/sap-audit-log-workbook/audit-trend-per-user.png)](media/sap-audit-log-workbook/audit-trend-per-user.png#lightbox)

In the following screenshot, note the **Risk score per system** area, where the **cb7** system under the **UAT** group is selected. The **SAP events for system** area below the system visualization shows the SAP event for this system.

[![Screenshot of the Risk score per system area of the SAP Audit workbook.](media/sap-audit-log-workbook/risk-score-per-system.png)](media/sap-audit-log-workbook/risk-score-per-system.png#lightbox)

In the following screenshot, note areas with events and event trends grouped by different types of data: MITRE ATT&CK tactics, SAP authorization group, and user type.

[![Screenshot of the different event data in the SAP Audit workbook.](media/sap-audit-log-workbook/event-data-categories.png)](media/sap-audit-log-workbook/event-data-categories.png#lightbox)