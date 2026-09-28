---
layout: Conceptual
title: Microsoft Defender for Identity in the Microsoft Defender portal - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/microsoft-365-security-center-mdi
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection:
- m365-security
- tier2
ms.service: defender-xdr
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: Learn how to use Microsoft Defender for Identity within the Microsoft Defender portal to monitor and manage security across your Microsoft identities, data, devices, apps, and infrastructure.
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.date: 2024-02-14T00:00:00.0000000Z
ms.topic: concept-article
ms.custom: admindeeplinkDEFENDER, defender-for-identity
locale: en-us
document_id: 1f609b23-4d00-171b-e873-fec530b26583
document_version_independent_id: 1f609b23-4d00-171b-e873-fec530b26583
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/microsoft-365-security-center-mdi.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: microsoft-365-security-center-mdi
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/microsoft-365-security-center-mdi.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
platformId: 67f14fe4-c96c-744f-dcc4-751e894a0975
---

# Microsoft Defender for Identity in the Microsoft Defender portal - Microsoft Defender for Identity | Microsoft Learn

**Applies to:**

- What is Microsoft Defender?
- [Microsoft Defender for Identity](/en-us/defender-for-identity/)

Microsoft Defender for Identity is part of the Microsoft Defender portal, the home for monitoring and managing security across your Microsoft identities, data, devices, apps, and infrastructure. The Microsoft Defender portal allows security admins to perform their security tasks in one location, which simplifies workflows and integrating functionality from other Microsoft Defender services.

Microsoft Defender for Identity contributes identity focused information into the incidents and alerts that the Microsoft Defender portal presents. This information is key to providing context and correlating alerts from the other products within Microsoft Defender.

## Converged experiences in the Microsoft Defender portal

