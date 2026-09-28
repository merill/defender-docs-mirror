---
layout: Conceptual
title: Configure email alert notifications in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/configure-email-notifications
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Configure email notifications in Microsoft Defender XDR so specified recipients are alerted to new security alerts based on severity and other criteria.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.custom: sfi-ga-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: f4498d32-0e32-5251-3f08-e194bf2b05c1
document_version_independent_id: f4498d32-0e32-5251-3f08-e194bf2b05c1
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/configure-email-notifications.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: configure-email-notifications
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/configure-email-notifications.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: 600ae44e-de3f-8932-5056-c937be948f2d
---

# Configure email alert notifications in Microsoft Defender XDR - Microsoft Defender XDR | Microsoft Learn

You can configure Microsoft Defender XDR to send email notifications to specified recipients for new alerts. This feature enables you to identify a group of individuals who will immediately be informed and can act on alerts based on their severity.

If you're using [Defender for Business](/en-us/defender-business/mdb-overview), you can set up email notifications for specific users (not roles or groups).

Note

- Only users with **Manage security settings** permissions or higher roles can configure email notifications. If you've chosen to use basic permissions management, users with Security Administrator higher roles can configure email notifications.
- Device group creation is supported in Defender for Endpoint Plan 1 and Plan 2.

You can set the alert severity levels that trigger notifications. You can also add or remove recipients of the email notification. New recipients get notified about alerts triggered after they're added. For more information about alerts, see [View and organize the Alerts queue](/en-us/defender-endpoint/alerts-queue).

If you're using role-based access control (RBAC), recipients will only receive notifications based on the device groups that were configured in the notification rule. Users with the proper permission can only create, edit, or delete notifications that are limited to their device group management scope. Only users assigned to the Global administrator role can manage notification rules that are configured for all device groups.

Note

Microsoft recommends using roles with fewer permissions for better security. The Global Administrator role, which has many permissions, should only be used in emergencies when no other role fits.

The email notification includes basic information about the alert and a link to the portal where you can do further investigation.

## Create rules for alert notifications

You can create rules that determine the devices and alert severities to send email notifications for and the notification recipients.

1. Go to the [Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2077139) and sign in using an account with the Security administrator or Global administrator role assigned.
2. In the navigation pane, select **Settings** &gt; **Endpoints** &gt; **General** &gt; **Email notifications**.
3. Click **Add item**.
4. Specify the General information:

    - **Rule name** - Specify a name for the notification rule.
    - **Include organization name** - Specify the customer name that appears on the email notification.
    - **Include tenant-specific portal link** - Adds a link with the tenant ID to allow access to a specific tenant.
    - **Include device information** - Includes the device name in the email alert body.

        Note

        This information might be processed by recipient mail servers that are not in the geographic location you have selected for your Defender data.
    - **Devices** - Choose whether to notify recipients for alerts on all devices (Global administrator role only) or on selected device groups. For more information, see [Create and manage device groups](/en-us/defender-endpoint/machine-groups). (If you're using [Defender for Business](/en-us/defender-business/mdb-overview), device groups do not apply.)
    - **Alert severity** - Choose the alert severity level.
5. Click **Next**.
6. Enter the recipient's email address then click **Add recipient**. You can add multiple email addresses.
7. Check that email recipients can receive the email notifications by selecting **Send test email**.
8. Click **Save notification rule**.

## Edit a notification rule

To edit an existing notification rule, follow these steps:

1. Select the notification rule you'd like to edit.
2. Update the General and Recipient tab information.
3. Click **Save notification rule**.

## Delete a notification rule

To delete a notification rule, follow these steps:

Warning

Deleting a notification rule is permanent. Future email notifications for that rule will stop, and you must recreate the rule if you remove it by mistake.

1. Select the notification rule you'd like to delete.
2. Click **Delete**.

## Troubleshoot email notifications for alerts

The following troubleshooting information covers issues you might encounter when using email notifications for alerts.

**Problem:** Intended recipients report they're not getting the notifications.

**Solution:** Make sure that the notifications aren't blocked by email filters:

1. Check that the email notifications aren't sent to the Junk Email folder. Mark them as Not junk.
2. Check that your email security product isn't blocking the email notifications.
3. Check your email application rules that might be catching and moving your email notifications.