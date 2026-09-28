---
layout: Conceptual
title: Multitenant identities - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/multitenant-identities-inventory
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: A multi-tenant identity inventory
ms.service: defender-xdr
author: guywi-ms
ms.author: guywild
ms.topic: article
ms.date: 2025-06-29T00:00:00.0000000Z
ms.custom: sfi-ga-nochange
locale: en-us
document_id: a1b7ff54-c13e-59e6-6454-4a27313a72ed
document_version_independent_id: a1b7ff54-c13e-59e6-6454-4a27313a72ed
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/multitenant-identities-inventory.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: multitenant-identities-inventory
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/multitenant-identities-inventory.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 32a6e2a1-e939-3c8f-f87e-8a8ae1d2e186
---

# Multitenant identities - Microsoft Defender XDR | Microsoft Learn

The **Identities** page in multitenant management enables you to quickly manage tenants and identities.

## Identity inventory

The Identity inventory page lists all the identities in each tenant that you have access to. The page is like the [Defender for Identity inventory](/en-us/defender-for-identity/identity-inventory) with the addition of the **Tenant name** column and filter.

You can navigate to the identity inventory page by selecting **Assets &gt; Identities** in Microsoft Defender XDR's navigation menu.

[![Screenshot of inventory.](media/multitenant-identities-inventory/screenshot-of-inventory.png)](media/multitenant-identities-inventory/screenshot-of-inventory.png#lightbox)

At the top of the page, the following identities counts are available for all tenants:

**Total**: The total number of identities.

**Critical:** The number of your critical assets.

**Disabled:** The number of all disabled identities in your organization.

**Services:** The number of all service accounts both on-premises and cloud.

You can use this information to help you prioritize identities for security posture improvements.

Highly privileged identities card helps you investigate in Advanced hunting all sensitive accounts in your organization, including Microsoft Entra ID security administrators and Global admin users.

There are several options you can choose from to customize the identities list view. On the top navigation you can:

- Add or remove columns.
- Apply filters.
- Search for an identity by name or full UPN, SID, and Object ID.
- Export the list to a CSV file.
- Copy list link with the included filters configured.

Note

When exporting the identities list to a CSV file, a maximum of 5,000 identities are displayed.

To view full identity details, select a specific identity from the list. Tenant ID and Tenant name are available in the identity side panel and page:

![Screenshot of tenant details on identity.](media/multitenant-identities-inventory/screenshot-of-tenant-details-on-identity.png)