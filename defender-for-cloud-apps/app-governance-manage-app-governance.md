---
layout: Conceptual
title: App governance in Microsoft Defender for Cloud Apps and Microsoft Defender XDR - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/app-governance-manage-app-governance
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
ms.date: 2025-08-12T00:00:00.0000000Z
ms.reviewer: anandd512
ms.topic: concept-article
description: Implement Microsoft app governance capabilities over Microsoft Defender for Cloud Apps and Microsoft Defender XDR to govern your apps.
locale: en-us
document_id: 7bc9e017-1b79-5b5e-5775-1adb70a3d602
document_version_independent_id: 7bc9e017-1b79-5b5e-5775-1adb70a3d602
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/app-governance-manage-app-governance.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: app-governance-manage-app-governance
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/app-governance-manage-app-governance.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 4510c6d5-ef8c-e337-dd8b-dc6de0798120
---

# App governance in Microsoft Defender for Cloud Apps and Microsoft Defender XDR - Microsoft Defender for Cloud Apps | Microsoft Learn

Cyber attacks have become increasingly sophisticated in the ways they exploit the apps you have deployed in your on-premises and cloud infrastructure, establishing a starting point for privilege escalation, lateral movement, and data exfiltration.

To understand the potential risks and stop these types of attacks, you need to gain clear visibility into your organization’s app compliance posture. You need to be able to quickly identify when an app exhibits anomalous behaviors and respond when these behaviors present risks to your environment, data, and users. 

## App governance features

App governance in Defender for Cloud Apps is a set of security and policy management capabilities designed for OAuth-enabled apps registered on Microsoft Entra ID, Google, and Salesforce. App governance delivers visibility, remediation, and governance into how these apps and their users access, use, and share sensitive data in Microsoft 365 and other cloud platforms through actionable insights and automated policy alerts and actions.

App governance also enables you to see which user-installed OAuth applications have access to data on Microsoft 365, Google Workspace, and Salesforce. It tells you what permissions the apps have and which users have granted access to their accounts.

App governance insights enable you to make informed decisions around blocking or restricting apps that present significant risk to your organization. For example:

- **Insights**: See a view of all non-Microsoft apps registered to Microsoft Entra ID, Google, or Salesforce in your organization on a single dashboard. You can see the status of apps and their activities, and react or respond to them.
- **Governance**: Create proactive or reactive policies for app and user patterns and behaviors and protect your users from using noncompliant or malicious apps and limiting the access of risky apps to your data.
- **Detection**: Be alerted and notified when there are anomalies in app activity and when noncompliant, malicious, or risky apps are used.
- **Remediation**: Along with automatic remediation capabilities, use remediation controls in a timely manner to respond to anomalous app activity detections.

## Share data across Microsoft services

View app governance data together with other Defender for Cloud Apps data and Microsoft Entra data to aggregate information and jump between views.

For example:

- On the **App governance** page, view aggregated sign-in activity for each app. Select an app to view details in a side pane, and select **View in Azure AD** to view more details in the Microsoft Entra admin center.
- On other **Cloud apps** pages in Microsoft Defender XDR, view API usage levels and aggregate data transfer. From there, select links to go to the app governance **OAuth apps** page for more details.

App governance alerts show up in the Microsoft Defender XDR alerts list as alerts with the **Detection source** field set to *App Governance*.