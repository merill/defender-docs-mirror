---
layout: Conceptual
title: Microsoft Defender XDR prerequisites - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/prerequisites
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Learn about the licensing, hardware and software requirements, and other configuration settings for Microsoft Defender XDR
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.topic: install-set-up-deploy
ms.date: 2025-04-03T00:00:00.0000000Z
ms.custom: sfi-ga-nochange
locale: en-us
document_id: 4935a636-656b-8582-333b-5009abddf070
document_version_independent_id: 4935a636-656b-8582-333b-5009abddf070
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/prerequisites.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: prerequisites
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/prerequisites.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/1dd701e0-441f-4b0a-9806-aa47decc4e35
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/0a2fc935-5977-4aa6-9f55-0be03bd2acb8
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: ee5017ec-31f0-1f89-af74-3549f6bc9b11
---

# Microsoft Defender XDR prerequisites - Microsoft Defender XDR | Microsoft Learn

Learn about licensing and other requirements for provisioning and using [Microsoft Defender](microsoft-365-defender).

## Licensing requirements

Microsoft Defender natively correlates Microsoft security products' signals, providing security operations teams a single pane of glass to detect, investigate, respond, and protect your assets. These signals are dependent on the license that you have and the access provisioned to you.

Any of these licenses give you access to Microsoft Defender features via the Microsoft Defender portal without any additional cost:

- Microsoft 365 E5 or A5
- Microsoft 365 E3 with the Microsoft Defender Suite add-on
- Microsoft 365 E3 with the Enterprise Mobility + Security E5 add-on
- Microsoft 365 A3 with the Microsoft 365 A5 Security add-on
- Windows 10 Enterprise E5 or A5
- Windows 11 Enterprise E5 or A5
- Enterprise Mobility + Security (EMS) E5 or A5
- Office 365 E5 or A5
- Microsoft Defender for Endpoint
- [Microsoft Defender for IoT - Enterprise IoT protection](/en-us/defender-for-iot/enterprise-iot-licenses#enterprise-iot-licenses) (includes protection for enterprise IoT devices with the Microsoft 365 E5 (ME5) or E5 Security license)
- Microsoft Defender for Identity
- Microsoft Defender for Cloud Apps or [Cloud App Discovery](/en-us/defender-cloud-apps/editions-cloud-app-security-aad)
- Microsoft Defender for Office 365 (Plan 2)
- Microsoft 365 Business Premium
- Microsoft Defender for Business

For more information, [view the Microsoft 365 Enterprise service plans](https://www.microsoft.com/licensing/product-licensing/microsoft-365-enterprise).

Note

- Automatic attack disruption requires Microsoft Defender for Endpoint Plan 2. For more information, see [Configure automatic attack disruption capabilities](configure-attack-disruption).
- Threat analytics also requires Defender for Endpoint Plan 2. For more information, see [Threat analytics in Microsoft Defender](threat-analytics).

> 
> Don't have license yet? [Try or buy a Microsoft 365 subscription](/en-us/microsoft-365/commerce/try-or-buy-microsoft-365)

### Check your existing licenses

Go to Microsoft 365 admin center ([admin.microsoft.com](https://admin.microsoft.com/)) to view your existing licenses. In the admin center, go to **Billing** &gt; **Licenses**.

Note

You need to be assigned either the **Billing admin** or higher [role in Microsoft Entra ID](/en-us/azure/active-directory/roles/permissions-reference) to be able to see license information. If you encounter access problems, contact a Global Administrator.

## Required permissions

You must at least be a **security administrator** in Microsoft Entra ID to turn on Microsoft Defender. For the list of roles required to use Microsoft Defender and information on how access to data is regulated, read about [managing access to Microsoft Defender](m365d-permissions).

Important

Microsoft recommends that you use roles with the fewest permissions. Using lower permissioned accounts helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

## Browser requirements

Access Microsoft Defender in the Microsoft Defender portal using Microsoft Edge, Internet Explorer 11, or any HTML 5 compliant web browser.

## Availability to US GCC, GCC High, and other US government institutions

For information related to US Government customers, see [Microsoft Defender for US Government customers](usgov).

Currently, the Microsoft Defender for Office 365 integration into the unified Microsoft Defender features are not available to customers in the following Office 365 datacenter locations:

- Norway
- South Africa
- United Arab Emirates
- Sweden
- Singapore