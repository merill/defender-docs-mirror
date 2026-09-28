---
layout: Conceptual
title: Investigate incidents in the Microsoft Defender portal (Legacy) - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/investigate-incidents
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Investigate incidents on various assets from correlated signals of various Defender services and other Microsoft security products like Microsoft Sentinel.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.topic: article
ms.date: 2026-09-09T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: sfi-image-nochange
locale: en-us
document_id: 1e7fe495-919b-d9f6-2907-8067781add40
document_version_independent_id: 1e7fe495-919b-d9f6-2907-8067781add40
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/investigate-incidents.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: investigate-incidents
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/investigate-incidents.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/8f37329d-5c2f-4d50-b9b8-aa5cf54dbffe
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/e13db295-3de6-46d5-bcdf-8785a76e3843
platformId: 83d7e959-646a-9fe3-53de-b5d20da0ca09
---

# Investigate incidents in the Microsoft Defender portal (Legacy) - Microsoft Defender XDR | Microsoft Learn

Important

Some information in this article relates to a pre-released product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

Note

This article describes the legacy incident experience in the Microsoft Defender portal. Incident cases are in preview and are the recommended experience for managing incidents. The legacy incident experience remains available during this preview. For the recommended investigation experience, see [Investigate incident cases in the Microsoft Defender portal](investigate-incident-cases).

The Microsoft Defender portal presents correlated alerts, assets, investigations, and evidence from across all your assets into an incident to give you a comprehensive look into the entire breadth of an attack.

Within an incident, you analyze the alerts, understand what they mean, and gather the evidence so that you can create an effective remediation plan.

## Initial investigation

Before diving into the details, take a look at the properties and the entire attack story of the incident.

You can start by selecting the incident row, but not selecting the incident name. A summary pane opens with key information about the incident, including the priority assessment, the factors influencing the priority score, the incident's details, recommended actions, and related threats. Use the up and down arrows at the top of the pane to navigate to the previous or next incident in the incident queue.

