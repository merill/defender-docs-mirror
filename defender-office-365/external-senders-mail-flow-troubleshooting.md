---
layout: Conceptual
title: Troubleshooting mail sent to Microsoft 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/external-senders-mail-flow-troubleshooting
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: troubleshooting
ms.localizationpriority: medium
ms.assetid: f4caa4e1-e414-4b21-8822-31c08064c059
ms.collection:
- m365-security
- tier3
ms.custom:
- seo-marvel-apr2020
description: This article provides troubleshooting information for issues with sending email to inboxes in Microsoft 365 & best practices for bulk mailing to Microsoft 365 customers.
ms.service: defender-office-365
ms.date: 2023-06-15T00:00:00.0000000Z
locale: en-us
document_id: 2f53d52d-7614-1a53-35b9-48ae2c4ae639
document_version_independent_id: 2f53d52d-7614-1a53-35b9-48ae2c4ae639
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/external-senders-mail-flow-troubleshooting.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-senders-mail-flow-troubleshooting
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/external-senders-mail-flow-troubleshooting.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
platformId: 03727a14-1c17-a0ed-13b9-972c8a002e16
---

# Troubleshooting mail sent to Microsoft 365 - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

This article provides troubleshooting information for senders who are experiencing issues when trying to send email to recipients in Microsoft 365, and best practices for bulk mailing to customers.

## Are you managing your IP and domain's sending reputation?

[The built-in security features for all cloud mailboxes](eop-about) provide anti-spam protection. We also use email authentication technologies like SPF, DKIM, and DMARC to verify that the domain sending the email is authorized to do so. Many factors influence Microsoft 365 filtering. For example, the sending IP, domain, email authentication, list accuracy, complaint rates, content, and more. One of the principal factors in driving down a sender's reputation and their ability to deliver email is their junk email complaint rate.

## Are you sending email from new IP addresses?

IP addresses that have never been used to send email typically don't have any reputation in our systems. As a result, email from new sources are more likely to experience delivery issues. Once the IP address has built a reputation for not sending spam, Microsoft 365 typically allows for a better email delivery experience.

New IPs for domains with existing SPF records typically experience the added benefit of inheriting some of the domain's sending reputation. If your domain has a good sending reputation, new IPs might experience a faster ramp up time. A new IP can expect to be fully ramped within a couple of weeks or less depending on volume, list accuracy, and junk email complaint rates.

## Confirm that your DNS is set up correctly

For instructions about how to create and maintain DNS records, including the MX record required for mail routing, you need to contact your DNS hosting provider.

## Ensure that you don't advertise yourself as a nonroutable IP

We might not accept email from senders who fail a reverse-DNS lookup. In some cases, legitimate senders advertise themselves incorrectly as a non-internet routable IP when attempting to open a connection to Microsoft 365. IP addresses that are reserved for private (nonroutable) networking include:

- 192.168.0.0/16 (or 192.168.0.0 - 192.168.255.255)
- 10.0.0.0/8 (or 10.0.0.0 - 10.255.255.255)
- 172.16.0.0/11 (or 172.16.0.0 - 172.31.255.255)

## You received a non-delivery report (NDR) when sending email to a user in Office 365

Some delivery issues are the result of Microsoft blocking the sender's IP address, or the user account is identified as banned sender due to previous spam activity. If you believe that you received the non-delivery report (also known as an NDR or bounce message) in error, follow any instructions in the NDR message to resolve the issue.

For more information about the error you received, see the list of error codes in [Email non-delivery reports in Exchange Online](/en-us/exchange/mail-flow-best-practices/non-delivery-reports-in-exchange-online/non-delivery-reports-in-exchange-online).

For example, the following NDR indicates that Microsoft blocked the sending IP address:

`550 5.7.606-649 Access denied, banned sending IP [x.x.x.x]; To request removal from this list please visit https://sender.office.com/ and follow the directions.`

To request removal from this list, see [Use the delist portal to remove yourself from the blocked senders list](external-senders-use-the-delist-portal-to-unblock-yourself).

