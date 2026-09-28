---
layout: Conceptual
title: Remediation Actions for Compromised Users in Microsoft Defender for Identity - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/remediation-actions
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
description: Learn how to respond to compromised users with remediation actions in Microsoft Defender for Identity
ms.date: 2026-07-22T00:00:00.0000000Z
ms.topic: how-to
ms.custom: sfi-ga-blocked, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: c5bc5b5c-c969-3ae4-121c-3a467c0db9d8
document_version_independent_id: c5bc5b5c-c969-3ae4-121c-3a467c0db9d8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/remediation-actions.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: remediation-actions
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/remediation-actions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
- https://authoring-docs-microsoft.poolparty.biz/devrel/b1cfdec6-b0c3-4209-818c-736879856e0e
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
- https://authoring-docs-microsoft.poolparty.biz/devrel/2d0723c1-cf38-4c30-ab3d-5df787b33270
platformId: 2f76b528-6f99-5127-cd8f-42178b1dfddd
---

# Remediation Actions for Compromised Users in Microsoft Defender for Identity - Microsoft Defender for Identity | Microsoft Learn

Applies to:

- Microsoft Defender for Identity
- Microsoft Defender

Microsoft Defender for Identity lets you respond to compromised users with remediation actions that work consistently across your connected identity sources. The actions available for an identity depend on the connector that manages the account, and they span on-premises Active Directory and Microsoft Entra ID, identity providers such as Okta, CyberArk Identity, and SailPoint Identity Security Cloud, and applications connected through Microsoft Defender for Cloud Apps such as Google Workspace, Salesforce, and Box.

The response actions on users are available directly from the identity page, the identity side panel, the advanced hunting page, or in the action center. After you take action on a user, you can review the activity details in the action center.

## How remediation actions work

Remediation actions are initiated by a user in the Microsoft Defender portal and are authorized using role-based access control (RBAC) based on Microsoft Entra ID roles. If the initiating user isn’t authorized, the action is blocked before execution.

After authorization, the action is executed by the identity system that manages the affected account:

- **Active Directory**: Actions are executed by the Microsoft Defender for Identity sensor on the domain controller. Only sensors installed on domain controllers perform remediation actions; sensors on AD FS, AD CS, or Microsoft Entra Connect servers don't perform remediation actions. The sensor uses the domain controller's local system account to perform the action.

    Important

    Make sure the **Automatically use the sensor's local system account** option is selected. This is required for sensor v3.x and recommended for all environments, including mixed (v2.x and v3.x) deployments. To verify, in the [Microsoft Defender portal](https://security.microsoft.com), go to **Settings** &gt; **Identities** &gt; **Microsoft Defender for Identity** &gt; **Manage action accounts**.
- **Microsoft Entra ID**: Microsoft Defender for Identity creates and uses a Microsoft‑managed enterprise application to execute remediation actions in Entra ID.

    - **Application name:***Microsoft Defender for Identity*. In older tenants, the application might appear with the name *Radius Aad Syncer*.
    - **Application ID:**`60ca1954-583c-4d1f-86de-39d835f3e452`
- **Supported non‑Microsoft identity sources and connected apps**: Actions are executed through the source's connector, including identity provider connectors and Microsoft Defender for Cloud Apps app connectors, using the credentials configured for the integration.

Remediation actions are recorded by the identity system where the action is executed and are visible in Microsoft Defender audit logs.

## Remediation actions in Automatic Attack Disruption

Remediation actions can also be applied automatically by Microsoft Defender's automatic attack disruption. When an active attack is detected, attack disruption uses Defender for Identity remediation capabilities to contain the threat without manual intervention. For details, see [automatic attack disruption](/en-us/defender-xdr/automatic-attack-disruption).

## Supported actions

The following Defender for Identity actions can be performed on Identities.

Depending on your Microsoft Entra ID roles, you might see additional Microsoft Entra ID actions, such as requiring users to sign in again and confirming a user as compromised. For more information, see [Remediate risks and unblock users](/en-us/entra/id-protection/howto-identity-protection-remediate-unblock).

| Remediation action | Description | Supported identity sources |
| --- | --- | --- |
| Disable | Disables all accounts linked to an identity or a specific account. Disabling prevents sign-in and access to network resources until the accounts are re-enabled. This action doesn't delete the identity profile or associated data such as documents, calendar events, or email messages. | Active Directory, Microsoft Entra ID, Okta, CyberArk Identity, SailPoint Identity Security Cloud, Google Workspace, Salesforce, Box |
| Enable | Re-enables accounts that were previously disabled for the selected identity. | Active Directory, Microsoft Entra ID, Okta, CyberArk Identity, SailPoint Identity Security Cloud, Salesforce |
| Revoke session | Revokes active sessions for the selected identity. | Microsoft Entra ID, Okta |
| Mark as compromised | Marks all accounts linked to the selected identity as compromised in Microsoft Entra ID. | Microsoft Entra ID |
| Force password change | Forces a password change for one or more accounts linked to the selected identity. The user must change their password at next sign-in, which prevents further use of compromised credentials. | Active Directory, Microsoft Entra ID |

