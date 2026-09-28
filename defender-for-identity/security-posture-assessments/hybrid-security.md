---
layout: Conceptual
title: Remediate Hybrid Security Posture Assessments in Defender for Identity - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/security-posture-assessments/hybrid-security
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
description: View all hybrid security posture assessments for Microsoft Defender for Identity.
ms.topic: how-to
ms.date: 2026-08-18T00:00:00.0000000Z
ms.reviewer: LiorShapiraa
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1020
locale: en-us
document_id: bc5ae5a2-e7c0-0816-6b69-30bf2c737b43
document_version_independent_id: bc5ae5a2-e7c0-0816-6b69-30bf2c737b43
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/security-posture-assessments/hybrid-security.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-posture-assessments/hybrid-security
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/security-posture-assessments/hybrid-security.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/57eae307-c3a1-4cac-b645-1a899934bac8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/ee561821-1ac7-45a8-9409-6ba5eb7a5b97
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 305914a7-7de5-2a78-c465-eeb985889b6b
---

# Remediate Hybrid Security Posture Assessments in Defender for Identity - Microsoft Defender for Identity | Microsoft Learn

This article lists all hybrid security posture assessments for Microsoft Defender for Identity.

Note

While assessments are updated in near real time, scores and statuses are updated every 24 hours. While the list of impacted entities is updated within a few minutes of your implementing the recommendations, the status may still take time until it's marked as **Completed**.

## Change password for Microsoft Entra seamless SSO account

The **Change password for Microsoft Entra seamless SSO account** assessment lists all Microsoft Entra seamless SSO computer accounts with password last set over 90 days ago.

### User impact

Microsoft Entra seamless SSO automatically signs in users when they're using their corporate desktops that are connected to your corporate network. Seamless SSO provides your users with easy access to your cloud-based applications without using any other on-premises components. When setting up Microsoft Entra Seamless SSO, a computer account named AZUREADSSOACC is created in Active Directory. By default, the password for this Azure SSO computer account isn't automatically updated every 30 days. The AZUREADSSOACC account password functions as a shared secret between AD and Microsoft Entra, enabling Microsoft Entra to decrypt Kerberos tickets used in the seamless SSO process between Active Directory and Microsoft Entra ID. If an attacker gains control of this account, they can generate service tickets for the AZUREADSSOACC account on behalf of any user and impersonate any user within the Microsoft Entra tenant that has been synchronized from Active Directory.

### Implementation

