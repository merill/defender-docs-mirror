---
layout: Conceptual
title: Daily operational guide - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/ops-guide/ops-guide-daily
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
description: This article provides daily operational recommendations to help security operations teams to plan and run security activities.
ms.date: 2024-05-15T00:00:00.0000000Z
ms.topic: reference
locale: en-us
document_id: 387bcbba-1163-51d7-6306-93300570402e
document_version_independent_id: 387bcbba-1163-51d7-6306-93300570402e
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/ops-guide/ops-guide-daily.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: ops-guide/ops-guide-daily
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/ops-guide/ops-guide-daily.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/8a94907f-2511-4271-b5ca-ec7f2e75067c
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/bffa8e88-f633-409d-a24d-083bdbc68872
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 17135000-92dc-7085-96be-5a0802583f5a
---

# Daily operational guide - Microsoft Defender for Cloud Apps | Microsoft Learn

This article lists daily operational activities that we recommend you perform with Defender for Cloud Apps.

## Review alerts and incidents

Alerts and incidents are two of the most important items your security operations (SOC) team should be reviewing on a daily basis.

- Triage incidents and alerts regularly from the [incidents queue](https://security.microsoft.com/incidents) in Microsoft Defender XDR, prioritizing high and medium severity alerts.
- If you're working with a SIEM system, your SIEM system is usually the first stop for triage. SIEM systems provide more context with extra logs and SOAR functionality. Then, use Microsoft Defender XDR for a deeper understanding of an alert or incident timeline.

### Triage your incidents from Microsoft Defender

**Where**: In the Defender portal, select **Incidents & alerts**

**Persona**: SOC analysts

**When triaging incidents**:

1. In the incident dashboard, filter for the following items:

    | Filter | Values |
    | --- | --- |
    | **Status** | New, In progress |
    | **Severity** | High, Medium, Low |
    | **Service source** | Keep all service sources checked. Keeping all service source checked should list alerts with the most fidelity, with correlation in other Microsoft Defender workloads. Select **Defender for Cloud Apps** to view items that come specifically from Defender for Cloud Apps. |
2. Select each incident to review all details. Review all tabs in the incident, the activity log, and advanced hunting.

    In the incident's **Evidence and response** tab, select each evidence item. Select the options menu &gt; **Investigate** and then select **Activity log** or **Go hunt** as needed.
3. Triage your incidents. For each incident, select **Manage incident** and then select one of the following options:

    - **True positive**
    - **False positive**
    - **Informational, expected activity**

    For true alerts, specify the treat type to help your security team see threat patterns and defend your organization from risk.
4. When you're ready to start your active investigation, assign the incident to a user and update the incident status to **In progress**.
5. When the incident is remediated, resolve it to resolve all linked and related active alerts.

For more information, see:

- [Prioritize incidents in Microsoft Defender](/en-us/microsoft-365/security/defender/incident-queue)
- [Investigate alerts in Microsoft Defender](/en-us/microsoft-365/security/defender/investigate-alerts)
- [Incident response playbooks](/en-us/security/operations/incident-response-playbooks)
- [How to investigate anomaly detection alerts](../investigate-anomaly-alerts)
- [Manage app governance alerts](../app-governance-manage-alerts)
- [Investigate threat detection alerts](../app-governance-anomaly-detection-alerts)

### Triage your incidents from your SIEM system

**Persona**: SOC analysts

**Prerequisites**: You must be connected to a SIEM system, and we recommend integrating with Microsoft Sentinel. For more information, see:

- [Microsoft Sentinel integration (Preview)](../siem-sentinel)
- [Connect data from Microsoft Defender XDR to Microsoft Sentinel](/en-us/azure/sentinel/connect-microsoft-365-defender)
- [Generic SIEM integration](../siem)

Integrating Microsoft Defender with Microsoft Sentinel allows you to stream all Microsoft Defender incidents into Microsoft Sentinel and keep them synchronized between both portals. Microsoft Defender incidents in Microsoft Sentinel include all associated alerts, entities, and relevant information, providing enough context to triage and run a preliminary investigation.

Once in Microsoft Sentinel, incidents remain synchronized with Microsoft Defender so that you can use the features from both portals in your investigation.

- When installing Microsoft Sentinel's data connector for Microsoft Defender XDR, make sure to include the Microsoft Defender for Cloud Apps option.
- Consider using a [streaming API](/en-us/microsoft-365/security/defender/streaming-api) to send data to an event hub, where it can be consumed through any partner SIEM with an event hub connector, or placed in Azure Storage.

For more information, see:

- [Microsoft Defender XDR integration with Microsoft Sentinel](/en-us/azure/sentinel/microsoft-365-defender-sentinel-integration)
- [Navigate and investigate incidents in Microsoft Sentinel](/en-us/azure/sentinel/investigate-incidents)
- [Create custom analytics rules to detect threats](/en-us/azure/sentinel/detect-threats-custom)

## Review threat detection data

**Where**: In the [Microsoft Defender portal](https://security.microsoft.com), select:

- **Incidents & alerts**
- **Cloud apps &gt; Policies &gt; Policy management &gt; Threat Detection**
- **Cloud apps &gt; Oauth apps**

**Persona**: Security administrators and SOC analysts

Cloud app threat detection is where many SOC analysts focus their daily activities, identifying high-risk users who showing abnormal behavior.

Defender for Cloud Apps threat detection uses Microsoft threat intelligence and security research data. Alerts are available in the Defender portal and should be triaged regularly.

When security administrators and SOC analysts deal with alerts, they handle the following main types of threat detection policies:

- [Activity policies](../user-activity-policies)
- [Anomaly detection policies](../anomaly-detection-policy)
- [OAuth Policies](../app-permission-policy) and [App governance policies](../app-governance-manage-app-governance)

**Persona**: Security administrator

Make sure to create the threat protection policies needed by your organization, including handling any prerequisites.

## Review application governance

**Where**: In the [Microsoft Defender portal](https://security.microsoft.com), select:

- **Incidents & alerts**
- **Incidents & alerts / App governance**

**Persona**: SOC analysts

App governance offers in-depth visibility and control over OAuth apps. App governance helps to combat increasingly sophisticated campaigns that exploit the apps deployed on-premises and in cloud infrastructures, establishing a starting point for privilege escalation, lateral movement, and data exfiltration.

App governance is provided together with Defender for Cloud Apps. Alerts are also available in the Defender portal, and should be triaged regularly.

For more information, see:

- [Discovery alerts](../app-governance-anomaly-detection-alerts#discovery-alerts)
- [Investigate predefined app policy alerts](../app-governance-investigate-predefined-policies)
- [Investigate and remediate risky OAuth apps](../investigate-risky-oauth)

### Check app governance overview page

**Where**: In the [Microsoft Defender portal](https://security.microsoft.com), select:

- **Incidents & alerts**
- **Cloud apps &gt; App governance &gt; Overview**

**Persona**: SOC analysts and Security administrator

We recommend that you run a quick, daily assessment of the compliance posture of your apps and incidents. For example, check the following details:

- The number of over-privileged or highly privileged apps
- Apps with an unverified publisher
- Data usage for services and resources that were accessed using Graph API
- The number of apps that accessed data with the most common sensitivity labels
- The number of apps that accessed data with and without sensitivity labels across Microsoft 365 services
- An overview of app governance-related incidents

Based on the data you review, you might want to create new or adjust app governance policies.

For more information, see:

- [View and manage incidents and alerts](/en-us/defender-xdr/mto-incidents-alerts)
- [View your app details with app governance](../app-governance-visibility-insights-view-apps)
- [Create app policies in app governance](../app-governance-app-policies-create).

### Review OAuth app data

**Where**: In the [Microsoft Defender portal](https://security.microsoft.com), select:

- **Incidents & alerts**
- **Cloud apps &gt; App governance &gt; Microsoft 365**

We recommend that you check your list of OAuth-enabled apps daily, together with relevant app metadata and usage data. Select an app to view deeper insights and information.

App governance uses machine learning-based detection algorithms to detect anomalous app behavior in your Microsoft Defender XDR tenant, and generates alerts that you can see, investigate, and resolve. Beyond this built-in detection capability, you can use a set of default policy templates or create your own app policies that generate other alerts.

For more information, see:

- [View and manage incidents and alerts](/en-us/defender-xdr/mto-incidents-alerts)
- [View your app details with app governance](../app-governance-visibility-insights-view-apps)
- [Get detailed information about an app](../app-governance-visibility-insights-view-apps#get-detailed-information-about-an-app)

### Create and manage app governance policies

**Where**: In the [Microsoft Defender portal](https://security.microsoft.com), select **Cloud apps &gt; App governance &gt; Policies**

**Persona**: Security administrators

We recommend that you check your OAuth apps daily for regular in-depth visibility and control. Generate alerts based on machine learning algorithms, and create app policies for app governance.

For more information, see:

- [Create app policies in app governance](../app-governance-app-policies-create)
- [Manage app policies](../app-governance-app-policies-create#manage-app-policies)

## Review Conditional Access app control

**Where**: In the [Microsoft Defender portal](https://security.microsoft.com), select:

- **Incidents & alerts**
- **Cloud apps &gt; Policies &gt; Policy Management &gt; Conditional Access**

To configure Conditional Access app control, select **Settings &gt; Cloud apps &gt; Conditional Access App Control**

**Persona**: Security administrator

Conditional Access app control provides you with the ability to monitor and control user app access and sessions in real time, based on access and session policies.

Generated alerts are available in the Defender portal and should be triaged regularly.

By default, there's no access or session policies deployed, and therefore no related alerts available. You can onboard any web app to work with access and session controls, Microsoft Entra ID apps are automatically onboarded. We recommend that you create session and access policies as needed for your organization.

For more information, see:

- [View and manage incidents and alerts](/en-us/defender-xdr/mto-incidents-alerts)
- [Protect apps with Microsoft Defender for Cloud Apps Conditional Access app control](../proxy-intro-aad)
- [Block and protect download of sensitive data to unmanaged or risky devices](../best-practices#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices)
- [Secure collaboration with external users by enforcing real-time session controls](../best-practices#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls)

**Persona**: SOC administrator

We recommend that you review Conditional Access app control alerts daily, and the activity log. Filter activity logs by source, access control, and session control.

For more information, see Review alerts and incidents

## Review shadow IT - cloud discovery

**Where**: In the [Microsoft Defender portal](https://security.microsoft.com), select:

- **Incidents & alerts**
- **Cloud apps &gt; Cloud discovery / Cloud app catalog**
- **Cloud apps &gt; Policies &gt; Policy Management &gt; Shadow IT**

**Persona**: Security administrators

Defender for cloud apps analyzes your traffic logs against the cloud apps catalog of over 31,000 cloud apps. Apps are ranked and scored based on more than 90 risk factors to provide ongoing visibility into cloud use, Shadow IT, and the risks that Shadow IT poses into your organization.

Alerts related to cloud discovery are available in the Defender portal and should be triaged regularly.

Create app discovery policies to start alerting and tagging newly discovered apps based on certain conditions, like risk scores, categories, and app behaviors like daily traffic and downloaded data.

Tip

We recommend that you integrate Defender for Cloud Apps with Microsoft Defender for Endpoint to discover cloud apps beyond your corporate network or secure gateways and apply governance actions on your endpoints.

For more information, see:

- [View and manage incidents and alerts](/en-us/defender-xdr/mto-incidents-alerts)
- [Cloud discovery policies](../policies-cloud-discovery)
- [Create cloud discovery policies](../cloud-discovery-policies)
- [Set up cloud discovery](../set-up-cloud-discovery)
- [Discover and assess cloud apps](../best-practices#discover-and-assess-cloud-apps)

**Persona**: Security and Compliance administrators, SOC analysts

When you have large numbers of discovered apps, you might want to use the filtering options to learn more about your discovered apps.

For more information, see [Discovered app filters and queries in Microsoft Defender for Cloud Apps](../discovered-app-queries).

## Review the cloud discovery dashboard

**Where**: In the [Microsoft Defender portal](https://security.microsoft.com), select **Cloud apps &gt; Cloud discovery &gt; Dashboard**.

**Persona**: Security and Compliance administrators, SOC analysts

We recommend reviewing your cloud discovery dashboard on a daily basis. The cloud discovery dashboard is designed to give you more insight into how cloud apps are used in your organization, with an at-a-glance overview of the kids of apps being used, your open alerts, and the risk levels of apps in your organization.

**On the cloud discovery dashboard**:

1. Use the widgets at the top of the page to understand your overall cloud app usage.
2. Filter the dashboard graphs to generate specific views, depending on your interest. For example:

    - Understand top categories of apps used in your org, especially for sanctioned apps.
    - Review risk scores for your discovered apps.
    - Filter views to see your top apps in specific categories.
    - View top users and IP addresses to identify the users who are the most dominant users of cloud apps in your organization.
    - View app data on a world map to understand how discovered apps spread by geographic location.

After reviewing the list of discovered apps in your environment, we recommend that you secure your environment by approving safe apps (*Sanctioned* apps), prohibiting unwanted apps (*Unsanctioned* apps), or applying custom tags.

You might also want to proactively review and apply tags to the apps available in the cloud app catalog before they're discovered in your environment. To help you govern those applications, create relevant cloud discovery policies, triggered by specific tags.

For more information, see:

- [Working with discovery data](../working-with-cloud-discovery-data)
- [Working with discovered apps](../discovered-apps)

Tip

Depending on your environment configuration, you might benefit from the seamless and automated blocking, or even the *warn and educate* features provided by Microsoft Defender for Endpoint. For more information, see [Integrate Microsoft Defender for Endpoint with Microsoft Defender for Cloud Apps](../mde-integration).

## Review information protection

**Where**: In the [Microsoft Defender portal](https://security.microsoft.com), select:

- **Incidents & alerts**
- **Cloud apps &gt; Files**
- **Cloud apps &gt; Policies &gt; Policy Management &gt; Information protection**

**Persona**: Security and Compliance administrators, SOC analysts

Defender for Cloud Apps file policies and alerts allow you to enforce a wide range of automated processes. Create policies to provide information protection, including continuous compliance scans, legal eDiscovery tasks, and data loss protection (DLP) for sensitive content shared publicly.

Important

File policies retire on January 6, 2027. To maintain file-based data protection, [migrate to Microsoft Purview DLP or auto-labeling policies](../migrate-file-policies-to-purview).

In addition to triaging alerts and incidents, we recommend that your SOC teams run extra, proactive actions and queries. In the **Cloud apps &gt; Files** page, check for the following questions:

- How many files are shared publicly so that anyone can access them without a link?
- Which partners are you sharing files to using outbound sharing?
- Do any files have sensitive names?
- Are any of the files being shared with someone's personal account?

Use the results of these queries to adjust existing file policies or create new policies.

For more information, see:

- [View and manage incidents and alerts](/en-us/defender-xdr/mto-incidents-alerts)
- [Information protection policies](../policies-information-protection).