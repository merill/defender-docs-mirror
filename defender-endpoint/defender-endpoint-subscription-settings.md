---
layout: Conceptual
title: Manage your Microsoft Defender for Endpoint subscription settings across client devices - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/defender-endpoint-subscription-settings
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn about your options for managing your Defender for Endpoint subscription settings. Choose Plan 1, Plan 2, or mixed mode.
author: limwainstein
ms.author: lwainstein
ms.topic: overview
ms.date: 2025-03-05T00:00:00.0000000Z
ms.service: defender-endpoint
ms.subservice: onboard
ms.localizationpriority: medium
ms.reviewer: shlomiakirav, efratka
ms.collection:
- M365-security-compliance
- m365initiative-defender-endpoint
ms.custom: sfi-ga-nochange
locale: en-us
document_id: 15f80267-8d91-3ac8-5a98-ff997805c56f
document_version_independent_id: 15f80267-8d91-3ac8-5a98-ff997805c56f
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/defender-endpoint-subscription-settings.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-endpoint-subscription-settings
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/defender-endpoint-subscription-settings.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8b9ae643-2e85-42b8-beb2-eef4bae8c4bc
- https://authoring-docs-microsoft.poolparty.biz/devrel/68cb9039-df60-49b0-8ef8-89ad96497f63
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/e047e27d-b5f3-43a8-b4b0-4f6dca95e7c9
- https://authoring-docs-microsoft.poolparty.biz/devrel/725b6df3-93e8-472d-834e-e7e0d2953d35
platformId: 5c24b89f-25dd-40d9-5222-444fa7a7b9f1
---

# Manage your Microsoft Defender for Endpoint subscription settings across client devices - Microsoft Defender for Endpoint | Microsoft Learn

In Defender for Endpoint, a mixed-licensing scenario is a situation in which an organization is using a mix of Defender for Endpoint Plan 1 and Plan 2 licenses. The following table describes examples of mixed-licensing scenarios:

| Scenario | Description |
| --- | --- |
| *Mixed tenant* | Use different sets of capabilities for groups of users and their devices. Examples include:- Defender for Endpoint Plan 1 and Defender for Endpoint Plan 2- Microsoft 365 E3 and Microsoft 365 E5 |
| *Mixed trial* | Try a premium level subscription for some users. Examples include: - Defender for Endpoint Plan 1 (purchased for all users), and Defender for Endpoint Plan 2 (a trial subscription has been started for some users)- Microsoft 365 E3 (purchased for all users), and Microsoft 365 E5 (a trial subscription has been started for some users) |
| *Phased upgrades* | Upgrade user licenses in phases. Examples include:- Moving groups of users from Defender for Endpoint Plan 1 to Plan 2- Moving groups of users from Microsoft 365 E3 to E5 |

You can manage your subscription settings to accommodate mixed licensing scenarios across client devices. These capabilities enable you to:

- **Set your tenant to mixed mode and tag devices** to determine which client devices will receive features and capabilities from each plan (we call this option *mixed mode*); **OR**,
- **Use the features and capabilities from one plan across all your client devices**.

You can also use a newly added license usage report to track status.

# [Use mixed mode](#tab/mixed)
To set your tenant to mixed mode and tag devices, follow the guidance on this tab.

Important