[![Selecting an incident in the Microsoft Defender portal](media/investigate-incidents/incident-side-panel.png)](media/investigate-incidents/incident-side-panel.png#lightbox)

From here, you can select **Open incident page**. This opens the main page for the incident where you'll find the full attack story information and tabs for alerts, devices, users, investigations, and evidence. You can also open the main page for an incident by selecting the incident name from the incident queue.

## Attack story

Attack stories help you quickly review, investigate, and remediate attacks while viewing the full story of the attack on the same tab. By using an attack story, you can review the entity details and take remediation actions, such as deleting a file or isolating a device without losing context.

The following video briefly describes the attack story.

Within the attack story, you can find the alert page and the incident graph.

The incident alert page has these sections:

- Alert story, which includes:

    - What happened
    - Actions taken
    - Related events
- Alert properties in the right pane (state, details, description, and others)

Not every alert has all of the listed subsections in the **Alert story** section.

The graph shows the full scope of the attack, how the attack spread through your network over time, where it started, and how far the attacker went. It connects the different suspicious entities that are part of the attack with their related assets such as users, devices, and mailboxes.

From the graph, you can:

- Play the alerts and the nodes on the graph as they occurred over time to understand the chronology of the attack.

    ![Screenshot that shows playing of the alerts and nodes on the attack story graph page.](media/investigate-incidents/play-alert-attack-story.gif)
- Open an entity pane, allowing you to review the entity details and act on remediation actions, such as deleting a file or isolating a device.

    ![Screenshot that shows the review of the entity details on the attack story graph page.](media/investigate-incidents/review-entity-details-attack-story.gif)
- Highlight the alerts based on the entity to which they're related.
- Hunt for entity information of a device, file, IP address, URL, user, email, mailbox, or cloud resource.

### Go hunt

The ***go hunt*** action uses the [advanced hunting](advanced-hunting-go-hunt) feature to find relevant information about an entity. The *go hunt* query checks relevant schema tables for any events or alerts that involve the specific entity you're investigating. To find relevant information about the entity, select any of the following options:

- See all available queries – returns all available queries for the entity type you're investigating.
- All Activity – returns all activities associated with an entity, giving you a comprehensive view of the incident's context.
- Related Alerts – searches for and returns all security alerts that involve a specific entity, so you don't miss any information.
- All User anomalies (Preview) – returns all anomalies associated with the user from the past 30 days, helping you identify unusual behavior that might be relevant to the incident. This option is available only for user entities if you enable [Microsoft Sentinel User and Entity Behavior Analytics (UEBA)](/en-us/azure/sentinel/identify-threats-with-entity-behavior-analytics).

[![Screenshot where the Go Hunt option is selected on a device in an attack story.](media/investigate-incidents/gohunt-attackstory.png)](media/investigate-incidents/gohunt-attackstory.png#lightbox)

You can link the resulting logs or alerts to an incident by selecting a result and then selecting *Link to incident*.

[![Highlighting the link to incident option in go hunt query results](media/investigate-incidents/fig2-gohunt-attackstory.png)](media/investigate-incidents/fig2-gohunt-attackstory.png#lightbox)

If an analytics rule that you set created the incident or related alerts, you can also select ***Run query*** to see other related results.

### Blast radius analysis

Blast radius analysis is an advanced graph visualization integrated into the incident investigation experience. Built on the Microsoft Sentinel data lake and graph infrastructure, it generates an interactive graph showing possible propagation paths from the selected node to predefined critical targets, scoped to the user’s permissions.

Note

Blast radius analysis extends and replaces Attack path analysis.

The blast radius graph provides a unique unified view of both prebreach and post-breach information on the incident page. During an incident investigation, analysts can see the current impact of a breach and the possible future impact in one consolidated graph. Because it's integrated into the incident graph, the blast radius graph helps security teams better understand the scope of the security incident quicker and enhance their defensive measures to reduce the likelihood of widespread damage. Blast radius analysis helps analysts better assess the risk to highly regarded targets and understand the business impact.

The following prerequisites are required to use the blast radius graph:

- You must be onboarded to Microsoft Sentinel data lake. This capability is available for customers who have onboarded to Sentinel data lake, before September 23rd, 2026.
- Exposure management (read) permission or higher. For more information, see [Manage permissions with Microsoft Defender unified role-based access control (RBAC)](/en-us/security-exposure-management/prerequisites#manage-permissions-with-microsoft-defender-xdr-unified-role-based-access-control-rbac).

Important

Attack paths and blast radius features are calculated based on the organization’s available environment data. The value in the graph increases as more data is available for its calculation. If you don't enable further workloads or fully define critical assets, blast radius graphs won't fully represent your environmental risks. For more information on defining critical assets, see [Review and classify critical assets](/en-us/security-exposure-management/classify-critical-assets).

The following table summarizes the blast radius analysis use cases for different user roles:

| User role | Use case |
| --- | --- |
| Security analyst | Use blast radius analysis to investigate an incident. Instantly see the compromised component at the center of the graph and the paths to potentially compromised targets. The graph provides an intuitive visual understanding of the incident and helps you quickly learn the potential scope of a breach. Based on the target and paths, you can escalate, and trigger actions to disrupt, isolate, and contain the incident on nodes along the paths to the target. |
| IT administrators and SOC engineers | Use blast radius analysis to mobilize resources based on business impact and potential damage estimation. Engineers can prioritize the most critical vulnerabilities that require immediate attention. The engineer can proactively allocate the required resources based on the blast radius reach to critical targets in the organization by examining multiple nodes marked with vulnerabilities on the map. The engineer can clearly communicate what was protected and what was impacted and plan and prioritize additional defenses and network segmentations required to reduce further impact of future potential attacks. |
| Incident response team | Quickly determine the scope of incident, with a dynamic visual incident map enabling them to take targeted action on the systems indicated on the graph. |
| CISO or security leaders | Use the blast radius feature to indicate current status, set goals and metrics indicators, and use this to report and audit for compliance reasons. The feature can be used to track progress of defending actions and protection measures investments. |

#### View blast radius graphs

After selecting an incident from the list in the **Incidents** page, a graph view displays the entities and assets involved in the incident.

Select a node to open the context menu, and then select **View blast radius**. If no blast radius path is found, the menu item shows **No blast radius found**.

To view the blast radius of a single node in a group, use the **ungroup** toggle above the grid to present all nodes.

[![Screenshot showing the blast radius context menu item.](media/investigate-incidents/blast-radius.png)](media/investigate-incidents/blast-radius.png#lightbox)

A new graph view loads showing the eight top-rated attack paths. A full list of the paths is visible on the right side panel when selecting **View full blast radius list** above the graph. From the list of reachable targets, you can further explore the path by selecting one of the listed targets. The right panel shows the potential path from the entry point to this target. Some nodes might not have paths associated with them.

[![Screenshot showing the blast radius graph.](media/investigate-incidents/blast-radius-graph.png)](media/investigate-incidents/blast-radius-graph.png#lightbox)

For an explanation of the icons used for nodes and edges in the blast radius graph, see [Understanding graphs and visualizations in Microsoft Defender](understand-graph-icons).

Select **View blast radius list** to see a list of target assets. Select a target asset from the list to view its details and potential attack paths. Selecting the badges in connections shows more details about the connection.

When paths lead to grouped targets of the same types, to view discrete paths to targets, select the grouped icons. A right-side panel opens showing all the targets in the group. Selecting the check box on the left and selecting the **Expand** button on top displays each target and its paths separately.

[![Screenshot showing the blast radius list.](media/investigate-incidents/blast-radius-list.png)](media/investigate-incidents/blast-radius-list.png#lightbox)

Hide the blast radius graph and return to the original incident graph by selecting the node and choosing **Hide blast radius**.

#### Limitations

The following limitations apply to the blast radius graph:

- **Path length limitations (scope of analysis):** Blast radius graph length calculations are bounded up to seven hops from the source node. The blast radius is an approximation of the full attack reach. The maximum number of hops depends on the environment:

    - Five hops for cloud
    - Five hops for on-premises
    - Three hops for hybrid
- **Data freshness:** Latencies might exist between a change in the organization's environment and the reflection of that change in the blast radius graph. During this time, the model might be incomplete.
- **Possible paths:** The blast radius graph shows possible paths. It doesn't guarantee that an attacker takes every path shown.
- **Known attack vectors:** The graph relies on known attack vectors. If attackers find a new lateral movement or new technique that has yet to be modeled, it won't be shown in the blast radius graph.
- **User scopes:** The graph displayed is based on the allowed scopes for the viewing user. The graph shows only nodes and edges that are scoped for the user based on the defined RBAC and scoping settings. Paths containing out of scope nodes or edges aren't visible.
- **Island nodes:** Nonconnected nodes might appear on the graph due to changes that occur between the time the data is collected and the calculation of the blast radius.

### Incident details

You can view an incident's details on the right pane of an incident page. The incident details include incident assignment, ID, classification, categories, and first and last activity date and time. It also includes a description of the incident, impacted assets, active alerts, and, where applicable, the related threats, recommendations, and disruption summary and impact. Here's an example of the incident details where the incident description is highlighted.

[![An example of incident details where the description is highlighted.](media/investigate-incidents/incident-desc-small.png)](media/investigate-incidents/incident-desc.png#lightbox)

The incident description provides a brief overview of the incident. In some cases, the first alert in the incident is used as the incident description. In this case, the description is only shown in the portal and isn't stored in the activity log, advanced hunting tables, or the Microsoft Sentinel in Azure portal.

Tip

Microsoft Sentinel customers can also view and overwrite the same incident description in the Azure portal by setting the incident description through API or automation.

### Filter and focus the incident graph

Use filters on very large incidents with many alerts and entities or hide specific entities to simplify complex incident graphs. By simplifying the graph, you can focus your investigation on what matters most.

**To filter an incident graph:**

1. Select **Add filter** above the incident graph.
2. Choose any of the following available filter criteria, and then select **Add**:

    - **Severity:** Display high-, medium-, or low-severity alerts.
    - **Status:** Display new, in progress, or resolved alerts.
    - **Service sources:** Display alerts from specific services, such as Microsoft Defender for Endpoint, Microsoft Defender for Identity, Microsoft Defender for Office 365, and others.

    [![Screenshot of the incident graph in the Defender portal with add filter option highlighted.](media/investigate-incidents/incident-graph-filter-criteria.png)](media/investigate-incidents/incident-graph-filter-criteria.png#lightbox)
3. For each added filter criteria, choose the items you want to filter, and then select **Apply**.

    [![Screenshot of the incident graph in the Defender portal with add Severity filter highlighted.](media/investigate-incidents/incident-graph-apply-filter.png)](media/investigate-incidents/incident-graph-apply-filter.png#lightbox)

    Note

    If all entities are filtered out, an empty state message appears. Adjust your filters to see relevant entities.

**To hide specific entity types:**

1. Select **Entity types** above the incident graph.
2. Uncheck the entity types you want to hide, such as file or user. The graph redraws itself without these entities.

    [![Screenshot of the incident graph in the Defender portal with Entity types option highlighted.](media/investigate-incidents/incident-graph-hide-entity.png)](media/investigate-incidents/incident-graph-hide-entity.png#lightbox)

## Alerts

On the **Alerts** tab, you can view the alert queue for alerts related to the incident and other information about them, such as the following details:

- Severity of the alerts.
- The entities that were involved in the alert.
- The source of the alerts (Defender for Identity, Defender for Endpoint, Defender for Office 365, Microsoft Defender for Cloud Apps, and the app governance add-on).
- The reason the alerts link together.

[![The Alerts pane for an incident in the Microsoft Defender portal](media/investigate-incidents/incident-page-alerts-small.png)](media/investigate-incidents/incident-page-alerts.png#lightbox)

By default, you see the alerts in chronological order so you can see how the attack played out over time. When you select an alert within an incident, Microsoft Defender XDR displays the alert information specific to the context of the overall incident.

You can see the events of the alert, which other triggered alerts caused the current alert, and all the affected entities and activities involved in the attack, including devices, files, users, cloud apps, and mailboxes.

[![The details of an alert within an incident in the Microsoft Defender portal.](media/investigate-incidents/incident-alert-page-small.png)](media/investigate-incidents/incident-alert-page.png#lightbox)

For more information, see [investigate alerts](investigate-alerts).

Note

If you have provisioned access to Microsoft Purview Insider Risk Management, you can view and manage insider risk management alerts and hunt for insider risk management events in the Microsoft Defender portal. For more information, see [Investigate insider risk threats in the Microsoft Defender portal](irm-investigate-alerts-defender).

## Activities

The **Activities** tab displays a unified timeline of all manual and automated actions that occur within an incident. You can filter by *origin*, *category*, *provider*, *trigger*, *activity status*, *policy status*, *type*, *target name*, *target type*, or *performed by*. You can also access this information as a side panel in the [activity log](manage-incidents#view-the-activity-log-of-an-incident).

By using the Activities tab, analysts can triage and investigate incidents. This process includes identifying key steps taken by humans and automated systems, verifying recent changes (such as tags, merges, severity updates), reviewing comments and handovers, inspecting detailed metadata in side panels, and following automated workflows launched by automation rules, playbooks, or agents.

[![Screenshot of an incident with the Activities tab opened.](media/investigate-incidents/incident-activities-tab.png)](media/investigate-incidents/incident-activities-tab.png#lightbox)

## Assets

Easily view and manage all your assets in one place by using the **Assets** tab. This unified view includes Devices, Users, Mailboxes, and Apps.

The Assets tab displays the total number of assets beside its name. When you select the Assets tab, you see a list of different categories with the number of assets within each category.

[![The Assets page for an incident in the Microsoft Defender portal](media/investigate-incidents/incident-assets-tab-small.png)](media/investigate-incidents/incident-assets-tab.png#lightbox)

### Devices

The **Devices** view lists all the devices related to the incident.

[![The Devices page for an incident in the Microsoft Defender portal](media/investigate-incidents/incident-devices2.png)](media/investigate-incidents/incident-devices2.png#lightbox)

When you select a device from the list, you open a bar that you can use to manage the selected device. You can quickly export, manage tags, initiate automated investigation, and more.

You can select the check mark for a device to see details of the device, directory data, active alerts, and logged on users. Select the name of the device to see device details in the Defender for Endpoint device inventory.

[![The Devices options in the Assets page in the Microsoft Defender portal.](media/investigate-incidents/incident-devicebar.png)](media/investigate-incidents/incident-devicebar.png#lightbox)

From the device page, you can gather additional information about the device, such as all of its alerts, a timeline, and security recommendations. For example, from the **Timeline** tab, you can scroll through the device timeline and view all events and behaviors observed on the machine in chronological order, interspersed with the alerts raised.

### Users

The **Users** view lists all the users that have been identified to be part of or related to the incident.

[![The Users page in the Microsoft Defender portal.](media/investigate-incidents/incident-users2.png)](media/investigate-incidents/incident-users2.png#lightbox)

Select the check mark for a user to see details of the user account threat, exposure, and contact information. Select the user name to see additional user account details.

To learn how to view additional user information and manage the users of an incident, see [investigate users](investigate-users).

### Mailboxes

The **Mailboxes** view lists all the mailboxes that have been identified to be part of or related to the incident.

[![The Mailboxes page for an incident in the Microsoft Defender portal.](media/investigate-incidents/incident-mailboxes2.png)](media/investigate-incidents/incident-mailboxes2.png#lightbox)

Select the check mark for a mailbox to see a list of active alerts. Select the mailbox name to see additional mailbox details on the Explorer page for Defender for Office 365.

### Apps

The **Apps** view lists all the apps identified to be part of or related to the incident.

[![The Apps page for an incident in the Microsoft Defender portal.](media/investigate-incidents/incident-apps.png)](media/investigate-incidents/incident-apps.png#lightbox)

Select the check mark for an app to see a list of active alerts. Select the app name to see additional details on the Explorer page for Defender for Cloud Apps.

### Cloud resources

The **Cloud resources** view lists all the cloud resources that are part of or related to the incident.

[![The Cloud resources page for an incident in the Microsoft Defender portal.](media/investigate-incidents/incident-assets-cloudresource-small.png)](media/investigate-incidents/incident-assets-cloudresource.png#lightbox)

Select the check mark for a cloud resource to see the resource's details and a list of active alerts. Select *Open cloud resource page* to see additional details and to view its full details in Microsoft Defender for Cloud.

## Investigations

The **Investigations** tab lists [automated investigations](m365d-autoir) triggered by alerts in the incident. For incidents associated with Microsoft Defender for Office 365 alerts, the tab shows zero Defender for Office 365 investigations by design. Investigations from other workloads might still appear.

[![Screenshot of an incident with the Investigations tab showing zero investigations.](media/investigate-incidents/incident-investigationspage-small.png)](media/investigate-incidents/incident-investigationspage.png#lightbox)

The change doesn't affect automated investigation processing. To access an investigation linked to a Defender for Office 365 alert, select the associated alert to open the alert details pane, and then select the investigation link. Investigation evidence and entities appear on the **Evidence and Response** tab. Pending actions appear on the **Recommended actions** tab.

If an investigation appears on the **Investigations** tab, select it to open its details page and review the investigation and remediation status.

The **Investigation graph** tab shows:

- The connection of alerts to the impacted assets in your organization.
- Which entities are related to which alerts and how they are part of the story of the attack.
- The alerts for the incident.

The investigation graph helps you quickly understand the full scope of the attack by connecting the different suspicious entities that are part of the attack with their related assets such as users, devices, and mailboxes.

For more information, see [Automated investigation and response in Microsoft Defender XDR](m365d-autoir).

## Evidence and Response

The **Evidence and Response** tab shows all the supported events and suspicious entities in the alerts in the incident.

[![The Evidence and Response page for an incident in the Microsoft Defender portal](media/investigate-incidents/incidents-evidenceresponse-small.png)](media/investigate-incidents/incidents-evidenceresponse.png#lightbox)

Microsoft Defender XDR automatically investigates all the incidents' supported events and suspicious entities in the alerts, providing you with information about the important emails, files, processes, services, IP Addresses, and more. This helps you quickly detect and block potential threats in the incident.

Each analyzed entity is marked with a verdict (Malicious, Suspicious, Clean) and a remediation status. This information helps you understand the remediation status of the entire incident and what next steps you can take.

### Approve or reject remediation actions

For incidents with a remediation status of **Pending approval**, you can approve or reject a remediation action, open in Explorer, or Go hunt from within the Evidence and Response tab.

[![The Approve\Reject option in the Evidence and Response management pane for an incident in the Microsoft Defender portal.](media/investigate-incidents/evidence-approve-small.png)](media/investigate-incidents/evidence-approve.png#lightbox)

## Summary

Use the **Summary** page to assess the relative importance of the incident and quickly access the associated alerts and impacted entities. The **Summary** page gives you a snapshot glance at the top things to notice about the incident.

[![Screenshot that shows the summary information for an incident in the Microsoft Defender portal.](media/investigate-incidents/incident-summary.png)](media/investigate-incidents/incident-summary-small.png#lightbox)

The information is organized into these sections.

| Section | Description |
| --- | --- |
| Alerts and categories | A visual and numeric view of how advanced the attack has progressed against the kill chain. As with other Microsoft security products, Microsoft Defender XDR is aligned to the [MITRE ATT&CK™](https://attack.mitre.org/) framework. The alerts timeline shows the chronological order in which the alerts occurred and for each, their status and name. |
| Scope | Displays the number of impacted devices, users, and mailboxes. It lists the entities in order of risk level and investigation priority. |
| Alerts | Displays the alerts involved in the incident. |
| Evidence | Displays the number of entities affected by the incident. |
| Incident information | Displays the properties of the incident, such as tags, status, and severity. |

## Similar incidents

Some incidents might have similar incidents listed on the **Similar incidents** page. This section shows incidents that have similar alerts, entities, and other properties. This similarity can help you understand the scope of the attack and identify other incidents that might be related.

[![Screenshot that shows the Similar incidents tab for an incident in the Microsoft Defender portal.](media/investigate-incidents/incident-similartab-small.png)](media/investigate-incidents/incident-similartab.png#lightbox)

Tip

**Defender Boxed**, a series of cards showcasing your organization's security successes, improvements, and response actions in the past six months or year, appears for a limited time during January and July of each year. Learn how you can share your [Defender Boxed](incident-queue#defender-boxed) highlights.