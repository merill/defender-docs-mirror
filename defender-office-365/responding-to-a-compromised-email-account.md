---
layout: Conceptual
title: Respond to a compromised email account in Microsoft 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/responding-to-a-compromised-email-account
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: how-to
ms.collection:
- o365_security_incident_response
- m365-security
- m365solution-smb
- highpri
- tier1
ms.custom:
- msecd-doc-authoring-1016
- TopSMBIssues
- seo-marvel-apr2020
ms.localizationpriority: high
description: Learn how to recognize and respond to a compromised email account using tools available in Microsoft 365.
ms.service: defender-office-365
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: c9b5590d-7a42-f494-4b7a-a40a7a24f6db
document_version_independent_id: c9b5590d-7a42-f494-4b7a-a40a7a24f6db
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/responding-to-a-compromised-email-account.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: responding-to-a-compromised-email-account
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/responding-to-a-compromised-email-account.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
platformId: 94469ab8-c2a3-8ed9-c0f3-92ed06445ef8
---

# Respond to a compromised email account in Microsoft 365 - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

User credentials control access to Microsoft Entra ID accounts, which are central to compromise investigations. Once an attacker gains access to the account, they can access the associated Microsoft 365 mailbox, SharePoint folders, or files in the user's OneDrive. Remediation and investigation of a compromised user focuses on the affected account and the services associated with the account.

Attackers often use a compromised user's mailbox to send to recipients inside and outside of the organization. Business Email Compromise (BEC) is a prolific type of attack and is addressed in this article.

This article addresses the symptoms of account compromise (specifically, the mailbox) and how to regain control of the compromised account.

Important

The following button lets you test and identify suspicious account activity. Use this test with the guidance in this article to gain insight into potentially compromised accounts and determine the necessary remediation actions.

## Common symptoms of a compromised Microsoft 365 email account

One or more of the following activities might indicate an account associated with a Microsoft 365 mailbox is compromised:

