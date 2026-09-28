---
layout: Conceptual
title: Get started with Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/mdo-deployment-guide
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: get-started
ms.localizationpriority: medium
ms.collection:
- zerotrust-solution
- tier1
- essentials-get-started
ms.custom:
- sfi-ga-nochange
description: Learn how to get started with the initial deployment and configuration of Microsoft Defender for Office 365.
ms.service: defender-office-365
ms.date: 2026-02-06T00:00:00.0000000Z
locale: en-us
document_id: 6cea39c5-a842-54e7-b246-4a3b4aaecdb2
document_version_independent_id: 6cea39c5-a842-54e7-b246-4a3b4aaecdb2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/mdo-deployment-guide.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdo-deployment-guide
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/mdo-deployment-guide.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
platformId: b6408ea0-c93d-95cf-8dbd-f68722634a97
---

# Get started with Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn

In new Microsoft 365 organizations with Microsoft Defender for Office 365 (included or as an add-on subscription), this article describes the configuration steps you need to do in the earliest days of your organization.

Although your Microsoft 365 organization includes a default level of protection from the moment you create it (or add Defender for Office 365 to it), the steps in this article give you an actionable plan to unleash the full protection capabilities of Defender for Office 365. After you complete the steps, you can also use this article to show management that you're maximizing your investment in Microsoft 365.

Tip

For information about configuring protection for Microsoft Teams, see the following articles:

- [Microsoft Defender for Office 365 support for Microsoft Teams](mdo-support-teams-about)
- [Quickly configure Microsoft Teams protection in Microsoft Defender for Office 365](mdo-support-teams-quick-configure)
- [Security Operations Guide for Teams protection in Microsoft Defender for Office 365](mdo-support-teams-sec-ops-guide)

The steps to configure Defender for Office 365 are described in the following diagram:

[![A conceptual diagram showing the steps to configure Defender for Office 365.](media/mdo-deployment-guide.png)](media/mdo-deployment-guide.png#lightbox)

Tip

As a companion to this article, see our [Microsoft Defender for Office 365 setup guide](https://setup.cloud.microsoft/defender/office-365-setup-guide) to review best practices and to protect against email, link, and collaboration threats. Features include Safe Links, Safe Attachments, and more. For a customized experience based on your environment, you can access the [Microsoft Defender for Office 365 automated setup guide](https://admin.microsoft.com/Adminportal/Home?Q=ADG#/modernonboarding/office365advancedthreatprotectionadvisor) in the Microsoft 365 admin center.

## Requirements

[The built-in security features](eop-about) are included in *all* Microsoft 365 subscriptions with cloud mailboxes. Defender for Office 365 includes more protection features. For detailed feature comparisons, see [Microsoft Defender for Office 365 overview](mdo-about).

### Roles and permissions

Configuration requires permissions. The following table lists the permissions that you need to do the steps in this article (one is enough; you don't need all of them).

| Role or role group | Learn more |
| --- | --- |
| Global Administrator in Microsoft Entra^\*^ | [Microsoft Entra built-in roles](/en-us/entra/identity/role-based-access-control/permissions-reference#global-administrator) |
| Organization Management in Email & collaboration role groups | [Role groups in Microsoft Defender for Office 365](scc-permissions#role-groups-in-microsoft-defender-for-office-365-and-microsoft-purview) |
| Security Administrator in Microsoft Entra | [Microsoft Entra built-in roles](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator) |
| Security Administrator in Email & collaboration role groups | [Email & collaboration permissions in Microsoft Defender for Office 365](scc-permissions#role-groups-in-microsoft-defender-for-office-365-and-microsoft-purview) |
| Exchange Online Organization Management | [Permissions in Exchange Online](/en-us/exchange/permissions-exo/permissions-exo) |

Important

^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.

## Step 1: Configure email authentication for your Microsoft 365 domains

**Summary**: Configure [SPF](email-authentication-spf-configure), [DKIM](email-authentication-dkim-configure), and [DMARC](email-authentication-dmarc-configure) records (in that order) for all custom Microsoft 365 domains (including parked domains and subdomains). If necessary, configure any [trusted ARC sealers](email-authentication-arc-configure).

**Details**:

Email authentication (also known as *email validation*) is a group of standards to verify that email messages are legitimate, unaltered, and come from expected sources for the sender's email domain. For more information, see [Email authentication](email-authentication-about).

We assume you're using one or more [custom domains](/en-us/exchange/mail-flow-best-practices/manage-accepted-domains/manage-accepted-domains) in Microsoft 365 for email (for example contoso.com), so you need to create specific email authentication DNS records for each custom email domain.

Create the following email authentication DNS records at your DNS registrar or DNS hosting service for each custom domain that you use for email in Microsoft 365:

- **Sender Policy Framework (SPF)**: The SPF TXT record identifies valid sources of email from senders in the domain. For instructions, see [Set up SPF to identify valid email sources for your custom cloud domains](email-authentication-spf-configure).
- **DomainKeys Identified Mail (DKIM)**: DKIM signs outbound messages and stores the signature in the message header that survives message forwarding. For instructions, see [Set up DKIM to sign mail from your cloud domain](email-authentication-dkim-configure).
- **Domain-based Message Authentication, Reporting, and Conformance (DMARC)**: DMARC helps destination email servers decide what to do with messages from the custom domain that fail SPF and DKIM checks. Be sure to include the DMARC policy (`p=reject` or `p=quarantine`) and DMARC report destinations (aggregate and forensic reports) in the DMARC records. for instructions, see [Set up DMARC to validate the From address domain for cloud senders](email-authentication-dmarc-configure).
- **Authenticated Received Chain (ARC)**: If a non-Microsoft service modifies *inbound* messages before delivery to Microsoft 365, you can identify the service as a *trusted ARC sealer* (if the service supports it). Trusted ARC sealers preserve unmodified email information so the modified messages don't automatically fail email authentication checks in Microsoft 365. For instructions, see [Configure trusted ARC sealers](email-authentication-arc-configure).

If you're using the \*.onmicrosoft.com domain for email (also known as the Microsoft Online Email Routing Address or MOERA domain), there's not nearly as much for you to do:

- **SPF**: An SPF record is already configured for the \*.onmicrosoft.com domain.
- **DKIM**: DKIM signing is already configured for outbound mail using the \*.onmicrosoft.com domain, but you can also [manually customize it](email-authentication-dkim-configure#use-the-defender-portal-to-customize-dkim-signing-of-outbound-messages-using-the-onmicrosoftcom-domain).
- **DMARC**: You need to manually set up the DMARC record for the \*.onmicrosoft.com domain as described [here](email-authentication-dmarc-configure#use-the-microsoft-365-admin-center-to-add-dmarc-txt-records-for-onmicrosoftcom-domains-in-microsoft-365).

## Step 2: Configure threat policies

**Summary**: Turn on and use the Standard and/or Strict [preset security policies](preset-security-policies) for all recipients. Or, if business needs dictate, create and use custom threat policies instead, but check them periodically using the [configuration analyzer](configuration-analyzer-for-security-policies).

**Details**:

As you can probably imagine, a lot of threat policies for email and collaboration security are available in Microsoft 365. There are three basic types of policies:

- **Default threat policies**: These policies exist from the moment the organization is created. They apply to all recipients in the organization, you can't turn off the policies, and you can't modify who the policies apply to. But you can modify the security settings in the policies just like custom threat policies. The settings in the default threat policies are described in the tables in [Recommended email and collaboration threat policy settings for cloud organizations](recommended-settings-for-eop-and-office365).
- **Preset security policies**: Preset security policies are actually *profiles* that contain *most* of the available threat policies in Defender for Office 365 with settings that are tailored to specific levels of protection. The preset security policies are:

    - The Strict preset security policy.
    - The Standard preset security policy.
    - Built-in protection.

    The Standard and Strict preset security policies are turned off by default until you turn them on. You specify recipient conditions and exceptions (users, group members, domains, or all recipients) for the built-in security features for all cloud mailboxes and protection features in Defender for Office 365 within the Standard and Strict preset security policies.

    Built-in protection in Defender for Office 365 is on by default to provides basic Safe Attachments and Safe Links protection for all recipients. You can specify recipient exceptions to identify users who don't get the protection.

    In Standard and Strict preset security policies in Defender for Office 365 organizations, you need to configure entries and optional exceptions for user and domain impersonation protection. All other settings are locked into our recommended standard and strict values (many of which are the same). You can see the Standard and Strict values in the tables in [Recommended email and collaboration threat policy settings for cloud organizations](recommended-settings-for-eop-and-office365), and you can see the differences between Standard and Strict [here](preset-security-policies#policy-settings-in-preset-security-policies).

    As new protection capabilities are added to Defender for Office 365 and as the security landscape changes, the settings in preset security policies are automatically updated to our recommended settings.
- **Custom threat policies**: For most available policies, you can create any number of custom threat policies. You can apply the policies to users using recipient conditions and exceptions (users, group members, or domains) and you can customize the settings.

The previous information and the threat policies involved are summarized in the following table:

| - | Default threat policies | Preset security policies | Custom threat policies |
| --- | --- | --- | --- |
| **Threat policies in the built-in security features for all cloud mailboxes**: |  |  |  |
| [Anti-malware](anti-malware-policies-configure) | ✔ | ✔ | ✔ |
| [Anti-spam](anti-spam-policies-configure) | ✔ | ✔ | ✔ |
| [Anti-phishing (spoofing protection)](anti-phishing-policies-about#spoof-settings) | ✔ | ✔ | ✔ |
| [Outbound spam](outbound-spam-policies-configure) | ✔ |  | ✔ |
| [Connection filtering](connection-filter-policies-configure) | ✔¹ |  |  |
| **Threat policies in Defender for Office 365**: |  |  |  |
| [Anti-phishing (spoofing protection)](anti-phishing-policies-about#spoof-settings) plus: <br>- [Impersonation protection](anti-phishing-policies-about#impersonation-settings-in-anti-phishing-policies-in-microsoft-defender-for-office-365)<br>- [Phishing email thresholds](anti-phishing-policies-about#phishing-email-thresholds-in-anti-phishing-policies-in-microsoft-defender-for-office-365) | ✔² | ✔² | ✔ |
| [Safe Links](safe-links-policies-configure) | ³ | ✔ | ✔ |
| [Safe Attachments](safe-attachments-policies-configure) | ³ | ✔ | ✔ |
| **General behavior** |  |  |  |
| Protection on by default? | ✔ | ⁴ |  |
| Configure conditions/exceptions for protection? |  | ✔⁵ | ✔ |
| Customize security settings? | ✔ | ⁶ | ✔ |
| Protection settings automatically updated? |  | ✔ |  |

¹ There are no default entries in the IP Allow List or the IP Block List, so the default connection filter policy effectively does nothing unless you customize the settings.

² There are no entries or optional exceptions for user impersonation or domain impersonation protection in Defender for Office 365 until you configure them.

³ Although there are no default Safe Attachments or Safe Links policies in Defender for Office 365, the Built-in protection preset security policy provides basic Safe Attachments and Safe Links protection that's always on.

⁴ The Built-in protection preset security policy (Safe Attachments and Safe Links protection in Defender for Office 365) is the only preset security policy that's on by default.

⁵ For the Standard and Strict preset security policies, you can configure separate recipient conditions and optional exceptions for the built-in security features for all cloud mailboxes and protections in Defender for Office 365. For Built-in protection in Defender for Office 365, you can only configure recipient exceptions from protection.

⁶ The only customizable security settings in preset security policies are the entries and optional exceptions for user impersonation protection and domain impersonation protection in the Standard and Strict preset security policies in Defender for Office 365.

### Order of precedence for threat policies

How threat policies are applied is an important consideration as you decide how to configure security settings for users. The important points to remember are:

- Protection features have an unconfigurable [order of processing](how-policies-and-protections-are-combined). For example, incoming messages are always evaluated for malware before spam.
- The threat policies of a specific feature (anti-spam, anti-malware, anti-phishing, etc.) are applied in a specific order of precedence (more on the order of precedence later).
- If a user is intentionally or unintentionally included in multiple policies of a specific feature, the first applicable threat policy for that feature (based on the order of precedence) determines what happens to the item (a message, file, URL, etc.).
- Once the first threat policy is applied to a specific item for a user, policy processing for that feature stops. No more threat policies of that feature are evaluated for that user and that specific item.

The order of precedence is explained in detail at [Order of precedence for preset security policies and other policies](preset-security-policies#order-of-precedence-for-preset-security-policies-and-other-threat-policies), but is briefly summarized here:

1. Threat policies in preset security policies:
    1. The Strict preset security policy.
    2. The Standard preset security policy.
2. Custom threat policies for a specific feature (for example, anti-malware policies). Each custom policy has a priority value that determines the order that the policy is applied in relation to other threat policies for the same feature:
    1. A custom threat policy with the priority value 0.
    2. A custom threat policy with the priority value 1.
    3. And so on.
3. The default threat policy of a specific feature (for example, anti-malware) or the Built-in protection preset security policy in Defender for Office 365 (Safe Links and Safe Attachments).

Refer to the previous table to see how a specific threat policy is represented in the precedence order. For example, anti-malware policies are present at each level. Outbound spam policies are available at the custom policy and default policy levels. The connection filter policy is available only at the default policy level.

To avoid confusion and unintended application of policies, use the following guidelines:

- Use unambiguous groups or lists of recipients at each level. For example, use different groups or lists of recipients for the Standard and Strict preset security policies.
- Configure exceptions at each level as required. For example, configure recipients who need custom threat policies as exceptions to the Standard and Strict preset security policies.
- Any remaining recipients that aren't identified at the higher levels get the default threat policies or Built-in protection in Defender for Office 365 (Safe Links and Safe Attachments).

Armed with this information, you can decide the best way to implement threat policies in the organization.

### Determine your threat policy strategy

Now that you know about the different types of threat policies and how they're applied, you can decide how you want to protect the users in your organization. Your decision inevitably falls somewhere within the following spectrum:

- Use the Standard preset security policy only.
- Use the Standard and Strict preset security policies.
- Use preset security policies and custom threat policies.
- Use custom threat policies only.

Remember, default threat policies (and the Built-in protection preset security policy in Defender for Office 365) automatically protect all recipients in the organization (anyone who isn't defined in the Standard or Strict preset security policy or in custom threat policies). So even if you do nothing, all recipients in the organization get the default protections as described in [Recommended email and collaboration threat policy settings for cloud organizations](recommended-settings-for-eop-and-office365).

It's also important to realize that you aren't locked into your initial decision forever. The information in the [recommended settings tables](recommended-settings-for-eop-and-office365) and the [comparison table for Standard and Strict](preset-security-policies#policy-settings-in-preset-security-policies) should allow you to make an informed decision. But if needs, results, or circumstances change, it's not difficult to switch to a different strategy later.

**Without a compelling business need that indicates otherwise, we recommend starting with the Standard preset security policy for all users in your organization**. Preset security policies are configured with settings based on years of observations in the Microsoft 365 datacenters, and should be the right choice for the majority of organizations. And, the policies are automatically updated to match the threats of the security landscape.

In preset security policies, you can select the **All recipients** option to easily apply protection to all recipients in the organization.

If you want to include some users in the Strict preset security policy and the remaining users in the Standard preset security policy, remember to account for the order of precedence as described earlier in this article with the following methods:

- Use unambiguous groups or lists of recipients in each preset security policy.

    or
- Configure recipients who should get the settings of the Standard preset security policy as exceptions in the Strict preset security policy.

Keep in mind that the following protection feature configurations are unaffected by preset security policies (you can use preset security policies and also independently configure these protection settings):

- [Outbound spam policies (custom and default)](outbound-spam-policies-configure)
- [The default connection filter policy (IP Allow List and IP Block List)](connection-filter-policies-configure)
- [Globally turn on Safe Attachments for SharePoint, OneDrive, and Microsoft Teams](safe-attachments-for-spo-odfb-teams-configure)
- [Globally turn on and configure Safe Documents](safe-documents-in-e5-plus-security-about) (available and meaningful only with licenses that aren't included in Defender for Office 365 (for example, Microsoft 365 A5 or Microsoft Defender Suite))

To turn on and configure preset security policies, see [Preset security policies](preset-security-policies).

The decision to use custom threat policies instead of or in addition to preset security policies ultimately comes down to the following business requirements:

- Users require security settings that are *different* from the unmodifiable settings in preset security policies (junk vs. quarantine or vice-versa, no safety tips, notify custom recipients, etc.).
- Users require settings that *aren't configured* in preset security policies (for example, blocking email from specific countries or in specific languages in anti-spam policies).
- Users need a *quarantine experience* that's different from the unmodifiable settings in preset security policies. [Quarantine policies](quarantine-policies#appendix) define what users can do to their quarantined messages based on why the message was quarantined, and whether recipients are notified about their quarantined messages. The default end-user quarantine experience is summarized in the table [in this article](quarantine-end-user) and the quarantine policies that are used in the Standard and Strict preset security policies are described in the tables [in this article](recommended-settings-for-eop-and-office365).

Use the information in [Recommended email and collaboration threat policy settings for cloud organizations](recommended-settings-for-eop-and-office365) to compare the available settings in custom threat policies or default threat policies versus what's configured in the Standard and Strict preset security policies.

Design guidelines for multiple custom threat policies for a specific feature (for example, anti-malware policies) include:

- Users in custom threat policies can't be included in the Standard or Strict preset security policies due to the order of precedence.
- Assign fewer users to higher priority policies and more users to lower priority policies.
- Configure higher priority policies to have stricter or more specialized settings than lower priority policies (including the default policies).

If you decide to use custom threat policies, use the [Configuration analyzer](configuration-analyzer-for-security-policies) to periodically compare the settings in your policies to the recommended settings in the Standard and Strict preset security policies.

## Step 3: Assign permissions to admins

**Summary**: Assign the [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator) role in Microsoft Entra to other admins, specialists, and help desk personnel so they can do security tasks in Defender for Office 365.

**Details**:

You're probably already using the initial account that you used to enroll in Microsoft 365 to do all the work in this deployment guide. That account is an admin everywhere in Microsoft 365 (specifically, it's a member of the [Global Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#global-administrator) role in Microsoft Entra), and allows you to do pretty much anything. The required permissions were described earlier in this article at Roles and permissions.

But, the intent of this step is to configure other admins to help you manage the features Defender for Office 365 in the future. What you don't want is a lot of people with Global Administrator power who don't need it. For example, do they really need to delete/create accounts or make other users Global Administrators? The concept of *least privilege* (assigning only the required permissions to do the job and nothing more) is a good practice to follow.

When it comes to assigning permissions for tasks Defender for Office 365, the following options are available:

- [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): These permissions apply to all workloads in Microsoft 365 (Exchange Online, SharePoint, Microsoft Teams, etc.).
- [Exchange Online permissions](/en-us/exchange/permissions-exo/permissions-exo): Most tasks in Defender for Office 365 are available using Exchange Online permissions. Assigning permissions only in Exchange Online prevents administrative access in other Microsoft 365 workloads.
- [Email & collaboration permissions in the Microsoft Defender portal](scc-permissions): Administration of some security features in Defender for Office 365 is available with Email & collaboration permissions. For example:
    - [Configuration analyzer](configuration-analyzer-for-security-policies)
    - [Admin quarantine management](quarantine-admin-manage-messages-files) and [quarantine policies](quarantine-policies)
    - [Admin submissions and review of user reported messages](submissions-admin-review-user-reported-messages)
    - [User tags](user-tags-about)

**For simplicity, we recommend using the [Security Administrator](/en-us/entra/identity/role-based-access-control/permissions-reference#security-administrator) role in Microsoft Entra for others who need to configure settings in Defender for Office 365.**

For instructions, see [Assign Microsoft Entra roles to users](/en-us/entra/identity/role-based-access-control/manage-roles-portal) and [Manage access to Microsoft Defender XDR with Microsoft Entra global roles](/en-us/defender-xdr/m365d-permissions).

## Step 4: Priority accounts and user tags

**Summary**: Identify and tag the appropriate users in your organization as [priority accounts](/en-us/microsoft-365/admin/setup/priority-accounts) for easier identification in reports and investigations, and to receive [priority account protection](priority-accounts-turn-on-priority-account-protection) in Defender for Office 365. Consider creating and applying custom [user tags](user-tags-about) in Defender for Office 365 Plan 2.

**Details**:

In Defender for Office 365, priority accounts allows you to tag up to 250 high value users for ease of identification in reports and investigations. These priority account also receive additional heuristics that don't benefit regular employees. For more information, see [Manage and monitor priority accounts](/en-us/microsoft-365/admin/setup/priority-accounts) and [Configure and review priority account protection in Microsoft Defender for Office 365](priority-accounts-turn-on-priority-account-protection).

In Defender for Office 365 Plan 2, you also have access to create and apply custom *user tags* to easily identify specific groups of users in reports and investigations. For more information, see [User tags in Microsoft Defender for Office 365](user-tags-about).

**Identify appropriate users to tag as priority accounts, and decide if you need to create and apply custom user tags.**

## Step 5: Review and configure user reported message settings

**Summary**: Use the [built-in Report button in Outlook](submissions-outlook-report-messages#use-the-built-in-report-button-in-outlook) or a [supported non-Microsoft tool](submissions-user-reported-messages-custom-mailbox#message-submission-format-for-non-microsoft-reporting-tools) so users can report false positives and false negatives in Outlook, and so those reported messages are available to admins on the **User reported** tab of the **Submissions** page in the Defender portal. Configure the organization so reported messages go to a specified reporting mailbox, to Microsoft, or both.

**Details**:

The ability of users to report good messages marked as bad (false positives) or bad messages allowed (false negatives) is important for you to monitor and adjust protection settings in Defender for Office 365.

The important parts of user message reporting are:

- **How do users report messages?**: Make sure clients are using one of the following methods so reported messages appear on the **User reported** tab of the **Submissions** page in the Defender portal at https://security.microsoft.com/reportsubmission?viewid=user:
- The built-in **Report** button in Outlook on the web (formerly known as Outlook Web App or OWA).
- Non-Microsoft reporting tools that use the [supported message submission format](submissions-user-reported-messages-custom-mailbox#message-submission-format-for-non-microsoft-reporting-tools).

    Tip

    In [attack simulation training in Defender for Office 365 Plan 2](attack-simulation-training-get-started), simulation messages reported by non-Microsoft tools aren't captured in attack simulation reports.
- **Where do user reported messages go?**: You have the following options:

    - To a designated reporting mailbox and to Microsoft (this value is the default).
    - To a designated reporting mailbox only.
    - To Microsoft only.

    The default mailbox that's used to collect user reported messages is the Global Administrator's mailbox (the initial account in the organization). If you want user reported messages to go to a reporting mailbox in your organization, you should [create](/en-us/exchange/recipients-in-exchange-online/create-user-mailboxes) and [configure](submissions-user-reported-messages-custom-mailbox#configuration-requirements-for-the-reporting-mailbox) an exclusive mailbox to use.

    It's up to you whether you want user reported messages to also go to Microsoft for analysis (exclusively or along with delivery to your designated reporting mailbox).

    If you want user reported messages to go only to your designated reporting mailbox, admins should [manually submit user reported messages to Microsoft for analysis](submissions-admin#submit-user-reported-messages-to-microsoft-for-analysis) from the **User reported** tab of the **Submissions** page in the Defender portal at https://security.microsoft.com/reportsubmission?viewid=user.

    Submitting user reported messages to Microsoft is important to allow our filters to learn and improve.

For complete information about user reported message settings, see [User reported settings](submissions-user-reported-messages-custom-mailbox).

## Step 6: Block and allow entries

**Summary**: Familiarize yourself with the procedures to block and allow messages, files and URLs in Defender for Office 365.

**Details**:

You need to become familiar with how to block and (temporarily) allow message senders, files, and URLs at the following locations in the Defender portal:

- The [Tenant Allow/Block List](tenant-allow-block-list-about) at https://security.microsoft.com/tenantAllowBlockList.
- The **Submissions** page at https://security.microsoft.com/reportsubmission.
- The **Spoof intelligence insight** page at https://security.microsoft.com/spoofintelligence.

In general, it's easier to create blocks than allows, because unnecessary allow entries expose your organization to malicious email that the system would otherwise filter.

- **Block**:

    - You can create block entries for **domains and email addresses**, **files**, and **URLs** on the corresponding tabs in the Tenant Allow/Block List and by submitting the items to Microsoft for analysis from the **Submissions** page. When you submit an item to Microsoft, corresponding block entries are also created in the Tenant Allow/Block List.

        Tip

        Users in the organization also can't *send* email to domains or email addresses that are specified in block entries in the Tenant Allow/Block List.
    - Messages blocked by [spoof intelligence](anti-spoofing-spoof-intelligence) are shown on the **Spoof intelligence** page. If you change an allow entry to a block entry, the sender becomes a manual block entry on the **Spoofed senders** tab in the Tenant Allow/Block List. You can also proactively create block entries for not yet encountered spoofed senders on the **Spoofed senders** tab.
- **Allow**:

    - You can create allow entries for **domains and email addresses** and **URLs** on the corresponding tabs in the Tenant Allow/Block List to override the following verdicts:

        - Bulk
        - Spam
        - High confidence spam
        - Phishing (not high confidence phishing)
    - You can't create allow entries directly in the Tenant Allow/Block List for the following items:

        - Malware or high confidence phishing verdicts for **domains and email addresses** or **URLs**.
        - Any verdicts for **files**.

        Instead, you use the **Submissions** page to report the items to Microsoft. After you select **I've confirmed it's clean**, you can then select **Allow this message**, **Allow this URL**, or **Allow this file** to create a corresponding temporary allow entry in the Tenant Allow/Block list.
    - Messages allowed by [spoof intelligence](anti-spoofing-spoof-intelligence) are shown on the **Spoof intelligence** page. If you change a block entry to an allow entry, the sender becomes a manual allow entry on the **Spoofed senders** tab in the Tenant Allow/Block List. You can also proactively create allow entries for not yet encountered spoofed senders on the **Spoofed senders** tab.

For complete details, see the following articles:

- [Allow or block email using the Tenant Allow/Block List](tenant-allow-block-list-email-spoof-configure)
- [Allow or block files using the Tenant Allow/Block List](tenant-allow-block-list-files-configure)
- [Allow or block URLs using the Tenant Allow/Block List](tenant-allow-block-list-urls-configure)
- [Use the Submissions page to submit suspected spam, phish, URLs, legitimate email getting blocked, and email attachments to Microsoft](submissions-admin)
- [Override the spoof intelligence verdict](anti-spoofing-spoof-intelligence#override-the-spoof-intelligence-verdict)

## Step 7: Launch phishing simulations using Attack simulation training

In Defender for Office 365 Plan 2, Attack simulation training allows you to send simulated phishing messages to users and assign training based on how they respond. The following options are available:

- [Individual simulations](attack-simulation-training-simulations) using built-in or custom payloads.
- [Simulation automations](attack-simulation-training-simulation-automations) taken from real-world phishing attacks using multiple payloads and automated scheduling.
- [Training-only campaigns](attack-simulation-training-training-campaigns) where you don't need to launch a campaign and wait for users to click links or download attachments in the simulated phishing messages before trainings are assigned.

For more information, see [Get started using Attack simulation training](attack-simulation-training-get-started).

## Step 8: Investigate and respond

Now that your initial set up is complete, use the information in the [Microsoft Defender for Office 365 Security Operations Guide](mdo-sec-ops-guide) to monitor and investigate threats in the organization.