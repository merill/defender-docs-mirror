---
layout: Conceptual
title: Investigate predefined OAuth app policy alerts with app governance - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/app-governance-investigate-predefined-policies
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
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: shragar
description: Learn how to investigate predefined app policy alerts from app governance in Microsoft Defender XDR with Microsoft Defender for Cloud Apps.
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: 7871a290-8697-c7d7-2665-c0f46ebfd7cc
document_version_independent_id: 7871a290-8697-c7d7-2665-c0f46ebfd7cc
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/app-governance-investigate-predefined-policies.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: app-governance-investigate-predefined-policies
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/app-governance-investigate-predefined-policies.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/a3955c7b-f5ee-420d-aff5-d7119738f38b
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/b31948f4-2f38-404b-ac93-c3c8c5b3ae33
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 885430cf-17d8-5219-6bb4-6e450234f62b
---

# Investigate predefined OAuth app policy alerts with app governance - Microsoft Defender for Cloud Apps | Microsoft Learn

App governance provides predefined app policy alerts for anomalous activities. The purpose of this guide is to provide you with general and practical information on each alert, to help with your investigation and remediation tasks.

Included in this guide is general information about the conditions for triggering alerts. Because predefined policies are nondeterministic by nature, they're only triggered when there's behavior that deviates from the norm.

Tip

Some alerts might be in preview, so regularly review the updated alert statuses.

## Security alert classifications

Following proper investigation, all app governance alerts can be classified into one of the following activity types:

- **True positive (TP)**: An alert on a confirmed malicious activity.
- **Benign true positive (B-TP)**: An alert on suspicious but not malicious activity, such as a penetration test or other authorized suspicious action.
- **False positive (FP)**: An alert on a nonmalicious activity.

## General investigation steps

Use the following general guidelines when investigating any type of alert to gain a clearer understanding of the potential threat before applying the recommended action.

1. Review the app severity level and compare with the rest of the apps in your tenant. This review helps you identify which apps in your tenant pose greater risk.
2. If you identify a TP, review all the app activities to gain an understanding of the impact. For example, review the following app information:

    - Scopes granted access
    - Unusual behavior
    - IP address and location

## Review predefined app policy alerts

The following predefined app governance policy alerts include investigation and remediation guidance.

### Increase in data usage by an overprivileged or highly privileged app

An overprivileged app has permissions that exceed what it needs for its intended function, while a highly privileged app holds powerful permissions such as full mailbox or directory access. This alert detects unusual increases in data usage by overprivileged and highly privileged apps.

Note

As part of our continuous efforts to enhance Defender for Cloud apps alert accuracy, we have disabled this policy. The Increase in data usage by an overprivileged or highly privileged app policy remains visible in the Defender portal in a disabled state. If you want to continue using this policy, in the Defender portal, go to **App Governance**, and then the **Policies** page. Select the policy, and then select **Activate**.

**Severity**: Medium

Find apps with powerful or unused permissions that exhibit sudden increases in data usage through Graph API. Unusual changes in data usage might indicate compromise.

**TP or FP?**

To determine if the alert is a true positive (TP) or a false positive (FP), review all activities performed by the app, scopes granted to the app and user activity associated with the app.

- **TP**: Apply this recommended action if you have confirmed that the increase in data usage by an overprivileged or highly privileged app is irregular or potentially malicious.

    **Recommended action**: Contact users about the app activities that have caused the increase in data usage. Temporarily disable the app, reset the password, and then re-enable the app.
- **FP**: Apply this recommended action if you have confirmed that the detected app activity is intended and has a legitimate business use in the organization.

    **Recommended action**: Dismiss the alert.

### Unusual activity from an app with priority account consent

A priority account is a high-value account, such as an executive or service administrator, that you tag in Microsoft Defender for Cloud Apps. This alert triggers when an app that a priority account has consented to exhibits unusual activity.

Note

As part of our continuous efforts to enhance Defender for Cloud apps alert accuracy, we have disabled this policy. The Unusual activity from an app with priority account consent policy remains visible in the Defender portal in a disabled state. If you want to continue using this policy, in the Defender portal, go to **App Governance**, and then the **Policies** page. Select the policy, and then select **Activate**.

**Severity**: Medium

Find unusual increases in either data usage or Graph API access errors exhibited by apps that have been given consent by a priority account.

**TP or FP?**

Review all activities performed by the app, scopes granted to the app and user activity associated with the app.

- **TP**: Apply this recommended action if you have confirmed that the increase in data usage or API access errors by an app with consent from a priority account is highly irregular or potentially malicious.

    **Recommended action**: Contact priority account users about the app activities that have caused the increase in data usage or API access errors. Temporarily disable the app, reset the password, and then re-enable the app.
- **FP**: Apply this recommended action if you have confirmed that the detected app activity is intended and has a legitimate business use in the organization.

    **Recommended action**: Dismiss the alert.

### New app with low consent rate

**Severity**: Medium

Consent requests from a newly created app have been rejected frequently by users. Users typically reject consent requests from apps that exhibit unexpected behavior or arrived from an untrusted source. Apps that have low consent rates are more likely to be risky or malicious.

**TP or FP?**

Review all activities performed by the app, scopes granted to the app and user activity associated with the app.

- **TP**: Apply this recommended action if you have confirmed that the app is from an unknown source and its activities are highly irregular or potentially malicious.

    **Recommended action**: Temporarily disable the app, reset the password, and then re-enable the app.
- **FP**: Apply this recommended action if you have confirmed that the detected app activity is legitimate.

    **Recommended action**: Dismiss the alert.

### Spike in Graph API calls made to OneDrive

**Severity**: Medium

A cloud app showed a significant increase in Graph API calls to OneDrive. This app might be involved in data exfiltration or other attempts to access and retrieve sensitive data.

