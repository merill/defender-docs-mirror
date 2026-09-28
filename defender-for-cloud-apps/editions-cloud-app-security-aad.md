---
layout: Conceptual
title: Discovery capability differences for Defender for Cloud Apps and Cloud App Discovery - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/editions-cloud-app-security-aad
feedback_system: Standard
feedback_product_url: https://docs.microsoft.com/cloud-app-security/support-and-ts
uhfHeaderId: MSDocsHeader-MicrosoftDefender
breadcrumb_path: /defender-cloud-apps/breadcrumb/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: defender-for-cloud-apps
ms.suite: ems
description: This article describes the differences between discovery capabilities in Defender for Cloud Apps and Cloud App Discovery (part of Microsoft Entra ID).
ms.date: 2023-02-15T00:00:00.0000000Z
ms.topic: overview
ms.reviewer: Mravela 
locale: en-us
document_id: c0e8b536-7c8b-312f-cf39-e0309314aa96
document_version_independent_id: c0e8b536-7c8b-312f-cf39-e0309314aa96
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/editions-cloud-app-security-aad.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: editions-cloud-app-security-aad
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/editions-cloud-app-security-aad.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 50a249f3-a16b-3109-4dc0-940853e58bb5
---

# Discovery capability differences for Defender for Cloud Apps and Cloud App Discovery - Microsoft Defender for Cloud Apps | Microsoft Learn

This article describes the differences between discovery capabilities in Defender for Cloud Apps and Cloud App Discovery.

For information about licensing, see the [Microsoft 365 licensing datasheet](https://aka.ms/M365EnterprisePlans).

## Microsoft Defender for Cloud Apps

Microsoft Defender for Cloud Apps is a comprehensive cross-SaaS solution bringing deep visibility, strong data controls, and enhanced threat protection to your cloud apps. Cloud discovery is one of the features of Defender for Cloud Apps, which enables you to gain visibility into Shadow IT by discovering cloud apps in use.

## Cloud app discovery

Cloud app discovery comes at no additional cost as part of:

1. Microsoft Entra ID P1.
2. Enterprise Mobility + Security E3 (EMS E3).
3. Microsoft 365 E3.

This is a subset of Microsoft Defender for Cloud Apps. It includes cloud discovery capabilities that provide deeper visibility into cloud app usage in your organizations.

[Upgrade to Microsoft Defender for Cloud Apps](https://www.microsoft.com/security/business/cloud-apps-defender) to receive the full suite of Cloud Access Security Broker (CASB) capabilities offered by Microsoft Defender for Cloud Apps.

### Feature comparison

The following table is a comparison of the discovery capabilities in Defender for Cloud Apps and Cloud App Discovery.

| Capability | Feature | Microsoft Defender for Cloud Apps | Cloud App Discovery |
| --- | --- | --- | --- |
| Cloud discovery | Discovered apps | 31,000 + cloud apps | 31,000 + cloud apps |
|  | Deployment for discovery analysis | - Manual upload<br>- Automated upload - Log collector and API<br>- Native Defender for Endpoint integration | Manual and automatic log upload. [Learn more about setting up cloud discovery](set-up-cloud-discovery) |
|  | Log anonymization for user privacy | Yes | Yes |
|  | Access to full cloud app catalog | Yes | Yes |
|  | Cloud app risk assessment | Yes | Yes |
|  | Cloud usage analytics per app, user, IP address | Yes | Yes |
|  | Ongoing analytics & reporting | Yes | Yes |
|  | Custom policy creation | Yes | Yes |
|  | Anomaly detection for discovered apps | Yes |  |
| Information Protection | Data Loss Prevention (DLP) support | Cross-SaaS DLP and data sharing control |  |
|  | App permissions and ability to revoke access (OAuth apps) | Yes |  |
|  | Policy setting and enforcement | Yes |  |
|  | Integration with Microsoft Purview | Yes |  |
|  | Integration with third-party DLP solutions | Yes |  |
| Threat Detection | Anomaly detection and behavioral analytics | For Cross-SaaS apps |  |
|  | Manual and automatic alert remediation | Yes |  |
|  | SIEM connector | Yes. Alerts and activity logs for cross-SaaS apps. |  |
|  | Integration to Microsoft Intelligent Security Graph | Yes |  |
|  | Activity policies | Yes |  |