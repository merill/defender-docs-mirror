---
layout: Conceptual
title: Collaborate with Experts on Demand using Ask Defender Experts - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/defender-experts/defender-experts-hunting-ask-experts
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
ms.reviewer: 
description: Select Ask Defender Experts directly inside the Microsoft Defender security portal to get swift and accurate responses to all your threat hunting questions.
search.product: Windows 10
ms.service: defender-experts-for-hunting
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: security
ms.author: pauloliveria
author: poliveria
ms.custom:
- msecd-doc-authoring-1015
- cx-ti
- cx-ean
- sfi-image-nochange
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- essentials-manage
ms.topic: how-to
search.appverid: met150
ms.date: 2026-07-20T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: c7cbde87-4001-505d-935a-dc33c3e7b80b
document_version_independent_id: c7cbde87-4001-505d-935a-dc33c3e7b80b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/defender-experts/defender-experts-hunting-ask-experts.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-experts/defender-experts-hunting-ask-experts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/defender-experts/defender-experts-hunting-ask-experts.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 9e0c3ac0-c932-dae7-a6b5-8bb47e7ccdeb
---

# Collaborate with Experts on Demand using Ask Defender Experts - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- [Microsoft Defender](../microsoft-365-defender)

Note

Ask Defender Experts is included in your Defender Experts Hunting subscription with [quarterly allocations](defender-experts-hunting-prerequisites#eligibility-and-licensing).

Select **Ask Defender Experts** directly inside the Microsoft 365 security portal to get swift and accurate responses to all your threat hunting questions. Experts can provide insight to better understand the complex threats your organization might face. Ask Defender Experts can help:

- Gather additional information on alerts and incidents, including root causes and scope
- Gain clarity into suspicious devices, alerts, or incidents and take next steps if faced with an advanced attacker
- Determine risks and available protections related to threat actors, campaigns, or emerging attacker techniques

This article explains how to access Ask Defender Experts in the Microsoft Defender portal, the permissions you need, the types of questions you can ask, and where to view expert responses.

[![Screenshot of the Ask Defender Experts dialog box.](media/experts-on-demand/ask-defender-expert-dialog.png)](media/experts-on-demand/ask-defender-expert-dialog.png#lightbox)

## Required permissions for using Ask Defender Experts

To view and submit inquiries to Defender experts, select one of the following Microsoft Entra ID roles.

| Microsoft Entra ID role | Permission level |
| --- | --- |
| Global Reader | Read inquiries |
| Security Admin, Security Operator, or Security Reader | Read and submit inquiries |

To learn more about how Microsoft Entra ID roles map to Microsoft Defender unified RBAC permissions, see [Microsoft Entra Global roles access](../compare-rbac-roles#microsoft-entra-global-roles-access).

Microsoft Threat Experts customers using Ask Defender Experts can also use the following permissions from [Microsoft Defender unified RBAC](../custom-permissions-details).

| Microsoft Defender unified RBAC role | Permission level |
| --- | --- |
| Security data basics | Read |
| Alerts, Response | Read and submit |

## Where to submit inquiries to Ask Defender Experts

You can find the **Ask Defender Experts** option in several places throughout the portal:

- **Device page actions menu**:

    [![Screenshot of the Ask Defender Experts menu option in the Device page action menu in the Microsoft Defender portal.](media/experts-on-demand/device-page-actions-menu.png)](media/experts-on-demand/device-page-actions-menu.png#lightbox)
- **Device inventory page flyout menu**:

    [![Screenshot of the Ask Defender Experts menu option in the Device inventory page flyout menu in the Microsoft Defender portal.](media/experts-on-demand/device-inventory-flyout-menu.png)](media/experts-on-demand/device-inventory-flyout-menu.png#lightbox)
- **Alerts page flyout menu**:

    [![Screenshot of the Ask Defender Experts menu option in the Alerts page flyout menu in the Microsoft Defender portal.](media/alerts-flyout-menu.png)](media/alerts-flyout-menu.png#lightbox)
- **Incidents page actions menu**:

    [![Screenshot of the Ask Defender Experts menu option in the Incidents page actions menu in the Microsoft Defender portal.](media/incidents-page-actions-menu.png)](media/incidents-page-actions-menu.png#lightbox)
- **Defender Experts overview page**:

    [![Screenshot of the Ask Defender Experts option on the Defender Experts overview page in the Microsoft Defender portal.](media/defender-experts-hunting-ask-experts/ade-overview-page-final.png)](media/defender-experts-hunting-ask-experts/ade-overview-page-final.png#lightbox)
- **Defender Experts message center**:

    [![Screenshot of the Ask Defender Experts option in the Defender Experts message center in the Microsoft Defender portal.](media/defender-experts-hunting-ask-experts/ade-message-center.png)](media/defender-experts-hunting-ask-experts/ade-message-center.png#lightbox)

## Where to view responses from Defender Experts

You can view Defender Experts responses either in the Microsoft Defender portal or through email notifications.

### View Defender Experts responses in the portal

You can view responses to inquiries you submitted to Ask Defender Experts from up to six months ago by going to **Reports** &gt; **Defender Experts messages**. You can also ask follow-up questions or reply with more information to Defender Experts from this page.

[![Screenshot of in-portal managed response.](media/experts-on-demand/inportal-managed-response.png)](media/experts-on-demand/inportal-managed-response.png#lightbox)

### View Defender Experts responses by email

If you include contact email addresses when you submit your inquiry, they receive an email notification when Defender Experts posts a response.

[![Screenshot of email based managed response.](media/experts-on-demand/email-based-managed-response.png)](media/experts-on-demand/email-based-managed-response.png#lightbox)

## Sample questions you can ask from Defender Experts

The following examples show the kinds of questions you can submit to Defender Experts, grouped by scenario.

### Questions about alert information

Examples of alert-related questions include the following:

- We saw a new type of alert for a living-off-the-land binary. We can provide the alert ID. Can you tell us more about this alert and if it's related to any incident and how we can investigate it further?
- We've observed two similar attacks, which both try to execute malicious PowerShell scripts but generate different alerts. One is "Suspicious PowerShell command line" and the other is "A malicious file was detected based on indication provided by Office 365." What is the difference?
- We received an odd alert today about an abnormal number of failed logins from a high profile user's device. We can't find any further evidence for these attempts. How can Microsoft Defender see these attempts? What type of logins are being monitored?
- Can you give more context or insight about the alert and any related incidents, "Suspicious behavior by a system utility was observed"?
- I observed an alert titled "Creation of forwarding/redirect rule". I believe the activity is benign. Can you tell me why I received an alert?

### Questions about possible device compromise

Examples of device-compromise questions include the following:

- Can you help explain why we see a message or alert for "Unknown process observed" on many devices in our organization? We appreciate any input to clarify whether this message or alert is related to malicious activity or incidents.
- Can you help validate a possible compromise on the following system, dating from last week? It's behaving similarly as a previous malware detection on the same system six months ago.

### Questions about threat intelligence details

You can ask Defender Experts questions like the following about threat intelligence:

- We detected a phishing email that delivered a malicious Word document to a user. The document caused a series of suspicious events, which triggered multiple alerts for a particular malware family. Do you have any information on this malware? If yes, can you send us a link?
- We recently saw a blog post about a threat that is targeting our industry. Can you help us understand what protection Microsoft Defender provides against this threat actor?
- We recently observed a phishing campaign conducted against our organization. Can you tell us if this was targeted specifically to our company or vertical?

### Questions about Defender Experts Hunting alert communications

The following are examples of questions related to Defender Experts Hunting notifications:

- Can your incident response team help us address the Defender Experts Notification that we got?
- We received this Defender Experts Notification from Microsoft Defender Experts Hunting. We don't have our own incident response team. What can we do now, and how can we contain the incident?
- We received a Defender Experts Notification from Microsoft Defender Experts Hunting. What data can you provide to us that we can pass on to our incident response team?

## Services that aren't in scope for Defender Experts

Ask Defender Experts is focused on products that are only included in Microsoft Defender, that is, Microsoft Defender for Endpoint, Microsoft Defender for Office, Microsoft Defender for Cloud Apps, and Microsoft Defender for Identity.

Ask Defender Experts doesn't cover the following scenarios:

- **Inquiries related to custom detections**- Inquiries related to custom detections in the above products can't be handled in Ask Defender Experts because our experts typically don't have access to such telemetry or visibility into how these custom policies were set up. Examples of such policies include:

    - **Alerts with policy source** = **Custom**
    - **Detection source** = **Custom TI**
    - **Alert title** = **Anomaly Indicator**
    - **Threat family** = **Custom Enterprise Block Only**
- **Inquiries related to non-Microsoft Defender XDR products**- Defender Experts don't handle inquiries on non-Defender XDR products such as Microsoft Defender for Cloud, Microsoft Defender for IoT, Microsoft Sentinel, Microsoft Purview, Microsoft Priva, and other third-party cybersecurity products.
- **Inquiries regarding bugs**- Defender Experts don't handle inquiries regarding bugs in your product experience in the Microsoft Defender portal, such as, missing data on the alert or incident page or a recommended action not completing when you action it. You can reach out to Microsoft Support via the [Services Hub](https://serviceshub.microsoft.com/home) regarding such issues.
- **Inquiries related to security incident response issues**- Ask Defender Experts isn't a security incident response service. It's intended to provide a better understanding of complex threats affecting your organization. Engage with your own security incident response team to address urgent security incident response issues. If you don't have your own security incident response team and would like Microsoft's help, create a support request in the [Premier Services Hub](/en-us/services-hub/).

### Next step

After you submit inquiries and review responses, learn how to interpret the findings that Defender Experts provide in their reports.

For more information, see the following resource:

- [Understand the Defender Experts Hunting report in Microsoft Defender](defender-experts-hunting-report)

Tip

Do you want to learn more? Engage with the Microsoft Security community in our Tech Community: [Microsoft Defender XDR Tech Community](https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection).