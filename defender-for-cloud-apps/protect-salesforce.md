---
layout: Conceptual
title: Protect your Salesforce environment - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/protect-salesforce
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
description: Connect Salesforce to Microsoft Defender for Cloud Apps using the API connector to monitor user activity, detect threats and external sharing, and enable automated remediation.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: AmitMishaeli
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 6d7f0dc5-6f56-c224-d266-830a452c9fee
document_version_independent_id: 6d7f0dc5-6f56-c224-d266-830a452c9fee
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/protect-salesforce.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: protect-salesforce
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/protect-salesforce.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/cd48b104-e308-4e08-a405-66f04a7df418
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/ac23bdb5-c078-4620-8ee2-60eba45e97f8
platformId: 2cb98b5b-2d0d-9649-e0d1-0e647068cb8e
---

# Protect your Salesforce environment - Microsoft Defender for Cloud Apps | Microsoft Learn

As a major CRM cloud provider, Salesforce incorporates large amounts of sensitive information about customers, pricing playbooks, and major deals inside your organization. Being a business-critical app, people inside your organization and others outside of it (such as partners and contractors) access and use Salesforce for various purposes. In many cases, a large proportion of your users accessing Salesforce have low awareness of security and might put your sensitive information at risk by unintentionally sharing it. In other instances, malicious actors might gain access to your most sensitive customer-related assets.

Connecting Salesforce to Defender for Cloud Apps gives you improved insights into your users' activities, provides threat detection using machine learning based anomaly detections and information protection detections (such as detecting external information sharing). Defender for Cloud Apps also enables automated remediation controls, and detects threats from enabled third-party apps in your organization. Before you begin, review the prerequisites for connecting Salesforce to Defender for Cloud Apps.

Use this app connector to access SaaS Security Posture Management (SSPM) features, via security controls reflected in Microsoft Secure Score. [Learn more](/en-us/microsoft-365/security/defender/microsoft-secure-score).

## Main threats to your Salesforce environment

Connecting Salesforce to Defender for Cloud Apps helps you detect and respond to these key threats:

- Compromised accounts and insider threats
- Data leakage
- Elevated privileges
- Insufficient security awareness
- Malicious third-party apps and Google add-ons
- Ransomware
- Unmanaged bring your own device (BYOD)

## How Defender for Cloud Apps helps to protect your environment

Defender for Cloud Apps helps protect your Salesforce environment in the following ways:

