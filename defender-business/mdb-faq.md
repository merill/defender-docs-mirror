---
layout: FAQ
title: Microsoft Defender for Business Frequently Asked Questions - Microsoft Defender for Business | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-business/mdb-faq
summary: >
  <p>Use this article to get answers to questions you might have about Defender for Business.</p>
breadcrumb_path: /defender-business/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Get answers to questions about Defender for Business, a cybersecurity solution for small and medium sized businesses.
search.appverid: MET150
author: chrisda
ms.author: chrisda
audience: Admin
ms.topic: faq
ms.service: defender-business
ms.localizationpriority: medium
ms.date: 2026-06-10T00:00:00.0000000Z
ms.reviewer: efratka, nehabha
f1.keywords: NOCSH
ms.collection:
- SMB
- m365-security
- tier1
locale: en-us
document_id: bff2aa2f-6800-4408-da7c-29803588fd3d
document_version_independent_id: bff2aa2f-6800-4408-da7c-29803588fd3d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-business/mdb-faq.yml
site_name: Docs
depot_name: Learn.defender-business
page_type: faq
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdb-faq
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-business/mdb-faq.yml
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/b11ae577-8d18-47ab-998c-ea182a941e71
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/062d60c9-ee0f-402e-a046-b4e67c3572d6
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/87b1d24d-826d-4337-90a0-b6c35e4561f2
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/17d3b3f6-a66e-4c69-9774-14a73c38e669
platformId: 30067397-a51b-3d5a-34d1-184dbcd30dbb
---

# Microsoft Defender for Business Frequently Asked Questions - Microsoft Defender for Business | Microsoft Learn

Use this article to get answers to questions you might have about Defender for Business.

## How do I try or buy Defender for Business?

