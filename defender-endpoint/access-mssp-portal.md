---
layout: Conceptual
title: Access the Microsoft Defender XDR MSSP customer portal - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/access-mssp-portal
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how MSSPs access a customer tenant in Microsoft Defender XDR using a tenant-specific portal URL.
ms.service: defender-endpoint
ms.subservice: onboard
ms.author: chrisda
author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier3
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: a41eea7a-98d1-ff4d-f44f-a150da92c44a
document_version_independent_id: a41eea7a-98d1-ff4d-f44f-a150da92c44a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/access-mssp-portal.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: access-mssp-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/access-mssp-portal.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: bed3291f-bd9f-92ae-14f6-7782f2cd8236
---

# Access the Microsoft Defender XDR MSSP customer portal - Microsoft Defender for Endpoint | Microsoft Learn

## Access an MSSP customer tenant in Microsoft Defender XDR

Important

Some information relates to prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

Note

The following steps show MSSPs how to find a customer tenant ID and access the tenant-specific Microsoft Defender XDR portal URL.

By default, MSSP customers access their Microsoft Defender XDR tenant through the following URL: `https://security.microsoft.com/`.

MSSPs however, will need to use a tenant-specific URL in the following format: `https://security.microsoft.com?tid=customer_tenant_id` to access the MSSP customer portal.

In general, MSSPs will need to be added to each of the MSSP customer's Microsoft Entra ID that they intend to manage.

Use the following steps to obtain the MSSP customer tenant ID and then use the tenant ID to access the tenant-specific URL:

1. As an MSSP, log in to Microsoft Entra ID with your credentials.
2. Switch directory to the MSSP customer's tenant.
3. Select **Microsoft Entra ID &gt; Properties**. You'll find the tenant ID in the Tenant ID field.
4. Access the MSSP customer portal by replacing the `customer_tenant_id` value in the following URL: `https://security.microsoft.com/?tid=customer_tenant_id`.
5. Access a Unified View for MSSP (Preview) in `https://mto.security.microsoft.com/`