## My email landed in the recipient's Junk Email folder

If Microsoft 365 incorrectly identifies a message as spam, you can work with the recipient to submit this false positive message to Microsoft for analysis. For more information, see [Report messages and files to Microsoft](submissions-report-messages-files-to-microsoft).

## Microsoft 365 throttled traffic from my IP address

You receive the following NDR because suspicious activity was detected from the source IP address. Mail from the source has been temporarily restricted while it's being evaluated.

`host xxxx.outlook.com [x.x.x.x]: 451 4.7.550 Access denied, please try again later`

After we evaluate the messages and determine everything is OK, we remove the restriction.

## I can't receive email from senders in Microsoft 365

To receive messages from Microsoft 365 senders, make sure your network allows connections from the IP addresses used in Microsoft 365 datacenters. For more information, see [Microsoft 365 URLs and IP address ranges](/en-us/microsoft-365/enterprise/urls-and-ip-address-ranges).

## Best practices for bulk emailing to Microsoft 365 users

If you often conduct bulk email campaigns to Microsoft 365 users, follow the tips in this section.

### Ensure that the From name reflects who is sending the message

The Subject line of the message should be a brief summary of what the message is about. The message body should clearly and succinctly indicate what the offering, service, or product is about. For example:

Correct:

> 
> From: marketing@shoppershandbag.com  Subject: Updated catalog for the Christmas season!

Incorrect:

> 
> From: someone@outlook.com  Subject: Catalogs

The easier you make it for people to know who you are and what you're doing, the less difficulty you have with most spam filters.

### Always include an unsubscribe option in campaign emails

Marketing email, especially newsletters, should always include a way to unsubscribe. For example:

`This email was sent to example@contoso.com by sender@fabrikam.com.`

`Update Profile/Email Address | Instant removal with SafeUnsubscribe&trade; | Privacy Policy`

Requiring recipients to send email with "Unsubscribe" in the Subject line is less preferable than the one-click option. If you require recipients to send a message, ensure that the link takes them to a form where all required fields are populated.

### Use the double opt-in option for marketing email or newsletter registration

This industry best practice is recommended if your company requires or encourages users to register their contact information to access your product or services. The practice of automatically signing up users for marketing emails or e-newsletters during the registration process is questionable in today's internet environment.

If the options to receive your newsletter or special offers are selected by default in your registration process, it's very likely that uninterested users will get your email.

Microsoft recommends the double opt-in option, which means that the check box for marketing email or newsletters isn't selected by default. Additionally, once the registration form has been submitted, a verification email is sent to the user. The verification email contains a URL that allows the user to confirm their decision to receive marketing email.

The double opt-in method helps to eliminate any questionable email marketing practices, because no one can claim that they unintentionally signed up for marketing email.

### Ensure that email message content is transparent and traceable

Email content is as important as the way you send email. Use the following best practices to ensure that your email isn't flagged by email filtering services:

- Requests for recipients to add the sender to their address book should clearly state that this action doesn't guarantee of delivery.
- Redirects included in the body of the message should be similar and consistent, and not multiple and varied. A redirect in this context is anything that points away from the message, such as links and documents. If you have many advertising links, unsubscribe links, or update the profile links, they all should point to the same domain. For example:

    Correct (all domains are the same):

    `unsubscribe.bulkmailer.com`

    `profile.bulkmailer.com`

    `options.bulkmailer.com`

    Incorrect (all domains are different):

    `unsubscribe.bulkmailer.com`

    `profile.excite.com`

    `options.yahoo.com`
- Avoid content with large images and attachments, or messages that are composed entirely of an image.
- Your public privacy or P3P settings should clearly state the presence of tracking pixels (web bugs or beacons).

### Remove incorrect email aliases from your databases

Any incorrect email addresses in your database that result in NDRs are unnecessary and put your outbound email at risk for further scrutiny by email filtering services. Ensure that your email database is up-to-date.