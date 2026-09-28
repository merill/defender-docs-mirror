---
layout: Conceptual
title: View and manage Microsoft Defender for Identity security alerts - Microsoft Defender for Identity | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-for-identity/understanding-security-alerts
feedback_system: Standard
feedback_product_url: https://aka.ms/MDIcommunity
breadcrumb_path: /azure-advanced-threat-protection/bread/toc.json
author: AbbyMSFT
manager: bagol
ms.author: abbyweisberg
ms.collection: M365-security-compliance
ms.service: microsoft-defender-for-identity
uhfHeaderId: MSDocsHeader-MicrosoftDefender
ms.suite: ems
description: Learn how to view, filter, investigate, classify, and manage security alerts in Microsoft Defender for Identity using the alerts queue in the Microsoft Defender portal.
ms.date: 2026-07-02T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: rlitinsky
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 448b0551-12b9-73b2-152c-9d2e5cdbf6bc
document_version_independent_id: 448b0551-12b9-73b2-152c-9d2e5cdbf6bc
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-identity/understanding-security-alerts.md
site_name: Docs
depot_name: Learn.ATP-Docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: understanding-security-alerts
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-identity/understanding-security-alerts.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/5711eaa5-435f-4c40-8d89-924ef7945eec
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8ee4d551-d6c4-4e91-986e-0f1afd52559f
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
platformId: 81f306c5-35b3-46e0-9156-7df5d68328ad
---

# View and manage Microsoft Defender for Identity security alerts - Microsoft Defender for Identity | Microsoft Learn

The alerts queue shows a list of alerts that were flagged from identities in your network. By default, the queue displays alerts seen in the last seven days in a grouped view. The most recent alerts are shown at the top of the list helping you see the most recent alerts first.

This article explains how to view, filter, investigate, classify, and manage security alerts in Microsoft Defender for Identity.

## View the alerts queue

