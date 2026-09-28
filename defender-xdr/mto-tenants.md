---
layout: Conceptual
title: Manage tenants with Microsoft Defender multitenant management - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/mto-tenants
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about the tenant list in Microsoft Defender multitenant management
ms.service: defender-xdr
author: guywi-ms
ms.author: guywild
ms.collection:
- m365-security
- highpri
- tier1
- usx-security
ms.topic: concept-article
ms.date: 2024-08-19T00:00:00.0000000Z
locale: en-us
document_id: 438278f2-b8a2-6d18-d673-686d387ef82e
document_version_independent_id: 438278f2-b8a2-6d18-d673-686d387ef82e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/mto-tenants.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mto-tenants
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/mto-tenants.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 97cdaa02-d825-4ca3-82ec-566aade77995
---

# Manage tenants with Microsoft Defender multitenant management - Microsoft Defender XDR | Microsoft Learn

Add or remove tenants from the settings page in Microsoft Defender multitenant management.

## View the tenants page

To view the list of tenants that appear in multitenant management, go to [Settings page](https://mto.security.microsoft.com/mtosettings) in Microsoft Defender multitenant management:

[![Screenshot of Microsoft Defender multitenant management](media/mto-tenants/mto-tenant-settings.png)](media/mto-tenants/mto-tenant-settings.png#lightbox)

From the **Settings** page you can:

- **Add a tenant**: Select **Add tenants** &gt; Choose the tenants to want to add &gt; Select **Add tenant**.
- Select a tenant from the list to open the [Microsoft Defender portal](https://security.microsoft.com) for that tenant.
- **Remove a tenant**: Select the tenant you'd like to remove &gt; select **Remove**.

## Multitenant management status indicator

The multitenant management status indicator provides information on whether data issues exist for the page you're viewing, such as data loading issues or permissions issues. The indicator appears in the bottom right corner of the page:

When no issue exists, the status indicator is a green tick:

- ![No data issues](media/mto-tenants/mto_nodata_issue.png)

When an issue exists, the status indicator shows a red warning sign:

- ![data issues](media/mto-tenants/mto-data-issues.png)

Hovering over the red warning sign displays the issues that occurred and the tenant information. By expanding each section, you see all the tenants with this issue.

- ![tenant data issues](media/mto-tenants/mto-tenantdata-issues.png)