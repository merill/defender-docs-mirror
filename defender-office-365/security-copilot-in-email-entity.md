---
layout: Conceptual
title: Summarize Email Threats with Microsoft Security Copilot in Email Entity - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/security-copilot-in-email-entity
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: ajaj-shaikh
ms.author: ajajshaikh
ms.date: 2026-09-15T00:00:00.0000000Z
ms.topic: article
ms.service: defender-office-365
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- highpri
ms.custom:
- sfi-image-nochange
description: With the Security Copilot integration available in the Email Entity page, analysts can quickly understand why an email was delivered, blocked, quarantined, or remediated without manually reviewing large volumes of security signals and events.
locale: en-us
document_id: 1766535b-b6b5-375b-f68b-ab5564f86d48
document_version_independent_id: 1766535b-b6b5-375b-f68b-ab5564f86d48
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/security-copilot-in-email-entity.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: security-copilot-in-email-entity
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/security-copilot-in-email-entity.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/46e3c7c4-fe77-4a6e-b40a-44c569819fa5
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/d0c6fab8-2d7d-4bb0-bf40-589e08d7c132
platformId: 35a7e53d-8e6d-6173-1962-de0decf443dd
---

# Summarize Email Threats with Microsoft Security Copilot in Email Entity - Microsoft Defender for Office 365 | Microsoft Learn

Microsoft Defender for Office 365 applies the capabilities of [Security Copilot](/en-us/security-copilot/microsoft-security-copilot) to help security operations centre (SOC) analysts investigate email-based threats more efficiently. With the Security Copilot integration available in the Email Entity page, analysts can quickly understand why an email was delivered, blocked, quarantined, or remediated without manually reviewing large volumes of security signals and events. Email investigations often require analysts to correlate threat detections, email delivery actions, user interactions, policy decisions, and post-delivery remediation activities. Security Copilot streamlines this process by generating contextual summaries that explain the email's journey, threat posture, and the reasoning behind security decisions. This article describes the Security Copilot capabilities available within the Email Entity page, including Email Summary and Detonation Summary experiences.

## Prerequisites

If you're new to Security Copilot, familiarize yourself with it by reading the following articles:

- [What is Security Copilot?](/en-us/security-copilot/microsoft-security-copilot)
- [Security Copilot experiences](/en-us/security-copilot/experiences-security-copilot)
- [Get started with Security Copilot](/en-us/security-copilot/get-started-security-copilot)
- [Understand authentication in Security Copilot](/en-us/security-copilot/authentication)
- [Prompting in Security Copilot](/en-us/security-copilot/prompting-security-copilot)

## Security Copilot integration in the Email Entity page

The Email Entity page provides detailed information about individual email messages, including delivery actions, detections, policies, URLs, attachments, and post-delivery activities. Security Copilot enriches the Email Entity experience by generating AI-powered summaries that help analysts:

- Understand why a message was blocked, delivered, quarantined, or remediated
- Quickly identify the most important threat indicators
- Review how the email's threat posture evolved over time
- Understand the impact of post-delivery actions
- Investigate malicious URLs and attachments
- Analyze sandbox detonation results when available
- Reduce investigation time and improve analyst consistency

The Email Entity page includes the following Security Copilot experiences:

- Email Summary
- Detonation Summary

