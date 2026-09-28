---
layout: Conceptual
title: Manage Microsoft Sentinel platform solutions | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/sentinel/isv/manage-platform-solutions
breadcrumb_path: ../breadcrumb/toc.json
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
description: Learn how to configure, update, and uninstall components installed by a Microsoft Sentinel platform solution.
ms.topic: how-to
ms.author: monaberdugo
author: mberdugo
ms.reviewer: tbeerthuis
ms.date: 2025-09-18T00:00:00.0000000Z
locale: en-us
document_id: e2810df3-94b2-9fcd-7c95-49dd09dff3f7
document_version_independent_id: fa21d0fd-5aff-f3b6-b7a4-311906600024
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/sentinel/isv/manage-platform-solutions.md
site_name: Docs
depot_name: Azure.sentinel-azure
page_type: conceptual
toc_rel: ../toc.json
asset_id: sentinel/isv/manage-platform-solutions
moniker_range_name: 
monikers: []
item_type: Content
source_path: sentinel/isv/manage-platform-solutions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
platformId: b9941716-1c49-b173-b2d9-ba97a928272a
---

# Manage Microsoft Sentinel platform solutions | Microsoft Learn

After you install a Microsoft Sentinel platform solution, you manage its components in different places. This article explains how to configure, update, and uninstall the main types of components.

## Security Copilot agents

### Configure

Manage Security Copilot agents in the [Security Copilot portal](https://securitycopilot.microsoft.com), where you can enable, disable, or schedule them. For an overview of agent types, see [Microsoft Security Copilot agents overview](/en-us/copilot/security/agents-overview).

### Update

Agents update automatically when Microsoft releases a new version in the [Microsoft Security Store](https://security.microsoft.com/securitystore). Make sure your environment stays compatible to avoid breaking changes.

### Uninstall

Uninstalling the solution doesn’t remove the agent from the catalog. Enabled or scheduled agents keep running until you disable them in the portal. This behavior prevents unexpected disruption.

## Notebooks and notebook jobs

### Configure

Use the Microsoft Sentinel Jobs page to enable, disable, schedule, or view notebook jobs. You can also review notebook content and execution history.

### Update

To update notebooks or jobs, go to the [Microsoft Security Store](https://security.microsoft.com/securitystore), find the solution, and install the latest version. This deployment overwrites existing notebooks and jobs that share the same name. Each solution and publisher uses unique names to prevent conflicts.

Important

Installing the updated solution deletes local edits, such as changes made in Visual Studio Code.

### Uninstall

Uninstalling a solution doesn’t stop its notebook jobs. Jobs continue running until you disable them on the Microsoft Sentinel Jobs page.