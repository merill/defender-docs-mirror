---
layout: Conceptual
title: Protect your Google Cloud Platform environment - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/protect-gcp
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
description: Connect Google Cloud Platform to Microsoft Defender for Cloud Apps by using the API connector to monitor admin and sign-in activity and detect threats such as brute-force attacks and unusual VM deletions.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: AmitMishaeli
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: dc2f639d-eb96-8dca-68df-9f9e7b896dba
document_version_independent_id: dc2f639d-eb96-8dca-68df-9f9e7b896dba
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/protect-gcp.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: protect-gcp
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/protect-gcp.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://authoring-docs-microsoft.poolparty.biz/devrel/07bb3e10-d135-43ff-bc8b-360497cb39fa
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://authoring-docs-microsoft.poolparty.biz/devrel/12e559b9-eaf6-4aee-9af7-62334e15f863
platformId: fbe72d39-0b1f-2e31-7340-2bfe0c6b1691
---

# Protect your Google Cloud Platform environment - Microsoft Defender for Cloud Apps | Microsoft Learn

Google Cloud Platform (GCP) is a cloud provider that lets your organization host and manage workloads in the cloud. The cloud offers many benefits, but it can also expose critical assets to threats. These assets include storage with sensitive data, compute resources that run key apps, ports, and virtual private networks.

When you connect GCP to Defender for Cloud Apps, you can better secure your assets and detect threats. The service monitors admin and sign-in activities. It alerts you to brute force attacks, misuse of privileged accounts, and unusual deletions of virtual machines (VMs).

## Main threats to your GCP environment

Defender for Cloud Apps helps you find and address these GCP threats:

- Abuse of cloud resources
- Compromised accounts and insider threats
- Data leakage
- Resource misconfiguration and insufficient access control

## How Defender for Cloud Apps helps to protect your environment

Review the following best practices to learn how Defender for Cloud Apps helps protect your GCP environment:

