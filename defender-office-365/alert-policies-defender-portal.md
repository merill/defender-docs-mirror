---
layout: Conceptual
title: Alert policies in the Microsoft Defender portal - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/alert-policies-defender-portal
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: how-to
ms.collection:
- m365-security
- tier2
ms.localizationpriority: medium
ms.assetid: 
ms.custom:
- msecd-doc-authoring-1016
- seo-marvel-apr2020
- sfi-ga-nochange
description: Admins can use the Alert policy page in the Microsoft Defender portal to view and create alert policies to trigger alerts when the specified actions occur.
ms.service: defender-office-365
ms.date: 2026-07-03T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 97a89b5a-0be5-e59c-72b5-2a4907337c33
document_version_independent_id: 97a89b5a-0be5-e59c-72b5-2a4907337c33
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/alert-policies-defender-portal.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: alert-policies-defender-portal
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/alert-policies-defender-portal.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: abb753d2-0fcc-3bd8-eaf3-23ae628c6d41
---

# Alert policies in the Microsoft Defender portal - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

In organizations with cloud mailboxes, alert policies generate alerts in the alert dashboard when users take actions that match the conditions of the policy. There are many default alert policies that help you monitor activities. For example, default alert policies can monitor assigning admin privileges in Exchange Online, malware attacks, phishing campaigns, and unusual levels of file deletions and external sharing.

This article explains how to view and create alert policies on the **Alert policy** page in the Microsoft Defender portal. Before you begin, review the prerequisites for required permissions.

## What do you need to know before you begin?

Review the following prerequisites before you view or manage alert policies.

- You need to be assigned permissions before you can view or manage alert policies. You have the following options:

    - [Microsoft Defender XDR Unified role based access control (RBAC)](/en-us/defender-xdr/manage-rbac) (If **Email & collaboration** &gt; **Defender for Office 365** permissions is ![](media/scc-toggle-on.png)**Active**. Affects the Defender portal only, not PowerShell):

        - *Read only access to the Alert policies page*: **Security operations / Security data / Security data basics (read)**.
        - *Manage alert policies*: **Authorization and settings / Security settings / Detection tuning (manage)**.
    - [Email & collaboration permissions in the Microsoft Defender portal](mdo-portal-permissions):

        - *Create and manage alert policies in the Threat management category*: Membership in the **Organization Management** or **Security Administrator** role groups.
        - *View alerts in the Threat management* category: Membership in the **Security Reader** role group.
    - [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Membership in the **Global Administrator**^\*^, **Security Administrator**, or **Security Reader** roles gives users the required permissions and permissions for other features in Microsoft 365.

        Important

        ^\*^ Microsoft strongly advocates for the principle of least privilege. Assigning accounts only the minimum permissions necessary to perform their tasks helps reduce security risks and strengthens your organization's overall protection. Global Administrator is a highly privileged role that you should limit to emergency scenarios or when you can't use a different role.
- For information about other alert policy categories, see [Permissions required to view alerts](/en-us/defender-xdr/alert-policies#rbac-permissions-required-to-view-alerts).

## Built-in alert tuning rules

Microsoft Defender includes built-in alert tuning rules that help reduce reporting noise from common benign activity. These built-in rules suppress alerts without affecting other features like AIR investigations and email notifications. If the AIR investigation detects malicious or suspicious activity, the new alert is reactivated.

To see the built-in alert tuning rules in the [Microsoft Defender portal](https://security.microsoft.com), go to **System** &gt; **Settings** &gt; **Microsoft Defender XDR** &gt; **Rules** section &gt; **Alert tuning** or directly on the **Alert tuning** page at https://security.microsoft.com/securitysettings/defender/alert_suppression.

Be sure to review these rules to understand how they might affect which alerts appear in the Microsoft Defender portal.

Important

Built-in alert tuning rules don't apply to alerts from [custom detection rules](/en-us/defender-xdr/custom-detections-overview) and [Custom TI](/en-us/defender-endpoint/indicators-overview).

Note

The [Microsoft Security Copilot Phishing Triage Agent](/en-us/defender-xdr/phishing-triage-agent) doesn't classify alerts suppressed by [alert tuning](/en-us/defender-xdr/investigate-alerts#tune-an-alert). Be sure to disable the **Auto-Resolve - Email reported by user as malware or phish** built-in alert tuning rule and any custom tuning rules that suppress this alert.

## Open alert policies

In the Microsoft Defender portal at https://security.microsoft.com, go to **Email & collaboration** &gt; **Policies & rules** &gt; **Alert policy**. Or, to go directly to the **Alert policy** page, use https://security.microsoft.com/alertpoliciesv2.

On the **Alert policy** page, you can view and create alert policies. For more information, see [Alert policies in Microsoft 365](/en-us/defender-xdr/alert-policies)