---
layout: Conceptual
title: Managing end-to-end lifecycle of deprecated solutions in Microsoft Sentinel | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/sentinel-solution-deprecation
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
description: This article walks you through the process of identifying deprecated solutions in Microsoft Sentinel and managing the lifecycle of these solutions.
author: mberdugo
ms.author: monaberdugo
ms.reviewer: tbeerthuis
ms.topic: concept-article
ms.date: 2025-12-30T00:00:00.0000000Z
locale: en-us
document_id: e2060f10-9008-9ce9-e591-a1040a4473e5
document_version_independent_id: 0acad1a9-dbb2-67b6-cc31-d3b0f277a6d9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/sentinel-solution-deprecation.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: toc.json
asset_id: sentinel/sentinel-solution-deprecation
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/sentinel-solution-deprecation.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
platformId: ee48d4f0-ac81-1bfc-78cc-f4e939701fb2
---

# Managing end-to-end lifecycle of deprecated solutions in Microsoft Sentinel | Microsoft Learn

The document explains how to manage the lifecycle of out-of-the-box solutions in Microsoft Sentinel that the solution author no longer supports. This document explains how to identify the solutions that are marked for deprecation and what actions to take on those solutions.

## Reasons for solution deprecation

Here are some of the primary reasons why Solutions are sometimes deprecated in Microsoft Sentinel:

- The software service provider stopped supporting the product or service that sends data to Microsoft Sentinel.
- The author who originally published the solution is no longer actively supporting the solution or providing critical updates.
- The product or service is acquired by another company necessitating ownership transfer to a different entity.

In these cases, users have to uninstall the original solution and install alternate solutions where available. For more information on how to delete/uninstall solutions in Microsoft Sentinel, see [Delete installed Microsoft Sentinel out-of-the-box content and solutions](/en-us/azure/sentinel/sentinel-solutions-delete).

Warning

Microsoft Sentinel solutions that are deprecated are no longer supported by Microsoft. They aren't updated and bugs aren't fixed. As a result, functionality and reliability can degrade over time. Continued use should be carefully evaluated, and migration to a supported alternative is recommended.

## Identifying solutions that are marked as deprecated

Solutions that are marked as deprecated can be identified using the **DEPRECATED** tag against the solution name in Microsoft Sentinel content hub. Solutions that are marked as deprecated are shown first in the content hub, followed by other solutions in alphabetical order.

[![Screenshot of solutions marked as deprecated in Microsoft Sentinel content hub.](media/sentinel-solution-deprecation/solution-marked-deprecated.png)](media/sentinel-solution-deprecation/solution-marked-deprecated.png#lightbox)

## Actions to take on solutions that are marked as deprecated

1. Navigate to Microsoft Sentinel content hub and look for solutions that are flagged as **DEPRECATED** and the status shows **Installed**.
2. Select the solution matching this criterion. If an alternate solution is available, **Navigate to solution** button is visible at the bottom of the solutions details view. If the **Navigate to solution** button isn't available, this means that there are no alternate solutions available. In this case, proceed with uninstalling the deprecated solution.

    [![Screenshot showing navigate to solution option in content hub.](media/sentinel-solution-deprecation/navigate-to-solution.png)](media/sentinel-solution-deprecation/navigate-to-solution.png#lightbox)
3. Select on **Navigate to solution** button to go to the alternate solution and then select the **Install** button to install the new solution.
4. After you install the new solution, you can proceed to uninstall the deprecated solution. Disconnect the data connectors and remove the other content items that were part of the deprecated solution. For more information, see [Delete installed Microsoft Sentinel out-of-the-box content and solutions](/en-us/azure/sentinel/sentinel-solutions-delete).
5. Configure the new solution. For more information, see [Discover and manage Microsoft Sentinel out-of-the-box content](/en-us/azure/sentinel/sentinel-solutions-deploy?tabs=azure-portal#discover-content).

Note

Before configuring the alternate solution, make sure to fully remove all the content items in the deprecated solution to ensure that data isn't duplicated.