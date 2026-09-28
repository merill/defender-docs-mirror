---
layout: Conceptual
title: Enable DMARC reporting for Microsoft Online Email Routing Address (MOERA) and parked domains - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/step-by-step-guides/how-to-enable-dmarc-reporting-for-microsoft-online-email-routing-address-moera-and-parked-domains
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: The steps to configure DMARC for MOERA and parked domains.
ms.service: defender-office-365
author: chrisda
ms.author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-guidance-templates
- m365-security
- tier3
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.custom: sfi-ga-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 2329868b-83e1-aacc-c57f-e30aa5a6ab00
document_version_independent_id: 2329868b-83e1-aacc-c57f-e30aa5a6ab00
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/step-by-step-guides/how-to-enable-dmarc-reporting-for-microsoft-online-email-routing-address-moera-and-parked-domains.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: step-by-step-guides/how-to-enable-dmarc-reporting-for-microsoft-online-email-routing-address-moera-and-parked-domains
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/step-by-step-guides/how-to-enable-dmarc-reporting-for-microsoft-online-email-routing-address-moera-and-parked-domains.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 546798a1-b695-eb13-2896-6f806cd4eb4e
---

# Enable DMARC reporting for Microsoft Online Email Routing Address (MOERA) and parked domains - Microsoft Defender for Office 365 | Microsoft Learn

Best practice for domain email security protection is to protect yourself from spoofing using Domain-based Message Authentication, Reporting, and Conformance (DMARC). Enabling DMARC for your domains should be the first step. For instructions, see [Set up DMARC to validate the From address domain for cloud senders](../email-authentication-dmarc-configure).

This article explains how to configure DMARC for your `onmicrosoft.com` (MOERA) domain and parked custom domains, which aren't covered in [Set up DMARC to validate the From address domain for cloud senders](../email-authentication-dmarc-configure). These domains aren't used for email, but could be exploited by attackers if the domains remain unprotected:

- Your `onmicrosoft.com` domain, also known as the Microsoft Online Email Routing Address (MOERA) domain.
- Parked custom domains that you're currently not using for email yet.

## Prerequisites

Before you begin, make sure you have the following items:

- Microsoft 365 admin center and access to your DNS provider hosting your domains.
- Sufficient permissions as a Global Administrator^\*^ to make the appropriate changes in the Microsoft 365 admin center.
- 10 minutes to complete the steps in this article.

Important

^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.

## Activate DMARC for a MOERA domain

Use the following steps to add a DMARC TXT record for your MOERA domain in the Microsoft 365 admin center:

1. Open the Microsoft 365 admin center at https://admin.microsoft.com.
2. On the left-hand navigation, select **Show All**.
3. Expand **Settings** and press **Domains**.
4. Select your tenant domain (for example, contoso.onmicrosoft.com).
5. On the page that loads, select **DNS records**.
6. Select **+ Add record**.
7. A flyout opens. Ensure that the selected Type is **TXT (Text)**.
8. Add `_dmarc` as **TXT name**.
9. Add your specific DMARC value. For more information, see [Syntax for DMARC TXT records](../email-authentication-dmarc-configure#syntax-for-dmarc-txt-records).
10. Press **Save**.

## Activate DMARC for parked domains

Use the following steps to add a DMARC TXT record for your parked custom domains:

1. Check if SPF is already configured for your parked domain. For instructions, see [SPF TXT records for custom cloud domains](../email-authentication-spf-configure#spf-txt-records-for-custom-domains-in-microsoft-365).
2. Contact your DNS Domain provider.
3. Ask to add this DMARC txt record with your appropriate email addresses: `v=DMARC1; p=reject; rua=mailto:d@rua.contoso.com;ruf=mailto:d@ruf.contoso.com`.