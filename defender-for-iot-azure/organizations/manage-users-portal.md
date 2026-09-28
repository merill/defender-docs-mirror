---
layout: Conceptual
title: Manage Azure Users for Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-iot/organizations/manage-users-portal
breadcrumb_path: ../breadcrumb/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-iot-blog/bg-p/MicrosoftDefenderIoTBlog
feedback_help_link_type: ask-the-community
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
ms.service: defender-for-iot
author: limwainstein
manager: bagol
ms.author: lwainstein
description: Learn how to manage user permissions in the Azure portal for Microsoft Defender for IoT services.
ms.date: 2026-06-12T00:00:00.0000000Z
ms.topic: how-to
ms.collection:
- zerotrust-extra
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 71864f1b-d40c-83a7-6949-7a6f172fea92
document_version_independent_id: eb34e557-046a-d3e1-e57c-9ef42c10a5e3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot-azure/organizations/manage-users-portal.md
site_name: Docs
depot_name: Azure.d4iot-azure
page_type: conceptual
toc_rel: toc.json
asset_id: defender-for-iot/organizations/manage-users-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot-azure/organizations/manage-users-portal.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: 4a9f2855-6875-c362-c4aa-b407fbc7ad94
---

# Manage Azure Users for Microsoft Defender for IoT - Microsoft Defender for IoT | Microsoft Learn

## Manage user access

Microsoft Defender for IoT provides tools both in the Azure portal and on-premises for managing user access across Defender for IoT resources.

In the Azure portal, user management is managed at the *subscription* level with [Microsoft Entra ID](/en-us/azure/active-directory/) and [Azure role-based access control (RBAC)](/en-us/azure/role-based-access-control/overview). Assign Microsoft Entra users with Azure roles at the subscription level so that they can add or update Defender for IoT pricing plans, access device data, and manage sensors.

For OT network monitoring, Defender for IoT has the extra *site* level, which you can use to add granularity to your user management. For example, assign roles at the site level to apply different permissions for the same users across different sites.

Note

Site-based access control is currently in PREVIEW. The [Azure Preview Supplemental Terms](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include other legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

## Define Azure users for Defender for IoT per subscription

Use Azure RBAC to manage user access for Defender for IoT. Assign roles to users or user groups so they can access the features they need.

- [Grant a user access to Azure resources using the Azure portal](/en-us/azure/role-based-access-control/quickstart-assign-role-user-portal)
- [Grant a group access to Azure resources using Azure PowerShell](/en-us/azure/role-based-access-control/tutorial-role-assignments-group-powershell)
- [Azure user roles for OT and Enterprise IoT monitoring](roles-azure)

## Manage site-based access control (Public preview)

Define [Defender for IoT roles and permissions](roles-azure#roles-and-permissions-reference) per Defender for IoT site as part of a [Zero Trust security strategy](concept-zero-trust) to add a level of granularity to your Azure access policies. Defender for IoT sites generally reflect many devices grouped in a specific geographical location, such as the devices in an office building at a specific address.

Site-based access control activities also allow you to check the following details:

- Check your own access to the site, or check access to the site for other users, groups, service principals, or managed identities
- View current role assignments on the site, including role assignments that have been denied specific actions on the site
- View a full list of roles available for the site

Note

Sites and site-based access control is relevant only for OT monitoring sites, and isn't supported for default sites or Enterprise IoT monitoring.

To manage site-based access control:

1. In the Azure portal, go to the **Defender for IoT** &gt; **Sites and sensors** page, and select the OT site where you want to assign permissions.
2. In the **Edit site** pane that appears on the right, select **Manage site access control (Preview)**. For example:

    [![Screenshot of the site-based access option from the Sites and sensors page.](media/release-notes/site-based-access.png)](media/release-notes/site-based-access.png#lightbox)

    An **Access control** page opens in Defender for IoT for your site. This **Access control** page is the same interface as is available directly from the **Access control** tab on any Azure resource.

    For example:

    [![Screenshot of the Access Control page for site-based access control.](media/manage-users-portal/access-control-site.png)](media/manage-users-portal/access-control-site.png#lightbox)

For more information about site-based access control and user roles, see:

- [Azure user roles and permissions for Defender for IoT](roles-azure)
- [Grant a user access to Azure resources using the Azure portal](/en-us/azure/role-based-access-control/quickstart-assign-role-user-portal)
- [List Azure role assignments using the Azure portal](/en-us/azure/role-based-access-control/role-assignments-list-portal)
- [Check access for a user to Azure resources](/en-us/azure/role-based-access-control/check-access)