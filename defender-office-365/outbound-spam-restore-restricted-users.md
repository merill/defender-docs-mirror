---
layout: Conceptual
title: Remove blocked users from the Restricted entities page - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/outbound-spam-restore-restricted-users
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: how-to
ms.localizationpriority: high
ms.assetid: 712cfcc1-31e8-4e51-8561-b64258a8f1e5
ms.collection:
- m365-security
- tier2
description: Admins can learn how to remove user accounts from the Restricted entities page in the Microsoft Defender portal. Users are added to the Restricted entities page for sending outbound spam, typically as a result of account compromise.
ms.custom:
- msecd-doc-authoring-1015
- seo-marvel-apr2020
- sfi-ga-nochange
ms.service: defender-office-365
ms.date: 2026-08-24T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 23efd18b-ffd6-52fb-eb87-0bf21ec98e7d
document_version_independent_id: 23efd18b-ffd6-52fb-eb87-0bf21ec98e7d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/outbound-spam-restore-restricted-users.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: outbound-spam-restore-restricted-users
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/outbound-spam-restore-restricted-users.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 7dd93b52-1955-a96c-bf1e-d5c045e4c963
---

# Remove blocked users from the Restricted entities page - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

In all organizations with cloud mailboxes, several things happen if a user exceeds the [outbound sending limits of the service](/en-us/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits#sending-limits-across-office-365-options) or the [limits in outbound spam policies](outbound-spam-policies-configure):

- The user is restricted from sending email, but they can still receive email.
- The user is added to the **Restricted entities** page in the Microsoft Defender portal.

    A *restricted entity* is a **user account** or a **connector** that's blocked from sending email due to indications of compromise, which typically includes exceeding message receiving and sending limits.
- If the user tries to send email, the message is returned in a non-delivery report (also known as an NDR or bounce message) with the error code [Fix error code 5.1.8 in Exchange Online](/en-us/Exchange/mail-flow-best-practices/non-delivery-reports-in-exchange-online/fix-error-code-5-1-8-in-exchange-online) and the following text:

> 
> "Your message couldn't be delivered because you weren't recognized as a valid sender. The most common reason for this is that your email address is suspected of sending spam and it's no longer allowed to send email. Contact your email admin for assistance. Remote Server returned '550 5.1.8 Access denied, bad outbound sender."

For more information about compromised user accounts and how to regain control of those accounts, see [Responding to a compromised email account](responding-to-a-compromised-email-account).

The procedures in this article explain how admins can remove user accounts from the **Restricted entities** page in the Microsoft Defender portal or in Exchange Online PowerShell.

For more information about compromised *connectors* and how to remove connectors from the **Restricted entities** page, see [Remove blocked connectors from the Restricted entities page](connectors-remove-blocked).

## What do you need to know before you begin?

Before you begin, make sure you have access to the required tools and permissions:

- You open the Microsoft Defender portal at https://security.microsoft.com. To go directly to the **Restricted users** page, use https://security.microsoft.com/restrictedusers.
- To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- You need to be assigned permissions before you can do the procedures in this article. You have the following options:

    - [Microsoft Defender XDR Unified role based access control (RBAC)](/en-us/defender-xdr/manage-rbac) (If **Email & collaboration** &gt; **Defender for Office 365** permissions is ![](media/scc-toggle-on.png)**Active**. Affects the Defender portal only, not PowerShell): **Authorization and settings/Security settings/Core Security settings (manage)** or **Authorization and settings/Security settings/Core Security settings (read)**.
    - [Exchange Online permissions](/en-us/exchange/permissions-exo/permissions-exo):

        - *Remove user accounts from the Restricted entities page*: Membership in the **Organization Management** or **Security Administrator** role groups.
        - *Read-only access to the Restricted entities page*: Membership in the **Global Reader**, **Security Reader**, or **View-Only Organization Management** role groups.
    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in the **Global Administrator**^\*^, **Security Administrator**, **Global Reader**, or **Security Reader** roles gives users the required permissions *and* permissions for other features in Microsoft 365.

        Important

        ^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.
- A sender exceeding the outbound email limits is an indicator of a compromised account. Before you follow the procedures in this article to remove a user from the **Restricted entities** page, be sure to follow the required steps to regain control of the account as described in [Responding to a compromised email account in Office 365](responding-to-a-compromised-email-account).

## Remove a user from the Restricted entities page in the Microsoft Defender portal

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Review** &gt; **Restricted entities**. Or, to go directly to the **Restricted entities** page, use https://security.microsoft.com/restrictedentities.
2. On the **Restricted entities** page, identify the user account to unblock. The **Entity** value is **Mailbox**.

    Select a column header to sort by that column.

    To change the list of entities from normal to compact spacing, select ![](media/defender-portal-icon-standard.png)**Change list spacing to compact or normal**, and then select ![](media/defender-portal-icon-compact.png)**Compact list**.

    Use the ![](media/defender-portal-icon-search.png)**Search** box and a corresponding value to find specific users.
3. Select the user to unblock by selecting the check box for the entity, and then selecting the **Unblock** action that appears on the page.
4. In the **Unblock user** flyout that opens, read the details about the restricted account on the **Overview** page. Verify that you've gone through the suggestions in the **Recommendations** section to confirm that the account isn't compromised or to regain control of the account.

    When you're finished on the **Overview** page, select **Next**.
5. On the **Unblock user page**, consider the recommendations and use the links in the **Multi-factor authentication** and **Change password** sections to **Enable MFA** and **Reset the user's password** if you haven't done these steps already. Enabling MFA and resetting the password are a good defense against future account compromise.

    When you're finished on the **Unblock user page**, select **Submit**.
6. A warning dialog confirms that you're about to remove the sending restriction for the selected user. If you verified that the account is secured, select **Yes** to confirm.

    Note

    Under most circumstances, all restrictions should be removed from the user within one hour. Transient technical issues might cause a longer wait time, but the total wait should be no longer than 24 hours.

## Verify the alert settings for restricted users

The default alert policy named **User restricted from sending email** automatically notifies admins when users are blocked from sending email. For more information about alert policies, see [Alert policies in the Microsoft Defender portal](alert-policies-defender-portal).

Important

For alerts to work, audit logging must be turned on (it's on by default). To verify that audit logging is turned on or to turn it on, see [Turn auditing on or off](/en-us/purview/audit-log-enable-disable).

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Alert policy**. Or, to go directly to the **Alert policy** page, use https://security.microsoft.com/alertpoliciesv2.
2. On the **Alert policy** page, find the alert named **User restricted from sending email**. You can sort the alerts by name, or use the ![](media/defender-portal-icon-search.png)**Search** box to find the alert.

    Select the **User restricted from sending email** alert by clicking anywhere in the row other than the check box next to the name.
3. In the **User restricted from sending email** flyout that opens, verify or configure the following settings:

    - **Status**: Verify the alert is turned on ![](media/scc-toggle-on.png) .
    - Expand the **Set your recipients section** and verify the **Recipients** and **Daily notification limit** values.

        To change the values, select ![](media/defender-portal-icon-edit.png)**Edit recipient settings** in the section or select ![](media/defender-portal-icon-edit.png)**Edit policy** at the top of the flyout.

        - On the **Decide if you want to notify people when this alert is triggered** page of the wizard that opens, verify or change the following settings:

            - Verify **Opt-in for email notifications** is selected.
            - **Email recipients**: The default value is **TenantAdmins** group (**Global Administrator** members). To add more recipients, click in the empty area of the box. A list of recipients appears, and you can start typing a name to filter and select a recipient. Remove an existing recipient from the box by selecting ![](media/defender-portal-icon-remove-selection.png) next to their name.
            - **Daily notification limit**: The default value is **No limit**.

            When you're finished on the **Decide if you want to notify people when this alert is triggered** page, select **Next**.
        - On the **Review your settings** page, select **Submit**, and then select **Done**.
4. Back in the **User restricted from sending email** flyout, select ![](media/defender-portal-icon-remove.png) at the top of the flyout.

## Use Exchange Online PowerShell to view and remove users from the Restricted entities page

To view the list of users who are restricted from sending email, run the following command in [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell):

```powershell
Get-BlockedSenderAddress
```

The identifier for a restricted sender depends on the sender type:

- **Hosted mailbox**: The user principal name (UPN) of the blocked mailbox. The UPN and primary SMTP address aren't required to match.
- **Nonhosted sender**: The SMTP address that the sender uses. For example, an on-premises sender is listed by its sending SMTP address.

To view details about a specific restricted sender, replace &lt;emailaddress&gt; with the UPN of a hosted mailbox or the SMTP address of a nonhosted sender, and then run the following command:

```powershell
Get-BlockedSenderAddress -SenderAddress <emailaddress> | Format-List
```

For detailed syntax and parameter information, see [Get-BlockedSenderAddress](/en-us/powershell/module/exchangepowershell/get-blockedsenderaddress).

To remove a restricted sender, replace &lt;emailaddress&gt; with the UPN of a hosted mailbox or the SMTP address of a nonhosted sender, and then run the following command:

```powershell
Remove-BlockedSenderAddress -SenderAddress <emailaddress>
```

For detailed syntax and parameter information, see [Remove-BlockedSenderAddress](/en-us/powershell/module/exchangepowershell/remove-blockedsenderaddress).