We recommend working with a [Microsoft partner](https://www.microsoft.com/security/business/find-a-partner).

If you prefer to try or buy Defender for Business on your own, go to the [Defender for Business](https://www.microsoft.com/security/business/endpoint-security/microsoft-defender-business) product page, and select the option to try or buy Defender for Business.

For more information, see [Get Defender for Business](get-defender-business).

## Is there a limit to how many users can be licensed for Defender for Business?

Yes.

Defender for Business is designed for small and medium-sized businesses with up to 300 users. If you have more than 300 users, consider an enterprise solution. For example:

- [Defender for Endpoint](/en-us/defender-endpoint/microsoft-defender-endpoint)
- [Microsoft Defender XDR](/en-us/defender-xdr/microsoft-365-defender)
- [Microsoft 365 for enterprise](/en-us/microsoft-365/enterprise/microsoft-365-overview)

## How many devices can I onboard and secure with Defender for Business?

You can onboard and secure up to five client devices per user license.

Note

Servers require extra licenses. For example, [Microsoft Defender for Business servers](get-defender-business#how-to-get-microsoft-defender-for-business-servers).

## Does Defender for Business protect Mac, Android, and iOS/iPadOS client devices?

Yes.

Defender for Business supports protection for Windows, Mac, Android, and iOS/iPadOS devices. For more information, see [Onboard devices](mdb-onboard-devices).

## Does Defender for Business support servers?

Yes, but you need to buy extra licenses.

If you plan to onboard an instance of Windows Server or Linux Server, you need an extra license. For example, [Microsoft Defender for Business servers](get-defender-business#how-to-get-microsoft-defender-for-business-servers). This license is available as an add-on to the standalone version of Defender for Business and Microsoft 365 Business Premium. The Microsoft Defender for Business servers license is priced at $3 per server instance. You have two choices for implementation:

- Purchase a license for each onboarded server.
- Offboard servers from Defender for Business.

If you have more than 60 servers, you need a different kind of license. For example:

- Microsoft Defender for Endpoint Server.
- Microsoft Defender for Servers Plan 1 or Plan 2.

For more information, see [Onboard servers to Microsoft Defender for Endpoint](/en-us/defender-endpoint/onboard-server).

## What's different between Microsoft Defender for Business servers and Microsoft Defender for Servers Plan 1 and Plan 2?

The following table compares server options for Defender for Business customers:

| Server license | Description |
| --- | --- |
| [Microsoft Defender for Business servers](get-defender-business#how-to-get-microsoft-defender-for-business-servers) | An add-on to Defender for Business and Microsoft 365 Business Premium. This offering enables small and medium sized businesses with up to 300 users to onboard and protect servers and client devices in the Microsoft Defender portal at https://security.microsoft.com. |
| [Microsoft Defender for Servers Plan 1/Plan 2](/en-us/azure/defender-for-cloud/plan-defender-for-servers) | An enterprise-focused offering you can purchase with any Microsoft cloud subscription. This offering is part of [Microsoft Defender for Cloud](/en-us/azure/defender-for-cloud/defender-for-cloud-introduction), and includes advanced threat hunting with six months of data retention and the Microsoft Threat Experts service.  The admin experience for Defender for Cloud resides within the Azure portal at https://portal.azure.com. |

Adding Defender for Cloud to a Defender for Business organization doesn't change the simplified configuration experience in Defender for Business. The functionality in Microsoft Defender for Servers Plan 1 or Plan 2 works with Defender for Business.

## Can I configure more than one web content filtering policy in Defender for Business?

Currently, No.

Defender for Business supports only one uniform web filtering policy per Defender for Business organization.

For more information, see [Set up web content filtering](mdb-web-content-filtering).

## Can I use non-Microsoft antivirus/anti-malware software with Defender for Business?

Technically, yes.

However, you could run into an issue where real-time protection could be turned off on those devices. If real-time protection is turned off on a device, the device appears unprotected.

In Defender for Business, real-time protection is turned on by default. But devices running non-Microsoft antivirus/antimalware software could affect your settings.

To learn more, see [I'm seeing indications that some devices aren't protected even though they're onboarded to Defender for Business](mdb-troubleshooting#i-m-seeing-indications-that-some-devices-aren-t-protected-even-though-they-re-onboarded-to-defender-for-business).

## Are device control capabilities available in Microsoft Defender for Business?

Yes, but with limitations.

Defender for Business includes built-in attack surface reduction features. For more information, see [Attack surface reduction in Microsoft Defender for Business](mdb-asr).

You can't create custom ASR rules in Defender for Business. You need [Microsoft Intune](/en-us/intune/intune-service/fundamentals/what-is-intune) to create ASR rules.

On macOS devices, you can use Jamf or Microsoft Intune to set up device control on Mac. For more information, see [Device Control for macOS](/en-us/defender-endpoint/mac-device-control-overview).

[Device control in Microsoft Defender for Endpoint](/en-us/defender-endpoint/device-control-overview) prevents users, endpoints, or both from using unauthorized removable storage media.

## How do I configure attack surface reduction capabilities in Defender for Business?

See [Attack surface reduction in Microsoft Defender for Business](mdb-asr).

## How do I run custom reports with Defender for Business?

Defender for Business uses Defender for Endpoint APIs for all available capabilities. You can use the APIs with a reporting tool. As an example scenario, you can use a Power BI connector and schedule a PowerShell script to generate executive summaries formatted in HTML, and send those summaries by email.

For more information, see the following resources:

- [Overview of management and APIs](/en-us/defender-endpoint/api/management-apis)
- [API reference information](/en-us/defender-endpoint/api/exposed-apis-create-app-partners)
- [Microsoft Defender for Business and Microsoft partner resources](mdb-partners)

## I'm a Microsoft partner. Can I manage multiple organizations from one control panel, or do I need to sign in to each organization individually?

Several options are available, including Microsoft 365 Lighthouse and using APIs to integrate with your tools. For more information, see [Microsoft Defender for Business and Microsoft partner resources](mdb-partners).

Defender for Business integrates with Microsoft 365 Lighthouse for multitenant support in a single console (https://lighthouse.microsoft.com). For more information, see [Overview of Microsoft 365 Lighthouse](/en-us/microsoft-365/lighthouse/m365-lighthouse-overview).

You can use Defender for Endpoint APIs to integrate Defender for Business with your remote monitoring and management (RMM) tools and your professional service automation (PSA) software. For more information, see [Microsoft Defender for Business and Microsoft partner resources](mdb-partners).

## How does Microsoft Intune work with Defender for Business?

Defender for Business capabilities are integrated with endpoint security policies in the Microsoft Intune admin center. You can use either the Microsoft Defender portal or the Intune admin center to onboard devices and configure security policies. Some capabilities, such as controlled folder access and attack surface reduction rules must be configured in the Intune admin center.

For more information, see the following articles:

- [Set up, review, and edit your security policies and settings in Microsoft Defender for Business](mdb-configure-security-settings)
- [Manage device security with endpoint security policies in Microsoft Intune](/en-us/intune/intune-service/protect/endpoint-security-policy)

## If I'm already using Microsoft 365 Business Premium, why do I need Defender for Business?

[Defender for Business](mdb-overview) provides advanced threat protection for your organization's devices. [Microsoft 365 Business Premium](/en-us/microsoft-365/business-premium/m365bp-overview) includes Defender for Business and more capabilities. For example:

- Defender for Office 365 Plan 1 to protect your organization's email and files.
- Azure Information Protection Plan 1.
- Sensitivity labeling.
- Data loss prevention for email and files.

For more information, see [Microsoft 365 User Subscription Suites for Small and Medium-sized Businesses](https://cdn-dynmedia-1.microsoft.com/is/content/microsoftcorp/microsoft/bade/documents/products-and-services/en-us/education/Modern-Work-Plan-Comparison-SMB.pdf).

## What are the differences between Defender for Business and Defender for Endpoint Plans 1 and 2?

[Defender for Business](mdb-overview) is designed for small and medium-sized businesses who have up to 300 users. Capabilities in Defender for Business include next-generation protection, attack surface reduction, endpoint detection & response (EDR), and automated investigation and remediation. Defender for Business also features [simplified configuration](mdb-setup-configuration) and [device onboarding options](mdb-onboard-devices) that streamline the overall setup and configuration process.

[Defender for Endpoint](/en-us/defender-endpoint/microsoft-defender-endpoint) is an enterprise endpoint security platform designed to help organizations prevent, detect, investigate, and respond to advanced threats.

- Defender for Endpoint Plan 1 includes next-generation protection and attack surface reduction capabilities
- Defender for Endpoint Plan 2 extends Plan 1 capabilities with core vulnerability management capabilities, EDR, automated investigation & remediation, threat hunting, and six months of data retention

For a detailed comparison, see [How does Defender for Business compare to Microsoft Defender for Endpoint?](mdb-overview#how-does-defender-for-business-compare-to-microsoft-defender-for-endpoint).

## Can I have a mix of Microsoft endpoint security subscriptions?

No.

Microsoft Defender for Business doesn't support mixed licensing. An organization with Defender for Business (included in Microsoft 365 Business Premium) and with Defender for Endpoint Plan 2 (included in Microsoft 365 E5 Security) defaults to the Defender for Business experience.

For example, you have 80 users licensed for Defender for Business as part of a Microsoft 365 Business Premium, and you add Microsoft 365 E5 Security for 30 of those users. The experience for all users defaults to Defender for Business.

To use the Defender for Endpoint Plan 2 experience, do the following steps:

- License all users for Defender for Endpoint Plan 2 (through the standalone version of Defender for Endpoint Plan 2 or Microsoft 365 E5 Security).
- Contact Microsoft Support to request the switch for your organization.

For more information, see [Manage your subscription settings](mdb-manage-subscription).

For more information about licenses and product terms, see [Licensing and product terms for Microsoft 365 subscriptions](https://www.microsoft.com/licensing/terms/productoffering/Microsoft365/MCA).

## My organization now has more than 300 users, and I have a mix of Microsoft endpoint security subscriptions. Can I still use Defender for Business?

[Defender for Business](mdb-overview) and [Microsoft 365 Business Premium](/en-us/microsoft-365/business-premium/) are for organizations with a maximum of 300 users. If you now have more than 300 users, we recommend a subscription that includes [Defender for Endpoint](/en-us/defender-endpoint/microsoft-defender-endpoint) for all users.

For example, your company grew from 250 to 330 users, and you now have 300 Defender for Business licenses and 30 Microsoft 365 E3 licenses (Microsoft 365 E3 includes Defender for Endpoint Plan 1).

When it's time to renew your subscription, we recommend choosing one of the following enterprise plans:

- [Microsoft 365 E5](https://www.microsoft.com/microsoft-365/enterprise/E5) (includes Defender for Endpoint Plan 2 plus Defender for Office 365 Plan 2)
- [Microsoft 365 E3](https://www.microsoft.com/microsoft-365/enterprise/E3) (includes Defender for Endpoint Plan 1)
- [Defender for Endpoint Plan 1 or 2](https://www.microsoft.com/security/business/endpoint-security/microsoft-defender-endpoint)

For details about licenses and product terms, see [Licensing and product terms for Microsoft 365 subscriptions](https://www.microsoft.com/licensing/terms/productoffering/Microsoft365/MCA).

## How do I view my organization's Microsoft subscriptions and user licenses?

You can view your current subscriptions and licenses on the **Licenses** page of the Microsoft 365 admin center at https://admin.microsoft.com/Adminportal/Home#/licenses.

Also see [Understand subscriptions and licenses in Microsoft 365 for business](/en-us/microsoft-365/commerce/licenses/subscriptions-and-licenses).