- [Detect cloud threats, compromised accounts, and malicious insiders](best-practices#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [Discover, classify, label, and protect regulated and sensitive data stored in the cloud](best-practices#discover-classify-label-and-protect-regulated-and-sensitive-data-stored-in-the-cloud)
- [Discover and manage OAuth apps that have access to your environment](manage-app-permissions)
- [Enforce DLP and compliance policies for data stored in the cloud](best-practices#enforce-dlp-and-compliance-policies-for-data-stored-in-the-cloud)
- [Limit exposure of shared data and enforce collaboration policies](best-practices#limit-exposure-of-shared-data-and-enforce-collaboration-policies)
- [Use the audit trail of activities for forensic investigations](best-practices#use-the-audit-trail-of-activities-for-forensic-investigations)

## SaaS security posture management for Salesforce

Connect Salesforce to Microsoft Defender for Cloud Apps to automatically get security recommendations for Salesforce in Microsoft Secure Score. For connection steps, see Connect Salesforce to Microsoft Defender for Cloud Apps.

In Secure Score, select **Recommended actions** and filter by **Product** = **Salesforce**. For example, recommendations for Salesforce include:

- *Require identity verification during multifactor authentication (MFA) registration*
- *Enforce login IP ranges on every request*
- *Maximum invalid login attempts*
- *Password complexity requirement*

For more information, see:

- [Security posture management for SaaS apps](security-saas)
- [Microsoft Secure Score](/en-us/microsoft-365/security/defender/microsoft-secure-score)

## Control Salesforce with built-in policies and policy templates

Use the following built-in policy templates to detect and get notifications about potential threats:

Important

File policies retire on January 6, 2027. To maintain file-based data protection for this app, [migrate to Microsoft Purview DLP or auto-labeling policies](migrate-file-policies-to-purview).

| Type | Name |
| --- | --- |
| Built-in anomaly detection policy | [Activity from anonymous IP addresses](anomaly-detection-policy#activity-from-anonymous-ip-addresses)[Activity from infrequent country](anomaly-detection-policy#activity-from-infrequent-country)[Activity from suspicious IP addresses](anomaly-detection-policy#activity-from-suspicious-ip-addresses)[Impossible travel](anomaly-detection-policy#impossible-travel)[Activity performed by terminated user](anomaly-detection-policy#activity-performed-by-terminated-user) (requires Microsoft Entra ID as IdP)[Multiple failed login attempts](anomaly-detection-policy#multiple-failed-login-attempts)[Unusual administrative activities](anomaly-detection-policy#unusual-activities-by-user)[Unusual file deletion activities](anomaly-detection-policy#unusual-activities-by-user) (Temporarily not supported due to limitation in Salesforce API)[Unusual file share activities](anomaly-detection-policy#unusual-activities-by-user)[Unusual impersonated activities](anomaly-detection-policy#unusual-activities-by-user)[Unusual multiple file download activities](anomaly-detection-policy#unusual-activities-by-user) |
| Activity policy template | Logon from a risky IP addressMass download by a single user |
| File policy template | Detect a file shared with an unauthorized domainDetect a file shared with personal email addresses |

For more information about creating policies, see [Create a policy](control-cloud-apps-with-policies#create-a-policy).

## Automate governance controls

In addition to monitoring for potential threats, you can apply and automate the following Salesforce governance actions to remediate detected threats:

| Type | Action |
| --- | --- |
| User governance | - Notify users of pending alerts- Send DLP violation digest to file owners- Suspend user- Notify user on alert (via Microsoft Entra ID)- Require user to sign in again (via Microsoft Entra ID)- Suspend user (via Microsoft Entra ID) |
| OAuth app governance | - Revoke OAuth app for users |

For more information about remediating threats from apps, see [Governing connected apps](governance-actions).

## Protect Salesforce in real time

Review our best practices for [securing and collaborating with external users](best-practices#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls) and [blocking and protecting the download of sensitive data to unmanaged or risky devices](best-practices#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices).

## Connect Salesforce to Microsoft Defender for Cloud Apps

Use the following prerequisites and steps to connect Salesforce to Microsoft Defender for Cloud Apps.

### Prerequisites

SaaS security posture management (SSPM) doesn't require Salesforce Shield. For all other integrations, make sure that Salesforce Shield is available for your Salesforce instance.

Use the following instructions to connect Microsoft Defender for Cloud Apps to your existing Salesforce account using the app connector API. The Salesforce app connector gives you visibility into and control over Salesforce use.

Use this app connector to access SaaS Security Posture Management (SSPM) features, via security controls reflected in Microsoft Secure Score. [Learn more](/en-us/microsoft-365/security/defender/microsoft-secure-score).

- Install and authorize the Salesforce Connected App in the target Salesforce org before you start the connection process. Salesforce enforces usage restrictions on Connected Apps. For more information, see [Prepare for Connected App Usage Restrictions Change](https://help.salesforce.com/s/articleView?id=005132365&amp;type=1).
- Assign the **Approve Uninstalled Connected Apps** permission to the Salesforce service account used to connect Microsoft Defender for Cloud Apps. Salesforce requires this permission to connect third-party apps via OAuth.
- Make sure that the Salesforce account is assigned to one of the following editions, which support REST API access:
    - Performance
    - Enterprise
    - Unlimited
    - Developer
    - Professional. REST API must be added to the Professional edition separately.

### Configure Salesforce

Perform the following steps in Salesforce before connecting the app:

1. In your Salesforce account, create a dedicated service admin account for Defender for Cloud Apps.
2. Create a new profile for the Defender for Cloud Apps service account. Use this profile to configure the App connector.
3. Make sure that the service account profile includes the following permissions:

    - **API Enabled**
    - **View All Data**
    - **Manage Salesforce CRM Content**
    - **Manage Users**
    - **[Query All Files](https://go.microsoft.com/fwlink/?linkid=2106480)**
    - **Modify Metadata Through Metadata API Functions**
    - **View Setup And Configuration**
4. If **Salesforce CRM Content** is active in your organization:

    - Grant Salesforce CRM Content access to the Defender for Cloud Apps service admin account.
    - Turn off **Lock sessions to the IP address from which they originated** for the service account profile.
    - Turn on **Content Deliveries and Public Links**.

Note

To query file sharing data, enable the Content Deliveries feature for Defender for Cloud Apps. For more information, see [ContentDistribution](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contentdistribution.htm).

### Configure Defender for Cloud Apps

Perform the following steps to connect Defender for Cloud Apps to Salesforce:

1. In the Defender for Cloud Apps console, select **Investigate** and then **Connected apps**.
2. In the **App connectors** page, select **+Connect an app** followed by **Salesforce**.

    [![Screenshot that shows how to add the Salesforce app connector in the Defender portal.](media/connect-salesforce.png)](media/connect-salesforce.png#lightbox)
3. In the next window, enter a name for the connection and select **Next**.
4. In **Follow the link**, select **Connect Salesforce**.
5. Selecting **Connect Salesforce** opens the Salesforce sign-in page. Enter your credentials to allow Defender for Cloud Apps access to your team's Salesforce app.

    [![Screenshot that shows a pop-up and how to enter your Salesforce credentials.](media/salesforce-logon.png)](media/salesforce-logon.png#lightbox)
6. Salesforce asks if you want to allow Defender for Cloud Apps access to your team information and activity log and to perform any activity as any team member. Select **Allow** to continue.
7. You receive a success or failure notice for the deployment. Defender for Cloud Apps is now authorized in Salesforce.com.
8. Back in the Defender for Cloud Apps console, you see the **Salesforce was successfully connected** message.
9. In the Microsoft Defender portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**. Make sure the status of the connected App Connector is **Connected**.

After you connect Salesforce, Defender for Cloud Apps collects login events and Setup Audit Trail entries from the seven days before connection, and Event Monitoring data from the previous 30 days or one day, depending on your Salesforce Event Monitoring license.

Defender for Cloud Apps calls the Salesforce APIs directly. Because Salesforce limits the number of API calls per period, Defender for Cloud Apps reads the API counters returned in each Salesforce response and always keeps 10% of the available calls in reserve.

When you enable Salesforce real-time event monitoring (Preview), detection latency for identity and OAuth attacks drops from hours to minutes. Detections also include more context, such as the connected app name and ID, app permissions, user agent, IP address, and session information.

Note

- Defender for Cloud Apps throttling is calculated solely on its own API calls with Salesforce, not with those of any other applications making API calls with Salesforce. Limiting API calls due to throttling might temporarily slow data ingestion in Defender for Cloud Apps, but the process typically catches up overnight.
- If your Salesforce instance isn't in English, select the appropriate **language** attribute value for the integration service admin account. To change the language attribute, go to **Administration** &gt; **Users** &gt; **User** and open the integration system admin account. Now go to **Locale Settings** &gt; **Language** and select the desired language.

Defender for Cloud Apps processes Salesforce events on the following schedule:

- Sign-in events every 15 minutes
- Setup audit trails every 15 minutes
- Event logs every 1 hour. For more information about Salesforce events, see [Using event monitoring](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/using_resources_event_log_files.htm).

## Enable Salesforce real-time event monitoring (Preview)

To get the most detection coverage and the richest investigation context from the Salesforce connector, a Salesforce administrator must enable **Storing data** for a set of events in Salesforce Event Manager. Defender for Cloud Apps then ingests those events from Salesforce Real-Time Event Monitoring within minutes and uses them to improve detection coverage for OAuth abuse, session hijacking, credential stuffing, and anomalous API activity.

The Salesforce OAuth apps inventory also includes Connected Apps and External Client Apps (ECAs), along with each app's granted permissions and last used date. **Highly privileged** and **Unused** app insights for Salesforce help you identify OAuth apps that need review. For more information, see [Application inventory](applications-inventory) and [View your app details with app governance](app-governance-visibility-insights-view-apps).

Enable these events for the best detection coverage. Enabling these events gives you better latency and more robust detections.

### Enable the events in Salesforce Event Manager

Perform the following steps in Salesforce Event Manager to enable the required events:

1. Sign in to Salesforce as an administrator.
2. Go to `https://YOURDOMAIN.lightning.force.com/lightning/setup/EventManager/home`.
3. Search for each of the following events and enable **Storing data**:

    - API Anomaly Event
    - API Event
    - Credential Stuffing Event
    - Guest User Anomaly Event
    - Identity Provider Event
    - Identity Verification Event
    - Permission Set Event
    - Report Anomaly Event
    - Report Event
    - Session Hijacking Event