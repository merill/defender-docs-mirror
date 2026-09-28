---
layout: Conceptual
title: Get Started with Defense In-Depth Configuration for Email Security - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/step-by-step-guides/defense-in-depth-guide
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Step-by-step configuration guidance on how to get security value from Microsoft Defender for Office 365 when you have non-Microsoft email filtering.
ms.service: defender-office-365
f1.keywords:
- NOCSH
author: MSFTBen
ms.author: benharri
ms.localizationpriority: medium
audience: ITPro
ms.collection:
- m365-guidance-templates
- m365-security
- tier3
ms.topic: how-to
search.appverid: met150
ms.date: 2026-07-24T00:00:00.0000000Z
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 28ef75aa-7a84-eecd-bf3d-8d5a5241d257
document_version_independent_id: 28ef75aa-7a84-eecd-bf3d-8d5a5241d257
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/step-by-step-guides/defense-in-depth-guide.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: step-by-step-guides/defense-in-depth-guide
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/step-by-step-guides/defense-in-depth-guide.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
platformId: 4ddfca39-0dbe-2567-f8f7-ad6456b20c52
---

# Get Started with Defense In-Depth Configuration for Email Security - Microsoft Defender for Office 365 | Microsoft Learn

This guide is for you if:

- You're licensed for Microsoft Defender for Office 365 and host your mailboxes in Office 365
- You're also using a non-Microsoft solution for your email security

The following information explains how to get the most out of Microsoft Defender for Office 365 in a dual-use deployment, broken down into easy to follow steps.

## Prerequisites

Before you begin, make sure you have the following requirements in place:

