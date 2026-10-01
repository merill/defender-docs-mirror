---
layout: Conceptual
title: Understand Policy Order in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-business/mdb-policy-order
breadcrumb_path: /defender-business/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Policy order in Microsoft Defender for Business determines which settings devices receive. Learn how priority works and how to change the order of custom policies.
author: chrisda
ms.author: chrisda
ms.topic: overview
ms.service: defender-business
ms.localizationpriority: medium
ms.date: 2025-09-23T00:00:00.0000000Z
ms.reviewer: nehabha
ms.collection:
- SMB
- m365-security
- tier1
ms.custom: sfi-image-nochange
locale: en-us
document_id: 1b191750-6b73-08c3-bd12-c653e4153755
document_version_independent_id: 1b191750-6b73-08c3-bd12-c653e4153755
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-business/mdb-policy-order.md
site_name: Docs
depot_name: Learn.defender-business
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdb-policy-order
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-business/mdb-policy-order.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b11ae577-8d18-47ab-998c-ea182a941e71
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/87b1d24d-826d-4337-90a0-b6c35e4561f2
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: e2154b6d-953e-2a71-aa19-038d46271c1a
---

# Understand Policy Order in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn

Defender for Business includes [predefined policies](mdb-view-edit-create-policies#default-policies-in-defender-for-business) to help ensure user devices are protected. Your security team can [add new policies](mdb-view-edit-create-policies#create-a-new-policy) as well.

For example, suppose that your security team wants to apply different settings to different groups of devices. They can accomplish this goal by adding more next-generation protection policies or firewall policies. As you add policies, policy order comes into play.

## Policy order in Defender for Business

When you add policies, a priority order is assigned to all policies in the group, as shown in the following screenshot:

[![Screenshot showing multiple policies and policy order column.](media/mdb-deviceconfig-multpolicies.png)](media/mdb-deviceconfig-multpolicies.png#lightbox)

The **Order** column lists the priority for each policy. Predefined policies move down in priority order when you add new policies. You can edit the order of priority for policies you create. Select a policy, and then choose **Change order**. You can't change the priority of default policies. They're always last.

For example, suppose you have three next-generation protection policies that apply to Windows client devices. The default policy is priority 3 (last) and you can't change it. You can change the priority of policies 1 and 2 (switch places).

When multiple policies apply to a device, the device receives the policy with the highest priority only. After the settings of the highest priority policy are applied, policy processing for that type of policy stops. In the preceding example, the affected Windows client devices get the next-generation policy with priority 1. The devices never receive policies 2 and 3.

## Key points to remember about policy order

- Policies automatically get assigned a priority.
- You can change the priority for custom policies, but not for default policies.
- Default policies always get the lowest priority as you add new policies.
- Devices receive the first applied policy only, even if the devices are included in multiple policies.