**TP or FP?**

Review all activities performed by the app, scopes granted to the app and user activity associated with the app.

- **TP**: Apply this recommended action if you have confirmed that highly irregular, potentially malicious activities have resulted in the detected increase in OneDrive usage.

    **Recommended action**: Temporarily disable the app, reset the password, and then re-enable the app.
- **FP**: Apply this recommended action if you have confirmed that the detected app activity is legitimate.

    **Recommended action**: Dismiss the alert.

### Spike in Graph API calls made to SharePoint

**Severity**: Medium

A cloud app showed a significant increase in Graph API calls to SharePoint. This app might be involved in data exfiltration or other attempts to access and retrieve sensitive data.

**TP or FP?**

Review all activities performed by the app, scopes granted to the app and user activity associated with the app.

- **TP**: Apply this recommended action if you have confirmed that highly irregular, potentially malicious activities have resulted in the detected increase in SharePoint usage.

    **Recommended action**: Temporarily disable the app, reset the password, and then re-enable the app.
- **FP**: Apply this recommended action if you have confirmed that the detected app activity is legitimate.

    **Recommended action**: Dismiss the alert.

### Spike in Graph API calls made to Exchange

**Severity**: Medium

A cloud app showed a significant increase in Graph API calls to Exchange. This app might be involved in data exfiltration or other attempts to access and retrieve sensitive data.

**TP or FP?**

Review all activities performed by the app, scopes granted to the app and user activity associated with the app.

- **TP**: Apply this recommended action if you have confirmed that highly irregular, potentially malicious activities have resulted in the detected increase in Exchange usage.

    **Recommended action**: Temporarily disable the app, reset the password, and then re-enable the app.
- **FP**: Apply this recommended action if you have confirmed that the detected app activity is legitimate.

    **Recommended action**: Dismiss the alert.

### Suspicious app with access to multiple Microsoft 365 services

**Severity**: Medium

Find apps with OAuth access to multiple Microsoft 365 services that have exhibited statistically anomalous Graph API activity following a certificate or secret update. By identifying these apps and checking them for compromise, you can prevent lateral movement, data exfiltration, and other malicious activities that traverse cloud folders, emails, and other services.

**TP or FP?**

Review all activities performed by the app, scopes granted to the app and user activity associated with the app.

- **TP**: Apply this recommended action if you have confirmed that the updates to app certificates or secrets and other app activities have been highly irregular or potentially malicious.

    **Recommended action**: Temporarily disable the app, reset the password, and then re-enable the app.
- **FP**: Apply this recommended action if you have confirmed that the detected app activity is legitimate.

    **Recommended action**: Dismiss the alert.

### High volume of inbox rule creation activity by an app

**Severity**: Medium

An app made a large number of Graph API calls to create Exchange inbox rules. This app might be involved in data collection and exfiltration or other attempts to access and retrieve sensitive information.

**TP or FP?**

Review all activities performed by the app, scopes granted to the app and user activity associated with the app.

- **TP**: Apply this recommended action if you have confirmed that the creation of inbox rules and other activities is highly irregular or potentially malicious.

    **Recommended action**: Temporarily disable the app, reset the password, and then re-enable the app.
- **FP**: Apply this recommended action if you have confirmed that the detected app activity is legitimate.

    **Recommended action**: Dismiss the alert.

### High volume of email search activity by an app

**Severity**: Medium

An app made a large number of Graph API calls to search Exchange email content. This app might be involved in data collection or other attempts to access and retrieve sensitive information.

**TP or FP?**

Review all activities performed by the app, scopes granted to the app and user activity associated with the app.

- **TP**: Apply this recommended action if you have confirmed that the content searches on Exchange and other activities have been highly irregular or potentially malicious.

    **Recommended action**: Temporarily disable the app, reset the password, and then re-enable the app.
- **FP**: If you can confirm that no unusual mail search activities were performed by the app or that the app is intended to make unusual mail search activities through Graph API.

    **Recommended action**: Dismiss the alert.

### High volume of email sending activity by an app

**Severity**: Medium

An app made a large number of Graph API calls to send email messages using Exchange Online. This app might be involved in data collection and exfiltration or other attempts to access and retrieve sensitive information.

**TP or FP?**

Review all activities performed by the app, scopes granted to the app and user activity associated with the app.

- **TP**: Apply this recommended action if you have confirmed that the sending of email messages and other activities have been highly irregular or potentially malicious.

    **Recommended action**: Temporarily disable the app, reset the password, and then re-enable the app.
- **FP**: If you can confirm that no unusual mail send activities were performed by the app or that the app is intended to make unusual mail send activities through Graph API.

    **Recommended action**: Dismiss the alert.

### Access to sensitive data

This alert detects apps that access sensitive data in ways that might indicate risky or malicious behavior.

Note

As part of our continuous efforts to enhance Defender for Cloud apps alert accuracy, we have disabled this policy. The Access to sensitive data policy remains visible in the Defender portal in a disabled state. If you want to continue using this policy, in the Defender portal, go to **App Governance**, and then the **Policies** page. Select the policy, and then select **Activate**.

**Severity**: Medium

Find apps that access sensitive data identified by specific sensitively labels.

**TP or FP?**

To determine if the alert is a true positive (TP) or a false positive (FP), review resources accessed by the app.

- **TP**: Apply this recommended action if you have confirmed that the app or the detected activity is irregular or potentially malicious.

    **Recommended action**: Prevent the app from accessing any resources by deactivating it from Microsoft Entra ID.
- **FP**: Apply this recommended action if you have confirmed that the app has legitimate business use in the organization and the detected activity was expected.

    **Recommended action**: Dismiss the alert.