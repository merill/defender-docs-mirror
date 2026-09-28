---
layout: Conceptual
title: Control external email forwarding and fix 5.7.520 errors - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/outbound-spam-policies-external-email-forwarding
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
keywords: 5.7.520, Access Denied, external email forwarding, automatic forwarding, outbound spam policy, NDR
author: chrisda
ms.author: chrisda
ms.date: 2026-08-18T00:00:00.0000000Z
ms.topic: overview
ms.collection:
- m365-security
- tier2
ms.localizationpriority: medium
ms.assetid: 
ms.custom:
- seo-marvel-apr2020
- adminvideo
- msecd-doc-authoring-1015
description: Learn how to control automatic external email forwarding and resolve 5.7.520 Access Denied errors in Microsoft 365.
ms.service: defender-office-365
ai-usage: ai-assisted
locale: en-us
document_id: cd3ec995-778f-0763-f78e-72a16642ac2b
document_version_independent_id: cd3ec995-778f-0763-f78e-72a16642ac2b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/outbound-spam-policies-external-email-forwarding.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: outbound-spam-policies-external-email-forwarding
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/outbound-spam-policies-external-email-forwarding.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 8b464d03-72a7-4093-2a87-45dd5874a5a4
---

# Control external email forwarding and fix 5.7.520 errors - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

As an admin in a cloud email organization, you might have company requirements to restrict or control automatically forwarded messages to external recipients (recipients outside of your organization). Email forwarding can be useful, but can also pose a security risk due to the potential disclosure of information. Attackers might use this information to attack your organization or partners.

The following types of automatic forwarding are available in Microsoft 365:

