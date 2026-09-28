---
layout: Conceptual
title: Tune Protection Settings in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/step-by-step-guides/tune-microsoft-defender-for-office-365
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Learn how to tune Microsoft Defender for Office 365 by adjusting security controls, filtering thresholds, allows and blocks, routing configurations, and submission-based learning.
ms.service: defender-office-365
author: MSFTBen
ms.author: chrisda
ms.localizationpriority: medium
ms.collection:
- m365-guidance-templates
- m365-security
- tier3
ms.topic: how-to
ms.date: 2026-06-12T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1014
locale: en-us
document_id: a3cf53af-f1c3-b89f-9c4d-adefbfe83852
document_version_independent_id: a3cf53af-f1c3-b89f-9c4d-adefbfe83852
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/step-by-step-guides/tune-microsoft-defender-for-office-365.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: step-by-step-guides/tune-microsoft-defender-for-office-365
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/step-by-step-guides/tune-microsoft-defender-for-office-365.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 0f39048b-4137-d6be-7624-a02be2976be3
---

# Tune Protection Settings in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn

When a relevant license is enabled, Microsoft Defender for Office 365 protects collaboration across Exchange Online, Teams, SharePoint, OneDrive, and Microsoft 365 applications by default. However, you can do some "tuning" for maximum benefit.

The term "tuning" is used often and can mean different things. For example:

- Configuring security controls or configuring connectors for complex routing and dual filtering scenarios as part of initial setup.
- Setting security control thresholds (for example, the bulk email slider and the advanced filtering slider) to determine how aggressively email is blocked.
- Adding and managing customer configured allows and blocks. Allows are a powerful tool for managing email deliverability but can let malicious or unwanted email be delivered if not correctly managed. Blocks ensure unwanted email isn't delivered but can lead to user productivity loss.
- Submissions and system learning, or how the filtering stack self corrects based on the submission of false positive and false negative email.

## Configuring security controls

The easiest and safest way to configure security controls is by onboarding to [preset security policies](../preset-security-policies). By using the Standard or Strict preset security policies, you always have Microsoft's recommended, best practice configuration for users. For instructions, see [Steps to set up the Standard or Strict preset security policies for Microsoft Defender for Office 365](ensuring-you-always-have-the-optimal-security-controls-with-preset-security-policies).

Are you worried about attacks targeting your CEO, CIO, or CFO? You can [manage and monitor priority accounts in Microsoft 365](/en-us/microsoft-365/admin/security-and-compliance/priority-accounts).

If you use custom security policies, configuration analyzer gives recommendations to make sure you follow Microsoft's best practices. You can [Optimize and correct threat policies with configuration analyzer](optimize-and-correct-security-policies-with-configuration-analyzer).

## Complex routing and dual filtering scenarios

Using a non-Microsoft email filtering solution with Defender for Office 365 requires some extra configuration to ensure you're getting the best from both filtering solutions. For more information, see [Getting started with defense in-depth configuration for email security](defense-in-depth-guide). You need to be careful when using connectors to route mail to ensure that Defender for Office 365 has access to the original email sender information. To meet this requirement, configure [Enhanced filtering for connectors in Exchange Online](/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/enhanced-filtering-for-connectors).

## Security control thresholds

The bulk email slider and the phishing email threshold slider allow you to determine how aggressively each of those filters is applied. To optimize the threshold where bulk mail is treated as spam, you can [Assess and tune your filtering for bulk mail in Defender for Office 365](tune-bulk-mail-filtering-walkthrough). [Recommended email and collaboration threat policy settings for cloud organizations](../recommended-settings-for-eop-and-office365#phishing-email-thresholds-in-anti-phishing-policies-in-microsoft-defender-for-office-365) contains best practices for choosing the right [Phishing email threshold](../anti-phishing-policies-about#phishing-email-thresholds-in-anti-phishing-policies-in-microsoft-defender-for-office-365) for your organization.

## Customer configured allows and blocks

Overrides are a powerful tool that can be used to deliver or block email regardless of how Defender for Office 365 evaluates the message. [Understanding overrides within the email entity page in Microsoft Defender for Office 365](understand-overrides-in-email-entity) provides a guide for using the email entity page to understand why a message was allowed or blocked across all the different types of available overrides.

### How submissions and system learning affect allows and blocks

The single most important thing you can do to improve the accuracy of email filtering for users is to [Report spam, non-spam, phishing, suspicious email and files to Microsoft](../submissions-report-messages-files-to-microsoft). This information informs the Microsoft Security Analyst team what changes need to be made across the entire filtering stack to ensure users have the best possible experience. Here are some best practices for [How to handle malicious emails that are delivered to recipients using Microsoft Defender for Office 365](how-to-handle-false-negatives-in-microsoft-defender-for-office-365) and [How to handle legitimate emails getting blocked from delivery using Microsoft Defender for Office 365](how-to-handle-false-positives-in-microsoft-defender-for-office-365).