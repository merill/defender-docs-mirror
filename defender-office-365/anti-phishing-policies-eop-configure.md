---
layout: Conceptual
title: Configure anti-phishing policies for all cloud mailboxes - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/anti-phishing-policies-eop-configure
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
ms.assetid: 
ms.collection:
- m365-security
- tier2
ms.custom:
- msecd-doc-authoring-1016
- sfi-ga-nochange
description: Admins can learn how to create, modify, and delete the anti-phishing policies for all cloud mailboxes.
ms.service: defender-office-365
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 6fce70a4-1987-46ef-bac4-c2ed449ffa11
document_version_independent_id: 6fce70a4-1987-46ef-bac4-c2ed449ffa11
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/anti-phishing-policies-eop-configure.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: anti-phishing-policies-eop-configure
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/anti-phishing-policies-eop-configure.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
platformId: a5b6250e-3088-8ad8-d0a8-26ce45bd68a1
---

# Configure anti-phishing policies for all cloud mailboxes - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

In all organizations with cloud mailboxes, anti-phishing policies for all cloud mailboxes provide anti-spoofing protection. For more information, see [Spoof settings in anti-phishing policies](anti-phishing-policies-about#spoof-settings).

The default anti-phishing policy automatically applies to all recipients. For greater granularity, you can also create custom anti-phishing policies that apply to specific users, groups, or domains in your organization.

Tip

Instead of creating and managing custom anti-phishing policies, we typically recommend turning on and adding all users to the Standard and/or Strict preset security policies. For more information, see [Configure threat policies](mdo-deployment-guide#step-2-configure-threat-policies).

You configure anti-phishing policies in the Microsoft Defender portal or in [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

For anti-phishing policy procedures in organizations with Microsoft Defender for Office 365, see [Configure anti-phishing policies in Microsoft Defender for Office 365](anti-phishing-policies-mdo-configure).

## What do you need to know before you begin?

- You open the Microsoft Defender portal at https://security.microsoft.com. To go directly to the **Anti-phishing** page, use https://security.microsoft.com/antiphishing.
- To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).
- You need to be assigned permissions before you can do the procedures in this article. You have the following options:

    - [Microsoft Defender XDR Unified role based access control (RBAC)](/en-us/defender-xdr/manage-rbac) (If **Email & collaboration** &gt; **Defender for Office 365** permissions is ![](media/scc-toggle-on.png)**Active**. Affects the Defender portal only, not PowerShell): **Authorization and settings/Security settings/Core Security settings (manage)** or **Authorization and settings/Security settings/Core Security settings (read)**.
    - [Exchange Online permissions](/en-us/exchange/permissions-exo/permissions-exo):

        - *Add, modify, and delete policies*: Membership in the **Organization Management** or **Security Administrator** role groups.
        - *Read-only access to policies*: Membership in the **Global Reader**, **Security Reader**, or **View-Only Organization Management** role groups.
    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in the **Global Administrator**^\*^, **Security Administrator**, **Global Reader**, or **Security Reader** roles gives users the required permissions *and* permissions for other features in Microsoft 365.

        Important

        ^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.
- For our recommended settings for anti-phishing policies in Defender for Office 365, see [Anti-phishing policy settings in Microsoft Defender for Office 365](recommended-settings-for-eop-and-office365#anti-phishing-policy-settings-in-microsoft-defender-for-office-365).

    Tip

    Settings in the default or custom anti-phishing policies are ignored if a recipient is also included in the [Standard or Strict preset security policies](preset-security-policies). For more information, see [Order and precedence of email protection](how-policies-and-protections-are-combined).
- Allow up to 30 minutes for a new or updated policy to be applied.

## Use the Microsoft Defender portal to create anti-phishing policies

1. In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Threat policies** &gt; **Anti-phishing** in the **Policies** section. To go directly to the **Anti-phishing** page, use https://security.microsoft.com/antiphishing.
2. On the **Anti-phishing** page, select ![](media/defender-portal-icon-create.png)**Create** to open the new anti-phishing policy wizard.
3. On the **Policy name** page, configure these settings:

    - **Name**: Enter a unique, descriptive name for the policy.
    - **Description**: Enter an optional description for the policy.

    When you're finished on the **Policy name** page, select **Next**.
4. On the **Users, groups, and domains** page, identify the internal recipients that the policy applies to (recipient conditions):

    - **Users**: The specified mailboxes, or mail users.
    - **Groups**:

        - Members of the specified distribution groups or mail-enabled security groups (dynamic distribution groups aren't supported).
        - The specified Microsoft 365 Groups (dynamic membership groups in Microsoft Entra ID aren't supported).
    - **Domains**: All recipients in the organization with a primary email address in the specified [accepted domain](/en-us/exchange/mail-flow-best-practices/manage-accepted-domains/manage-accepted-domains).

        Tip

        Subdomains are automatically included unless you specifically exclude them. For example, a policy that includes contoso.com also includes marketing.contoso.com unless you exclude marketing.contoso.com.

    Click in the appropriate box, start typing a value, and select the value that you want from the results. Repeat this process as many times as necessary. To remove an existing value, select ![](media/defender-portal-icon-remove-selection.png) next to the value.

    For users or groups, you can use most identifiers (name, display name, alias, email address, account name, etc.), but the corresponding display name is shown in the results. For users or groups, enter an asterisk (\*) by itself to see all available values.

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

    When you're finished on the **Users, groups, and domains** page, select **Next**.
5. On the **Phishing threshold & protection** page, use the **Enable spoof intelligence** check box to turn spoof intelligence on or off. This setting is selected by default, and we recommend that you leave it selected. You specify the action to take on messages from blocked spoofed senders on the next page.

    To turn off spoof intelligence, clear the check box.

    Note

    You don't need to turn off spoof intelligence if your MX record doesn't point to Microsoft 365; you enable Enhanced Filtering for Connectors instead. For instructions, see [Enhanced Filtering for Connectors in Exchange Online](/en-us/Exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/enhanced-filtering-for-connectors).

    When you're finished on the **Phishing threshold & protection** page, select **Next**.
6. On the **Actions** page, configure the following settings:

    - **Honor DMARC record policy when the message is detected as spoof**: This setting is selected by default, and allows you to control what happens to messages where the sender fails explicit [DMARC](email-authentication-dmarc-configure) checks and the DMARC policy is set to `p=quarantine` or `p=reject`:

        - **If the message is detected as spoof and DMARC Policy is set as p=quarantine**: Select one of the following actions:

            - **Quarantine the message**: The default value.
            - **Move message to the recipients' Junk Email folders**
        - **If the message is detected as spoof and DMARC Policy is set as p=reject**: Select one of the following actions:

            - **Quarantine the message**
            - **Reject the message**: The default value.

        For more information, see [Spoof protection and sender DMARC policies](anti-phishing-policies-about#spoof-protection-and-sender-dmarc-policies).
    - **If the message is detected as spoof by spoof intelligence**: This setting is available only if you selected **Enable spoof intelligence** on the previous page. Select one of the following actions in the dropdown list for messages from blocked spoofed senders:

        - **Move the message to the recipients' Junk Email folders** (default)
        - **Quarantine the message**: If you select this action, an **Apply quarantine policy** box appears where you select the quarantine policy that applies to messages that are quarantined by spoof intelligence protection.

            If you don't select a quarantine policy, the default quarantine policy for spoof intelligence detections is used (DefaultFullAccessPolicy). When you later view or edit the anti-phishing policy settings, the quarantine policy name is shown.
    - **Safety tips & indicators** section: Configure the following settings:

        - **Show first contact safety tip**: For more information, see [First contact safety tip](anti-phishing-policies-about#first-contact-safety-tip).
        - **Show (?) for unauthenticated senders for spoof**: This setting is available only if you selected **Enable spoof intelligence** on the previous page. Adds a question mark (?) to the sender's photo in the From box in Outlook if the message doesn't pass SPF or DKIM checks **and** the message doesn't pass DMARC or [composite authentication](email-authentication-about#composite-authentication). This setting is selected by default.
        - **Show "via" tag**: This setting is available only if you selected **Enable spoof intelligence** on the previous page. Adds tag named via (`chris@contoso.com` via fabrikam.com) to the From address if it's different from the domain in the DKIM signature or the **MAIL FROM** address. This setting is selected by default.

        To turn on a setting, select the check box. To turn it off, clear the check box.

        For examples of what these indicators look like, see [Unauthenticated sender indicators](anti-phishing-policies-about#unauthenticated-sender-indicators).

    When you're finished on the **Actions** page, select **Next**.
7. On the **Review** page, review your settings. You can select **Edit** in each section to modify the settings within the section. Or you can select **Back** or the specific page in the wizard.

    When you're finished on the **Review** page, select **Submit**.
8. On the **New anti-phishing policy created** page, you can select the links to view the policy, view anti-phishing policies, and learn more about anti-phishing policies.

    When you're finished on the **New anti-phishing policy created** page, select **Done**.

    Back on the **Anti-phishing** page, the new policy is listed.

## Use the Microsoft Defender portal to view anti-phishing policy details

In the Microsoft Defender portal, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Threat policies** &gt; **Anti-phishing** in the **Policies** section. Or, to go directly to the **Anti-phishing** page, use https://security.microsoft.com/antiphishing.

On the **Anti-phishing** page, the following properties are displayed in the list of anti-phishing policies:

- **Name**
- **Status**: Values are:
    - **Always on** for the default anti-phishing policy.
    - **On** or **Off** for other anti-spam policies.
- **Priority**: For more information, see the Set the priority of custom anti-phishing policies section.

To change the list of policies from normal to compact spacing, select ![](media/defender-portal-icon-standard.png)**Change list spacing to compact or normal**, and then select ![](media/defender-portal-icon-compact.png)**Compact list**.

Use ![](media/defender-portal-icon-filter.png)**Filter** to filter the policies by **Time range** (creation date) or **Status**.

Use the ![](media/defender-portal-icon-search.png)**Search** box and a corresponding value to find specific anti-phishing policies.

Use ![](media/defender-portal-icon-download.png)**Export** to export the list of policies to a CSV file.

Select a policy by clicking anywhere in the row other than the check box next to the name to open the details flyout for the policy.

Tip

To see details about other anti-phishing policies without leaving the details flyout, use ![](media/updownarrows.png)**Previous item** and **Next item** at the top of the flyout.

## Use the Microsoft Defender portal to take action on anti-phishing policies

Use the following steps to enable, disable, delete, or modify anti-phishing policies in the Microsoft Defender portal.

1. In the Microsoft Defender portal, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Threat policies** &gt; **Anti-phishing** in the **Policies** section. Or, to go directly to the **Anti-phishing** page, use https://security.microsoft.com/antiphishing.
2. On the **Anti-phishing** page, select the anti-phishing policy by using either of the following methods:

    - Select the policy from the list by selecting the check box next to the name. The following actions are available in the ![](media/defender-portal-icon-more-actions.png)**More actions** dropdown list that appears:

        - **Enable selected policies**.
        - **Disable selected policies**.
        - **Delete selected policies**.

        [![The Anti-phishing page with a policy selected and the More actions control expanded.](media/anti-phishing-policies-main-page.png)](media/anti-phishing-policies-main-page.png#lightbox)
    - Select the policy from the list by clicking anywhere in the row other than the check box next to the name. Some or all following actions are available in the details flyout that opens:

        - Modify policy settings by clicking **Edit** in each section (custom policies or the default policy)
        - ![](media/defender-portal-icon-turn-on-off.png)**Turn on** or ![](media/defender-portal-icon-turn-on-off.png)**Turn off** (custom policies only)
        - ![](media/defender-portal-icon-increase.png)**Increase priority** or ![](media/defender-portal-icon-decrease.png)**Decrease priority** (custom policies only)
        - ![](media/defender-portal-icon-delete.png)**Delete policy** (custom policies only)

        [![The details flyout of a custom anti-phishing policy.](media/anti-phishing-policies-details-flyout.png)](media/anti-phishing-policies-details-flyout.png#lightbox)

The modify, enable or disable, set priority, and remove actions are described in the following sections: Modify anti-phishing policies, Enable or disable custom anti-phishing policies, Set the priority of custom anti-phishing policies, and Remove custom anti-phishing policies.

### Use the Microsoft Defender portal to modify anti-phishing policies

After you select the default anti-phishing policy or a custom policy by clicking anywhere in the row other than the check box next to the name, the policy settings are shown in the details flyout that opens. Select **Edit** in each section to modify the settings within the section. The editable settings include the policy name and description, recipient filters (users, groups, and domains), spoof intelligence protection, actions for spoofing and DMARC failures, and safety tips and indicators. For more information about these settings, see Use the Microsoft Defender portal to create anti-phishing policies.

For the default policy, you can't modify the name of the policy, and there are no recipient filters to configure (the policy applies to all recipients). But, you can modify all other settings in the policy.

For the anti-phishing policies named **Standard Preset Security Policy** and **Strict Preset Security Policy** that are associated with [preset security policies](preset-security-policies), you can't modify the policy settings in the details flyout. Instead, you select ![](media/defender-portal-icon-open.png)**View preset security policies** in the details flyout to go to the **Preset security policies** page at https://security.microsoft.com/presetSecurityPolicies to modify the preset security policies.

### Use the Microsoft Defender portal to enable or disable custom anti-phishing policies

You can't disable the default anti-phishing policy (it's always enabled).

You can't enable or disable the anti-phishing policies that are associated with Standard and Strict preset security policies. You enable or disable the Standard or Strict preset security policies on the **Preset security policies** page at https://security.microsoft.com/presetSecurityPolicies.

After you select an enabled custom anti-phishing policy (the **Status** value is **On**), use either of the following methods to disable it:

- **On the Anti-phishing page**: Select ![](media/defender-portal-icon-more-actions.png)**More actions** &gt; **Disable selected policies**.
- **In the details flyout of the policy**: Select ![](media/defender-portal-icon-turn-on-off.png)**Turn off** at the top of the flyout.

After you select a disabled custom anti-phishing policy (the **Status** value is **Off**), use either of the following methods to enable it:

- **On the Anti-phishing page**: Select ![](media/defender-portal-icon-more-actions.png)**More actions** &gt; **Enable selected policies**.
- **In the details flyout of the policy**: Select ![](media/defender-portal-icon-turn-on-off.png)**Turn on** at the top of the flyout.

On the **Anti-phishing** page, the **Status** value of the policy is now **On** or **Off**.

### Use the Microsoft Defender portal to set the priority of custom anti-phishing policies

Anti-phishing policies are processed in the order they're displayed on the **Anti-phishing** page:

- The anti-phishing policy named **Strict Preset Security Policy** that's associated with the Strict preset security policy is always applied first (if the Strict preset security policy is [assigned to users in the Defender portal](preset-security-policies#use-the-microsoft-defender-portal-to-assign-standard-and-strict-preset-security-policies-to-users)).
- The anti-phishing policy named **Standard Preset Security Policy** that's associated with the Standard preset security policy is always applied next (if the Standard preset security policy is enabled).
- Custom anti-phishing policies are applied next in priority order (if they're enabled):
    - A lower priority value indicates a higher priority (0 is the highest).
    - By default, a new policy is created with a priority that's lower than the lowest existing custom policy (the first is 0, the next is 1, etc.).
    - No two policies can have the same priority value.
- The default anti-phishing policy always has the priority value **Lowest**, and you can't change it.

Anti-phishing protection stops for a recipient after the first policy is applied (the highest priority policy for that recipient). For more information, see [Order and precedence of email protection](how-policies-and-protections-are-combined).

After you select the custom anti-phishing policy by clicking anywhere in the row other than the check box next to the name, you can increase or decrease the priority of the policy in the details flyout that opens:

- The custom policy with the **Priority** value **0** on the **Anti-Phishing** page has the ![](media/defender-portal-icon-decrease.png)**Decrease priority** action at the top of the details flyout.
- The custom policy with the lowest priority (highest **Priority** value; for example, **3**) has the ![](media/defender-portal-icon-increase.png)**Increase priority** action at the top of the details flyout.
- If you have three or more policies, the policies between **Priority** 0 and the lowest priority have both the ![](media/defender-portal-icon-increase.png)**Increase priority** and the ![](media/defender-portal-icon-decrease.png)**Decrease priority** actions at the top of the details flyout.

When you're finished in the policy details flyout, select **Close**.

Back on the **Anti-phishing** page, the order of the policy in the list matches the updated **Priority** value.

### Use the Microsoft Defender portal to remove custom anti-phishing policies

You can't remove the default anti-phishing policy or the anti-phishing policies named **Standard Preset Security Policy** and **Strict Preset Security Policy** that are associated with [preset security policies](preset-security-policies).

Warning

Deleting a custom anti-phishing policy permanently removes it from the policy list. Review the policy carefully before you continue.

After you select the custom anti-phishing policy, use either of the following methods to remove it:

- **On the Anti-phishing page**: Select ![](media/defender-portal-icon-more-actions.png)**More actions** &gt; **Delete selected policies**.
- **In the details flyout of the policy**: Select ![](media/defender-portal-icon-delete.png)**Delete policy** at the top of the flyout.

Select **Yes** in the warning dialog that opens.

On the **Anti-phishing** page, the deleted policy is no longer listed.

## Use Exchange Online PowerShell to configure anti-phishing policies

In PowerShell, the basic elements of an anti-phishing policy are:

- **The anti-phish policy**: Specifies the phishing protections to enable or disable, the actions to apply for those protections, and other options.
- **The anti-phish rule**: Specifies the priority and recipient filters (who the policy applies to) for the associated anti-phish policy.

The difference between these two elements isn't obvious when you manage anti-phishing policies in the Microsoft Defender portal:

- When you create a policy in the Defender portal, you're actually creating an anti-phish rule and the associated anti-phish policy at the same time using the same name for both.
- When you modify a policy in the Defender portal, settings related to the name, priority, enabled or disabled, and recipient filters modify the anti-phish rule. All other settings modify the associated anti-phish policy.
- When you remove a policy in the Defender portal, the anti-phish rule and the associated anti-phish policy are removed at the same time.

In Exchange Online PowerShell, the difference between anti-phish policies and anti-phish rules is apparent. You manage anti-phish policies by using the **\*-AntiPhishPolicy** cmdlets, and you manage anti-phish rules by using the **\*-AntiPhishRule** cmdlets.

- In PowerShell, you create the anti-phish policy first, then you create the anti-phish rule, which identifies the associated policy that the rule applies to.
- In PowerShell, you modify the settings in the anti-phish policy and the anti-phish rule separately.
- When you remove an anti-phish policy from PowerShell, the corresponding anti-phish rule isn't automatically removed, and vice versa.

### Use PowerShell to create anti-phishing policies

Use the following steps to create an anti-phishing policy and its associated rule in Exchange Online PowerShell.

Creating an anti-phishing policy in PowerShell is a two-step process:

1. Create the anti-phish policy.
2. Create the anti-phish rule that specifies the anti-phish policy that the rule applies to.

**Notes**:

- You can create a new anti-phish rule and assign an existing, unassociated anti-phish policy to it. An anti-phish rule can't be associated with more than one anti-phish policy.
- You can configure the following settings on new anti-phish policies in PowerShell that aren't available in the Microsoft Defender portal until after you create the policy:

    - Create the new policy as disabled (*Enabled*`$false` on the **New-AntiPhishRule** cmdlet).
    - Set the priority of the policy during creation (*Priority* *&lt;Number&gt;*) on the **New-AntiPhishRule** cmdlet).
- A new anti-phish policy that you create in PowerShell isn't visible in the Microsoft Defender portal until you assign the policy to an anti-phish rule.

#### Step 1: Use PowerShell to create an anti-phish policy

To create an anti-phish policy, use this syntax:

```powershell
New-AntiPhishPolicy -Name "<PolicyName>" [-AdminDisplayName "<Comments>"] [-EnableSpoofIntelligence <$true | $false>] [-AuthenticationFailAction <MoveToJmf | Quarantine>] [-HonorDmarcPolicy <$true | $false>] [-DmarcQuarantineAction <MoveToJmf | Quarantine>] [-DmarcRejectAction <Quarantine | Reject>] [-EnableUnauthenticatedSender <$true | $false>] [-EnableViaTag <$true | $false>] [-SpoofQuarantineTag <QuarantineTagName>]
```

This example creates an anti-phish policy named Research Quarantine with the following settings:

- The description is: Research department policy.
- Changes the default action for spoofing detections to Quarantine and uses the default quarantine policy for the quarantined messages (we aren't using the *SpoofQuarantineTag* parameter).
- Honoring `p=quarantine` and `p=reject` in sender DMARC policies is on by default (we aren't using the *HonorDmarcPolicy* parameter, and the default value is `$true`).
    - Messages that fail DMARC where the sender's DMARC policy is `p=quarantine` are quarantined (we aren't using the *DmarcQuarantineAction* parameter, and the default value is Quarantine).
    - Messages that fail DMARC where the sender's DMARC policy is `p=reject` are rejected (we aren't using the *DmarcRejectAction* parameter, and the default value is Reject).

```powershell
New-AntiPhishPolicy -Name "Monitor Policy" -AdminDisplayName "Research department policy" -AuthenticationFailAction Quarantine
```

For detailed syntax and parameter information, see [New-AntiPhishPolicy](/en-us/powershell/module/exchangepowershell/New-AntiPhishPolicy).

Tip

For detailed instructions to specify the quarantine policies to use in an anti-phish policy, see [Use PowerShell to specify the quarantine policy in anti-phishing policies](quarantine-policies#anti-phishing-policies).

#### Step 2: Use PowerShell to create an anti-phish rule

To create an anti-phish rule, use this syntax:

```powershell
New-AntiPhishRule -Name "<RuleName>" -AntiPhishPolicy "<PolicyName>" <Recipient filters> [<Recipient filter exceptions>] [-Comments "<OptionalComments>"]
```

This example creates an anti-phish rule named Research Department with the following conditions:

- The rule is associated with the anti-phish policy named Research Quarantine.
- The rule applies to members of the group named Research Department.
- Because we aren't using the *Priority* parameter, the default priority is used.

```powershell
New-AntiPhishRule -Name "Research Department" -AntiPhishPolicy "Research Quarantine" -SentToMemberOf "Research Department"
```

For detailed syntax and parameter information, see [New-AntiPhishRule](/en-us/powershell/module/exchangepowershell/New-AntiPhishRule).

### Use PowerShell to view anti-phish policies

To view existing anti-phish policies, use the following syntax:

```powershell
Get-AntiPhishPolicy [-Identity "<PolicyIdentity>"] [| <Format-Table | Format-List> <Property1,Property2,...>]
```

This example returns a summary list of all anti-phish policies along with the specified properties.

```powershell
Get-AntiPhishPolicy | Format-Table Name,IsDefault
```

This example returns all the property values for the anti-phish policy named Executives.

```powershell
Get-AntiPhishPolicy -Identity "Executives"
```

For detailed syntax and parameter information, see [Get-AntiPhishPolicy](/en-us/powershell/module/exchangepowershell/Get-AntiPhishPolicy).

### Use PowerShell to view anti-phish rules

To view existing anti-phish rules, use the following syntax:

```powershell
Get-AntiPhishRule [-Identity "<RuleIdentity>"] [-State <Enabled | Disabled] [| <Format-Table | Format-List> <Property1,Property2,...>]
```

This example returns a summary list of all anti-phish rules along with the specified properties.

```powershell
Get-AntiPhishRule | Format-Table Name,Priority,State
```

To filter the list by enabled or disabled rules, run the following commands:

```powershell
Get-AntiPhishRule -State Disabled | Format-Table Name,Priority
```

```powershell
Get-AntiPhishRule -State Enabled | Format-Table Name,Priority
```

This example returns all the property values for the anti-phish rule named Contoso Executives.

```powershell
Get-AntiPhishRule -Identity "Contoso Executives"
```

For detailed syntax and parameter information, see [Get-AntiPhishRule](/en-us/powershell/module/exchangepowershell/Get-AntiPhishrule).

### Use PowerShell to modify anti-phish policies

Other than the following items, the same settings are available when you modify an anti-phish policy in PowerShell as when you create a policy. These settings include spoof intelligence, authentication fail actions, DMARC policy honoring, unauthenticated sender indicators, and quarantine tags. For the full list of parameters, see [New-AntiPhishPolicy](/en-us/powershell/module/exchangepowershell/New-AntiPhishPolicy) and Step 1: Use PowerShell to create an anti-phish policy.

- The *MakeDefault* switch that turns the specified policy into the default policy (applied to everyone, always **Lowest** priority, and you can't delete it) is available only when you modify an anti-phish policy in PowerShell.
- You can't rename an anti-phish policy (the **Set-AntiPhishPolicy** cmdlet has no *Name* parameter). When you rename an anti-phishing policy in the Microsoft Defender portal, you're only renaming the anti-phish *rule*.

To modify an existing anti-phish policy in PowerShell, use this syntax:

```powershell
Set-AntiPhishPolicy -Identity "<PolicyName>" <Settings>
```

For detailed syntax and parameter information, see [Set-AntiPhishPolicy](/en-us/powershell/module/exchangepowershell/Set-AntiPhishPolicy).

Tip

For detailed instructions to specify the quarantine policy to use in an anti-phish policy, see [Use PowerShell to specify the quarantine policy in anti-phishing policies](quarantine-policies#anti-phishing-policies).

### Use PowerShell to modify anti-phish rules

The only setting that's not available when you modify an anti-phish rule in PowerShell is the *Enabled* parameter that allows you to create a disabled rule. To enable or disable existing anti-phish rules, see the next section.

Otherwise, the same settings are available when you create a rule as described in Step 2: Use PowerShell to create an anti-phish rule.

To modify an existing anti-phish rule in PowerShell, use the following syntax:

```powershell
Set-AntiPhishRule -Identity "<RuleName>" <Settings>
```

For detailed syntax and parameter information, see [Set-AntiPhishRule](/en-us/powershell/module/exchangepowershell/set-antiphishrule).

### Use PowerShell to enable or disable anti-phish rules

Enabling or disabling an anti-phish rule in PowerShell enables or disables the whole anti-phishing policy (the anti-phish rule and the assigned anti-phish policy). You can't enable or disable the default anti-phishing policy (always applied to all recipients).

To enable or disable an anti-phish rule in PowerShell, use the following syntax:

```powershell
<Enable-AntiPhishRule | Disable-AntiPhishRule> -Identity "<RuleName>"
```

This example disables the anti-phish rule named Marketing Department.

```powershell
Disable-AntiPhishRule -Identity "Marketing Department"
```

This example enables the same rule.

```powershell
Enable-AntiPhishRule -Identity "Marketing Department"
```

For detailed syntax and parameter information, see [Enable-AntiPhishRule](/en-us/powershell/module/exchangepowershell/enable-antiphishrule) and [Disable-AntiPhishRule](/en-us/powershell/module/exchangepowershell/disable-antiphishrule).

### Use PowerShell to set the priority of anti-phish rules

The highest priority value you can set on a rule is 0. The lowest value you can set depends on the number of rules. For example, if you have five rules, you can use the priority values 0 through 4. Changing the priority of an existing rule can have a cascading effect on other rules. For example, you have five custom rules (priorities 0 through 4), and you change the priority of a rule to 2. The existing rule with priority 2 is changed to priority 3, and the rule with priority 3 is changed to priority 4.

To set the priority of an anti-phish rule in PowerShell, use the following syntax:

```powershell
Set-AntiPhishRule -Identity "<RuleName>" -Priority <Number>
```

This example sets the priority of the rule named Marketing Department to 2. All existing rules with priority less than or equal to 2 are decreased by 1 (their priority numbers are increased by 1).

```powershell
Set-AntiPhishRule -Identity "Marketing Department" -Priority 2
```

**Notes**:

- To set the priority of a new rule when you create it, use the *Priority* parameter on the **New-AntiPhishRule** cmdlet instead.
- The default anti-phish policy doesn't have a corresponding anti-phish rule, and it always has the unmodifiable priority value **Lowest**.

### Use PowerShell to remove anti-phish policies

When you use PowerShell to remove an anti-phish policy, the corresponding anti-phish rule isn't removed.

Warning

Removing an anti-phish policy is permanent and doesn't remove the associated anti-phish rule. An orphaned anti-phish rule has no effect, but you should remove it separately to avoid confusion.

To remove an anti-phish policy in PowerShell, use this syntax:

```powershell
Remove-AntiPhishPolicy -Identity "<PolicyName>"
```

This example removes the anti-phish policy named Marketing Department.

```powershell
Remove-AntiPhishPolicy -Identity "Marketing Department"
```

For detailed syntax and parameter information, see [Remove-AntiPhishPolicy](/en-us/powershell/module/exchangepowershell/Remove-AntiPhishPolicy).

### Use PowerShell to remove anti-phish rules

When you use PowerShell to remove an anti-phish rule, the corresponding anti-phish policy isn't removed.

Warning

Removing an anti-phish rule is permanent. The associated anti-phish policy isn't automatically removed and no longer applies to any recipients. Remove the orphaned anti-phish policy separately if it's no longer needed.

To remove an anti-phish rule in PowerShell, use this syntax:

```powershell
Remove-AntiPhishRule -Identity "<PolicyName>"
```

This example removes the anti-phish rule named Marketing Department.

```powershell
Remove-AntiPhishRule -Identity "Marketing Department"
```

For detailed syntax and parameter information, see [Remove-AntiPhishRule](/en-us/powershell/module/exchangepowershell/Remove-AntiPhishRule).

## How do you know these procedures worked?

To verify you successfully configured anti-phishing policies for all cloud mailboxes, do any of the following steps:

- On the **Anti-phishing** page in the Microsoft Defender portal at https://security.microsoft.com/antiphishing, verify the list of policies, their **Status** values, and their **Priority** values. To view more details, select the policy from the list by clicking on the name and viewing the details in the flyout that appears.
- In Exchange Online PowerShell, replace &lt;Name&gt; with the name of the policy or rule, and then run the following commands to verify the anti-phish policy and rule settings:

    ```powershell
    Get-AntiPhishPolicy -Identity "<Name>"
    ```

    ```powershell
    Get-AntiPhishRule -Identity "<Name>"
    ```