## Roles and permissions

The following table lists the remediation actions supported by Defender for Identity and the roles required to initiate each action.

| Remediation Action | Active Directory | Microsoft Entra ID | Okta, SailPoint, CyberArk | Supported SaaS apps |
| --- | --- | --- | --- | --- |
| Disable | See [Required permissions Defender for Identity in Microsoft Defender XDR](/en-us/defender-for-identity/role-groups#required-permissions-defender-for-identity-in-microsoft-defender-xdr) | Global Administrator, User Administrator, Authentication Administrator, Privileged Authentication Administrator, Directory Writers, SOC Identity Responder | See [Required permissions Defender for Identity in Microsoft Defender XDR](/en-us/defender-for-identity/role-groups#required-permissions-defender-for-identity-in-microsoft-defender-xdr) | Global Administrator, Security Administrator, Cloud App Security Administrator |
| Enable | See [Required permissions Defender for Identity in Microsoft Defender XDR](/en-us/defender-for-identity/role-groups#required-permissions-defender-for-identity-in-microsoft-defender-xdr) | Global Administrator, User Administrator, Authentication Administrator, Privileged Authentication Administrator, Directory Writers | See [Required permissions Defender for Identity in Microsoft Defender XDR](/en-us/defender-for-identity/role-groups#required-permissions-defender-for-identity-in-microsoft-defender-xdr) | Global Administrator, Security Administrator, Cloud App Security Administrator |
| Revoke session | N/A | Global Administrator, User Administrator, Authentication Administrator, Privileged Authentication Administrator, Directory Writers, Helpdesk Administrator, SOC Identity Responder | See [Required permissions Defender for Identity in Microsoft Defender XDR](/en-us/defender-for-identity/role-groups#required-permissions-defender-for-identity-in-microsoft-defender-xdr) | N/A |
| Mark as compromised | N/A | Global Administrator, Security Administrator, Security Operator, SOC Identity Responder | N/A | N/A |
| Force password change | See [Required permissions Defender for Identity in Microsoft Defender XDR](/en-us/defender-for-identity/role-groups#required-permissions-defender-for-identity-in-microsoft-defender-xdr) | Global Administrator, Privileged Authentication Administrator, Authentication Administrator, User Administrator, Password Administrator, Helpdesk Administrator, SOC Identity Responder | N/A | N/A |

Note

There are some limitations for Microsoft Entra ID when performing certain actions on other roles. For more information, see the [Graph API documentation](/en-us/graph/api/resources/users?view=graph-rest-1.0&amp;preserve-view=true).

## Prerequisites

To perform any of the supported actions, you need to:

- **Configure the account that Microsoft Defender for Identity uses to perform actions**: Make sure the **Automatically use the sensor's local system account** option is selected. In the [Microsoft Defender portal](https://security.microsoft.com), go to **Settings** &gt; **Identities** &gt; **Microsoft Defender for Identity** &gt; **Manage action accounts**. This setting is required if any of your sensors are v3.x. For more information, see [Manage action accounts](deploy/manage-action-accounts).
- **Sign in to the Microsoft Defender portal with the required permissions**: For Defender for Identity actions, you'll need a custom role with **Response (manage)** permissions. For more information, see [Create custom roles with Microsoft Defender unified RBAC](/en-us/microsoft-365/security/defender/create-custom-rbac-roles). For details on the specific roles required for each action, see Roles and permissions.

To apply a remediation action to an identity, perform the following steps:

1. In the [Microsoft Defender portal](https://security.microsoft.com), go to one of the following locations:

    - **Identity page**: Go to **Assets** &gt; **Identities** and select the identity you want to act on.
    - **Advanced hunting page**: Go to **Hunting** &gt; **Advanced hunting** and identify a result that includes an identity entity.
    - **Action center**: Go to **Actions & submissions** &gt; **Action center** to review and manage pending or completed actions.
2. Select **Actions** or right-click the identity to open the actions menu.
3. Select the remediation action you want to apply, such as **Disable**, **Revoke session**, or **Force password change**.
4. Confirm the action when prompted.

The action is submitted and executed by the relevant identity system. You can track the status in the **Action center**.