---
layout: Conceptual
title: Address compromised user accounts with automated investigation and response - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/address-compromised-users-quickly
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: how-to
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.custom:
- msecd-doc-authoring-1016
- sfi-image-nochange
ms.date: 2026-07-03T00:00:00.0000000Z
description: Learn how to speed up the process of detecting and addressing compromised user accounts with automated investigation and response capabilities in Microsoft Defender for Office 365 Plan 2.
ms.service: defender-office-365
ai-usage: ai-assisted
locale: en-us
document_id: ea181b42-8471-94e7-76f9-273d6438be07
document_version_independent_id: ea181b42-8471-94e7-76f9-273d6438be07
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/address-compromised-users-quickly.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: address-compromised-users-quickly
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/address-compromised-users-quickly.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 6c94f078-6728-b6dd-8d19-404e3f81bc7e
---

# Address compromised user accounts with automated investigation and response - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

[Microsoft Defender for Office 365 Plan 2](mdo-about#defender-for-office-365-plan-1-vs-plan-2-cheat-sheet) includes powerful [automated investigation and response](air-about) (AIR) capabilities. Such capabilities can save your security operations team a lot of time and effort dealing with threats. This article describes one of the facets of the AIR capabilities, the compromised user security playbook.

The compromised user security playbook enables your organization's security team to:

- Speed up detection of compromised user accounts;
- Limit the scope of a breach when an account is compromised; and
- Respond to compromised users more effectively and efficiently.

## Review alerts for compromised users

When a user account is compromised, atypical or anomalous behaviors occur. For example, phishing and spam messages might be sent internally from a trusted user account. Defender for Office 365 can detect such anomalies in email patterns and collaboration activity within Office 365. When Defender for Office 365 detects these anomalies, alerts are triggered, and the threat mitigation process begins.

## Investigate and respond to a compromised user

When Defender for Office 365 detects signs that a user account is compromised, it triggers alerts. In some cases, that user account is blocked and prevented from sending any further email messages until the issue is resolved by your organization's security operations team. In other cases, an automated investigation begins which can result in recommended actions that your security team should take.

Important

You must have appropriate permissions to perform the following tasks. For more information, see [Required permissions to use AIR capabilities](air-about#required-permissions-and-licensing-for-air).

Use the following procedures to investigate and respond to a compromised user:

- View and investigate restricted users
- View details about automated investigations

Watch this short video to learn how you can detect and respond to user compromise in Microsoft Defender for Office 365 using Automated Investigation and Response (AIR) and compromised user alerts.

### View and investigate restricted users

You have a few options for navigating to a list of restricted users. For example, in the Microsoft Defender portal, you can go to **Email & collaboration** &gt; **Review** &gt; **Restricted Users**. The following procedure describes navigation using the **Alerts** dashboard, which is a good way to see various kinds of alerts that might have been triggered.

1. Open the Microsoft Defender portal at https://security.microsoft.com and go to **Incidents & alerts** &gt; **Alerts**. Or, to go directly to the **Alerts** page, use https://security.microsoft.com/alerts.
2. On the **Alerts** page, filter the results by time period and the policy named **User restricted from sending email**.

    [![The Alerts page in the Microsoft Defender portal filtered for restricted users](media/m365-sc-alerts-page-with-restricted-user.png)](media/m365-sc-alerts-page-with-restricted-user.png#lightbox)
3. If you select the entry by clicking on the name, a **User restricted from sending email** page opens with additional details for you to review. Next to the **Manage alert** button, you can click ![](media/defender-portal-icon-more-actions.png)**More options** and then select **View restricted user details** to go to the **Restricted users** page, where you can [release the restricted user](outbound-spam-restore-restricted-users).

[![The User restricted from sending email page](media/m365-sc-alerts-user-restricted-from-sending-email-page.png)](media/m365-sc-alerts-user-restricted-from-sending-email-page.png#lightbox)

### View details about automated investigations

When an automated investigation has begun, you can see its details and results in the **Action center** in the Microsoft Defender portal.

For detailed instructions on viewing automated investigation results, see [View details of an investigation](air-view-investigation-results).

## Important considerations for automated investigation and response

Keep the following guidance in mind when investigating and responding to compromised users:

- **Stay on top of your alerts**. As you know, the longer a compromise goes undetected, the larger the potential for widespread impact and cost to your organization, customers, and partners. Early detection and timely response are critical to mitigate threats, and especially when a user's account is compromised.
- **Automation assists your security operations team**. Automated investigation and response capabilities can detect a compromised user early on and enable your security operations team to take action to remediate the threat. For help reviewing or approving remediation actions, see [Review and approve actions](air-review-approve-pending-completed-actions).

## Related resources

- [Review the required permissions to use AIR capabilities](air-about#required-permissions-and-licensing-for-air)
- [Find and investigate malicious email in Office 365](threat-explorer-investigate-delivered-malicious-email)
- [Learn about AIR in Microsoft Defender for Endpoint](/en-us/windows/security/threat-protection/microsoft-defender-atp/automated-investigations)
- [Microsoft 365 Roadmap for Defender for Office 365](https://www.microsoft.com/microsoft-365/roadmap?filters=Microsoft%20Defender%20for%20Office%20365)