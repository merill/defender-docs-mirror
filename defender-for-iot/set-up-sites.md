---
layout: Conceptual
title: Set up and create sites for site security with Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-iot/set-up-sites
breadcrumb_path: /defender-for-iot/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Create and configure sites in the Defender portal's Site security page so security teams can monitor and assess the security status of OT production environments.
ms.service: defender-for-iot
author: limwainstein
ms.author: lwainstein
ms.localizationpriority: medium
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: d9d5f722-4d5a-90c6-9316-34ee67377296
document_version_independent_id: d9d5f722-4d5a-90c6-9316-34ee67377296
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-iot/set-up-sites.md
site_name: Docs
depot_name: Learn.defender-for-iot
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: set-up-sites
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-iot/set-up-sites.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1438b371-d010-4b69-a622-5b0950c389fc
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/86b71af1-f926-4f84-ad97-652864405350
platformId: a441e0c0-446a-ca1f-b107-2b2c786c8b00
---

# Set up and create sites for site security with Microsoft Defender for IoT in the Defender portal - Microsoft Defender for IoT | Microsoft Learn

Microsoft Defender for IoT in the Microsoft Defender portal includes the **Site security** page, which offers an overview of the security state of your entire operational technology (OT) environment. Your organization's security team use this page to regularly monitor the security status of your production sites.

In this article, you learn how to set up a site in the **Site security** page. Before you begin, make sure you meet the prerequisites.

Learn more about the [site security benefits and use cases](site-security-overview).

Important

This article discusses Microsoft Defender for IoT in the Defender portal (Preview).

Some features are not yet available in the Defender portal. If you're interested in these features, or you're an existing customer working on the Azure portal, see the [Defender for IoT on Azure documentation](/en-us/azure/defender-for-iot/organizations/overview).

