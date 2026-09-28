---
layout: Conceptual
title: Set up the Standard or Strict preset security policies for Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/step-by-step-guides/ensuring-you-always-have-the-optimal-security-controls-with-preset-security-policies
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Assign users to the Standard or Strict preset security policies in Microsoft Defender for Office 365. These recommended policies apply and maintain Microsoft's best-practice protection settings automatically.
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
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: d8109ecf-6b3d-d09a-cba2-4bc5c30131ad
document_version_independent_id: d8109ecf-6b3d-d09a-cba2-4bc5c30131ad
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/step-by-step-guides/ensuring-you-always-have-the-optimal-security-controls-with-preset-security-policies.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: step-by-step-guides/ensuring-you-always-have-the-optimal-security-controls-with-preset-security-policies
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/step-by-step-guides/ensuring-you-always-have-the-optimal-security-controls-with-preset-security-policies.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 329b809f-0744-216d-89d0-696f399c9af5
---

# Set up the Standard or Strict preset security policies for Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn

When a best practice for a security control changes due to the evolving threat landscape, or as new controls are added, security control settings are automatically updated for accounts assigned to the Standard or Strict preset security policy.

Standard and Strict preset security policies apply predefined security control settings that reflect recommended best practices and are maintained by the service.

To assign accounts to a Standard or Strict preset security policy and let Defender for Office 365 manage ongoing security control updates, follow this procedure.

## Prerequisites

- Microsoft Defender for Office 365 Plan 1 or higher (Included in E5)
- Sufficient permissions (Security Administrator role)
- 5 minutes to complete this procedure.

## Choose between Standard and Strict policies

Our Strict preset security policy has more aggressive limits and settings for security controls that result in more aggressive detections and involve the admin in making decisions on which blocked emails are released to end users.

- Collect the list of your users that require more aggressive detections even if it means more good mail gets flagged as suspicious. These are typically your executive staff, executive support staff, and historically highly targeted users.
- Ensure that the selected users have admin coverage to review and release emails if the end user thinks that the mail might be good and requests that the message be released to them.
- If the user requires more aggressive detections and has admin coverage to review and release blocked messages, place the user in the Strict preset security policy. Otherwise, place the user in the Standard preset security policy.

Tip

For information on what Standard and Strict security policies are, see [Recommended settings for EOP and Microsoft Defender for Office 365 security](../recommended-settings-for-eop-and-office365).

## Enable Security Presets in Microsoft Defender for Office 365

Once you've chosen between the Standard and Strict security preset policies for your users, complete the following steps to assign users to each preset.

1. Identify the users, groups, or domains you would like to include in Standard and Strict security presets.
2. Sign in to the Microsoft Security portal at https://security.microsoft.com.
3. On the left nav, under **Email & collaboration**, select **Policies & rules**.
4. Select **Threat policies**.
5. Select **Preset Security Policies** underneath the **Templated policies** heading
6. Select **Manage** underneath the Standard protection preset.
7. Select **All Recipients** to apply [the built-in security features](../eop-about) to all recipients in the organization, or select **Specific recipients** to manually add users, groups, or domains you want to apply the preset security policy to. Click the **Next** button.
8. Select **All Recipients** to apply Defender for Office 365 Protection for all recipients in the organization, or select **Specific recipients** to manually add users, groups, or domains you want to apply the preset security policy to. Click the **Next** button.
9. On the **Impersonation Protection** section, add email addresses & domains to protect from impersonation attacks, then add any trusted senders and domains you don't want the impersonation protection to apply to, then press **Next**.
10. Click on the **Confirm** button.
11. Select the **Manage protection settings** link in the Strict protection preset.
12. Repeat steps 7-10 again, but for these users *strict* protection should be applied.
13. Click on the **Confirm** button.

Tip

To learn more, see [Preset security policies in Microsoft Defender for Office 365](../preset-security-policies).

## Next step: Use Config Analyzer

Use [Configuration analyzer](../configuration-analyzer-for-security-policies) to determine whether your users are configured according to Microsoft's best practices.

Tip

Configuration analyzer allows admins to find and fix threat policies where the settings are below the Standard or Strict protection profile settings in preset security policies. For more information, see [Configuration analyzer for threat policies in cloud organizations](../configuration-analyzer-for-security-policies).

We recommend preset security policies because they *ensure* admins are exercising Microsoft best practices. However, customized configurations are required is some cases. Learn about the [reasons to use custom threat policies](../mdo-deployment-guide#determine-your-protection-policy-strategy).