---
layout: Conceptual
title: Troubleshoot outbound sending limits in Exchange Online - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/outbound-spam-sending-limits-troubleshoot
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn about outbound sending limits in Exchange Online, how to monitor usage, and resolve blocked sending for users and organizations.
author: chrisda
ms.author: chrisda
ms.date: 2026-05-26T00:00:00.0000000Z
ms.topic: troubleshooting
ms.service: defender-office-365
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ai-usage: ai-assisted
locale: en-us
document_id: 1c64d393-d986-f9e0-e6e4-32e3aa0483b2
document_version_independent_id: 1c64d393-d986-f9e0-e6e4-32e3aa0483b2
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/outbound-spam-sending-limits-troubleshoot.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: outbound-spam-sending-limits-troubleshoot
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/outbound-spam-sending-limits-troubleshoot.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/cf9b82c5-b6dc-45f3-b005-b1bc5fc03bea
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0c85d34e-bfd2-4466-957c-f0b61e9692df
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
platformId: 87f62497-d770-8997-5867-8283a895b1c8
---

# Troubleshoot outbound sending limits in Exchange Online - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

Exchange Online enforces outbound sending limits to protect the service from spam, bulk-mailing abuse, and compromised accounts. When a user or organization exceeds these limits, email sending is restricted.

## Sending limits in Exchange Online

Exchange Online applies outbound sending limits to all cloud mailboxes. These limits apply at the user and organization levels.