The [Microsoft Defender portal](https://security.microsoft.com) combines security capabilities that protect, detect, investigate, and respond to email, collaboration, identity, and device threats.

The following sections describe enhanced Defender for Identity features found in the Microsoft Defender portal.

Note

Customers using the classic Defender for Identity portal are [automatically redirected to the Microsoft Defender portal](https://techcommunity.microsoft.com/t5/microsoft-365-defender-blog/leveraging-the-convergence-of-microsoft-defender-for-identity-in/ba-p/3856321), with no option to revert back to the classic portal.

### Configuration and posture

| Area | Description |
| --- | --- |
| **Global exclusions** | Global exclusions allow you to define certain entities, such as IP addresses, devices, or domains, to be excluded across all Defender for Identity detections. For example, if you only exclude a device, the exclusion applies only to detections that have a *device* identification as part of the detection.  For more information, see [Global excluded entities](/en-us/defender-for-identity/exclusions). |
| **Manage action and directory service accounts** | You might want to respond to compromised users by disabling their accounts or resetting their password. When you take either of these actions, the Microsoft Defender portal is configured by default to use the *local system* account. Therefore, you'll only need to configure action and directory service account settings if you want to have more control, and define a different user account to perform user remediation actions. For more information, see [Microsoft Defender for Identity action accounts](/en-us/defender-for-identity/manage-action-accounts). |
| **Custom permission roles** | The Microsoft Defender portal supports custom permission roles. For more information, see [Microsoft Defender XDR role-based access control (RBAC)](/en-us/defender-xdr/manage-rbac). |
| **Microsoft Secure Score** | Defender for Identity security posture assessments is available in [Microsoft Secure Score](https://security.microsoft.com/securescore). Each assessment is a downloadable report with instructions for use and tools to build an action plan for remediating or resolving the issue. Filter Microsoft Secure Score by **Identity** to view Defender for Identity assessments.  For more information, see [Microsoft Defender for Identity's security posture assessments](/en-us/defender-for-identity/security-assessment). |
| **API** | Use any of the following Microsoft Defender XDR APIs with Defender for Identity: - [Query activities via API](/en-us/defender-xdr/api-advanced-hunting)- [Manage security alerts via API](/en-us/defender-xdr/api-incident)- [Stream security alerts and activities to Microsoft Sentinel](/en-us/defender-xdr/streaming-api)**Tip**: The Microsoft Defender portal only stores advanced hunting data for 30 days. If you need longer retention periods, stream the activities to Microsoft Sentinel or another partner security information and event management (SIEM) system. |
| **Onboarding** | Defender for Identity onboarding is now automatic for new customers, with no need to configure a workspace. If you need to delete your instance, open a Microsoft support case. |

### Investigation

| Area | Description |
| --- | --- |
| **Identities** area | In the Microsoft Defender portal, expand the **Identities** area to view a **Dashboard** of graphs and widgets with commonly used data, and other identity security pages. The **Health issues** page, listing all health issues for your Defender for Identity deployment, is available under **Settings** &gt; **Identities** &gt; **Deployment**. For more information, see [View the Identity Security dashboard](/en-us/defender-for-identity/dashboard) and [Defender for Identity health issues](/en-us/defender-for-identity/health-alerts). |
| **Identity page** | The Microsoft Defender portal identity details page provides inclusive data about each identity, such as: - Any associated alerts - Active Directory account control- Risky lateral movement paths- A timeline of activities and alerts- Details about observed locations, devices, and groups. For more information, see [Investigate users in the Microsoft Defender portal](/en-us/defender-xdr/investigate-users). |
| **Device page** | The Microsoft Defender portal alert evidence lists all devices and users connected to each suspicious activity. Investigate further by selecting a specific device in an alert to access a device details page. For more information, see [Investigate devices in the Microsoft Defender for Endpoint Devices list](/en-us/defender-endpoint/investigate-machines). |
| **Advanced hunting** | The Microsoft Defender portal helps you proactively search for threats and malicious activity by using advanced hunting queries. These powerful queries can be used to locate and review threat indicators and entities for both known and potential threats. Build custom detection rules from advanced hunting queries to help you proactively watch for events that might be indicative of breach activity and misconfigured devices. For more information, see [Proactively hunt for threats with advanced hunting in the Microsoft Defender portal](/en-us/defender-xdr/advanced-hunting-overview). |
| **Global search** | Use the search bar at the top of the Microsoft Defender portal page to search for any entity being monitored by Microsoft Defender XDR, including identities, endpoints, Office 365 data, Active Directory groups (Preview), and more. Select results directly from the search drop-down, or select **All users** or **All devices** to see all entities associated with a given search term. |

### Detection and response

| Area | Description |
| --- | --- |
| **Alert and incident correlation** | Defender for Identity alerts is now included in the Microsoft Defender portal's alert queue, making them available to the automated incident correlation feature. View all of your alerts in one place, and determine the scope of the breach even quicker than before. For more information, see [Investigate Defender for Identity alerts in the Microsoft Defender portal](/en-us/defender-for-identity/manage-security-alerts). |
| **Alert exclusions** | The Microsoft Defender portal's alert interface is more user friendly, and includes a search function and global exclusions, meaning you can exclude any entity from all alerts generated by Defender for Identity. For more information, see [Configure Defender for Identity detection exclusions in Microsoft Defender](/en-us/defender-for-identity/exclusions). |
| **Alert tuning** | Alert tuning, previously known as *alert suppression*, allows you to adjust and optimize your alerts. Alert tuning reduces false positives, allowing your SOC teams to focus on high-priority alerts, and improves threat detection coverage throughout your system. In Microsoft Defender, create rule conditions based on evidence types, and then apply your rule on any rule type that matches your conditions. For more information, see [Tune an alert](/en-us/defender-xdr/investigate-alerts#tune-an-alert). |
| **Remediation actions** | Defender for Identity remediation actions, such as disabling accounts or requiring password resets, are available from the Microsoft Defender portal user details page. For more information, see [Remediation actions in Microsoft Defender for Identity](/en-us/defender-for-identity/remediation-actions). |

## Quick reference for legacy portal users

The following table lists the changes in navigation between Microsoft Defender for Identity and the Microsoft Defender portal.

| **Defender for**Identity | **The Microsoft Defender portal** |
| --- | --- |
| **Timeline** | - Microsoft Defender portal Alerts/Incidents queue |
| **Reports** | The following types of reports are available from the **Reports** &gt; **Identities** &gt; **Report management** page in the Microsoft Defender portal, either for immediate download or scheduled for a periodic email delivery: - A summary report of alerts and health issues you should take care of. - A list of each time a modification is made to sensitive groups. - A list of source computer and account passwords that are detected as being sent in clear text.  For more information, see [Report management](/en-us/defender-for-identity/reports). |
| **Identity page** | Microsoft Defender portal user details page |
| **Device page** | Microsoft Defender portal device details page |
| **Group page** | Microsoft Defender portal groups side pane |
| **Alert page** | Microsoft Defender portal alert details page **Tip**: Use [alert tuning](/en-us/defender-xdr/investigate-alerts#tune-an-alert) to optimize the alerts you see in the Microsoft Defender portal. |
| **Search** | Microsoft Defender portal global search |
| **Health issues** | Microsoft Defender portal **Settings &gt; Identities &gt; Health issues** |
| **Entity activities** | - **Advanced hunting**- Device page &gt; **Timeline**- Identity page &gt; **Timeline** tab - **Group** pane &gt; **Timeline** tab |
| **Settings** | **Settings** -&gt; **Identities** |
| **Users and accounts** | **Assets** -&gt; **Identities** |
| **Identity security posture** | [Microsoft Defender for Identity's security posture assessments](/en-us/defender-for-identity/security-assessment) |
| **Onboarding a new workspace** | **Settings** -&gt; **Identities** (automatically) |
| **About** | **Settings &gt; Identities &gt; About** |