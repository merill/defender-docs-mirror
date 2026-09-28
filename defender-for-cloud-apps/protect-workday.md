---
layout: Conceptual
title: Protect your Workday environment - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/protect-workday
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
description: Connect Workday to Microsoft Defender for Cloud Apps with the API connector to monitor user activity and detect anomalous behavior.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: AmitMishaeli
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 5e63cbe7-5ad6-1b71-ce43-138b6c84011a
document_version_independent_id: 5e63cbe7-5ad6-1b71-ce43-138b6c84011a
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/protect-workday.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: protect-workday
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/protect-workday.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/12ed19f9-ebdf-4c8a-8bcd-7a681836774d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/3a764584-4f97-452b-8f1d-36f19b12f6ae
platformId: ddf7b97b-bdbe-7b48-f201-ad29ea6395e1
---

# Protect your Workday environment - Microsoft Defender for Cloud Apps | Microsoft Learn

As a major HCM solution, Workday holds some of the most sensitive information in your organization such as employees' personal data, contracts, vendor details, and more. Preventing exposure of this data requires continuous monitoring to prevent any malicious actors or security unaware insiders from exfiltrating the sensitive information.

Connecting Workday to Defender for Cloud Apps gives you improved insights into your users' activities and provides threat detection for anomalous behavior. Before you begin, review the prerequisites for connecting Workday to Defender for Cloud Apps.

## Main threats to your Workday environment

Workday deployments commonly face the following threats:

- Compromised accounts and insider threats
- Data leakage
- Insufficient security awareness
- Unmanaged bring your own device (BYOD)

## How Defender for Cloud Apps helps to protect your environment

Use the following guidance to help protect your Workday environment with Defender for Cloud Apps:

- [Detect cloud threats, compromised accounts, and malicious insiders](best-practices#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [Use the audit trail of activities for forensic investigations](best-practices#use-the-audit-trail-of-activities-for-forensic-investigations)

## Control Workday with built-in policies and policy templates

You can use the following built-in policy templates to detect and notify you about potential threats:

| Type | Name |
| --- | --- |
| Built-in anomaly detection policy | [Activity from anonymous IP addresses](anomaly-detection-policy#activity-from-anonymous-ip-addresses)[Activity from infrequent country](anomaly-detection-policy#activity-from-infrequent-country)[Activity from suspicious IP addresses](anomaly-detection-policy#activity-from-suspicious-ip-addresses)[Impossible travel](anomaly-detection-policy#impossible-travel) |
| Activity policy template | Logon from a risky IP address |

For more information about creating policies, see [Create a policy for controlling cloud apps](control-cloud-apps-with-policies#create-a-policy).

## Automate governance controls

Currently, there are no governance controls available for Workday. If you are interested in having governance actions for this connector, you can [contact Microsoft Defender support](/en-us/defender-xdr/contact-defender-support) with details of the actions you want.

For more information about remediating threats from apps, see [Governing connected apps](governance-actions).

## Protect Workday in real time

Review our best practices for [securing and collaborating with external users](best-practices#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls) and [blocking and protecting the download of sensitive data to unmanaged or risky devices](best-practices#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices).

## Connect Workday to Microsoft Defender for Cloud Apps

The following instructions explain how to connect Microsoft Defender for Cloud Apps to your existing Workday account using the app connector API. Connecting Defender for Cloud Apps to your Workday account through the app connector API gives you visibility into and control over Workday use. For information about how Defender for Cloud Apps protects Workday, see [Protect Workday](protect-workday).

### Quick start: Connect Workday to Defender for Cloud Apps

Watch our quick start video showing how to configure the prerequisites and perform the steps in Workday. Once you've completed the Workday prerequisite and configuration steps shown in the quick start video, you can proceed to add the Workday connector.

Note

The video does not show the prerequisite step for configuring the security group **Set Up: Tenant Setup – System** permission. Make sure you configure the **Set Up: Tenant Setup – System** permission as well.

### Prerequisites

The Workday account used for connecting to Defender for Cloud Apps must be a member of a security group (new or existing). We recommended using a Workday Integration System User. The security group must have the following permissions selected for the following domain security policies:

| Functional area | Domain Security policy | Subdomain Security policy | Report/Task Permissions | Integration Permissions |
| --- | --- | --- | --- | --- |
| System | Set Up: Tenant Setup – General | Set Up: Tenant Setup – Security | View | Get, Put |
| System | Set Up: Tenant Setup – General | Set Up: Tenant Setup – System | View | None |
| System | Security Administration |  | View | Get, Put |
| System | System auditing |  | View | Get |
| Staffing | Worker Data: Staffing | Worker Data: Public Worker Reports | View | Get |

Note

- The account that is used to set up permissions for the security group must be a Workday Administrator.
- To set permissions, search for "Domain Security Policies for Functional Area", then search for each functional area ("System"/"Staffing") and grant the permissions listed in the table.
- Once all permissions have been set, search for "Activate Pending Security Policy Changes" and approve the changes.

For more information about setting up Workday integration users, security groups, and permissions, see steps 1 to 4 of the [Grant Integration or External Endpoint Access to Workday](https://go.microsoft.com/fwlink/?linkid=2103212) guide (accessible with Workday documentation/community credentials).

### How to connect Workday to Defender for Cloud Apps using OAuth

Perform the following steps in Workday to prepare the OAuth connection:

1. Sign in to Workday with an account that is a member of the security group mentioned in the prerequisites.
2. Search for "Edit tenant setup – system", and under **User Activity Logging**, select **Enable User Activity Logging**.

    ![Screenshot of the Workday tenant setup page with the Enable User Activity Logging option selected.](media/connect-workday-enable-logging.png)
3. Search for "Edit tenant setup – security", and under **OAuth 2.0 Settings**, select **OAuth 2.0 Clients Enabled**.
4. Search for "Register API Client" and select **Register API Client – Task**.
5. On the **Register API Client** page, fill out the following information, and then select **OK**.

    | Field name | Value |
    | --- | --- |
    | Client Name | Microsoft Defender for Cloud Apps |
    | Client Grant Type | Authorization Code Grant |
    | Access Token Type | Bearer |
    | Redirection URI | `https://portal.cloudappsecurity.com/api/oauth/connect`**Note**: For US Government GCC High customers, enter the following value: `https://portal.cloudappsecurity.us/api/oauth/connect` |
    | Non-Expiring Refresh Tokens | Yes |
    | Scope (Functional Areas) | **Staffing** and **System** |

    ![Screenshot of the Workday Register API Client page with client name, grant type, and scope fields.](media/connect-workday-register-api-client.png)
6. Once registered, make a note for the following parameters, and then select **Done**.

    - Client ID
    - Client Secret
    - Workday REST API Endpoint
    - Token Endpoint
    - Authorization Endpoint

    ![Screenshot of the Workday API client registration confirmation showing the Client ID, Client Secret, and endpoint values.](media/connect-workday-register-api-client-confirm.png)

Note

If the Workday account is enabled with SAML SSO, then append the query string parameter `'redirect=n'` to the authorization endpoint.

If the authorization endpoint already has other query string parameters, then append `'&redirect=n'` to the end of authorization endpoint. If the authorization endpoint doesn't have any query string parameters, then append `'?redirect=n'` to the end of authorization endpoint.

### How to connect Defender for Cloud Apps to Workday

Complete the following steps in Microsoft Defender for Cloud Apps to add the Workday connector:

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**.
2. In the **App connectors** page, select **+Connect an app**, and then **Workday**.

    ![Screenshot of the App Connectors page with the Connect an app option and Workday selected.](media/connect-workday-add-app.png)
3. In the next screen, give your connector a name and then select **Next**.

    ![Screenshot of the Workday app connector setup page with the connector instance name field.](media/connect-workday-add-app-connect.png)
4. On the **Enter details** page, enter the Client ID, Client Secret, Workday REST API Endpoint, Token Endpoint, and Authorization Endpoint values that you noted during Workday API client registration, and then select **Next**.

    ![Screenshot of the Workday connector Enter details page with Client ID, Client Secret, and endpoint fields.](media/connect-workday-add-app-connect-details.png)
5. In the **External link** page, select **Connect Workday**.
6. In Workday, a pop-up appears asking you if you want to allow Defender for Cloud Apps access to your Workday account. To proceed, select **Allow**.

    ![Screenshot of the Workday permission prompt asking to allow Defender for Cloud Apps access to the account.](media/connect-workday-add-app-allow.png)
7. In Defender for Cloud Apps, you should see a message that Workday was successfully connected.
8. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**. Make sure the status of the connected App Connector is **Connected**.

Note

After connecting Workday, you'll receive events for seven days prior to connection.

Note

If you are connecting Defender for Cloud Apps to a Workday sandbox account for testing, note that Workday refreshes their sandbox account every week, causing the Defender for Cloud Apps connection to fail. You should reconnect the sandbox environment every week with Defender for Cloud Apps to continue testing.

If you have any problems connecting the app, see [Troubleshooting App Connectors](troubleshooting-api-connectors-using-error-messages).