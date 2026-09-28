---
layout: Conceptual
title: Plan Defender for Servers roles and permissions - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/plan-defender-for-servers-roles
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Review roles and permissions for Microsoft Defender for Servers.
ms.topic: concept-article
ms.date: 2025-02-19T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 6f39ecd8-77b0-d41b-c093-f4e35d0c84e0
document_version_independent_id: fcf0c965-3cec-34af-7a78-bd273f4c743b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/plan-defender-for-servers-roles.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/plan-defender-for-servers-roles
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/plan-defender-for-servers-roles.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 68744f13-99c7-ecf8-6207-e0464dd7f292
---

# Plan Defender for Servers roles and permissions - Microsoft Defender for Cloud | Microsoft Learn

This article helps you understand how to control access to Defender for Servers. Defender for Servers is one of the paid plans provided by [Microsoft Defender for Cloud](defender-for-cloud-introduction).

## Before you begin

This article is the *second* article in the Defender for Servers planning guide. Before you begin, review the earlier articles:

1. Start [planning your deployment](plan-defender-for-servers).

## Determine ownership and access

It's critical that you identify ownership for server and endpoint security in your organization. Ownership that's undefined or hidden increases security risk, making it more difficult for SecOps team to identity and follow threats across enterprise silos.

- Security leadership should identify the teams, roles, and individuals that are responsible for making and implementing decisions about server security. [Review cloud security functions](/en-us/azure/cloud-adoption-framework/organize/cloud-security) to get started.
- Responsibility is usually shared between a [central IT team](/en-us/azure/cloud-adoption-framework/organize/central-it) and a [cloud infrastructure and endpoint security team](/en-us/azure/cloud-adoption-framework/organize/cloud-security-infrastructure-endpoint). Individuals on these teams need access rights to manage and use Defender for Cloud.
- During planning, determine the right level of access for individuals based on the Defender for Cloud role-based access control (RBAC) model.

## Defender for Cloud roles

In addition to the built-in Owner, Contributor, and Reader roles for Azure subscriptions and resource groups, Defender for Cloud has built-in roles to control access.

Learn more about [roles and allowed actions](permissions#roles-and-allowed-actions) in Defender for Cloud.