- [Detect cloud threats, compromised accounts, and malicious insiders](best-practices#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [Use the audit trail of activities for forensic investigations](best-practices#use-the-audit-trail-of-activities-for-forensic-investigations)

## Control GCP with built-in policies and policy templates

You can use the following built-in policy templates to detect and notify you about potential threats:

| Type | Name |
| --- | --- |
| Built-in anomaly detection policy | [Activity from anonymous IP addresses](anomaly-detection-policy#activity-from-anonymous-ip-addresses)[Activity from infrequent country](anomaly-detection-policy#activity-from-infrequent-country)[Activity from suspicious IP addresses](anomaly-detection-policy#activity-from-suspicious-ip-addresses)[Impossible travel](anomaly-detection-policy#impossible-travel)[Activity performed by terminated user](anomaly-detection-policy#activity-performed-by-terminated-user) (requires Microsoft Entra ID as IdP) |
| Activity policy template | Changes to compute engine resourcesChanges to StackDriver configurationChanges to storage resourcesChanges to Virtual Private NetworkLogon from a risky IP address |

For more information about creating policies, see [Create a policy](control-cloud-apps-with-policies#create-a-policy).

## Automate governance controls

In addition to monitoring for potential threats, you can apply and automate the following GCP governance actions to remediate detected threats:

| Type | Action |
| --- | --- |
| User governance | - Require user to reset password to Google (requires connected linked Google Workspace instance)- Suspend user (requires connected linked Google Workspace instance)- Notify user on alert (via Microsoft Entra ID)- Require user to sign in again (via Microsoft Entra ID)- Suspend user (via Microsoft Entra ID) |

For more information about remediating threats from apps, see [Governing connected apps](governance-actions).

## Protect GCP in real time

Review our best practices for [securing and collaborating with external users](best-practices#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls) and [blocking and protecting the download of sensitive data to unmanaged or risky devices](best-practices#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices).

## Connect Google Cloud Platform to Microsoft Defender for Cloud Apps

The following instructions describe how to connect Microsoft Defender for Cloud Apps to your existing Google Cloud Platform (GCP) account using the connector APIs. The connector gives you visibility into and control over GCP use. For information about how Defender for Cloud Apps protects GCP, see [Protect GCP](protect-gcp).

We recommend that you use a dedicated project for the Defender for Cloud Apps–GCP integration and restrict access to the project to maintain stable integration and prevent deletions or modifications of the setup process.

Note

The instructions for connecting your GCP environment for auditing follow [Google's recommendations](https://cloud.google.com/blog/products/it-ops/best-practices-for-working-with-google-cloud-audit-logging) for consuming aggregated logs. The integration leverages Google StackDriver and will consume additional resources that might impact your billing. The consumed resources are:

- [Aggregated export sink – Organization level](https://cloud.google.com/logging/docs/export/aggregated_sinks#concept)
- [Pub/Sub topic – GCP project level](https://cloud.google.com/logging/docs/export/using_exported_logs#pubsub-overview)
- [Pub/Sub subscription – GCP project level](https://cloud.google.com/logging/docs/export/using_exported_logs#pubsub-overview)

The Defender for Cloud Apps auditing connection only imports Admin Activity audit logs; Data Access and System Event audit logs aren't imported. For more information about GCP logs, see [Cloud Audit Logs](https://go.microsoft.com/fwlink/?linkid=2109230).

### Prerequisites

The integrating GCP user must have the following permissions:

- **IAM and Admin edit** – Organization level
- **Project creation and edit**

You can connect GCP **Security auditing** to your Defender for Cloud Apps connections to gain visibility into and control over GCP app use.

### Configure Google Cloud Platform

1. Create a dedicated project in GCP under your organization to enable integration isolation and stability.
2. Enable the **Cloud Logging API** and **Cloud Pub/Sub API** for the dedicated project.

    Note

    Make sure that you don't select **Pub/Sub Lite API**.

#### Create a dedicated service account with required roles

To create a service account and assign the required roles, perform the following steps:

1. Create a dedicated service account.
2. Copy the **Email** value. You'll need the service account email address later.
3. Assign the **Pub/Sub Admin** role to the service account.
4. Assign the **Logs Configuration Writer** role to the service account at the organization level.

#### Create a private key for the dedicated service account

To generate a private key for the service account, perform the following steps:

1. Switch to project level.
2. Select **Service accounts**.
3. Generate a **JSON private key**.

    Note

    You'll need the JSON file that is downloaded to your device later.

#### Retrieve your Organization ID

Make a note of your **Organization ID**. You'll need the Organization ID later. For more information, see [Getting your organization ID](https://cloud.google.com/resource-manager/docs/creating-managing-organization#retrieving_your_organization_id).

### Connect Google Cloud Platform auditing to Defender for Cloud Apps

This procedure describes how to add the GCP connection details to connect Google Cloud Platform auditing to Defender for Cloud Apps.

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**.
2. In the **App connectors** page, to provide the GCP connector credentials, do one of the following:

    Note

    We recommended that you connect your Google Workspace instance to get unified user management and governance. This is the recommended even if you don't use any Google Workspace products and the GCP users are managed via the Google Workspace user management system.

**For a new connector**

1. Select **+Connect an app**, followed by **Google Cloud Platform**.

    [![Screenshot that shows where to find the Google Cloud Platform app connector in the Defender portal.](media/connect-gcp-add.png)](media/connect-gcp-add.png#lightbox)
2. In the next window, provide a name for the connector, and then select **Next**.

    [![Screenshot that shows where to add the instance name in the Defender portal.](media/connect-gcp-name.png)](media/connect-gcp-name.png#lightbox)
3. In the **Enter details** page, do the following, and then select **Submit**.

    1. In the **Organization ID** box, enter the **Organization ID** you saved previously.
    2. In the **Private key file** box, browse to the JSON private key file you downloaded when you created the service account key.

    [![Screenshot that shows where to enter the organization ID and private key file in the Defender portal.](media/connect-gcp-app-audit.png)](media/connect-gcp-app-audit.png#lightbox)

**For an existing connector**

1. In the list of connectors, on the row in which the GCP connector appears, select **Edit settings**.
2. In the **Enter details** page, do the following, and then select **Submit**.

    1. In the **Organization ID** box, enter the **Organization ID** you saved previously.
    2. In the **Private key file** box, browse to the JSON private key file you downloaded when you created the service account key.

    [![Screenshot that shows where to enter the organization ID and private key file in the Defender portal.](media/connect-gcp-app-audit.png)](media/connect-gcp-app-audit.png#lightbox)
3. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**. Make sure the status of the connected App Connector is **Connected**.

    Note

    Defender for Cloud Apps will create an aggregated export sink (organization level), a Pub/Sub topic, and Pub/Sub subscription using the integration service account in the integration project.

    Aggregated export sink is used to aggregate logs across the GCP organization and the Pub/Sub topic created is used as the destination. Defender for Cloud Apps subscribes to this topic through the Pub/Sub subscription created to retrieve the admin activity logs across the GCP organization.