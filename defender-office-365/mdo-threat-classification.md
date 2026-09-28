---
layout: Conceptual
title: Threat classification in Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/mdo-threat-classification
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.topic: overview
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
description: Admins can learn about threat classification in Microsoft Defender for Office 365.
ms.service: defender-office-365
ms.date: 2025-04-08T00:00:00.0000000Z
locale: en-us
document_id: bf7ad7b6-f121-73dc-6bf2-c5815711ddcc
document_version_independent_id: bf7ad7b6-f121-73dc-6bf2-c5815711ddcc
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/mdo-threat-classification.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdo-threat-classification
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/mdo-threat-classification.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c6f99e62-1cf6-4b71-af9b-649b05f80cce
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3f56b378-07a9-4fa1-afe8-9889fdc77628
platformId: 945f2ceb-59f1-4431-9659-5c87cc1497c3
---

# Threat classification in Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn

Effective threat classification is a crucial component of cybersecurity that enables organizations to quickly identify, assess, and mitigate potential risks. The threat classification system in Microsoft Defender for Office 365 uses advanced technologies such as large language models (LLMs), small language models (SLMs), and machine learning (ML) models to automatically detect and classify email-based threats. These models work together to provide comprehensive, scalable, and adaptive threat classification, helping security teams stay ahead of emerging attacks.

By categorizing email threats into specific types, such as phishing, malware, and business email compromise (BEC), our system provides organizations with actionable insights to protect against malicious activities.

## Threat types

*Threat type* refers to the primary categorization of a threat based on fundamental characteristics or attack method. Historically, these broad categories are identified early in the attack lifecycle and help organizations understand the nature of the attack. Common threat types include:

- **Phishing**: Attackers impersonate trusted entities to deceive recipients into revealing sensitive information such as sign in credentials or financial data.
- **Malware**: Malicious software designed to damage or exploit systems, networks, or devices.
- **Spam**: Unsolicited, often irrelevant email sent in bulk, typically for malicious or promotional purposes.

## Threat detections

*Threat detections* refer to the technologies and methodologies that are used to identify specific indicators or suspicious activities within an email message or communication. Threat detections help spot the presence of threats by identifying anomalies or characteristics in the message. Common threat detections include:

- **Spoof**: Identifies when the sender's email address is forged to look like a trusted source.
- **Impersonation**: Detects when an email message impersonates a legitimate entity, such as an executive or trusted business partner, to trick recipients into taking harmful actions.
- **URL reputation**: Assesses the reputation of URLs included in an email to determine if they lead to malicious websites.
- **Other filters**

## Threat classification

*Threat classification* is the process of categorizing a threat based on intent and the specific nature of the attack. The threat classification system uses LLMs, ML models, and other advanced techniques to understand the intent behind threats and provide a more accurate classification. As the system evolves, you can expect new threat classifications to keep pace with emerging attack methods.

Currently available threat classes are described in the following list:

- **Advance fee scam**: Victims are promised large financial rewards, contracts, or prizes in exchange for upfront payments or a series of payments, which the attacker never delivers.
- **Adware**: A program that displays an advertisement that is out of context
- **Business intelligence**: Requests for information regarding vendors or invoices, which are used by attackers to build a profile for further targeted attacks, often from a look-alike domain that mimics a trusted source.
- **Contact establishment**: Email messages (often generic text) to verify whether an inbox is active and to initiate a conversation. These messages aim to bypass security filters and build a trusted reputation for malicious future messages.
- **Downloader**: A trojan that downloads other malware.
- **Gift cards**: Attackers impersonate trusted individuals or organizations, convincing the recipient to purchase and send gift card codes, often using social engineering tactics.
- **HackTool**: Tools that are used for hacking.
- **Invoice fraud**: Invoices that look legitimate, either by altering details of an existing invoice or submitting a fraudulent invoice, with the intent to trick recipients into making payments to the attacker.
- **Payroll fraud**: Manipulate users into updating payroll or personal account details to divert funds into the attacker's control.
- **Personally identifiable information (PII) gathering**: Attackers impersonate a high-ranking individual, such as a CEO, to request personal information. These email messages are often followed by a shift to external communication channels like WhatsApp or text messages to evade detection.
- **Ransom**: Software (often called ransomware) that prevents users from using or accessing their PC, usually for malicious purposes. The software might take the following actions:

    - Require users to pay (the ransom).
    - Encrypt files and other data.
    - Require users to do activities like answering surveys or CAPTCHAS to regain access to the machine.

        Commonly, users can't move input device focus out of the ransomware, and users can't easily end the malicious process. In some cases, the ransomware denies PC access to users, even after a reboot or booting into Safe Mode.
- **Remote Access Trojan**: Software that gives attackers unauthorized remote access and control of infected computers. Bots are a subcategory of backdoor trojans.
- **Spyware**: Software that can steal information from an affected user beyond passwords.
- **Task fraud**: Short, seemingly safe email messages asking for assistance with a specific task. These requests are designed to gather information or induce actions that can compromise security.

## Where threat classification results are available

The results of threat classification are available in the following experiences in Defender for Office 365:

- [Explorer (Threat Explorer)](threat-explorer-real-time-detections-about)
- [Incidents and alerts](mdo-sec-ops-manage-incidents-and-alerts)
- [Advanced hunting](/en-us/defender-xdr/advanced-hunting-overview)
- The [Threat protection status report](reports-email-security#view-data-by-email--phish-and-chart-breakdown-by-threat-classification-defender-for-office-365)
- The [Mailflow status report](reports-email-security#mailflow-view-for-the-mailflow-status-report)