[![Screenshot of the Security Copilot integration on the Email entity page.](media/email-entity-security-copilot.png)](media/email-entity-security-copilot.png#lightbox)

## Email Summary

The Email Summary capability provides an end-to-end narrative of the email investigation by analyzing delivery events, threat detections, policy actions, URLs, attachments, and remediation activities. The summary helps analysts quickly understand both the original state of the email and its current state, including any changes that occurred after delivery.

### What information is included in an Email Summary?

Depending on data availability, the summary can include:

**Top Level Summary:**

A concise overview of the email investigation, including:

- Original threat verdict and latest threat verdict
- Current email location
- Original delivery outcome
- Detection rationale
- Override actions
- Policy-based decisions
- Post-delivery changes that affected the message

The summary explains why Microsoft Defender took specific actions and highlights changes that occurred during the email lifecycle.

**Email Timeline Events:**

A chronological summary of email events starting from the original delivery event and continuing through all post-delivery actions. Examples include:

- Initial delivery
- Zero-hour auto purge (ZAP)
- Quarantine operations
- User-reported actions
- Manual remediation

**URL Analysis:**

Security Copilot identifies and summarizes the most relevant URLs found within the message. The analysis can include:

- Malicious or suspicious URLs
- Reputation findings
- Phishing indicators
- Redirect behavior
- Related threat activity
- URL-related security signals

**Attachment Analysis:**

Security Copilot identifies and summarizes high-risk attachments present in the message. The analysis can include:

- Attachment threat verdicts
- Malware indicators
- Suspicious file behaviors
- Known malicious characteristics
- File-related security signals

### Generate an Email Summary

To generate an Email Summary, open an email from the Email Entity page and select Generate in the Email summary tab in Security Copilot pane. Depending on the available data, the summary can automatically highlight important investigative findings and potential next steps.

[![Screenshot 1 of the Email Summary on the Email entity page.](media/email-entity-email-summary-1.png)](media/email-entity-email-summary-1.png#lightbox)

[![Screenshot 2 of the Email Summary on the Email entity page.](media/email-entity-email-summary-2.png)](media/email-entity-email-summary-2.png#lightbox)

## Detonation Summary

Detonation Summary provides an AI-generated analysis of sandbox detonation results for URLs and files extracted from email messages.

Tip

The detonation summary is available only when detonation results exist for a URL or file present in the email.

### What information is included in a Detonation Summary?

Depending on data availability, the summary includes the following sections.

**Top Level Summary:**

Provides a concise overview of the detonation findings, including:

- Nature of the threat (Malware, Phish, Suspicious, or Benign)
- Core attack technique
- MITRE ATT&CK technique (when available)
- Primary behavioral signal observed during execution

**Verdict and Reason:**

Provides the final assessment and explanation.

***Verdict:*** One of the Malware, Phish or Spam

***Reasons:*** Security Copilot summarizes the most significant verdict reasons, including:

- Distinct detection findings
- High-confidence malicious indicators
- Supporting evidence used in classification

Reasons are presented as concise findings to help analysts quickly understand why the verdict was assigned.

**Execution Flow and Behavioral Summary:**

Provides a simplified explanation of the detonation path and observed behavior. The summary includes:

- Initial URL or file execution point
- Significant intermediate behaviors
- Final destination or landing page
- Redirect chains
- Abuse of legitimate services
- Page rendering observations when available

The execution flow is presented in an easy-to-follow format:

Initial → Intermediate → Final

For example:

Suspicious URL → Redirect chain → Credential harvesting page

or

Attachment execution → Script download → Malware payload delivery

**Malicious Indicators:**

Highlights only the most relevant and actionable indicators observed during detonation. Examples include:

- Non-benign verdict categories
- Lookalike domains
- Typosquatting indicators
- Credential phishing techniques
- Abuse of trusted platforms
- Suspicious redirects
- High-confidence malicious behaviors
- Threat intelligence findings Generic observations are omitted in favor of high-value investigative insights.

**Payload and Artifacts Observed:**

Provides a summary of the content and artifacts discovered during analysis. Examples include:

- HTML content
- JavaScript files
- PDF documents
- Archive files
- Executables
- Script content

When applicable, the summary can also identify:

- Credential collection pages
- Script-heavy behavior
- Malicious downloads
- Embedded payloads
- Macro-enabled files
- Additional suspicious artifacts

### Generate a Detonation Summary

To generate a detonation summary, open an Email Entity page and navigate to Security Copilot pane. Whenever detonation results are available for any URL or attachment from the email, a new cart of Detonation summary will be shown with the list of URLs or files having detonation result. Select any URL or file and click on Generate button to generate the summary.

[![Screenshot of the Detonation Summary on the Email entity page.](media/email-entity-detonation-summary.png)](media/email-entity-detonation-summary.png#lightbox)

## Provide feedback

Microsoft encourages users to provide feedback on generated summaries. Feedback helps improve the relevance, accuracy, and usefulness of Security Copilot experiences in Microsoft Defender. Use the feedback controls available in the Security Copilot pane to indicate whether the generated summary was helpful and to provide additional comments.