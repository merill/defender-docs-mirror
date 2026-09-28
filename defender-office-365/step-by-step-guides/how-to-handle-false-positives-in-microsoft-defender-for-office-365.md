---
layout: Conceptual
title: Resolve email false positives in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/step-by-step-guides/how-to-handle-false-positives-in-microsoft-defender-for-office-365
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to resolve false positives in Microsoft Defender for Office 365 when legitimate emails are blocked, quarantined, or delivered to Junk Email.
ms.service: defender-office-365
ai-usage: ai-assisted
author: chrisda
ms.author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-guidance-templates
- m365-security
- tier3
ms.topic: how-to
ms.custom: msecd-doc-authoring-1016
ms.date: 2026-08-03T00:00:00.0000000Z
locale: en-us
document_id: 7bf413e0-c19f-a093-d9a9-15352e972f01
document_version_independent_id: 7bf413e0-c19f-a093-d9a9-15352e972f01
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/step-by-step-guides/how-to-handle-false-positives-in-microsoft-defender-for-office-365.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: step-by-step-guides/how-to-handle-false-positives-in-microsoft-defender-for-office-365
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/step-by-step-guides/how-to-handle-false-positives-in-microsoft-defender-for-office-365.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
- https://authoring-docs-microsoft.poolparty.biz/devrel/3e34b70d-bca0-4369-a01b-71d1edfd427b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ca32b3f-fa14-46df-b09a-9c4a591d6396
platformId: fbaffb89-5485-d562-f91b-9328f1d687e9
---

# Resolve email false positives in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn

Microsoft Defender for Office 365 helps you identify and fix false positives — legitimate business emails that are mistakenly blocked as threats. Use this guide to understand *why* legitimate emails were blocked, resolve the issue, and prevent similar situations in the future.

## Prerequisites

Before you begin, make sure you meet the following requirements:

- Microsoft Defender for Office 365 Plan 1 or Plan 2 (included in Microsoft 365 A5/E5/G5).
- Sufficient permissions (for example, membership in the **Security Administrator** role in [Microsoft Entra ID](/en-us/entra/identity/role-based-access-control/manage-roles-portal)).
- 5-10 minutes to complete the steps.

## Identify your false positive type

Before you begin troubleshooting, identify whether the false positive is spam-related or phishing/malware-related. The resolution steps differ based on the type of detection.

**Use the spam false positive steps in this article if**:

- Legitimate bulk email (newsletters, marketing) is marked as spam.
- Messages are delivered to the **Junk Email** folder instead of the Inbox.
- Messages are quarantined as spam (not phishing or malware).
- Message headers show a high Bulk Complaint Level (BCL 7-9).
- Message headers show `SFV:SPM` (spam filter verdict).

**Use the phishing/malware false positive steps in this article if**:

- Messages are blocked by Safe Links or Safe Attachments.
- Impersonation protection triggers incorrectly.
- Messages are detected as phishing or malware.

## Handle spam false positives

Use the following steps when legitimate email is incorrectly classified as spam.

### Step 1: Check message headers for spam indicators

