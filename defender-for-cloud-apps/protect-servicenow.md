---
layout: Conceptual
title: Protect your ServiceNow environment - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/protect-servicenow
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
description: Connect ServiceNow to Microsoft Defender for Cloud Apps with the API connector to monitor user activity and detect anomalous behavior and sensitive data exposure.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: AmitMishaeli
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: b8f76f5b-175e-df62-3770-8fff9b98a632
document_version_independent_id: b8f76f5b-175e-df62-3770-8fff9b98a632
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/protect-servicenow.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: protect-servicenow
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/protect-servicenow.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/cd48b104-e308-4e08-a405-66f04a7df418
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ac23bdb5-c078-4620-8ee2-60eba45e97f8
platformId: c0b03a82-31ce-1dea-51af-28697f969e33
---

# Protect your ServiceNow environment - Microsoft Defender for Cloud Apps | Microsoft Learn

ServiceNow is a major CRM cloud provider. It stores sensitive data about customers, internal processes, incidents, and reports. As a business-critical app, people both inside and outside your organization use it, including partners and contractors. Many of these users might not follow security best practices. They could share sensitive data without meaning to. Malicious actors might also try to access your most sensitive customer assets.

Connecting ServiceNow to Defender for Cloud Apps improves insights into your users' activities. It also helps detect threats using machine-learning anomaly detection and information protection, such as identifying when sensitive customer data is uploaded to ServiceNow.

Use this app connector to access SaaS Security Posture Management (SSPM) features, via security controls reflected in Microsoft Secure Score. [Learn more](/en-us/microsoft-365/security/defender/microsoft-secure-score).

## Main threats

Connecting ServiceNow to Defender for Cloud Apps helps you address the following threats:

- Compromised accounts and insider threats
- Data leakage
- Insufficient security awareness
- Unmanaged bring your own device (BYOD)

## Protect your environment with Defender for Cloud Apps

You can protect your ServiceNow environment in these ways:

