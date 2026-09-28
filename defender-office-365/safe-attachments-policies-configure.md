---
layout: Conceptual
title: Set up Safe Attachments policies in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/safe-attachments-policies-configure
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: how-to
ms.localizationpriority: medium
ms.assetid: 078eb946-819a-4e13-8673-fe0c0ad3a775
ms.collection:
- m365-security
- tier2
description: Learn about how to define Safe Attachments policies to protect your organization from malicious files in email.
ms.custom:
- seo-marvel-apr2020
- sfi-ga-nochange
- msecd-doc-authoring-1016
ms.service: defender-office-365
ms.date: 2026-07-17T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 19594ffc-c2b3-e6bb-2ca7-8967b2f902fd
document_version_independent_id: 19594ffc-c2b3-e6bb-2ca7-8967b2f902fd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/safe-attachments-policies-configure.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: safe-attachments-policies-configure
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/safe-attachments-policies-configure.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
platformId: e8488dfb-f724-4f56-783d-4b9521572456
---

# Set up Safe Attachments policies in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

Important

This article is intended for business customers who have [Microsoft Defender for Office 365](defender-for-office-365-whats-new). If you're a home user looking for information about attachment scanning in Outlook, see [Advanced Outlook.com security](https://support.microsoft.com/office/882d2243-eab9-4545-a58a-b36fee4a46e2).

In organizations with Microsoft Defender for Office 365, Safe Attachments is an additional layer of protection against harmful files in email messages (for example, malware, ransomware, or phishing). After message attachments are scanned by [Anti-malware protection](anti-malware-protection-about), Safe Attachments opens files in a virtual environment to see what happens when the attachment is opened (a process known as *detonation*) before the messages are delivered to recipients. For more information, see [Safe Attachments in Microsoft Defender for Office 365](safe-attachments-about).

Although there's no default Safe Attachments policy, the **Built-in protection** preset security policy provides Safe Attachments protection to all recipients by default. Recipients who are specified in the Standard or Strict preset security policies or in custom Safe Attachments policies aren't affected. For more information, see [Preset security policies](preset-security-policies).

For greater granularity, you can also use the procedures in this article to create Safe Attachments policies that apply to specific users, group, or domains.

Tip

