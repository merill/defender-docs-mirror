---
layout: Conceptual
title: Basic incident tasks for Microsoft Sentinel incidents in the Azure portal | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/incident-navigate-triage
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
description: This article describes how to navigate and triage incidents in Microsoft Sentinel in the Azure portal.
ms.author: guywild
author: guywi-ms
ms.reviewer: mmagenheim
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: a6665b8b-9b89-edd9-bf1f-3b9372279508
document_version_independent_id: ba444eb2-99ea-1715-1ef6-60bd77b8fa93
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/incident-navigate-triage.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/incident-navigate-triage
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/incident-navigate-triage.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 5d7f6ed6-12b4-b6d4-e172-ea9c81ae72a1
---

# Basic incident tasks for Microsoft Sentinel incidents in the Azure portal | Microsoft Learn

This article describes how to navigate and run basic triage on your incidents in the Azure portal. You learn how to search for and filter incidents, assign ownership, update status and severity, and close resolved incidents.

## Prerequisites

Before you investigate incidents, make sure you have the following roles and permissions.

- The [**Microsoft Sentinel Responder**](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-responder) role assignment is required to investigate incidents.

    Learn more about [roles in Microsoft Sentinel](roles).
- If you have a guest user that needs to assign incidents, the user must be assigned the [Directory Reader](/en-us/azure/active-directory/roles/permissions-reference#directory-readers) role in your Microsoft Entra tenant. Regular (nonguest) users have this role assigned by default.

## Navigate and triage incidents

Use the following steps to navigate to and triage incidents in Microsoft Sentinel.

1. From the Microsoft Sentinel navigation menu, under **Threat management**, select **Incidents**.

    The **Incidents** page gives you basic information about all of your open incidents. For example:

    [![Screenshot of view of incident severity.](media/investigate-incidents/incident-grid.png)](media/investigate-incidents/incident-grid.png#lightbox)

    - **Across the top of the screen**, you have a toolbar with actions you can take outside of a specific incident—either on the grid as a whole, or on multiple selected incidents. You also have the counts of open incidents, whether new or active, and the counts of open incidents by severity.
    - **In the central pane**, you have an incident grid, which is a list of incidents as filtered by the filtering controls at the top of the list, and a search bar to find specific incidents.
    - **On the side**, you have a details pane that shows important information about the incident highlighted in the central list, along with buttons for taking certain specific actions regarding that incident.
2. Your security operations team might have [automation rules](automate-incident-handling-with-automation-rules#automatic-assignment-of-incidents) in place to perform basic triage on new incidents and assign them to the proper personnel.

    In that case, filter the incident list by **Owner** to limit the list to the incidents assigned to you or to your team. The incidents filtered by owner represent your personal workload.

    If automation rules aren't assigning incidents, you can perform basic triage yourself. Start by filtering the list of incidents by available filtering criteria, whether status, severity, or product name. For more information, see Search for incidents.
3. Triage a specific incident and take initial action on it immediately, right from the details pane on the **Incidents** page, without having to enter the incident’s full details page. For example:

    - **Investigate Microsoft Defender XDR incidents in Microsoft Defender XDR:** Follow the [**Investigate in Microsoft Defender XDR**](microsoft-365-defender-sentinel-integration) link to pivot to the parallel incident in the Defender portal. Any changes you make to the incident in Microsoft Defender XDR are synchronized to the same incident in Microsoft Sentinel.
    - **Open the list of assigned tasks:** Incidents that have tasks assigned display a count of completed and total tasks and a **View full details** link. Follow the link to open the [**Incident tasks**](incident-tasks) page to see the list of tasks for this incident.
    - **Assign ownership of the incident** to a user or group by selecting from the **Owner** drop-down list.

        ![Screenshot of assigning incident to user.](media/investigate-incidents/assign-incident-to-user.png)

        Recently selected users and groups appear at the top of the pictured drop-down list.
    - **Update the incident’s status** (for example, from **New** to **Active** or **Closed**) by selecting from the **Status** drop-down list. When closing an incident, you're required to specify a reason. For more information, see Close an incident.
    - **Change the incident’s severity** by selecting from the **Severity** drop-down list.
    - **Add tags** to categorize your incidents. You might need to scroll down to the bottom of the details pane to see where to add tags.
    - **Add comments** to log your actions, ideas, questions, and more. You might need to scroll down to the bottom of the details pane to see where to add comments.
4. If the information in the details pane is sufficient to prompt further remediation or mitigation actions, select the **Actions** button at the bottom to do one of the following:

    | Action | Description |
    | --- | --- |
    | **Investigate** | Use the [graphical investigation tool](investigate-incidents#investigate-incidents-visually-using-the-investigation-graph) to discover relationships between alerts, entities, and activities, both within this incident and across other incidents. |
    | **Run playbook** | Run a [playbook](automate-responses-with-playbooks#run-a-playbook-manually) on this incident to take particular [enrichment, collaboration, or response actions](automate-responses-with-playbooks#use-cases-for-playbooks) such as your SOC engineers might have made available. |
    | **Create automation rule** | Create an [automation rule](automate-incident-handling-with-automation-rules#common-use-cases-and-scenarios) that runs only on incidents like this one (generated by the same analytics rule) in the future, in order to reduce your future workload or to account for a temporary change in requirements (such as for a penetration test). |
    | **Create team (Preview)** | Create a team in Microsoft Teams to collaborate with other individuals or teams across departments on handling the incident. |

    For example:

    ![Screenshot of menu of actions that can be performed on an incident from the details pane.](media/investigate-incidents/incident-actions.png)
5. If more information about the incident is needed, select **View full details** in the details pane to open and see the incident's details in their entirety, including the alerts and entities in the incident, a list of similar incidents, and selected top insights.

## Search for incidents

To find a specific incident quickly, enter a search string in the search box above the incidents grid and press **Enter** to modify the list of incidents shown accordingly. If your incident isn't included in the results, you might want to narrow your search by using **Advanced search** options.

To modify the search parameters, select the **Search** button and then select the parameters where you want to run your search.

For example:

![Screenshot of the incident search box and button to select basic and/or advanced search options.](media/investigate-incidents/advanced-search.png)

By default, incident searches run across the **Incident ID**, **Title**, **Tags**, **Owner**, and **Product name** values only. In the search pane, scroll down the list to select one or more other parameters to search, and select **Apply** to update the search parameters. Select **Set to default** reset the selected parameters to the default option.

Note

Searches in the **Owner** field support both names and email addresses.

Using advanced search options changes the search behavior as follows:

| Search behavior | Description |
| --- | --- |
| **Search button color** | The color of the search button changes, depending on the types of parameters currently being used in the search. <br>- As long as only the default parameters are selected, the button is grey.<br>- As soon as different parameters are selected, such as advanced search parameters, the button turns blue. |
| **Auto-refresh** | Using advanced search parameters prevents you from selecting to automatically refresh your results. |
| **Entity parameters** | All entity parameters are supported for advanced searches. When searching in any entity parameter, the search runs in all entity parameters. |
| **Search strings** | Searching for a string of words includes all of the words in the search query. Search strings are case sensitive. |
| **Cross workspace support** | Advanced searches aren't supported for cross-workspace views. |
| **Number of search results displayed** | When you're using advanced search parameters, only 50 results are shown at a time. |

Tip

If you're unable to find the incident you're looking for, remove search parameters to expand your search. If your search results in too many items, add more filters to narrow down your results.

## Close an incident

Once you resolve a particular incident (for example, when your investigation reaches its conclusion), set the incident’s status to **Closed**. When you do so, you're asked to classify the incident by specifying the reason you're closing it. Selecting a classification is mandatory.

Select **Select classification** and choose one of the following from the drop-down list:

- **True Positive** – suspicious activity
- **Benign Positive** – suspicious but expected
- **False Positive** – incorrect alert logic
- **False Positive** – incorrect data
- **Undetermined**

![Screenshot that highlights the classifications available in the Select classification list.](media/investigate-incidents/closing-reasons-dropdown.png)

For more information about false positives and benign positives, see [Handle false positives in Microsoft Sentinel](false-positives).

After choosing the appropriate classification, add descriptive text in the **Comment** field. A descriptive comment is useful if you need to refer back to the incident later. Select **Apply** when you’re done, and the incident is closed.

![Screenshot of closing an incident.](media/investigate-incidents/closing-reasons-comment-apply.png)