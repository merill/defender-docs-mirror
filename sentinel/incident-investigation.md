---
layout: Conceptual
title: Microsoft Sentinel incident investigation in the Azure portal | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/incident-investigation
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
description: This article describes Microsoft Sentinel's incident investigation and management capabilities in the Azure portal.
ms.author: guywild
author: guywi-ms
ms.reviewer: idpelleg
ms.topic: concept-article
ms.date: 2024-12-22T00:00:00.0000000Z
locale: en-us
document_id: 6ace191a-86b6-7e9a-3ecc-9580942018e5
document_version_independent_id: 2b7a5018-f476-4159-fe1b-c6f6949ea0f9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/incident-investigation.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/incident-investigation
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/incident-investigation.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 921c3db0-c2d8-d01c-8853-2c872c8edb31
---

# Microsoft Sentinel incident investigation in the Azure portal | Microsoft Learn

Microsoft Sentinel provides an incident management experience for investigating and managing security incidents in the Azure portal. **Incidents** are Microsoft Sentinel records that contain a complete and constantly updated chronology of a security threat, including evidence (alerts), suspects and parties of interest (entities), insights collected and curated by security experts and AI/machine learning models, comments, and logs of actions taken during the investigation.

The incident investigation experience in Microsoft Sentinel begins with the **Incidents** page—an experience designed to give you everything you need for your investigation in one place. The key goal of this experience is to increase your SOC’s efficiency and effectiveness, reducing its mean time to resolve (MTTR).

This article describes Microsoft Sentinel's incident investigation and management capabilities in the Azure portal, taking you through the phases of a typical incident investigation while presenting the displays and tools available to help you investigate and resolve incidents.

## Prerequisites

- The [**Microsoft Sentinel Responder**](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-responder) role assignment is required to investigate incidents.

    Learn more about [roles in Microsoft Sentinel](roles).