Message headers reveal why a message was classified as spam. You can extract headers from the [email entity page](../mdo-email-entity-page) in the Defender portal or from message properties in [Outlook message headers](https://support.microsoft.com/office/cd039382-dc6e-4264-ac74-c048563d212c). Use the [Message Header Analyzer](https://mha.azurewebsites.net/) to parse raw headers into a readable format. For a complete list of header fields and values, see [Anti-spam message headers](../message-headers-eop-mdo).

Look for these key values in the **X-Forefront-Antispam-Report** header:

| Value | Description | Implication |
| --- | --- | --- |
| `SFV:SPM` | Spam filtering verdict | Spam filtering processed the message. Use the `CAT` value to determine whether the message was identified as spam, phishing, or malware. |
| `CAT:SPM` | Category: spam | Delivered to Junk Email folder by default |
| `CAT:HSPM` | Category: high confidence spam | Quarantined by default |
| `BCL:7` to `BCL:9` | High bulk complaint level | Likely blocked by bulk mail threshold |
| `SFV:BLK` | Blocked sender | Sender is on the user's Blocked Senders list in Outlook |

### Step 2: Identify the source of the classification

Based on the header values, determine what caused the false positive:

- **Tenant Allow/Block List block entry**: Check the [email entity page](../mdo-email-entity-page) overrides information, or check the Tenant Allow/Block List directly for block entries that match the sender.
- **User's Blocked Senders list**: Look for `SFV:BLK` in the message headers.
- **Exchange mail flow rule (transport rule)**: Look for the `X-MS-Exchange-Organization-RuleID` header.
- **Anti-spam policy settings**: A **Spam** or **High confidence spam** verdict (`SFV:SPM` with `CAT:SPM` or `CAT:HSPM`), or the BCL threshold is exceeded.
- **Connection filter (IP block list)**: Check the [connection filter policy settings](../connection-filter-policies-configure) for the sending IP address in the IP Block List.

### Step 3: Apply the appropriate fix

Based on the false-positive source identified in the message headers or policy checks, apply the corresponding resolution:

| Source identified | Recommended fix |
| --- | --- |
| Tenant Allow/Block List block entry | Remove the block entry or [create an allow entry for the sender](../tenant-allow-block-list-email-spoof-configure#create-allow-entries-for-domains-and-email-addresses). |
| User's Blocked Senders list | Remove the sender from the user's [Blocked Senders list in Outlook](../configure-junk-email-settings-on-exo-mailboxes) or use an admin allow override. |
| IP block list | Add the sending IP to the [connection filter IP Allow List](../connection-filter-policies-configure). |
| Anti-spam policy (spam verdict) | [Tune the anti-spam policy](../anti-spam-policies-configure). For example, increase the BCL threshold or adjust the spam action. |
| Mail flow rule | Modify the [mail flow rule conditions in Exchange](/en-us/exchange/security-and-compliance/mail-flow-rules/mail-flow-rules) or add exceptions for the affected sender. |
| Spam filtering error (no organization configuration issue) | [Submit the message to Microsoft for analysis](../submissions-admin#report-good-email-to-microsoft) as a false positive. |

### Step 4: Validate the fix

After you apply the selected remediation, confirm that the false-positive spam classification is resolved:

1. Ask the sender to send a test message with the same content type and sender domain.
2. Use [message trace](../message-trace-defender-portal) to verify the message was delivered to the Inbox.
3. Check the message headers to confirm the spam verdict is no longer applied (for example, `SFV:NSPM` or `CAT:NONE`).

Tip

Allow 15-30 minutes for policy changes to take effect. Mail flow rule changes might take up to one hour due to caching.

### Common spam false positive scenarios

The following table describes common scenarios and recommended approaches:

| Scenario | Key indicators | Recommended approach |
| --- | --- | --- |
| Legitimate bulk newsletter or marketing email consistently quarantined | High BCL (7-9), `CAT:BULK` | Increase the [Bulk Complaint Level (BCL) threshold](../anti-spam-policies-configure) (the default value is 7). |
| Legitimate newsletter or marketing email identified as spam or high confidence spam | `CAT:SPM` or `CAT:HSPM` | [Submit the messages to Microsoft for analysis](../submissions-admin#report-good-email-to-microsoft) and create an allow entry for the sender during the submission. |
| All email from a specific partner domain is blocked | Sender found in the Tenant Allow/Block List (check the [email entity page](../mdo-email-entity-page) or the Tenant Allow/Block List directly) | Remove the block entry or [create an allow entry for the domain](../tenant-allow-block-list-email-spoof-configure#create-allow-entries-for-domains-and-email-addresses). |
| Marketing automation platform email blocked (Marketo, HubSpot, Mailchimp, etc.) | High BCL, possible email authentication failures | Verify the sender's SPF/DKIM/DMARC configuration. If authentication passes but filtering still triggers, increase the BCL threshold or add the sending domain to the allow list. |
| Forwarded emails quarantined as spoofing | DMARC failure, spoof detection triggered | Configure [ARC trusted sealers](../email-authentication-arc-configure) for the forwarding service, or add a [spoof intelligence override](../anti-spoofing-spoof-intelligence) for the sender/infrastructure pair. |

### Troubleshoot fixes that aren't working

If the selected remediation doesn't resolve the false-positive spam classification, check for the following common causes:

- **Propagation delay**: Allow 15-30 minutes for anti-spam policy changes and up to one hour for mail flow rule changes.
- **Policy precedence conflict**: A higher-priority policy (preset security policy) might override your custom policy settings. For details, see [Troubleshoot anti-spam policy issues](../anti-spam-policies-troubleshooting).
- **Multiple detection reasons**: The message triggered more than one detection (for example, spam *and* spoof detection). Resolving one cause might not be enough.
- **Allow entry expired or incorrect**: Verify the [Tenant Allow/Block List entry](../tenant-allow-block-list-email-spoof-configure) is active, not expired, and uses the correct format (email address vs. domain).
- **Mail flow rule action**: Mail flow rules can request that messages [bypass spam filtering](/en-us/exchange/security-and-compliance/mail-flow-rules/use-rules-to-set-scl). Spam filtering considers the request with other signals when it determines how to handle the message. Mail flow rules can also delete messages.

## Handle phishing and malware false positives

Use the phishing, malware, and non-spam false-positive remediation steps in this section when legitimate email is incorrectly detected as phishing, malware, or another non-spam threat.

### Legitimate emails delivered to the Junk Email folder

Follow the end-user and admin remediation steps in this subsection when messages are delivered but land in the wrong folder.

#### End user actions

End users can try the following actions to correct messages that were delivered to Junk Email:

1. Report the email as **Not junk** by using the [built-in **Report** button in supported versions of Outlook](../submissions-outlook-report-messages#use-the-built-in-report-button-in-outlook).
2. Optionally, add the sender to the [Safe Senders list](https://support.microsoft.com/office/add-recipients-to-the-safe-senders-list-in-outlook-be1baea0-beab-4a30-b968-9004332336ce) in Outlook to prevent future messages from that sender from going to Junk Email.

#### Actions admins can take for legitimate emails in Junk Email

Admins can use the following process to investigate and remediate these reports:

1. Triage user-reported messages from [the User reported tab on the Submissions page](../submissions-admin#view-user-reported-messages-to-microsoft).

    Tip

    In organizations with Defender for Office 365 Plan 2 and Security Copilot, the [Phishing Triage Agent](/en-us/defender-xdr/phishing-triage-agent) can autonomously triage and classify user-reported phishing emails, reducing manual investigation work for security teams.
2. [Submit the messages to Microsoft for analysis](../submissions-admin#notify-users-about-admin-submitted-messages-to-microsoft) to understand why the email was blocked.
3. If needed, while submitting to Microsoft for analysis, [create an allow entry for the sender](../tenant-allow-block-list-email-spoof-configure#create-allow-entries-for-domains-and-email-addresses) to mitigate the false positive.
4. After the submission results are available, read the verdict on the **Submissions** page to understand why the emails were blocked.
5. Use the results to improve your organization's configuration and *prevent* similar false positives in the future.

### Legitimate emails in quarantine (end user view)

End users can take the following actions on quarantined messages:

1. Review [quarantine notifications](../quarantine-quarantine-notifications) about quarantined messages. The notifications are based on the settings that security admins configure.
2. Preview, release, or report quarantined messages by using the steps in [Find and release quarantined messages as a user](../quarantine-end-user).

### Legitimate emails in quarantine (admin view)

Admins can release quarantined messages and submit them to Microsoft for analysis:

1. View quarantined emails (including messages where users requested release) from the [admin quarantine review page for messages and files](../quarantine-admin-manage-messages-files).
2. [Release messages from quarantine while submitting them to Microsoft for analysis](../quarantine-admin-manage-messages-files#release-quarantined-email). You can also create a temporary allow entry in the Tenant Allow/Block List during the submission to mitigate the issue.
3. After submission results are available, [read the Microsoft submission verdict results](../submissions-admin#results-from-microsoft)to understand why the message was detected as phishing, malware, or spoofing.
    - If false positives are due to your organization's mail-flow, anti-spam, or spoof-protection configuration, correct those settings to mitigate the false positive.
    - If false positives are due to other factors, Microsoft learns from the submission and similar messages aren't quarantined anymore.

Note

Admins need to manually release any similar quarantined messages. Quarantined messages aren't released automatically. To find and release quarantined messages in bulk, see [Can I release or report more than one quarantined message at a time?](../quarantine-faq#can-i-release-or-report-more-than-one-quarantined-message-at-a-time-).

### Forwarded or spoofed emails incorrectly blocked

Externally forwarded emails or legitimate cross-domain senders can trigger spoof detection because the sending infrastructure doesn't match the From address domain. If you see forwarded or non-Microsoft emails blocked as spoofing:

- Review the [spoof intelligence insight and configure overrides](../anti-spoofing-spoof-intelligence) for legitimate sender/infrastructure pairs.
- If your organization receives mail through an intermediary (mailing list, forwarding service, or email gateway), configure Authenticated Received Chain (ARC) [trusted sealers](../email-authentication-arc-configure) so messages preserve authentication through the relay.
- Ask the external sender to fix their SPF, DKIM, and DMARC records to align with their sending infrastructure.