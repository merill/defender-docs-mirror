---
layout: Conceptual
title: Device groups in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-business/mdb-create-edit-device-groups
breadcrumb_path: /defender-business/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Device groups in Defender for Business let you apply security policies to specific devices. Learn how to create, view, and manage device groups in the portal.
author: chrisda
ms.author: chrisda
ms.topic: how-to
ms.service: defender-business
ms.localizationpriority: medium
ms.reviewer: nehabha
ms.date: 2026-07-03T00:00:00.0000000Z
ms.collection:
- SMB
- m365-security
- m365-initiative-defender-business
- tier1
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 94d76a90-9f80-fb38-4c09-3a6826f87096
document_version_independent_id: 94d76a90-9f80-fb38-4c09-3a6826f87096
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-business/mdb-create-edit-device-groups.md
site_name: Docs
depot_name: Learn.defender-business
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdb-create-edit-device-groups
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-business/mdb-create-edit-device-groups.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b11ae577-8d18-47ab-998c-ea182a941e71
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/87b1d24d-826d-4337-90a0-b6c35e4561f2
platformId: c6984848-6b6f-27e9-0366-986cb23aacc6
---

# Device groups in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn

In Defender for Business, you apply policies to devices through collections called *device groups*.

## What is a device group?

A *device group* is a collection of devices grouped together based on specified criteria, such as operating system version. Devices that meet the criteria are included in that device group, unless you exclude them. In Defender for Business, you apply policies to devices by using device groups.

Defender for Business includes default device groups that you can use. The default device groups include all the devices that you onboard to Defender for Business. For example, there's a default device group for Windows devices. When you onboard Windows devices, you automatically add them to the default device group.

You can also create new device groups to assign policies with specific settings to certain devices. For example, you might have a firewall policy assigned to one set of Windows devices, and a different firewall policy assigned to another set of Windows devices. You can define specific device groups to use with your policies.

Note

As you create policies in Defender for Business, the system assigns an order of priority. If you apply multiple policies to a given set of devices, those devices receive the first applied policy only. For more information, see [Understand policy order in Defender for Business](mdb-policy-order).

All device groups, including your default device groups and any custom device groups that you define, are stored in [Microsoft Entra ID](/en-us/entra/fundamentals/what-is-entra).

## Create a new device group

In Defender for Business, a *policy* is a set of security configuration settings that are applied to devices. You create device groups from within the policy creation or editing workflow.

Currently, you can create a new device group while you're creating or editing a policy, as described in the following procedure:

1. Go to the [Microsoft Defender portal](https://security.microsoft.com) and sign in.
2. In the navigation pane, choose **Configuration management** and select **Device configuration**.
3. Take one of the following actions:

    - Select an existing policy, and then choose **Edit**.
    - Choose **+ Add** to create a new policy.

    Tip

    To get help creating or editing a policy, see [View or edit policies in Defender for Business](mdb-view-edit-create-policies).
4. On the **General information** page, review the information, edit if necessary, and then choose **Next**.
5. Choose **+ Create new group**.
6. Specify a name and description for the device group, and then choose **Next**.
7. Select the devices to include in the group, and then choose **Create group**.
8. On the **Device groups** step, review the list of device groups for the policy. If needed, remove a group from the list. Then choose **Next**.
9. On the **Configuration settings** page, review and edit settings as needed, and then choose **Next**. For more information about these settings, see [Configuration settings](mdb-next-generation-protection).
10. On the **Review your policy** step, review all the settings, make any needed edits, and then choose **Create policy** or **Update policy**.

## View an existing device group

Currently, in Defender for Business, you can view your existing device groups while you are in the process of creating or editing a policy, as described in the following procedure:

1. Go to the [Microsoft Defender portal](https://security.microsoft.com) and sign in.
2. In the navigation pane, choose **Device configuration**.
3. Take one of the following actions:

    - Select an existing policy, and then choose **Edit**.
    - Choose **+ Add** to create a new policy.

    Tip

    To get help creating or editing a policy, see [View or edit policies in Defender for Business](mdb-view-edit-create-policies).
4. On the **General information** step, review the information, edit if necessary, and then select **Next**.
5. Select **Use existing group**. A flyout opens and displays device groups. If you don't have any device groups yet, it prompts you to create a new device group.

## What does the Add All Devices option do?

When you create or edit a policy, you might see the **Add all devices** option.

![Screenshot of the Add All Devices option.](media/add-all-devices-option.png)

Microsoft Intune is the service that manages and tracks your devices. If you select this option, all devices in Intune get the current policy.