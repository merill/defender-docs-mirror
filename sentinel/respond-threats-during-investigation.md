---
layout: Conceptual
title: Respond to Threat Actors During Investigations and Threat Hunts in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/respond-threats-during-investigation
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
description: Take response actions against threat actors directly from Microsoft Sentinel investigations and threat hunts. Use playbooks with the entity trigger to respond without leaving the investigation context.
ms.author: guywild
author: guywi-ms
ms.reviewer: noak
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 409b5d32-371e-a57e-4ae7-9fdef00c0e80
document_version_independent_id: 9908c137-e004-49eb-94a6-4148e28432d7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/respond-threats-during-investigation.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/respond-threats-during-investigation
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/respond-threats-during-investigation.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 0f66a9d4-2104-5fe1-9abe-b01db463d641
---

# Respond to Threat Actors During Investigations and Threat Hunts in Microsoft Sentinel | Microsoft Learn

This article shows you how to take response actions against threat actors on the spot, during the course of an incident investigation or threat hunt, without pivoting or context switching out of the investigation or hunt. You accomplish this using playbooks based on the new entity trigger.

The entity trigger currently supports the following entity types:

- [Account entity reference](entities-reference#account)
- [Host entity reference](entities-reference#host)
- [IP address entity reference](entities-reference#ip)
- [URL entity reference](entities-reference#url)
- [DNS entity reference](entities-reference#dns-resolution)
- [File hash entity reference](entities-reference#file-hash)

Important

The **entity trigger** is currently in **PREVIEW**. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

## Run playbooks with the entity trigger

When you're investigating an incident, and you determine that a given entity - a user account, a host, an IP address, a file, and so on - represents a threat, you can take immediate remediation actions on that threat by running a playbook on-demand. You can do likewise if you encounter suspicious entities while proactively hunting for threats outside the context of incidents.

1. Select the entity in whichever context you encounter it, and choose the appropriate means to run a playbook, as follows:

    - In the **Entities** widget on an incident's **Overview tab** in the [new incident details page](investigate-incidents#explore-the-incidents-entities) (now in Preview), or in its [**Entities tab**](investigate-incidents#entities-tab), choose an entity from the list, select the three dots next to the entity, and select **Run playbook (Preview)** from the pop-up menu.

        ![Screenshot of incident details page.](media/respond-threats-during-investigation/incident-details-overview.png)

        ![Screenshot of entities tab on incident details page.](media/respond-threats-during-investigation/entities-tab.png)
    - In an incident's **Entities** tab, choose the entity from the list and select the **Run playbook (Preview)** link at the end of its line in the list.

        ![Screenshot of selecting entity from incident details page to run a playbook on it.](media/respond-threats-during-investigation/incident-details-page.png)
    - From the **Investigation graph**, select an entity and select the **Run playbook (Preview)** button in the entity side panel.

        ![Screenshot of selecting an entity from the investigation graph to run a playbook on it.](media/respond-threats-during-investigation/investigation-graph.png)
    - From the **Entity behavior** page, select an entity. From the resulting entity page, select the **Run playbook (Preview)** button in the left-hand panel.

        ![Screenshot of selecting an entity from the entity behavior page to run a playbook on it.](media/respond-threats-during-investigation/entity-behavior-page.png)

        ![Screenshot of the selected entity page to run a playbook on an entity.](media/respond-threats-during-investigation/entity-page.png)
2. Selecting **Run playbook (Preview)** from any of the views described in step 1 opens the **Run playbook on *&lt;entity type&gt;*** panel.

    ![Screenshot of Run playbook on entity panel.](media/respond-threats-during-investigation/run-playbook-on-entity.png)

    In the **Run playbook on *&lt;entity type&gt;*** panel, you'll see two tabs: **Playbooks** and **Runs**.
3. In the **Playbooks** tab, you'll see a list of all the playbooks that you have access to and that use the **Microsoft Sentinel Entity** trigger for the selected entity type (for example, user accounts). Select the **Run** button for the playbook you want to run it immediately.

    If you don't see the playbook you want to run in the list, it means Microsoft Sentinel doesn't have permissions to run playbooks in that resource group.

    To grant those permissions, select **Settings &gt; Settings &gt; Playbooks permissions &gt; Configure permissions**. In the **Manage permissions** panel, mark the check boxes of the resource groups containing the playbooks you want to run, and select **Apply**.

    For more information, see [Extra permissions required for Microsoft Sentinel to run playbooks](automation/automate-responses-with-playbooks#extra-permissions-required-for-microsoft-sentinel-to-run-playbooks).
4. You can audit the activity of your entity-trigger playbooks in the **Runs** tab. You'll see a list of all the times any playbook has been run on the entity you selected. It might take a few seconds for any just-completed run to appear in this list. Selecting a specific run will open the full run log in Azure Logic Apps.