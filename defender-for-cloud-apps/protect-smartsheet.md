---
layout: Conceptual
title: Protect your Smartsheet - Microsoft Defender for Cloud Apps | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-cloud-apps/protect-smartsheet
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
description: Connect Smartsheet to Microsoft Defender for Cloud Apps with the API connector to monitor activities and detect anomalous behavior.
ms.date: 2026-07-03T00:00:00.0000000Z
ms.topic: how-to
ms.reviewer: AmitMishaeli
ms.custom: sfi-image-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 0092bb4c-ded6-e091-e95a-3ebf671d20c7
document_version_independent_id: 0092bb4c-ded6-e091-e95a-3ebf671d20c7
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud-apps/protect-smartsheet.md
site_name: Docs
depot_name: Learn.defender-cloud-apps
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: protect-smartsheet
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud-apps/protect-smartsheet.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
- https://authoring-docs-microsoft.poolparty.biz/devrel/1e69816a-aaaa-474e-a36f-3ec7790fadc3
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1433a524-c01f-4b87-beab-670c040dea4f
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
- https://authoring-docs-microsoft.poolparty.biz/devrel/ae012320-d2b3-47d8-abdc-898a64d069a9
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/312f1f05-a431-4193-8a4d-e6245d5966de
platformId: 0210920c-4f21-9afb-fa2c-80e9f2d8b001
---

# Protect your Smartsheet - Microsoft Defender for Cloud Apps | Microsoft Learn

As a productivity and collaboration cloud solution, Smartsheet holds sensitive information to your organization. Any abuse of Smartsheet by a malicious actor or any human error may expose your most critical assets and services to potential attacks.

Connecting Smartsheet to Defender for Cloud Apps gives you improved insights into your Smartsheet activities and provides threat detection for anomalous behavior.

## Main threats to your Smartsheet environment

Connecting Smartsheet to Defender for Cloud Apps helps you address threats such as:

- Compromised accounts and insider threats
- Data leakage
- Insufficient security awareness
- Unmanaged bring your own device (BYOD)

## How Defender for Cloud Apps helps to protect your environment

Use the following best practices to help protect your environment:

- [Detect cloud threats, compromised accounts, and malicious insiders](best-practices#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [Use the audit trail of activities for forensic investigations](best-practices#use-the-audit-trail-of-activities-for-forensic-investigations)

## Control Smartsheet with policies

The following policies can help you monitor and control Smartsheet:

| **Type** | **Name** |
| --- | --- |
| Built-in anomaly detection policy | [Unusual file share activities](anomaly-detection-policy#unusual-activities-by-user)[Unusual file deletion activities](anomaly-detection-policy#unusual-activities-by-user)[Unusual administrative activities](anomaly-detection-policy#unusual-activities-by-user)[Unusual multiple file download activities](anomaly-detection-policy#unusual-activities-by-user) |
| Activity policy | Build a customized policy by the Smartsheet [Audit Log](https://smartsheet.redoc.ly/tag/eventsObjects) activities |

Note

- Login/Logouts activities are not supported by Smartsheet.
- Smartsheet activities does not contain IP addresses.

For more information about creating policies, see [Create a policy](control-cloud-apps-with-policies#create-a-policy).

## Automate governance controls

You can automate the following Smartsheet governance actions in Defender for Cloud Apps to fix detected threats:

| **Type** | **Action** |
| --- | --- |
| User governance | Notify user on alert (via Microsoft Entra ID) Require user to sign in again (via Microsoft Entra ID)  Suspend user (via Microsoft Entra ID) |

For more information about remediating threats from apps, see [Governing connected apps](governance-actions).

## Protect Smartsheet in real time

Review our best practices for [securing and collaborating with external users](best-practices#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls) and [blocking and protecting the download of sensitive data to unmanaged or risky devices](best-practices#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices).

## Connect Smartsheet to Microsoft Defender for Cloud Apps

The following instructions describe how to connect Microsoft Defender for Cloud Apps to your existing Smartsheet via the App Connector APIs. The resulting connection gives you visibility into and control over your organization's use of Smartsheet.

### Prerequisites

Before you connect Smartsheet, make sure the following prerequisites are met:

- You must have a Smartsheet license that is part of an Enterprise plan with the Platinum package.
- The Smartsheet user used to log in to Smartsheet must be a System Admin.
- Event Reporting must be enabled by Smartsheet, either through standalone purchase or via an Enterprise plan with the Advance Platinum package.
- Smartsheet accounts must be in the **smartsheet.com**domain. These domains are not currently supported:
    - smartsheet.au
    - smartsheet.eu
    - smartsheetgov.com

### Configure Smartsheet

1. Register to add Developer Tools to your existing Smartsheet account:

    1. Go to the [Developer Sandbox Account Registration](https://developers.smartsheet.com/register/) page.
    2. Enter your Smartsheet email address in the text box:

        ![Screenshot of the Developer Sandbox Account Registration page with the email address text box for registering developer tools.](media/smartsheet-register-to-developer-tools.png)
    3. An activation mail will appear in your mailbox. Activate Developer Tools by using the activation mail.
    4. In Smartsheet, select **Create Developer Profile**. Enter your name and email address. Select **Save** and then **Close**:

        ![Screenshot of the Create Developer Profile form with fields for entering your name and email address.](media/smartsheet-create-developer-tools.png)
2. In Smartsheet, select **Developer Tools**:

    ![Screenshot of the Smartsheet menu with the Developer Tools option selected.](media/smartsheet-entering-developer-tools.png)
3. In the **Developer Tools** dialog, select **Create New App**:

    ![Screenshot of the Developer Tools page with the Create New App option.](media/smartsheet-developer-tools.png)
4. In the **Create New App** dialog, provide the following values:

    - **App name**: For example, **Microsoft Defender for Cloud Apps**.
    - **App description**: For example, **Microsoft Defender for Cloud Apps connects to Smartsheet via its API and detects threats within users' activity.**
    - **App URL**: `https://portal.cloudappsecurity.com`
    - **App contact/support**: `https://learn.microsoft.com/cloud-app-security/support-and-ts`
    - **App redirect URL**: `https://portal.cloudappsecurity.com/api/oauth/saga`
    - **Publish App?**: Select.
    - **Logo**: Leave blank.

        ![Screenshot of the Create New App dialog for entering OAuth app details such as app name, description, and redirect URL.](media/smartsheet-oauth-app-creation.png)
5. Select **Save**. Copy the **App client id** and the **App secret** that are generated. You'll need these values when you configure Defender for Cloud Apps.

### Configure Defender for Cloud Apps

Note

The Smartsheet user configuring the integration must always remain a Smartsheet admin, even after the connector is installed.

1. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**.
2. On the **App connectors** tab, select **+Connect an app**, and then select **Smartsheet**.
3. In the next window, give the connector a descriptive name, and then select **Next**.

    ![Screenshot of the app connector dialog with the Connect Smartsheet option selected.](media/connect-smartsheet.png)
4. On the **Enter details** screen, enter these values and select **Next**:

    - **Client ID**: The app client ID that you saved earlier.
    - **Client Secret**: The app secret that you saved earlier.
5. On the **External Link** page, select **Connect Smartsheet**.
6. In the Microsoft Defender Portal, select **Settings**. Then choose **Cloud Apps**. Under **Connected apps**, select **App Connectors**. Make sure the status of the connected App Connector is **Connected**.
7. The first connection can take up to four hours to get all users and their activities in the seven days before the connection.
8. After the connector's **Status** is marked as **Connected**, the connector is live and works.

## Rate limits and limitations

The default rate limit is 300 requests per minute. For more information, see the [Smartsheet documentation](https://smartsheet.redoc.ly/#section/Work-at-Scale/Rate-Limiting).

Limitations include:

- Log in and log out activities aren't supported by Smartsheet.
- Smartsheet activities don't contain IP addresses.
- System activities are shown with the Smartsheet account name.