In the [Microsoft Defender portal](https://security.microsoft.com), go to **Incidents & alerts** and then to **Alerts**.

Alerts from the last seven days are displayed with the following information:

- Alert name
- Tags
- Severity
- Investigation state
- Status
- Category
- Detection source
- Impacted assets
- First activity
- Last activity

[![Screenshot showing the Alerts page in the Defender portal. Two alerts named Suspected brute-force are listed with full alert details.](media/understanding-security-alerts/filtered-alerts.png)](media/understanding-security-alerts/filtered-alerts.png#lightbox)

## Customize the view of the alerts queue

You can customize the view of the alerts queue in a few ways. Using the tools at the top of the page, you can:

- Customize the view to add or remove columns.
- Apply filters.
- Customize the duration. Display the alerts for a particular duration, such as 1 Day, 3 Days, 1 Week, 30 Days, and 6 Months.
- Export a detailed Excel report for analysis.

### Filter the alerts view

You can apply the following filters to get a more focused view of the alerts.

| Alert | Description |
| --- | --- |
| **Severity** | Alert severity is based on several factors, including how much access the attacker might have, the potential impact if the attack succeeds, and the likelihood that the alert is a true positive. For a full list of alert types and their assigned severity levels, see the article [Security alert name mapping and unique external IDs](alerts-overview) |
| **Status** | You can choose to filter the list of alerts based on their Status. For example, you can filter to show only alerts that are **New**, **In Progress**, or **Resolved**. |
| **Detection sources** | You can filter the alerts based on the following Detection sources: **Microsoft Defender for Identity** or **Microsoft Defender XDR** |
| **Tags** | You can filter the alerts based on Tags assigned to alerts. |

### View an alert

You can access individual alerts from multiple locations, by selecting the alert name from any of the following:

- The **Alerts** page
- The **Incidents** page
- The **Identities** page
- The pages of individual **Devices**
- The **Advanced hunting** page

## Understand the alerts page

The alerts page provides context into the alert, by combining attack signals and alerts related to the selected alert to construct a detailed alert story. The alerts page helps you quickly triage, investigate, and take effective action on alerts.

Note

Microsoft Defender for Identity alerts currently appear in two different layouts in the Microsoft Defender portal. While the alert views show different information, all alerts are based on Defender for Identity collected data. The differences between these two alert layouts are part of an ongoing transition to a unified alerting experience across Microsoft Defender products.

To view alerts from both Defender for Identity and Defender XDR, select **Filter**, then under **Service sources** choose **Microsoft Defender for Identity** and **Defender XDR**, and select **Apply**:

![Screenshot showing the alerts filter menu per service.](media/understanding-security-alerts/filter-alerts-menu.png)

### Microsoft Defender for Identity alerts

At the top of the page, there are sections for the **Accounts**, **Destination Host**, and **Source Host** of the alert. Depending on the alert, you might see details about additional hosts, accounts, IP addresses, domains, and security groups. Select any listed entity to get more details about the entities involved.

- The **Alert story**section gives information to provide a complete story with the details of the alert. The alert story is divided into two sections:
    - **What happened** includes the alert's timeline and the entities involved in the alert.
    - **Alert graph** provides a visual representation of the alert, including the entities involved in the alert and their relationships. The graph helps you understand how the entities are connected and how they relate to the alert.
- **Important information** provides technical context that supports alert investigation. You can use this information to validate whether the activity was expected or suspicious and decide what actions to take to contain or escalate the incident.
- **Activity details** provides detailed information, including the timestamp, the base object, the search scope, and other details about the alert.
- The **details pane** on the right side of the page provides additional information about the alert, including the **Alert details**, **Comments & history**. The details pane also provides additional options, such as:
    - Manage alert
    - Export alert
    - Move alert to another incident
    - Classify an alert

[![Screenshot showing the Defender for Identity alert structure.](media/understanding-security-alerts/legacy-mdi-alert-structure.png)](media/understanding-security-alerts/legacy-mdi-alert-structure.png#lightbox)

### Microsoft Defender XDR alerts

At the top of the page, there are sections for the **Accounts**, **Destination Host**, and **Source Host** of the alert. Depending on the alert, you might see buttons for details about additional hosts, accounts, IP addresses, domains, and security groups. Select any of these entities to get more details about the entities involved.

- The **Alert story**section gives information to provide a complete story with the details of the alert. The alert story is divided into two sections:
    - **What happened** includes the alert's timeline and the entities involved in the alert.
- The **details pane** on the right side of the page provides additional information about the alert, including the **Alert details**, **Comments & history**. The details pane also provides additional options, such as:
    - Manage alert
    - Move alert to another incident
    - Classify an alert

[![Screenshot showing the Defender for XDR alert structure](media/understanding-security-alerts/defender-xdr-alert-structure.png)](media/understanding-security-alerts/defender-xdr-alert-structure.png#lightbox)

## Manage security alerts

Selecting an alert opens the Alert management pane, where you can perform the following actions:

- Change the status of an alert
- Move an alert to another incident
- Assign alerts
- Add comments to an alert
- Classify security alerts
- Tuning alerts

### Change the status of an alert

You can categorize alerts as New, In Progress, or Resolved by changing their status as your investigation progresses. This helps you organize and manage how your team can respond to alerts. For example, a team leader can review all New alerts, and decide to assign them to the In Progress queue for further analysis. The team leader might assign the alert to the Resolved queue if they know the alert is benign, or coming from a device that is irrelevant (such as one belonging to a security administrator), or is being dealt with through an earlier alert.

### Move an alert to another incident

You can create a new incident from the alert or link to an existing incident.

![Screenshot showing the option to move an alert to another incident.](media/understanding-security-alerts/move-alert-to-other-incident.png)

### Assign alerts

If an alert isn't yet assigned, you can select Assign to me to assign the alert to yourself.

[![Screenshot that shows how to assign an alert to yourself.](media/understanding-security-alerts/alert-state.png)](media/understanding-security-alerts/alert-state.png#lightbox)

### Add comments to an alert

You can add comments to an alert to provide additional context or information. Adding comments is useful for sharing insights with your team or documenting your investigation process. Whenever a change or comment is made to an alert, it's recorded in the Comments and history section.

[![Screenshot showing the Comments &amp; history section in the Microsoft Defender portal. A text box is provided for entering comments.](media/understanding-security-alerts/comments-history.png)](media/understanding-security-alerts/comments-history.png#lightbox)

### Classify security alerts

Defender for Identity security alerts can be classified as true positive, benign true positive, or false positive. These classifications are abbreviated as TP, B-TP, and FP throughout this section. For each alert, ask the following questions to determine the alert classification and help decide what to do next:

1. Is the security alert a TP, B-TP, or FP?
2. How common is this specific security alert in your environment?
3. Was the alert triggered by the same types of computers or users? For example, servers with the same role or users from the same group/department? If the computers or users were similar, you might decide to exclude this alert type to avoid extra future FP alerts.

Following proper investigation, all Defender for Identity security alerts can be classified as one of the following activity types:

- **True positive (TP)**: A malicious action detected by Defender for Identity.
- **Benign true positive (B-TP)**: An action detected by Defender for Identity that is real, but not malicious, such as a penetration test or known activity generated by an approved application.
- **False positive (FP)**: A false alarm, meaning the activity didn't happen.

[![Screenshot that shows how to classify an alert as a true or false alert.](media/understanding-security-alerts/classify-alert.png)](media/understanding-security-alerts/classify-alert.png#lightbox)

Note

An increase of alerts of the exact same type typically reduces the suspicious/importance level of the alert. For repeated alerts, verify configurations, and use security alert details and definitions to understand exactly what is happening that trigger the repeats.

### Tune security alerts

Tune your alerts to adjust and optimize them, reducing false positives. Alert tuning allows your SOC teams to focus on high-priority alerts and improve threat detection coverage in your system. In Microsoft Defender, create rule conditions based on evidence types, and then apply your rule on any rule type that matches your conditions.

For more information, see [Tune an alert](/en-us/microsoft-365/security/defender/investigate-alerts#tune-an-alert).