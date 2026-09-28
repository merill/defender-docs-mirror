---
layout: Conceptual
title: Outbound spam limits with Send As and Send on behalf permissions - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/outbound-spam-policies-send-as-send-on-behalf
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how outbound spam policy limits apply when users send email with Send As or Send on behalf permissions in Exchange Online.
author: chrisda
ms.author: chrisda
ms.topic: overview
ms.service: defender-office-365
ms.date: 2026-07-27T00:00:00.0000000Z
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.custom: msecd-doc-authoring-1015
ai-usage: ai-assisted
locale: en-us
document_id: ce33e3e8-2ea0-0d95-b721-35ea9f02faac
document_version_independent_id: ce33e3e8-2ea0-0d95-b721-35ea9f02faac
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/outbound-spam-policies-send-as-send-on-behalf.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: outbound-spam-policies-send-as-send-on-behalf
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/outbound-spam-policies-send-as-send-on-behalf.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: ba0cedda-4087-1e4b-4915-f965ea3a5467
---

# Outbound spam limits with Send As and Send on behalf permissions - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

In organizations with Microsoft 365 cloud mailboxes, [outbound spam policies](outbound-spam-protection-about) can limit:

- Internal recipients per hour
- External recipients per hour
- Total recipients per day

For more information about these limits, see [Sending limits](/en-us/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits#sending-limits).

When users send email with delegated permissions, Microsoft 365 evaluates two different identities to enforce these limits:

- The address in the **From** field (also known as the `5322.From` address or P2 sender) determines which outbound spam policy applies to the message.
- The authenticated user who submits the message accumulates the recipient counts that enforcement uses.

This behavior applies to messages sent with either **Send As** or **Send on behalf** permissions. If the mailbox in the **From** field is governed by a different outbound spam policy than the authenticated sender, enforcement can seem inconsistent with the policy assigned to the sender's own mailbox.

Important

Adding a user to a custom outbound spam policy doesn't guarantee that the policy governs every message the user submits. In delegated sending scenarios, you also need to evaluate every mailbox or group address that the user can put in the **From** field.

## Sender identities used for policy enforcement

For each outbound message, Microsoft 365 evaluates policy selection and recipient counting independently.

| Evaluation | Identity used | Result |
| --- | --- | --- |
| Select the outbound spam policy | Address in the message's **From** field | Determines the internal recipient limit, external recipient limit, daily recipient limit, and the action that's taken when a limit is exceeded. |
| Accumulate the recipient count | Authenticated user who submits the message | Recipients from all messages the user submits are added to the user's cumulative count, even when the messages are sent from other addresses. |

When a user sends email from their own mailbox, the From address and the authenticated sender are the same identity. The difference becomes visible only when the user sends as, or on behalf of, another mailbox or group.

Although these settings are often described as sending limits, enforcement is based on recipient counts. A single message addressed to multiple recipients increases the count by the number of recipients on that message.

### Example: A lower limit applies after the From address changes

Consider the following configuration. Both policies are custom outbound spam policies with customized limits. The built-in default outbound spam policy allows 500 external recipients per hour.

| Identity | Applicable policy | External recipient limit per hour | Restriction action |
| --- | --- | --- | --- |
| `sender@contoso.com` | High-volume senders | 500 | Restrict the user from sending mail until the following day |
| `shared@contoso.com` | Standard senders | 100 | Restrict the user from sending mail until the following day |

The user `sender@contoso.com` has **Send As** permission to use `shared@contoso.com`. The following sequence shows how enforcement works:

- Between 12:00 and 12:30, the user sends messages to 300 external recipients while using `sender@contoso.com` as the From address.
- Because the From address is `sender@contoso.com`, the **High-volume senders** outbound spam policy is selected. The accumulated external recipient count for the authenticated user reaches 300, which is below the limit of 500 recipients per hour.
- At 12:31, the same authenticated user sends another message, but this time uses `shared@contoso.com` as the From address and sends to one external recipient.
- The applicable outbound spam policy changes because the From address changed. The **Standard senders** policy now applies.
- The extra recipient is added to the same authenticated user's cumulative recipient count. The count is now 301 recipients.
- The current message is evaluated against the limit for `shared@contoso.com`, which is 100 external recipients per hour. Because the accumulated count exceeds that limit, the configured restriction action is triggered.

Key takeaways:

- A delegated mailbox doesn't inherit the higher limit that's assigned to the authenticated sender.
- Switching to a different From address doesn't reset the authenticated user's accumulated recipient count.

## How policy changes affect a user's accumulated count

Recipient accumulation can span messages that are evaluated under different outbound spam policies. For each message, the policy selected from the current From address determines both the applicable limit and the enforcement action.

As a result:

- A message sent from an address with a lower limit can trigger enforcement because of recipients that accumulated while sending from a different address.
- A message sent from an address with a higher limit is evaluated against that higher limit, but its recipients still contribute to the submitting user's cumulative count.
- Different restriction actions can apply as users switch among From addresses governed by different policies.
- Multiple users who send from the same shared mailbox don't share a single cumulative sending count. Each authenticated sender keeps an independent count.
- When a limit is exceeded, enforcement applies to the authenticated user who submitted the message, even if the triggering message used a different From address.

## Plan outbound spam policies for delegated sending

When users send email through shared mailboxes, Microsoft 365 Groups, or other delegated identities, consider the following practices:

- Maintain an inventory of the delegated From addresses that users can access through **Send As** or **Send on behalf** permissions. For steps, see [Inventory delegated From addresses for outbound spam policies](outbound-spam-delegated-from-addresses-inventory).
- If a user requires a custom sending limit, make sure the delegated From addresses they regularly use are covered by policies that provide compatible limits and restriction actions.
- Verify outbound spam policy priority whenever an address matches multiple custom policies. The highest priority applicable policy is used.
- Reevaluate policy coverage when delegated permissions are added or changed.
- Avoid broad exceptions that grant elevated limits unnecessarily.
- Use a dedicated bulk-mail solution when large-scale mailing is required, because Microsoft 365 isn't intended to function as a bulk email platform.

When a Microsoft 365 Group is included in an outbound spam policy, the behavior differs depending on where you add the group:

- Adding the group under **Groups** applies the policy to messages sent by the group's members.
- Adding the group under **Users** applies the policy to messages sent using the group's address.

For configuration steps, see [Configure outbound spam policies](outbound-spam-policies-configure).

## Troubleshoot an unexpected restriction

If a user is blocked or restricted sooner than expected, investigate both the authenticated sender and the mailbox used in the **From** field. Recommended checks include:

- Identify the user account that was restricted.
- Review the messages that the user submitted before the restriction occurred, including messages that were sent through delegated permissions.
- Determine which From address was used on the message that triggered enforcement.
- Identify the outbound spam policy that applied to that From address at processing time.
- Review the policy settings for external recipients per hour, internal recipients per hour, and total recipients per day.
- Verify the configured restriction action in the applicable policy.
- Analyze sending activity for all From addresses that the sender used, instead of focusing only on the sender's primary mailbox.
- Consider whether delegated access was granted directly or through group and nested group membership.

Exceeding a sending limit can indicate that an account is compromised. Investigate the account before you remove the restriction.

For more guidance, see [Troubleshoot outbound sending limits in Exchange Online](outbound-spam-sending-limits-troubleshoot).

## Frequently asked questions

### Does sending from another mailbox reset the recipient count?

No. Recipient accumulation continues against the authenticated user who submits the messages, no matter which mailbox address is used in the **From** field.

### Does the outbound spam policy assigned to the authenticated user always apply?

No. Outbound spam policy selection is based on the address that appears in the **From** field for the specific message being evaluated.

### Which account is restricted when a limit is exceeded?

The authenticated user who submitted the message is the account that's restricted, even when delegated permissions were used and the message was sent from another address.

### Is adding a high-volume sender to a custom policy enough?

Not always. If the user sends from other mailboxes or group addresses, evaluate each delegated From address and, when appropriate, include it in a policy that provides compatible limits and enforcement actions.

### Do Send As and Send on behalf permissions behave differently for these limits?

No. In both cases, the From address determines which outbound spam policy applies, and the authenticated sender accumulates the recipient count.

### Do multiple delegates share a recipient count when they send from the same shared mailbox?

No. Each authenticated user keeps a separate cumulative recipient count. The shared mailbox address affects policy selection, but it doesn't maintain a single count that all delegates share.