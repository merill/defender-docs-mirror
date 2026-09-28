---
layout: FAQ
title: Delegated administration FAQ - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/delegated-administration-faq
summary: >
  <div class="TIP">

  <p>Tip</p>

  <p><em>Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?</em> Use the 90-day Defender for Office 365 trial at the <a href="https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef">Microsoft Defender portal trials hub</a>. Learn about who can sign up and trial terms on <a href="/defender-office-365/try-microsoft-defender-for-office-365">Try Microsoft Defender for Office 365</a>.</p>

  </div>

  <p>This article provides frequently asked questions and answers about delegated administration tasks in Microsoft 365 for Microsoft partners and resellers. Delegated administration includes the ability to manage the built-in security features for all cloud mailboxes in other tenants (companies).</p>
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
f1.keywords:
- NOCSH
author: chrisda
ms.author: chrisd
ms.date: 2023-06-22T00:00:00.0000000Z
audience: ITPro
ms.topic: faq
ms.localizationpriority: medium
ms.assetid: d6a87ce8-2c22-433a-b430-5eab14f6afdc
ms.collection:
- m365-security
- tier3
ms.custom:
- seo-marvel-apr2020
description: Admins can view frequently asked questions and answers about delegated administration tasks in Microsoft 365 for Microsoft partners and resellers.
ms.service: defender-office-365
locale: en-us
document_id: 0d3a45b8-da41-3c13-8071-127131cc2781
document_version_independent_id: 0d3a45b8-da41-3c13-8071-127131cc2781
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/delegated-administration-faq.yml
site_name: Docs
depot_name: Learn.defender-office-365
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: delegated-administration-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/delegated-administration-faq.yml
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 8c0a1c7b-45f2-108e-4974-9304a73a4e97
---

# Delegated administration FAQ - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

This article provides frequently asked questions and answers about delegated administration tasks in Microsoft 365 for Microsoft partners and resellers. Delegated administration includes the ability to manage the built-in security features for all cloud mailboxes in other tenants (companies).

## I'm a reseller and I need to manage my customer tenants. How does this work?

If you're a Microsoft partner or reseller, and you've signed up to be a Microsoft Cloud Solution Provider (CSP), you can request *delegated administration* capabilities in your customer's Microsoft 365 organization. For more information, see the following articles:

- [Cloud Solution Provider program](/en-us/partner-center/csp-overview)
- [Obtain permissions to manage a customer's service or subscription](/en-us/partner-center/customers-revoke-admin-privileges).

## I'm a customer, not a reseller. How can I set up delegated administrator for my subtenants?

Delegated administration is only available for resellers and partners. However, there's a sample PowerShell script to help you view policies in your subtenants (companies). For more information, see [Sample script to view Built-in security add-on for on-premises mailboxes settings for multiple on-premises organizations](/en-us/exchange/standalone-eop/sample-script-standalone-eop-settings-to-multiple-tenants).

## Can I prevent my subtenant admin from modifying my policy?

No. Microsoft 365 doesn't currently have this capability.

## Can I get consolidated reporting across all of my subtenants?

Consolidated reporting across the companies you manage isn't available in Microsoft 365 admin center reports. However, you can get reports by using [Microsoft Graph](/en-us/graph/overview).