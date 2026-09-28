---
layout: Conceptual
title: Get started with Microsoft Defender for Endpoint Plan 1 - Microsoft Defender for Endpoint | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-endpoint/mde-plan1-getting-started
breadcrumb_path: /defender-endpoint/breadcrumb/toc.json
feedback_system: Standard
permissioned-type: public
feedback_product_url: https://techcommunity.microsoft.com/t5/security-compliance-and-identity/ct-p/MicrosoftSecurityandCompliance
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: bagol
description: Get started using Defender for Endpoint Plan 1. Learn how to use the Microsoft Defender portal, manage alerts and devices, and view reports.
author: limwainstein
ms.author: lwainstein
ms.topic: overview
ms.date: 2025-03-21T00:00:00.0000000Z
ms.service: defender-endpoint
ms.subservice: onboard
ms.localizationpriority: medium
ms.reviewer: shlomiakirav
ms.collection:
- m365-security
- tier1
ms.custom: intro-get-started
locale: en-us
document_id: 69bf204e-77a0-a763-7fb1-b172991ab0cf
document_version_independent_id: 69bf204e-77a0-a763-7fb1-b172991ab0cf
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-endpoint/mde-plan1-getting-started.md
site_name: Docs
depot_name: Learn.defender-endpoint
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: mde-plan1-getting-started
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-endpoint/mde-plan1-getting-started.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 6c395217-c9bf-97e9-3c85-b734f2ba116b
---

# Get started with Microsoft Defender for Endpoint Plan 1 - Microsoft Defender for Endpoint | Microsoft Learn

