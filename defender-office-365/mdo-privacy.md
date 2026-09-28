---
layout: Conceptual
title: Privacy in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-office-365/mdo-privacy
breadcrumb_path: /defender-office-365/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
author: chrisda
ms.author: chrisda
ms.date: 2026-04-01T00:00:00.0000000Z
ms.topic: concept-article
ms.service: defender-office-365
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- essentials-privacy
ms.custom: 
description: Admins can learn about privacy in Defender for Office 365.
locale: en-us
document_id: d5ff0557-dae3-889f-8a20-8d3c88e92a5b
document_version_independent_id: d5ff0557-dae3-889f-8a20-8d3c88e92a5b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-office-365/mdo-privacy.md
site_name: Docs
depot_name: Learn.defender-office-365
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mdo-privacy
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-office-365/mdo-privacy.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
- https://authoring-docs-microsoft.poolparty.biz/devrel/609dad7f-61d2-4958-9386-e6e4bb38d61e
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
- https://authoring-docs-microsoft.poolparty.biz/devrel/1af30562-083a-42e2-aad4-17ae29f4ad72
platformId: 511541ec-491e-0f14-ce7d-edc0722c216b
---

# Privacy in Microsoft Defender for Office 365 - Microsoft Defender for Office 365 | Microsoft Learn

Microsoft Defender for Office 365 helps protect organizations against threats in email messages, links (URLs), file attachment, and collaboration tools. For more information about Defender for Office 365, see [Microsoft Defender for Office 365 overview](mdo-about).

## What do we collect?

We collect the following personal data as part of metadata when Microsoft 365 receives and processes email or Microsoft Teams messages:

- Display names
- Email addresses
- IP addresses
- Domains

Microsoft gathers system execution metadata for offline machine learning, and IP address and sender reputation information to protect users from malicious email or to filter unwanted email. This protection includes proactive [zero-hour auto purge (ZAP)](zero-hour-auto-purge) to remove messages that were already delivered.

All [reports in Defender for Office 365](reports-defender-for-office-365) are subject to End User Pseudonymous Identifiers (EUPI) and End User Identifiable Information (EUII):

- Data is shared within the organization only and is stored as plain text.
- All related data is securely stored in the organization's region.
- Only authorized users in the organization can access the data.

Microsoft stores this data securely in Microsoft Entra and maintains it in accordance with Microsoft privacy practices and [Microsoft Trust Center policies](https://go.microsoft.com/fwlink/p/?linkid=827578). All service log data at rest is encrypted and hashed using Office Data Loader (ODL) and Common Data Platform (CDP) encryption (no clear text). Defender for Office 365 uses this data for the following features:

- Threat policies to set the appropriate level of protection for your organization.
- Real-time reports to monitor Defender for Office 365 performance in your organization.
- Threat investigation and response capabilities that use leading-edge tools to investigate, understand, simulate, and prevent threats.
- Automated investigation and response capabilities that save time and effort investigating and mitigating threats.
- Advanced machine learning techniques and isolated detonation to detect the latest malware.

## Data location

Defender for Office 365 operates in the Microsoft Entra datacenters. For the following geo locations, data at rest for organizations that were provisioned in these geo locations is stored only in these geo locations:

- Australia
- Brazil
- Canada
- The European Union
- France
- Germany
- India
- Israel
- Italy
- Japan
- Norway
- Poland
- Qatar
- Singapore
- South Africa
- South Korea
- Sweden
- Switzerland
- United Arab Emirates
- United Kingdom
- United States

In [the built-in security features for all cloud mailboxes](eop-about), the following data is stored at rest in the local region geo:

- Alerts
- Attachments
- Block lists (URLs, block entries in the Tenant Allow/Block List, user Blocked Senders lists)
- Email metadata
- Grading analysis
- Junk email
- Quarantined email and quarantined attachments
- Reports
- Service configuration data and policies
- Spam domains
- URLs

In Defender for Office 365, the following customer data is stored at rest in the local region geo:

- Alerts
- Attachments
- Block lists (URLs, block entries in the Tenant Allow/Block List, user Blocked Senders lists)
- Email metadata
- Grading analysis
- Junk email
- Quarantined email and quarantined attachments
- Reports
- Service configuration data and policies
- Spam domains
- URLs

## Data Retention

Data from Defender for Office is retained for 180 days in reporting and logs. When email and Microsoft Teams messages are sent to Microsoft 365, sender and recipient personal data is extracted. Data is stored and processed securely: personal information is encrypted and automatically deleted 30 days after the retention period.

Your data is available to you while the license is within the grace period or suspended. At the end of this period, the data is erased from Microsoft systems in an unrecoverable manner no later than 190 days from the end of the subscription or after user account deletion.

## Data sharing for Defender for Office 365

Defender for Office 365 shares data, including customer data, among the following Microsoft products, if they're also licensed by a customer. For customers in the Government Community Cloud (GCC), data sharing between government and commercial cloud environments may occur, depending on the location of the service offering.

- Microsoft Defender
- Microsoft Sentinel
- Audit logs

## Advanced email analysis in Defender for Office 365

Defender for Office 365 improves email filtering against unwanted, malicious and abusive email by analyzing email messages processed by the service. Microsoft uses limited email data, with human review, for research purposes to improve the security and effectiveness of Defender for Office 365 and to reduce unwanted or malicious email (for example, spam, phishing or malware), in accordance with Microsoft's compliance, legal, and privacy standards.