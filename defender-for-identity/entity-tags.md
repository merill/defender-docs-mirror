---
layout: Conceptual
title: Entity tags in Microsoft Defender for Identity - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/entity-tags
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: Learn about when to use entity tags with Microsoft Defender for Identity and how to apply them in Microsoft Defender XDR.
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: LiorShapiraa
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 5853c03f-f14a-758b-7996-e26763aa2c81
document_version_independent_id: 5853c03f-f14a-758b-7996-e26763aa2c81
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/entity-tags.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: entity-tags
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/entity-tags.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://authoring-docs-microsoft.poolparty.biz/devrel/0b654e73-5728-4af3-8c2e-17bfbf4c9f23
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://authoring-docs-microsoft.poolparty.biz/devrel/11529658-843a-40bd-b2f8-5eed118be619
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 4829cf74-df4a-82c7-3880-42fc37990d3d
---

# Entity tags in Microsoft Defender for Identity - Microsoft Defender for Identity | Microsoft Learn

This article describes how to apply entity tags in Microsoft Defender for Identity. You can tag accounts as sensitive, as Exchange servers, or as honeytokens.

- Tag sensitive accounts so that detections work correctly. Some detections, like sensitive group changes, rely on this tag.

    Defender for Identity tags Exchange servers as sensitive by default. You can also tag devices as Exchange servers manually.
- Tag honeytoken accounts to set traps for malicious actors. These accounts are usually dormant. Any sign-in from a honeytoken account triggers an alert.

## Prerequisites

To set Defender for Identity entity tags in Microsoft Defender, you'll need Defender for Identity [deployed in your environment](deploy-defender-identity), and administrator or user access to Microsoft Defender.

For more information, see [Microsoft Defender for Identity role groups](role-groups).

## Tag entities manually

To manually tag an entity in Microsoft Defender XDR, such as a honeytoken account or an entity not automatically tagged as *Sensitive*, use the following steps:

1. Sign into [Microsoft Defender XDR](https://security.microsoft.com) and select **Settings** &gt; **Identities**.
2. Select the type of tag you want to apply: **Sensitive**, **Honeytoken**, or **Exchange server**.

    The page lists the entities already tagged in your system, listed on separate tabs for each entity type:

    - The *Sensitive* tag supports users, devices, and groups.
    - The *Honeytoken* tag supports users and devices.
    - The *Exchange server* tag supports devices only.
3. To tag additional entities, select the **Tag ...** button, such as **Tag users**. A pane opens on the right listing the available entities for you to tag.
4. Use the search box to find your entity if you need to. Select the entities you want to tag, and then select **Add selection**.

    For example:

    [![Screenshot of tagging user accounts as sensitive.](media/entity-tags/tag-entities.png)](media/entity-tags/tag-entities.png#lightbox)

## Default sensitive entities

The groups in the following list are considered **Sensitive** by Defender for Identity. Any entity that is a member of one of these Active Directory groups, including nested groups and their members, is automatically considered sensitive:

- Administrators
- Power Users
- Account Operators
- Server Operators
- Print Operators
- Backup Operators
- Replicators
- Network Configuration Operators
- Incoming Forest Trust Builders
- Domain Admins
- Domain Controllers
- Group Policy Creator Owners
- Read-only Domain Controllers
- Enterprise Read-only Domain Controllers
- Schema Admins
- Enterprise Admins
- Microsoft Exchange Servers

    Note

    Until September 2018, Remote Desktop Users were also automatically considered sensitive by Defender for Identity. Remote Desktop entities or groups added after this date are no longer automatically marked as sensitive while Remote Desktop entities or groups added before this date may remain marked as Sensitive. This Sensitive setting can now be changed manually.

In addition to these groups, Defender for Identity identifies the following high value asset servers and automatically tags them as **Sensitive**:

- Certificate Authority Server
- DHCP Server
- DNS Server
- Microsoft Exchange Server
- Replicating Directory Changes Permissions

## Supported integrations for entity tags

The following roles are designated as Sensitive by Microsoft Defender for Identity. Any entity assigned membership in these roles is automatically classified as sensitive.

### Okta sensitive roles

The following Okta roles are designated as Sensitive by Defender for Identity:

- Super Administrator
- Application Administrator
- Group Administrator
- API Access Management Administrator
- Group Membership Administrator
- Help Desk Administrator
- Mobile Administrator
- Organization Administrator
- Read-only Administrator
- Report Administrator

### CyberArk Identity sensitive roles

The following CyberArk Identity roles are designated as Sensitive by Defender for Identity:

- Administration Role
- Cloud Onboarding Admin
- Connector Management Admin
- Flows Admin
- Privilege Cloud Administrators
- Privilege Cloud Administrators Basic
- Privilege Cloud Administrators Lite
- Privilege Cloud Safe Managers
- Privilege Cloud Safe Managers Basic
- Privilege Cloud Safe Managers Lite
- Privilege Cloud Session Admin
- Privilege Cloud Session Risk Managers
- System Administrator

### SailPoint Identity Security Cloud sensitive roles

The following Entra ID and SailPoint Identity Security Cloud roles are used for sensitive entity tagging in Defender for Identity.

#### Entra ID roles used for tagging

The following Entra ID roles are designated as Sensitive by Defender for Identity:

- Global Administrator
- User Administrator
- Authentication Administrator
- Privileged Authentication Administrator
- Helpdesk Administrator
- Agent ID Administrator
- Application Administrator
- Directory Writers
- Domain Name Administrator
- Password Administrator
- Privileged Role Administrator
- Hybrid Identity Administrator
- Cloud Application Administrator

#### SailPoint Identity Security Cloud roles used for tagging

The following SailPoint Identity Security Cloud role is designated as Sensitive by Defender for Identity:

- IdentityNow Administrator