- [Detect cloud threats, compromised accounts, and malicious insiders](best-practices#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [Discover, classify, label, and protect regulated and sensitive data stored in the cloud](best-practices#discover-classify-label-and-protect-regulated-and-sensitive-data-stored-in-the-cloud)
- [Enforce DLP and compliance policies for data stored in the cloud](best-practices#enforce-dlp-and-compliance-policies-for-data-stored-in-the-cloud)
- [Limit exposure of shared data and enforce collaboration policies](best-practices#limit-exposure-of-shared-data-and-enforce-collaboration-policies)
- [Use the audit trail of activities for forensic investigations](best-practices#use-the-audit-trail-of-activities-for-forensic-investigations)

## SaaS security posture management for ServiceNow

Connect ServiceNow to Microsoft Defender for Cloud Apps to get security tips for ServiceNow in Microsoft Secure Score.

In Secure Score, select **Recommended actions**. Filter by **Product** = **ServiceNow**. Examples include:

- *Enable MFA*
- *Activate the explicit role plugin*
- *Enable high security plugin*
- *Enable script request authorization*

For more information, see:

- [Security posture management for SaaS apps](security-saas)
- [Microsoft Secure Score](/en-us/microsoft-365/security/defender/microsoft-secure-score)

## Control ServiceNow with built-in policies and policy templates

You can use the following built-in policy templates to detect and notify you about potential threats:

Important

File policies retire on January 6, 2027. To maintain file-based data protection for this app, [migrate to Microsoft Purview DLP or auto-labeling policies](migrate-file-policies-to-purview).

| Type | Name |
| --- | --- |
| Built-in anomaly detection policy | [Activity from anonymous IP addresses](anomaly-detection-policy#activity-from-anonymous-ip-addresses)[Activity from infrequent country](anomaly-detection-policy#activity-from-infrequent-country) |
| [Activity from suspicious IP addresses](anomaly-detection-policy#activity-from-suspicious-ip-addresses)[Impossible travel](anomaly-detection-policy#impossible-travel)[Activity performed by terminated user](anomaly-detection-policy#activity-performed-by-terminated-user) (requires Microsoft Entra ID as IdP)[Multiple failed login attempts](anomaly-detection-policy#multiple-failed-login-attempts)[Ransomware detection](anomaly-detection-policy#ransomware-activity)[Unusual multiple file download activities](anomaly-detection-policy#unusual-activities-by-user) |  |
| Activity policy template | Logon from a risky IP addressMass download by a single user |
| File policy template | Detect a file shared with an unauthorized domainDetect a file shared with personal email addressesDetect files with PII/PCI/PHI |

For more information about creating policies, see [Create a policy](control-cloud-apps-with-policies#create-a-policy).

## Automate governance controls

You can also automate ServiceNow governance actions to fix detected threats. These actions run through Microsoft Entra ID:

| Type | Action |
| --- | --- |
| User governance | - Notify user on alert (via Microsoft Entra ID)- Require user to sign in again (via Microsoft Entra ID)- Suspend user (via Microsoft Entra ID) |

For more information about remediating threats from apps, see [Governing connected apps](governance-actions).

## Protect ServiceNow in real time

Review our best practices for [securing and collaborating with external users](best-practices#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls) and [blocking and protecting the download of sensitive data to unmanaged or risky devices](best-practices#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices).

## Connect ServiceNow to Microsoft Defender for Cloud Apps

Use the app connector API to connect Microsoft Defender for Cloud Apps to your existing ServiceNow account. The ServiceNow app connector gives you visibility into and control over ServiceNow use. For threat detection, governance controls, and real-time protection guidance, see [Protect ServiceNow](protect-servicenow).

Use this app connector to access SaaS Security Posture Management (SSPM) features, via security controls reflected in Microsoft Secure Score. [Learn more](/en-us/microsoft-365/security/defender/microsoft-secure-score).

### Prerequisites

- In order to connect ServiceNow with Defender for Cloud Apps,
- Your ServiceNow instance must support API access.
- You must have an admin role.
- The admin account used to make the connection must have permissions to use the API.

Defender for Cloud Apps supports the following ServiceNow versions:

- Eureka
- Fiji
- Geneva
- Helsinki
- Istanbul
- Jakarta
- Kingston
- London
- Madrid
- New York
- Orlando
- Paris
- Quebec
- Rome
- San Diego
- Tokyo
- Utah
- Vancouver
- Washington
- Xanadu
- Yokohama
- Zurich
- Australia

For more information, see [ServiceNow OAuth applications documentation](https://docs.servicenow.com/bundle/paris-platform-administration/page/administer/security/concept/c_OAuthApplications.html#c_OAuthApplications).

Tip

We recommend deploying ServiceNow using OAuth app tokens, available for Fuji and later releases. For more information, see [Configure OAuth applications in ServiceNow](https://docs.servicenow.com/bundle/paris-platform-administration/page/administer/security/concept/c_OAuthApplications.html#c_OAuthApplications).

For earlier releases, a legacy connection mode is used that uses usernames and passwords The username and password provided are only used for API token generation and aren't saved after the initial connection process.

### How to connect ServiceNow to Defender for Cloud Apps using OAuth

Perform the following steps to create an OAuth profile in ServiceNow and connect it to Defender for Cloud Apps:

1. Sign in with an Admin account to your ServiceNow account.

    Note

    For earlier releases, a legacy connection mode is available based on user/password. The username/password provided are only used for API token generation and aren't saved after the initial connection process.
2. Create a new OAuth profile and then select **Create an OAuth API endpoint for external clients**.
3. Fill in the following **Application Registries New record** fields:

    1. Enter a name for your OAuth profile, for example, CloudAppSecurity.
    2. Copy the **Client ID**. You'll need it later.
    3. In the **Client Secret** field, enter a string. If left empty, a random secret is generated automatically. Copy and save it for later.
    4. Increase the **Access Token Lifespan** to at least 3,600.
    5. Change the **Scope Restriction** value to **Broadly Scoped**.
4. Select the name of the OAuth that was defined, and change the **Refresh Token Lifespan** to **7,776,000 seconds** (90 days).
5. Establish an internal procedure to ensure that the connection remains active.

    1. Make sure to revoke the old refresh token before the expected expiration of the refresh token.
    2. In the Microsoft Defender Portal, edit the existing connector, using the same client ID and client secret. This will generate a new refresh token.

    Note

    Token rotation is a recurring process every 90 days. Without refreshing the token before expiration, the ServiceNow connection will stop working.

### Connect ServiceNow to Microsoft Defender for Cloud Apps

To complete the connection in the Microsoft Defender Portal, follow these steps:

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**.
2. In the **App connectors** page, select **+Connect an app**, and then **ServiceNow**.

    ![Screenshot that shows where to find the ServiceNow connector in the Defender portal.](media/connect-servicenow.png)
3. In the next window, give the connection a name and select **Next**.
4. In the **Enter details** page, select **Connect using OAuth token (recommended)**. Select **Next**.

    ![Screenshot of the ServiceNow App Connector Details Dialog.](media/servicenow-app-connector-details-screenshot.png)
5. To find your ServiceNow user name, in the ServiceNow portal, go to **Users** and then locate your name in the table. (Optional) To use a non-admin user for this step, create a non-admin user by following the steps in the below section.
6. In the **OAuth Details** page, enter your **Client ID** and **Client Secret**. Select **Next**.
7. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**. Make sure the status of the connected App Connector is **Connected**.

After connecting ServiceNow, you'll receive events for 1 hour prior to connection.

### Optional: Create a non-admin user in ServiceNow

#### Step 1: Create custom access control lists (ACLs) in ServiceNow

1. Sign in to ServiceNow with an administrator account.
2. Open the **Elevate Roles** menu and enable both **admin** and **security\_admin**. These elevated roles are required to create ACLs for certain tables.
3. Navigate to **Access Control (ACL)** configuration.
4. Create a **Read**ACL for each of the following tables:
    - sys\_user
    - sys\_user\_group
    - sys\_user\_grmember
    - sys\_user\_has\_role
    - sys\_properties
    - v\_plugin
    - sysevent\_script\_action
    - sys\_attachment
    - sys\_attachment\_doc
    - sysevent
    - syslog\_transaction
    - incident
    - sys\_user\_role\_contains
5. For each ACL, set **Type** = **record**, **Operation** = **read**, **Name** = the table name, and **Required Role** = a custom role such as **custom\_table\_access**.
6. Use the same custom role across all ACLs to simplify management.

#### Step 2: Create a non-admin user

1. In ServiceNow, go to **User Administration** &gt; **Users**.
2. Create a new user account.
3. Record the username and password for later use in the integration setup.
4. Open the newly created user profile.
5. Scroll to the **Roles** section.
6. Assign the custom role created in Step 1 (for example, **custom\_table\_access**) to the user.

### Legacy ServiceNow connection

To connect ServiceNow with Defender for Cloud Apps, you must have admin-level permissions and make sure the ServiceNow instance supports API access.

1. Sign in with an Admin account to your ServiceNow account.
2. Create a new service account for Defender for Cloud Apps and attach the Admin role to the newly created account.
3. Make sure the REST API plug-in is turned on.