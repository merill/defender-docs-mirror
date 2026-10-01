---
layout: Conceptual
title: Automatic Attack Disruption in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-business/mdb-attack-disruption
breadcrumb_path: /defender-business/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Automatic attack disruption helps businesses limit ransomware damage. Learn how Defender for Business contains threats and gives your team time to respond.
author: chrisda
ms.author: chrisda
ms.date: 2024-06-07T00:00:00.0000000Z
ms.topic: article
ms.service: defender-business
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.reviewer: efratka
locale: en-us
document_id: c12a64ce-6d66-4076-8a3c-8660b594c44d
document_version_independent_id: c12a64ce-6d66-4076-8a3c-8660b594c44d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-business/mdb-attack-disruption.md
site_name: Docs
depot_name: Learn.defender-business
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdb-attack-disruption
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-business/mdb-attack-disruption.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b11ae577-8d18-47ab-998c-ea182a941e71
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/87b1d24d-826d-4337-90a0-b6c35e4561f2
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: b334a62b-206e-4bcb-1767-7a1f6444971f
---

# Automatic Attack Disruption in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn

A human-operated attack is an active attack with the following goals:

- Infiltrate the organization.
- Elevate their privileges.
- Navigate the network.
- Deploy ransomware or steal information.

These types of attacks can be catastrophic to business operations. They tend to be difficult to address and sometimes continue to threaten business operations after the initial encounter. For more information, see [Human-operated ransomware attacks](/en-us/security/ransomware/human-operated-ransomware#human-operated-ransomware-attacks).

Automatic attack disruption is designed to:

- Contain advanced attacks that are in progress.
- Limit the effect and progression of attacks on your devices.
- Provide more time for your security team to fully remediate an attack.

This article describes how automatic attack disruption works in Microsoft Defender for Business, how to view details about an attack, and how to get these capabilities.

## How automatic attack disruption works

Automatic attack disruption uses insights from Microsoft Security researchers and advanced AI models to counteract the complexities of advanced attacks. It limits an attacker's progress early on and dramatically reduces the overall effect of an attack, from associated costs to loss of productivity. See some examples at the [Microsoft Security Blog](https://aka.ms/ContainUserSecBlog).

By using automatic attack disruption, as soon as a human-operated attack is detected on a device, the system takes steps to contain the affected device and user accounts on the device. The system creates an incident in the Microsoft Defender portal: https://security.microsoft.com. Your IT or security team can view details about the risk and containment status of compromised assets during and after the process. An **Incident** page provides details about the attack and up-to-date status of affected assets.

Automated response actions include:

- Containing a device by blocking incoming or outgoing communication
- Containing a user account by disconnecting current user connections at the device level

Important

- To view information about a detected advanced attack, you must have an appropriate role, such as Security Reader or Security Administrator.
- To take remediation actions, release a contained device/user, or re-enable a user account, you must have the Security Administrator role.

For more information, see [Security roles and permissions in Defender for Business](mdb-roles-permissions).

## View details about an attack in the Microsoft Defender portal

1. In the Microsoft Defender portal, go to **Incidents**.
2. Select an incident that's tagged with *Attack Disruption*.
3. Review the incident graph. You can get the entire attack story and assess the attack disruption effect and status.
4. When you're ready to release a contained device or user account, or re-enable a user account, take one of the following steps:

    - To release a contained device, select the device, and then select **Release from containment**.
    - To release a contained user, select the user account, and then, in the side pane, select **Undo**.

Disrupted incidents include a tag for `Attack Disruption` and the specific threat type identified, such as ransomware. If your IT or security team receives [incident email notifications](mdb-email-notifications), these tags also appear in the emails.

When an incident is disrupted, highlighted text appears below the incident title. Contained devices or user accounts are listed with a label that indicates their status.

## Track attack disruption actions in the Action center

The [Action center](mdb-review-remediation-actions) brings together all remediation and response actions, whether those actions were taken automatically or manually. You can view all automatic attack disruption actions in the Action center. After your IT or security team mitigates the risk and completes the investigation of an incident, they can release contained assets.

1. In the Microsoft Defender portal, go to **Actions & submissions** &gt; **Action center**.
2. Select the **History** tab.
3. Select an action, such as **Contain user** or **Contain device**, and then choose **Undo**.

For more information, see [Review remediation actions in the Action center](mdb-review-remediation-actions).

## How to get automatic attack disruption

Automatic attack disruption is built into Defender for Business. You don't have to explicitly turn on these capabilities. It's important to [onboard all your organization's devices](mdb-onboard-devices) (computers, phones, and tablets) to Defender for Business so that they're protected as soon as possible.

Additionally, sign up to receive [preview features](/en-us/defender-xdr/preview) so that you get the latest and greatest capabilities as soon as they're available.