---
layout: Conceptual
title: Collaborate in Microsoft Teams with a Microsoft Sentinel incident team | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/collaborate-in-microsoft-teams
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
description: Learn how to connect to Microsoft Teams from Microsoft Sentinel to collaborate with others on your team using Microsoft Sentinel data.
ms.author: guywild
author: guywi-ms
ms.reviewer: idpelleg
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 343e3cd3-76ca-3d92-ff55-e54417865226
document_version_independent_id: 9bb54971-0476-4683-dfdb-038503e66a8a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/collaborate-in-microsoft-teams.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/collaborate-in-microsoft-teams
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/collaborate-in-microsoft-teams.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: a49fc13e-06eb-b5c0-ad5a-1b32048b5b80
---

# Collaborate in Microsoft Teams with a Microsoft Sentinel incident team | Microsoft Learn

Microsoft Sentinel in the Azure portal supports a direct integration with [Microsoft Teams](/en-us/microsoftteams/), enabling you to jump directly into teamwork on specific incidents.

Important

Integration with Microsoft Teams is currently in **PREVIEW**. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

## Overview

Integrating with Microsoft Teams directly from Microsoft Sentinel enables your teams to collaborate seamlessly across the organization, and with external stakeholders.

Use Microsoft Teams with a Microsoft Sentinel *incident team* to centralize your communication and coordination across the relevant personnel. Incident teams are especially helpful when used as a dedicated conference bridge for high-severity, ongoing incidents.

Organizations that already use Microsoft Teams for communication and collaboration can use the Microsoft Sentinel integration to bring security data directly into their conversations and daily work.

A Microsoft Sentinel incident team always has the most updated and recent data from Microsoft Sentinel, ensuring that your teams have the most relevant data right at hand.

## Required permissions

In order to create teams from Microsoft Sentinel:

- The user creating the team must have Incident write permissions in Microsoft Sentinel. For example, the [Microsoft Sentinel Responder](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-responder) role is an ideal, minimum role for this privilege.
- The user creating the team must also have permissions to create teams in Microsoft Teams.
- Any Microsoft Sentinel user, including users with the [Microsoft Sentinel Reader](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-reader), [Microsoft Sentinel Responder](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-responder), or [Microsoft Sentinel Contributor](/en-us/azure/role-based-access-control/built-in-roles#microsoft-sentinel-contributor) roles, can gain access to the created team by requesting access.

## Use an incident team to investigate

Investigate together with an *incident team* by integrating Microsoft Teams directly from your incident.

**To create your incident team**:

1. In Microsoft Sentinel, in the **Threat management** &gt; **Incidents** grid, select the incident you're currently investigating.
2. At the bottom of the incident pane that appears on the right, select **Actions** &gt; **Create team (Preview)**.

    [![Screenshot of the incident page with the option to create a Microsoft Teams team.](media/collaborate-in-microsoft-teams/create-team.png)](media/collaborate-in-microsoft-teams/create-team.png#lightbox)

    The **Incident team** pane opens on the right. Define the following settings for your incident team:

    - **Team name**: Automatically defined as the name of your incident. Modify the name as needed so that it's easily identifiable to you.
    - **Team description**: Enter a meaningful description for your incident team.
    - **Add groups and members**: Select one or more Microsoft Entra users and/or groups to add to your incident team. As you select users and groups, they will appear in the **Selected groups and users:** list below the **Add groups and members** list.

        Tip

        If you regularly work with the same users and groups, you may want to select the star ![](media/collaborate-in-microsoft-teams/save-as-favorite.png) next to each one in the **Selected groups and users** list to save them as favorites.

        Favorites are automatically selected the next time you create a team. If you want to remove a favorite from the next team you create, either select **Delete**![](media/collaborate-in-microsoft-teams/delete-user-group.png) , or select the star ![](media/collaborate-in-microsoft-teams/save-as-favorite.png) again to remove that user or group from your favorites altogether.
3. When you're done adding users and groups, select **Create team** to create your incident team.

    The incident pane refreshes, with a link to your new incident team under the **Team name** title.

    [![Screenshot of an incident showing the added link to the related Microsoft Teams team.](media/collaborate-in-microsoft-teams/teams-link-added-to-incident.jpg)](media/collaborate-in-microsoft-teams/teams-link-added-to-incident.jpg#lightbox)
4. Select your **Teams integration** link to switch into Microsoft Teams, where all of the data about your incident is listed on the **Incident page** tab.

    [![Screenshot of incident details and conversation thread available in Microsoft Teams.](media/collaborate-in-microsoft-teams/incident-in-teams.png)](media/collaborate-in-microsoft-teams/incident-in-teams.png#lightbox)

Continue the conversation about the investigation in Teams for as long as needed. You have the full incident details directly in Microsoft Teams.

Tip

- If you need to add individual users to your team, you can do so in Microsoft Teams using the **Add more people** button on the **Posts** tab.
- When you [close an incident](investigate-cases#close-an-incident), the related incident team you've created in Microsoft Teams is archived. If the incident is ever re-opened, the related incident team is also re-opened in Microsoft Teams so that you can continue your conversation, right where you left off.