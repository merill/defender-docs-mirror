---
layout: Conceptual
title: Subscribe to Microsoft Defender Experts Hunting - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/defender-experts/defender-experts-hunting-onboarding
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
ms.reviewer: 
description: If you're new to Microsoft Defender and Defender Experts Hunting, this is how you onboard, receive, and set up Defender Experts Notifications.
ms.service: defender-experts-for-hunting
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
- essentials-get-started
ms.topic: how-to
ms.custom:
- msecd-doc-authoring-1014
- cx-ti
- cx-ean
- msecd-doc-authoring-1012
ai-usage: ai-assisted
ms.date: 2026-06-16T00:00:00.0000000Z
locale: en-us
document_id: aa46ba23-70e3-c38c-8ab0-54fc29201fd8
document_version_independent_id: aa46ba23-70e3-c38c-8ab0-54fc29201fd8
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/defender-experts/defender-experts-hunting-onboarding.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: ../toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: defender-experts/defender-experts-hunting-onboarding
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/defender-experts/defender-experts-hunting-onboarding.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://authoring-docs-microsoft.poolparty.biz/devrel/63959238-cb90-4871-a33d-4a5519097e47
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://authoring-docs-microsoft.poolparty.biz/devrel/78d87f42-5582-4a6b-90be-7db2f12b34e6
platformId: 404987ba-bde8-cf6b-5bbd-da9c08387f69
---

# Subscribe to Microsoft Defender Experts Hunting - Microsoft Defender XDR | Microsoft Learn

**Applies to:**

- [Microsoft Defender](../microsoft-365-defender)

To get started with the Microsoft Defender Experts Hunting service, onboard to the service, set up notification contacts, and configure Defender Experts Notifications.

## Onboard to Defender Experts Hunting

If you're new to Microsoft Defender and Defender Experts Hunting:

1. When you receive your welcome email, select **Log into Microsoft Defender**.
2. Sign in if you already have a Microsoft account. If you don't have a Microsoft account, create one.
3. The Microsoft Defender quick tour introduces you to the security suite, where the capabilities are, and how important they are. Select **Take a quick tour**.
4. Read the short descriptions about what the Microsoft Defender Experts service is and the capabilities it provides. Select **Next**. You see the welcome page:

    ![Screenshot of the Microsoft Defender welcome page with a card for the Defender Experts Hunting service.](media/onboarding-defender-experts-for-hunting/start-using-defender-experts-for-hunting.png)

## Tell us who to contact for important matters

Defender Experts Hunting lets you set up **Notification contacts**. These contacts are the individuals or groups within your organization that Microsoft needs to notify if there are critical incidents or service updates:

- **Incident notification contacts** – These contacts are persons or teams that Microsoft can notify for any critical incidents or hunting clarifications that require immediate response.

    You can designate the call priority of your incident notification contacts. In an event of a critical incident, Microsoft reaches out to the primary contact first by using the phone number you provided, and then the backup contact if needed.
- **Service review notification contacts** – These contacts are persons or teams that Microsoft can engage with for service updates, reports, and opportunities for feedback.

Set up your notification contacts in the setup wizard when you first onboard to the service, or from the Microsoft Defender portal navigation menu by going to **System** &gt; **Settings** &gt; **Defender Experts** &gt; **Notification contacts**.

## Receive Defender Experts notifications

The Defender Experts Notifications service includes:

- Threat monitoring and analysis, reducing dwell time and the risk to your business
- Hunter-trained artificial intelligence to discover and target both known attacks and emerging threats
- Identification of the most pertinent risks, helping SOCs maximize their effectiveness
- Help in scoping compromises and as much context as can be quickly delivered to enable a swift SOC response

The following screenshot shows a sample Defender Experts Notification:

![Screenshot of a Defender Experts Notification in Microsoft Defender showing the threat title, executive summary, and recommendations.](media/onboarding-defender-experts-for-hunting/receive-defender-experts-notification.png)

### Where to find Defender Experts Notifications

You can receive Defender Experts Notifications from Defender Experts through the following channels:

