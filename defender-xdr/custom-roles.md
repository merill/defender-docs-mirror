---
layout: Conceptual
title: Custom roles for role-based access control - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/custom-roles
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn how to manage custom roles for Microsoft Defender in the Microsoft Defender XDR portal.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.date: 2025-04-25T00:00:00.0000000Z
ms.collection:
- m365-security
- tier3
ms.topic: concept-article
ms.custom: sfi-ga-nochange
locale: en-us
document_id: 8a8e8c06-6110-c157-fbe9-e8386e196075
document_version_independent_id: 8a8e8c06-6110-c157-fbe9-e8386e196075
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/custom-roles.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: custom-roles
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/custom-roles.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 6702e80f-6718-a07c-3608-9b3aa72da34a
---

# Custom roles for role-based access control - Microsoft Defender XDR | Microsoft Learn

By default, access to services available in the Microsoft Defender portal are managed collectively using [Microsoft Entra global roles](m365d-permissions). If you need greater flexibility and control over access to specific product data, and aren't yet using the [Microsoft Defender unified role-based access control (RBAC)](manage-rbac) for centralized permissions management, we recommend creating custom roles for each service.

For example, create a custom role for Microsoft Defender for Endpoint to manage access to specific Defender for Endpoint data, or create a custom role for Microsoft Defender for Office to manage access to specific email and collaboration data.

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Locate custom role management settings in the Microsoft Defender portal

Each Microsoft Defender service has its own custom role management settings, with some services being represented in a central location in the Microsoft Defender portal. To locate custom role management settings in the Microsoft Defender portal:

1. Sign in to the Microsoft Defender portal at https://security.microsoft.com.
2. In the navigation pane, select **Permissions**.
3. Select the **Roles** link for the service where you want to create a custom role. For example, for Defender for Endpoint:

[![Screenshot that shows Roles link for Defender for Endpoint.](media/custom-roles/custom-roles-endpoint.png)](media/custom-roles/custom-roles-endpoint.png#lightbox)

In each service, custom role names aren't connected to global roles in Microsoft Entra ID, even if similarly named. For example, a custom role named *Security Admin* in Microsoft Defender for Endpoint isn't connected to the global *Security Admin* role in Microsoft Entra ID.

## Reference of Defender portal service content

For information about the permissions and roles for each Microsoft Defender XDR service, see the following articles:

- [Microsoft **Defender for Cloud** user roles and permissions](/en-us/azure/defender-for-cloud/permissions)
- [Configure access for **Defender for Cloud Apps**](/en-us/defender-cloud-apps/manage-admins)
- [Create and manage roles in **Defender for Endpoint**](/en-us/defender-endpoint/user-roles)
- [Roles and permissions in **Defender for Identity**](/en-us/defender-for-identity/role-groups)
- [Microsoft **Defender for IoT** user management](/en-us/azure/defender-for-iot/organizations/manage-users-overview)
- [Microsoft **Defender for Office 365** permissions](/en-us/defender-office-365/mdo-portal-permissions)
- [Manage access to **Microsoft Defender**](m365d-permissions)
- [**Microsoft Security Exposure Management** permissions](/en-us/security-exposure-management/prerequisites#permissions)
- [Roles and permissions in **Microsoft Sentinel**](/en-us/azure/sentinel/roles)

Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.