- **Mixed-mode settings apply to client endpoints only**. Tagging server devices won't change their subscription state. All server devices running Windows Server or Linux should have appropriate licenses, such as [Defender for Servers](/en-us/azure/defender-for-cloud/plan-defender-for-servers-select-plan). See [Options for onboarding servers](onboard-windows-server).
- **Make sure to follow the procedures in this article to try mixed-license scenarios in your environment**. Assigning user licenses in the Microsoft 365 admin center (https://admin.microsoft.com) doesn't set your tenant to mixed mode.
- **You should have active trial or paid licenses for both Defender for Endpoint Plan 1 and Plan 2**.
- To access license information, you must have one of the following roles assigned in Microsoft Entra ID:
    - Security Administrator
    - License Administrator and Defender for Endpoint Administrator

1. As an admin, go to the Microsoft Defender portal (https://security.microsoft.com) and sign in.
2. Go to **Settings** &gt; **Endpoints** &gt; **Licenses**. Your usage report opens and displays information about your organization's Defender for Endpoint licenses.
3. Under **Subscription state**, select **Manage subscription settings**.

    Note

    If you don't see **Manage subscription settings**, at least one of the following conditions is true:

    - You have Defender for Endpoint Plan 1 or Plan 2 (but not both); or
    - Mixed-license capabilities haven't rolled out to your tenant yet.
4. A **Subscription settings** flyout opens. Choose the option to use Defender for Endpoint Plan 1 and Plan 2. (No changes will occur until devices are tagged as per the next step.)
5. Tag the devices that should receive either Defender for Endpoint Plan 1 or Plan 2 capabilities. You can choose to tag your devices manually or by using a dynamic rule. Learn more about device tagging.

    | Method | Details |
    | --- | --- |
    | Tag devices manually | To tag devices manually, create a tag called `License MDE P1` and apply it to devices. To get help with this step, see [Create and manage device tags](machine-tags).Note that devices that are tagged with the `License MDE P1` tag using the [registry key method](machine-tags#create-tags) will not receive downgraded functionality. If you want to tag devices by using the registry key method, use a dynamic rule instead of manual tagging. |
    | Tag devices automatically by using a dynamic rule | *Dynamic rule functionality is new for mixed-license scenarios! It allows you to apply a dynamic and granular level of control over how you manage devices*. To use a dynamic rule, you specify a set of criteria based on device name, domain, operating system platform, and/or device tags. Devices that meet the specified criteria will receive the Defender for Endpoint Plan 1 or Plan 2 capabilities according to your rule. As you define your criteria, you can use the following condition operators: - `Equals` / `Not equals`- `Starts with`- `Contains` / `Does not contain`For **Device name**, you can use freeform text.For **Domain**, select from a list of domains.For **OS platform**, select from a list of operating systems.For **Tag**, use the freeform text option. Type the tag value that corresponds to the devices that should receive either Defender for Endpoint Plan 1 or Plan 2 capabilities. See the example in More details about device tagging. |

    Device tags are visible in the **Device inventory** view and in the [Defender for Endpoint APIs](/en-us/defender-vulnerability-management/tvm-supported-os).

    Note

    Dynamically added Defender for Endpoint P1 tags are not currently filterable in the Device inventory view.
6. Save your rule and wait for up to three (3) hours for tags to be applied. Then, proceed to Validate that a device is receiving only Defender for Endpoint Plan 1 capabilities.

### More details about device tagging

As described in [Tech Community blog: How to use tagging effectively](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/how-to-use-tagging-effectively-part-1/ba-p/1964058), device tagging provides you with granular control over devices. With device tags, you can:

- Display certain devices to individual users in the Microsoft Defender portal so that they see only the devices they're responsible for.
- Include or exclude devices from specific security policies.
- Determine which devices should receive Defender for Endpoint Plan 1 or Plan 2 capabilities.

For example, suppose that you want to use a tag called `VIP` for all the devices that should receive Defender for Endpoint Plan 2 capabilities. Here's what you would do:

1. Create a device tag called `VIP`, and apply it to all the devices that should receive Defender for Endpoint Plan 2 capabilities. Use one of the following methods to create your device tag:

    - [Add device tags using the portal](machine-tags#add-device-tags-using-the-portal).
    - [Add device tags by setting a registry key value](machine-tags#create-tags).
    - [Add or remove machine tags by using the Defender for Endpoint API](api/add-or-remove-machine-tags).
    - [Add device tags by creating a custom profile in Microsoft Intune](machine-tags#create-tags).
2. Set up a dynamic rule using the condition operator `Tag Does not contain VIP`. In this case, all devices that do not have the `VIP` tag will receive the `License MDE P1` tag and Defender for Endpoint Plan 1 capabilities.

# [Use one plan](#tab/oneplan)
To use the features and capabilities from one plan across all your devices, follow the guidance on this tab.

Important

To access license information, you must have one of the following roles assigned in Microsoft Entra ID:

- Security Administrator
- License Administrator and Defender for Endpoint Administrator

1. Go to the Microsoft Defender portal (https://security.microsoft.com) and sign in as a Security Administrator.
2. Go to **Settings** &gt; **Endpoints** &gt; **Licenses**.
3. Under **Subscription state**, select **Manage subscription settings**.

    Note

    If you don't see **Manage subscription settings**, at least one of the following conditions is true:

    - You have Defender for Endpoint Plan 1 or Plan 2 (but not both); or
    - Mixed-license capabilities haven't rolled out to your tenant yet.
4. A **Subscription settings** flyout opens. Choose one plan for all users and devices, and then select **Done**. It can take up to three hours for your changes to be applied.

    If you chose to apply Defender for Endpoint Plan 1 to all devices, proceed to Validate that devices are receiving only Defender for Endpoint Plan 1 capabilities.

---

Microsoft Defender for Business isn't supported for mixed-license scenarios. If you're using Defender for Business and you want to switch to Defender for Endpoint Plan 2, contact support. For more information, see [Change your endpoint security subscription](/en-us/defender-business/mdb-manage-subscription).

Important

If you want to run multiple security solutions side by side, see [Considerations for performance, configuration, and support](/en-us/defender-endpoint/mde-side-by-side).

You might have already configured mutual security exclusions for devices onboarded to Microsoft Defender for Endpoint. If you still need to set mutual exclusions to avoid conflicts, see [Add Microsoft Defender for Endpoint to the exclusion list for your existing solution](/en-us/defender-endpoint/switch-to-mde-phase-2#step-2-add-microsoft-defender-for-endpoint-to-the-exclusion-list-for-your-existing-solution).

Important

Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

## Validate that a device is receiving only Defender for Endpoint Plan 1 capabilities

After you have assigned Defender for Endpoint Plan 1 capabilities to some or all devices, you can verify that an individual device is receiving those capabilities.

1. In the Microsoft Defender portal (https://security.microsoft.com), go to **Assets** &gt; **Devices**.
2. Select a device that is tagged with `License MDE P1`. You should see that Defender for Endpoint Plan 1 is assigned to the device.

Note

Devices that are assigned Defender for Endpoint Plan 1 capabilities don't have any vulnerabilities or security recommendations listed.

## Review license usage

The license usage report is estimated based on sign-in activities on the device. Defender for Endpoint Plan 2 licenses are per user, and each user can have up to five concurrent, onboarded devices. To learn more about license terms, see [Microsoft Licensing](https://www.microsoft.com/en-us/licensing/default).

To reduce management overhead, there's no requirement for device-to-user mapping and assignment. Instead, the license report provides a utilization estimation that is calculated based on device usage seen across your organization. It might take up to one day for your usage report to reflect the active usage of your devices.

Important

To access license information, you must have one of the following roles assigned in Microsoft Entra ID:

- Security Administrator
- License Administrator and Defender for Endpoint Administrator

1. Go to the Microsoft Defender portal (https://security.microsoft.com) and sign in.
2. Choose **Settings** &gt; **Endpoints** &gt; **Licenses**.
3. Review your available and assigned licenses. The calculation is based on detected users who have accessed devices that are onboarded to Defender for Endpoint.