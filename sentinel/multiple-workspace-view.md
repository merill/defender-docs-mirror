---
layout: Conceptual
title: Work with Microsoft Sentinel incidents in many workspaces at once | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/multiple-workspace-view
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
description: How to view incidents in multiple workspaces concurrently in Microsoft Sentinel.
ms.author: guywild
author: guywi-ms
ms.reviewer: idpelleg
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 19540897-96a9-4323-861a-7ea7c266f8f8
document_version_independent_id: 0ebd649a-69ce-923d-0c1d-919f1ece75eb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/multiple-workspace-view.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/multiple-workspace-view
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/multiple-workspace-view.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: 44fea384-c6e2-11eb-aedd-e0744277e105
---

# Work with Microsoft Sentinel incidents in many workspaces at once | Microsoft Learn

To take full advantage of Microsoft Sentinel’s capabilities, Microsoft recommends using a single-workspace environment. However, there are some use cases that require having several workspaces, in some cases – for example, that of a [Managed Security Service Provider (MSSP)](multiple-tenants-service-providers) and its customers – across multiple tenants. **Multiple workspace view** lets you see and work with security incidents across several workspaces at the same time, even across tenants, allowing you to maintain full visibility and control of your organization’s security responsiveness.

Note

For information about feature availability in US Government clouds, see the Microsoft Sentinel tables in [Cloud feature availability for US Government customers](/en-us/azure/security/fundamentals/feature-availability).

If you onboard Microsoft Sentinel to the Microsoft Defender portal, see:

- [Multiple Microsoft Sentinel workspaces in the Defender portal](/en-us/azure/sentinel/workspaces-defender-portal)
- [Microsoft Defender multitenant management](/en-us/defender-xdr/mto-overview)

## Enter multiple-workspace view

When you open Microsoft Sentinel, you're presented with a list of all the workspaces to which you have access rights, across all selected tenants and subscriptions. Selecting the name of a single workspace brings you into that workspace. To choose multiple workspaces, select all the corresponding checkboxes, and then select the **View incidents** button at the top of the page.

Important

Multiple Workspace View now supports a maximum of 100 concurrently displayed workspaces.

In the list of workspaces, you can see the directory, subscription, location, and resource group associated with each workspace. The directory corresponds to the tenant.

![Screenshot of selecting multiple workspaces.](media/multiple-workspace-view/workspaces.png)

## Work with incidents across workspaces

Multiple workspace view is currently available only for incidents. The multiple workspace view incidents page looks and functions in most ways like the regular [Incidents](investigate-cases) page, with the following important differences:

[![Screenshot of viewing incidents across multiple workspaces.](media/multiple-workspace-view/incidents.png)](media/multiple-workspace-view/incidents.png#lightbox)

- The counters at the top of the page - *Open incidents*, *New incidents*, *Active incidents*, etc. - show the numbers for all of the selected workspaces collectively.
- You see incidents from all of the selected workspaces and directories (tenants) in a single unified list. You can filter the list by workspace and directory, in addition to the filters from the regular **Incidents** screen.
- You need to have read and write permissions on all the workspaces from which you've selected incidents. If you have only read permissions on some workspaces, you see warning messages if you select incidents in those workspaces. You aren't able to modify those incidents or any others you've selected together with those (even if you do have permissions for the others).
- If you choose a single incident and select **View full details** or **Actions** &gt; **Investigate**, you'll from then on be in the data context of the selected incident's workspace and no others.