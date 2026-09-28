---
layout: Conceptual
title: Add entities to threat intelligence - Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/add-entity-to-threat-intelligence
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
description: Learn how to add a malicious entity discovered in an incident investigation to your threat intelligence in Microsoft Sentinel.
ms.author: pauloliveria
author: poliveria
ms.reviewer: yoninave
ms.topic: how-to
ms.date: 2026-07-01T00:00:00.0000000Z
ms.collection: usx-security
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 0637ee3e-03d8-9caa-23a9-2bd9a553304d
document_version_independent_id: 2791e13b-2461-ba60-7656-5ecea1a2af3c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/add-entity-to-threat-intelligence.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/add-entity-to-threat-intelligence
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/add-entity-to-threat-intelligence.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: e2b3301a-85f6-861d-b582-9c974d5dc72d
---

# Add entities to threat intelligence - Microsoft Sentinel | Microsoft Learn

This article shows how to add entities discovered in an incident investigation as threat intelligence indicators in Microsoft Sentinel, and how to find and use those indicators afterward.

During an investigation, you examine entities and their context as an important part of understanding the scope and nature of an incident. When you discover an entity as a malicious domain name, URL, file, or IP address in the incident, it should be labeled and tracked as an indicator of compromise (IOC) in your threat intelligence.

For example, you might discover an IP address that performs port scans across your network or functions as a command and control node by sending and/or receiving transmissions from large numbers of nodes in your network.

With Microsoft Sentinel, you can flag malicious domain names, URLs, files, and IP addresses from within your incident investigation and add them to your threat intelligence. You can view the added indicators by querying them or searching for them in the threat intelligence management interface and use them across your Microsoft Sentinel workspace.

## Add an entity to your threat intelligence

The [Incident details page](investigate-incidents) and the investigation graph give you two ways to add entities to threat intelligence.

# [Incident details page](#tab/incidents)
Perform the following steps to add an entity to threat intelligence from the Incident details page:

1. On the Microsoft Sentinel menu, select **Incidents** from the **Threat management** section.
2. Select an incident to investigate. On the **Incident details** pane, select **View full details** to open the **Incident details** page.
3. On the **Entities** pane, find the entity that you want to add as a threat indicator. (You can filter the list or enter a search string to help you locate it.)

    [![Screenshot that shows the Incident details page.](media/add-entity-to-threat-intelligence/incident-details-overview.png)](media/add-entity-to-threat-intelligence/incident-details-overview.png#lightbox)
4. Select the three dots to the right of the entity, and select **Add to TI** from the pop-up menu.

    Add only the following types of entities as threat indicators:

    - Domain name
    - IP address (IPv4 and IPv6)
    - URL
    - File (hash)

    ![Screenshot that shows adding an entity to threat intelligence.](media/add-entity-to-threat-intelligence/entity-actions-from-overview.png)

# [Investigation graph](#tab/cases)
The [investigation graph](investigate-cases) is a visual, intuitive tool that presents connections and patterns and enables your analysts to ask the right questions and follow leads. Use the investigation graph to add entities to your threat intelligence indicator lists by making them available across your workspace.

1. On the Microsoft Sentinel menu, select **Incidents** from the **Threat management** section.
2. Select an incident to investigate. On the **Incident details** pane, select **Actions**, and choose **Investigate** from the pop-up menu to open the investigation graph.

    ![Screenshot that shows selecting an incident from the list to investigate.](media/add-entity-to-threat-intelligence/select-incident-to-investigate.png)
3. Select the entity from the graph that you want to add as a threat indicator. On the side pane that opens, select **Add to TI**.

    Only add the following types of entities as threat indicators:

    - Domain name
    - IP address (IPv4 and IPv6)
    - URL
    - File (hash)

    ![Screenshot that shows adding an entity to threat intelligence.](media/add-entity-to-threat-intelligence/add-entity-to-ti.png)

---

After you select **Add to TI** from either the Incident details page or the investigation graph, the **New indicator** side pane opens.

1. The following fields are populated automatically:

    - **Types**

        - The type of indicator represented by the entity you're adding.
            - Dropdown list with possible values: `ipv4-addr`, `ipv6-addr`, `URL`, `file`, and `domain-name`.
        - Required. Automatically populated based on the *entity type*.
    - **Value**

        - The name of this field changes dynamically to the selected indicator type.
        - The value of the indicator itself.
        - Required. Automatically populated by the *entity value*.
    - **Tags**

        - Free-text tags you can add to the indicator.
        - Optional. Automatically populated by the *incident ID*. You can add others.
    - **Name**

        - Name of the indicator. This name is what appears in your list of indicators.
        - Optional. Automatically populated by the *incident name*.
    - **Created by**

        - Creator of the indicator.
        - Optional. Automatically populated by the user signed in to Microsoft Sentinel.

    Fill in the remaining fields accordingly.

    - **Threat types**

        - The threat type represented by the indicator.
        - Optional. Free text.
    - **Description**

        - Description of the indicator.
        - Optional. Free text.
    - **Revoked**

        - Revoked status of the indicator. Select the checkbox to revoke the indicator. Clear the checkbox to make it active.
        - Optional. Boolean.
    - **Confidence**

        - Score that reflects confidence in the correctness of the data, by percent.
        - Optional. Integer, 1-100.
    - **Kill chains**

        - Phases in the [Lockheed Martin Cyber Kill Chain](https://www.lockheedmartin.com/en-us/capabilities/cyber/cyber-kill-chain.html#OVERVIEW) to which the indicator corresponds.
        - Optional. Free text.
    - **Valid from**

        - The time from which this indicator is considered valid.
        - Required. Date/time.
    - **Valid until**

        - The time at which this indicator should no longer be considered valid.
        - Optional. Date/time.

    ![Screenshot that shows entering information in the new threat indicator pane.](media/add-entity-to-threat-intelligence/new-indicator-panel.png)
2. When all the fields are filled in to your satisfaction, select **Apply**. A message appears in the upper-right corner to confirm that your indicator was created.
3. The entity is added as threat intelligence in your workspace. You can [search and filter threat intelligence](work-with-threat-indicators#search-and-filter-threat-intelligence). You can also query it by [finding and viewing threat intelligence with queries](work-with-threat-indicators#find-and-view-threat-intelligence-with-queries).