---
layout: Conceptual
title: Set up, review, and edit your security policies and settings in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-business/mdb-configure-security-settings
breadcrumb_path: /defender-business/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: View and edit security policies and settings in Defender for Business
author: chrisda
ms.author: chrisda
ms.topic: overview
ms.service: defender-business
ms.localizationpriority: medium
ms.date: 2026-06-10T00:00:00.0000000Z
ms.reviewer: efratka
ms.collection:
- SMB
- m365-security
- m365solution-mdb-setup
- highpri
- tier1
locale: en-us
document_id: bce81127-0e3c-4b63-5aa5-df4c578e1e5a
document_version_independent_id: bce81127-0e3c-4b63-5aa5-df4c578e1e5a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-business/mdb-configure-security-settings.md
site_name: Docs
depot_name: Learn.defender-business
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdb-configure-security-settings
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-business/mdb-configure-security-settings.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b11ae577-8d18-47ab-998c-ea182a941e71
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/68e4b2d8-b70c-4019-b49a-d1f8881e2aea
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/87b1d24d-826d-4337-90a0-b6c35e4561f2
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/67b2ba1a-6f74-4044-a48a-f0f8ad076b8f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 93619019-9868-9167-b0c0-975163c5825d
---

# Set up, review, and edit your security policies and settings in Microsoft Defender for Business - Microsoft Defender for Business | Microsoft Learn

This article walks you through how to review, create, or edit your security policies, and how to navigate advanced settings in [Microsoft Defender for Business](mdb-overview).

![Visual depicting step 6 - Review and edit security policies in Defender for Business.](media/mdb-setup-step6.png)

When you're setting up or maintaining Defender for Business, an important task is reviewing and configuring device policies:

- **Default policies**:

    - [Next-generation protection](mdb-next-generation-protection)
    - [Firewall protection](mdb-firewall)
- **Other settings**:

    - [Attack surface reduction features](mdb-asr)
- **Settings for advanced features**:

    - [Turn on (or off) advanced features](mdb-portal-advanced-feature-settings#view-settings-for-advanced-features);
    - [Specifying which time zone to use in the Microsoft Defender portal](mdb-portal-advanced-feature-settings#view-and-edit-other-settings-in-the-microsoft-365-defender-portal); and
    - [Whether to receive preview features as they become available](/en-us/defender-xdr/preview).

## Choose where to manage security policies and devices

Before you create or edit security policies, you need to decide which portal to use:

- **Microsoft Defender portal** at https://security.microsoft.com.
- **Microsoft Intune admin center** at https://intune.microsoft.com.

The following table explains both options.

| Option | Description |
| --- | --- |
| Defender portal | A one-stop shop for managing company devices, security policies, and security settings in Defender for Business. With a simplified configuration process, you can use the Defender portal to: <br>- Onboard devices.<br>- Access your security policies and settings.<br>- Use the [Microsoft Defender Vulnerability Management dashboard](mdb-view-tvm-dashboard).<br>- [view and manage incidents](mdb-view-manage-incidents)<br><br>. |
| Intune admin center | Although Defender for Business doesn't include Microsoft Intune, you can use the Intune admin center to: <br>- Manage your company devices and apps, including how they access your company data.<br>- Onboard devices and access your security policies and settings in Intune.<br>- Set up and configure attack surface reduction rules.<br><br> If your company has Intune, you can continue using Intune to manage your devices and security policies. To learn more, see [Manage device security with endpoint security policies in Microsoft Intune](/en-us/intune/intune-service/protect/endpoint-security-policy) |

If you use Intune, and you attempt to view or edit security policies in the Defender portal by going to **Configuration management** &gt; **Device configuration**, you're prompted to choose whether to continue using Intune, or switch to using the Defender portal, as shown in the following screenshot:

![Screenshot showing the prompt to keep using Intune or switch to the Microsoft Defender portal.](media/mdb-usingintune-switchquestion.png)

In the preceding screenshot, **Use Defender for Business configuration instead** refers to using the Defender portal. The Defender portal provides a simplified configuration experience designed for small and medium-sized businesses. If you decide to use the Defender portal, you need to delete any existing security policies in Intune to avoid policy conflicts. For more information, see [I need to resolve a policy conflict](mdb-troubleshooting#i-need-to-resolve-a-policy-conflict).

Note

Policies you manage in the Defender portal are listed in the Intune admin center as **Antivirus** or **Firewall** policies. When you view your firewall policies in the Intune admin center, you see two policies listed: one policy for firewall protection and another for custom rules.

You can export your list of policies from the Intune admin center.