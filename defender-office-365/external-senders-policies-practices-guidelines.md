---
layout: Conceptual
title: Reference Policies, practices, and guidelines - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/external-senders-policies-practices-guidelines
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: article
ms.localizationpriority: medium
ms.assetid: ff3f140b-b005-445f-bfe0-7bc3f328aaf0
ms.collection:
- m365-security
- tier2
description: Microsoft has developed various policies, procedures, and adopted several industry best practices to help protect our users from abusive, unwanted, or malicious email.
ms.service: defender-office-365
ms.date: 2023-06-22T00:00:00.0000000Z
locale: en-us
document_id: b06aa703-5f50-1eda-0781-686e2021afeb
document_version_independent_id: b06aa703-5f50-1eda-0781-686e2021afeb
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/external-senders-policies-practices-guidelines.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: external-senders-policies-practices-guidelines
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/external-senders-policies-practices-guidelines.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: f144548e-b855-4771-b72f-5bbbd07699a7
---

# Reference Policies, practices, and guidelines - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

Microsoft is dedicated to helping provide the most trusted user experience on the web. Therefore, Microsoft has developed various policies, procedures, and adopted several industry best practices to help protect our users from abusive, unwanted, or malicious email. Senders attempting to send email to users should ensure they fully understand and are following the guidance in this article to help in this effort and to help avoid potential delivery issues.

If you aren't in compliance with these policies and guidelines, it may not be possible for our support team to assist you. If you're adhering to the guidelines, practices, and policies presented in this article and are still experiencing delivery issues based on your sending IP address, follow the steps to submit a delisting request. For instructions, see [Use the delist portal to remove yourself from the blocked senders list](external-senders-use-the-delist-portal-to-unblock-yourself).

## General Microsoft policies

Email sent to Microsoft 365 users must comply with all Microsoft policies governing email transmission and use of Microsoft 365.

- Terms of Services applicable to Microsoft 365; in particular, the prohibition against using the service to spam or distribute malware.
- [Microsoft Services Agreement](https://www.microsoft.com/servicesagreement/)

## Governmental regulations

Email sent to Microsoft 365 users must adhere to all applicable laws and regulations governing email communications in the applicable jurisdiction.

- [CAN-SPAM Act: A Compliance Guide for Business](https://www.ftc.gov/business-guidance/resources/can-spam-act-compliance-guide-business)
- ["Remove Me" Responses and Responsibilities: Email Marketers Must Honor "Unsubscribe" Claims](https://www.lawpublish.com/ftc-emai-marketers-unsubscribe-claims.html)

## Technical guidelines

Email sent to Microsoft 365 should comply with the applicable recommendations listed in the following documents (some links are only available in English).

- [RFC 2505: Anti-Spam Recommendations for SMTP MTAs](https://www.ietf.org/rfc/rfc2505.txt)
- [RFC 2920: SMTP Service Extension for Command Pipelining](https://www.ietf.org/rfc/rfc2920.txt)

In addition, email servers connecting to Microsoft 365 must adhere to the following requirements:

- The sender is expected to comply with all technical standards for the transmission of Internet email, as published by The Internet Society's Internet Engineering Task Force (IETF), including RFC 5321, RFC 5322, and others.
- After given a numeric SMTP error response code between 500 and 599 (also known as a permanent non-delivery response or NDR), the sender must not attempt to retransmit that message to that recipient.
- After multiple non-delivery responses, the sender must cease further attempts to send email to that recipient.
- Messages must not be transmitted through insecure email relay or proxy servers.
- The mechanism for unsubscribing, either from individual lists or all lists hosted by the sender, must be clearly documented and easy for recipients to find and use.
- Connections from dynamic IP addresses might not be accepted.
- Email servers must have valid reverse DNS records.

## Reputation management

Senders, ISP's, and other service providers should actively manage the reputation of your outbound IP addresses.

## Microsoft 365 limits

Senders must adhere to Microsoft 365 limits listed in [Built-in security features limits](/en-us/office365/servicedescriptions/exchange-online-protection-service-description/exchange-online-protection-limits).

## Email delivery resources and organizations

Microsoft actively works with industry bodies and service providers in order to improve the internet and email ecosystem. These organizations have published best practice documents that we support and recommend senders adhere to. Adhering to these recommendations improves your ability to deliver email among several email service providers around the world.

- [Messaging Malware Mobile Anti-Abuse Working Group](https://www.m3aawg.org/)
- [Online Trust Alliance](https://www.internetsociety.org/ota/)
- [Email Sender & Provider Coalition](https://www.espcoalition.org/)

## Abuse and spam reporting

To report unlawful, abusive, unwanted or malicious email, see [Report messages and files to Microsoft](submissions-report-messages-files-to-microsoft). Sending these types of communications is a violation of Microsoft policy, and appropriate action is taken on confirmed reports.

## Law enforcement

If you're a member of law enforcement and wish to serve Microsoft Corporation with legal documentation regarding Microsoft 365, or if you have questions regarding legal documentation that you submitted to Microsoft, call +1 (425) 722-1299.