1. Review the recommended action at https://security.microsoft.com/securescore?viewid=actions for *Change password for Microsoft Entra seamless SSO account*.
2. Review the list of exposed entities to discover which of your Microsoft Entra SSO computer accounts have a password more than 90 days old.
3. Take appropriate action on those accounts by following the steps described in [how to roll over the Microsoft Entra SSO account password](https://aka.ms/RollOverAzureadssoAccount) article.

Note

The **Change password for Microsoft Entra seamless SSO account** security assessment is available only if Microsoft Defender for Identity sensor is installed on servers running Microsoft Entra Connect services and Sign on method as part of Microsoft Entra Connect configuration is set to single sign-on and the SSO computer account exists. Learn more about [Microsoft Entra seamless sign-on](/en-us/entra/identity/hybrid/connect/how-to-connect-sso).

## Ensure no privileged SaaS app accounts exist outside of IdP control

The **Ensure no privileged SaaS app accounts exist outside of IdP control** assessment lists privileged accounts that are created and managed directly in SaaS applications instead of through the organization's identity provider.

### User impact

Privileged local accounts in SaaS apps can bypass centralized identity controls, including single sign-on, multifactor authentication, Conditional Access, lifecycle governance, and security monitoring. If an attacker compromises one of these accounts, they may be able to sign in directly to the SaaS application and access sensitive data without triggering the protections applied to identities managed by the identity provider.

### Implementation

1. Review the recommended action in the Microsoft Defender portal for **Ensure no privileged SaaS app accounts exist outside of IdP control**.
2. Review the list of exposed entities to identify privileged SaaS accounts that aren't managed by your identity provider.
3. Migrate required privileged access to identities managed by the identity provider.
4. Disable or remove app-native privileged accounts that are no longer required.
5. Apply single sign-on, multifactor authentication, Conditional Access, and lifecycle governance to remaining privileged SaaS access.

## Rotate password for Microsoft Entra Connect AD DS Connector account

The **Rotate password for Microsoft Entra Connect AD DS Connector account** assessment lists all MSOL accounts in your organization with password last set over 90 days ago.

### User impact

Smart attackers are likely to target Microsoft Entra Connect in on-premises environments, and for good reason. The Microsoft Entra Connect server can be a prime target, especially based on the permissions assigned to the AD DS Connector account (created in on-premises AD with the MSOL\_ prefix).

It's important to change the password of MSOL accounts every 90 days to prevent attackers from allowing use of the high privileges that the connector account typically holds - replication permissions, reset password and so on.

### Implementation

1. Review the recommended action at [Microsoft Secure Score actions](https://security.microsoft.com/securescore?viewid=actions) for *Rotate password for Microsoft Entra Connect AD DS Connector account*.
2. Review the list of exposed entities to discover which of your AD DS Connector accounts have a password more than 90 days old.
3. Take appropriate action on those accounts by following the steps on [how to change the AD DS Connector account password](https://aka.ms/MicrosoftEntraIdPasswordChangeSyncService).

Note

The **Rotate password for Microsoft Entra Connect AD DS Connector account** security assessment is only available if Microsoft Defender for Identity sensor is installed on servers running Microsoft Entra Connect services.

## Remove unnecessary replication permissions for Microsoft Entra Connect AD DS Connector account

Smart attackers are likely to target Microsoft Entra Connect in on-premises environments, and for good reason. The Microsoft Entra Connect server can be a prime target, especially based on the permissions assigned to the AD DS Connector account (created in on-premises AD with the MSOL\_ prefix). In the default 'express' installation of Microsoft Entra Connect, the connector service account is granted replication permissions, among others, to ensure proper synchronization. If [Password Hash Sync](/en-us/entra/identity/hybrid/connect/whatis-phs) (a feature that synchronizes password hashes from on-premises AD to Microsoft Entra ID) isn’t configured, it’s important to remove unnecessary permissions to minimize the potential attack surface.

Note

- The **Remove unnecessary replication permissions for Microsoft Entra Connect AD DS Connector account** security assessment is available only if Microsoft Defender for Identity sensor is installed on servers running Microsoft Entra Connect services.
- If the Password Hash Sync (PHS) sign-on method is set up, AD DS Connector accounts with replication permissions won't be affected because those permissions are necessary.
- For environments with multiple Microsoft Entra Connect servers, it’s crucial to install sensors on each server to ensure Microsoft Defender for Identity can fully monitor your setup. If Microsoft Defender for Identity detects that your Microsoft Entra Connect configuration doesn't use Password Hash Sync, replication permissions aren't necessary for the accounts in the Exposed Entities list. Ensure that each exposed MSOL account isn't required for Replication Permissions by any other applications.

### Implementation

1. Review the recommended action at https://security.microsoft.com/securescore?viewid=actions for Remove unnecessary replication permissions for *Microsoft Entra Connect AD DS Connector account*.
2. Review the list of exposed entities to discover which of your AD DS Connector accounts have unnecessary replication permissions.
3. Take appropriate action on those accounts and remove their 'Replication Directory Changes' and 'Replication Directory Changes All' permissions by unchecking the following permissions:

![Screenshot that shows the list of permissions for Microsoft Entra Connect.](../media/remove-replication-permissions-microsoft-entra-connect/replicationconfiguration.png)

## Remove unsafe permissions on sensitive Microsoft Entra Connect accounts

Microsoft Entra Connect accounts like AD DS Connector account (also known as MSOL\_) and Microsoft Entra Seamless Single Sign-On (SSO) computer account (AZUREADSSOACC) have powerful privileges, including replication and password reset rights. If these accounts are granted unsafe permissions, attackers could exploit them to gain unauthorized access, escalate privileges, or take control of hybrid identity infrastructure. This could lead to account takeovers, unauthorized directory modifications, and a broader compromise of both on-premises and cloud environments.

Note

The **Remove unsafe permissions on sensitive Microsoft Entra Connect accounts** security assessment is available only if Microsoft Defender for Identity sensor is installed on servers running Microsoft Entra Connect services and Sign on method as part of Microsoft Entra Connect configuration is set to single sign-on and the SSO computer account exists. Learn more about **[Microsoft Entra seamless sign-on](/en-us/entra/identity/hybrid/connect/how-to-connect-sso)**.

### Implementation

1. Review the recommended action at [Microsoft Secure Score actions](https://security.microsoft.com/securescore?viewid=actions) for *Remove unsafe permissions on sensitive Microsoft Entra Connect accounts*.
2. Review the list of exposed entities to identify accounts with unsafe permissions. For example:

    ![Screenshot of exposed entities.](../media/remove-unsafe-permissions-sensitive-entra-connect/screenshot-of-exposed-entities.png)
3. If you select on "Click to expand" you can find more details about the granted permissions. For example:

    [![Screenshot of excessive permissions](../media/remove-unsafe-permissions-sensitive-entra-connect/screenshot-of-excessive-permissions.png)](../media/remove-unsafe-permissions-sensitive-entra-connect/screenshot-of-excessive-permissions.png#lightbox)
4. For each exposed account, remove problematic permissions that allow unprivileged accounts to takeover critical hybrid assets.

## Replace Enterprise or Domain Admin account for Microsoft Entra Connect AD DS Connector account

Smart attackers often target Microsoft Entra Connect in on-premises environments due to the elevated privileges associated with its AD DS Connector account (typically created in Active Directory with the MSOL\_ prefix). Using an **Enterprise Admin** or **Domain Admin** account for this purpose significantly increases the attack surface, as these accounts have broad control over the directory.

Starting with [Entra Connect build 1.4.###.#](/en-us/entra/identity/hybrid/connect/reference-connect-accounts-permissions), Enterprise Admin and Domain Admin accounts can no longer be used as the AD DS Connector account. This best practice prevents over-privileging the connector account, reducing the risk of domain-wide compromise if the account is targeted by attackers. Organizations must now create or assign a lower-privileged account specifically for directory synchronization, ensuring better adherence to the principle of least privilege and protecting critical admin accounts.

Note

The **Replace Enterprise or Domain Admin account for Microsoft Entra Connect AD DS Connector account** security assessment is available only if Microsoft Defender for Identity sensor is installed on servers running Microsoft Entra Connect services.

### Implementation

1. Review the recommended action at [Microsoft Secure Score actions](https://security.microsoft.com/securescore?viewid=actions) for *Replace Enterprise or Domain Admin account for Microsoft Entra Connect AD DS Connector account*.
2. Review the exposed accounts and their group memberships. The list contains members of Domain/Enterprise Admins through direct and recursive membership.
3. Perform one of the following actions:

    - Remove MSOL\_ user account user from privileged groups, ensuring it retains the necessary permissions to function as the Microsoft Entra Connect Connector account.
    - Change the Microsoft Entra Connect AD DS Connector account (MSOL\_) to a lower-privileged account.