---
layout: Conceptual
title: Common threat protection policies - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/policies-threat-protection
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
description: This topic outlines the steps to configure many threat protection policies in Defender for Cloud Apps.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: Ronen-Refaeli
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: e1bee1a7-a772-a923-1c8d-1bfcdcba1da9
document_version_independent_id: e1bee1a7-a772-a923-1c8d-1bfcdcba1da9
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/policies-threat-protection.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: policies-threat-protection
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/policies-threat-protection.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 0a27ba74-552f-4927-8960-ce789cb92591
---

# Common threat protection policies - Microsoft Defender for Cloud Apps | Microsoft Learn

This article describes common threat protection policies in Defender for Cloud Apps and explains how to configure them. Use these policies to identify high-risk use, detect abnormal user behavior, and prevent threats in your sanctioned cloud apps. Each section covers the prerequisites and steps to set up a specific policy, including both built-in anomaly detections and custom activity policies.

Note

When integrating Defender for Cloud Apps with Microsoft Defender for Identity, policies from Defender for Identity also appear on the policies page. For a list of Defender for Identity policies, see [Security Alerts](/en-us/defender-for-identity/suspicious-activity-guide).

## Detect and control user activity from unfamiliar locations

The activity from unfamiliar locations detection identifies user access or activity from locations that no one in your organization has visited before.

### Prerequisites

You must have at least one app connected using [app connectors](enable-instant-visibility-protection-and-governance-actions-for-your-apps).

### Steps

The unfamiliar locations detection is set up by default to alert you when access comes from new locations. No action is needed to turn on this policy. For more information, see [Anomaly detection policies](anomaly-detection-policy).

## Detect compromised account by impossible location (impossible travel)

The impossible travel detection identifies user access or activity from two different locations within a time period that is shorter than the time it takes to travel between them.

### Prerequisites

You must have at least one app connected using [app connectors](enable-instant-visibility-protection-and-governance-actions-for-your-apps).

### Steps

