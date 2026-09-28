---
layout: Conceptual
title: Work with results containing Microsoft Sentinel data - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/advanced-hunting-defender-results
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to explore and act on advanced hunting query results that include Microsoft Sentinel data in the Microsoft Defender portal, including linking results to incidents and taking response actions.
ms.service: defender-xdr
ms.subservice: adv-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- m365initiative-m365-defender
- tier1
- usx-security
ms.topic: how-to
ms.custom:
- msecd-doc-authoring-1014
- cx-ti
- cx-ah
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 5415444a-d81d-4027-d44a-5bbbe17f8423
document_version_independent_id: 5415444a-d81d-4027-d44a-5bbbe17f8423
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/advanced-hunting-defender-results.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: advanced-hunting-defender-results
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/advanced-hunting-defender-results.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: b35a4d8e-227b-7fe2-3dc6-aaa7cf713a3f
---

# Work with results containing Microsoft Sentinel data - Microsoft Defender XDR | Microsoft Learn

## Explore advanced hunting results

Use the following options to inspect and work with advanced hunting results inline.

[![Screenshot of advanced hunting results with options to expand result rows in the Microsoft Defender portal](media/advanced-hunting-defender-results/advanced-hunting-unified-results.png)](/en-us/defender/media/advanced-hunting-unified-results.png#lightbox)

In advanced hunting, you can explore query results inline with the following features:

- Expand a result by selecting the dropdown arrow at the left of each result.
- Where applicable, expand details for results that are in JSON or array format by selecting the dropdown arrow at the left of applicable result row for added readability.
- Open the side pane to see a record's details (concurrent with expanded rows).

You can also right-click on any result value in a row so that you can use it to:

- Add more filters to the existing query
- Copy the value for use in further investigation
- Update the query to extend a JSON field to a new column

For Microsoft Defender XDR data, you can take further action by selecting the checkboxes to the left of each result row. Select **Link to incident** to link the selected results to an incident (read [Link query results to an incident](advanced-hunting-link-to-incident)) or **Take actions** to open the Take actions wizard (read [Take action on advanced hunting query results](advanced-hunting-take-action)).

## Link query results to an incident

You can use the link to incident feature to add advanced hunting query results to a new or existing incident under investigation. The **Link to incident** feature helps you capture records from advanced hunting activities, which allows you to create a richer timeline or context of events regarding an incident.

### Link results to new or existing incidents

Perform the following steps to link advanced hunting query results to a new or existing incident.

1. In the advanced hunting query pane, enter your query in the query field provided, then select **Run query** to get your results. [![Screenshot of the advanced hunting page in the Microsoft Defender portal](media/advanced-hunting-defender-results/advanced-hunting-results-link1.png)](/en-us/defender/media/advanced-hunting-results-link1.png#lightbox)
2. In the Results page, select the events or records that are related to a new or current investigation you're working on, then select **Link to incident**. [![Screenshot of the link to incident feature in advanced hunting in the Microsoft Defender portal](media/advanced-hunting-defender-results/advanced-hunting-results-link2.png)](/en-us/defender/media/advanced-hunting-results-link2.png#lightbox)
3. In the **Alert details** section in the Link to incident pane, select **Create new incident** to convert the events to alerts and group them to a new incident:

    You can also select **Link to an existing incident** to add the selected records to an existing incident. Choose the related incident from the dropdown list of existing incidents. You can also enter the first few characters of the incident name or ID to find the incident you want.[![Screenshot of the options available in saved queries in the Microsoft Defender portal](media/advanced-hunting-results-link4.png)](media/advanced-hunting-results-link4.png#lightbox)
4. Whether you selected **Create new incident** or **Link to an existing incident**, provide the following details, then select **Next**:

    - **Alert title** – A descriptive title for the results that your incident responders can understand; this descriptive title becomes the alert title
    - **Severity** – Choose the severity applicable to the group of alerts
    - **Category** – Choose the appropriate threat category for the alerts
    - **Description** – Give a helpful description of the grouped alerts
    - **Recommended actions** – List the recommended remediation actions for the security analysts who are investigating the incident
5. In the **Entities** section, select the entities that are involved in the suspicious events. Those entities are used to correlate other alerts to the linked incident and are visible from the incident page.

    For Microsoft Defender XDR data, the entities are automatically selected. If the data is from Microsoft Sentinel, you need to select the entities manually.

    There are two sections for which you can select entities:

    a. **Impacted assets** – Impacted assets that appear in the selected events should be added here. The following types of assets can be added:

    - Account
    - Device
    - Mailbox
    - Cloud application
    - Azure resource
    - Amazon Web Services resource
    - Google Cloud Platform resource

    b. **Related evidence** – Non-assets that appear in the selected events can be added in this section. The supported entity types are:

    - Process
    - File
    - Registry value
    - IP
    - OAuth application
    - DNS
    - Security group
    - URL
    - Mail cluster
    - Mail message

Note

For queries containing only Defender data, only entity types that are available in Defender tables are shown.

1. After an entity type is selected, select an identifier type that exists in the selected records so that it can be used to identify this entity. Each entity type has a list of supported identifiers, as can be seen in the relevant drop down. Read the description displayed when hovering over each identifier to better understand the identifier.
2. After selecting the identifier, select a column from the query results that contain the selected identifier. You can select **Explore query and results** to open the advanced hunting context panel. The advanced hunting context panel allows you to explore your query and results to make sure you chose the right column for the selected identifier. [![Screenshot of the link to incident wizard entities branch in the Microsoft Defender portal](media/advanced-hunting-defender-results-identifier.png)](media/advanced-hunting-defender-results-identifier.png#lightbox) In our example, we used a query to find events related to a possible email exfiltration incident, therefore the recipient's mailbox and recipient's account are the impacted entities, and the sender's IP as well as email message are related evidence.

    [![Screenshot of the link to incident wizard full entities branch in the Microsoft Defender portal](media/advanced-hunting-defender-results-link-entities.png)](media/advanced-hunting-defender-results-link-entities.png#lightbox)

    A different alert is created for each record with a unique combination of impacted entities. In our example, if there are three different recipient mailboxes and recipient object ID combinations, for instance, then three alerts are created and linked to the chosen incident.
3. Select **Next**.
4. Review the details you've provided in the Summary section.
5. Select **Done**.

### View linked records in the incident

You can select the incident link generated in the Summary step of the wizard, or select the incident name from the incident queue, to view the incident to which the events are linked.

[![Screenshot of the summary step in the link to incident wizard in the Microsoft Defender portal](media/advanced-hunting-results-link7.png)](media/advanced-hunting-results-link7.png#lightbox)

In our example, the three alerts, representing the three selected events, were linked successfully to a new incident. In each of the alert pages, you can find the complete information on the event or events in timeline view (if available) and the query results view.

You can also select the event from the timeline view or from the query results view to open the **Inspect record** pane.

[![Screenshot of the incident page in the Microsoft Defender portal](media/advanced-hunting-results-link8.png)](media/advanced-hunting-results-link8.png#lightbox)

### Filter for events added using advanced hunting

You can view which alerts were generated from advanced hunting by filtering incidents and alerts by **Manual** detection source.

[![Screenshot of the filter dropdown in advanced hunting in the Microsoft Defender portal](media/advanced-hunting-results-link9.png)](media/advanced-hunting-results-link9.png#lightbox)