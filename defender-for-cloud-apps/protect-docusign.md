---
layout: Conceptual
title: Protect your DocuSign environment - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/protect-docusign
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
description: Connect DocuSign to Microsoft Defender for Cloud Apps by using the API connector to monitor admin activity and user sign-ins, and detect anomalous behavior.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: AmitMishaeli
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 5d1a4511-eabc-c1ad-e200-fa19c8d8482a
document_version_independent_id: 5d1a4511-eabc-c1ad-e200-fa19c8d8482a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/protect-docusign.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: protect-docusign
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/protect-docusign.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
- https://authoring-docs-microsoft.poolparty.biz/devrel/cd48b104-e308-4e08-a405-66f04a7df418
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
- https://authoring-docs-microsoft.poolparty.biz/devrel/ac23bdb5-c078-4620-8ee2-60eba45e97f8
platformId: 2cc6183d-9818-e66c-2b52-4700e5291da0
---

# Protect your DocuSign environment - Microsoft Defender for Cloud Apps | Microsoft Learn

Note

The DocuSign App Connector requires an active, paid DocuSign and DocuSign Monitor subscription to access and retrieve events.

DocuSign helps organizations manage electronic agreements, and so your DocuSign environment holds sensitive information for your organization. Any abuse of DocuSign by a malicious actor or any human error may expose your most critical assets to potential attacks.

Connecting your DocuSign environment to Defender for Cloud Apps gives you improved insights into your DocuSign admin activities and managed users sign-ins, and provides threat detection for anomalous behavior.

Use this app connector to access SaaS Security Posture Management (SSPM) features, via security controls reflected in Microsoft Secure Score. [Learn more](/en-us/microsoft-365/security/defender/microsoft-secure-score).

## Main threats to your DocuSign environment

Without Defender for Cloud Apps, your DocuSign environment is open to these threats:

- Compromised accounts and insider threats
- Data leakage
- Insufficient security awareness
- Unmanaged bring your own device (BYOD)

## Protect your environment with Defender for Cloud Apps

Use these best practices to help protect your DocuSign environment:

- [Detect cloud threats, compromised accounts, and malicious insiders](best-practices#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [Use the audit trail of activities for forensic investigations](best-practices#use-the-audit-trail-of-activities-for-forensic-investigations)

## SaaS security posture management for DocuSign

To see security posture recommendations for DocuSign in Microsoft Secure Score, create an API connector via the **Connectors** tab.

If a connector already exists and you don't see DocuSign recommendations yet, refresh the connection. Disconnect the API connector, and then reconnect it.

In Secure Score, select **Recommended actions** and filter by **Product** = **DocuSign**. DocuSign supports recommendations for session timeout and password requirements.

For more information, see:

- [Connect DocuSign to Microsoft Defender for Cloud Apps](protect-docusign#connect-docusign-to-microsoft-defender-for-cloud-apps)
- [Security posture management for SaaS apps](security-saas)
- [Microsoft Secure Score](/en-us/microsoft-365/security/defender/microsoft-secure-score)

## Control DocuSign with policies

You can use the following policies to control DocuSign activity:

| **Type** | **Name** |
| --- | --- |
| Built-in anomaly detection policy | [Activity from anonymous IP addresses](anomaly-detection-policy#activity-from-anonymous-ip-addresses)[Activity from infrequent countries/regions](anomaly-detection-policy#activity-from-infrequent-country)[Activity from suspicious IP addresses](anomaly-detection-policy#activity-from-suspicious-ip-addresses)[Impossible travel](anomaly-detection-policy#impossible-travel)[Activity performed by terminated user](anomaly-detection-policy#activity-performed-by-terminated-user) (requires Microsoft Entra ID as IdP) [Multiple failed login attempts](anomaly-detection-policy#multiple-failed-login-attempts) |
| Activity policy | Build a customized policy by the DocuSign audit log |

For more information about creating policies, see [Create a policy](control-cloud-apps-with-policies#create-a-policy).

## Automate governance controls

In addition to monitoring for potential threats, you can apply and automate the following DocuSign governance actions to remediate detected threats:

| **Type** | **Action** |
| --- | --- |
| User governance | Notify user on alert (via Microsoft Entra ID) Require user to sign in again (via Microsoft Entra ID)  Suspend user (via Microsoft Entra ID) |

For more information about remediating threats from apps, see [Governing connected apps](governance-actions).

## Protect DocuSign in real time

Review our best practices for [securing and collaborating with external users](best-practices#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls) and [blocking and protecting the download of sensitive data to unmanaged or risky devices](best-practices#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices).

## Connect DocuSign to Microsoft Defender for Cloud Apps

Use the App Connector APIs to connect Microsoft Defender for Cloud Apps to your existing DocuSign environment. This connection gives you visibility into and control over your organization’s DocuSign use.

Use this app connector to access SaaS Security Posture Management (SSPM) features, via security controls reflected in Microsoft Secure Score. [Learn more](/en-us/microsoft-365/security/defender/microsoft-secure-score).

### Prerequisites

- **DocuSign Enterprise Pro account plan with Monitor API enabled.**

    - For more information about DocuSign Monitor API, see [How to get monitoring data | DocuSign](https://developers.docusign.com/docs/monitor-api/how-to/get-monitoring-data/) and [Enable DocuSign Monitor for your organization | DocuSign](https://developers.docusign.com/docs/monitor-api/how-to/enable-monitor/).
- **DNS domains used in your organization should be claimed and validated in your DocuSign organization.** For more information on claiming and validating domains, see [Domains | DocuSign](https://support.docusign.com/en/guides/org-admin-guide-claim-domain/)
- **The DocuSign user used for logging into DocuSign must be mapped to the user role 'Docusign Administrator' and must be an organization admin of one organization only.** For more information, see the prerequisite role in [How to get monitoring data | DocuSign](https://developers.docusign.com/docs/monitor-api/how-to/get-monitoring-data/) and [Organization Administrators - DocuSign Admin for Organization Management | DocuSign Support Center](https://support.docusign.com/en/guides/org-admin-guide-org-admins).
- Due to DocuSign’s API limitation, in order to have SaaS Security Posture management (SSPM) support you need to reconnect the API connector with additional permissions: **account\_read account\_write** and **user\_read organization\_read**.
- **The DocuSign account must be mapped to an organization**. For more information, see:

    - Create new organization: [Organizations - DocuSign Admin for Organization Management | DocuSign Support Center](https://support.docusign.com/en/guides/org-admin-guide-create-org)
    - Link account to an existing organization: [Managing Accounts - DocuSign Admin for Organization Management | DocuSign Support Center](https://support.docusign.com/en/guides/org-admin-guide-accounts)
    - DocuSign Organization Admin guide: [DocuSign Admin for Organization Management (PDF) | DocuSign Support Center](https://support.docusign.com/guides/org-admin-guide).

### Configure DocuSign

Before you begin, sign in with a DocuSign account that is mapped to your organization and has Account Admin permissions. Then collect the following values to use during the connector setup:

1. Go to your DocuSign account.
2. Go to **Settings** and then **Apps and keys**.
3. Copy the User ID and Account Base URI. You'll need them later.

### Configure Defender for Cloud Apps

To create the DocuSign connector in Defender for Cloud Apps, follow these steps:

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**.
2. In the **App connectors** page, select **+Connect an app**, and then select **DocuSign**.
3. In the window that appears, give the connector a descriptive name, and then select **Next**.

    ![Screenshot of the dialog to connect DocuSign in Defender for Cloud Apps.](media/connect-docusign.png)
4. In the next screen, enter the following:

    - User ID: the User ID that you copied earlier.
    - Endpoint: the Account Base URI you copied earlier.

    ![Screenshot of the fields to enter DocuSign User ID and endpoint details.](media/docusign-details.png)
5. Select **Next**.
6. In the next screen, select **Connect DocuSign**.
7. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**. Make sure the status of the connected App Connector is **Connected**.

Note

SaaS Security Posture Management (SSPM) data will be shown in the Microsoft Defender Portal on the **Secure Score** page. For more information, see [Security posture management for SaaS apps](/en-us/defender-cloud-apps/security-saas).

## Limitations

Be aware of the following limitations when using the DocuSign connector:

- Only active DocuSign users will be shown in Defender for Cloud Apps.
    - If a user isn't active in all of the DocuSign accounts mapped to the connected DocuSign organization, the user will be shown as deleted in Defender for Cloud Apps.
- For SaaS Security Posture Management (SSPM) support, the provided credentials must have these permissions - **account\_read account\_write** and **user\_read organization\_read**.
- Defender for Cloud Apps won't show whether a user is an administrator or not.
- The DocuSign activities that will be shown in Defender for Cloud Apps are the activities at the account level (of every account that is mapped to the connected DocuSign organization) and at the organization level.