Instead of creating and managing custom Safe Attachments policies, we typically recommend turning on and adding all users to the Standard and/or Strict preset security policies. For more information, see [Configure threat policies](mdo-deployment-guide#step-2-configure-threat-policies).

To understand how threat protection works in Microsoft Defender for Office 365, see [Step-by-step threat protection in Microsoft Defender for Office 365](protection-stack-microsoft-defender-for-office365).

Typically, email attachment scanning completes within 15 minutes. Sometimes, it takes longer due to retry delays and processing time to analyze the file in the virtual environment.

You configure Safe Attachments policies in the Microsoft Defender portal or in Exchange Online PowerShell.

Note

In the global settings of Safe Attachments settings, you configure features that aren't dependent on Safe Attachments policies. For instructions see [Turn on Safe Attachments for SharePoint, OneDrive, and Microsoft Teams](safe-attachments-for-spo-odfb-teams-configure) and [Safe Documents in Microsoft 365 E5](safe-documents-in-e5-plus-security-about).

## What do you need to know before you begin?

Verify the following prerequisites before you configure Safe Attachments policies:

- You open the Microsoft Defender portal at https://security.microsoft.com. To go directly to the **Safe Attachments** page, use https://security.microsoft.com/safeattachmentv2.
- To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- You need to be assigned permissions before you can do the procedures in this article. You have the following options:

    - [Microsoft Defender XDR Unified role based access control (RBAC)](/en-us/defender-xdr/manage-rbac) (If **Email & collaboration** &gt; **Defender for Office 365** permissions is ![](media/scc-toggle-on.png)**Active**. Affects the Defender portal only, not PowerShell): **Authorization and settings/Security settings/Core Security settings (manage)** or **Authorization and settings/Security settings/Core Security settings (read)**.
    - [Email & collaboration permissions in the Microsoft Defender portal](mdo-portal-permissions) and [Exchange Online permissions](/en-us/exchange/permissions-exo/permissions-exo):

        - *Create, modify, and delete policies*: Membership in the **Organization Management** or **Security Administrator** role groups in Email & collaboration permissions and membership in the **Organization Management** role group in Exchange Online permissions.
        - *Read-only access to policies*: Membership in one of the following role groups:
            - **Global Reader** or **Security Reader** in Email & collaboration permissions.
            - **View-Only Organization Management** in Exchange Online permissions.
    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in the **Global Administrator**^\*^, **Security Administrator**, **Global Reader**, or **Security Reader** roles gives users the required permissions *and* permissions for other features in Microsoft 365.

        Important

        ^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.

    Tip

    If policy changes fail to save with a 403 or **CmdletAccessDeniedException** error and you verified that you have the required permissions, the issue might be related to an Exchange Online role-based access control (RBAC) configuration problem. Some organizations require a backend RBAC configuration refresh before policy changes succeed. If the issue persists, contact [Microsoft Support](/en-us/microsoft-365/admin/get-help-support) and reference "RBAC configuration refresh."
- For our recommended settings for Safe Attachments policies, see [Safe Attachments settings](recommended-settings-for-eop-and-office365#safe-attachments-settings).

    Tip

    [Exceptions to Built-in protection for Safe Attachments](preset-security-policies#use-the-microsoft-defender-portal-to-add-exclusions-to-the-built-in-protection-preset-security-policy) or settings in custom Safe Attachments policies are ignored if a recipient is also included in the [Standard or Strict preset security policies](preset-security-policies). For more information, see [Order and precedence of email protection](how-policies-and-protections-are-combined).
- Allow up to 30 minutes for a new or updated policy to be applied.
- For more information about licensing requirements, see [Licensing terms](/en-us/office365/servicedescriptions/office-365-advanced-threat-protection-service-description#licensing-terms).

## Use the Microsoft Defender portal to create Safe Attachments policies

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Threat policies** &gt; **Safe Attachments** in the **Policies** section.Or, to go directly to the **Safe Attachments** page, use https://security.microsoft.com/safeattachmentv2.
2. On the **Safe Attachments** page, select ![](media/defender-portal-icon-create.png)**Create** to start the new Safe Attachments policy wizard.
3. On the **Name your policy** page, configure these settings:

    - **Name**: Enter a unique, descriptive name for the policy.
    - **Description**: Enter an optional description for the policy.

    When you're finished on the **Name your policy** page, select **Next**.
4. On the **Users and domains** page, identify the internal recipients that the policy applies to (recipient conditions):

    - **Users**: The specified mailboxes, or mail users.
    - **Groups**:
        - Members of the specified distribution groups or mail-enabled security groups (dynamic distribution groups aren't supported).
        - The specified Microsoft 365 Groups (dynamic membership groups in Microsoft Entra ID aren't supported).
    - **Domains**: All recipients in the organization with a primary email address in the specified [accepted domain](/en-us/exchange/mail-flow-best-practices/manage-accepted-domains/manage-accepted-domains).

    Tip

    Leave **Users**, **Groups**, and **Domains** blank to create a policy that applies to all recipients.

    Subdomains are automatically included unless you specifically exclude them. For example, a policy that includes contoso.com also includes marketing.contoso.com unless you exclude marketing.contoso.com.

    Click in the appropriate box, start typing a value, and select the value that you want from the results. Repeat this process as many times as necessary. To remove an existing value, select ![](media/defender-portal-icon-remove-selection.png) next to the value.

    For users or groups, you can use most identifiers (name, display name, alias, email address, account name, etc.), but the corresponding display name is shown in the results. For users, enter an asterisk (\*) by itself to see all available values.

    You can use a condition only once, but the condition can contain multiple values:

    - Multiple **values** of the **same condition** use OR logic (for example, *&lt;recipient1&gt;* or *&lt;recipient2&gt;*). If the recipient matches **any** of the specified values, the policy is applied to them.
    - Different **types of conditions** use AND logic. The recipient must match **all** of the specified conditions for the policy to apply to them. For example, you configure a condition with the following values:

        - Users: `romain@contoso.com`
        - Groups: Executives

        The policy is applied to `romain@contoso.com`*only* if he's also a member of the Executives group. Otherwise, the policy isn't applied to him.
    - **Exclude these users, groups, and domains**: To add exceptions for the internal recipients that the policy applies to (recipient exceptions), select this option and configure the exceptions.

        You can use an exception only once, but the exception can contain multiple values:

        - Multiple **values** of the **same exception** use OR logic (for example, *&lt;recipient1&gt;* or *&lt;recipient2&gt;*). If the recipient matches **any** of the specified values, the policy isn't applied to them.
        - Different **types of exceptions** use OR logic (for example, *&lt;recipient1&gt;* or *&lt;member of group1&gt;* or *&lt;member of domain1&gt;*). If the recipient matches **any** of the specified exception values, the policy isn't applied to them.

        Tip

        If not all users in your organization have Defender for Office 365 licenses, you can use **User** or **Group** exceptions to exclude users who aren't eligible for Safe Attachments protections.

    When you're finished on the **Users and domains** page, select **Next**.
5. On the **Settings** page, configure the following settings:

    - **Safe Attachments unknown malware response**: Select one of the following values:

        - **Off**
        - **Monitor**
        - **Block**: This value is the default, and is the value used in Standard and Strict [preset security policies](preset-security-policies).
        - **Dynamic Delivery (Preview messages)**

        These values are explained in [Safe Attachments policy settings](safe-attachments-about#safe-attachments-policy-settings).
    - **Quarantine policy**: Select the quarantine policy that applies to messages that are quarantined by Safe Attachments (**Block** or **Dynamic Delivery**). Quarantine policies define what users are able to do to quarantined messages, and whether users receive quarantine notifications. For more information, see [Anatomy of a quarantine policy](quarantine-policies#anatomy-of-a-quarantine-policy).

        By default, the quarantine policy named AdminOnlyAccessPolicy is used for detections by Safe Attachments policies. For more information about this quarantine policy, see [Anatomy of a quarantine policy](quarantine-policies#anatomy-of-a-quarantine-policy).

        Note

        Quarantine notifications are disabled in the policy named AdminOnlyAccessPolicy. To notify recipients that have messages quarantined as malware or phishing by Safe Attachments, create or use an existing quarantine policy where quarantine notifications are turned on. For instructions, see [Create quarantine policies in the Microsoft Defender portal](quarantine-policies#step-1-create-quarantine-policies-in-the-microsoft-defender-portal).

        Users can't release their own messages quarantined as malware or phishing by Safe Attachments policies, regardless of how the quarantine policy is configured. If the policy is configured for users to release these quarantined messages, users are instead allowed to *request* the release of these quarantined messages.
    - **Redirect messages with detected attachments**: If you select **Enable redirect**, you can specify an email address in the **Send messages that contain monitored attachments to the specified email address** box to send messages that contain detected attachments for analysis and investigation.

        Note

        Redirection is available only for the **Monitor** action. For more information, see [Safe Attachments redirection changes (MC424899)](https://admin.microsoft.com/AdminPortal/Home?#/MessageCenter/:/messages/MC424899).
    - **Block messages containing encrypted attachments that could not be scanned**: This section appears only when you select **Block** as the **Safe Attachments unknown malware response** value. The following settings are available:

        - **Block unscanned attachments**: Select this option to quarantine messages that contain encrypted (password-protected) attachments when Safe Attachments can't scan or detonate them. For more information, see [Encrypted (password-protected) attachments in Safe Attachments policies](safe-attachments-about#encrypted-password-protected-attachments-in-safe-attachments-policies).

            When you select **Block unscanned attachments**, the following settings appear:

            - **Exclude these attachment types**: Select any attachment types to exclude from this setting:

                - **Acrobat (pdf)**
                - **Archive (zip, gzip, 7z, rar, tar only)**
                - **Office (doc, docx, xls, xlsx, ppt, pptx only)**
                - **All other file types**
            - **Quarantine policy**: Select the quarantine policy that applies to messages quarantined by this setting. Quarantine policies define what users are able to do to quarantined messages, and whether users receive quarantine notifications. By default, the quarantine policy named DefaultFullAccessWithNotificationPolicy is used. For more information, see [Anatomy of a quarantine policy](quarantine-policies#anatomy-of-a-quarantine-policy).

    When you're finished on the **Settings** page, select **Next**.
6. On the **Review** page, review your settings. You can select **Edit** in each section to modify the settings within the section. Or you can select **Back** or the specific page in the wizard.

    When you're finished on the **Review** page, select **Submit**.
7. On the **New Safe Attachments policy created** page, you can select the links to view the policy, view Safe Attachments policies, and learn more about Safe Attachments policies.

    When you're finished on the **New Safe Attachments policy created** page, select **Done**.

    Back on the **Safe Attachments** page, the new policy is listed.

## Use the Microsoft Defender portal to view Safe Attachments policy details

In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Threat policies** &gt; **Safe Attachments** in the **Policies** section. To go directly to the **Safe Attachments** page, use https://security.microsoft.com/safeattachmentv2.

On the **Safe Attachments** page, the following properties are displayed in the list of policies:

- **Name**
- **Status**: Values are **On** or **Off**.
- **Priority**: For more information, see the Set the priority of Safe Attachments policies section.

To change the list of policies from normal to compact spacing, select ![](media/defender-portal-icon-standard.png)**Change list spacing to compact or normal**, and then select ![](media/defender-portal-icon-compact.png)**Compact list**.

Use the ![](media/defender-portal-icon-search.png)**Search** box and a corresponding value to find specific Safe Attachment policies.

Use ![](media/defender-portal-icon-download.png)**Export** to export the list of policies to a CSV file.

Use ![](media/defender-portal-icon-view-reports.png)**View reports** to open the [Threat protection status report](reports-defender-for-office-365#threat-protection-status-report).

Select a policy by clicking anywhere in the row other than the check box next to the name to open the details flyout for the policy.

Tip

To see details about other Safe Attachments policies without leaving the details flyout, use ![](media/updownarrows.png)**Previous item** and **Next item** at the top of the flyout.

## Use the Microsoft Defender portal to take action on Safe Attachments policies

In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Threat policies** &gt; **Safe Attachments** in the **Policies** section. To go directly to the **Safe Attachments** page, use https://security.microsoft.com/safeattachmentv2.

On the **Safe Attachments** page, select the Safe Attachments policy by using either of the following methods:

- Select the policy from the list by selecting the check box next to the name. The following actions are available in the ![](media/defender-portal-icon-more-actions.png)**More actions** dropdown list that appears:

    - **Enable selected policies**.
    - **Disable selected policies**.
    - **Delete selected policies**.

    [![The Safe Attachments page with a policy selected and the More actions control expanded.](media/safe-attachments-policies-main-page.png)](media/safe-attachments-policies-main-page.png#lightbox)
- Select the policy from the list by clicking anywhere in the row other than the check box next to the name. Some or all following actions are available in the details flyout that opens:

    - Modify policy settings by clicking **Edit** in each section (custom policies or the default policy)
    - ![](media/defender-portal-icon-turn-on-off.png)**Turn on** or ![](media/defender-portal-icon-turn-on-off.png)**Turn off** (custom policies only)
    - ![](media/defender-portal-icon-increase.png)**Increase priority** or ![](media/defender-portal-icon-decrease.png)**Decrease priority** (custom policies only)
    - ![](media/defender-portal-icon-delete.png)**Delete policy** (custom policies only)

    [![The details flyout of a custom Safe Attachments policy.](media/anti-phishing-policies-details-flyout.png)](media/anti-phishing-policies-details-flyout.png#lightbox)

These actions are described in Modify custom Safe Attachments policies, Enable or disable custom Safe Attachments policies, Set the priority of custom Safe Attachments policies, and Remove custom Safe Attachments policies.

### Use the Microsoft Defender portal to modify custom Safe Attachments policies

After you select a custom Safe Attachments policy by clicking anywhere in the row other than the check box next to the name, the policy settings are shown in the details flyout that opens. Select **Edit** in each section to modify the settings within the section. For more information about the settings, see Create Safe Attachments policies.

You can't modify the Safe Attachments policies named **Standard Preset Security Policy**, **Strict Preset Security Policy**, or **Built-in protection (Microsoft)** that are associated with [preset security policies](preset-security-policies) in the policy details flyout. Instead, you select ![](media/defender-portal-icon-open.png)**View preset security policies** in the details flyout to go to the **Preset security policies** page at https://security.microsoft.com/presetSecurityPolicies to modify the preset security policies.

### Use the Microsoft Defender portal to enable or disable custom Safe Attachments policies

You can't enable or disable the Safe Attachments policies named **Standard Preset Security Policy**, **Strict Preset Security Policy**, or **Built-in protection (Microsoft)** that are associated with [preset security policies](preset-security-policies) here. You enable or disable preset security policies on the **Preset security policies** page at https://security.microsoft.com/presetSecurityPolicies.

After you select an enabled custom Safe Attachments policy (the **Status** value is **On**), use either of the following methods to disable it:

- **On the Safe Attachments page**: Select ![](media/defender-portal-icon-more-actions.png)**More actions** &gt; **Disable selected policies**.
- **In the details flyout of the policy**: Select ![](media/defender-portal-icon-turn-on-off.png)**Turn off** at the top of the flyout.

After you select a disabled custom Safe Attachments policy (the **Status** value is **Off**), use either of the following methods to enable it:

- **On the Safe Attachments page**: Select ![](media/defender-portal-icon-more-actions.png)**More actions** &gt; **Enable selected policies**.
- **In the details flyout of the policy**: Select ![](media/defender-portal-icon-turn-on-off.png)**Turn on** at the top of the flyout.

On the **Safe Attachments** page, the **Status** value of the policy is now **On** or **Off**.

### Use the Microsoft Defender portal to set the priority of custom Safe Attachments policies

Safe Attachments policies are processed in the order they're displayed on the **Safe Attachments** page:

- The Safe Attachments policy named **Strict Preset Security Policy** that's associated with the Strict preset security policy is always applied first (if the Strict preset security policy is [assigned to users](preset-security-policies#use-the-microsoft-defender-portal-to-assign-standard-and-strict-preset-security-policies-to-users)).
- The Safe Attachments policy named **Standard Preset Security Policy** that's associated with the Standard preset security policy is always applied next (if the Standard preset security policy is enabled).
- Custom Safe Attachments policies are applied next in priority order (if they're enabled):
    - A lower priority value indicates a higher priority (0 is the highest).
    - By default, a new policy is created with a priority that's lower than the lowest existing custom policy (the first is 0, the next is 1, etc.).
    - No two policies can have the same priority value.
- The Safe Attachments policy named **Built-in protection (Microsoft)** that's associated with Built-in protection always has the priority value **Lowest**, and you can't change it.

Safe Attachments protection stops for a recipient after the first policy is applied (the highest priority policy for that recipient). For more information, see [Order and precedence of email protection](how-policies-and-protections-are-combined).

After you select the custom Safe Attachments policy by clicking anywhere in the row other than the check box next to the name, you can increase or decrease the priority of the policy in the details flyout that opens:

- The custom policy with the **Priority** value **0** on the **Safe Attachments** page has the ![](media/defender-portal-icon-decrease.png)**Decrease priority** action at the top of the details flyout.
- The custom policy with the lowest priority (highest **Priority** value; for example, **3**) has the ![](media/defender-portal-icon-increase.png)**Increase priority** action at the top of the details flyout.
- If you have three or more policies, the policies between **Priority** 0 and the lowest priority have both the ![](media/defender-portal-icon-increase.png)**Increase priority** and the ![](media/defender-portal-icon-decrease.png)**Decrease priority** actions at the top of the details flyout.

When you're finished in the policy details flyout, select **Close**.

Back on the **Safe Attachments** page, the order of the policy in the list matches the updated **Priority** value.

### Use the Microsoft Defender portal to remove custom Safe Attachments policies

You can't remove the Safe Attachments policies named **Standard Preset Security Policy**, **Strict Preset Security Policy**, or **Built-in protection (Microsoft)** that are associated with [preset security policies](preset-security-policies).

After you select the custom Safe Attachments policy, use either of the following methods to remove it:

- **On the Safe Attachments page**: Select ![](media/defender-portal-icon-more-actions.png)**More actions** &gt; **Delete selected policies**.
- **In the details flyout of the policy**: Select ![](media/defender-portal-icon-delete.png)**Delete policy** at the top of the flyout.

Select **Yes** in the warning dialog that opens.

Back on the **Safe Attachments** page, the removed policy is no longer listed.

## Use Exchange Online PowerShell to configure Safe Attachments policies

In PowerShell, the basic elements of a Safe Attachments policy are:

- **The safe attachment policy**: Specifies the actions for detections, whether to send messages with detected attachments to a specified email address, and whether to deliver messages if Safe Attachments scanning can't complete.
- **The safe attachment rule**: Specifies the priority and recipient filters (who the policy applies to).

The difference between these two elements isn't obvious when you manage Safe Attachments policies in the Microsoft Defender portal:

- When you create a Safe Attachments policy in the Defender portal, you're actually creating a safe attachment rule and the associated safe attachment policy at the same time using the same name for both.
- When you modify a Safe Attachments policy in the Defender portal, settings related to the name, priority, enabled or disabled, and recipient filters modify the safe attachment rule. All other settings modify the associated safe attachment policy.
- When you remove a Safe Attachments policy from the Defender portal, the safe attachment rule and the associated safe attachment policy are removed.

In PowerShell, the difference between safe attachment policies and safe attachment rules is apparent. You manage safe attachment policies by using the **\*-SafeAttachmentPolicy** cmdlets, and you manage safe attachment rules by using the **\*-SafeAttachmentRule** cmdlets.

- In PowerShell, you create the safe attachment policy first, then you create the safe attachment rule, which identifies the associated policy that the rule applies to.
- In PowerShell, you modify the settings in the safe attachment policy and the safe attachment rule separately.
- When you remove a safe attachment policy from PowerShell, the corresponding safe attachment rule isn't automatically removed, and vice versa.

### Use PowerShell to create Safe Attachments policies

Creating a Safe Attachments policy in PowerShell is a two-step process:

1. Create the safe attachment policy.
2. Create the safe attachment rule that specifies the safe attachment policy that the rule applies to.

**Notes**:

- You can create a new safe attachment rule and assign an existing, unassociated safe attachment policy to it. A safe attachment rule can't be associated with more than one safe attachment policy.
- You can configure the following settings on new safe attachment policies in PowerShell that aren't available in the Microsoft Defender portal until after you create the policy:

    - Create the new policy as disabled (*Enabled*`$false` on the **New-SafeAttachmentRule** cmdlet).
    - Set the priority of the policy during creation (*Priority* *&lt;Number&gt;*) on the **New-SafeAttachmentRule** cmdlet).
- A new safe attachment policy that you create in PowerShell isn't visible in the Microsoft Defender portal until you assign the policy to a safe attachment rule.

#### Step 1: Use PowerShell to create a safe attachment policy

To create a safe attachment policy, use this syntax:

```powershell
New-SafeAttachmentPolicy -Name "<PolicyName>" -Enable $true [-AdminDisplayName "<Comments>"] [-Action <Allow | Block | DynamicDelivery>] [-Redirect <$true | $false>] [-RedirectAddress <SMTPEmailAddress>] [-QuarantineTag <QuarantinePolicyName>] [-EnableBlockingEncryptedAttachments <$true | $false>] [-ExcludedTypesFromBlockingEncryptedAttachments <FileTypes>] [-QuarantineTagForBlockingEncryptedAttachments <QuarantinePolicyName>]
```

This example creates a safe attachment policy named Contoso All with the following values:

- Block messages that are found to contain harmful attachments by Safe Attachments scanning (we aren't using the *Action* parameter, and the default value is `Block`).
- The default quarantine policy is used (AdminOnlyAccessPolicy), because we aren't using the *QuarantineTag* parameter.

```powershell
New-SafeAttachmentPolicy -Name "Contoso All" -Enable $true
```

For detailed syntax and parameter information, see [New-SafeAttachmentPolicy](/en-us/powershell/module/exchangepowershell/new-safeattachmentpolicy).

Tip

For detailed instructions to specify the quarantine policy to use in a safe attachment policy, see [Use PowerShell to specify the quarantine policy in Safe Attachments policies](quarantine-policies#safe-attachments-policies-in-powershell).

#### Step 2: Use PowerShell to create a safe attachment rule

To create a safe attachment rule, use this syntax:

```powershell
New-SafeAttachmentRule -Name "<RuleName>" -SafeAttachmentPolicy "<PolicyName>" <Recipient filters> [<Recipient filter exceptions>] [-Comments "<OptionalComments>"] [-Enabled <$true | $false>]
```

This example creates a safe attachment rule named Contoso All with the following conditions:

- The rule is associated with the safe attachment policy named Contoso All.
- The rule applies to all recipients in the contoso.com domain.
- Because we aren't using the *Priority* parameter, the default priority is used.
- The rule is enabled (we aren't using the *Enabled* parameter, and the default value is `$true`).

```powershell
New-SafeAttachmentRule -Name "Contoso All" -SafeAttachmentPolicy "Contoso All" -RecipientDomainIs contoso.com
```

For detailed syntax and parameter information, see [New-SafeAttachmentRule](/en-us/powershell/module/exchangepowershell/new-safeattachmentrule).

### Use PowerShell to view safe attachment policies

To view existing safe attachment policies, use the following syntax:

```powershell
Get-SafeAttachmentPolicy [-Identity "<PolicyIdentity>"] [| <Format-Table | Format-List> <Property1,Property2,...>]
```

This example returns a summary list of all safe attachment policies.

```powershell
Get-SafeAttachmentPolicy
```

This example returns detailed information for the safe attachment policy named Contoso Executives.

```powershell
Get-SafeAttachmentPolicy -Identity "Contoso Executives" | Format-List
```

For detailed syntax and parameter information, see [Get-SafeAttachmentPolicy](/en-us/powershell/module/exchangepowershell/get-safeattachmentpolicy).

### Use PowerShell to view safe attachment rules

To view existing safe attachment rules, use the following syntax:

```powershell
Get-SafeAttachmentRule [-Identity "<RuleIdentity>"] [-State <Enabled | Disabled>] [| <Format-Table | Format-List> <Property1,Property2,...>]
```

This example returns a summary list of all safe attachment rules.

```powershell
Get-SafeAttachmentRule
```

To filter the list by enabled or disabled rules, run the following commands:

```powershell
Get-SafeAttachmentRule -State Disabled
```

```powershell
Get-SafeAttachmentRule -State Enabled
```

This example returns detailed information for the safe attachment rule named Contoso Executives.

```powershell
Get-SafeAttachmentRule -Identity "Contoso Executives" | Format-List
```

For detailed syntax and parameter information, see [Get-SafeAttachmentRule](/en-us/powershell/module/exchangepowershell/get-safeattachmentrule).

### Use PowerShell to modify safe attachment policies

You can't rename a safe attachment policy in PowerShell (the **Set-SafeAttachmentPolicy** cmdlet has no *Name* parameter). When you rename a Safe Attachments policy in the Microsoft Defender portal, you're only renaming the safe attachment *rule*.

Otherwise, the same settings are available when you create a safe attachment policy as described in Step 1: Use PowerShell to create a safe attachment policy.

To modify a safe attachment policy, use this syntax:

```powershell
Set-SafeAttachmentPolicy -Identity "<PolicyName>" <Settings>
```

For detailed syntax and parameter information, see [Set-SafeAttachmentPolicy](/en-us/powershell/module/exchangepowershell/set-safeattachmentpolicy).

Tip

For detailed instructions to specify the quarantine policy to use in a safe attachment policy, see [Use PowerShell to specify the quarantine policy in Safe Attachments policies](quarantine-policies#safe-attachments-policies-in-powershell).

### Use PowerShell to modify safe attachment rules

The only setting that's not available when you modify a safe attachment rule in PowerShell is the *Enabled* parameter that allows you to create a disabled rule. To enable or disable existing safe attachment rules, see the next section.

Otherwise, the same settings are available when you create a rule as described in Step 2: Use PowerShell to create a safe attachment rule.

To modify a safe attachment rule, use this syntax:

```powershell
Set-SafeAttachmentRule -Identity "<RuleName>" <Settings>
```

For detailed syntax and parameter information, see [Set-SafeAttachmentRule](/en-us/powershell/module/exchangepowershell/set-safeattachmentrule).

### Use PowerShell to enable or disable safe attachment rules

Enabling or disabling a safe attachment rule in PowerShell enables or disables the whole Safe Attachments policy (the safe attachment rule and the assigned safe attachment policy).

To enable or disable a safe attachment rule in PowerShell, use this syntax:

```powershell
<Enable-SafeAttachmentRule | Disable-SafeAttachmentRule> -Identity "<RuleName>"
```

This example disables the safe attachment rule named Marketing Department.

```powershell
Disable-SafeAttachmentRule -Identity "Marketing Department"
```

This example enables same rule.

```powershell
Enable-SafeAttachmentRule -Identity "Marketing Department"
```

For detailed syntax and parameter information, see [Enable-SafeAttachmentRule](/en-us/powershell/module/exchangepowershell/enable-safeattachmentrule) and [Disable-SafeAttachmentRule](/en-us/powershell/module/exchangepowershell/disable-safeattachmentrule).

### Use PowerShell to set the priority of safe attachment rules

The highest priority value you can set on a rule is 0. The lowest value you can set depends on the number of rules. For example, if you have five rules, you can use the priority values 0 through 4. Changing the priority of an existing rule can have a cascading effect on other rules. For example, you have five custom rules (priorities 0 through 4), and you change the priority of a rule to 2. The existing rule with priority 2 is changed to priority 3, and the rule with priority 3 is changed to priority 4.

To set the priority of a safe attachment rule in PowerShell, use the following syntax:

```powershell
Set-SafeAttachmentRule -Identity "<RuleName>" -Priority <Number>
```

This example sets the priority of the rule named Marketing Department to 2. All existing rules with priority less than or equal to 2 are decreased by 1 (their priority numbers are increased by 1).

```powershell
Set-SafeAttachmentRule -Identity "Marketing Department" -Priority 2
```

**Note**: To set the priority of a new rule when you create it, use the *Priority* parameter on the **New-SafeAttachmentRule** cmdlet instead.

For detailed syntax and parameter information, see [Set-SafeAttachmentRule](/en-us/powershell/module/exchangepowershell/set-safeattachmentrule).

### Use PowerShell to remove safe attachment policies

When you use PowerShell to remove a safe attachment policy, the corresponding safe attachment rule isn't removed.

To remove a safe attachment policy in PowerShell, use this syntax:

```powershell
Remove-SafeAttachmentPolicy -Identity "<PolicyName>"
```

This example removes the safe attachment policy named Marketing Department.

```powershell
Remove-SafeAttachmentPolicy -Identity "Marketing Department"
```

For detailed syntax and parameter information, see [Remove-SafeAttachmentPolicy](/en-us/powershell/module/exchangepowershell/remove-safeattachmentpolicy).

### Use PowerShell to remove safe attachment rules

When you use PowerShell to remove a safe attachment rule, the corresponding safe attachment policy isn't removed.

To remove a safe attachment rule in PowerShell, use this syntax:

```powershell
Remove-SafeAttachmentRule -Identity "<PolicyName>"
```

This example removes the safe attachment rule named Marketing Department.

```powershell
Remove-SafeAttachmentRule -Identity "Marketing Department"
```

For detailed syntax and parameter information, see [Remove-SafeAttachmentRule](/en-us/powershell/module/exchangepowershell/remove-safeattachmentrule).

## How do you know these procedures worked?

To verify you successfully created, modified, or removed Safe Attachments policies, do any of the following steps:

- On the **Safe Attachments** page in the Microsoft Defender portal at https://security.microsoft.com/safeattachmentv2, verify the list of policies, their **Status** values, and their **Priority** values. To view more details, select the policy from the list by clicking on the name, and view the details in the fly out.
- In Exchange Online PowerShell, replace &lt;Name&gt; with the name of the policy or rule, run the following commands, and verify the settings:

    ```powershell
    Get-SafeAttachmentPolicy -Identity "<Name>" | Format-List; Get-SafeAttachmentRule -Identity "<Name>" | Format-List
    ```
- To verify that Safe Attachments is scanning messages, check the available Defender for Office 365 reports. For more information, see [View reports for Defender for Office 365](reports-defender-for-office-365) and [Use Explorer in the Microsoft Defender portal](threat-explorer-real-time-detections-about).