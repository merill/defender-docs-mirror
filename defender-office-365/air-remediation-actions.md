---
layout: Conceptual
title: Remediation actions from AIR - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/air-remediation-actions
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: article
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
description: Learn about calculated and recommended remediation actions in automated investigation and response (AIR) in Microsoft Defender for Office 365 Plan 2.
ms.date: 2024-07-10T00:00:00.0000000Z
ms.custom:
- air
ms.service: defender-office-365
locale: en-us
document_id: 4e92cf96-e2a1-3662-597d-494ca4c75782
document_version_independent_id: 4e92cf96-e2a1-3662-597d-494ca4c75782
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/air-remediation-actions.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: air-remediation-actions
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/air-remediation-actions.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 7d452b48-56b1-74d6-9326-97671ca46fbd
---

# Remediation actions from AIR - Microsoft Defender for Office 365 | Microsoft Learn

Tip

*Did you know you can try the features in Microsoft Defender for Office 365 Plan 2 for free?* Use the 90-day Defender for Office 365 trial at the [Microsoft Defender portal trials hub](https://security.microsoft.com/trialHorizontalHub?sku=MDO&amp;ref=DocsRef). Learn about who can sign up and trial terms on [Try Microsoft Defender for Office 365](/en-us/defender-office-365/try-microsoft-defender-for-office-365).

[Automated investigation and response (AIR) in Microsoft Defender for Office 365 Plan 2](air-about) often results in remediation actions that require [approval](air-review-approve-pending-completed-actions) from you security operations (SecOps) team.

In some cases, AIR doesn't result in specific remediation actions. To further investigate and take appropriate actions, use the guidance in the following table.

| Category | Threat/risk | Remediation actions |
| --- | --- | --- |
| Email | Malware | Soft delete email/cluster.  If more than a handful of related messages contain malware, the entire cluster is considered to be malicious. |
| Email | A malicious URL was detected by [Safe Links](safe-links-about). | Soft delete email/cluster.  Block URL at time-of-click.  The message that contains a malicious URL is considered to be malicious. |
| Email | Phishing | Soft delete email/cluster.  If more than a handful of related messages contain phishing attempts, the entire cluster is considered to be a phishing attempt. |
| Email | Phishing email delivered and then [removed by zero-hour auto purge (ZAP)](zero-hour-auto-purge).) | Soft delete email/cluster.  To see if ZAP removed a message, see [How to see if ZAP moved your message](zero-hour-auto-purge#how-to-see-if-zap-moved-your-message). |
| Email | [User reported phishing email](submissions-submit-files-to-microsoft) | [Automated investigation triggered by the user's report](air-examples#example-a-user-reported-phishing-message-launches-an-investigation-playbook) |
| Email | Volume anomaly (recent email quantities exceed the previous 7-10 days for matching criteria). | No specific pending actions from AIR.  A volume anomaly isn't a clear threat. Although a high volume of email can indicate potential issues, confirmation is required in terms of either malicious verdicts or a manual review of email messages/clusters. For more information, see [Find suspicious email that was delivered](threat-explorer-investigate-delivered-malicious-email#find-suspicious-email-that-was-delivered). |
| Email | No threats found (the system found no threats based on files, URLs, or analysis of email cluster verdicts). | No specific pending actions from AIR.  Threats found and [removed by ZAP](zero-hour-auto-purge) after a completed investigation aren't reflected in an investigation's numerical results, but such threats are viewable in [Threat Explorer](threat-explorer-real-time-detections-about). |
| User | A user clicked a malicious URL (a user visited a page that was later found to be malicious, or bypassed a [Safe Links warning page](safe-links-about#warning-pages-from-safe-links) to get to a malicious page.) | No specific pending actions from AIR.  Block URL at time-of-click.  Use Threat Explorer to [view data about URLs and click verdicts](threat-explorer-real-time-detections-about#click-verdict-pivot-for-the-url-clicks-view-for-the-details-area-of-the-all-email-view-in-threat-explorer).  If your organization is using [Microsoft Defender for Endpoint](/en-us/windows/security/threat-protection/), consider [investigating the user](/en-us/defender-endpoint/investigate-user) to determine if their account is compromised. |
| User | User sending malware/phishing messages | No specific pending actions from AIR.  The user might be reporting malware/phishing messages, or someone could be [spoofing the user](anti-phishing-protection-spoofing-about) as part of an attack. Use [Threat Explorer](threat-explorer-real-time-detections-about) to view and handle email containing [malware](threat-explorer-real-time-detections-about#malware-view-in-threat-explorer-and-real-time-detections) or [phishing](threat-explorer-real-time-detections-about#phish-view-in-threat-explorer-and-real-time-detections). |
| User | Automatic external email forwarding ([SMTP forwarding](/en-us/exchange/recipients-in-exchange-online/manage-user-mailboxes/configure-email-forwarding), Inbox rules, or Exchange mail flow rules (also known as transport rules) could be used for data exfiltration). | Remove the forwarding rule or configuration.  Use the [Autoforwarded messages report](/en-us/exchange/monitoring/mail-flow-reports/mfr-auto-forwarded-messages-report) to view specific details about forwarded email. |
| User | Email delegation (an account has delegations set up). | Remove delegations.  If your organization is using [Defender for Endpoint](/en-us/windows/security/threat-protection/), consider [investigating the user](/en-us/defender-endpoint/investigate-user) with the delegation permission. |
| User | Data exfiltration (a user violated email or file-sharing [DLP policies](/en-us/purview/dlp-learn-about-dlp)). | AIR doesn't result in a specific pending action. [Get started with Activity Explorer](/en-us/purview/data-classification-activity-explorer#get-started-with-activity-explorer). |
| User | Anomalous email sending (a user recently sent more email than during the previous 7-10 days.) | No specific pending actions from AIR.  Sending a large volume of email isn't necessarily malicious (for example, the user might have sent email to a large group of recipients for an event). To investigate, use the [New users forwarding email insight](/en-us/exchange/monitoring/mail-flow-insights/mfi-new-users-forwarding-email-insight) and [Outbound message report](/en-us/exchange/monitoring/mail-flow-reports/mfr-inbound-messages-and-outbound-messages-reports) in the Exchange admin center (EAC). |