The Microsoft Defender portal (https://security.microsoft.com) enables you to view information about detected threats, manage your alerts and incidents, take any needed action on detected threats, and manage devices. The Microsoft Defender portal is where you can get started interacting with the threat protection capabilities you get with Defender for Endpoint Plan 1. The following sections describe how to get started:

- The Microsoft Defender portal
- Viewing and managing incidents & alerts
- Managing devices
- Viewing reports

## The Microsoft Defender portal

The Microsoft Defender portal (https://security.microsoft.com) is where you view alerts, manage devices, and view reports. When you sign into the Microsoft Defender portal, you start with the **Home** page, which resembles the following image:

[![The portal of Microsoft Defender XDR](/en-us/defender/media/mde-p1/m365-defender-portal.png)](/en-us/defender/media/mde-p1/m365-defender-portal.png#lightbox)

The Home page provides your security team with a snapshot aggregate view of alerts, device status, and threats detected. Microsoft Defender XDR is set up so that your security operations team can find the information they're looking for quickly and easily.

Note

Our examples shown in this article might differ from what you see in your Microsoft Defender portal. What you see in your portal depends on your licenses and permissions. In addition, your security team can customize your organization's portal by adding, removing, and rearranging cards.

### Cards highlight key information and include recommendations

The Home page includes cards, such as the Active incidents card shown in the following image:

[![The Active incidents card](/en-us/defender/media/mde-p1/active-incidents-card.png)](/en-us/defender/media/mde-p1/active-incidents-card.png#lightbox)

The card provides you with information at a glance, along with a link or button that you can select to view more detailed information. Referring to our example Active incidents card, we can select **View all incidents** to navigate to our list of incidents.

[![The list of Incidents](/en-us/defender/media/mde-p1/incidents.png)](/en-us/defender/media/mde-p1/incidents.png#lightbox)

### Navigation bar makes it easy to find alerts, the Action center, and more

The navigation bar on the left side of the screen enables you to move easily between incidents, alerts, the Action center, reports, and settings. The following table describes the navigation bar.

| Navigation bar item | Description |
| --- | --- |
| **Home** | Navigates to the Home page of the [Microsoft Defender portal](/en-us/defender-xdr/microsoft-365-security-center-mde). |
| **Incidents & alerts** | Expands to show **Incidents** and **Alerts**. |
| **Incidents & alerts** &gt; **Incidents** | Navigates to the **Incidents** list. Incidents are created when alerts are triggered and/or threats are detected. By default, the **Incidents** list displays data for the last 30 days, with the most recent incident listed first.  To learn more, see [Incidents](view-incidents-queue). |
| **Incidents & alerts** &gt; **Alerts** | Navigates to the **Alerts** list (also referred to as the **Alerts queue**). Alerts are triggered when a suspicious or malicious file, process, or behavior is detected. By default, the **Alerts** list displays data for the last 30 days, with the most recent alert listed first.  To learn more, see [Alerts](alerts-queue). |
| **Incidents & alerts** &gt; **Email & collaboration alerts** | If your subscription includes [Microsoft Defender for Office 365](/en-us/defender-office-365/mdo-about#defender-for-office-365-plan-1-vs-plan-2-cheat-sheet), alerts are generated when potential threats are detected in email and Office files. |
| **Actions & submissions** &gt; **Action center** | Navigates to the Action center, which tracks remediation and manual response actions. The Action center tracks activities like these: - Microsoft Defender Antivirus encounters a malicious file and then blocks/removes that file. - Your security team isolates a device.- Defender for Endpoint detects and quarantines a file.  To learn more, see [Action center](auto-investigation-action-center). |
| **Actions & submissions** &gt; **Submissions** | Navigates to the unified submissions portal, where admins can submit files to Microsoft for review. To learn more, see [Submit files in Microsoft Defender for Endpoint](admin-submissions-mde). |
| **Secure score** | Displays a representation of your organization's security posture along with a list of recommended actions and metrics.  To learn more, see [Microsoft Secure Score](/en-us/defender-xdr/microsoft-secure-score). |
| **Learning hub** | Navigates to a list of learning paths that you can access to learn more about Microsoft 365 security capabilities. |
| **Trials** | Navigates to a list of free Microsoft 365 trial subscriptions you can start. Starting a trial helps you make informed decisions about purchases or upgrades. Certain terms and conditions apply. See [Microsoft 365 trial terms and conditions](https://go.microsoft.com/fwlink/?linkid=2194722). |
| **Partner catalog** | If you're looking for a Microsoft partner to help you with your security and other settings, check out the lists of partners in this catalog. |
| **Assets** &gt; **Devices** | Navigates to your list of devices that are onboarded to Defender for Endpoint. Provides information about devices, such as their exposure and risk levels.  To learn more, see [Device inventory](machines-view-overview). |
| **Endpoints** &gt; **Configuration management** &gt; **Dashboard** | Navigates to a dashboard with cards that show your current security state with links to improve your score, set up your capabilities, onboard devices, and learn more about your capabilities. |
| **Reports** | Navigates to your reports, such as your [Threat protection report](threat-protection-reports), [Device health and compliance report](device-health-reports) and your [Web protection report](web-protection-overview). |
| **Health** | Includes links to the **Service health** and **Message center**. |
| **Health** &gt; **Service health** | Navigates to the Service health page in the Microsoft 365 admin center. This page enables you to view health status across all the services available with your organization's subscriptions. |
| **Health** &gt; **Message center** | Navigates to the Message center in the Microsoft 365 admin center. The Message center provides information about planned changes. Each message describes what's coming, how it might affect users, and how to manage changes. |
| **Permissions & roles** | Enables you to grant permissions to use the Microsoft Defender portal. Permissions are granted through roles in Microsoft Entra ID. Select a role, and a flyout pane appears. The flyout contains a link to Microsoft Entra ID where you can add or remove members in a role group.  To learn more, see [Manage portal access using role-based access control](rbac). |
| **Settings** | Navigates to general settings for your Microsoft Defender portal (listed as **Security center**) and Defender for Endpoint (listed as **Endpoints**).  To learn more, see [Settings](/en-us/defender-xdr/microsoft-365-defender-portal). |
| **More resources** | Displays a list of more portals and centers, such as Microsoft Entra ID and the Microsoft Purview portal.  To learn more, see [Microsoft security portals and admin centers](/en-us/defender-xdr/portals). |

Tip

To learn more, see the [Microsoft Defender portal overview](/en-us/defender-xdr/microsoft-365-security-center-mde).

## View and manage incidents & alerts

When you sign into the Microsoft Defender portal, make sure to view and manage your incidents and alerts. Start with your **Incidents** list. The following image shows a list of incidents, including one with high severity, and another with medium severity.

![Incidents list](/en-us/defender/media/mde-p1/incidents.png)

Select an incident to view details about the incident. Details include what alerts were triggered, how many devices and users were affected, and other details. The following image shows an example of incident details.

[![The details of an incident](/en-us/defender/media/mde-p1/single-incident.png)](/en-us/defender/media/mde-p1/single-incident.png#lightbox)

Use the **Alerts**, **Devices**, and **Users** tabs to view more information, such as the alerts that were triggered, devices that were affected, and user accounts that were affected. From there, you can take manual response actions, such as isolating a device, stopping and quarantining a file, and so on.

Tip

To learn more about using the **Incident** view, see [Manage incidents](manage-incidents).

## Manage devices

To view and manage your organization's devices, in the navigation bar, under **Assets**, select **Devices**. You see a list of devices. The list includes devices for which alerts were generated. By default, the data shown is for the past 30 days, with the most recent items listed first. Select a device to view more information about it. A flyout pane opens, as shown in the following image:

[![Selected device details](/en-us/defender/media/mde-p1/device-inventory-selecteddevice.png)](/en-us/defender/media/mde-p1/device-inventory-selecteddevice.png#lightbox)

The flyout pane displays details, such as any active alerts for the device, and includes links to take action, such as isolating a device.

If there are active alerts on the device, you can view them in the flyout pane. Select an individual alert to view more details about it. Or, take an action, such as **Isolate device**, so you can investigate the device further while minimizing the risk of infecting other devices.

Tip

To learn more, see [Investigate devices in the Defender for Endpoint devices list](investigate-machines).

## View reports

In Defender for Endpoint Plan 1, several reports are available in the Microsoft Defender portal. To access your reports, follow these steps:

1. Go to the Microsoft Defender portal (https://security.microsoft.com) and sign in.
2. In the navigation bar, choose **Reports**.
3. Select a report in the list. Reports include:

    - Threat protection report
    - Device health report
    - Web protection report

Tip

For more information, see [Threat protection reports](threat-protection-reports).

### Threat protection report

To access your Threat protection report, in the Microsoft Defender portal, choose **Reports**, and then choose **Threat protection**. The Threat Protection report shows alert trends, status, categories, and more. Views are arranged in two columns: **Alert trends** and **Alert status**, as shown in the following image:

[![Threat protection report](/en-us/defender/media/mde-p1/threat-protection-report.png)](/en-us/defender/media/mde-p1/threat-protection-report.png#lightbox)

Scroll down to see all the views in each list.

- By default, the views in the **Alert trends** column display data for the past 30 days, but you can set a view to display data for the last three months, last six months, or a custom time range (up to 180 days).
- The views in the **Alert status** column are a snapshot for the previous business day.

Tip

To learn more, see [Threat protection report in Defender for Endpoint](threat-protection-reports).

### Device health report

To access your Device health report, in the Microsoft Defender portal, choose **Reports**, and then choose **Device health**. The Device health report shows health state and antivirus across devices in your organization. Similar to the Threat protection report, views are arranged in two columns: **Device trends** and **Device summary**, as shown in the following image:

[![Device health report](/en-us/defender/media/mde-p1/device-health-report.png)](/en-us/defender/media/mde-p1/device-health-report.png#lightbox)

Scroll down to see all the views in each list. By default, the views in the **Device trends** column display data for the past 30 days, but you can change a view to display data for the last three months, last six months, or a custom time range (up to 180 days). The **Device summary** views are snapshots for the previous business day.

Tip

To learn more, see [Device health](device-health-reports).

### Web protection report

To access your Device health report, in the Microsoft Defender portal, choose **Reports**, and then choose **Web protection**. The Web protection report shows detections over time, such as malicious URLs and attempts to access blocked URLs, as shown in the following image:

[![Web protection report](/en-us/defender/media/mde-p1/web-protection-report.png)](/en-us/defender/media/mde-p1/web-protection-report.png#lightbox)

Scroll down to see all the views in the Web protection report. Some views include links that enable you to view more details, configure your threat protection features, and even manage indicators that serve as exceptions in Defender for Endpoint.

Tip

To learn more, see [Web protection](web-protection-overview).