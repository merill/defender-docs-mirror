---
layout: Conceptual
title: Automated investigation and response in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/air-about
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: article
ms.date: 2026-05-12T00:00:00.0000000Z
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
description: Learn how automated investigation and response (AIR) in Microsoft Defender for Office 365 Plan 2 helps your security team identify and remediate threats efficiently.
ms.custom:
- air
- seo-marvel-mar2020
- msecd-doc-authoring-1012
- sfi-ga-nochange
ms.service: defender-office-365
locale: en-us
document_id: ec49ac58-f018-207c-06da-370f85fbbf80
document_version_independent_id: ec49ac58-f018-207c-06da-370f85fbbf80
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/air-about.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: air-about
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/air-about.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 00f72224-daf2-945d-25c8-80548b08c90d
---

# Automated investigation and response in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

As [security alerts](/en-us/defender-xdr/investigate-alerts) appear in a Microsoft 365 organization at https://security.microsoft.com/alerts, it's up to the security operations (SecOps) team to review, prioritize, and respond to those alerts. Keeping up with the volume of incoming alerts can be overwhelming. Automating some of those tasks can help.

[Microsoft Defender for Office 365 Plan 2](mdo-about#defender-for-office-365-plan-2-capabilities) (included in Microsoft 365 licenses like E5 or as a standalone subscription) includes automated investigation and response (AIR) capabilities that save time and effort for SecOps teams.

AIR triages high-impact, high-volume alerts by completing organization-level investigations. AIR investigations expand on detections or provide extra analysis to determine the threat status for the organization. When AIR identifies threats, it queues threat remediation actions for SecOps personnel to approve. AIR provides the following benefits:

- Automated investigation of well-known threats without manual intervention.
- Appropriate remediation actions awaiting approval, enabling your SecOps team to respond effectively to detected threats.
- SecOps teams can focus on higher-priority tasks without losing sight of important alerts.

AIR in Defender for Office 365 Plan 2 requires that [audit logging is turned on](/en-us/purview/audit-log-enable-disable) (it's on by default).

## The overall flow of AIR

An alert is triggered, and a security playbook starts an automated investigation, which results in findings and recommended actions. Here's the overall flow of AIR, step by step:

1. An automated investigation is initiated in one of the following ways:

    - Specific alerts that are designed to initiate AIR. These alerts include:

        - Something suspicious is identified in email (for example, the message itself, an attachment, a URL, or a compromised user account).
        - [Zero-hour auto purge (ZAP)](zero-hour-auto-purge).
        - User submissions.
        - User click alerts.
        - Suspicious mailbox behavior.

            Tip

            Be sure to regularly review the alerts in your organization. For more information about alert policies that trigger automated investigations, see the [default alert policies in the Threat management category](/en-us/defender-xdr/alert-policies#threat-management-alert-policies). The entries that contain the value **Yes** for **Automated investigation** can trigger automated investigations. AIR isn't triggered when:

            - These alerts are disabled.
            - These alerts were replaced by custom alerts.
    - A security analyst manually triggers the investigation by selecting ![](media/defender-portal-icon-take-actions.png)**Take action** in Threat Explorer, Advanced hunting, custom detection, the Email entity page, or the Email summary panel. For more information, see [Threat hunting: Email remediation](threat-explorer-threat-hunting#email-remediation). For examples, see [Automated investigation and response (AIR) examples in Microsoft Defender for Office 365 Plan 2](air-examples).
2. The automated investigation evaluates and analyzes the nature of the alert, the message involved, and additional evidence surrounding the message. The scope of the investigation can increase based on the evidence uncovered and collected during the investigation.
3. During and after an automated investigation, [details and results](air-view-investigation-results) are available. Results might include [recommended actions](air-remediation-actions) for SecOps personnel to remediate the threats that were found.
4. The SecOps team reviews the [investigation results and recommendations](air-view-investigation-results) in the investigation itself, the incident, or in the Action center, and [approves or rejects the remediation actions](air-review-approve-pending-completed-actions).

    Tip

    The auto-remediation capabilities in AIR fully automate the remediation of malicious similarity clusters, including malicious URL and file clusters. For these cluster types, AIR automatically approves the pending remediation actions it generates, which eliminates the need for manual intervention and streamlines the response process for SOC teams.

    AIR also saves time by evaluating and automatically resolving alerts and incidents where no threats are found. This result is common in user submission scenarios. AIR closes the investigation if no threats are found or if the threats are in messages that were already remediated.
5. After pending remediation actions are approved or rejected, the automated investigation completes.

    The automated investigation automatically closes if no recommended actions are identified. The details of the investigation are still available on the **Investigations** page at https://security.microsoft.com/airinvestigation.

During and after each automated investigation, the SecOps team can do the following tasks:

- [View details about an alert related to an investigation](air-view-investigation-results#view-details-about-an-alert-related-to-an-investigation)
- [View the results details of an investigation](air-view-investigation-results#view-investigation-details-from-air-in-defender-for-office-365-plan-2)
- [Review and approve actions as a result of an investigation](air-review-approve-pending-completed-actions)

## Built-in alert tuning rules

Microsoft Defender includes built-in alert tuning rules that help reduce reporting noise from common benign activity. These built-in rules suppress alerts without affecting other features like AIR investigations and email notifications. If the AIR investigation detects malicious or suspicious activity, the new alert is reactivated.

To see the built-in alert tuning rules in the [Microsoft Defender portal](https://security.microsoft.com), go to **System** &gt; **Settings** &gt; **Microsoft Defender XDR** &gt; **Rules** section &gt; **Alert tuning** or directly on the **Alert tuning** page at https://security.microsoft.com/securitysettings/defender/alert_suppression.

Be sure to review these rules to understand how they might affect which alerts appear in the Microsoft Defender portal.

Important

Built-in alert tuning rules don't apply to alerts from [custom detection rules](/en-us/defender-xdr/custom-detections-overview) and [Custom TI](/en-us/defender-endpoint/indicators-overview).

Note

The [Microsoft Security Copilot Phishing Triage Agent](/en-us/defender-xdr/phishing-triage-agent) doesn't classify alerts suppressed by [alert tuning](/en-us/defender-xdr/investigate-alerts#tune-an-alert). Be sure to disable the **Auto-Resolve - Email reported by user as malware or phish** built-in alert tuning rule and any custom tuning rules that suppress this alert.

## Required permissions and licensing for AIR

You need to be assigned permissions to use AIR. You have the following options:

- [Microsoft Defender XDR Unified role-based access control (RBAC)](/en-us/defender-xdr/manage-rbac) (If **Email & collaboration** &gt; **Defender for Office 365** permissions is ![](media/scc-toggle-on.png)**Active**. Affects the Defender portal only, not PowerShell):
    - *Start an automated investigation* or *Approve or reject recommended actions*: **Security operations/Security data/Email & collaboration advanced actions (manage)**.
- [Email & collaboration permissions in the Microsoft Defender portal](mdo-portal-permissions):
    - *Set up AIR features*: Membership in the **Organization Management** or **Security Administrator** role groups.
    - *Start an automated investigation* or *Approve or reject recommended actions*:
        - Membership in the **Organization Management**, **Security Administrator**, **Security Operator**, **Security Reader**, or **Global Reader** role groups.
        - The **Search and Purge** role, which is assigned only to the **Data Investigator** or **Organization Management** role groups by default. Or you can [create a new role group](mdo-portal-permissions#create-email--collaboration-role-groups-in-the-microsoft-defender-portal) with the **Search and Purge** role assigned, and add the users to the custom role group.
- [Microsoft Entra permissions](/en-us/entra/identity/role-based-access-control/manage-roles-portal): Give users the required permissions *and*permissions for other features in Microsoft 365:
    - *Set up AIR features*: Membership in the **Global Administrator** or **Security Administrator** roles.
    - *Start an automated investigation* or *Approve or reject recommended actions*:
        - Membership in the **Global Administrator**, **Security Administrator**, **Security Operator**, **Security Reader**, or **Global Reader** roles. *and*
        - Membership in an Email & collaboration role group with the **Search and Purge** role assigned as previously described.

To use Automated Investigation and Response (AIR), you must have Microsoft Defender for Office 365 Plan 2 licenses (included with eligible subscriptions or available as an add‑on).