---
layout: Conceptual
title: Protect your Zendesk - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/protect-zendesk
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
description: Connect Zendesk to Microsoft Defender for Cloud Apps by using the API connector to gain visibility into admin activities and detect anomalous behavior.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: AmitMishaeli
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1016
locale: en-us
document_id: c7bc447d-2b9d-75f5-506e-20f03976e27d
document_version_independent_id: c7bc447d-2b9d-75f5-506e-20f03976e27d
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/protect-zendesk.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: protect-zendesk
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/protect-zendesk.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: d9b7b2b3-e8af-0716-c798-5749126c2a07
---

# Protect your Zendesk - Microsoft Defender for Cloud Apps | Microsoft Learn

As a customer service software solution, Zendesk holds the sensitive information to your organization. Any abuse of Zendesk by a malicious actor or any human error might expose your most critical assets and services to potential attacks.

Connecting Zendesk to Defender for Cloud Apps gives you improved insights into your Zendesk admin activities and provides threat detection for anomalous user and admin activity in Zendesk.

## Main threats to your Zendesk environment

Zendesk usage without proper protection can expose your organization to the following threats:

- Compromised accounts and insider threats
- Data leakage
- Insufficient security awareness
- Unmanaged bring your own device (BYOD)

## How Defender for Cloud Apps helps to protect your environment

Use the following Defender for Cloud Apps best practices to help protect your Zendesk environment:

- [Detect cloud threats, compromised accounts, and malicious insiders](best-practices#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [Use the audit trail of activities for forensic investigations](best-practices#use-the-audit-trail-of-activities-for-forensic-investigations)

## Control Zendesk with policies

The following table lists the policy types you can use to monitor and control Zendesk activity:

| Type | Name |
| --- | --- |
| Built-in anomaly detection policy | [Activity from anonymous IP addresses](anomaly-detection-policy#activity-from-anonymous-ip-addresses)[Activity from infrequent country](anomaly-detection-policy#activity-from-infrequent-country)[Activity from suspicious IP addresses](anomaly-detection-policy#activity-from-suspicious-ip-addresses)[Impossible travel](anomaly-detection-policy#impossible-travel)[Activity performed by terminated user](anomaly-detection-policy#activity-performed-by-terminated-user) (requires Microsoft Entra ID as IdP) [Multiple failed login attempts](anomaly-detection-policy#multiple-failed-login-attempts)[Unusual administrative activities](anomaly-detection-policy#unusual-activities-by-user)[Unusual impersonated activities](anomaly-detection-policy#unusual-activities-by-user) |
| Activity policy | Built a customized policy by the Zendesk audit log |

For more information about creating policies, see [Create a policy](control-cloud-apps-with-policies#create-a-policy).

## Automate governance controls

In addition to monitoring for potential threats, you can apply and automate the following Zendesk governance actions to remediate detected threats:

| Type | Action |
| --- | --- |
| User governance | Notify user on alert (via Microsoft Entra ID) Require user to sign in again (via Microsoft Entra ID)  Suspend user (via Microsoft Entra ID) |

For more information about remediating threats from apps, see [Governing connected apps](governance-actions).

## Protect Zendesk in real time

Review our best practices for [securing and collaborating with external users](best-practices#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls) and [blocking and protecting the download of sensitive data to unmanaged or risky devices](best-practices#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices).

## SaaS security posture management for Zendesk

Software as a Service (SaaS) security posture management helps you evaluate and improve the security configuration of your SaaS apps. After you connect Zendesk to Microsoft Defender for Cloud Apps, you automatically get security posture recommendations for Zendesk in Microsoft Secure Score. In Secure Score, select **Recommended actions** and filter by **Product** = **Zendesk**. For example, recommendations for Zendesk include:

- *Enable multifactor authentication (MFA)*
- *Enable session timeout for users*
- *Enable IP restrictions*
- *Block admins to set passwords.*

For more information, see:

- [Security posture management for SaaS apps](security-saas)
- [Microsoft Secure Score](/en-us/microsoft-365/security/defender/microsoft-secure-score)

## Connect Zendesk to Microsoft Defender for Cloud Apps

The following instructions explain how to connect Microsoft Defender for Cloud Apps to your existing Zendesk using the App Connector APIs. This connection gives you visibility into and control over your organization's Zendesk use.

### Prerequisites

- The Zendesk user used for logging into Zendesk must be an admin.
- Supported Zendesk licenses:
    - Enterprise
    - Enterprise Plus

Note

Connecting Zendesk to Defender for Cloud Apps with a Zendesk user that isn't an admin will result in a connection error.

### Configure Zendesk

Perform the following steps in Zendesk to create the OAuth credentials required for the connector:

1. Select **Add OAuth client**.
2. Select **New Credential**. Fill out the following fields:

    - Client name: **Microsoft Defender for Cloud Apps** (you can also choose another name).
    - Description: **Microsoft Defender for Cloud Apps API Connector** (you can also choose another description).
    - Company: **Microsoft Defender for Cloud Apps** (you can also choose another company).
    - Unique identifier: **microsoft\_cloud\_app\_security** (you can also choose another unique identifier).
    - Client Kind: **Confidential**
    - Redirect URL: `https://portal.cloudappsecurity.com/api/oauth/saga`

        Note

        - For US Government GCC customers, enter the following value: `https://portal.cloudappsecuritygov.com/api/oauth/saga`
        - For US Government GCC High customers, enter the following value: `https://portal.cloudappsecurity.us/api/oauth/saga`
3. Copy the **Secret** that was generated. You'll need it in the upcoming steps.

### Configure Defender for Cloud Apps

Note

The Zendesk user that's configuring the integration must always remain a Zendesk admin, even after the connector is installed.

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**.
2. In the **App connectors** page, select **+Connect an app**, followed by **Zendesk**.
3. In the next window, give the connector a descriptive name, and select **Next**.

    [![Screenshot that shows where to add the instance name in the Defender portal.](media/connect-zendesk.png)](media/connect-zendesk.png#lightbox)
4. In the **Enter details** page, enter the following fields, and then select **Next**.

    - **Client ID**: the Unique identifier you used when you created the OAuth app in the Zendesk admin portal.
    - **Client Secret**: your saved secret.
    - **Client endpoint**: Zendesk URL. It should be `<account_name>.zendesk.com`.
5. In the **External link** page, select **Connect Zendesk**.
6. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**. Make sure the status of the connected App Connector is **Connected**.
7. The first connection can take up to four hours to get all users and their activities in the seven days before the connection.
8. After the connector's **Status** is marked as **Connected**, the connector is live and works.

Note

- Microsoft recommends using a short lived access token. Zendesk doesn't currently support short lived tokens. We recommend refreshing your token every 6 months as a security best practice. To refresh and revoke an old access token see: [Revoke Token](https://developer.zendesk.com/api-reference/ticketing/oauth/oauth_tokens/#revoke-token). After you revoke the old token, create a new secret and reconnect the Zendesk connector.
- System activities are shown with the **Zendesk** account name.

## Zendesk connector rate limits

The default rate limit is 200 requests per minute. To increase the rate limit, [open a support ticket](/en-us/defender-xdr/contact-defender-support).

For more information about the maximum rate limit for every subscription, see: [Zendesk Suite plan limits](https://developer.zendesk.com/api-reference/ticketing/account-configuration/usage_limits/#zendesk-support-plan-limits).