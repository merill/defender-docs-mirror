---
layout: Conceptual
title: Set up your Microsoft Defender XDR trial lab or pilot environment - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/setup-m365deval
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Set up a dedicated Microsoft Defender XDR trial lab or pilot environment in the Microsoft Defender portal, including tenant provisioning and subscription activation for a non-production evaluation.
search.appverid: met150
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
audience: ITPro
ms.collection:
- m365-security
- m365solution-scenario
- m365solution-evalutatemtp
- highpri
- tier1
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.custom: sfi-ga-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 0608bbe2-9138-64a6-75f7-862f23734391
document_version_independent_id: 0608bbe2-9138-64a6-75f7-862f23734391
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/setup-m365deval.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: setup-m365deval
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/setup-m365deval.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: b77a3a1b-4537-77a2-4fcf-bd2a40ecd7bb
---

# Set up your Microsoft Defender XDR trial lab or pilot environment - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- Microsoft Defender XDR

This article guides you to set up a dedicated lab environment. For information on setting up a trial in production, see the new [Pilot and deploy Microsoft Defender](pilot-deploy-overview) guide.

Important

Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

## Create a Microsoft 365 E5 trial tenant

Perform the following steps to create a Microsoft 365 E5 trial tenant.

Note

If you already have an existing Microsoft 365 or Microsoft Entra subscription, you can skip the Microsoft 365 E5 trial tenant creation steps.

1. Go to the [Microsoft 365 E5 product portal](https://www.microsoft.com/microsoft-365/business/office-365-enterprise-e5-business-software?activetab=pivot%3aoverviewtab) and select **Free trial**.
2. Complete the trial registration by entering your email address (personal or corporate). Select **Set up account**.
3. Fill in your first name, last name, business phone number, company name, company size, and country or region.

    Note

    The country or region you set here determines the data center region your Microsoft 365 will be hosted.
4. Choose your verification preference: through a text message or call. Select **Send Verification Code**.
5. Set the custom domain name for your tenant, then select **Next**.
6. Set up the first identity, which is a Global Administrator for the tenant. Fill in **Name** and **Password**. Select **Sign up**.
7. Select **Go to Setup** to complete the Microsoft 365 E5 trial tenant provisioning.
8. Connect your corporate domain to the Microsoft 365 tenant. [Optional] Choose **Connect a domain you already own** and type in your domain name. Select **Next**.
9. Add a TXT or MX record to validate the domain ownership. Once you've added the TXT or MX record to your domain, select **Verify**.
10. [Optional] Create more user accounts for your tenant. You can skip this step by clicking **Next**.
11. [Optional] Download Office apps. Select **Next** to skip this step.
12. [Optional] Migrate email messages. You can skip this step by selecting **Next**.
13. Choose online services. Select **Exchange** and select **Next**.
14. Add MX, CNAME, and TXT records to your domain. When completed, select **Verify**.

Congratulations! You have completed the provisioning of your Microsoft 365 tenant.

## Enable your Microsoft 365 trial subscription

Perform the following steps to enable your Microsoft 365 trial subscription.

Note

Signing up for a trial gives you 25 user licenses to use for a month. See [Try or buy a Microsoft 365 subscription](/en-us/microsoft-365/commerce/try-or-buy-microsoft-365) for details.

1. From [Microsoft 365 Admin Center](https://admin.microsoft.com/), select **Billing** and then navigate to **Purchase services**.
2. Select **Microsoft 365 E5** and select **Start free trial**.
3. Choose your verification preference: through a text message or call. Once you have decided, enter the phone number, select **Text me** or **Call me** depending on your selection.
4. Enter the verification code and select **Start your free trial**.
5. Select **Try now** to confirm your Microsoft 365 E5 trial.
6. Go to the **Microsoft 365 Admin Center** &gt; **Users** &gt; **Active users**. Select your user account, select **Manage product licenses**, and then assign the Microsoft 365 E5 license. Then select **Save**.
7. Select the Global Administrator account again then select **Manage username**.
8. [Optional] Change the domain from *onmicrosoft.com* to your own domain—depending on whether you connected your own domain during tenant setup. Select **Save changes**.