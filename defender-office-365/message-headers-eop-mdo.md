---
layout: Conceptual
title: Anti-spam message headers - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/message-headers-eop-mdo
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: article
ms.localizationpriority: high
ms.assetid: 2e3fcfc5-5604-4b88-ac0a-c5c45c03f1db
ms.collection:
- m365-security
- tier2
description: Admins can learn about the header fields added to incoming messages by the built-in security features for all cloud mailboxes and by Microsoft Defender for Office 365. These header fields provide information about the message and how it was processed.
ms.custom: seo-marvel-apr2020, msecd-doc-authoring-1015
ms.service: defender-office-365
ms.date: 2026-07-27T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 86c86b88-44f6-992e-5998-3975970d4ae1
document_version_independent_id: 86c86b88-44f6-992e-5998-3975970d4ae1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/message-headers-eop-mdo.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: message-headers-eop-mdo
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/message-headers-eop-mdo.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/1ae5c491-970a-4062-8301-6336e69f9026
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/f2c3e52e-3667-4e8a-bf11-20b9eaccdc8c
platformId: d0355ae1-bdbc-79dd-e52c-355594adca7b
---

# Anti-spam message headers - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

In all organizations with cloud mailboxes, Microsoft 365 scans all incoming messages for spam, malware, and other threats. The results of these scans are added to the following header fields in messages:

- **X-Forefront-Antispam-Report**: Contains information about the message and about how it was processed.
- **X-Microsoft-Antispam**: Contains additional information about bulk mail and phishing.
- **Authentication-results**: Contains information about email authentication results including Sender Policy Framework (SPF), Domainkeys Identified Mail (DKIM), and Domain-based Message Authentication, Reporting, and Conformance (DMARC).

This article describes what's available in these header fields.

For information about how to view an email message header in various email clients, see [View internet message headers in Outlook](https://support.microsoft.com/office/cd039382-dc6e-4264-ac74-c048563d212c).

Tip

You can copy and paste the contents of a message header into the [Message Header Analyzer](https://mha.azurewebsites.net/) tool. This tool helps parse headers into a more readable format.

## X-Forefront-Antispam-Report message header fields

After you have the message header information, find the **X-Forefront-Antispam-Report** header. There are multiple field and value pairs in this header separated by semicolons (;). For example:

`...CTRY:;LANG:hr;SCL:1;SRV:;IPV:NLI;SFV:NSPM;PTR:;SFTY:;...`

The individual fields and values are described in the following table.

Note

The **X-Forefront-Antispam-Report** header contains many different fields and values. Fields that aren't described in the table are used exclusively by the Microsoft anti-spam team for diagnostic purposes.

| Field | Description |
| --- | --- |
| `ARC` | The `Authenticated Received Chain (ARC)` protocol has the following fields: <br>- `AAR`: Records the content of the **Authentication-results** header from DMARC.<br>- `AMS`: Includes cryptographic signatures of the message.<br>- `AS`: Includes cryptographic signatures of the message headers. This field contains a tag of a chain validation called `"cv="`, which includes the outcome of the chain validation as **none**, **pass**, or **fail**. |
| `CAT:` | The category of threat policy applied to the message: <br>- `AMP`: Anti-malware<br>- `BIMP`: Brand impersonation^\*^<br>- `BULK`: Bulk<br>- `DIMP`: Domain impersonation^\*^<br>- `FTBP`: Anti-malware [common attachments filter](anti-malware-protection-about#common-attachments-filter-in-anti-malware-policies)<br>- `GIMP`: [Mailbox intelligence](anti-phishing-policies-about#impersonation-settings-in-anti-phishing-policies-in-microsoft-defender-for-office-365) impersonation^\*^<br>- `HPHSH` or `HPHISH`: High confidence phishing<br>- `HSPM`: High confidence spam<br>- `INTOS`: Intra-Organization phishing<br>- `MALW`: Malware<br>- `OSPM`: Outbound spam<br>- `PHSH`: Phishing<br>- `SAP`: Safe Attachments^\*^<br>- `SPM`: Spam<br>- `SPOOF`: Spoofing<br>- `UIMP`: User impersonation^\*^<br><br>^\*^Defender for Office 365 only.  Multiple forms of protection and multiple detection scans might flag an inbound message. Policies are applied in an order of precedence, and the policy with the highest priority is applied first. For more information, see [What policy applies when multiple protection methods and detection scans run on your email](how-policies-and-protections-are-combined). |
| `CIP:[IP address]` | The connecting IP address. You can use this IP address in the IP Allow List or the IP Block List. For more information, see [Configure connection filtering](connection-filter-policies-configure). |
| `CTRY` | The source country/region as determined by the connecting IP address, which might not be the same as the originating sending IP address. |
| `DIR` | The Directionality of the message: <br>- `INB`: Inbound message.<br>- `OUT`: Outbound message.<br>- `INT`: Internal message. |
| `H:[helostring]` | The HELO or EHLO string of the connecting email server. |
| `IPV:CAL` | The message skipped spam filtering because the source IP address was in the IP Allow List. For more information, see [Configure connection filtering](connection-filter-policies-configure). |
| `IPV:NLI` | The IP address wasn't found on any IP reputation list. |
| `LANG` | The language that the message was written in as specified by the country code (for example, ru\_RU for Russian). |
| `PTR:[ReverseDNS]` | The PTR record (also known as the reverse DNS lookup) of the source IP address. |
| `SCL` | The spam confidence level (SCL) of the message. In cloud organizations, this value doesn't determine whether the message is identified as spam or the action taken on it. It's used primarily in on-premises Exchange environments, including hybrid delivery to the Junk Email folder. To understand how the message was filtered, use the `CAT` and `DIR` values instead. For more information, see [Spam confidence level (SCL)](anti-spam-spam-confidence-level-scl-about). |
| `SFTY` | The message was identified as phishing and is also marked with one of the following values: <br>- 9.19: Domain impersonation. The sending domain is attempting to [impersonate a protected domain](anti-phishing-policies-about#impersonation-settings-in-anti-phishing-policies-in-microsoft-defender-for-office-365). The safety tip for domain impersonation is added to the message (if domain impersonation is enabled).<br>- 9.20: User impersonation. The sending user is attempting to impersonate a user in the recipient's organization, or [a protected user specified in an anti-phishing policy](anti-phishing-policies-about#impersonation-settings-in-anti-phishing-policies-in-microsoft-defender-for-office-365) in Microsoft Defender for Office 365. The safety tip for user impersonation is added to the message (if user impersonation is enabled).<br>- 9.25: First contact safety tip. This value *might* be an indication of a suspicious or phishing message. For more information, see [First contact safety tip](anti-phishing-policies-about#first-contact-safety-tip). |
| `SFV:BLK` | Filtering was skipped and the message was blocked because it was sent from an address in a user's Blocked Senders list.  For more information about how admins can manage a user's Blocked Senders list, see [Configure junk email settings on cloud mailboxes](configure-junk-email-settings-on-exo-mailboxes). |
| `SFV:NSPM` | Spam filtering marked the message as nonspam and the message was sent to the intended recipients. |
| `SFV:SFE` | Filtering was skipped and the message was allowed because it was sent from an address in a user's Safe Senders list.  For more information about how admins can manage a user's Safe Senders list, see [Configure junk email settings on cloud mailboxes](configure-junk-email-settings-on-exo-mailboxes). |
| `SFV:SKA` | The message skipped spam filtering and was delivered to the Inbox because the sender was in the allowed senders list or allowed domains list in an anti-spam policy. For more information, see [Configure anti-spam policies](anti-spam-policies-configure). |
| `SFV:SKB` | The message was marked as spam because it matched a sender in the blocked senders list or blocked domains list in an anti-spam policy. For more information, see [Configure anti-spam policies](anti-spam-policies-configure). |
| `SFV:SKI` | The message skipped spam filtering because the source IP address was in the IP Allow List in the connection filter policy. For more information, see [Configure connection filtering](connection-filter-policies-configure). |
| `SFV:SKN` | The message bypassed spam filtering due to an [Exchange mail flow rule (transport rule)](/en-us/exchange/security-and-compliance/mail-flow-rules/use-rules-to-set-scl). |
| `SFV:SKQ` | The message was released from the quarantine and was sent to the intended recipients. |
| `SFV:SKS` | The message was marked as spam before spam filtering processed it, either by an [Exchange mail flow rule (transport rule) that set the SCL](/en-us/exchange/security-and-compliance/mail-flow-rules/use-rules-to-set-scl), or by a spam decision passed from on-premises Exchange in a [hybrid deployment](/en-us/exchange/exchange-hybrid). These actions are inputs to filtering, not the final decision. [Secure by default](secure-by-default) evaluates the request and might not honor it, so `SFV:SKS` is stamped only when the request to mark the message as spam is honored. |
| `SFV:SPM` | The message was marked as spam by spam filtering. |
| `SRV:BULK` | The message was identified as bulk email by spam filtering and the bulk complaint level (BCL) threshold. When the *MarkAsSpamBulkMail* parameter is `On` (it's on by default), bulk email messages are identified as spam. For more information, see [Configure anti-spam policies](anti-spam-policies-configure). |
| `X-CustomSpam: [ASFOption]` | The message matched an Advanced Spam Filter (ASF) setting. To see the X-header value for each ASF setting, see [Advanced Spam Filter (ASF) settings in anti-spam policies](anti-spam-policies-asf-settings-about). **Note**: ASF adds `X-CustomSpam:` X-header fields to messages *after* mail flow rules process messages. You can't use mail flow rules to identify and act on messages filtered by ASF. |

## X-Microsoft-Antispam message header fields

The following table describes useful fields in the **X-Microsoft-Antispam** message header. Other fields in this header are used exclusively by the Microsoft anti-spam team for diagnostic purposes.

| Field | Description |
| --- | --- |
| `BCL` | The bulk complaint level (BCL) of the message. A higher BCL indicates a bulk mail message is more likely to generate complaints (and is therefore more likely to be spam). For more information, see [Bulk complaint level (BCL)](anti-spam-bulk-complaint-level-bcl-about). |

## Authentication-results message header

The results of email authentication checks for SPF, DKIM, and DMARC are recorded (stamped) in the **Authentication-results** message header in inbound messages. The **Authentication-results** header is defined in [RFC 7001](https://datatracker.ietf.org/doc/html/rfc7001).

The following list describes the text added to the **Authentication-Results** header for each type of email authentication check:

- SPF uses the following syntax:

    ```text
    spf=<pass (IP address)|fail (IP address)|softfail (reason)|neutral|none|temperror|permerror> smtp.mailfrom=<domain>
    ```

    For example:

    ```text
    spf=pass (sender IP is 192.168.0.1) smtp.mailfrom=contoso.com
    
    spf=fail (sender IP is 127.0.0.1) smtp.mailfrom=contoso.com
    ```
- DKIM uses the following syntax:

    ```text
    dkim=<pass|fail (reason)|none> header.d=<domain>
    ```

    For example:

    ```text
    dkim=pass (signature was verified) header.d=contoso.com
    
    dkim=fail (body hash did not verify) header.d=contoso.com
    ```
- DMARC uses the following syntax:

    ```text
    dmarc=<pass|fail|bestguesspass|none> action=<permerror|temperror|oreject|pct.quarantine|pct.reject> header.from=<domain>
    ```

    For example:

    ```text
    dmarc=pass action=none header.from=contoso.com
    
    dmarc=bestguesspass action=none header.from=contoso.com
    
    dmarc=fail action=none header.from=contoso.com
    
    dmarc=fail action=oreject header.from=contoso.com
    ```

### Authentication-results message header fields

The following table describes the fields and possible values for each email authentication check.

| Field | Description |
| --- | --- |
| `action` | Indicates the action taken by the spam filter based on the results of the DMARC check. For example: <br>- `pct.quarantine`: Indicates that a percentage less than 100% of messages that don't pass DMARC are delivered anyway. This result means that the message failed DMARC and the DMARC policy was set to `p=quarantine`. But, the pct field wasn't set to 100%, and the system randomly determined not to apply the DMARC action per the specified domain's DMARC policy.<br>- `pct.reject`: Indicates that a percentage less than 100% of messages that don't pass DMARC are delivered anyway. This result means that the message failed DMARC and the DMARC policy was set to `p=reject`. But, the pct field wasn't set to 100% and the system randomly determined not to apply the DMARC action per the specified domain's DMARC policy.<br>- `permerror`: A permanent error occurred during DMARC evaluation, such as encountering an incorrectly formed DMARC TXT record in DNS. Resending this message isn't likely to have a different result. Instead, you might need to contact the domain's owner in order to resolve the issue.<br>- `temperror`: A temporary error occurred during DMARC evaluation. If the sender sends the message later, it might be processed properly. |
| `compauth` | Composite authentication result. Microsoft 365 combines multiple types of authentication (SPF, DKIM, and DMARC) and other parts of the message to determine whether the message is authenticated. Uses the From: domain as the basis of evaluation. **Note**: Despite a `compauth` failure, the message might still be allowed if other assessments don't indicate a suspicious nature. |
| `dkim` | Describes the results of the DKIM check for the message. Possible values include: <br>- **pass**: Indicates the DKIM check for the message passed.<br>- **fail (reason)**: Indicates the DKIM check for the message failed and why. For example, if the message wasn't signed or the signature wasn't verified.<br>- **none**: Indicates that the message wasn't signed. This result might or might not indicate that the domain has a DKIM record or the DKIM record doesn't evaluate to a result. |
| `dmarc` | Describes the results of the DMARC check for the message. Possible values include: <br>- **pass**: Indicates the DMARC check for the message passed.<br>- **fail**: Indicates the DMARC check for the message failed.<br>- **bestguesspass**: Indicates that no DMARC TXT record exists for the domain exists. If the domain had a DMARC TXT record, the DMARC check for the message would pass.<br>- **none**: Indicates that no DMARC TXT record exists for the sending domain in DNS. |
| `header.d` | Domain identified in the DKIM signature, if any. This domain is queried for the public key. |
| `header.from` | The domain of the From address in the email message header (also known as the `5322.From` address or P2 sender). Recipient sees the From address in email clients. |
| `reason` | The reason composite authentication passed or failed. The value is a three-digit code. For more information, see the Composite authentication Reason codes section. |
| `smtp.mailfrom` | The domain of the MAIL FROM address (also known as the `5321.MailFrom` address, P1 sender, or envelope sender). This email address is used for non-delivery reports (also known as NDRs or bounce messages). |
| `spf` | Describes the results of the SPF check for the message (whether the message source is included in the SPF record for the domain). Possible values include: <br>- `pass (IP address)`: The message source is included in the SPF record for the domain. The source is authorized to send or relay email for the domain.<br>- `fail (IP address)`: Also known as *hard fail*. The message source isn't included in the SPF record for the domain, and the domain instructs the destination email system to reject the message (`-all`).<br>- `softfail (reason)`: Also known as *soft fail*. The message source isn't included in the SPF record for the domain, and the domain instructs the destination email system to accept and mark the message (`~all`).<br>- `neutral`: The message source isn't included in the SPF record for the domain, and the domain offers the destination no specific instruction for the message (`?all`).<br>- `none`: The domain doesn't have an SPF record or the SPF record doesn't evaluate to a result.<br>- `temperror`: A temporary error occurred. For example, a DNS error. The same check later might succeed.<br>- `permerror`: A permanent error occurred. For example, the domain has a badly formatted SPF record. |

### Composite authentication Reason codes

The following table describes the three-digit `reason` codes used with `compauth` results.

Tip

For more information about email authentication results and how to correct failures, see [Security Operations guide for email authentication in Microsoft 365](email-auth-sec-ops-guide).

| Reason code | Description |
| --- | --- |
| 000 | The message failed explicit authentication (`compauth=fail`). The message received a DMARC fail and the DMARC policy action is `p=quarantine` or `p=reject`. |
| 001 | The message failed implicit authentication (`compauth=fail`). The sending domain didn't have email authentication records published, or if they did, they had a weaker failure policy (SPF `~all` or `?all`, or a DMARC policy of `p=none`). |
| 002 | The organization has a policy for the sender/domain pair that's explicitly prohibited from sending spoofed email. An admin manually configures this setting. |
| 010 | The message failed DMARC, the DMARC policy action is `p=reject` or `p=quarantine`, and the sending domain is one of your organization's accepted domains (self-to-self or intra-org spoofing). |
| 1xx | The message passed explicit or implicit authentication (`compauth=pass`). |
| 100 | SPF passed or DKIM passed and the domains in the MAIL FROM and From addresses are aligned. |
| 101 | The message was DKIM signed by the domain used in the From address. |
| 102 | The MAIL FROM and From address domains were aligned, and SPF passed. |
| 103 | The From address domain aligns with the DNS PTR record (reverse lookup) associated with the source IP address |
| 104 | The DNS PTR record (reverse lookup) associated with the source IP address aligns with the From address domain. |
| 108 | DKIM failed due to a message body modification attributed to previous legitimate hops. For example, the message body was modified in the organization's on-premises email environment. |
| 109 | Although the sender's domain has no DMARC record, the message would pass, anyway. |
| 111 | Despite a DMARC temporary error or permanent error, the SPF or DKIM domain aligns with the From address domain. |
| 112 | A DNS timeout prevented the DMARC record from being retrieved. |
| 115 | The message was sent from a Microsoft 365 organization where the From address domain is configured as an [accepted domain](/en-us/exchange/mail-flow-best-practices/manage-accepted-domains/manage-accepted-domains). |
| 116 | The MX record for the From address domain aligns with the PTR record (reverse lookup) of the connecting IP address. |
| 130 | The ARC result from a [trusted ARC sealer](email-authentication-arc-configure) overrode the DMARC failure. |
| 2xx | The message soft-passed implicit authentication (`compauth=softpass`). |
| 201 | The PTR record for the From address domain aligns with the subnet of the PTR record for the connecting IP address. |
| 202 | The From address domain aligns with the domain of the PTR record for the connecting IP address. |
| 3xx | The message wasn't checked for composite authentication (`compauth=none`). |
| 4xx | The message bypassed composite authentication (`compauth=none`). |
| 501 | DMARC wasn't enforced. The message is a valid non-delivery report (also known as an NDR or bounce message), and contact between the sender and recipient is previously established. |
| 502 | DMARC wasn't enforced. The message is a valid NDR for a message sent from this organization. |
| 6xx | The message failed implicit email authentication (`compauth=fail`). |
| 601 | The sending domain is an [accepted domain](/en-us/exchange/mail-flow-best-practices/manage-accepted-domains/manage-accepted-domains) in your organization (self-to-self or intra-org spoofing). |
| 7xx | The message passed implicit authentication (`compauth=pass`). |
| 701-704 | DMARC wasn't enforced because this organization has a history of receiving legitimate messages from the sending infrastructure. |
| 9xx | The message bypassed composite authentication (`compauth=none`). |
| 905 | DMARC wasn't enforced due to complex routing. For example, internet messages are routed through an on-premises Exchange environment or a non-Microsoft service before reaching Microsoft 365. |