- The Defender portal's [Incidents](https://security.microsoft.com/incidents) page
- The Defender portal's [Alerts](https://security.microsoft.com/alerts) page
- OData alerting [Get alerts API](/en-us/defender-endpoint/api/get-alerts) and [SIEM integration REST API](/en-us/defender-endpoint/configure-siem)
- [DeviceAlertEvents](../advanced-hunting-migrate-from-mde#map-devicealertevents-table) table in Advanced hunting
- Your email if you [configure an email notifications rule](defender-experts-hunting-onboarding#set-up-defender-experts-email-notifications)
- Your Microsoft Teams if you set up Defender Experts Teams notifications

### Filter to view just the Defender Experts Notifications

You can filter your incidents and alerts if you want to only see the Defender Experts Notifications among the many alerts. To filter incidents and alerts to show only Defender Experts Notifications:

1. On the navigation menu, go to **Incidents & alerts** &gt; **Incidents** &gt; select the ![Screenshot of the Filter control used to filter incidents on the Incidents page](media/onboarding-defender-experts-for-hunting/filter.png) icon.
2. Scroll down to **Service/detection sources** then select the **Microsoft Defender Experts** checkboxes under *Microsoft Defender for Endpoint* and *Microsoft Defender*.
3. Select **Apply**.

### Set up Defender Experts email notifications

You can set up Microsoft Defender to notify you or your staff by using an email about new incidents or updates to existing incidents, including those observed by Microsoft Defender Experts. [Learn more about getting incident notifications by email](../m365d-notifications-incidents).

1. In the Microsoft Defender navigation pane, select **Settings** &gt; **Microsoft Defender** &gt; **Email notifications** &gt; **Incidents**.
2. Update your existing email notification rules or create a new one. For more information, see [Auditing](defender-experts-mdr-auditing).
3. On the rule's **Notification settings**page, make sure to configure the following values:
    - **Source** – Choose **Microsoft Defender Experts** under **Microsoft Defender** and **Microsoft Defender for Endpoint**.
    - **Alert severity** – Choose the alert severities that trigger an incident notification. For example, if you only want to be informed about high-severity incidents, select High.

### Set up Defender Experts Teams notifications

You can use Microsoft Teams, in addition to email, to receive Defender Experts Notifications.

Important

To set up Teams notifications, you must have a **Security Administrator** role or higher, and a Microsoft Teams license.

When Teams notifications are enabled:

- A dedicated Defender Experts team and a **Hunting notifications** channel are automatically created.
- Notifications are posted directly into the channel.
- Incident updates appear as replies in the same thread.
- Each notification includes the incident title, incident ID, and a direct link to the Defender portal.

Note

Teams notifications are a one-way notification experience. Defender Experts have access to messages in the channel but don't monitor or respond to messages posted there. To communicate with Defender Experts, use **Ask Defender Experts** in the Defender portal.

**To set up Teams notifications:**

1. In the Microsoft Defender portal, go to **Settings** &gt; **Defender Experts**.
2. Select **Teams**.
3. Turn on **Notify me on Teams**.
4. Select **Save**. Any notification contacts you added during notification contact setup are also added automatically as members of the Teams channel.
5. To add additional SOC team members to the created channel, go to **Microsoft Teams** &gt; **Defender Experts team** &gt; **More options (...)** &gt; **Manage team** &gt; **Add member**.

After setup, the system creates the Defender Experts team and the **Hunting notifications** channel, and provides a link to open the Teams channel. A welcome message appears in Teams confirming the setup is complete.

Tip

If the setup fails, see [Configuring the Microsoft Defender Experts app in Teams](defender-experts-teams-app-permissions) for troubleshooting guidance.

### Generate sample Defender Experts Notifications

You can generate a sample Defender Experts Notification to start experiencing the Defender Experts Hunting service without waiting for an actual critical activity in your environment. By generating a sample notification, you can also test any email notifications configured in the Microsoft Defender portal for this service. You can also test the configuration of playbooks (if configured for such notifications) and rules in your Security Information and Event Management (SIEM) environment.

A sample Defender Experts Notification appears in your **Incidents** page with the title *Defender Experts: Test Notification from Microsoft Defender Experts*. The notification's title, summary, and recommendations are placeholder text, while the other elements such as alerts are randomly generated from events present in your tenant and aren't actually impacted.

[![Screenshot of a sample Defender Experts Notification in the Incidents page for Defender Experts Hunting.](media/onboarding-defender-experts-for-hunting/sample-den-dexh.png)](media/onboarding-defender-experts-for-hunting/sample-den-dexh.png#lightbox)

**To generate a sample notification:**

1. In your Microsoft Defender navigation pane, go to **Settings** &gt; **Defender Experts** and then select **Sample notifications**.
2. Select **Generate a sample notification**. A green status message appears, confirming that your sample notification is ready for review.
3. Under **Recently generated Defender Experts Notification**, select a link from the list to view its corresponding generated sample notification. The most recent sample appears at the top of the list. Selecting a link redirects you to the **Incidents** page.

    [![Screenshot of the recently generated Defender Experts Notification links list.](media/onboarding-defender-experts-for-hunting/sample-den-links-dexh.png)](media/onboarding-defender-experts-for-hunting/sample-den-links-dexh.png#lightbox)