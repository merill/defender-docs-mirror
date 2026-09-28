---
layout: Conceptual
title: Microsoft Defender Experts report - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/defender-experts/defender-experts-mdr-reports
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
ms.reviewer: 
description: Defender Experts MDR includes an interactive, on-demand report that provides a clear summary of our expert analysts.
ms.service: defender-experts-for-xdr
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- essentials-manage
ms.topic: concept-article
ms.custom:
- cx-ti
- cx-dex
- sfi-image-nochange
ms.date: 2025-10-31T00:00:00.0000000Z
locale: en-us
document_id: f5ab4927-9c9a-ee81-53a6-798afb7ff175
document_version_independent_id: f5ab4927-9c9a-ee81-53a6-798afb7ff175
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/defender-experts/defender-experts-mdr-reports.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-experts/defender-experts-mdr-reports
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/defender-experts/defender-experts-mdr-reports.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 565d65aa-8199-9ab7-9880-bb0752edc5b0
---

# Microsoft Defender Experts report - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- [Microsoft Defender Experts MDR](defender-experts-mdr-overview)
- [Microsoft Defender Experts for Servers](defender-experts-servers-overview)

For Defender Experts reports instructions, check out this short video.

The Microsoft Defender Experts service includes an interactive, on-demand report that provides a clear summary of the work our expert analysts are doing on your behalf, aggregate information about your incident landscape, and granular details about specific incidents. Your Security Delivery Expert (SDX) also uses the report to provide you with more context regarding the service during a monthly business review.

[![Screenshot of the Report overview tab in Defender Experts report.](media/defender-xdr-report.png)](media/defender-xdr-report.png#lightbox)

The report is designed to provide more insights about the incidents our experts investigated and resolved in your environment in real time or during a specific period. To view the report in your Microsoft Defender portal, go to **Reports**, select **Defender Experts** &gt; **XDR report**. It's divided into two sections:

- Report overview
- Trends

## Report overview: Quickly understand the investigated incidents

The **Report overview** tab gives you a view of the types of incidents we resolved in your environment in the last 30 days, providing you with transparency in our operations. You can also select a custom date range in **Showing results for** to get detailed information about incidents during a specific period.

### Resolved incidents

The top section of the report overview shows the percentage of resolved incidents. The report also shows the following figures:

- **Incidents investigated** - The number of active threats and other incidents from your incident queue that we triaged, investigated, or are currently investigating within our scope.
- **Incidents resolved** - The total number of investigated incidents that were closed.
- **Resolved directly** - The number of investigated incidents that we closed directly on your behalf.
- **Resolved with your help** - The number of investigated incidents that were resolved because of your action on one or more managed response tasks.
- **Third-party enriched** - The number of incidents that were enriched with third-party network signals. This data is available when you're enrolled in the [third-party network enrichment](defender-experts-mdr-third-party-enrichment).

### Average time to resolve incidents

The **Average time to resolve incidents** section displays a bar chart of the average time, in minutes, our experts spent investigating and closing incidents in your environment and the average time you spent performing the required managed response actions.

### Incidents by severity, category, and service source

The **Incidents by severity**, **Incidents by category**, and **Incidents by service source** sections break down resolved incidents by severity, attack technique, and Microsoft security service source, respectively. These sections let you identify potential attack entry points and types of threats detected in your environment, assess their impact, and develop strategies to mitigate and prevent them. Select **View selected incidents** to get a filtered view of the incident queue based on the selections you made in each of the sections.

### Most impacted assets

The **Most impacted assets** section shows the users and devices in your environment that were involved in the most number of incidents during your selected date range. You can see the number of incidents each asset was involved in. Select an asset to get a filtered view of the incident queue based on the incidents that included the said asset.

### Incidents resolved by MITRE tactics

The **Incidents resolved by MITRE tactics** section shows the total number of investigated incidents and resolved true positive incidents, categorized by their associated threat tactics. These threat tactics are based on the [MITRE ATT&CK attack framework](https://attack.mitre.org/), and they can help you visualize what the incidents were trying to achieve in each attack phase so you can plan the corresponding mitigation actions.

By default, this section displays all tactic categories, regardless if there are incidents associated with them. To display only the tactics with related incidents, turn off the **Show all tactics** button.

### Incidents resolved by severity and category

The **Incidents resolved by severity and category** section displays a bar chart that shows the total resolved incidents, broken down by their corresponding severity and threat categories.

By default, this section displays data from all resolved incident types (true positive, false positive, and informational). You can filter the results by these different incident types by selecting their corresponding options in the **Select incident type** dropdown box.

### Incidents that required your action

The **Incidents that required your action** section shows the number of incidents that our experts investigated but needed further actions from your team through one or more managed response tasks. It summarizes the number of actions that you completed, marked as pending, skipped, or performed but failed. It also displays a bar chart of these incidents based on their severity.

This section also displays a table with a list of incident titles and their corresponding severity, the number of required actions, and the status of these actions. You can sort and filter incidents according to severity and action status to better manage them. Selecting an incident title opens its corresponding incident page, where you can then perform the required managed response actions.

## Trends: See incident patterns and response efficiency to make informed decisions

The **Trends** tab of the report provides you with the monthly volume of investigated and resolved incidents for the last six months, visualized according to the incidents' severity, MITRE tactic, and threat type. The trends section gives you insight into how Defender Experts are tangibly improving your security operations by showing important operational metrics on a month-over-month basis.

[![Screenshot of the Trends tab in Defender Experts report.](media/reports-xdr/xdr-report-trends.png)](media/reports-xdr/xdr-report-trends.png#lightbox)

The visualizations are respectively displayed in the **Incidents by severity**, **Incidents by MITRE tactic**, and **Incidents by classification** sections. For each section, you can filter data according to the different incident types (true positive, false positive, and informational) by selecting their corresponding options in the **Select incident type** dropdown box. The **Incidents by severity** and **Incidents by MITRE tactic** sections also have the **View selected incidents** button, which you can select to get a filtered view of the incident queue based on the selections you made in each of these sections.

The **Trends** tab also has the **Managed response task completion and efficiency** widget, which shows the monthly volume of managed response tasks your team completed each month, along with the median time it took your team to complete those tasks. This widget helps identify any spikes in your team's response efficacy and efficiency, which is increasingly important as attackers continue to decrease the time between initial access and lateral movement.

[![Screenshot of the Managed response task completion and efficiency widget in Defender Experts report.](media/reports-xdr/xdr-report-manage-response-task.png)](media/reports-xdr/xdr-report-manage-response-task.png#lightbox)