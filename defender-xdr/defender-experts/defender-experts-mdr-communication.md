---
layout: Conceptual
title: Communicating with Microsoft Defender Experts - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/defender-experts/defender-experts-mdr-communication
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
ms.reviewer: 
description: The Defender Experts service has multiple channels to discuss incidents, managed response, and service support.
ms.service: defender-experts-for-xdr
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- essentials-manage
ms.topic: concept-article
ms.custom:
- cx-ti
- cx-dex
ms.date: 2026-07-29T00:00:00.0000000Z
ai-usage: ai-assisted
locale: en-us
document_id: 478700f9-ee1e-bac7-57ed-50e51b70fecd
document_version_independent_id: 478700f9-ee1e-bac7-57ed-50e51b70fecd
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/defender-experts/defender-experts-mdr-communication.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-experts/defender-experts-mdr-communication
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/defender-experts/defender-experts-mdr-communication.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 52b0c24c-5bd2-88df-55c2-d43af92e8adf
---

# Communicating with Microsoft Defender Experts - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- [Microsoft Defender Experts MDR](defender-experts-mdr-overview)
- [Microsoft Defender Experts for Servers](defender-experts-servers-overview)

The Microsoft Defender Experts service provides you with multiple channels of communication to discuss incidents with our experts, ask them questions on demand, or get service readiness or operations support from your Security Delivery Experts (SDXs), if included in your service.

## Incident and managed response notifications

When an incident requires your attention, such as the incidents our experts issue [managed response actions](defender-experts-mdr-managed-response), you receive notifications through one or more of the following channels:

### In-portal chat

Note

The chat option is only available for incidents where the experts issued managed response.

The **Chat** tab within the Microsoft Defender portal provides a space to engage with experts and further understand the incident, the investigation, and the required actions. You can ask about a malicious executable, malicious attachment, information about activity groups, advanced hunting queries, or any other information that would assist you with the incident resolution.

[![Screenshot of managed response in-portal chat.](media/communicate-defender-experts-xdr/in-portal-xdr-chat.png)](media/communicate-defender-experts-xdr/in-portal-xdr-chat.png#lightbox)

Defender Experts-trained AI sometimes posts on behalf of the experts to respond to your messages more quickly (for example, to acknowledge your message that your SOC team is still working on remediation actions). Its messages show up as coming from *Defender Experts virtual assistant*.

You can also translate the chat messages to another language by selecting the **Translate messages** icon ![](media/communicate-defender-experts-xdr/translate-messages-icon.png) on the upper-right corner of the chat window. This feature uses AI to support English, Spanish, Japanese, and Portuguese (Brazil and Portugal) translations.

To leave feedback about your chat experience, select the **thumbs up** or **thumbs down** icon at the top of the chat window.

### Teams chat

Apart from using the in-portal chat, you can also engage in real-time chat conversations with Defender Experts directly within Microsoft Teams. This capability provides you and your security operations center (SOC) team more flexibility when responding to incidents that require managed response. [Learn more about turning on notifications and chat on Teams](defender-experts-mdr-get-started#receive-managed-response-notifications-and-updates-in-microsoft-teams).

Once you turn on chat on Teams, a new team named **Defender Experts team** is created and the Defender Experts Teams app is installed in it. Each incident that requires your attention is posted on this team's **Managed response** channel as a new post. To engage with our experts (for example, ask follow-up questions about the investigation summary or actions published by Defender Experts), use the **Reply** text bar and type your message. If you have issues setting up the Defender Experts channel or tagging @*Defender Experts*, see [troubleshooting Defender Experts app permissions in Microsoft Teams](defender-experts-teams-app-permissions).

[![Screenshot of managed response teams channel.](media/communicate-defender-experts-xdr/teams-chat-managed-response-01.png)](media/communicate-defender-experts-xdr/teams-chat-managed-response-01.png#lightbox)

**Important reminders when using the Teams chat:**

- Our experts have access to messages in **Defender Experts team** through the Defender Experts Teams app so you don't have to explicitly add them to this team.
- Our experts only see replies to existing posts created by Defender Experts regarding a managed response. If you create a new post, our experts can't see it.
- While Defender Experts might have access to all messages in any channel in **Defender Experts team**, type a message in your replies so they're notified to join the chat conversation.
- Don't attach any attachments (for example, files for analysis) in the chat. For security reasons, Defender Experts can't view the attachments. Instead, send them to appropriate submissions channels or provide links where they can be found in Microsoft Defender portal.
- Conversations in the Teams chat about an incident are also synchronized with the incident's **Chat** tab in the Microsoft Defender portal so that you can see messages and updates about an investigation wherever you go.

### Email

The Defender Experts service typically sends automated emails whenever a managed response with completed or pending actions is published in the Microsoft Defender portal, or when it needs to remind you about incidents awaiting your action.

However, our experts can also send emails to your identified notification contacts directly during any of the following situations:

- When they need additional information or context to investigate an incident
- When they detect a malicious or suspicious activity manually and outside of incidents or alerts in the Microsoft Defender portal, and it requires a response action
- When they reply to the requests or queries sent to them through email

Important

Remember to verify emails claiming to be from Defender Experts.

### Phone call

In break-glass scenarios or matters that require immediate attention (for example, malware on high-value infrastructure, ransomware, data exfiltration, insider threat, or other signs of a determined human adversary), the experts reach out to your identified **incident notification contacts** by using the details you provided, including calling their listed phone numbers. [Learn more about adding contact persons or groups for incident notifications](defender-experts-mdr-get-started#tell-us-who-to-contact-for-important-matters).

## Ask Defender Experts

While the previous scenarios involve the experts initiating communication with you, you can also request advanced threat expertise on demand by selecting **Ask Defender Experts** directly inside the Microsoft Defender portal. [Learn more](defender-experts-hunting-ask-experts).

## Collaborating with your Security Delivery Expert

The Security Delivery Expert (SDX) is responsible for managing the overall relationship for your organization with the Defender Experts MDR service. They are your trusted advisor working along with XDR experts' team to help you protect your organization.

Note

Security Delivery Experts are included if your Defender Experts service is licensed for 1,500 or more seats.

The SDX provides the following services:

- Service readiness support
    - Educate customers about the end-to-end service experience, from signup to regular operations and escalation process.
    - Help establish a service-ready security posture, including guidance on required controls and policy updates.
- Service operations support
    - Provide tailored service delivery content and reporting, including periodic business reviews.
    - Serve as a single point of contact for feedback and escalations related to Defender Experts Service.

The SDX engages with your identified **service review contacts**. [Learn more about adding contact persons or groups for service review and delivery](defender-experts-mdr-get-started#tell-us-who-to-contact-for-important-matters).

### See also

- [Get started with Microsoft Defender Experts MDR](defender-experts-mdr-get-started)
- [Managed detection and response](defender-experts-mdr-managed-response)
- [Get real-time visibility with Defender Experts reports](defender-experts-mdr-reports)

Tip

Do you want to learn more? Engage with the Microsoft Security community in our Tech Community: [Microsoft Defender XDR Tech Community](https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection).