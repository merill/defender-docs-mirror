---
layout: Conceptual
title: Configure email notifications for alerts and attack paths - Microsoft Defender for Cloud | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/azure/defender-for-cloud/configure-email-notifications
breadcrumb_path: /azure/breadcrumb/defender-for-cloud/toc.json
feedback_help_link_url: https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/bd-p/MicrosoftDefenderCloud
feedback_help_link_type: ask-the-community
permissioned-type: public
feedback_product_url: ''
uhfHeaderId: MSDocsHeader-MicrosoftDefender
adobe-target: true
author: ElazarK
ms.author: elkrieger
manager: orspodek
ms.service: defender-for-cloud
description: Learn how to fine-tune the Microsoft Defender for Cloud security alert emails to ensure the right people receive timely notifications.
ms.topic: how-to
ms.date: 2026-05-26T00:00:00.0000000Z
ms.custom: mode-other
ai-usage: ai-assisted
locale: en-us
document_id: 70c6a1e1-490d-532e-9646-8a407206eb4c
document_version_independent_id: fcd3bf7a-2a94-6598-ea9e-63304bb5f304
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-for-cloud/configure-email-notifications.md
site_name: Docs
depot_name: Learn.defender-for-cloud
page_type: conceptual
toc_rel: toc.json
feedback_system: None
asset_id: defender-for-cloud/configure-email-notifications
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-for-cloud/configure-email-notifications.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/8e3fdb08-a059-4277-98f6-c0e21e940707
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/88291526-9c74-4f87-878c-de0a82134421
platformId: 204c9053-b3b5-5615-9be1-e1ceb43823ed
---

# Configure email notifications for alerts and attack paths - Microsoft Defender for Cloud | Microsoft Learn

Microsoft Defender for Cloud lets you configure email notifications for alerts and attack paths. You can choose who gets notified and when they get notified. You can also set severity thresholds for alerts and risk thresholds for externally driven attack paths. Notifications focus on real, exploitable threats instead of broad scenarios. By default, subscription owners receive email notifications for high-severity alerts and attack paths.

Defender for Cloud's **Email notifications** settings page lets you set:

- ***who* should be notified**: Emails can go to specific individuals or to users in selected Azure roles for a subscription.
- ***what* they should be notified about**: You can choose the severity levels that trigger notifications.

[![Screenshot showing how to configure the details of the contact who is to receive emails about alerts and attack paths.](media/configure-email-notifications/email-notification-settings.png)](media/configure-email-notifications/email-notification-settings.png#lightbox)

## Email frequency

To avoid alert fatigue, Defender for Cloud limits the volume of outgoing emails. For each email address, Defender for Cloud sends:

| Alert type | Severity/Risk level | Email volume |
| --- | --- | --- |
| Alert | High | Four emails per day |
| Alert | Medium | Two emails per day |
| Alert | Low | One email per day |
| Attack path | Critical | One email per 30 minutes |
| Attack path | High | One email per hour |
| Attack path | Medium | One email per two hours |
| Attack path | Low | One email per three hours |

## Availability

Required roles and permissions: Security Admin, Subscription Owner, or Contributor.

## Customize the email notifications in the portal

You can send email notifications to individuals or to all users with specific Azure roles.

To customize email notifications in the Azure portal:

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Navigate to **Microsoft Defender for Cloud** &gt; **Environment settings**.
3. Select the relevant subscription.
4. Select **email notifications**.
5. Define the recipients for your notifications with one or both of these options:

    - From the dropdown list, select from the available roles.
    - Enter specific email addresses separated by commas. There's no limit to the number of email addresses that you can enter.
6. Select the notification types:

    - **Notify about alerts with the following severity (or higher)** and select a severity level.
    - **Notify about attack paths with the following risk level (or higher)** and select a risk level.
7. Select **Save**.

## Customize the email notifications with an API

You can also manage email notifications through the REST API. For details, see the [Security contacts REST API reference](/en-us/rest/api/defenderforcloud-composite/security-contacts?view=rest-defenderforcloud-composite-latest&amp;preserve-view=true).

This API is an example request body for the PUT request when creating a security contact configuration:

URI: `https://management.azure.com/subscriptions/<SubscriptionId>/providers/Microsoft.Security/securityContacts/default?api-version=2020-01-01-preview`

```json
{
    "properties": {
        "emails": "admin@contoso.com;admin2@contoso.com",
        "notificationsByRole": {
            "state": "On",
            "roles": ["AccountAdmin", "Owner"]
        },
        "alertNotifications": {
            "state": "On",
            "minimalSeverity": "Medium"
        },
        "phone": ""
    }
}
```