- Users can configure [Inbox rules](https://support.microsoft.com/office/c24f5dea-9465-4df4-ad17-a50704d66c59) to automatically forward messages to external senders (deliberately or as a result of a compromised account).
- Admins can configure [mailbox forwarding](/en-us/exchange/recipients-in-exchange-online/manage-user-mailboxes/configure-email-forwarding) (also known as *SMTP forwarding*) to automatically forward messages to external recipients. The admin can choose whether to forward messages, or keep copies of forwarded messages in the mailbox.

Tip

Users with automatic forwarding from on-premises email systems through Microsoft 365 are subject to the same policy controls as cloud mailboxes.

You can use outbound spam filter policies to control automatic forwarding to external recipients. Three settings are available:

- **Automatic - System-controlled**: This value is the default. When this value was introduced, it was equivalent to **On - Forwarding is enabled**. In 2021, the value changed to **Off - Forwarding is disabled** for new organizations and for existing organizations that weren't actively using the **Automatic - System-controlled** value. For existing organizations that were already using the value, it can remain equivalent to **On - Forwarding is enabled**. Because the behavior can differ by organization, configure **On - Forwarding is enabled** or **Off - Forwarding is disabled** instead of **Automatic - System-controlled**. For more information, see [automatic email forwarding in Exchange Online](https://techcommunity.microsoft.com/blog/exchange/all-you-need-to-know-about-automatic-email-forwarding-in-exchange-online/2074888).
- **On - Forwarding is enabled**: Automatic external forwarding is allowed and not restricted.
- **Off - Forwarding is disabled**: Automatic external forwarding is disabled and results in a non-delivery report (also known as an NDR or bounce message) to the sender.

[![Screenshot of the Protection settings flyout in the properties of the default outbound spam filter policy with the Automatic forwarding rules options highlighted.](media/outbound-spam-protection-settings.png)](media/outbound-spam-protection-settings.png#lightbox)

For instructions on how to configure these settings, see [Configure outbound spam filtering](outbound-spam-policies-configure).

Note

- Disabling automatic forwarding disables any Inbox rules (users) or mailbox forwarding (admins) that redirect messages to external addresses.
- Automatic forwarding of messages between internal users isn't affected by the settings in outbound spam filter policies.

## How the outbound spam filter policy settings work with other automatic email forwarding controls

As an admin, you might use other controls to allow or block automatic email forwarding. For example:

- [Remote domains](/en-us/exchange/mail-flow-best-practices/remote-domains/remote-domains) to allow or block automatic email forwarding to some or all external domains.

    [![Screenshot of the Email reply types flyout in the properties of a remote domain in the Exchange admin center with the Allow automatic forwarding option highlighted.](media/outbound-spam-remote-domains-auto-forwarding.png)](media/outbound-spam-remote-domains-auto-forwarding.png#lightbox)
- Conditions and actions in Exchange [mail flow rules](/en-us/exchange/security-and-compliance/mail-flow-rules/mail-flow-rules) (also known as transport rules) to detect and block automatically forwarded messages to external recipients by Inbox rules.

    [![Screenshot of a mail flow rule to detect and block messages automatically forwarded to external recipients by Inbox rules.](media/outbound-spam-mail-flow-rule-detect-block-forwarded.png)](media/outbound-spam-mail-flow-rule-detect-block-forwarded.png#lightbox)

When one setting allows external forwarding, but another setting blocks external forwarding, the block typically wins. Examples are described in the following table:

| Scenario | Result |
| --- | --- |
| - You configure remote domain settings to allow automatic forwarding.<br>- Automatic forwarding in the outbound spam filter policy is set to \***Off - Forwarding is disabled**. | Automatically forwarded messages to recipients in the affected domains are blocked. |
| - You configure remote domain settings to allow automatic forwarding.<br>- Automatic forwarding in the outbound spam filter policy is set to **Automatic - System-controlled**. | The result depends on how **Automatic - System-controlled** works in your organization. To avoid this ambiguity, configure the outbound spam filter policy to **On - Forwarding is enabled** or \***Off - Forwarding is disabled**. |
| - Automatic forwarding in the outbound spam filter policy is set to **On - Forwarding is enabled**<br>- You use mail flow rules or remote domains to block automatically forwarded email. | Automatically forwarded messages to affected recipients are blocked by mail flow rules or remote domains. |

You can use this behavior (for example) to allow automatic forwarding in outbound spam filter policies, but use remote domains to control the external domains that users can forward messages to.

## How to find users that are automatically forwarding

You can see information about users that are automatically forwarding messages to external recipients in the [Auto forwarded messages report](/en-us/exchange/monitoring/mail-flow-reports/mfr-auto-forwarded-messages-report) for cloud-based accounts.

For on-premises users that automatically forward from their on-premises email system through Microsoft 365, you need to create a mail flow rule to track these users. For general instructions on how to create a mail flow rule, see [Use the EAC to create a mail flow rule](/en-us/exchange/security-and-compliance/mail-flow-rules/manage-mail-flow-rules#use-the-eac-to-create-a-mail-flow-rule).

Use the following information to create the mail flow rule in the Exchange admin center (EAC):

- **Set rule conditions** page:

    - **Apply this rule if** (condition): **The message headers** &gt; **matches these text patterns**.

        - Select **Enter text** to specify the following header: `X-MS-Exchange-Inbox-Rules-Loop`
        - Select **Enter words** to specify the following header value: `.` (match any value for the header)

        The condition looks like this: **'X-MS-Exchange-Inbox-Rules-Loop'** message header matches **'.'**
    - **Do the following** (action): Configure an appropriate action. For example, you can use the action **Modify the message properties** &gt; **set a message header**, with the header name **X-Forwarded** and the value **True**.

    [![The rule conditions and action in the EAC for a mail flow rule to identify forwarded messages.](media/mail-flow-rule-for-forwarded-messages-conditions.png)](media/mail-flow-rule-for-forwarded-messages-conditions.png#lightbox)
- **Set rule settings** page:

    - Set the **Severity** value to **Low**, **Medium**, or **High**. This setting allows you to use the [Exchange transport rule report](reports-email-security#exchange-transport-rule-report) to get details of users that are forwarding.

    [![Setting the mail flow rule severity to Medium in the EAC for the mail flow rule to identify forwarded messages.](media/mail-flow-rule-for-forwarded-messages-settings.png)](media/mail-flow-rule-for-forwarded-messages-settings.png#lightbox)

## Blocked email forwarding messages

When a message is detected as automatically forwarded, and the [outbound spam filter](outbound-spam-policies-configure) policy *blocks* that activity, the message is returned to the sender in an NDR that contains the following information:

`5.7.520 Access denied, Your organization does not allow external forwarding. Please contact your administrator for further assistance. AS(7555)`