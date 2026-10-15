---
layout: Conceptual
title: Group policy security assessments - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/security-posture-assessments/group-policy
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
description: This section provides security assessments related to Group Policy Objects (GPOs) in Active Directory environments.
ms.topic: article
ms.date: 2026-10-08T00:00:00.0000000Z
ms.reviewer: LiorShapiraa
ai-usage: ai-generated
locale: en-us
document_id: 1e55d9fe-c33c-5cee-894f-d2ed2f24f127
document_version_independent_id: 1e55d9fe-c33c-5cee-894f-d2ed2f24f127
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/security-posture-assessments/group-policy.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-posture-assessments/group-policy
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/security-posture-assessments/group-policy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/bcbcbad5-4208-4783-8035-8481272c98b8
- https://authoring-docs-microsoft.poolparty.biz/devrel/fcc3cd4a-59ea-47a2-9cc1-784142a5a25d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/43b2e5aa-8a6d-4de2-a252-692232e5edc8
- https://authoring-docs-microsoft.poolparty.biz/devrel/d7a55faf-a992-4e27-aa3a-eadc9830e778
platformId: 98f38c37-5d7a-a768-d259-a659347e27d5
---

# Group policy security assessments - Microsoft Defender for Identity | Microsoft Learn

Group policy security assessments identify Group Policy Objects (GPOs) that grant excessive access or expose credentials in your Active Directory environment.

## GPO assigns unprivileged identities to local groups with elevated privileges

**Description**

This recommendation identifies GPOs that grant unprivileged identities elevated access through membership in local groups.

Using a GPO to add users or groups to a local group can introduce a security risk when the resulting access exceeds their business requirements. For example, granting **Authenticated Users** or **Everyone** membership in the local **Administrators** or **Remote Desktop Users** group can provide broad administrative privileges or remote access to affected devices.

Attackers can exploit these group memberships to gain additional access and move laterally within the environment. Review the affected GPOs and restrict membership to identities that require the access.

**User impact**

Removing group memberships can prevent users, services, or applications from performing operations that depend on those memberships. Review business requirements and dependencies before making changes.

**Implementation**

1. Review the affected GPOs and the local group memberships they configure.
2. Identify unprivileged users or broadly scoped groups, such as **Authenticated Users** or **Everyone**, that receive unnecessary elevated privileges or remote access.
3. Modify the GPOs to remove unnecessary memberships. Retain only the users and groups that require access for their responsibilities.
4. Allow the updated policy to apply to affected devices, then verify that the resulting local group memberships meet your security and operational requirements.

## GPO can be modified by unprivileged accounts

**Description**

This recommendation lists any Group Policy Objects in your environment that can be modified by standard users which can potentially lead to the compromise of the domain.

Attackers may attempt to obtain information on Group Policy settings to uncover vulnerabilities that can be exploited to gain higher levels of access, understand the security measures in place within a domain, and identify patterns in domain objects. This information can be used to plan subsequent attacks, such as identifying potential paths to exploit within the target network or finding opportunities to blend in or manipulate the environment.

**User impact**

A user, service or application that relies on these permissions may stop functioning. 

**Implementation**

Carefully review each assigned permission, identify any dangerous permission granted, and modify them to remove any unnecessary or excessive user rights. 

## Reversible passwords found in GPOs

**Description**

This recommendation identifies GPOs that contain password data in Group Policy Preferences (GPP).

Group Policy Preferences previously allowed administrators to embed credentials in domain policies. [Security update MS14-025](/en-us/security-updates/securitybulletins/2014/ms14-025) removed the ability to configure and distribute passwords through the affected preference extensions because the passwords were stored insecurely.

However, applying the update doesn't remove previously configured password data. Files containing these credentials can remain in the domain's `SYSVOL` folder, where domain users can read them. The passwords can be decrypted using a publicly available AES key.

An attacker who obtains these credentials might use them to gain unauthorized access or elevate privileges. Remove existing preferences that contain embedded credentials.

**User impact**

Removing password-containing preferences can disrupt dependent configurations, such as mapped drives, scheduled tasks, services, local account management, or data source connections. Identify these dependencies and arrange an alternative that doesn't store passwords in Group Policy Preferences before removing the affected configuration.

**Implementation**

Use **Group Policy Management Console (GPMC)** on a domain controller or on a management computer with **Remote Server Administration Tools (RSAT)** installed.

1. In the recommendation's **Exposed entities** tab, identify the affected GPOs.
2. In GPMC, edit each reported GPO and locate the preference items that contain password data.
3. Review the affected configuration and its dependencies. Replace any required functionality with a configuration that doesn't store passwords in Group Policy Preferences.
4. If you need to remove the configured item from clients, use the cleanup action supported by that preference type. For example, to remove a scheduled task deployed by a preference, open the preference's properties, set **Action** to **Delete**, and select **Apply** and **OK**.

    [![Screenshot of a scheduled task preference with Delete highlighted in the Action list.](../media/reversible-passwords-group-policy/screenshot-of-group-policy-objects.png)](../media/reversible-passwords-group-policy/screenshot-of-group-policy-objects.png#lightbox)
5. Allow the policy changes to replicate and apply to affected clients. If you configured a cleanup action, verify that it completed on the affected clients before removing the preference item from the GPO.
6. Remove the password-containing preference items from the GPO. Verify that the password-containing preference data is no longer present in `SYSVOL` after replication.
7. Change the exposed account passwords and update legitimate dependencies. Removing the stored credentials doesn't invalidate passwords that might already have been obtained.
8. Repeat the procedure for all affected GPOs.

Important

Removing a preference item from a GPO doesn't necessarily remove settings that were previously applied to clients. The **Delete** action removes the configured item, such as a scheduled task or local user account, rather than just its stored password. Review the impact before applying a cleanup action. Don't delete an entire GPO when only individual preference items require remediation.

For more information, see [MS14-025: Vulnerability in Group Policy Preferences could allow elevation of privilege](https://support.microsoft.com/kb/2962486).