- Mailboxes hosted in Office 365
- One or more of:
    - Microsoft Defender for Office 365 Plan 1 for protection features.
    - Microsoft Defender for Office 365 Plan 2 for most other features (included in E5 plans).
    - Microsoft Defender for Office 365 Trial (available to all customers at https://aka.ms/tryMDO).
- Sufficient permissions to configure the features discussed in this article.

## Step 1: Understand the value you already have

Start by reviewing the protection and investigation capabilities already included with Microsoft Defender for Office 365.

### Review built-in protection features

Built-in protection features provide a baseline layer of security that's included with Microsoft Defender for Office 365.

- Built-in protection offers a base level of unobtrusive protection, and includes malware, zero day (Safe Attachments), and URL protection (Safe Links) in email (including internal email), SharePoint, OneDrive, and Microsoft Teams. URL protection provided by built-in protection is via API call only. It doesn't wrap or rewrite URLs but does require a supported Outlook client. You can create your own custom Safe Links policies and Safe Attachments policies to expand your protection.

    To learn more and watch an overview video on Safe Links, see [Complete Safe Links overview](../safe-links-about)

    To learn more about Safe Attachments, see [Safe Attachments](../safe-attachments-about)

### Review detection, investigation, response, and hunting features

The following capabilities help security teams investigate, respond to, and proactively hunt threats.

- When alerts fire in Microsoft Defender for Office 365, they're automatically correlated, and combined into Incidents to help reduce the alert fatigue on security staff. Automated Investigation and Response (AIR) triggers investigations to help remediate and contain threats.

    To learn more, watch an overview video, and get started, see [Incident response with Microsoft Defender XDR](/en-us/defender-xdr/incidents-overview)
- Threat Analytics is our in-product, detailed threat intelligence solution from expert Microsoft security researchers. Threat Analytics contains detailed reports that are designed to get you up to speed on the latest threat groups, attack techniques, how to protect your organization with Indicators of Compromise (IOC) and much more.

    To learn more, watch an overview video, and get started, see [Threat analytics in Microsoft Defender XDR](/en-us/defender-xdr/threat-analytics)
- Explorer can be used to hunt threats, visualize mail flow patterns, spot trends, and identify the affect of changes you make during tuning Defender for Office 365. You can also quickly delete messages from your organization with a few simple clicks.

    To learn more and get started, see [Threat Explorer and Real-time detections](../threat-explorer-real-time-detections-about)
- Advanced hunting can be used to proactively hunt for threats in your organization, using shared queries from the community to help you get started. You can also use custom detections to set up alerts when personalized criteria are met.

To learn more, watch an overview video, and get started, see [Overview - Advanced hunting](/en-us/defender-xdr/advanced-hunting-overview)

## Step 2: Enhance the value further with these simple steps

After reviewing your existing protections, enable additional features and user education tools to close gaps and strengthen coverage.

### Enable additional protection features

You can increase protection further by enabling additional Defender for Office 365 features.

- Consider enabling policies beyond the built-in Protection. Enabling time-of-click protection, or impersonation protection, for example, to add extra layers or fill gaps missing from your non-Microsoft protection. If you have [Exchange mail flow rules (transport rules) that bypass spam filtering](/en-us/exchange/security-and-compliance/mail-flow-rules/use-rules-to-set-scl) (SCL -1) or [IP Allow List entries in the connection filter policy](../connection-filter-policies-configure), you need to address these overrides before turning on other protection features.

To learn more, see [Anti-phishing policies](../anti-phishing-policies-about)

- If your current security provider is configured to modify messages *in any way*, it's important to note that authentication signals can affect the ability for Defender for Office 365 to protect you against attacks such as spoofing. If your non-Microsoft service supports Authenticated Received Chain (ARC), we highly recommend enabling ARC in your journey to advanced dual filtering. Moving any message modification configuration to Defender for Office 365 is also an alternative.

    To learn more, see [Configure trusted ARC sealers](../email-authentication-arc-configure)
- Enhanced Filtering for connectors allows IP address and sender information to be preserved through the non-Microsoft service. Enhanced Filtering for connectors improves the accuracy of Microsoft Defender for Office 365 filtering, post-breach capabilities, and authentication analysis.

    To learn more, see [Enhanced filtering for connectors in Exchange Online](/en-us/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/enhanced-filtering-for-connectors)
- Priority account protection offers enhanced visibility for accounts in tooling, along with additional protection when in an advanced defense in-depth configuration state.

    To learn more, see [Manage and monitor priority accounts](/en-us/microsoft-365/admin/security-and-compliance/priority-accounts)
- Advanced Delivery should be configured to deliver any non-Microsoft phish simulations correctly, and if you have a Security Operations mailbox, consider defining it as a SecOps mailbox to ensure emails *don't* get removed from the mailbox due to threats.

    To learn more, see [Advanced delivery](../advanced-delivery-policy-configure)
- You can configure user reported settings to allow users to report good or bad messages to Microsoft, to a designated reporting mailbox (to integrate with current security workflows) or both using the built-in **Report** button in [supported versions of Outlook](../submissions-outlook-report-messages#use-the-built-in-report-button-in-outlook) or using [supported non-Microsoft solutions](../submissions-user-reported-messages-custom-mailbox#options-for-non-microsoft-reporting-tools). Admins can use the **User reported** tab on the **Submissions** page to triage false positives and false negative user reported messages. In organizations with Defender for Office 365 Plan 2 and Security Copilot, the [Phishing Triage Agent](/en-us/defender-xdr/phishing-triage-agent) can autonomously triage and classify user-reported phishing emails.

    Tip

    In [attack simulation training in Defender for Office 365 Plan 2](../attack-simulation-training-get-started), simulation messages reported by non-Microsoft tools aren't captured in attack simulation reports.

    To learn more, see [User reported settings](../submissions-user-reported-messages-custom-mailbox) and [Report phishing and suspicious emails in Outlook for admins](../submissions-outlook-report-messages)

### Use education features to improve user awareness

Education features help users recognize and respond to threats before real attacks occur.

- Attack simulation training allows you to run realistic but benign cyber-attack scenarios in your organization. If you don't already have phishing simulation capabilities from your primary email security provider, Microsoft's simulated attacks can help you identify and find vulnerable users, policies, and practices. Attack simulation training provides important knowledge to have and correct *before* a real attack impacts your organization. Post simulation we assign in product or custom training to educate users about the threats they missed, ultimately reducing your organization's risk profile. With Attack simulation training, we deliver messages directly into the inbox, so the user experience is rich. Because Attack simulation training delivers messages directly into the inbox, no security changes such as overrides are needed to get simulations delivered correctly.

To learn more, see [Get started using Attack simulation.](../attack-simulation-training-get-started)

To get started delivering a simulation, see [How to setup automated attacks and training within Attack simulation training](how-to-setup-attack-simulation-training-for-automated-attacks-and-training)

## Step 3 and beyond: Become a dual-use hero

For dual-use Defender for Office 365 deployments alongside non-Microsoft email filtering, continue with these ongoing operational practices.

- Your security teams should repeat many of the detection, investigation, response, and hunting activities described in the [Security Operations Guide for Defender for Office 365](../mdo-sec-ops-guide). The Security Operations Guide offers a detailed description of recommended tasks, cadence, and team assignments.

    To learn more, see [Security Operations Guide for Defender for Office 365](../mdo-sec-ops-guide)
- Consider user experiences such as accessing multiple quarantines, or the submission / reporting of false positives and false negatives. You can mark messages detected by the non-Microsoft service with a custom *X* header. For example, you can use mail flow rules to detect and quarantine email that contains the *X* header. Quarantining messages identified by the custom *X* header also gives users a single place to access quarantined mail.

    \*To learn more, see [How to configure quarantine permissions and policies](how-to-configure-quarantine-permissions-with-quarantine-policies)
- The [Migrate from a non-Microsoft protection service to Microsoft Defender for Office 365](../migrate-to-defender-for-office-365) guide contains useful guidance on preparing and tuning your environment for a migration. Many of the steps in that guide are *also* applicable to a dual-use scenario. Ignore the MX switch guidance in that guide, because you're maintaining a dual-use configuration rather than fully migrating.

    To learn more, see [Migrate from a non-Microsoft protection service to Microsoft Defender for Office 365](../migrate-to-defender-for-office-365)