For the complete list of service limits, see [Exchange Online sending limits](/en-us/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits#sending-limits-1).

### Per-user sending limits

The recipient rate limit and message rate limit are hard limits enforced at the service level and can't be increased.

| Limit | Value | Notes |
| --- | --- | --- |
| **Recipient rate limit** | 10,000 recipients per day | 24-hour sliding window. The mailbox can't send until the number of recipients sent to in the past 24 hours drops below the limit. |
| **Message rate limit** | 30 messages per minute | Excess submissions are throttled and carried over to following minutes. |
| **Recipient limit per message** | 500 recipients (default) | Customizable from 1 to 1000 in the Exchange admin center (EAC) or PowerShell. For more information, see [Customizable recipient limits in Office 365](https://techcommunity.microsoft.com/t5/exchange-team-blog/customizable-recipient-limits-in-office-365/ba-p/1183228). |

Note

For the recipient rate limit, distribution groups in the organization's address book count as **one recipient**. Distribution groups in a mailbox's Contacts folder are counted **individually** by member.

### Tenant External Recipient Rate Limit

The Tenant External Recipient Rate Limit (TERRL) is the maximum number of external recipients an organization can send to per day. TERRL scales automatically with the number of licenses in the organization. Trial organizations have a default limit of 5,000 external recipients per day.

When the TERRL is exceeded, senders receive a non-delivery report (also known as an NDR or bounce message) with the following error:

> 
> `550 5.7.233 Your message can't be sent because your tenant exceeded its daily limit for sending email to external recipients (tenant external recipient rate limit).`

Note

TERRL counts distribution group members individually. For example, a message sent to a distribution group with 1,000 external recipients counts as 1,000 external recipients.

### Outbound spam policy limits

Admins can configure more limits in outbound spam policies. For instructions, see [Configure outbound spam policies](outbound-spam-policies-configure).

| Setting | Description | Valid range |
| --- | --- | --- |
| **External message limit** | Maximum number of external recipients per hour | 0–10,000 (0 = service default) |
| **Internal message limit** | Maximum number of internal recipients per hour | 0–10,000 (0 = service default) |
| **Daily message limit** | Maximum total number of recipients per day | 0–10,000 (0 = service default) |

### Connector and relay sending limits

The following limits apply to outbound mail sent through connectors, SMTP relay, or Direct Send scenarios:

| Sending method | Limit | Details |
| --- | --- | --- |
| **Client SMTP submission (SMTP AUTH)** | 10,000 recipients/day, 30 messages/minute | Uses authenticated user credentials. Subject to per-user limits. |
| **SMTP relay (connector-based)** | 10,000 recipients/day per mailbox used for relay | Requires a configured outbound connector. Subject to per-user limits for the mailbox. |
| **Direct Send** | Subject to receiving limits (3,600 messages/hour per recipient) | Sends to internal recipients only. Unauthenticated; not subject to per-user sending limits. |

Tip

For applications or devices that need to send large volumes of outbound email, use **SMTP relay** through a connector or a **non-Microsoft bulk email service** rather than Client SMTP submission. For configuration instructions, see [Set up a multifunction device or application to send email using Microsoft 365](/en-us/exchange/mail-flow-best-practices/how-to-set-up-a-multifunction-device-or-application-to-send-email-using-microsoft-365-or-office-365).

## Monitor sending usage

Use the following tools to monitor outbound email activity and detect potential issues:

- **Message trace**: Track individual outbound messages and identify delivery failures. For more information, see [Message trace in the Microsoft Defender portal](message-trace-defender-portal).
- **Mail flow reports**: Use the following reports in the Exchange admin center to monitor outbound sending. On the **Mail flow** reports page in the Exchange admin center at https://admin.exchange.microsoft.com/#/reports/mailflowreportsmain, select the report to view. For a complete list of available reports, see [Mail flow reports](/en-us/exchange/monitoring/mail-flow-reports/mail-flow-reports).
    - **Tenant Outbound External Recipients** report: Shows TERRL usage for your organization.
    - [Mailboxes exceeding receiving limits report](/en-us/exchange/monitoring/mail-flow-reports/mailboxes-exceeding-receiving-limits-report): Identifies mailboxes receiving unusually high volumes.
- **Built-in alert policies**: The following [alert policies](/en-us/defender-xdr/alert-policies#threat-management-alert-policies) are enabled by default and send notifications to the **TenantAdmins** (Global Administrator) group. On the **Alert policy** page in the Microsoft Defender portal at https://security.microsoft.com/alertpoliciesv2, search for the policy to review or modify its settings:
    - [Email sending limit exceeded](/en-us/defender-xdr/alert-policies#threat-management-alert-policies): A user exceeds the outbound sending limits.
    - [Suspicious email sending patterns detected](/en-us/defender-xdr/alert-policies#threat-management-alert-policies): Unusual outbound email activity is detected from a user.
    - [User restricted from sending email](/en-us/defender-xdr/alert-policies#threat-management-alert-policies): A user is blocked from sending due to outbound spam.

Tip

For programmatic monitoring, use the [Get-MailDetailTransportRuleReport](/en-us/powershell/module/exchangepowershell/get-maildetailtransportrulereport) and [Get-MailTrafficSummaryReport](/en-us/powershell/module/exchangepowershell/get-mailtrafficsummaryreport) cmdlets in [Exchange Online PowerShell](/en-us/powershell/exchange/connect-to-exchange-online-powershell).

## Best practices for bulk senders

Exchange Online isn't designed for bulk mailing scenarios. If your sending volumes exceed these limits, use a dedicated bulk email service provider. For detailed recommendations, see [Outbound spam protection](outbound-spam-protection-about#recommendations-for-customers-who-want-to-send-mass-mailings-through-microsoft-365).

### Alternatives for bulk email

If your organization needs to send bulk or marketing email, use a service designed for high-volume sending.

- **[Azure Communication Services Email](/en-us/azure/communication-services/concepts/email/email-overview)**: A Microsoft service purpose-built for high-volume email sending.
- **Non-Microsoft bulk email providers**: Purpose-built services for bulk sending.
- **On-premises email servers**: Maintain your own email infrastructure for mass mailings.

### Alternative sending methods for application mail

The following options are for application-generated or device-generated messages, not bulk marketing email. These methods are still subject to Exchange Online sending limits.

- **SMTP relay via Microsoft 365**: For application-generated messages that need to route through your organization. For more information, see [Set up a multifunction device or application to send email using Microsoft 365](/en-us/exchange/mail-flow-best-practices/how-to-set-up-a-multifunction-device-or-application-to-send-email-using-microsoft-365-or-office-365#smtp-relay-configure-a-connector-to-relay-email-from-your-device-or-application-through-microsoft-365-or-office-365).
- **Direct Send**: For devices/applications that send to your own organization only. For more information, see [Direct Send](/en-us/exchange/mail-flow-best-practices/how-to-set-up-a-multifunction-device-or-application-to-send-email-using-microsoft-365-or-office-365#direct-send-send-mail-directly-from-your-device-or-application-to-microsoft-365-or-office-365).

### If you must send bulk email through Microsoft 365

Follow these guidelines to reduce the risk of being blocked or routed to the [high-risk delivery pool](outbound-spam-high-risk-delivery-pool-about):

- **Configure email authentication**: Set up [SPF](email-authentication-spf-configure), [DKIM](email-authentication-dkim-configure), and [DMARC](email-authentication-dmarc-configure) for your sending domain.
- **Maintain list hygiene**: Remove invalid and bouncing email addresses. Honor unsubscribe requests immediately. Use confirmed opt-in (double opt-in) for new subscribers.
- **Follow content best practices**: Use a consistent and recognizable **From** address. Write clear, accurate **Subject** lines. Include a visible and functional **unsubscribe** link.
- **Manage sending rate**: Spread bulk sends over time rather than sending all at once. Monitor bounce rates and don't exceed 30 messages per minute per mailbox.
- **Protect domain reputation**: Use a custom subdomain for bulk email (for example, `m.contoso.com` for marketing). Use message trace to check whether your messages are being routed to the high-risk delivery pool.

## What happens when limits are exceeded

The following table summarizes the behavior when each type of sending limit is exceeded:

| Limit exceeded | Behavior | User experience | Admin notification |
| --- | --- | --- | --- |
| **Per-user recipient rate limit** | Mailbox can't send until the 24-hour sliding window drops below the limit. | Messages are rejected. The user can send again after the recipient count from the past 24 hours drops below 10,000. In some cases, the user might also appear on the [Restricted entities](outbound-spam-restore-restricted-users) page. | Alert: **Email sending limit exceeded** |
| **Per-user message rate limit** | Messages are throttled (queued and delivered over subsequent minutes). | Slight sending delay; no NDR. | No alert unless sustained. |
| **TERRL** | All tenant users sending to external recipients are blocked. | NDR `550 5.7.233` returned to senders. | Alert: **Email sending limit exceeded** |
| **Outbound spam policy limit** | Action depends on policy configuration (**Restrict**, **Restrict until next day**, or **Alert only**). | NDR or delivery delay depending on the configured action. | Configured notification recipients are notified. |
| **Outbound spam detected** | Messages routed to the [high-risk delivery pool](outbound-spam-high-risk-delivery-pool-about). If volume continues, user is restricted. | Reduced deliverability; eventual block. | Alert: **Suspicious email sending patterns detected** |

Tip

Set up custom alert policies to receive notifications before your organization reaches sending limits. For example, create an alert at 80% of your TERRL to allow time to redistribute sending or shift to a non-Microsoft provider.

## Resolve blocked sending

When a user exceeds outbound sending limits or is detected sending spam, Exchange Online restricts the user from sending email. The user appears on the **Restricted entities** page in the Microsoft Defender portal at https://security.microsoft.com/restrictedusers.

A blocked user shows the following symptoms:

- The user receives an NDR with error code [5.1.8](https://support.microsoft.com/servicing/Exchange/non-delivery-report/ndr-error-code-550-5-1-8-access-denied-bad-outbound-sender) (bad outbound sender, typically due to suspected spam) when trying to send email.
- The user appears on the **Restricted entities** page.
- Admins receive the **User restricted from sending email**[alert notification](outbound-spam-restore-restricted-users#verify-the-alert-settings-for-restricted-users).

Before unblocking the user, determine why the restriction was applied:

- **Compromised account**: The account might be compromised and used to send spam. Check sign-in logs for suspicious activity, look for unknown inbox rules or forwarding rules, and review recent sent items.
- **Legitimate bulk send**: The user intentionally sent a large volume of email that exceeded limits. Consider the alternative sending methods described in Best practices for bulk senders.

For detailed steps to investigate, remediate compromised accounts, and remove users from the **Restricted entities** page, see [Remove blocked users from the Restricted entities page](outbound-spam-restore-restricted-users).

To prevent future blocks, take the following actions:

- [Configure outbound spam policies](outbound-spam-policies-configure) with appropriate per-hour and daily limits and notifications.
- Ensure **Email sending limit exceeded**[alert policies](alert-policies-defender-portal) are active.
- Inform users about sending limits and bulk email alternatives.
- [Enable MFA](/en-us/entra/identity/authentication/concept-mfa-howitworks) to protect accounts from compromise.
- Review [mail flow reports](/en-us/exchange/monitoring/mail-flow-reports/mail-flow-reports) and [message traces](message-trace-defender-portal) periodically.