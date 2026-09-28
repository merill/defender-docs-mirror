---
layout: Conceptual
title: Get incident notifications by email - Microsoft Defender XDR | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/defender-xdr/m365d-notifications-incidents
breadcrumb_path: /defender-xdr/breadcrumb/toc.json
permissioned-type: public
feedback_system: Standard
feedback_product_url: https://techcommunity.microsoft.com/t5/microsoft-365-defender/bd-p/MicrosoftThreatProtection
uhfHeaderId: MSDocsHeader-MicrosoftDefender
manager: orspodek
description: Set up email notifications to get notified of new incidents or updates to incidents in the Microsoft Defender portal.
ms.service: defender-xdr
ms.author: guywild
author: guywi-ms
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier1
ms.topic: how-to
ms.date: 2026-07-02T00:00:00.0000000Z
ms.custom: sfi-ga-nochange, msecd-doc-authoring-1016
ai-usage: ai-assisted
locale: en-us
document_id: 96fd580e-3dd8-9287-6967-235fb204f3ea
document_version_independent_id: 96fd580e-3dd8-9287-6967-235fb204f3ea
original_content_git_url: https://github.com/MicrosoftDocs/defender-docs-pr/blob/live/defender-xdr/m365d-notifications-incidents.md
site_name: Docs
depot_name: MSDN.defender-xdr
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: m365d-notifications-incidents
moniker_range_name: 
monikers: []
item_type: Content
source_path: defender-xdr/m365d-notifications-incidents.md
cmProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/c671beaa-a830-4c9f-aceb-97379ee031ca
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/1577a46d-8446-40bd-bfae-0578362f4d94
spProducts:
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/8921374c-4dbe-4ed0-b011-a39e18bfbd98
- https://microsoft-devrel.poolparty.biz/DevRelOfferingOntology/cdf3f22d-5420-4d59-a2bf-66d6b3d9c828
platformId: bd68a828-e030-d720-0d57-70c314d3178b
---

# Get incident notifications by email - Microsoft Defender XDR | Microsoft Learn

Important

Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

You can set up email notifications for your staff to get notified about new incidents or updates to existing incidents. You can choose to get email notifications based on:

- Alert severity
- Alert sources
- Device group

**Choose to receive email notifications only for specific service source**: You can easily select specific service sources that you want to get email notifications for.

**Get more granularity with specific detection sources**: You can get email notifications only for a specific detection source.

**Set the severity per detection or service source**: You can choose to get email notifications only on specific severities for each service source or detection source. For example, you can get notified for Medium and High alerts for EDR and all severities for Microsoft Defender Experts.

The email notification contains important details about the incident like the incident name, severity, and categories, among others. You can also go directly to the incident and start your analysis right away. For more information, see [Investigate incidents](investigate-incidents).

You can add or remove recipients in the email notifications. New recipients get notified about incidents after they're added.

Note

You need the **Manage security settings** permission to configure email notification settings. If you've chosen to use basic permissions management, users with Security Administrator or higher roles can configure email notifications.  Likewise, if your organization is using role-based access control (RBAC), you can only create, edit, delete, and receive notifications based on device groups that you are allowed to manage.

## Create a rule for email notifications

Follow these steps to create a new rule and customize email notification settings.

1. Go to the [Microsoft Defender portal](https://security.microsoft.com). In the navigation pane, select **Settings &gt; Microsoft Defender XDR**, then select **Email notifications** under General.
2. In the **Incidents** tab, select **Add incident notification rule**.
3. On the **Basics** page, type the rule name and a description, and then select **Next**.
4. On the **Notification settings** page, configure:

    - **Alert severity** - Choose the alert severities that triggers an incident notification. For example, if you only want to be informed about high-severity incidents, select **High**.
    - **Device group scope** - You can specify all device groups or select from the list of device groups in your tenant.
    - **Send only one notification per incident** - Select if you want one notification per incident.
    - **Include organization name in the email** - Select if you want your organization name to appear in the email notification.
    - **Include tenant-specific portal link** - Select if you want to add a link with the tenant ID in the email notification for access to a specific Microsoft 365 tenant.

    [![Screenshot of the Notification settings page for incident email notifications in the Microsoft Defender portal.](media/m365d-notifications-incidents/incident-notif-settings-small.png)](media/m365d-notifications-incidents/incident-notif-settings.png#lightbox)
5. Select **Next**. On the **Recipients** page, add the email addresses where the incident notifications are to be sent. Select **Add** after typing each new email address. To test notifications and ensure that the recipients receive them in the inboxes, select **Send test email**.
6. Select **Next**. On the **Review rule** page, review the settings of the rule, and then select **Create rule**. Recipients will start receiving incident notifications through email based on the rule settings you configured.

To edit an existing rule, select it from the list of rules. On the pane with the rule name, select **Edit rule** and make your changes on the **Basics**, **Notification settings**, and **Recipients** pages.

Warning

Deleting a notification rule removes it permanently and can't be undone.

To delete a rule, select it from the list of rules. On the pane with the rule name, select **Delete**.

Once you receive an incident email notification, you can go directly to the incident and start your investigation right away. For more information on investigating incidents, see [Investigate incidents](investigate-incidents).