- If you have a guest user that needs to assign incidents, the user must be assigned the [Directory Reader](/en-us/azure/active-directory/roles/permissions-reference#directory-readers) role in your Microsoft Entra tenant. Regular (nonguest) users have this role assigned by default.

## Increase your SOC's maturity

Microsoft Sentinel incidents give you tools to help your Security Operations (SecOps) maturity level up by standardizing your processes and auditing your incident management.

### Standardize your processes

**Incident tasks** are workflow lists of tasks for analysts to follow to ensure a uniform standard of care and to prevent crucial steps from being missed:

- **SOC managers and engineers** can develop these task lists and have them automatically apply to different groups of incidents as appropriate, or across the board.
- **SOC analysts** can then access the assigned tasks within each incident, marking them off as they’re completed.

    Analysts can also manually add tasks to their open incidents, either as self-reminders or for the benefit of other analysts who may collaborate on the incident (for example, due to a shift change or escalation).

For more information, see [Use tasks to manage incidents in Microsoft Sentinel in the Azure portal](incident-tasks).

### Audit your incident management

The incident **activity log** tracks actions taken on an incident, whether initiated by humans or automated processes, and displays them along with all the comments on the incident.

You can add your own comments here as well. For more information, see [Investigate Microsoft Sentinel incidents in depth in the Azure portal](investigate-incidents).

## Investigate effectively and efficiently

First things first: As an analyst, the most basic question you want to answer is, why is this incident being brought to my attention? Entering an incident’s details page will answer that question: right in the center of the screen, you’ll see the **Incident timeline** widget.

Use Microsoft Sentinel incidents to investigate security incidents effectively and efficiently using the incident timeline, learning from similar incidents, examining top insights, viewing entities, and exploring logs.

### Incident timelines

The incident timeline is the diary of all the **alerts** that represent all the logged events that are relevant to the investigation, in the order in which they happened. The timeline also shows **bookmarks**, snapshots of evidence collected while hunting and added to the incident.

Search the list of alerts and bookmarks, or filter the list by severity, tactics, or content type (alert or bookmark), to help you find the item you want to pursue. The initial display of the timeline immediately tells you several important things about each item in it, whether alert or bookmark:

- The **date and time** of the creation of the alert or bookmark.
- The **type** of item, alert or bookmark, indicated by an icon and a ToolTip when hovering on the icon.
- The **name** of the alert or the bookmark, in bold type on the first line of the item.
- The **severity** of the alert, indicated by a color band along the left edge, and in word form at the beginning of the three-part "subtitle" of the alert.
- The **alert provider**, in the second part of the subtitle. For bookmarks, the **creator** of the bookmark.
- The MITRE ATT&CK **tactics** associated with the alert, indicated by icons and ToolTips, in the third part of the subtitle.

For more information, see [Reconstruct the timeline of the attack story](investigate-incidents#reconstruct-the-timeline-of-the-attack-story).

### Lists of similar incidents

If anything you’ve seen so far in your incident looks familiar, there may be good reason. Microsoft Sentinel stays one step ahead of you by showing you the incidents most similar to the open one.

The **Similar incidents** widget shows you the most relevant information about incidents deemed to be similar, including their last updated date and time, last owner, last status (including, if they are closed, the reason they were closed), and the reason for the similarity.

This can benefit your investigation in several ways:

- Spot concurrent incidents that may be part of a larger attack strategy.
- Use similar incidents as reference points for your current investigation—see how they were dealt with.
- Identify owners of past similar incidents to benefit from their knowledge.

For example, you want to see if other incidents like this have happened before or are happening now.

- You might want to identify concurrent incidents that might be part of the same larger attack strategy.
- You might want to identify similar incidents in the past, to use them as reference points for your current investigation.
- You might want to identify the owners of past similar incidents, to find the people in your SOC who can provide more context, or to whom you can escalate the investigation.

The widget shows you the 20 most similar incidents. Microsoft Sentinel decides which incidents are similar based on common elements including entities, the source analytics rule, and alert details. From this widget you can jump directly to any of these incidents' full details pages, while keeping the connection to the current incident intact.

[![Screenshot of the similar incidents display.](media/investigate-incidents/similar-incidents.png)](media/investigate-incidents/similar-incidents.png#lightbox)

Similarity is determined based on the following criteria:

| Criteria | Description |
| --- | --- |
| **Similar entities** | An incident is considered similar to another incident if they both include the same [entities](entities). The more entities two incidents have in common, the more similar they're considered to be. |
| **Similar rule** | An incident is considered similar to another incident if they were both created by the same [analytics rule](detect-threats-built-in). |
| **Similar alert details** | An incident is considered similar to another incident if they share the same title, product name, and/or [custom details](surface-custom-details-in-alerts). |

Incident similarity is calculated based on data from the 14 days prior to the last activity in the incident, that being the end time of the most recent alert in the incident. Incident similarity is also recalculated every time you enter the incident details page, so the results might vary between sessions if new incidents were created or updated.

For more information, see [Check for similar incidents in your environment](investigate-incidents#check-for-similar-incidents-in-your-environment).

### Top incident insights

Next, having the broad outlines of what happened (or is still happening), and having a better understanding of the context, you’ll be curious about what interesting information Microsoft Sentinel has already found out for you.

Microsoft Sentinel automatically asks the big questions about the entities in your incident and shows the top answers in the **Top insights** widget, visible on the right side of the incident details page. This widget shows a collection of insights based on both machine-learning analysis and the curation of top teams of security experts.

These are a specially selected subset of the insights that appear on [entity pages](entity-pages#entity-insights), but in this context, insights for all the entities in the incident are presented together, giving you a more complete picture of what's happening. The full set of insights appears on the **Entities tab**, for each entity separately—see below.

The **Top insights** widget answers questions about the entity relating to its behavior in comparison to its peers and its own history, its presence on watchlists or in threat intelligence, or any other sort of unusual occurrence relating to it.

Most of these insights contain links to more information. These links open the Logs panel in-context, where you'll see the source query for that insight along with its results.

### List of related entities

Now that you have some context and some basic questions answered, you’ll want to get some more depth on the major players are in this story.

Usernames, hostnames, IP addresses, file names, and other types of entities can all be “persons of interest” in your investigation. Microsoft Sentinel finds them all for you and displays them front and center in the **Entities** widget, alongside the timeline.

Select an entity from this widget to pivot you to that entity's listing in the **Entities tab** on the same **incident page**, which contains a list of all the entities in the incident.

Select an entity in the list to open a side panel with information based on the [entity page](entity-pages), including the following details:

- **Info** contains basic information about the entity. For a user account entity this might be things like the username, domain name, security identifier (SID), organizational information, security information, and more.
- **Timeline** contains a list of the alerts that feature this entity and activities the entity has done, as collected from logs in which the entity appears.
- **Insights** contains answers to questions about the entity relating to its behavior in comparison to its peers and its own history, its presence on watchlists or in threat intelligence, or any other sort of unusual occurrence relating to it.

    These answers are the results of queries defined by Microsoft security researchers that provide valuable and contextual security information on entities, based on data from a collection of sources.

Depending on the entity type, you can take a number of further actions from this side panel, including:

- **Pivot to the entity's full [entity page](entity-pages)** to get even more details over a longer timespan or launch the graphical investigation tool centered on that entity.
- **Run a [playbook](respond-threats-during-investigation)** to take specific response or remediation actions on the entity (in Preview).
- **Classify the entity as an [indicator of compromise (IOC)](add-entity-to-threat-intelligence)** and add it to your Threat intelligence list.

Each of these actions is currently supported for certain entity types and not for others. The following table shows which actions are supported for each entity type:

| Available actions ▶Entity types ▼ | View full details(in entity page) | Add to TI \* | Run playbook \*(Preview) |
| --- | --- | --- | --- |
| **User account** | ✔ |  | ✔ |
| **Host** | ✔ |  | ✔ |
| **IP address** | ✔ | ✔ | ✔ |
| **URL** |  | ✔ | ✔ |
| **Domain name** |  | ✔ | ✔ |
| **File (hash)** |  | ✔ | ✔ |
| **Azure resource** | ✔ |  |  |
| **IoT device** | ✔ |  |  |

\* For entities for which the **Add to TI** or **Run playbook** actions are available, you can take those actions right from the **Entities** widget in the **Overview tab**, never leaving the incident page.

### Incident logs

Explore incident logs to get down into the details to know *what exactly happened?*

From almost any area in the incident, you can drill down into the individual alerts, entities, insights, and other items contained in the incident, viewing the original query and its results.

These results are displayed in the Logs (log analytics) screen that appears here as a panel extension of the incident details page, so you don’t leave the context of the investigation.

## Organized records with incidents

In the interests of transparency, accountability, and continuity, you’ll want a record of all the actions that have been taken on the incident—whether by automated processes or by people. The incident **activity log** shows you all of these activities. You can also see any comments that have been made and add your own.

The activity log is constantly auto-refreshing, even while open, so you can see changes to it in real time.