1. This detection is automatically configured out-of-the-box to alert you when there's access from impossible locations. You don't need to take any action to configure this policy. For more information, see [Anomaly detection policies](anomaly-detection-policy).
2. Optional: you can [customize anomaly detection policies](anomaly-detection-policy#scope-anomaly-detection-policies):

    - Customize the detection scope in terms of users and groups
    - Choose the types of sign-ins to consider
    - Set your sensitivity preference for alerting
3. Create the impossible travel anomaly detection policy.

## Detect suspicious activity from an "on-leave" employee

Detect when a user, who is on unpaid leave and shouldn't be active on any organizational resource, is accessing any of your organization's cloud resources.

### Prerequisites

- You must have at least one app connected using [app connectors](enable-instant-visibility-protection-and-governance-actions-for-your-apps).
- Create a security group in Microsoft Entra ID for the users on unpaid leave and add all the users you want to monitor.

### Steps

1. On the [User groups](user-groups) screen, select **Create user group** and import the relevant Microsoft Entra group.
2. In the Microsoft Defender Portal, under **Cloud Apps**, go to **Policies** -&gt; **Policy management**. Create a new **Activity policy**.
3. Set the filter **User group** equals to the name of the user groups you created in Microsoft Entra ID for the unpaid leave users.
4. Optional: Set the **Governance** actions to be taken when a violation is detected. Governance actions are automated responses—such as notifying a user, suspending an account, or revoking access—that vary between services. You can choose **Suspend user**.
5. Create the activity policy.

## Detect and notify when outdated browser OS is used

Detect when a user is using a browser with an outdated client version that might pose compliance or security risks to your organization.

### Prerequisites

You must have at least one app connected using [app connectors](enable-instant-visibility-protection-and-governance-actions-for-your-apps).

### Steps

1. In the Microsoft Defender Portal, under **Cloud Apps**, go to **Policies** -&gt; **Policy management**. Create a new **Activity policy**.
2. Set the filter **User agent tag** equals to **Outdated browser** and **Outdated operating system**.
3. Set the **Governance** actions to be taken on files when a violation is detected. The governance actions available vary between services. Under **All apps**, select **Notify user**, so that your users can act upon the alert and update the necessary components.
4. Create the Activity policy.

## Detect and alert when Admin activity is detected on risky IP addresses

A risky IP address is one that Defender for Cloud Apps identifies as suspicious based on threat intelligence. Detect admin activities performed from a risky IP address, and notify the system admin for further investigation or set a governance action on the acting administrator's account. Learn more [how to work with IP ranges and Risky IP](/en-us/defender-cloud-apps/ip-tags).

### Prerequisites

- You must have at least one app connected using [app connectors](enable-instant-visibility-protection-and-governance-actions-for-your-apps).
- From the Settings cog, select **IP address ranges** and select the + to add IP address ranges for your internal subnets and their egress public IP addresses. Set the **Category** to **Internal**.

### Steps

1. In the Microsoft Defender Portal, under **Cloud Apps**, go to **Policies** -&gt; **Policy management**. Create a new **Activity policy**.
2. Set **Act on** to **Single activity**.
3. Set the filter **IP address** to **Category** equals **Risky**
4. Set the filter **Administrative activity** to **True**
5. Set the **Governance** actions to be taken on files when a violation is detected. The governance actions available vary between services. Under **All apps**, select **Notify user**, so that your users can act upon the alert and update the necessary components **CC the user's manager**.
6. Create the activity policy.

## Detect activities by service account from external IP addresses

Detect service account activities originating from non-internal IP addresses. Activity from non-internal IP addresses could indicate suspicious behavior or a compromised account.

### Prerequisites

- You must have at least one app connected using [app connectors](enable-instant-visibility-protection-and-governance-actions-for-your-apps).
- From the Settings cog, select **IP address ranges** and select the + to add IP address ranges for your internal subnets and their egress public IP addresses. Set the **Category** to **Internal**.
- Standardize a naming conventions for service accounts in your environment, for example, set all account names to start with "svc".

### Steps

1. In the Microsoft Defender Portal, under **Cloud Apps**, go to **Policies** -&gt; **Policy management**. Create a new **Activity policy**.
2. Set the filter **User** to **Name** and then **Starts with** and enter your naming convention, such as svc.
3. Set the filter **IP address** to **Category** does not equal **Other** and **Corporate**.
4. Set the **Governance** actions to be taken on files when a violation is detected. The governance actions available vary between services.
5. Create the policy.

## Detect mass download (data exfiltration)

Detect when a certain user accesses or downloads a massive number of files in a short period of time.

### Prerequisites

You must have at least one app connected using [app connectors](enable-instant-visibility-protection-and-governance-actions-for-your-apps).

### Steps

1. In the Microsoft Defender Portal, under **Cloud Apps**, go to **Policies** -&gt; **Policy management**. Create a new **Activity policy**.
2. Set the filter **IP addresses** to **Tag** does not equal **Microsoft Azure**. This will exclude non-interactive device-based activities.
3. Set the filter **Activity types** equals to and then select all relevant download activities.
4. Set the **Governance** actions to be taken on files when a violation is detected. The governance actions available vary between services.
5. Create the policy.

## Detect potential Ransomware activity

Automatic detection of potential Ransomware activity.

### Prerequisites

- Ransomware detection applies only to Microsoft 365, Google Workspace, Box, and Dropbox.
- You must have at least one app connected using [app connectors](enable-instant-visibility-protection-and-governance-actions-for-your-apps).

### Steps

1. This detection is set up by default to alert you when a ransomware risk is found. No action is needed to turn on this policy. For more information, see [Anomaly detection policies](anomaly-detection-policy).
2. You can configure the **Scope** of the ransomware detection and choose which governance actions to take when an alert fires. To learn how Defender for Cloud Apps spots ransomware, see [Protecting your organization from ransomware](best-practices#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware).

## Detect malware in the cloud

Detect files containing malware in your cloud environments by utilizing the Defender for Cloud Apps integration with Microsoft Threat Intelligence, Microsoft's security analysis capability that identifies known malicious indicators such as malware signatures and suspicious IP addresses.

### Prerequisites

- For Microsoft 365 malware detection, you must have a valid license for Microsoft Defender for Microsoft 365 P1.
- You must have at least one app connected using [app connectors](enable-instant-visibility-protection-and-governance-actions-for-your-apps).

### Steps

- The malware detection is automatically configured out-of-the-box to alert you when there's a file that may contain malware. You don't need to take any action to configure this policy. For more information, see [Anomaly detection policies](anomaly-detection-policy).

## Detect rogue admin takeover

Detect repeated admin activity that might indicate malicious intentions.

### Prerequisites

You must have at least one app connected using [app connectors](enable-instant-visibility-protection-and-governance-actions-for-your-apps).

### Steps

1. In the Microsoft Defender Portal, under **Cloud Apps**, go to **Policies** -&gt; **Policy management**. Create a new **Activity policy**.
2. Set **Act on** to **Repeated activity** and customize the **Minimum repeated activities** and set a **Timeframe** to comply with your organization's policy..
3. Set the filter **User** to **From group** equals and select all the related admin group as **Actor only**.
4. Set the filter **Activity type** equals to all activities that relate to password updates, changes, and resets.
5. Set the **Governance** actions to be taken on files when a violation is detected. The governance actions available vary between services.
6. Create the policy.

## Detect suspicious inbox manipulation rules

If a suspicious inbox rule was set on a user's inbox, it may indicate that the user account is compromised, and that the mailbox is being used to distribute spam and malware in your organization.

### Prerequisites

- Use of Microsoft Exchange for email.

### Steps

- The suspicious inbox rule detection is automatically configured out-of-the-box to alert you when there's a suspicious inbox rule set. You don't need to take any action to configure this policy. For more information, see [Anomaly detection policies](anomaly-detection-policy).

## Detect leaked credentials

When cyber criminals compromise valid passwords of legitimate users, they often share those credentials. This is usually done by posting them publicly on the dark web or paste sites or by trading or selling the credentials on the black market.

Defender for Cloud Apps utilizes Microsoft's Threat intelligence to match such credentials to the ones used inside your organization.

### Prerequisites

You must have at least one app connected using [app connectors](enable-instant-visibility-protection-and-governance-actions-for-your-apps).

### Steps

The leaked credentials detection is automatically configured out-of-the-box to alert you when a possible credential leak is detected. You don't need to take any action to configure this policy. For more information, see [Anomaly detection policies](anomaly-detection-policy).

## Detect anomalous file downloads

Detect when users perform multiple file download activities in a single session, relative to the baseline learned. This could indicate an attempted breach.

### Prerequisites

You must have at least one app connected using [app connectors](enable-instant-visibility-protection-and-governance-actions-for-your-apps).

### Steps

1. This detection is automatically configured out-of-the-box to alert you when an anomalous download occurs. You don't need to take any action to configure this policy. For more information, see [Anomaly detection policies](anomaly-detection-policy).
2. It's possible to configure the scope of the detection and to customize the action to be taken when an alert is triggered.

## Detect anomalous file shares by a user

Detect when users perform multiple file-sharing activities in a single session with respect to the baseline learned, which could indicate an attempted breach.

### Prerequisites

You must have at least one app connected using [app connectors](enable-instant-visibility-protection-and-governance-actions-for-your-apps).

### Steps

1. This detection is automatically configured out-of-the-box to alert you when users perform multiple file sharing. You don't need to take any action to configure this policy. For more information, see [Anomaly detection policies](anomaly-detection-policy).
2. It's possible to configure the scope of the detection and to customize the action to be taken when an alert is triggered.

## Detect anomalous activities from infrequent country/region

Detect activities from a location that wasn't recently or was never visited by the user or by any user in your organization.

Note

This detection requires an initial learning period of 7 days. During the learning period, Defender for Cloud Apps does not generate alerts for new locations.

### Prerequisites

You must have at least one app connected using [app connectors](enable-instant-visibility-protection-and-governance-actions-for-your-apps).

### Steps

1. This detection is automatically configured out-of-the-box to alert you when an anomalous activity occurs from an infrequent country/region. You don't need to take any action to configure this policy. For more information, see [Anomaly detection policies](anomaly-detection-policy).
2. It's possible to configure the scope of the detection and to customize the action to be taken when an alert is triggered.

## Detect activity performed by a terminated user

Detect when a user who is no longer an employee of your organization performs an activity in a sanctioned app. This may indicate malicious activity by a terminated employee who still has access to corporate resources.

### Prerequisites

You must have at least one app connected using [app connectors](enable-instant-visibility-protection-and-governance-actions-for-your-apps).

### Steps

1. This detection is automatically configured out-of-the-box to alert you when an activity is performed by a terminated employee. You don't need to take any action to configure this policy. For more information, see [Anomaly detection policies](anomaly-detection-policy).
2. It's possible to configure the scope of the detection and to customize the action to be taken when an alert is triggered.