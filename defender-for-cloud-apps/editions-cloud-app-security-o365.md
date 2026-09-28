---
layout: Conceptual
title: Differences between Defender for Cloud Apps and Office 365 Cloud App Security - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/editions-cloud-app-security-o365
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
description: This article describes the differences between Defender for Cloud Apps and Office 365 Cloud App Security.
ms.date: 2024-11-18T00:00:00.0000000Z
ms.topic: overview
ms.review: AmitMishaeli
locale: en-us
document_id: 4e790736-5d22-b657-1a20-63c16a09613b
document_version_independent_id: 4e790736-5d22-b657-1a20-63c16a09613b
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/editions-cloud-app-security-o365.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: editions-cloud-app-security-o365
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/editions-cloud-app-security-o365.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/6ab06385-661e-4214-8870-bbe4071c960d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/131ba09e-4280-4ae7-8622-1f9f1c0daad1
platformId: 10f93176-d70d-ec6a-e289-357f7fcdb72d
---

# Differences between Defender for Cloud Apps and Office 365 Cloud App Security - Microsoft Defender for Cloud Apps | Microsoft Learn

This article describes the differences between Defender for Cloud Apps and Office 365 Cloud App Security.

Both Microsoft Defender for Cloud Apps and Office 365 Cloud App Security are accessed through the Microsoft Defender portal. Depending on your license, you'll either have access to Office 365 Cloud App Security only or the entire Defender for Cloud Apps solution.

For more information, see the [Office 365 licensing datasheet](https://aka.ms/M365EnterprisePlans).

## Microsoft Defender for Cloud Apps

Microsoft Defender for Cloud Apps is a comprehensive cross-SaaS solution bringing deep visibility, strong data controls, and enhanced threat protection to your cloud apps. With this service, you can gain visibility into Shadow IT by discovering cloud apps in use. You can control and protect data in the apps once you sanction them to the service.

## Office 365 Cloud App Security

Office 365 Cloud App Security is a subset of Microsoft Defender for Cloud Apps that provides enhanced visibility and control for Office 365.

Office 365 Cloud App Security includes threat detection based on user activity logs, discovery of Shadow IT for apps that have similar functionality to Office 365 offerings, control app permissions to Office 365, and apply access and session controls. Office 365 Cloud App Security has access to all of the features of Microsoft Defender for Cloud Apps, but supports only the Office 365 app connector.

### Feature support

| Capability | Feature | Microsoft Defender for Cloud Apps | Office 365 Cloud App Security |
| --- | --- | --- | --- |
| App Governance | App Governance | Yes |  |
| Cloud discovery | Discovered apps | 34,000 + cloud apps | 750+ cloud apps with similar functionality to Office 365 |
|  | Deployment for discovery analysis | - Manual upload<br>- Automated upload - Log collector and API<br>- Native Defender for Endpoint integration | Manual log upload |
|  | Log anonymization for user privacy | Yes |  |
|  | Access to full cloud app catalog | Yes |  |
|  | Cloud app risk assessment | Yes |  |
|  | Cloud usage analytics per app, user, IP address | Yes |  |
|  | Ongoing analytics & reporting | Yes |  |
|  | Anomaly detection for discovered apps | Yes |  |
| Information Protection | Data Loss Prevention (DLP) support | Cross-SaaS DLP and data sharing control | Uses existing Office DLP (available in Office E3 and above) |
|  | App permissions and ability to revoke access | Yes | Yes |
|  | Policy setting and enforcement | Yes |  |
|  | Integration with Microsoft Purview | Yes |  |
|  | Integration with third-party DLP solutions | Yes |  |
| Threat Detection | Anomaly detection and behavioral analytics | For Cross-SaaS apps including Office 365 | For Office 365 apps |
|  | Manual and automatic alert remediation | Yes | Yes |
|  | SIEM connector | Yes. Alerts and activity logs for cross-SaaS apps. | For Office 365 alerts only |
|  | Integration to Microsoft Intelligent Security Graph | Yes | Yes |
|  | Activity policies | Yes | Yes |
| Conditional access app control | Real-time session monitoring and control | Any cloud and on-premises app | For Office 365 apps |
| Cloud Platform Security | Security configurations | For Azure, AWS, and GCP | For Azure |