Learn more about the [Defender for IoT management portals](/en-us/defender-for-iot/microsoft-defender-iot#what-are-the-different-management-portals-for-microsoft-defender-for-iot).

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Prerequisites

Before you create a site, make sure you meet the following prerequisites:

- We recommend you have IP or MAC address details of at least one OT device at the site that is discovered by Microsoft Defender for Endpoint. You need these details when you associate devices with the site.
- Review [the general prerequisites for Microsoft Defender for IoT](prerequisites).
- Review the required site security permissions according to [RBAC requirements](set-up-rbac).
- Have a Microsoft Defender for IoT license. For more information, see [Get started with Defender for IoT](get-started).
- We recommend you have IP or MAC address details of at least one OT device at the site that is discovered by Microsoft Defender for Endpoint.

## Create a site

To set up a site and associate the OT devices in your network to it:

1. In the [Microsoft Defender portal](https://security.microsoft.com/machines) menu, select **Operational technology** &gt; **Site security**.
2. In the **Site security** page, select **Create new site** or **Create Your First Site**.
3. Type the following details:

    - **Site name**: A name for the site, for example, San Francisco.
    - **Location**: The physical location of the production site.
    - **Site description**: Describe the purpose of the site, what activities occur there, the types and number of devices used, and other important information about the site.
    - **Owners**: The contact emails of any users administering the site who must be contacted when problems occur.

    ![Screenshot showing the details for creating a new site in the Site security page of Microsoft Defender for IoT in the Microsoft Defender portal.](media/set-up-sites/site-security-set-up-details.png)
4. When completed, select **Next** to associate devices to the site.

## Associate devices with a site

In this stage, you configure Defender for IoT to associate devices to the site, so Defender for IoT can correctly identify and associate all types of devices at the same site.

1. In the search bar, type either:

    - A public IP address
    - The IP/MAC address for a specific device located at this site
    - The name of a specific device located at this site (can be an OT, IT, network, enterprise IoT device, and so on)

    A list of suggested sites appears in the table.
2. If you don't know any of the site's device addresses:

    1. Select **Show all suggestions**.

        A list of all possible sites appears in the table. Each row in the table represents a suggested site location based on the devices in that location.
    2. Open the location and check that at least one of these devices exists at your site.

        Check each location, because Defender for IoT might list your devices in more than one suggested location. If Defender for IoT lists your devices in more than one suggested location, select all of the suggested locations that include an identified device. You can select any number of locations. However, you can't edit the list of devices that appear at a specific location.
3. Review the devices and select the suggested sites to associate with the site. You might need to select more than one suggested site.

    Use the **Group** column to check the ID for each suggested site. Sites with the same ID indicate that the devices are likely located at the same physical location. Because suggested sites with the same Group ID are expected to belong to the same physical site, review and confirm that the listed devices are correct before you associate those suggested sites.

    [![Screenshot showing the associate devices screen and the suggested list of OT devices per location with the Group column in the site set-up page of Microsoft Defender for IoT in the Microsoft Defender portal.](media/set-up-sites/site-security-associate-group.png)](media/set-up-sites/site-security-associate-group.png#lightbox)
4. Select **Next** to review the site details.

Note

Currently, devices discovered in the Defender portal aren't synchronized with the Azure portal, and therefore the list of devices discovered could be different in each portal.

## Preview devices before assigning them to a site

In this stage, you review all of the devices discovered by Defender for IoT. This gives admins the opportunity to review and remove devices before confirming the site creation. A list of all devices to be associated with this site is displayed.

To manage devices in bulk, use the search bar to find devices by their name, IP, or MAC address.

If, during your editing, you want to reset the device list to its original state, selecting **Discard all changes** undoes any device exclusions and restores the initial device selection.

To remove any of the devices from this list:

1. Select **Deselect devices from site**. All of the devices become editable.
2. Deselect the checkbox of the devices to be removed.

    1. To reset the device list to its original state, select **Discard all changes**.

    [![Screenshot of the site associtation preview devices page](media/set-up-sites/site-security-associate-device-list-preview.png)](media/set-up-sites/site-security-associate-device-list-preview.png#lightbox)
3. When you're finished, select **Next**. The confirmation box appears.

    1. Select **Confirm** to change the list of devices to associate with this site and removal of any unchecked devices.
    2. If you haven't made changes, select **Skip**.

Important

When you exclude a specific device from site association, it is no longer assigned to sites based on network parameters. If the device is later moved to a different location, you’ll need to manually update its site settings, as automatic updates will not apply.

## Review site details

Review the information for the site you want to create:

1. Review the selected OT devices. If needed, select **Edit devices** to return to the **Associate devices** screen.
2. Select **Complete**.

    The site is now set up and appears in the **Site security** page.

    Regarding device data:

    - The site data in the **Device Inventory** under **Site tag** and **Site attribute** starts to appear after each OT device performs network activity and contacts the Defender portal. For some devices, this happens quickly, but for other devices, the data takes time to appear in the inventory. When the site tag and attribute data appears, the device is protected by Defender for IoT, including all of the security value, such as alerts, vulnerabilities, and more.
    - Any new devices that are added to the network are automatically detected and added to the **Device Inventory**. If a device is moved to a different or new location within the network, the device's location and site association in the **Device Inventory** are updated automatically.
3. Select **Create device group** to create a device group now, or select **Close** and [set up a device group at a later stage](/en-us/defender-endpoint/machine-groups).

## Add a device group to a site

Use a device group to make sure that the correct users have access to the site. To create a device group:

1. Select **Create device group**.

    The **Settings &gt; Endpoints &gt; Device groups** page opens.
2. Select **Add device group** and type a device group name.
3. Select the remediation level, type a description, and select **Next**.

    The **Devices** page opens.
4. Type the value for the **Tag** condition in the format: *Site: &lt;Site name&gt;*. For example, *Site: San Francisco*.
5. Select **Next**.

    The **Preview devices** page opens with a list of devices in the group.
6. Select **Next**.

    The **User access** page opens.
7. Filter the user groups or select the user groups to add to the device group.
8. Select **Submit** and select **Done**.

    Your device group is now set up and appears in the device groups list.

## Rank device groups

If a device group lists different preferences for the same user, you need to rank the importance of each device group.

To move a group up or down, drag the row to the correct position in the list. For more information, see [ranking device groups in Microsoft Defender for Endpoint](/en-us/defender-endpoint/machine-groups).

## Assign device group roles and permissions

To get the full benefit of the device group you created, you might need to create roles and permission settings. For more information, see [role based access control in Microsoft Defender for Endpoint](/en-us/defender-endpoint/rbac), and [create and manage roles in Microsoft Defender for Endpoint](/en-us/defender-endpoint/user-roles).