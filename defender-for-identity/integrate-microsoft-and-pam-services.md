---
layout: Conceptual
title: Integrate Defender for Identity with PAM services - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/integrate-microsoft-and-pam-services
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
ms.date: 2025-03-30T00:00:00.0000000Z
ms.topic: concept-article
description: Learn how to integrate Microsoft Defender for Identity with your Privileged Access Management (PAM) services.
ms.custom: sfi-image-nochange
locale: en-us
document_id: e42bc69d-43d0-b103-4b95-35cb5669041a
document_version_independent_id: e42bc69d-43d0-b103-4b95-35cb5669041a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/integrate-microsoft-and-pam-services.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: integrate-microsoft-and-pam-services
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/integrate-microsoft-and-pam-services.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: 682637a8-7946-c17d-95e9-714d000778c9
---

# Integrate Defender for Identity with PAM services - Microsoft Defender for Identity | Microsoft Learn

## What are PAM services?

Privileged Access Management (PAM) solutions help reduce the risk of credential misuse by securing, monitoring, and controlling privileged account access to critical resources. PAM solutions secure privileged accounts by storing their credentials in a secure vault, controlling access through approval workflows, and monitoring active sessions to enforce just-in-time (JIT) and just-enough-access (JEA) policies. Common PAM capabilities include, automated password rotation, multifactor authentication, session isolation, and anomaly detection.

## Defender for Identity and PAM

Defender for Identity helps identify and investigate suspicious activities related to privileged accounts, such as unusual sign in patterns or privilege escalation attempts. When integrated with a PAM solution, Microsoft Defender for Identity can detect and investigate suspicious activity involving privileged accounts—such as abnormal sign-ins or privilege escalation attempts. The integration combines PAM’s access controls with Defender for Identity’s behavioral analytics for enhanced threat detection and containment.

## Technology partners

Microsoft Defender for Identity currently supports integration with the following PAM vendors. Dedicated integrations for each partner are now available in the Microsoft 365 Defender partner catalog for streamlined onboarding and visibility.

![Screenshot of the defender for identity connections page](media/integrate-with-partner-system-services/screenshot-of-mdi-technology-partners.png)

| Vendor | Description |
| --- | --- |
| CyberArk | Provides credential vaulting, session monitoring, and threat remediation for privileged identities. |
| BeyondTrust | BeyondTrust Offers identity-centric controls to manage the privilege attack surface and mitigate internal and external threats. |
| Delinea | Delivers centralized authorization and session control for privileged identities across enterprise environments. |

### Reset password

Once PAM integration is enabled, Microsoft Defender automatically tags identities managed by your PAM solution, providing critical context during investigations.

Additionally, you can initiate a password reset for high-risk privileged accounts directly from the Microsoft Defender console. This action uses the connected PAM system.

To reset a password:

1. Go to **Assets &gt; Identities**.
2. Select the relevant identity.
3. Click the three-dot menu (**⋯**) in the top-right corner.
4. Select **Reset password**. The label might vary based on the vendor (for example, **Reset password by CyberArk**, **Reset password by BeyondTrust**).

[![Screenshot of the priviledge access management tags assigned to identity accounts](media/screenshot-of-privilege-access-management-tags-for-identities.png)](media/screenshot-of-privilege-access-management-tags-for-identities.png#lightbox)

This capability streamlines containment and response workflows by embedding privileged access controls directly into the investigation experience.

### Next steps

For more information, see:

[How to integrate Defender for Identity with Delinea](https://docs.delinea.com/online-help/integrations/microsoft/mdi/integrating-mdi.htm)

[How to integrate Defender for Identity with CyberArk](https://community.cyberark.com/marketplace/s/#a35Ht0000018sDVIAY-a39Ht000004GLaEIAW)

[How to integrate Defender for Identity with BeyondTrust](https://docs.beyondtrust.com/insights/docs/microsoft-defender)