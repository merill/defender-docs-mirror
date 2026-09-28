---
layout: Conceptual
title: Create and manage device groups in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/machine-groups
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Create device groups and set automated remediation levels on them by confirming the rules that apply on the group
ms.service: defender-endpoint
ms.author: painbar
author: paulinbar
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.topic: how-to
ms.subservice: onboard
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 4e5399b5-6742-9700-5ce0-ad429be2139c
document_version_independent_id: 4e5399b5-6742-9700-5ce0-ad429be2139c
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/machine-groups.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: machine-groups
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/machine-groups.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
platformId: 53389e05-033c-808d-4621-aa430594cdcc
---

# Create and manage device groups in Microsoft Defender for Endpoint - Microsoft Defender for Endpoint | Microsoft Learn

## Overview

Note

Device group creation is supported in Defender for Endpoint Plan 1 and Plan 2.

In an enterprise scenario, security operation teams are typically assigned a set of devices. These devices are grouped together based on a set of attributes such as their domains, computer names, or designated tags.

In Microsoft Defender for Endpoint, you can create device groups and use them to:

- Limit access to related alerts and data to specific Microsoft Entra user groups that have [assigned RBAC roles](rbac)
- Configure different auto-remediation settings for different sets of devices
- Assign specific remediation levels to apply during automated investigations
- In an investigation, filter the **Devices list** to specific device groups by using the **Group** filter.

You can create device groups in the context of role-based access (RBAC) to control who can take specific action or see information by assigning the device group(s) to a user group. For more information, see [Manage portal access using role-based access control](rbac).

Tip

For a comprehensive look into RBAC application, read: [Is your SOC running flat with RBAC](https://techcommunity.microsoft.com/t5/Windows-Defender-ATP/Is-your-SOC-running-flat-with-limited-RBAC/ba-p/320015).

As part of the process of creating a device group, you'll:

- Set the automated remediation level for that group. For more information on remediation levels, see [Use Automated investigation to investigate and remediate threats](automated-investigations).
- Specify the matching rule that determines which devices belong to the device group based on the device name, domain, tags, and OS platform. If a device is also matched to other groups, it's added only to the highest ranked device group.
- Select the Microsoft Entra user group that should have access to the device group.
- Rank the device group relative to other groups after it's created.

Note

A device group is accessible to all users if you don't assign any Microsoft Entra groups to it.

## Create a device group

Note

Device Groups in Defender for Business are managed differently. For more information, see [Device groups in Microsoft Defender for Business](/en-us/defender-business/mdb-create-edit-device-groups).

Note

You can create up to 2,000 device groups per tenant.

Important

Before you begin, make sure the Microsoft Entra user groups you want to assign are already configured with [RBAC roles](rbac).

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Settings** &gt; **Endpoints** &gt; **Permissions** section &gt; **Device groups**. Or, to go directly to the device groups tab, use https://security.microsoft.com/securitysettings/endpoints/machine_groups.
2. On the device groups tab, select **Add device group**.
3. The **Add device group** wizard opens. On the **General** page, configure the following settings:

    - **Device group name**: Enter a unique, descriptive name for the device group.
    - **Remediation level**: Select one of the following values:
        - **No automated response**
        - **Semi - Approval required for all folders**
        - **Semi - Approval required for non-temporary folders**
        - **Semi - Approval required for system folders**
        - **Full remediation**
    - **Description**: Enter an optional description.

    Select **Next**
4. On the **Devices** page, configure the matching rule that determines which devices belong to the group. You can define conditions based on device name, domain, tags, and OS platform. Devices that match all specified conditions are added to the group. For information about how matching rules and automated investigations work together, see [How the automated investigation starts](automated-investigations#how-the-automated-investigation-starts).

    Tip

    To use tagging for grouping devices, see [Create and manage device tags](machine-tags).

    Select **Next**.
5. On the **Preview devices** page, select **Show preview** to show up to 10 devices that match the device rule you configured on the previous page. If you're satisfied with the previewed devices, select **Next**.
6. On the **User access** page, assign the user groups that can access the device group you created.

    Note

    You can only grant access to Microsoft Entra user groups that have been assigned to RBAC roles.

    When you're ready to create the device group, select **Submit**.

## Manage device groups

You can promote or demote the rank of a device group so that it's given higher or lower priority during matching. A device group with a rank of 1 is the highest ranked group. When a device is matched to more than one group, it's added only to the highest ranked group. You can also edit and delete groups.

Warning

Deleting a device group may affect email notification rules. If a device group is configured under an email notification rule, it will be removed from that rule. If the device group is the only group configured for an email notification, that email notification rule will be deleted along with the device group.

By default, device groups are accessible to all users with portal access. You can change the default behavior by assigning Microsoft Entra user groups to the device group.

Devices that aren't matched to any groups are added to Ungrouped devices (default) group. You cannot change the rank of this group or delete it. However, you can change the remediation level of this group, and define the Microsoft Entra user groups that can access this group.

Note

Applying changes to device group configuration may take up to several minutes. In some environments, changes can take several hours to fully propagate. For example, new device groups might not appear as filter options under **Assets** &gt; **Devices** for up to several hours after creation.

### Add device group definitions

A device group definition can include multiple values for each condition. You can set multiple tags, device names, and domains to the definition of a single device group.

1. Create a new device group, then select **Devices** tab.
2. Add the first value for one of the conditions.
3. Select `+` to add more rows of the same property type.

Tip

Use the 'OR' operator between rows of the same condition type, which allows multiple values per property. You can add up to 10 rows (values) for each property type - tag, device name, domain.

For more information about device group definitions, see [Device groups - Microsoft 365 security](https://sip.security.microsoft.com/homepage).