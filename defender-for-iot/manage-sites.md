---
layout: Conceptual
title: Manage sites for Microsoft Defender for IoT in the Microsoft Defender portal - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-iot/manage-sites
breadcrumb_path: /defender-for-iot/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to manage site information in the Site security page, including updating device site associations, editing or deleting sites, and adding device groups in the Microsoft Defender portal.
ms.service: defender-for-iot
author: limwainstein
ms.author: lwainstein
ms.localizationpriority: medium
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: c1fefcec-7a37-9041-c8e2-7f271a7646f3
document_version_independent_id: c1fefcec-7a37-9041-c8e2-7f271a7646f3
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot/manage-sites.md
site_name: Docs
depot_name: Learn.defender-for-iot
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: manage-sites
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot/manage-sites.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 055096e8-0673-a73a-a157-014a9d9b1984
---

# Manage sites for Microsoft Defender for IoT in the Microsoft Defender portal - Microsoft Defender for IoT | Microsoft Learn

Microsoft Defender for IoT in the Microsoft Defender portal includes the **Site security** page, which allows you to see the up-to-date security state of your production sites. Learn more about the [site security benefits and use cases](site-security-overview) or how to [monitor site security](monitor-site-security).

When you manage a site, you might need to edit or delete the site information listed in the **Site security** page. Use the **Site security** page to update device site associations, edit or delete a site, and add a device group in the Microsoft Defender portal.

Important

This article discusses Microsoft Defender for IoT in the Defender portal (Preview).

Some features are not yet available in the Defender portal. If you're interested in these features, or you're an existing customer working on the Azure portal, see the [Defender for IoT on Azure documentation](/en-us/azure/defender-for-iot/organizations/overview).

Learn more about the [Defender for IoT management portals](/en-us/defender-for-iot/microsoft-defender-iot#what-are-the-different-management-portals-for-microsoft-defender-for-iot).

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Manually update device site association

Security admininstrators can manually assign or modify the site location for a device. Manually assigning a site overrides the automatic site association created when making the site.

To quickly update a group of devices, select multiple devices from the inventory and set the site for all of the selected devices simulataneously.

**To change the site associated with a device**:

1. Select **Assets -&gt; Devices** to open the **Device Inventory**.
2. Select the device, or group of devices, to update. A list of action buttons appear at the top of the Device Inventory table.
3. Select **Set site**. The **Set site** pane opens.

    [![Screenshot of the set site button in the device inventory table for changing the site location setting](media/manage-sites/set-site-from-inventory-boxed.png)](media/manage-sites/set-site-from-inventory-boxed.png#lightbox)
4. In **Set site manually**, open the **Select site** drop down list and select the site to associate with this device. If you want to leave a device unassociated with a specific site, select **Unassigned**.

    [![Screenshot of the set site manually drop down list for changing the site location setting](media/manage-sites/device-set-site-manually.png)](media/manage-sites/device-set-site-manually.png#lightbox)
5. Select **Save and close**.
6. The Set site confirmation box appears. Select **Confirm** to finalize the change. Finalizing the change prevents automatic site reassignment based on existing site security rules. The manual site assignment remains until the device is reset manually.

Note

For managing an entire site, instead of manually changing each individual device to a new site, it is recommended to go to **Site security** and use the **Edit site** wizard to more efficiently manage the site and the devices associated to it. For more information, see [Monitor site security](monitor-site-security).

## Edit or delete a site

To edit or delete a site:

1. In the [Microsoft Defender portal](https://security.microsoft.com/machines) menu, select **Operational technology** &gt; **Site security**.
2. Select the ellipsis (![](media/manage-sites/menu-ellipsis.png) ) to the right of the site name.
3. Select one of the following:

    - Select **Edit site** to open the **Site details** pane, where you can make changes to the site. For more information, see [Site details](set-up-sites).
    - Select **Delete site** to remove a site from the site list.

        Warning

        Deleting a site removes all site-related information for the associated devices. This action can't be undone.

## Add a device group to a site

You can create a device group based on a site location to restrict access to a specific site or group of sites, and verify that the correct users have access to your site.

You can set up a device group at different stages:

- To set up a device group as part of the site setup, see [Add a device group](set-up-sites#add-device-group).
- To set up a device group after you set up a site, see [Create and manage device groups](/en-us/defender-endpoint/machine-groups).

To get the full benefit of a site-based device group, you might need to create roles and permission settings. For more information, see:

- [Role based access control in Microsoft Defender for Endpoint](/en-us/defender-endpoint/rbac)
- [Create and manage roles in Microsoft Defender for Endpoint](/en-us/defender-endpoint/user-roles)