- The mailbox is blocked from sending email.
- Suspicious activity. For example, missing or deleted email.
- Suspicious [Inbox rules](https://support.microsoft.com/office/c24f5dea-9465-4df4-ad17-a50704d66c59). For example:
    - Rules that automatically forward email to unknown addresses.
    - Rules that move messages to the **Notes**, **Junk Email**, or **RSS Subscriptions** folders.
- The **Sent Items** or **Deleted Items** folders contain suspicious messages. For example, "I'm stuck in London, send money."
- Changes to the user's contact in the Global Address List (GAL). For example, name, telephone number, or postal code.
- Frequent password changes or unexplained account lockouts.
- Recently added [external email forwarding](outbound-spam-policies-external-email-forwarding).
- Suspicious email message signatures. For example, a fake banking signature or a prescription drug signature.

If the mailbox exhibits any of these symptoms, use the steps in Secure and Restore Email Function to a Compromised Microsoft 365 Mail Enabled Account to regain control of the account.

## Secure and restore email functionality for a compromised Microsoft 365 mail-enabled account

After the attacker gains access to an account, you need to block access to the account as soon as possible.

The following steps address known methods that might allow the attacker to maintain persistence and regain control of the account later. Be sure to address each step.

### Step 1: Disable the affected user account

Use the following guidance to disable the affected user account during the investigation.

- Disabling the compromised account is preferred and highly recommended until you complete the investigation.

    1. If necessary, install the Microsoft Graph PowerShell module in PowerShell by running the following command:

        ```powershell
        Install-Module -Name Microsoft.Graph -Scope CurrentUser
        ```
    2. Connect to Microsoft Graph by running the following command:

        ```powershell
        Connect-MgGraph -Scopes "User.ReadWrite.All"
        ```
    3. To store the details of the user account in the variable named `$user`, replace &lt;UPN&gt; with the user's account name (user principal name or UPN), and then run the following command:

        ```powershell
        $user = Get-MgUser -Search UserPrincipalName:'<UPN>' -ConsistencyLevel Eventual
        ```

        For example:

        ```powershell
        $user = Get-MgUser -Search UserPrincipalName:'jason@contoso.onmicrosoft.com' -ConsistencyLevel Eventual
        ```
    4. Run the following command to disable the user account:

        ```powershell
        Update-MgUser -UserId $user.Id -AccountEnabled $false
        ```

    For detailed syntax and parameter information, see [Update-MgUser](/en-us/powershell/module/microsoft.graph.users/update-mguser)
- If you can't disable the account, the next best step is to reset the password. For instructions, see [Reset passwords in Microsoft 365 for business](/en-us/microsoft-365/admin/add-users/reset-passwords).

    - Be sure to use a strong password: upper and lowercase letters, at least one number, and at least one special character.
    - **Don't send the new password to the user through email, because the attacker could have access to the mailbox at this point**.
    - Use a unique password the attacker can't guess. Even if the password history requirement allows it, don't reuse any of the last five passwords.
    - If the account is synced from Active Directory, reset the password in Active Directory and reset it twice to mitigate the risk of [pass-the-hash](https://en.wikipedia.org/wiki/Pass_the_hash) attacks. For instructions, see [Set-ADAccountPassword](/en-us/powershell/module/activedirectory/set-adaccountpassword).
    - If the user's identity is federated with Microsoft 365, you must change the account password in the on-premises environment and then notify the administrator of the compromise.
    - Be sure to update app passwords. App passwords aren't automatically revoked when you reset the password. The user should delete existing app passwords and create new ones. For more information, see [Manage app passwords for two-step verification](https://support.microsoft.com/account-billing/d6dc8c6d-4bf7-4851-ad95-6d07799387e9).
- We highly recommend enabling and enforcing multifactor authentication (MFA) for the account. MFA effectively safeguards against account compromise and is essential for accounts with admin privileges.

    For more information, see the following articles:

    - [Set up multifactor authentication](/en-us/microsoft-365/admin/security-and-compliance/set-up-multi-factor-authentication)
    - [Require phishing-resistant MFA for admins](/en-us/entra/identity/conditional-access/policy-admin-phish-resistant-mfa)

### Step 2: Revoke User Access

Revoking active sessions immediately invalidates any active access using the stolen credentials, and prevents the attacker from accessing more sensitive data or doing unauthorized actions on the compromised account.

1. If your environment blocks local script execution, set the PowerShell execution policy to `RemoteSigned` so you can install and run the required Microsoft Graph modules. Run the following command in an elevated PowerShell window (a PowerShell window you open by selecting **Run as administrator**):

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```
2. If necessary, install the Microsoft Graph PowerShell modules required to authenticate and revoke active user sessions:

    ```powershell
    Install-Module Microsoft.Graph.Authentication
    
    Install-Module Microsoft.Graph.Users.Actions
    ```
3. Connect to Microsoft Graph with the `User.RevokeSessions.All` permission scope so you can invalidate the user's active sign-in sessions:

    ```powershell
    Connect-MgGraph -Scopes User.RevokeSessions.All
    ```
4. To revoke all active sign-in sessions and invalidate existing refresh tokens for the affected user, replace &lt;UPN&gt; with the user's account (user principal name or UPN), and then run the following command:

    ```powershell
    Revoke-MgUserSignInSession -UserId <UPN>
    ```

    For example, the following command revokes all active sessions for the user `jason@contoso.onmicrosoft.com`:

    ```powershell
    Revoke-MgUserSignInSession -UserId jason@contoso.onmicrosoft.com
    ```

For more information, see [Revoke user access in an emergency in Microsoft Entra ID](/en-us/entra/identity/users/users-revoke-access).

### Step 3: Review the MFA registered devices for the affected user

Identify and remove any suspicious devices added by an attacker. Also, ensure any unrecognized MFA methods are removed to secure the user's account.

For instructions, see [Manage user authentication options](/en-us/entra/identity/authentication/howto-mfa-userdevicesettings#manage-user-authentication-options).

### Step 4: Review the list of applications with user consent

Remove and revoke any applications that shouldn't be allowed.

For instructions, see [Application review](/en-us/entra/identity/enterprise-apps/manage-application-permissions?pivots=portal#review-and-revoke-permissions).

### Step 5: Review the administrative roles assigned to the user

Remove any roles that shouldn't be allowed.

For more information, see the following articles:

- [List Azure role assignments using the Azure portal](/en-us/azure/role-based-access-control/role-assignments-list-portal)
- [List Microsoft Entra role assignments](/en-us/entra/identity/role-based-access-control/view-assignments?tabs=admin-center#list-role-assignments-for-a-user)
- [Permissions in the Microsoft Purview portal](/en-us/purview/purview-compliance-portal-permissions)
- [Microsoft Defender for Office 365 permissions in the Microsoft Defender portal](/en-us/defender-office-365/mdo-portal-permissions)

### Step 6: Review mail forwarders

Remove any suspicious mailbox forwarding that the attacker added.

1. [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
2. To check whether the mailbox has forwarding settings that redirect messages to another recipient (also known as *SMTP forwarding*), replace &lt;Identity&gt; with the name, email address, or account name of the mailbox, and then run the following command:

    ```powershell
    Get-Mailbox -Identity \<Identity\> | Format-List Forwarding*Address,DeliverTo*
    ```

    For example, the following command inspects the forwarding settings on Jason's mailbox:

    ```powershell
    Get-Mailbox -Identity jason@contoso.com | Format-List Forwarding*Address,DeliverTo*
    ```

    Observe the values of the following properties:

    - *ForwardingAddress*: A nonblank value means email is being forwarded to the specified internal recipient.
    - *ForwardingSmtpAddress*: A nonblank value means email is being forwarded to the specified external recipient. If both *ForwardingAddress* and *ForwardingSmtpAddress* are configured, email is forwarded only to the *ForwardingAddress* internal recipient.
    - *DeliverToMailboxAndForward*: Controls how messages are delivered and forwarded to recipients specified by *ForwardingAddress* or *ForwardingSmtpAddress*:
        - True: Messages are delivered to this mailbox and forwarded to the specified recipient.
        - False: Messages are forwarded to the specified recipient. Messages aren't delivered to this mailbox.
3. To review all Inbox rules (including hidden ones) for rules that redirect or forward messages without the user's knowledge, replace &lt;Identity&gt; with the name, email address, or account name of the mailbox, and then run the following command:

    ```powershell
    Get-InboxRule -Mailbox <Identity> -IncludeHidden | Format-List Name,Enabled,RedirectTo,Forward*,Identity
    ```

    For example, the following command inspects Inbox rules on Jason's mailbox for suspicious forwarding behavior:

    ```powershell
    Get-InboxRule -Mailbox jason@contoso.com -IncludeHidden | Format-List Name,Enabled,RedirectTo,Forward*,Identity
    ```

    Observe the values of the following properties:

    - *Enabled*: Whether the rule is enabled (True) or disabled (False).
    - *RedirectTo*: A nonblank value means email is being redirected to the specified recipients. Messages aren't delivered to this mailbox.
    - *ForwardTo*: A nonblank value means email is being forwarded to the specified recipients.
    - *ForwardAsAttachmentTo*: A nonblank value means email is being forwarded to the specified recipients as an email attachment.
    - *Identity*: The globally unique value of the rule. To see complete details of the rule, replace &lt;Identity&gt; with the Identity value, and then run the following command:

        ```powershell
        Get-InboxRule -Identity "<Identity>" -IncludeHidden | Format-List
        ```

        For example:

        ```powershell
        Get-InboxRule -Identity "jason\10210541742734704641" -IncludeHidden | Format-List
        ```

For more information, see [Control automatic external email forwarding](/en-us/defender-office-365/outbound-spam-policies-external-email-forwarding).

## Investigate the compromised account

When a user reports unusual symptoms, it's crucial to conduct a thorough investigation. The Microsoft Entra admin center and the Microsoft Defender portal provide several tools to help examining suspicious activity on user accounts. Be sure to review the audit logs from the onset of the suspicious activity until you complete the remediation steps.

- **Microsoft Entra sign-in logs and other risk reports in the Microsoft Entra admin center**: Examine the values in these columns:

    - IP address
    - Sign-in locations
    - Sign-in times
    - Sign-in success or failure

    For more information, see the following articles:

    - [What are Microsoft Entra audit logs?](/en-us/entra/identity/monitoring-health/concept-audit-logs)
    - [What are Microsoft Entra sign-in logs?](/en-us/entra/identity/monitoring-health/concept-sign-ins)
- **Azure audit logs**: For more information, see [Azure security logging and auditing](/en-us/azure/security/fundamentals/log-audit).
- **Audit logs in the Defender portal**: Filter the logs for activity using a date range that starts immediately before the suspicious activity occurred. Don't filter specific activities during the initial search.

    For more information, see [Search the audit log](audit-log-search-defender-portal).

By analyzing the provided logs, you can pinpoint the specific time frame that requires further attention. Once identified, review the messages sent by the user during this period for more insight.

- **Message Trace in the Defender portal**: Verify the contents of the **Sent items** folder of the account in Outlook or Outlook on the web.

    For more information, see [Message trace in the Microsoft Defender portal](message-trace-defender-portal).

## After the investigation is complete

Complete the following tasks after you finish the investigation:

1. If you disabled the account during the investigation, reset the password and then enable the account as described in Step 1: Disable the affected user account.
2. If the account was used to send spam or a high volume of email, it's likely that the mailbox is blocked from sending mail. Remove the user from the Restricted entities page as described in [Remove blocked users from the Restricted entities page](outbound-spam-restore-restricted-users).