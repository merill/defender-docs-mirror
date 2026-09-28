---
layout: Conceptual
title: Protect your NetDocuments environment - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/protect-netdocuments
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
description: Connect NetDocuments to Microsoft Defender for Cloud Apps by using the API connector to gain visibility into activity and detect anomalous behavior.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: AmitMishaeli
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: a1429740-fd5f-41ca-8e2e-383039e2f206
document_version_independent_id: a1429740-fd5f-41ca-8e2e-383039e2f206
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/protect-netdocuments.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: protect-netdocuments
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/protect-netdocuments.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 7dedd04b-b1d0-e8b0-09fa-674573eaf105
---

# Protect your NetDocuments environment - Microsoft Defender for Cloud Apps | Microsoft Learn

NetDocuments is a cloud solution for productivity and collaboration that stores sensitive data. Misuse by a bad actor or a human error can expose critical assets to attacks.

Connect NetDocuments to Defender for Cloud Apps to get better visibility into user activity and detect unusual behavior.

## Main threats to your NetDocuments environment

NetDocuments environments face the following key security threats:

- Compromised accounts and insider threats
- Data leakage
- Insufficient security awareness
- Unmanaged bring your own device (BYOD)

## How Defender for Cloud Apps helps to protect your environment

Defender for Cloud Apps helps protect your NetDocuments environment with the following best practices:

- [Detect cloud threats, compromised accounts, and malicious insiders](best-practices#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [Use the audit trail of activities for forensic investigations](best-practices#use-the-audit-trail-of-activities-for-forensic-investigations)

## Control NetDocuments with policies

The following table lists the policy types you can use to control NetDocuments:

| **Type** | **Name** |
| --- | --- |
| Built-in anomaly detection policy | [Activity from anonymous IP addresses](anomaly-detection-policy#activity-from-anonymous-ip-addresses)[Activity from infrequent country](anomaly-detection-policy#activity-from-infrequent-country)[Activity from suspicious IP addresses](anomaly-detection-policy#activity-from-suspicious-ip-addresses)[Impossible travel](anomaly-detection-policy#impossible-travel)[Activity performed by terminated user](anomaly-detection-policy#activity-performed-by-terminated-user) (requires Microsoft Entra ID as the identity provider (IdP)) [Unusual file share activities](anomaly-detection-policy#unusual-activities-by-user)[Unusual file deletion activities](anomaly-detection-policy#unusual-activities-by-user)[Unusual administrative activities](anomaly-detection-policy#unusual-activities-by-user)[Unusual multiple file download activities](anomaly-detection-policy#unusual-activities-by-user) |
| Activity policy | Built a customized policy by the NetDocuments [Audit Log](https://support.netdocuments.com/hc/en-us/articles/205220260-Consolidated-Activity-Log) activities |

Note

Login/Logouts activities aren't supported by NetDocuments.

For more information about creating policies, see [Create a policy](control-cloud-apps-with-policies#create-a-policy) .

## Automate governance controls

You can also apply and automate NetDocuments governance actions to fix detected threats:

| **Type** | **Action** |
| --- | --- |
| User governance | Notify user on alert (via Microsoft Entra ID) Require user to sign in again (via Microsoft Entra ID)  Suspend user (via Microsoft Entra ID) |

To learn more about fixing threats from apps, see [Governing connected apps](governance-actions).

## Protect NetDocuments in real time

Review our best practices for [securing and collaborating with external users](best-practices#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls) and [blocking and protecting the download of sensitive data to unmanaged or risky devices](best-practices#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices).

## SaaS security posture management (Preview)

After you connect NetDocuments to Defender for Cloud Apps, you automatically get security posture recommendations for NetDocuments in Microsoft Secure Score. In Secure Score, select **Recommended actions** and filter by **Product** = **NetDocument**. NetDocument supports security recommendations to *Adopt SSO (Single sign on) in NetDocument*.

To learn more, see:

- [Security posture management for SaaS apps](security-saas)
- [Microsoft Secure Score](/en-us/microsoft-365/security/defender/microsoft-secure-score)

## Connect NetDocuments to Microsoft Defender for Cloud Apps

This section provides instructions for connecting Microsoft Defender for Cloud Apps to your existing NetDocuments account using the App Connector APIs. The Defender for Cloud Apps connection to NetDocuments gives administrators visibility into and control over their organization's NetDocuments use.

### Configure NetDocuments

Perform the following steps in NetDocuments to collect the values needed for the connector setup:

1. Sign in to your NetDocuments account with a Full NetDocuments Repository Admin user.
2. Copy your repository ID. You enter the repository ID in the **Repository ID** field when you configure Defender for Cloud Apps.
3. Copy your account URL. You enter the account URL in the **Application URL** field when you configure Defender for Cloud Apps. Make sure that the account URL matches one of the following NetDocuments service URLs.

    | Location | URL |
    | --- | --- |
    | United Kingdom | https://eu.netdocuments.com |
    | Australia | https://au.netdocuments.com |
    | Germany | https://de.netdocuments.com |
    | United States or any other location | https://vault.netvoyage.com |

### Configure Defender for Cloud Apps

Perform the following steps in Defender for Cloud Apps to create the NetDocuments connector:

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**.
2. In the **App connectors** page, select **+Connect an app**, followed by **NetDocuments**.
3. In the connector setup window, give the connector a descriptive name, and select **Next**.

    ![Screenshot of the NetDocuments connection screen prompting the user to name the connector.](media/netdocuments-connecting-screen.png)
4. In the **Enter details** screen, enter the **Repository ID** and **Application URL** values:

    - **Repository ID**: the app repository ID that you saved.
    - **Application URL**: the URL that you saved.
5. Select **Next**.
6. Select **Connect NetDocuments**.
7. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**. Make sure the status of the connected App Connector is **Connected**.

## Rate limits and limitations

Be aware of the following rate limits and limitations for the NetDocuments connector:

- The default rate limit is 100,000 requests per minute.
- Login/Logouts activities aren't supported by NetDocuments.